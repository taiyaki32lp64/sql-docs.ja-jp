---
title: 初期スナップショットの作成および適用 | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], creating
- snapshot replication [SQL Server], initial snapshots
ms.assetid: 742727a1-5189-44ec-b3ae-6fd7aa1f5347
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 11628e5b490c30ef64329f6b9d06aee1b6c10fa9
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908290"
---
# <a name="create-and-apply-the-initial-snapshot"></a>初期スナップショットの作成および適用
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、初期スナップショットを作成および適用する方法について説明します。 パラメーター化されたフィルターを使用するマージ パブリケーションでは、2 つの部分から成るスナップショットが必要です。 詳しくは、「 [パラメーター化されたフィルターを使用したパブリケーションのスナップショットの作成](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」をご覧ください。  
  スナップショットは、パブリケーションの作成後に、スナップショット エージェントによって生成されます。 スナップショットは、以下の方法で生成できます。  
  
-   すぐに生成。 既定では、マージ パブリケーションのスナップショットは、パブリケーションの新規作成ウィザードでパブリケーションが作成された後、すぐに生成されます。    
-   スケジュールで設定した時刻に生成。 スケジュールは、パブリケーションの新規作成ウィザードの **[スナップショット エージェント]** ページで指定するか、ストアド プロシージャまたはレプリケーション管理オブジェクト (RMO) の使用時に指定します。    
-   手動で作成。 コマンド プロンプトまたは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]からスナップショット エージェントを実行します。 エージェントの実行の詳細については、「[レプリケーション エージェント実行可能ファイルの概念](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)」および「[レプリケーション エージェントを起動および停止する &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)」を参照してください。  
  
マージ レプリケーションの場合は、スナップショット エージェントが起動するたびにスナップショットが生成されます。 トランザクション レプリケーションでは、スナップショットの生成はパブリケーション プロパティ **immediate_sync**の設定で決まります。 プロパティが TRUE に設定されていると (パブリケーションの新規作成ウィザードを使用する際の既定の設定)、スナップショット エージェントを実行するたびにスナップショットが生成され、いつでもスナップショットをサブスクライバーに適用できます。 プロパティが FALSE に設定されていると ( **sp_addpublication**を使用する場合の既定の設定)、最後にスナップショット エージェントを実行してから新しいサブスクリプションが追加された場合にのみスナップショットが生成されます。サブスクライバーは、スナップショット エージェントが完了するまで同期することはできません。  
  
既定では、スナップショットが生成されると、そのスナップショットはディストリビューター上の既定のスナップショット フォルダーに保存されます。 スナップショット ファイルは、リムーバブル ディスク、CD-ROM などのリムーバブル メディアや、既定のスナップショット フォルダー以外の場所に保存することもできます。 また、格納および転送しやすいようにファイルを圧縮することや、サブスクライバーでスナップショットを適用する前または後にスクリプトを実行することもできます。 これらのオプションの詳細については、「 [Snapshot Options](../../relational-databases/replication/snapshot-options.md)」をご覧ください。  
  
パラメーター化されたフィルターを使用するマージ パブリケーションに対するスナップショットの場合は、2 段階の処理でスナップショットが作成されます。 まず、パブリッシュされたオブジェクトのレプリケーション スクリプトとスキーマが含まれるスキーマ スナップショットが作成されます。ただしデータは含まれません。 次に、スキーマ スナップショットからコピーしたスクリプトとスキーマが含まれるスナップショットと、サブスクリプションのパーティションに属するデータを使用して、各サブスクリプションが初期化されます。 詳しくは、「 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」をご覧ください。  
  
パブリッシャーで作成され、既定の位置または代替位置に格納されたスナップショットは、サブスクライバーに転送して適用することができます。 ディストリビューション エージェント (スナップショット レプリケーションおよびトランザクション レプリケーションの場合) またはマージ エージェント (マージ レプリケーションの場合) によって、最初の同期時に、サブスクライバー側のサブスクリプション データベースにスナップショットが転送され、スキーマ ファイルとデータ ファイルが適用されます。 サブスクリプションの新規作成ウィザードを使用する場合、既定では、サブスクリプションの作成後すぐに最初の同期が行われます。 この動作は、ウィザードの **[サブスクリプションの初期化]** ページの **[次の場合に初期化]** オプションによって制御されます。 サブスクリプションの初期化後に生成されたスナップショットは、サブスクリプションに再初期化のマークが付けられない限り、サブスクライバーに適用されません。 詳細については、「 [サブスクリプションの再初期化](../../relational-databases/replication/reinitialize-subscriptions.md)」を参照してください。  
  
