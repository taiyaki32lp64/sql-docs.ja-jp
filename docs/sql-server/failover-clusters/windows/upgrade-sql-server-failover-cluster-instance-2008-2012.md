---
title: Windows Server 2008/2008 R2/2012 クラスターで実行されている SQL Server インスタンスのアップグレード | Microsoft Docs
ms.date: 01/25/2018
ms.prod: sql
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading failover clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c8825d0d4c8ff0ac6d83b152b8606be6d9fd0cc5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904960"
---
# <a name="upgrade-sql-server-instances-running-on-windows-server-20082008-r22012-clusters"></a>Windows Server 2008/2008 R2/2012 クラスターで実行されている SQL Server インスタンスのアップグレード

[!INCLUDE[nextref-longhorn-md](../../../includes/nextref-longhorn-md.md)]、[!INCLUDE[winserver2008r2-md](../../../includes/winserver2008r2-md.md)]、[!INCLUDE[win8srv-md](../../../includes/win8srv-md.md)] の場合、クラスターで許可される [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のバージョンが制限され、Windows Server フェールオーバー クラスターでオペレーティング システムのインプレース アップグレードを実行できません。 クラスターを [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)] 以上にアップグレードすれば、最新の状態に保つことができます。

## <a name="prerequisites"></a>Prerequisites

-   移行方法のいずれかを実行する前に、Windows Server 2016/2012 R2 で並列 Windows Server フェールオーバー クラスターを準備する必要があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (FCI) を構成するすべてのノードを、並列 FCI がインストールされている Windows クラスターに結合する必要があります。 移行前に、Windows Server フェールオーバー クラスターにスタンドアロン コンピューターを結合することは**できません**。 移行前に、ユーザー データベースを新しい環境で同期する必要があります。
-   対象のすべてのインスタンスは、元の環境の並列インスタンスと同じバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を同じインスタンス名と ID で実行し、同じ機能と共にインストールされる必要があります。 インストール パスとディレクトリ構造は、対象のコンピューターで同じである必要があります。 これには FCI 仮想ネットワーク名は含まれません。移行前は、この名前は異なっている必要があります。 元のインスタンスで有効になっているすべての機能 (Always On、FILESTREAM など) は、対象のインスタンスでも有効にする必要があります。

-   移行前に、並列クラスターに [!INCLUDE[sshadrc-md](../../../includes/sshadrc-md.md)]をインストールする必要はありません。

-   (SQL FCI の有無に関係なく) 厳密に可用性グループを使用するクラスターの移行時のダウンタイムは、分散型可用性グループを使用して大幅に制限できます。ただし、その場合、すべてのインスタンスで [!INCLUDE[sssql15-md](../../../includes/sssql15-md.md)] RTM (以上) のバージョンを実行する必要があります。

-   すべての移行方法で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sysadmin ロールが必要になります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスで使用されるすべての Windows ユーザー (つまり、レプリケーション エージェントを実行している Windows アカウント) には、新しい環境内の各コンピューターに対する OS レベルのアクセス許可が必要です。

-   元の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] クラスター環境で使用されているネットワーク ファイル共有とネットワークで割り当てられたドライブは引き続き存在する必要があり、元のインスタンスと同じアクセス許可でターゲット クラスターからアクセスできる必要があります。

-   元の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスでリッスンされる TCP/IP ポートは未使用である必要があり、ターゲット コンピューターでの受信トラフィックを許可する必要があります。
-   SQL 関連のサービスをすべてインストールし、同じ Windows ユーザーが実行する必要があります。

-   対象のインスタンスは、元のインスタンスと同じロケールでインストールする必要があります。

## <a name="migration-scenarios"></a>移行シナリオ

適切な移行方法は、元の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] クラスター トポロジの特定のパラメーター (つまり、[!INCLUDE[sshadrc-md](../../../includes/sshadrc-md.md)] と SQL フェールオーバー クラスター インスタンスの使用) によって異なります。 選択する方法は対象環境の要件によっても異なります。 新しい環境で、各コンピューターまたは SQL FCI が元の仮想ネットワーク名 (VNN) を維持する必要があるか、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] トポロジが、元のインスタンスのシステム オブジェクトをすべて継承する新しいインスタンスに依存する場合は、これらを移行する方法を選択する必要があります。

