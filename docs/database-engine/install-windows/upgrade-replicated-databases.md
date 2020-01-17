---
title: レプリケートされたデータベースのアップグレードまたは修正プログラム | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- merge replication database upgrades [SQL Server replication]
- replication [SQL Server], upgrading
- transactional replication, upgrading databases
- snapshot replication [SQL Server], upgrading databases
- upgrading replicated databases
ms.assetid: 9926a4f7-bcd8-4b9b-9dcf-5426a5857116
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 46156a9e7b1180d5ed70f0dbcb6b25d2f608f0fc
ms.sourcegitcommit: 84e6922a57845a629391067ca4803e8d03e0ab90
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72008455"
---
# <a name="upgrade-or-patch-replicated-databases"></a>レプリケートされたデータベースのアップグレードまたは修正プログラム

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] では、レプリケートされたデータベースを以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]からアップグレードすることができます。ノードのアップグレード中は、その他のノードでの操作を停止する必要はありません。 トポロジでサポートされるバージョンに関して、以下の規則が守られていることを確認してください。  
  
-   ディストリビューターは、パブリッシャーのバージョン以上であればどのバージョンでも使用できます (多くの場合、ディストリビューターはパブリッシャーと同じインスタンスです)。    
-   パブリッシャーは、ディストリビューターのバージョン以下であればどのバージョンでも使用できます。    
-   サブスクライバーのバージョンは、次のように、パブリケーションの種類によって異なります。    
    - トランザクション パブリケーションのサブスクライバーは、2 つのパブリッシャー バージョンのうちどちらでも使用できます。 例: SQL Server 2012 (11.x) パブリッシャーでは SQL Server 2014 (12.x) および SQL Server 2016 (13.x) のサブスクライバーを使用でき、SQL Server 2016 (13.x) パブリッシャーでは SQL Server 2014 (12.x) および SQL Server 2012 (11.x) のサブスクライバーを使用できます。     
    - マージ パブリケーションに対するサブスクライバーでは、バージョンのライフ サイクル サポート サイクルに従ってサポートされているパブリッシャー バージョンと等しいかそれより前のすべてのバージョンを使用できます。  
 