ディストリビューション エージェントまたはマージ エージェントによる初期スナップショットの適用後、それらのエージェントによって以後の更新とその他のデータ変更が反映されます。 スナップショットがディストリビュートされサブスクライバーに適用されるときは、初期スナップショットまたは新しいスナップショットを待機しているサブスクライバーのみが影響を受けます。 そのパブリケーションへの他のサブスクライバー (パブリッシュされたデータへの挿入、更新、削除、またはその他の変更を既に受信中のサブスクライバー) は影響を受けません。  

スナップショット フォルダーの既定の場所を表示または変更するには、「  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:[スナップショット オプションの変更](../../relational-databases/replication/snapshot-options.md)  
  
-   レプリケーション プログラミングおよび RMO プログラミング:[パブリッシングおよびディストリビューションの構成](../../relational-databases/replication/configure-publishing-and-distribution.md)  

## <a name="default-snapshot-location"></a>既定のスナップショットの場所

 ディストリビューションの構成ウィザードの **[スナップショット フォルダー]** ページで、既定のスナップショットの場所を指定します。 ウィザードの使用の詳細については、「[パブリッシングおよびディストリビューションの構成](../../relational-databases/replication/configure-publishing-and-distribution.md)」を参照してください。 ディストリビューターとして構成されていないサーバーでパブリケーションを作成する場合は、パブリケーションの新規作成ウィザードの **[スナップショット フォルダー]** ページで既定のスナップショットの場所を指定します。 このウィザードの使用の詳細については、「[パブリケーションの作成](../../relational-databases/replication/publish/create-a-publication.md)」を参照してください。  
  
 **[ディストリビューターのプロパティ - \<Distributor>]** ダイアログ ボックスの **[パブリッシャー]** ページで、既定のスナップショットの場所を変更します。 詳細については、「[ディストリビューターとパブリッシャーのプロパティの表示および変更](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)」を参照してください。 **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスで、各パブリケーションのスナップショット フォルダーを設定します。 詳しくは、「 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」をご覧ください。  
  
### <a name="modify-the-default-snapshot-location"></a>既定のスナップショットの場所の変更  
  
1.  **[ディストリビューターのプロパティ - \<Distributor>]** ダイアログ ボックスの **[パブリッシャー]** ページで、既定のスナップショットの場所を変更するパブリッシャーのプロパティ ボタン ( **[...]** ) をクリックします。  
  
2.  **[パブリッシャーのプロパティ - \<Publisher>]** ダイアログ ボックスで、 **[既定のスナップショット フォルダー]** プロパティの値を入力します。  
  
    > [!NOTE]  
    >  スナップショット エージェントには、指定したディレクトリに対する書き込み権限が必要です。また、ディストリビューション エージェントまたはマージ エージェントには、読み取り権限が必要です。 プル サブスクリプションを使用する場合は、共有ディレクトリを UNC (汎用名前付け規則) パス (\\\computername\snapshot など) で指定する必要があります。 詳細については、「[Secure the Snapshot Folder](../../relational-databases/replication/security/secure-the-snapshot-folder.md)」(スナップショット フォルダーのセキュリティ保護) をご覧ください。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="create-snapshot"></a>スナップショットの作成
SQL Server エージェントが実行されている場合、既定でパブリケーションの新規作成ウィザードでパブリケーションが作成された直後に、スナップショット エージェントによってスナップショットが生成されます。 既定では、スナップショットはディストリビューション エージェント (スナップショット レプリケーションおよびトランザクション レプリケーションの場合) またはマージ エージェント (マージ サブスクリプションの場合) によって、すべてのサブスクリプションに対して適用されます。 スナップショットは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] およびレプリケーション モニターを使用して生成することもできます。 レプリケーション モニターの起動の詳細については、「[Start the Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)」 (レプリケーション モニターの開始) を参照してください。  

### <a name="using-sql-server-management-studio"></a>SQL Server Management Studio の使用