|                                   | すべてのサーバー オブジェクトと VNN が必要 | すべてのサーバー オブジェクトと VNN が必要 | サーバー オブジェクト/VNN は不要\* | サーバー オブジェクト/VNN は不要\* |
|-----------------------------------|--------------------------------------|--------------------------------------------------------------------|------------|------------|
| **_可用性グループ(Y/N_)**                  | **_Y_**                              | **_N_**                                                            | **_Y_**    | **_N_**    |
| **クラスターで SQL FCI のみを使用**         | [シナリオ 3](#scenario-3-windows-cluster-has-both-sql-fcis-and-sql-server-availability-groups)                           | [シナリオ 2](#scenario-2-windows-clusters-with-sql-server-failover-cluster-instances-fcis)                                                        | [シナリオ 1](#scenario-1-windows-cluster-with-sql-server-availability-groups-and-no-failover-cluster-instances-fcis) | [シナリオ 2](#scenario-2-windows-clusters-with-sql-server-failover-cluster-instances-fcis) |
| **クラスターでスタンドアロン インスタンスを使用** | [シナリオ 5](#scenario-5-windows-cluster-with-standalone-sql-server-instances-and-availability-groups)                           | [シナリオ 4](#scenario-4-windows-cluster-with-standalone-sql-server-instances-and-no-availability-groups)                                                         | [シナリオ 1](#scenario-1-windows-cluster-with-sql-server-availability-groups-and-no-failover-cluster-instances-fcis) | [シナリオ 4](#scenario-4-windows-cluster-with-standalone-sql-server-instances-and-no-availability-groups) |

\* 可用性グループ リスナー名を除く

## <a name="scenario-1-windows-cluster-with-sql-server-availability-groups-and-no-failover-cluster-instances-fcis"></a>シナリオ 1:SQL Server 可用性グループを使用する、フェールオーバー クラスター インスタンス (FCI) のない Windows クラスター
可用性グループ (AG) を使用する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップの場合、Windows Server 2016/2012 R2 とは異なる Windows クラスターに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の並列配置を作成することで新しいクラスターに移行できます。 その後、ターゲット クラスターが現在の運用クラスターに対してセカンダリとなる分散型 AG を作成できます。 その場合、ユーザーは [!INCLUDE[sssql15-md](../../../includes/sssql15-md.md)] 以降にアップグレードする必要があります。

###  <a name="to-perform-the-upgrade"></a>アップグレードを実行するには

1.  必要に応じて、すべてのインスタンスを [!INCLUDE[sssql15-md](../../../includes/sssql15-md.md)] 以降にアップグレードします。 並列インスタンスは、同じバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を実行する必要があります。

2.  ターゲット クラスターの可用性グループを作成します。 ターゲット クラスターのプライマリ ノードが FCI でない場合は、リスナーを作成します。

3.  ターゲット クラスターがセカンダリ可用性グループとなる分散型可用性グループを形成します。

    >[!NOTE]
    >分散型 AG T-SQL の作成の LISTENER\_URL パラメーターの動作は、プライマリ インスタンスとして SQL FCI を使用する AG では異なります。 これがプライマリまたはセカンダリ AG のいずれかの場合、データベース ミラーリング エンドポイントのポートと共に、リスナーのネットワーク名の代わりに、リスナー URL としてプライマリ SQL FCI の VNN を使用します。

4.  セカンダリ可用性グループを分散型 AG に結合します。

5.  セカンダリ AG のセカンダリ データベースを結合します。

    >[!NOTE]
    >ターゲット可用性グループで自動シード処理を使用する場合、これは自動で行われます。これは、データとログのパスがすべてのレプリカで同じである場合にのみ可能です。

6.  プライマリ AG へのトラフィックをすべて切断し、セカンダリでの同期を許可します。

7.  両方の可用性グループのコミット ポリシーを SYNCHRONOUS_COMMIT に変更し、状態が SYNCHRONIZED になったらターゲット クラスターにフェールオーバーします。

8.  分散型 AG を削除します。

9.  元の AG のリスナーを削除するか、名前を変更します。

10. 名前を変更するか、元の AG のリスナー名の名前を使用して新しい AG のリスナーを作成します。

    >[!NOTE]
    >元の AG リスナーの DNS レコードが存在している間は、この名前を使用してリスナーを作成しようとすると失敗します。

11. リスナーに対するトラフィックを再開します。

## <a name="scenario-2-windows-clusters-with-sql-server-failover-cluster-instances-fcis"></a>シナリオ 2: SQL Server フェールオーバー クラスター インスタンス (FCI) を使用する Windows クラスター

SQL FCI インスタンスのみを使用する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 環境の場合、Windows Server 2016/2012 R2 とは異なる Windows クラスターに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の並列環境を作成することで、新しいクラスターに移行できます。 古い SQL FCI の VNN を "スティール" して、それらを新しいクラスターで取得することで、ターゲット クラスターに移行します。 これにより、DNS の伝達時間に応じて、追加のダウンタイムが作成されます。

###  <a name="to-perform-the-upgrade"></a>アップグレードを実行するには

1.  完全バックアップを取得して、元の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] クラスターに対するトラフィックを停止します。

2.  ユーザー データベースのログ末尾バックアップを取得し、新しい環境で RECOVERY を指定して復元します。

3.  ターゲット クラスターのフェールオーバー クラスター マネージャーで、各 SQL FCI のクラスター化されたロールを停止します。

4.  引き続き、ターゲット クラスターのフェールオーバー クラスター マネージャーで、各 SQL FCI で使用されるクラスター ディスクを元に戻します。

5.  元のクラスターのフェールオーバー クラスター マネージャーで、各 SQL FCI のクラスター化されたロールを停止します。

6.  引き続き、元のクラスターのフェールオーバー クラスター マネージャーで、各 SQL FCI で使用されるクラスター ディスクを元に戻します。

7.  システム データベースを元のコンピューターからその並列ターゲット コンピューターにコピーします。

8.  元の環境のフェールオーバー クラスター マネージャーで、各 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI ロールの 'Server Name' リソースの名前を変更します。

9.  この時点で、各 SQL FCI ロールの名前を変更した Server Name リソースのみをオンラインに戻します。

10. この時点で、ターゲット クラスターのフェールオーバー クラスター マネージャーで、元のクラスターで以前保持されていた [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI ロールの "Server Name" リソースの名前をそれぞれ変更します。

    >[!NOTE]
    >名前が別のコンピューターで既に保持されている場合、その名前の DNS レコードが削除されると、エラーが発生して停止します。

11. すべての FCI の名前が変更されたら、新しいクラスター内の各コンピューターを再起動します。

12. コンピューターが再起動後にオンラインに戻ったら、フェールオーバー クラスター マネージャーで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI ロールをそれぞれ開始します。

## <a name="scenario-3-windows-cluster-has-both-sql-fcis-and-sql-server-availability-groups"></a>シナリオ 3: SQL FCI と SQL Server 可用性グループの両方を含む Windows クラスター

1 つ以上の可用性グループに含まれる、SQL FCI のみを使用し、スタンドアロン [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを使用しない [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップがある場合、"可用性グループなし、スタンドアロン インスタンスなし" のシナリオと同様の方法を使用して、新しいクラスターにこれを移行することができます。 ターゲットの FCI 共有ディスクにシステム テーブルをコピーする前に、元の環境ですべての可用性グループを削除する必要があります。 すべてのデータベースがターゲット コンピューターに移行された後、同じスキーマとリスナーの名前で可用性グループを再作成します。 これにより、Windows Server フェールオーバー クラスター リソースがターゲット クラスターで正しく形成され、管理されます。 **Always On は、移行前にターゲット環境内の各コンピューターの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーで有効にする必要があります。**

### <a name="to-perform-the-upgrade"></a>アップグレードを実行するには

1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に対するトラフィックを停止します。

2.  ユーザー データベースのログ末尾バックアップを取得し、新しい環境の対象のプライマリで RECOVERY を指定して復元します。この場合、対象のすべてのセカンダリでは NORECOVERY を指定します。

3.  ターゲット クラスターのフェールオーバー クラスター マネージャーで、各 SQL FCI のクラスター化されたロールを停止します。

4.  引き続き、ターゲット クラスターのフェールオーバー クラスター マネージャーで、各 SQL FCI で使用されるクラスター ディスクを元に戻します。

5.  元のクラスターで、可用性グループを削除します。

6.  元のクラスターのフェールオーバー クラスター マネージャーで、各 SQL FCI のクラスター化されたロールを停止します。

7.  引き続き、元のクラスターのフェールオーバー クラスター マネージャーで、各 SQL FCI で使用されるクラスター ディスクを元に戻します。

8.  システム データベースを元のコンピューターからその並列ターゲット コンピューターにコピーします。

9.  元の環境のフェールオーバー クラスター マネージャーで、各 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI ロールの 'Server Name' リソースの名前を変更します。

10. この時点で、各 SQL FCI ロールの名前を変更した Server Name リソースのみをオンラインに戻します。

11. この時点で、ターゲット クラスターのフェールオーバー クラスター マネージャーで、元のクラスターで以前保持されていた [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI ロールの "Server Name" リソースの名前をそれぞれ変更します。

12. すべての FCI の名前が変更されたら、新しいクラスター内の各コンピューターを再起動します。

13. コンピューターが再起動後にオンラインに戻ったら、フェールオーバー クラスター マネージャーで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI ロールをそれぞれ開始します。

14. すべてのインスタンスがオンラインになったら、データベースが RECOVERY を指定して復元されたレプリカで可用性グループを形成します。

15. すべてのセカンダリ レプリカを AG に結合し、すべてのセカンダリ データベースを AG に結合します。

16. 元の可用性グループのリスナーのリスナー名を使用して、新しい AG にリスナーを作成します。

## <a name="scenario-4-windows-cluster-with-standalone-sql-server-instances-and-no-availability-groups"></a>シナリオ 4: スタンドアロン SQL Server インスタンスを使用する、可用性グループのない Windows クラスター

スタンドアロン インスタンスのクラスターの移行は、FCI のみの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] クラスターの移行プロセスと似ていますが、FCI のネットワーク名クラスター リソースの VNN を変更するのではなく、元のスタンドアロン コンピューターのコンピューター名を変更し、ターゲット コンピューターの古いコンピューター名を "スティール" します。 古いコンピューターのネットワーク名を取得するまでは、WSFC にターゲットのスタンドアロン コンピューターを結合できないため、これによりスタンドアロンなしのシナリオに関するダウンタイムが増えます。

###  <a name="to-perform-the-upgrade"></a>アップグレードを実行するには

1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に対するトラフィックを停止します。

2.  ユーザー データベースのログ末尾バックアップを取得し、各コンピューターの新しい環境で RECOVERY を指定して復元します。

3.  ターゲット クラスターのフェールオーバー クラスター マネージャーで、各 SQL FCI のクラスター化されたロールを停止します。

4.  引き続き、ターゲット クラスターのフェールオーバー クラスター マネージャーで、各 SQL FCI で使用されるクラスター ディスクを元に戻します。

5.  元のクラスターのフェールオーバー クラスター マネージャーで、各 SQL FCI のクラスター化されたロールを停止し、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] スタンドアロン インスタンスを停止します。

6.  元のクラスター内のスタンドアロン コンピューターごとに、各コンピューターの名前を新しい一意のコンピューター名に変更します。 指示に従って、これらのコンピューターをそれぞれ再起動します。

7.  元のクラスターのフェールオーバー クラスター マネージャーで、各 SQL FCI で使用されるクラスター ディスクを元に戻します。

8.  システム データベースをターゲット コンピューターにコピーします。

9.  元の環境のフェールオーバー クラスター マネージャーで、各 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI ロールの 'Server Name' リソースを新しい一意の名前に変更します。

10. この時点で、各 SQL FCI ロールの名前を変更した Server Name リソースのみをオンラインに戻します。

11. この時点で、並列スタンドアロン インスタンスで、コンピューターの名前を元のスタンドアロン コンピューター名に変更します (古いサーバー名を削除し、ローカル パラメーターを使用して新しいサーバー名を追加します)。指示に従って、コンピューターを再起動します。

12. 再起動後に、各スタンドアロン コンピューターをターゲットの Windows Server フェールオーバー クラスターに結合します。

13. この時点で、ターゲット クラスターのフェールオーバー クラスター マネージャーで、元のクラスターで以前保持されていた [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI ロールの "Server Name" リソースの名前をそれぞれ変更します。

14. すべての FCI の名前が変更されたら、新しいクラスター内の各コンピューターを再起動します。

15. コンピューターが再起動後にオンラインに戻ったら、フェールオーバー クラスター マネージャーで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI ロールをそれぞれ開始します。

## <a name="scenario-5-windows-cluster-with-standalone-sql-server-instances-and-availability-groups"></a>シナリオ 5: スタンドアロン SQL Server インスタンスを使用し、可用性グループを含む Windows クラスター

スタンドアロン レプリカを含む可用性グループを使用するクラスターの移行は、可用性グループを使用する FCI を含むクラスターの移行プロセスと似ています。 ここでも、元の可用性グループを削除して、ターゲット クラスターで再構築する必要があります。ただし、スタンドアロン インスタンスの移行には追加コストがかかるため、ダウンタイムが増えます。 **Always On は、移行前にターゲット環境内の各 FCI で有効にする必要があります。**

###  <a name="to-perform-the-upgrade"></a>アップグレードを実行するには

1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に対するトラフィックを停止します。

2.  ユーザー データベースのログ末尾バックアップを取得して、対象のプライマリの新しい環境で RECOVERY を指定して復元します。この場合、対象の各セカンダリでは NORECOVERY を指定します。

3.  元のクラスターで可用性グループを削除します。

4.  ターゲット クラスターのフェールオーバー クラスター マネージャーで、各 SQL FCI のクラスター化されたロールを停止します。

5.  引き続き、ターゲット クラスターのフェールオーバー クラスター マネージャーで、各 SQL FCI で使用されるクラスター ディスクを元に戻します。

6.  元のクラスターのフェールオーバー クラスター マネージャーで、各 SQL FCI のクラスター化されたロールを停止し、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] スタンドアロン インスタンスを停止します。

7.  元のクラスター内のスタンドアロン コンピューターごとに、各コンピューターの名前を新しい一意のコンピューター名に変更します。 指示に従って、これらのコンピューターをそれぞれ再起動します。

8.  元のクラスターのフェールオーバー クラスター マネージャーで、各 SQL FCI で使用されるクラスター ディスクを元に戻します。

9.  システム データベースをターゲット コンピューターにコピーします。

10. 元の環境のフェールオーバー クラスター マネージャーで、各 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI ロールの 'Server Name' リソースを新しい一意の名前に変更します。

11. この時点で、各 SQL FCI ロールの名前を変更した Server Name リソースのみをオンラインに戻します。

12. この時点で、並列スタンドアロン インスタンスで、コンピューターの名前を元のスタンドアロン コンピューター名に変更します (SQL のサーバー名を削除して追加します)。指示に従って、コンピューターを再起動します。

13. 再起動後に、各スタンドアロン コンピューターをターゲットの Windows Server フェールオーバー クラスターに結合します。

14. この時点で、ターゲット クラスターのフェールオーバー クラスター マネージャーで、元のクラスターで以前保持されていた [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI ロールの "Server Name" リソースの名前をそれぞれ変更します。

15. すべての FCI の名前が変更されたら、新しいクラスター内の各コンピューターを再起動します。

16. コンピューターが再起動後にオンラインに戻ったら、フェールオーバー クラスター マネージャーで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI ロールをそれぞれ開始します。

17. すべてのインスタンスがオンラインになったら、対象のプライマリで可用性グループを再作成します。

18. 各セカンダリ レプリカとセカンダリ データベースを結合します。

19. 元のものと同じ名前で可用性グループ リスナーを再作成します。

## <a name="specific-concerns-for-individual-features"></a>各機能の特定の問題

### [!INCLUDE[sshadrc-md](../../../includes/sshadrc-md.md)]

-   **データベース ミラーリング エンドポイント**

    SQL の観点から、データベース ミラーリング エンドポイントは、システム テーブルと共に新しい [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスに移行されます。 移行前に、ファイアウォールで適切なルールが適用されており、他のプロセスが同じポートでリッスンしていないことを確認してください。

-   **可用性グループ**

    可用性グループとそのリスナーをインスタンス間で移行することはできません。 可用性グループで作成された Windows Server フェールオーバー クラスター リソースを、ターゲット環境で簡単に再作成することはできません。 可用性グループの移行を試みるのではなく、ここでは可用性グループを削除し、ターゲット クラスターで再作成することを試みます。

-   **可用性グループ リスナー**

    可用性グループ自体と同じように、リスナーを直接移行するのではなく、削除してから再作成します。

### <a name="replication"></a>レプリケーション

-   **リモート ディストリビューター、パブリッシャー、サブスクライバー**

    ディストリビューターとパブリッシャーとの関係は、これら 2 つをホストするコンピューターの VNN のみに依存します。これにより、新しいコンピューターに適切に解決されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント ジョブもシステム テーブルと共に適切に移行されるため、さまざまなレプリケーション エージェントで通常どおり実行を継続できます。 移行するには、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント自体または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント ジョブを実行する Windows アカウントに、ターゲット環境での同じアクセス許可が必要になります。 パブリッシャーとサブスクライバーの両方との通信は通常どおり実行されます。

-   **[スナップショット フォルダー]**

    移行するには、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 機能で使用されるネットワーク共有に、元の環境と同じアクセス許可でターゲット環境内のコンピューターからアクセスできる必要があります。 移行前に、アクセスできることを確認する必要があります。

### <a name="service-broker"></a>Service Broker

-   **Service Broker エンドポイント**

    [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の観点から、エンドポイントに関する問題はありません。 移行前に、同じポートで既にプロセスがリッスンしていないことと、ファイアウォール ルールでそのポートがブロックされていないこと、あるいはポートを特に許可するファイアウォール ルールがあることを確認する必要があります。

-   **証明書**

    証明書をバックアップし、新しいコンピューターにその証明書を復元する必要がある場合にターゲット コンピューターに復元する必要もあります。

-   **ルート**

    ルートはターゲットの仮想ネットワーク名によって異なります。これにより、コンピューター名と SQL FCI ネットワーク名の両方が、新しい環境内の正しいコンピューターに適切に解決されます。 参照される他の VNN を新しいコンピューターにリダイレクトする必要もあります。

-   **リモート サービス バインド**

    リモート サービス バインドを使用するすべてのユーザーが適切に移行すると、移行後にリモート サービス バインドは意図したとおりに機能します。

### <a name="includessnoversionincludesssnoversion-mdmd-agent"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント

-   **ジョブ**

    ジョブは、システム データベースと共に適切に移行されます。 SQL エージェント ジョブまたは SQL エージェント自体を実行するすべてのユーザーは、ターゲット コンピューターに対して、前提条件で指定されているものと同じアクセス許可を持つことになります。

-   **アラートと演算子**

    アラートと演算子は、システム データベースと共に適切に移行されます。

### <a name="filestream"></a>FILESTREAM

-   **Windows ファイル共有ポート**

    Windows ファイル共有ポートの 139 と 445 の両方に、受信トラフィックでの FILESTREAM の使用を許可するルールが必要です。

-   **Windows 共有**

    Windows 共有パスは、`\\ServerName\ShareName` でアクセスされるため、SQL FCI 名リソースに依存します。 FILESTREAM を移行するには、ターゲット FCI のすべてのノードで FILESTREAM を有効にする必要があります。また、Windows 共有を使用する場合は、元のコンピューターと同じ Windows 共有名を使用するように構成する必要があります。 ターゲット FCI は、正しいサーバー名を取得すると、必要なパスを使用して Windows 共有をホストします。

-   **FILESTREAM データ**

    FILESTREAM データはバックアップに含まれます。

### <a name="integration-services"></a>Integration Services

-   **SSIS プロジェクト**

    SSIS プロジェクトは SSIS データベースと共に移行されます。 SSIS データベースが移動されると、システム テーブルを移動する直前にパッケージが実行可能となります。

-   **ファイルベースのデータ ソース**

    フラット ファイル、Excel ファイル、XML ソースなどには、SSIS パッケージで指定されたのと同じ場所からアクセスできる必要があります。

## <a name="next-steps"></a>次の手順
- [データベース エンジンのアップグレードの完了](../../../database-engine/install-windows/complete-the-database-engine-upgrade.md)
- [データベース互換性モードの変更とクエリ ストアの使用](../../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)
- [SQL Server 2016 の新機能を利用する](https://msdn.microsoft.com/library/d8879659-8efa-4442-bcbb-91272647ae16)
- [SQL Server フェールオーバー クラスター インスタンスのアップグレード](upgrade-a-sql-server-failover-cluster-instance.md)
- [SQL Server セットアップ ログ ファイルの表示と読み取り](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)
- [SQL Server 2016 のインスタンスへの機能の追加 (セットアップ)](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)
