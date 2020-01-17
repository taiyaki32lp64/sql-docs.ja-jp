---
title: フェールオーバー クラスターのトラブルシューティング | Microsoft Docs
ms.custom: ''
ms.date: 10/21/2015
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- troublshooting, failover clustering
- failover clustering, troubleshooting
- cluster troubleshooting
ms.assetid: 84012320-5a7b-45b0-8feb-325bf0e21324
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e1cf8ea99cac00670bd96437e0a5484d2888cbe9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044792"
---
# <a name="failover-cluster-troubleshooting"></a>フェールオーバー クラスターのトラブルシューティング
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、次の問題について説明します。  
  
-   基本的なトラブルシューティング手順  
  
-   フェールオーバー クラスター障害からの復旧  
  
-   フェールオーバー クラスタリングに関する一般的な問題の解決  
  
-   拡張ストアド プロシージャおよび COM オブジェクトの使用  
  
## <a name="basic-troubleshooting-steps"></a>基本的なトラブルシューティング手順  
 診断の最初の手順では、新しいクラスターの検証チェックを実行します。 検証の詳細については、[フェールオーバー クラスターのステップ バイ ステップ ガイド: フェールオーバー クラスターのハードウェアの検証](https://technet.microsoft.com/library/cc732035.aspx)に関する記事を参照してください。  これは、オンラインのクラスター リソースに影響しないため、サービスを中断することなく実行できます。 フェールオーバー クラスタ リング機能をインストールしたら、クラスターの展開前、クラスターの作成中、クラスターの実行中を含め、いつでも検証を実行することができます。 実際には、クラスターの使用中に、可用性の高いワークロードのベスト プラクティスに従っているかどうかをチェックする追加テストも実行されます。 数十回のテストのうち数回は、実行中のクラスターのワークロードに影響しますが、これらはすべてストレージ カテゴリ内にあるため、このカテゴリ全体をスキップすると、簡単に中断を伴うテストを回避できます。  
フェールオーバー クラスタ リングには、検証でストレージ テストを実行する際の偶発的なダウンタイムを回避する組み込みのセーフガードが付属しています。 検証の開始時にクラスターにオンライン グループが含まれており、ストレージ テストが選択されたままになっていると、すべてのテストを実行する (この場合、ダウンタイムが発生します) か、ダウンタイムを避けるためにすべてのオンライン グループのディスクのテストをスキップするかを確認するプロンプトが表示されます。 ストレージ カテゴリ全体をテスト対象から除外すると、このプロンプトは表示されません。 これにより、ダウンタイムなしのクラスターの検証が有効になります。  
  
#### <a name="how-to-revalidate-your-cluster"></a>クラスターを再検証する方法  
  
1.  フェールオーバー クラスター スナップインのコンソール ツリーで、 **[フェールオーバー クラスター管理]** が選択されていることを確認し、 **[管理]** の **[構成の検証]** をクリックします。  
  
2.  ウィザードの指示に従って、サーバーとテストを指定し、テストを実行します。 テストの実行後、 **[概要]** ページが表示されます。  
  
3.  **[概要]** ページで **[レポートの表示]** をクリックしてテスト結果を表示します。  
  
     ウィザードを閉じた後にテスト結果を表示するには、 **%SystemRoot%\Cluster\Reports\Validation Report date and time.html** を参照してください。 **%SystemRoot%** はオペレーティング システムがインストールされているフォルダーです (たとえば、 **C:\Windows**)。  
  
4.  結果の解釈に役立つヘルプ トピックを表示するには、 **[クラスター検証テストの詳細]** をクリックします。  
  
 ウィザードを閉じた後にクラスター検証のヘルプ トピックを表示するには、フェールオーバー クラスター スナップインで **[ヘルプ]** 、 **[ヘルプ トピック]** 、 **[コンテンツ]** タブの順にクリックし、フェールオーバー クラスター ヘルプのコンテンツを展開して、 **[フェールオーバー クラスター構成の検証]** をクリックします。  検証ウィザードが完了すると、 **[概要レポート]** に結果が表示されます。 すべてのテスト結果が緑色のチェック マーク、または場合によっては黄色の三角形 (警告) になる必要があります。 問題の領域 (赤色の X 印または黄色の疑問符) がないかどうかを調べるには、テスト結果を要約したレポートで個々のテストをクリックして、詳細を確認します。 赤色の X 印の問題は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の問題のトラブルシューティングより前に解決する必要があります。  
  
 **更新プログラムをインストールする**  
  
 更新プログラムのインストールは、システムの問題を防ぐために重要です。 役に立つリンク:  
  
-   [Windows Server 2012 R2 ベースのフェールオーバー クラスターの推奨される修正プログラムと更新プログラム](https://support.microsoft.com/kb/2920151)  
  
-   [Windows Server 2012 ベースのフェールオーバー クラスターの推奨される修正プログラムと更新プログラム](https://support.microsoft.com/kb/2784261)  
  
-   [Windows Server 2008 R2 ベースのフェールオーバー クラスターの推奨される修正プログラムと更新プログラム](https://support.microsoft.com/kb/980054)  
  
-   [Windows Server 2008 ベースのフェールオーバー クラスターの推奨される修正プログラムと更新プログラム](https://support.microsoft.com/kb/957311)  
  
## <a name="recovering-from-failover-cluster-failure"></a>フェールオーバー クラスター障害からの復旧  
 フェールオーバー クラスター障害の一般的な原因は、次の 2 つのいずれかです。  
  
-   2 ノード クラスターのいずれかのノードでハードウェア障害が発生しています。 このハードウェア障害は、SCSI カードまたはオペレーティング システムの障害によって発生する可能性があります。  
  
     この障害から復旧するには、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップ プログラムを使用して、障害が発生したノードをフェールオーバー クラスターから削除し、コンピューターをオフラインにしてハードウェアの障害を処置し、コンピューターを再び起動します。その後、修復されたノードをフェールオーバー クラスター インスタンスに追加します。  
  
     詳細については、「[新しい SQL Server フェールオーバー クラスターの作成 &#40;セットアップ&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)」および「[フェールオーバー クラスター インスタンス障害からの復旧](../../../sql-server/failover-clusters/windows/recover-from-failover-cluster-instance-failure.md)」を参照してください。  
  
-   オペレーティング システムの障害が発生しています。 このときノードはオフラインになりますが、復旧不可能なほどには破損していません。  
  
     オペレーティング システムの障害から復旧するには、ノードを復旧してフェールオーバーをテストします。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスのフェールオーバーが正しく行われない場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップ プログラムを使用してフェールオーバー クラスターから [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を削除し、必要な修復を行い、コンピューターを再び起動します。その後、修復されたノードをフェールオーバー クラスター インスタンスに追加する必要があります。  
  
     この方法でオペレーティング システムの障害から復旧すると、時間がかかる場合があります。 オペレーティング システムの障害から簡単に復旧できる場合には、この方法は使用しないでください。  
  
     詳細については、「[新しい SQL Server フェールオーバー クラスターの作成 &#40;セットアップ&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)」と「[How to: Recover from Failover Cluster Failure in Scenario 2](recover-from-failover-cluster-instance-failure.md)」 (方法: シナリオ 2 でフェールオーバー クラスター障害から復旧する) を参照してください。  
  
## <a name="resolving-common-problems"></a>一般的な問題の解決  
 次に、一般的な使用上の問題とその解決策を示します。  
  
### <a name="problem-incorrect-use-of-command-prompt-syntax-to-install-sql-server"></a>問題: SQL Server をインストールするコマンド プロンプト構文の使用方法が正しくない  
 **問題点 1:** コマンド プロンプトで **/qn** スイッチを使用すると、 **/qn** スイッチによりすべてのセットアップのダイアログ ボックスとエラー メッセージが表示されなくなるため、セットアップの問題を診断することが難しくなります。 **/qn** スイッチを指定すると、エラー メッセージを含むすべてのセットアップ メッセージがセットアップ ログ ファイルに書き込まれます。 ログ ファイルの詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」を参照してください。  
  
 **解決策 1**: **/qn** スイッチの代わりに **/qb** スイッチを使用します。 **/qb** スイッチを使用すると、各ステップでは、エラー メッセージなどの基本的な UI が表示されます。  
  
### <a name="problem-sql-server-cannot-log-on-to-the-network-after-it-migrates-to-another-node"></a>問題: SQL Server を別のノードに移行した後、ネットワークにログオンできない  
 **現象 1** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントがドメイン コントローラーと通信できません。  
  
 **解決策 1**: アダプターの障害や DNS の問題など、ネットワークに関する問題の兆候をイベント ログで確認します。 ドメイン コントローラーに対して ping を実行できることを確認します。  
  
 **現象 2** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントのパスワードがすべてのクラスター ノードで同一でないか、障害が発生したノードから移行した [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスがノードで再起動されません。  
  
 **解決策 2:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントのパスワードを変更します。 この操作を行わず、1 つのノードで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントのパスワードを変更した場合、他のすべてのノードでもパスワードを変更する必要があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーを使用すると、この操作が自動的に行われます。  
  
### <a name="problem-sql-server-cannot-access-the-cluster-disks"></a>問題: SQL Server がクラスター ディスクにアクセスできない  
 **問題点 1:** すべてのノードのファームウェアまたはドライバーが更新されていません。  
  
 **解決策 1:** すべてのノードで正しいファームウェアのバージョンおよび同じドライバーのバージョンを使用していることを確認します。  
  
 **問題点 2:** ノードでは、ドライブ文字が異なる共有クラスター ディスクで、障害が発生したノードから移行したクラスター ディスクを復旧できません。  
  
 **解決策 2:** クラスター ディスクのディスク ドライブ文字は、両方のサーバーで同じである必要があります。 同じでない場合は、オペレーティング システムおよび MSCS ( [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Cluster Service) の初期のインストール状態を確認してください。  
  
### <a name="problem-failure-of-a-sql-server-service-causes-failover"></a>問題: SQL Server サービスの障害によりフェールオーバーが発生する  
 **解決方法:** 特定のサービスの障害による [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] グループのフェールオーバーを回避するには、Windows のクラスター アドミニストレーターを使用してサービスを次のように構成します。  
  
-   **[フルテキストのプロパティ]** ダイアログ ボックスの **[詳細設定]** タブで、 **[グループに適用する]** チェック ボックスをオフにします。 ただし、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によりフェールオーバーが発生した場合は、フルテキスト検索サービスが再起動します。  
  
### <a name="problem-sql-server-does-not-start-automatically"></a>問題: SQL Server が自動的に起動しない  
 **解決方法:** フェールオーバー クラスターを自動的に起動するには、MSCS でクラスター アドミニストレーターを使用します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスは手動で開始するように設定されています。クラスター アドミニストレーターは MSCS で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスを開始するように構成されています。 詳細については、「 [サービスの管理](https://msdn.microsoft.com/library/ms178096\(v=sql.105\).aspx)」を参照してください。  
  
### <a name="problem-the-network-name-is-offline-and-you-cannot-connect-to-sql-server-using-tcpip"></a>問題: ネットワーク名がオフラインで、SQL Server に TCP/IP で接続できない  
 **問題点 1:** DNS 必須に設定されているクラスター リソースで DNS が失敗します。  
  
 **解決策 1:** DNS の問題を修正します。  
  
 **問題点 2:** ネットワーク上に重複する名前があります。  
  
 **解決策 2:** NBTSTAT を使用して重複する名前を検索し、問題を修正します。  
  
 **現象 3** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の接続に名前付きパイプが使用されていません。  
  
 **解決策 3:** 名前付きパイプで接続するには、SQL Server 構成マネージャーを使用して別名を作成し、適切なコンピューターに接続します。 たとえば、2 つのノード (**Node A** および **Node B**) から成るクラスター、および既定のインスタンスを使用するフェールオーバー クラスター インスタンス (**Virtsql**) がある場合、次の手順に従って、オフラインのネットワーク名リソースがあるサーバーに接続できます。  
  
1.  クラスター アドミニストレーターを使用して、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを含むグループが実行されているノードを特定します。 この例では、 **Node A**です。  
  
2.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] net start **を使用して、そのコンピューターの**サービスを開始します。 **net start**の使用方法については、「 [手動による SQL Server の起動](https://msdn.microsoft.com/library/ms191193\(v=sql.105\).aspx)」を参照してください。  
  
3.  **Node A** で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQL Server 構成マネージャーを起動します。サーバーがリッスンしているパイプ名を確認します。 パイプ名は \\\\.\\$$\VIRTSQL\pipe\sql\query のように表示されます。  
  
4.  クライアント コンピューターで、SQL Server 構成マネージャーを起動します。  
  
5.  "SQLTEST1" という別名を作成し、名前付きパイプ経由でこのパイプ名に接続します。 これを行うには、サーバー名として「 **Node A** 」と入力し、パイプ名を編集して \\\\.\pipe\\$$\VIRTSQL\sql\query とします。  
  
6.  別名 SQLTEST1 をサーバー名として使用して、このインスタンスに接続します。  
  
### <a name="problem-sql-server-setup-fails-on-a-cluster-with-error-11001"></a>問題: クラスターでエラー 11001 が発生して SQL Server セットアップが失敗する  
 **問題点:** [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL.X\Cluster] に孤立したレジストリ キーがあります。  
  
 **解決方法:** MSSQL.X レジストリ ハイブが使用中でないことを確認し、クラスター キーを削除します。  
  
### <a name="problem-cluster-setup-error-the-installer-has-insufficient-privileges-to-access-this-directory-drivemicrosoft-sql-server-the-installation-cannot-continue-log-on-as-an-administrator-or-contact-your-system-administrator"></a>問題: クラスターのセットアップ エラー: "インストーラーにはディレクトリ \<drive>\Microsoft SQL Server にアクセスするための十分な特権がありません。 インストールを続行できません。 管理者としてログオンするか、またはシステム管理者に問い合わせてください。" が発生する  
 **問題点:** このエラーは SCSI 共有ドライブのパーティションが適切に分割されていないために発生します。  
  
 **解決方法:** 次の手順に従って、共有ディスクに単一のパーティションを再作成します。  
  
1.  クラスターからディスク リソースを削除します。  
  
2.  ディスクのすべてのパーティションを削除します。  
  
3.  ディスクのプロパティで、ディスクが基本ディスクになっていることを確認します。  
  
4.  共有ディスクにパーティションを 1 つ作成し、ディスクをフォーマットして、ドライブ文字を割り当てます。  
  
5.  クラスター アドミニストレーター (cluadmin) を使用してディスクをクラスターに追加します。  
  
6.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップを実行します。  
  
### <a name="problem-applications-fail-to-enlist-sql-server-resources-in-a-distributed-transaction"></a>問題: アプリケーションで SQL Server リソースを分散トランザクションに参加させることができない  
 **問題点:** MS DTC ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] 分散トランザクション コーディネーター) が Windows で完全に構成されていないために、アプリケーションから [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースを分散トランザクションに参加させることができない場合があります。 この問題は、分散トランザクションを使用するリンク サーバー、分散クエリ、およびリモート ストアド プロシージャに影響することがあります。 MS DTC を構成する方法の詳細については、「 [Before Installing Failover Clustering](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)」を参照してください。  
  
 **解決方法:** このような問題を回避するには、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をインストールして MS DTC を構成したサーバーで、MS DTC サービスを完全に有効にする必要があります。  
  
 MS DTC を完全に有効にするには、次の手順を実行します。  
  
1.  コントロール パネルで、 **[管理ツール]** を開き、 **[コンピューターの管理]** を開きます。  
  
2.  [コンピューターの管理] の左ペインで、 **[サービスとアプリケーション]** を展開し、 **[サービス]** をクリックします。  
  
3.  [コンピューターの管理] の右ペインで、 **[Distributed Transaction Coordinator]** を右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[Distributed Transaction Coordinator のプロパティ]** ウィンドウで **[全般]** タブをクリックし、 **[停止]** をクリックしてサービスを停止します。  
  
5.  **[Distributed Transaction Coordinator のプロパティ]** ウィンドウで **[ログオン]** タブをクリックし、ログイン アカウント NT AUTHORITY\NetworkService を設定します。  
  
6.  **[適用]** をクリックして **[OK]** をクリックし、 **[分散トランザクション コーディネーター]** ウィンドウを閉じます。 **[コンピューターの管理]** ウィンドウを閉じます。 **[管理ツール]** ウィンドウを閉じます。  
  
## <a name="using-extended-stored-procedures-and-com-objects"></a>拡張ストアド プロシージャおよび COM オブジェクトの使用  
 フェールオーバー クラスタリング構成で拡張ストアド プロシージャを使用する場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]に依存するクラスター ディスク上にすべての拡張ストアド プロシージャをインストールする必要があります。 これは、ノードがフェールオーバーしても拡張ストアド プロシージャを使用できるようにするためです。  
  
 拡張ストアド プロシージャで COM コンポーネントが使用される場合、管理者はその COM コンポーネントをクラスター内の各ノードに登録する必要があります。 COM コンポーネントを作成するには、COM コンポーネントを読み込んで実行するための情報をアクティブなノードのレジストリに格納する必要があります。 この場所に格納しないと、その情報は COM コンポーネントを最初に登録したコンピューターのレジストリに残ります。  
  
## <a name="see-also"></a>参照  
 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [拡張ストアド プロシージャのしくみ](../../../relational-databases/extended-stored-procedures-programming/how-extended-stored-procedures-work.md)   
 [拡張ストアド プロシージャの実行における特性](../../../relational-databases/extended-stored-procedures-programming/execution-characteristics-of-extended-stored-procedures.md)  
  
  