1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。    
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。    
3.  スナップショットを作成するパブリケーションを右クリックして、 **[スナップショット エージェントの状態の表示]** をクリックします。    
4.  **[スナップショット エージェントの状態の表示 - \<Publication>]** ダイアログ ボックスで **[開始]** をクリックします。    
 スナップショット エージェントによるスナップショットの生成が完了すると、"[100%] 17 個のアーティクルのスナップショットが生成されました。" などのメッセージが表示されます。  
  
### <a name="in-replication-monitor"></a>レプリケーション モニターで次を実行します。  
  
1.  レプリケーション モニターの左ペインでパブリッシャー グループを展開し、パブリッシャーを展開します。    
2.  スナップショットを生成するパブリケーションを右クリックして、 **[スナップショットの生成]** をクリックします。    
3.  スナップショット エージェントの状態を表示するには、 **[エージェント]** タブをクリックします。詳細情報については、グリッドでスナップショット エージェントを右クリックし、 **[詳細表示]** をクリックしてください。  

## <a name="using-transact-sql"></a>Transact-SQL の使用
初期スナップショットは、スナップショット エージェント ジョブを作成、実行するか、スナップショット エージェントの実行可能ファイルをバッチ ファイルから実行することによってプログラムから作成できます。 生成された初期スナップショットは、サブスクリプションの初回同期時にサブスクライバーに転送されて適用されます。 スナップショット エージェントをコマンド プロンプトまたはバッチ ファイルから実行する場合、既存のスナップショットが無効になるたびにエージェントを再実行する必要があります。  
  
> [!IMPORTANT]  
>  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  

1.  スナップショット パブリケーション、トランザクション パブリケーション、またはマージ パブリケーションを作成します。 詳細については、「 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)」を参照してください。  
  
2.  [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) を実行します。 このとき、 **\@publication** パラメーターを指定したうえで、次のパラメーターを指定します。  
  
    -   **\@job_login**。これにより指定される Windows 認証の資格情報の下、ディストリビューターでスナップショット エージェントが実行されます。  
  
    -   **\@job_password**。これは指定された Windows 資格情報のパスワードです。  
  
    -   (省略可能) エージェントからパブリッシャーへの接続に SQL Server 認証を使用する場合は、 **\@publisher_security_mode** の値に **0** を指定します。 この場合は、さらに、 **\@publisher_login** と **\@publisher_password** に対して、SQL Server 認証のログイン情報を指定する必要があります。  
  
    -   (省略可) スナップショット エージェント ジョブの同期スケジュールを指定します。 詳しくは、「 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)」をご覧ください。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
3.  パブリケーションにアーティクルを追加します。 詳しくは、「 [アーティクルを定義](../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
4.  パブリケーション データベースのパブリッシャーで [sp_startpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md) を実行し、手順 1 の **\@publication** の値を指定します。  
  
## <a name="apply-a-snapshot"></a>スナップショットの適用  

### <a name="using-sql-server-management-studio"></a>SQL Server Management Studio の使用
  
1.  生成したスナップショットは、ディストリビューション エージェントまたはマージ エージェントによるサブスクリプションの同期によって適用されます。   
    -   エージェントを連続して実行するように設定している場合 (トランザクション レプリケーションの既定の動作)、スナップショットは生成後に自動的に適用されます。   
    -   スケジュールに基づいてエージェントを実行するように設定している場合、スナップショットは、スケジュールによる次回のエージェント実行時に適用されます。    
    -   要求時にエージェントを実行するように設定している場合、スナップショットは、次回のエージェント実行時に適用されます。  
  
     サブスクリプションの同期の詳細については、「 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md) 」および「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)ダイアログ ボックスを使用します。  
  
###   <a name="use-transact-sql"></a>Transact-SQL の使用  
 
1.  スナップショット パブリケーション、トランザクション パブリケーション、またはマージ パブリケーションを作成します。 詳細については、「 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)」を参照してください。  
  