SQL Server へのアップグレード パスは、配置のパターンによって異なります。 SQL Server では、2 つの一般的なアップグレード パスが提供されています。
- サイド バイ サイド: 並列環境を配置し、ログインやジョブなどの関連付けられたインスタンス レベル オブジェクトと共に、データベースを新しい環境に移動します。 
- インプレース アップグレード: SQL Server のインストール メディアを使用して、SQL Server のビットを置き換え、データベース オブジェクトをアップグレードすることにより、既存の SQL Server のインストールをアップグレードできます。 Always On 可用性グループまたはフェールオーバー クラスター インスタンスを実行している環境の場合、インプレース アップグレードと[ローリング アップグレード](choose-a-database-engine-upgrade-method.md#rolling-upgrade)を組み合わせると、ダウンタイムが最小限になります。 

レプリケーション トポロジのサイド バイ サイド アップグレードに対して採用されてきた一般的なアプローチは、トポロジ全体を移動するのではなく、パブリッシャーとサブスクライバーのペアを個別に新しいサイド バイ サイド環境に移動するというものです。 この段階的アプローチは、ダウンタイムを管理し、レプリケーションに依存するビジネスの特定の範囲に影響を最小限に抑えるのに役立ちます。  

この記事の多くは、SQL Server のバージョンのアップグレードを対象としています。 ただし、Service Pack または累積更新プログラムで SQL Server を修正するときには、インプレース アップグレード プロセスも同様に使用する必要があります。 

 >[!WARNING]
 > レプリケーション トポロジのアップグレードは、複数のステップから成るプロセスです。 テスト環境でレプリケーション トポロジのレプリカをアップグレードしてみてから、実際の運用環境でアップグレードを実行することをお勧めします。 これは、実際のアップグレード プロセス中に高価で長いダウンタイムを発生させずに、アップグレードを円滑に処理するために必要な運用ドキュメントの問題を解決するのに役立ちます。 レプリケーション トポロジをアップグレードするときに、運用環境で Always On 可用性グループや SQL Server フェールオーバー クラスター インスタンスを使用することで、ダウンタイムが大幅に減った事例があります。 また、アップグレードを試みる前に、MSDB、マスター、ディストリビューション データベースと、レプリケーションに参加しているユーザー データベースを含む、すべてのデータベースのバックアップを行うことをお勧めします。


## <a name="replication-matrix"></a>レプリケーションのマトリックス

[!INCLUDE[repl matrix](../../includes/replication-compat-matrix.md)]
  
## <a name="run-the-log-reader-agent-for-transactional-replication-before-upgrade"></a>アップグレードの前にトランザクション レプリケーション用にログ リーダー エージェントを実行する方法  
 [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] をアップグレードする前に、パブリッシュされたテーブルからコミットされたすべてのトランザクションが、ログ リーダー エージェントによって処理されているかどうかを確認する必要があります。 すべてのトランザクションが処理されたことを確認するには、トランザクション パブリケーションを含んだ各データベースに対して次の手順を実行します。  
  
1.  データベースのログ リーダー エージェントが実行されていることを確認します。 既定では、エージェントは継続的に実行されています。    
2.  パブリッシュされたテーブル上のユーザー アクティビティを停止します。  
3.  トランザクションをディストリビューション データベースにコピーする時間をログ リーダー エージェントに与えてから、エージェントを停止します。  
4.  [sp_replcmds](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) を実行し、すべてのトランザクションが処理されたことを確認します。 この手順の結果セットを空にする必要があります。   
5.  [sp_replflush](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md) を実行し、sp_replcmds から接続を閉じます。   
6.  最新バージョンの [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] へのサーバー アップグレードを実行します。   
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントとログ リーダー エージェントがアップグレードの後に自動的に起動しない場合は、これらを再起動します。  
  
## <a name="run-agents-for-merge-replication-after-upgrade"></a>アップグレード後のマージ レプリケーション用エージェントの実行  
 アップグレード後は、マージ パブリケーションごとにスナップショット エージェントを実行し、サブスクリプションごとにマージ エージェントを実行して、レプリケーション メタデータを更新します。 サブスクリプションを再初期化する必要がないので、新しいスナップショットを適用する必要はありません。 サブスクリプション メタデータは、アップグレード後に最初にマージ エージェントを実行したときに更新されます。 そのため、サブスクリプション データベースは、パブリッシャーのアップグレード中にオンライン状態でアクティブなままにすることができます。  
  
 マージ レプリケーションでは、パブリケーション データベースおよびサブスクリプション データベース内の多数のシステム テーブルに、パブリケーション メタデータおよびサブスクリプション メタデータが格納されます。 スナップショット エージェントを実行すると、パブリケーション メタデータが更新され、マージ エージェントを実行すると、サブスクリプション メタデータが更新されます。 生成が必要なのはパブリケーション スナップショットのみです。 パラメーター化されたフィルターがマージ パブリケーションで使用される場合は、各パーティションにもスナップショットが必要です。 これらのパーティション スナップショットを更新する必要はありません  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、レプリケーション モニター、またはコマンド ラインで各エージェントを実行します。 スナップショット エージェントの実行について詳しくは、次の記事をご覧ください。  
  
-   [初期スナップショットの作成および適用](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)
-   [レプリケーション エージェントを起動および停止する &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)
-   [初期スナップショットの作成および適用](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)
-   [Replication Agent Executables Concepts](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  

マージ エージェントの実行について詳しくは、次の記事をご覧ください。
-   [プル サブスクリプションの同期](../../relational-databases/replication/synchronize-a-pull-subscription.md)
-   [プッシュ サブスクリプションの同期](../../relational-databases/replication/synchronize-a-push-subscription.md)  
  

マージ レプリケーションを使用するトポロジで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をアップグレードした後に、新しい機能を使用する場合は、すべてのパブリケーションのパブリケーション互換性レベルを変更します。  
  
## <a name="upgrading-to-standard-workgroup-or-express-editions"></a>Standard Edition、Workgroup Edition、または Express Edition へのアップグレード  
[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] のいずれかのエディションから別のエディションへアップグレードする前に、現在使用している機能がアップグレード先のエディションでサポートされているかどうかを確認します。 詳細については、[SQL Server の各エディションとサポートされる機能](../../sql-server/editions-and-components-of-sql-server-2017.md)に関するページのレプリケーションのセクションをご覧ください。  

## <a name="steps-to-upgrade-a-replication-topology"></a>レプリケーション トポロジをアップグレードする手順
以下の手順では、レプリケーション トポロジ内のサーバーをアップグレードする順序の概要を示します。 トランザクション レプリケーションまたはマージ レプリケーションのどちらを実行している場合でも、同じ手順が適用されます。 ただし、以下の手順は、ピア ツー ピア レプリケーション、キュー更新サブスクリプション、または即時更新サブスクリプションには適用されません。 

### <a name="in-place-upgrade"></a>一括アップグレード 
1. ディストリビューターを更新します。 
2. パブリッシャーとサブスクライバーを更新します。 これらは、任意の順序でアップグレードできます。 

 >[!NOTE]
 > SQL 2008 および 2008 R2 では、レプリケーション トポロジのマトリックスと一致するように、パブリッシャーとサブスクライバーのアップグレードを同時に行う必要があります。 SQL 2008 または 2008 R2 のパブリッシャーまたはサブスクライバーでは、SQL 2016 (またはそれ以降) のパブリッシャーまたはサブスクライバーを使用できません。 同時にアップグレードできない場合は、中間アップグレードを使用して SQL インスタンスを SQL 2014 にアップグレードした後、再度 SQL 2016 (またはそれ以降) にアップグレードします。  

### <a name="side-by-side-upgrade"></a>サイド バイ サイド アップグレード
1. ディストリビューターを更新します。
1. 新しい SQL Server インスタンスで[ディストリビューション](../../relational-databases/replication/configure-distribution.md)を再構成します。
1. パブリッシャーをアップグレードします。
1. サブスクライバーをアップグレードします。
1. サブスクライバーの再初期化を含めて、すべてのパブリッシャーとサブスクライバーのペアを再構成します。 


## <a name="steps-for-side-by-side-migration-of-the-distributor-to-windows-server-2012-r2"></a>Windows Server 2012 R2 へのディストリビューターのサイド バイ サイド移行の手順
SQL Server インスタンスを SQL Server 2016 (またはそれ以降) にアップグレードしようとしていて、現在の OS が Windows 2008 (または 2008 R2) である場合は、Windows Server R2 以降への OS のサイド バイ サイド アップグレードを実行する必要があります。 この中間 OS アップグレードの理由は、SQL Server 2016 は Windows Server 2008/2008 R2 にインストールできず、Windows Server 2008/20008 R2 では Windows Server 2016 に直接インプレース アップグレードできないためです。 Windows Server 2008/2008 R2 から Windows server 2012 へのインプレース アップグレードを実行してから、Windows Server 2016 にアップグレードすることは可能ですが、ダウンタイムが発生し、複雑さが増してロールバック パスが容易にならないため、通常は推奨されません。 フェールオーバー クラスターに参加している SQL Server インスタンスで使用できるアップグレード パスは、サイド バイ サイド アップグレードだけです。  以下の手順は、スタンドアロン SQL Server インスタンス上、または Always On フェールオーバー クラスター インスタンス (FCI) 内のいずれかで実行できます。

1. Windows Server 2012 R2/2016 上のディストリビューターとして、新しい SQL Server インスタンス (スタンドアロンまたは Always On フェールオーバー クラスター)、エディション、およびバージョンを、異なる Windows クラスターと SQL Server FCI 名またはスタンドアロン ホスト名で設定します。 レプリケーション エージェントの実行可能ファイル、レプリケーション フォルダー、およびデータベース ファイルのパスが、新しい環境でも同じパスで見つかるように、ディレクトリ構造を古いディストリビューターと同じにする必要があります。 これにより、移行/アップグレード後に必要な手順が減ります。
1. レプリケーションが同期されていることを確認した後、すべてのレプリケーション エージェントをシャットダウンします。 
1. 現在の SQL Server ディストリビューター インスタンスをシャットダウンします。 スタンドアロン インスタンスの場合は、サーバーをシャットダウンします。 SQL FCI の場合は、ネットワーク名を含む SQL Server ロール全体を、クラスター マネージャーでオフラインにします。 
1. 古い (現在のディストリビューター インスタンス) 環境用の DNS および AD コンピューター オブジェクトのエントリを削除します。 
1. 古いサーバーと一致するように、新しいサーバーのホスト名を変更します。
    1. SQL FCI の場合は、新しい SQL FCI の名前を古いインスタンスと同じ仮想サーバー名に変更します。 
1. SAN リダイレクト、ストレージ コピー、またはファイル コピーを使用して、以前のインスタンスからデータベース ファイルをコピーします。 
1. 新しい SQL Server インスタンスをオンラインにします。 
1. すべてのレプリケーション エージェントを再起動し、エージェントが正常に動作していることを確認します。
1. アプリケーションが予期したとおりに動作していることを確認します。 
1. SQL Server のセットアップ メディアを使用して、SQL Server の新しいバージョンへの SQL Server インスタンスのインプレース アップグレードを実行します。 


  >[!NOTE]
  > ダウンタイムを減らすため、ディストリビューターの "*サイド バイ サイド移行*" と、"*SQL Server 2016 へのインプレース アップグレード*" を、別のアクティビティとして実行することをお勧めします。 これにより、段階的なアプローチを採用して、リスクを軽減し、ダウンタイムを最小限に抑えることができます。

## <a name="web-synchronization-for-merge-replication"></a>マージ レプリケーションの Web 同期  
 マージ レプリケーションの Web 同期オプションでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーション リスナー (replisapi.dll) を、同期に使用するインターネット インフォメーション サービス (IIS) サーバーの仮想ディレクトリにコピーする必要があります。 Web 同期を構成すると、Web 同期の構成ウィザードにより、ファイルが仮想ディレクトリにコピーされます。 IIS サーバーにインストールされた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントをアップグレードする場合、replisapi.dll を COM ディレクトリから IIS サーバーの仮想ディレクトリへ手動でコピーする必要があります。 Web 同期の構成の詳細については、「 [Web 同期の構成](../../relational-databases/replication/configure-web-synchronization.md)」を参照してください。  
  
## <a name="restoring-a-replicated-database-from-an-earlier-version"></a>以前のバージョンからレプリケートされたデータベースの復元  
 以前のバージョンからレプリケートされたデータベースのバックアップを復元するときにレプリケーション設定が保持されるようにするには、バックアップが作成されたサーバーおよびデータベースと同じ名前のサーバーおよびデータベースに復元します。  
  
## <a name="see-also"></a>参照  
 [SQL Server のレプリケーション](../../relational-databases/replication/sql-server-replication.md)  
 [レプリケーション管理に関する FAQ](../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)   
 [レプリケーションの下位互換性](../../relational-databases/replication/replication-backward-compatibility.md)   
 [サポートされているバージョンとエディションのアップグレード](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [SQL Server のアップグレード](../../database-engine/install-windows/upgrade-sql-server.md)  
 [SQL Server 2016 へのレプリケーション トポロジのアップグレード](https://blogs.msdn.microsoft.com/sql_server_team/upgrading-a-replication-topology-to-sql-server-2016/)