2.  パブリケーションにアーティクルを追加します。 詳しくは、「 [アーティクルを定義](../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
3.  コマンド プロンプトまたはバッチ ファイルから、次のコマンド ライン引数を指定して [snapshot.exe](../../relational-databases/replication/agents/replication-snapshot-agent.md) を実行し、 **レプリケーション マージ エージェント**を起動します。  
  
    -   **-Publication**  
    -   **-Publisher**  
    -   **-Distributor**   
    -   **-PublisherDB**   
    -   **-ReplicationType**  
  
     SQL Server 認証を使用する場合は、次の引数も指定する必要があります。  
  
    -   **-DistributorLogin**    
    -   **-DistributorPassword**   
    -   **-DistributorSecurityMode** =  **\@publisher_security_mode**    
    -   **-PublisherLogin**    
    -   **-PublisherPassword**    
    -   **-PublisherSecurityMode** =  **\@publisher_security_mode**  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、トランザクション パブリケーションを作成し、 **sqlcmd** スクリプト変数を使用して、新しいパブリケーション用にスナップショット エージェント ジョブを追加します。 ジョブを開始するコードも含まれています。  
  
 [!code-sql[HowTo#sp_trangenerate_snapshot](../../relational-databases/replication/codesnippet/tsql/create-and-apply-the-ini_1.sql)]  
  
 次の例では、マージ パブリケーションを作成し、 **sqlcmd** 変数を使用して、そのパブリケーション用のスナップショット エージェント ジョブを追加します。 ジョブを開始するコードも含まれています。  
  
 [!code-sql[HowTo#sp_mergegenerate_snapshot](../../relational-databases/replication/codesnippet/tsql/create-and-apply-the-ini_2.sql)]  
  
 次のコマンド ライン引数は、スナップショット エージェントを起動して、マージ パブリケーション用のスナップショットを生成します。  
  
> [!NOTE]  
>  読みやすくするために、改行が追加されています。 バッチ ファイルの場合、コマンドは 1 行で入力する必要があります。  
  
```  
  
REM -- Declare variables  
SET Publisher=%InstanceName%  
SET PublicationDB=AdventureWorks2012   
SET Publication=AdvWorksSalesOrdersMerge   
  
REM --Start the Snapshot Agent to generate the snapshot for AdvWorksSalesOrdersMerge.  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %Publication%   
-Publisher %Publisher% -Distributor %Publisher% -PublisherDB %PublicationDB%   
-ReplicationType 2 -OutputVerboseLevel 1 -DistributorSecurityMode 1  
  
```  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 スナップショット エージェントは、パブリッシャーが作成された後でスナップショットを生成します。 レプリケーション管理オブジェクト (RMO) およびレプリケーション エージェント機能への直接的なマネージド コード アクセスを使用して、これらのスナップショットをプログラムで生成できます。 使用するオブジェクトは、レプリケーションの種類によって異なります。 スナップショット エージェントを同期的に開始する場合は <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> オブジェクトを使用し、非同期的に開始する場合はエージェント ジョブを使用します。 初期スナップショットの生成後、サブスクリプションを最初に同期するときに、初期スナップショットをサブスクライバーに転送して適用することができます。 既存のスナップショットに最新の有効なデータが含まれていない場合は、エージェントを再実行する必要があります。 詳細については、「[Maintain Publications](../../relational-databases/replication/publish/maintain-publications.md)」(パブリケーションの管理) を参照してください。  
  
> [!IMPORTANT]  
>  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 資格情報を保存する必要がある場合は、 [Windows .NET&#xA0;Framework に用意されている](https://go.microsoft.com/fwlink/?LinkId=34733) 暗号化サービス [!INCLUDE[msCoName](../../includes/msconame-md.md)] を使用します。  
  
#### <a name="to-generate-the-initial-snapshot-for-a-snapshot-or-transactional-publication-by-starting-the-snapshot-agent-job-asynchronous"></a>スナップショット エージェント ジョブを非同期的に開始して、スナップショット パブリケーションまたはトランザクション パブリケーションの初期スナップショットを生成するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPublication> クラスのインスタンスを作成します。 パブリケーションの <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> プロパティおよび <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> プロパティを設定し、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに手順 1. で作成した接続を設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトの残りのプロパティを読み込みます。 このメソッドが **false**を返す場合、手順 2. でパブリケーション プロパティを不適切に設定したか、パブリケーションが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> の値が **false** の場合は、<xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> を呼び出して、このパブリケーション用のスナップショット エージェント ジョブを作成します。  
  
5.  <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> メソッドを呼び出して、このパブリケーションのスナップショットを生成するエージェント ジョブを開始します。  
  
6.  (省略可) <xref:Microsoft.SqlServer.Replication.TransPublication.SnapshotAvailable%2A> の値が **true**である場合は、スナップショットをサブスクライバーに使用できます。  
  
#### <a name="to-generate-the-initial-snapshot-for-a-snapshot-or-transactional-publication-by-running-the-snapshot-agent-synchronous"></a>スナップショット エージェント ジョブを同期的に実行して、スナップショット パブリケーションまたはトランザクション パブリケーションの初期スナップショットを生成するには  
  
1.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> クラスのインスタンスを作成し、次の必須プロパティを設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - パブリッシャーの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - パブリケーション データベースの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - パブリケーションの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - ディストリビューターの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> - パブリッシャーへの接続時に Windows 認証を使用する場合は <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> を指定します。パブリッシャーへの接続時に <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 認証を使用する場合は <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> を指定し、 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に値を指定します。 推奨されるのは、Windows 認証です。  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> - ディストリビューターへの接続時に Windows 認証を使用する場合は <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> を指定します。ディストリビューターへの接続時に <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 認証を使用する場合は <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> を指定し、 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に値を指定します。 推奨されるのは、Windows 認証です。  
  
2.  <xref:Microsoft.SqlServer.Replication.ReplicationType.Transactional> に <xref:Microsoft.SqlServer.Replication.ReplicationType.Snapshot> または <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>を設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> メソッドを呼び出します。  
  
#### <a name="to-generate-the-initial-snapshot-for-a-merge-publication-by-starting-the-snapshot-agent-job-asynchronous"></a>スナップショット エージェント ジョブを非同期的に開始して、マージ パブリケーションの初期スナップショットを生成するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePublication> クラスのインスタンスを作成します。 パブリケーションの <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> プロパティおよび <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> プロパティを設定し、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに手順 1. で作成した接続を設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトの残りのプロパティを読み込みます。 このメソッドが **false**を返す場合、手順 2. でパブリケーション プロパティを不適切に設定したか、パブリケーションが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> の値が **false** の場合は、<xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> を呼び出して、このパブリケーション用のスナップショット エージェント ジョブを作成します。  
  
5.  <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> メソッドを呼び出して、このパブリケーションのスナップショットを生成するエージェント ジョブを開始します。  
  
6.  (省略可) <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> の値が **true**である場合は、スナップショットをサブスクライバーに使用できます。  
  
#### <a name="to-generate-the-initial-snapshot-for-a-merge-publication-by-running-the-snapshot-agent-synchronous"></a>スナップショット エージェントを同期的に実行して、マージ パブリケーションの初期スナップショットを生成するには  
  
1.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> クラスのインスタンスを作成し、次の必須プロパティを設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - パブリッシャーの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - パブリケーション データベースの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - パブリケーションの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - ディストリビューターの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> - パブリッシャーへの接続時に Windows 認証を使用する場合は <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> を指定します。パブリッシャーへの接続時に <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 認証を使用する場合は <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> を指定し、 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に値を指定します。 推奨されるのは、Windows 認証です。  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> - ディストリビューターへの接続時に Windows 認証を使用する場合は <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> を指定します。ディストリビューターへの接続時に <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 認証を使用する場合は <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> を指定し、 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に値を指定します。 推奨されるのは、Windows 認証です。  
  
2.  <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> に <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>を設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> メソッドを呼び出します。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 次の例では、スナップショット エージェントを同期的に実行して、トランザクション パブリケーションの初期スナップショットを生成します。  
  
 [!code-cs[HowTo#rmo_GenerateSnapshot](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatesnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatesnapshot)]  
  
 次の例では、エージェント ジョブを非同期的に開始して、トランザクション パブリケーションの初期スナップショットを生成します。  
  
 [!code-cs[HowTo#rmo_GenerateSnapshot_WithJob](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatesnapshot_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot_WithJob](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatesnapshot_withjob)]  
  
## <a name="see-also"></a>参照  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)   
 [Initialize a Subscription with a Snapshot (スナップショットを使用したサブスクリプションの初期化)](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Replication Management Objects Concepts](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Replication System Stored Procedures Concepts](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [sqlcmd でのスクリプト変数の使用](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
