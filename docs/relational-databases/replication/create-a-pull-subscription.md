---
title: プル サブスクリプションの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- pull subscriptions [SQL Server replication], creating
- merge replication subscribing [SQL Server replication], pull subscriptions
- subscriptions [SQL Server replication], pull
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: 41d1886d-59c9-41fc-9bd6-a59b40e0af6e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 5dde30d826d5b6662a4f488aed7c3a1f21dd00b2
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908432"
---
# <a name="create-a-pull-subscription"></a>プル サブスクリプションの作成

<!--
2019-10-24 , GeneMi:
This article .md file exists in the so-called "2016+" section of repo 'sql-docs-pr'.
No article in 2016+ should ever have the moniker 'sql-server-2014' on its metadata line 'monikerRange:', I think.
Presently 'sql-server-2014' moniker is on this 'monikerRange'. This situation deserves further investigation.
-->

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用してプル サブスクリプションを作成する方法について説明します。  
  
 P2P レプリケーションのプル サブスクリプションの設定にはスクリプトを使用できますが、ウィザードは使用できません。  
 
  ##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 サブスクリプションの新規作成ウィザードを使用して、パブリッシャーまたはサブスクライバーでプル サブスクリプションを作成します。 ウィザードのページに従って、次の操作を実行します。  
  
-   パブリッシャーとパブリケーションを指定します。  
  
-   レプリケーション エージェントが実行される場所を選択します。 プル サブスクリプションでは、パブリケーションの種類に応じて、 **[ディストリビューション エージェントの場所]** ページまたは **[マージ エージェントの場所]** ページで、 **[サブスクライバーで各エージェントを実行する (プル サブスクリプション)]** を選択します。  
  
-   サブスクライバーとサブスクリプション データベースを指定します。  
  
-   レプリケーション エージェントによって作成された接続に対して使用されるログインとパスワードを指定します。  
  
    -   スナップショット パブリケーションとトランザクション パブリケーションに対するサブスクリプションでは、 **[ディストリビューション エージェント セキュリティ]** ページで資格情報を指定します。  
  
    -   マージ パブリケーションに対するサブスクリプションでは、 **[マージ エージェント セキュリティ]** ページで資格情報を指定します。  
  
     各エージェントで必要な権限の詳細については、「 [レプリケーション エージェント セキュリティ モデル](../../relational-databases/replication/security/replication-agent-security-model.md)」を参照してください。  
  
-   同期スケジュール、およびサブスクライバーをいつ初期化するかを指定します。  
  
-   マージ パブリケーションの追加オプションである、サブスクリプションの種類、パラメーター化されたフィルターの値、およびパブリケーションが Web 同期に対して有効になっている場合の HTTPS を使用した同期に関する情報を指定します。  
  
-   サブスクリプションの更新が許可されるトランザクション パブリケーションの追加オプションを指定します。サブスクライバーがパブリッシャーで変更をすぐにコミットするかどうか、変更をキューに書き込むかどうか、およびサブスクライバーからパブリッシャーへの接続に使用される資格情報を指定します。  
  
-   必要に応じて、サブスクリプションのスクリプトを作成します。  
  
#### <a name="to-create-a-pull-subscription-from-the-publisher"></a>パブリッシャーからプル サブスクリプションを作成するには  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。  
  
3.  1 つ以上のサブスクリプションを作成するパブリケーションを右クリックし、 **[新しいサブスクリプション]** をクリックします。  
  
4.  サブスクリプションの新規作成ウィザードのページに従って操作を実行します。  

#### <a name="to-create-a-pull-subscription-from-the-subscriber"></a>サブスクライバーからプル サブスクリプションを作成するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でサブスクライバーに接続して、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開します。  
  
3.  **[ローカル サブスクリプション]** フォルダーを右クリックし、 **[新しいサブスクリプション]** をクリックします。  
  
4.  サブスクリプションの新規作成ウィザードの **[パブリケーション]** ページで、 **[パブリッシャー]** ボックスの一覧から **[\<SQL Server パブリッシャーの検索>]** または **[\<Oracle パブリッシャーの検索>]** を選択します。  
  
5.  **[サーバーへの接続]** ダイアログ ボックスでパブリッシャーに接続します。  
  
6.  **[パブリケーション]** ページでパブリケーションを選択します。  
  
7.  サブスクリプションの新規作成ウィザードのページに従って操作を実行します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 レプリケーション ストアド プロシージャを使用して、プル サブスクリプションをプログラムで作成できます。 使用するストアド プロシージャは、サブスクリプションが属するパブリケーションの種類によって変わります。  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションに対するプル サブスクリプションを作成するには  
  
1.  パブリッシャーで、 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) を実行することにより、パブリケーションがプル サブスクリプションをサポートしていることを確認します。  
  
    -   結果セットの **allow_pull** の値が **1**である場合、パブリケーションはプル サブスクリプションをサポートします。  
  
    -   **allow_pull** の値が **0** である場合は、 **\@property** に **allow_pull** を、 **\@value** に **true** を指定して、[sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) を実行します。  
  
2.  サブスクライバーで、[sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md) を実行します。 **\@publisher** と **\@publication** を指定します。 サブスクリプションの更新の詳細については、「 [トランザクション パブリケーションの更新可能なサブスクリプションの作成](publish/create-an-updatable-subscription-to-a-transactional-publication.md)」を参照してください。   
  
3.  サブスクライバーで、[sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) を実行します。 次の指定を行います。  
  
    -   **\@publisher**、 **\@publisher_db**、 **\@publication** の各パラメーター。  
  
    -   **\@job_login** および **\@job_password** に、サブスクライバーでディストリビューション エージェントを実行するときに使用する [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 資格情報。  
  
        > [!NOTE]  
        >  Windows 統合認証を使用して行われる接続では、常に **\@job_login** および **\@job_password** で指定された Windows 資格情報が使用されます。 ディストリビューション エージェントは、常に Windows 統合認証を使用してサブスクライバーへのローカル接続を作成します。 既定では、エージェントは Windows 統合認証を使用してディストリビューターに接続します。  
  
    -   (省略可) ディストリビューターへの接続時に SQL Server 認証を使用する必要がある場合は、 **\@distributor_security_mode** に **0**、 **\@distributor_login** および **\@distributor_password** に SQL Server ログイン情報。  
  
    -   このサブスクリプションでのディストリビューション エージェント ジョブのスケジュール。 詳細については、「 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)」を参照してください。  
  
4.  パブリッシャー側で [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) を実行し、プル サブスクリプションを登録します。 **\@publication**、 **\@subscriber**、および **\@destination_db** を指定します。 **\@subscription_type** には **pull** を指定します。  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプル サブスクリプションを作成するには  
  
1.  パブリッシャーで、[sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md) を実行することにより、パブリケーションがプル サブスクリプションをサポートしていることを確認します。  
  
    -   結果セットの **allow_pull** の値が **1**である場合、パブリケーションはプル サブスクリプションをサポートします。  
  
    -   **allow_pull** の値が **0** である場合は、 **\@property** に **allow_pull** を、 **\@value** に **true** を指定して、[sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) を実行します。  
  
2.  サブスクライバーで、[sp_addmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md) を実行します。 **\@publisher**、 **\@publisher_db**、 **\@publication**、および次のパラメーターを指定します。  
  
    -   **\@subscriber_type** - クライアント サブスクリプションには **local** を指定し、サーバー サブスクリプションには **global** を指定します。  
  
    -   **\@subscription_priority** - サブスクリプションの優先度 (**0.00** から **99.99**) を指定します。 これは、サーバー サブスクリプションにのみ必要です。  
  
         詳細については、「 [マージ レプリケーションの競合検出および解決の詳細](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)」を参照してください。  
  
3.  サブスクライバーで、 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) を実行します。 次のパラメーターを指定します。  
  
    -   **\@publisher**、 **\@publisher_db**、および **\@publication** の各パラメーター。  
  
    -   **\@job_login** および **\@job_password** に、サブスクライバーでマージ エージェントを実行するときに使用する Windows 資格情報。  
  
        > [!NOTE]  
        >  Windows 統合認証を使用して行われる接続では、常に **\@job_login** および **\@job_password** で指定された Windows 資格情報が使用されます。 マージ エージェントは、常に Windows 統合認証を使用してサブスクライバーへのローカル接続を作成します。 既定では、エージェントは Windows 統合認証を使用してディストリビューターおよびパブリッシャーに接続します。  
  
    -   (省略可) ディストリビューターへの接続時に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する必要がある場合は、 **\@distributor_security_mode** に **0**、 **\@distributor_login** および **\@distributor_password** に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン情報。  
  
    -   (省略可) パブリッシャーへの接続時に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する必要がある場合は、 **\@publisher_security_mode** に **0**、 **\@publisher_login** および **\@publisher_password** に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン情報。  
  
    -   このサブスクリプションでのマージ エージェント ジョブのスケジュール。 詳しくは、「 [トランザクション パブリケーションの更新可能なサブスクリプションの作成](publish/create-an-updatable-subscription-to-a-transactional-publication.md)」をご覧ください。  
  
4.  パブリッシャーで [sp_addmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) を実行します。 **\@publication**、 **\@subscriber**、 **\@subscriber_db**、 **\@subscription_type** に対する **pull** の値を指定します。 これにより、プル サブスクリプションが登録されます。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、トランザクション パブリケーションに対するプル サブスクリプションを作成します。 最初のバッチはサブスクライバーで実行され、2 番目のバッチはパブリッシャーで実行されます。 ログインとパスワードの値は、実行時に sqlcmd スクリプト変数を使用して入力されます。  
  
```  
-- This script uses sqlcmd scripting variables. They are in the form  
-- $(MyVariable). For information about how to use scripting variables    
-- on the command line and in SQL Server Management Studio, see the   
-- "Executing Replication Scripts" section in the topic  
-- "Programming Replication Using System Stored Procedures".  
  
-- Execute this batch at the Subscriber.  
DECLARE @publication AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @publicationDB AS sysname;  
SET @publication = N'AdvWorksProductTran';  
SET @publisher = $(PubServer);  
SET @publicationDB = N'AdventureWorks';  
  
-- At the subscription database, create a pull subscription   
-- to a transactional publication.  
USE [AdventureWorksReplica]  
EXEC sp_addpullsubscription   
  @publisher = @publisher,   
  @publication = @publication,   
  @publisher_db = @publicationDB;  
  
-- Add an agent job to synchronize the pull subscription.  
EXEC sp_addpullsubscription_agent   
  @publisher = @publisher,   
  @publisher_db = @publicationDB,   
  @publication = @publication,   
  @distributor = @publisher,   
  @job_login = $(Login),   
  @job_password = $(Password);  
GO  
```  
  
```  
-- This script uses sqlcmd scripting variables. They are in the form  
-- $(MyVariable). For information about how to use scripting variables    
-- on the command line and in SQL Server Management Studio, see the   
-- "Executing Replication Scripts" section in the topic  
-- "Programming Replication Using System Stored Procedures".  
  
-- Execute this batch at the Publisher.  
DECLARE @publication AS sysname;  
DECLARE @subscriber AS sysname;  
DECLARE @subscriptionDB AS sysname;  
SET @publication = N'AdvWorksProductTran';  
SET @subscriber = $(SubServer);  
SET @subscriptionDB = N'AdventureWorksReplica';  
  
-- At the Publisher, register the subscription, using the defaults.  
EXEC sp_addsubscription   
  @publication = @publication,   
  @subscriber = @subscriber,   
  @destination_db = @subscriptionDB,   
  @subscription_type = N'pull',  
  @status = N'subscribed';  
GO  
  
```  
  
 次の例では、マージ パブリケーションに対するプル サブスクリプションを作成します。 最初のバッチはサブスクライバーで実行され、2 番目のバッチはパブリッシャーで実行されます。 ログインとパスワードの値は、実行時に **sqlcmd** スクリプト変数を使用して入力されます。  
  
```  
-- This script uses sqlcmd scripting variables. They are in the form  
-- $(MyVariable). For information about how to use scripting variables    
-- on the command line and in SQL Server Management Studio, see the   
-- "Executing Replication Scripts" section in the topic  
-- "Programming Replication Using System Stored Procedures".  
  
-- Execute this batch at the Subscriber.  
DECLARE @publication AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @publicationDB AS sysname;  
DECLARE @hostname AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge';  
SET @publisher = $(PubServer);  
SET @publicationDB = N'AdventureWorks';  
SET @hostname = N'adventure-works\david8';  
  
-- At the subscription database, create a pull subscription   
-- to a merge publication.  
USE [AdventureWorksReplica]  
EXEC sp_addmergepullsubscription   
  @publisher = @publisher,   
  @publication = @publication,   
  @publisher_db = @publicationDB;  
  
-- Add an agent job to synchronize the pull subscription.   
EXEC sp_addmergepullsubscription_agent   
  @publisher = @publisher,   
  @publisher_db = @publicationDB,   
  @publication = @publication,   
  @distributor = @publisher,   
  @job_login = $(Login),   
  @job_password = $(Password),  
  @hostname = @hostname;  
GO  
```  
  
```  
-- Execute this batch at the Publisher.  
DECLARE @myMergePub  AS sysname;  
DECLARE @mySub       AS sysname;  
DECLARE @mySubDB     AS sysname;  
  
SET @myMergePub = N'AdvWorksSalesOrdersMerge';  
SET @mySub = N'MYSUBSERVER';  
SET @mySubDB = N'AdventureWorksReplica';  
  
-- At the Publisher, register the subscription, using the defaults.  
USE [AdventureWorks]  
EXEC sp_addmergesubscription @publication = @myMergePub,   
@subscriber = @mySub, @subscriber_db = @mySubDB,   
@subscription_type = N'pull';  
GO  
```  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 プル サブスクリプションの作成に使用する RMO のクラスは、サブスクリプションが属しているパブリケーションの種類によって異なります。  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションに対するプル サブスクリプションを作成するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、サブスクライバーおよびパブリッシャーへの接続を作成します。  
  
2.  手順 1. のパブリッシャー接続を使用して、 <xref:Microsoft.SqlServer.Replication.TransPublication> クラスのインスタンスを作成します。 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 、および <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>を指定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出します。 このメソッドが **false**を返す場合、手順 2. で指定したプロパティが誤っているか、サーバーにパブリケーションが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> プロパティと <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull> のビットごとの論理 AND 演算 (Visual C# では **&** 、Visual Basic では **And**) を実行します。 結果が <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>の場合、 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> と **|** プロパティと **Or** 、Visual Basic では <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> に <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>」を参照してください。 続けて、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> を呼び出して、プル サブスクリプションを有効にします。  
  
5.  サブスクリプション データベースが存在しない場合は、 <xref:Microsoft.SqlServer.Management.Smo.Database> クラスを使用して作成します。 詳細については、「[データベースの作成、変更、および削除](../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)」を参照してください。  
  
6.  <xref:Microsoft.SqlServer.Replication.TransPullSubscription> クラスのインスタンスを作成します。  
  
7.  次のサブスクリプション プロパティを設定します。  
  
    -   手順 1. で作成した、サブスクライバーに対する <xref:Microsoft.SqlServer.Management.Common.ServerConnection> を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>に指定します。  
  
    -   サブスクリプション データベース名を <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>に指定します。  
  
    -   パブリッシャー名を <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>に指定します。  
  
    -   パブリケーション データベース名を <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>に指定します。  
  
    -   パブリケーション名を <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>に指定します。  
  
    -   手順 1. で作成した、サブスクライバーに対する <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> @value <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> (または [!INCLUDE[msCoName](../../includes/msconame-md.md)] ) フィールドに指定します。 このアカウントは、サブスクライバーとのローカル接続を確立したり、Windows 認証を使用したリモート接続を確立するときに使用されます。  
  
        > [!NOTE]  
        >  サブスクリプションが <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> 固定サーバー ロールのメンバーにより作成される場合、 **P:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity** の設定は必須ではありませんが、推奨されます。 この場合、エージェントは SQL Server エージェントのアカウントを借用します。 詳細については、「 [レプリケーション エージェント セキュリティ モデル](../../relational-databases/replication/security/replication-agent-security-model.md)」を参照してください。  
  
    -   (省略可) ディストリビューターへの接続時に **true** allow_pull <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> を指定します。 **false** (既定値) を指定した場合、サブスクリプションはプログラムによってのみ同期できます。また、このオブジェクトに <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A> プロパティからアクセスする場合は、<xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> のプロパティを別途指定する必要があります。 詳細については、「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)」をご覧ください。  
  
        > [!NOTE]  
        >  SQL Server エージェントは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]」を参照してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。 Express のサブスクライバーに対して値 **true** を指定しても、エージェント ジョブは作成されません。 ただし、サブスクリプション関連の重要なメタデータについてはサブスクライバーに保存されます。  
  
    -   (省略可) SQL Server 認証を使ってディストリビューターに接続する場合は、 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> の <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (または <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> ) フィールドを設定します。  
  
8.  <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> メソッドを呼び出します。  
  
9. 手順 2. で作成した <xref:Microsoft.SqlServer.Replication.TransPublication> クラスのインスタンスを使用して、 <xref:Microsoft.SqlServer.Replication.TransPublication.MakePullSubscriptionWellKnown%2A> メソッドを呼び出し、パブリッシャーにプル サブスクリプションを登録します。 既に登録されている場合は、例外が発生します。  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプル サブスクリプションを作成するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、サブスクライバーとパブリッシャーの両方に対する接続を作成します。  
  
2.  手順 1. のパブリッシャー接続を使用して、 <xref:Microsoft.SqlServer.Replication.MergePublication> クラスのインスタンスを作成します。 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>、および <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>を指定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出します。 このメソッドが **false**を返す場合、手順 2. で指定したプロパティが誤っているか、サーバーにパブリケーションが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> プロパティと <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull> のビットごとの論理 AND 演算 (Visual C# では **&** 、Visual Basic では **And**) を実行します。 結果が <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>の場合、 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> と **|** プロパティと **Or** 、Visual Basic では <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> に <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>」を参照してください。 続けて、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> を呼び出して、プル サブスクリプションを有効にします。  
  
5.  サブスクリプション データベースが存在しない場合は、 <xref:Microsoft.SqlServer.Management.Smo.Database> クラスを使用して作成します。 詳細については、「[データベースの作成、変更、および削除](../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)」を参照してください。  
  
6.  <xref:Microsoft.SqlServer.Replication.MergePullSubscription> クラスのインスタンスを作成します。  
  
7.  次のサブスクリプション プロパティを設定します。  
  
    -   手順 1. で作成した、サブスクライバーに対する <xref:Microsoft.SqlServer.Management.Common.ServerConnection> を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>に指定します。  
  
    -   サブスクリプション データベース名を <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>に指定します。  
  
    -   パブリッシャー名を <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>に指定します。  
  
    -   パブリケーション データベース名を <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>に指定します。  
  
    -   パブリケーション名を <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>に指定します。  
  
    -   手順 1. で作成した、サブスクライバーに対する <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> @value <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> (または [!INCLUDE[msCoName](../../includes/msconame-md.md)] ) フィールドに指定します。 このアカウントは、サブスクライバーとのローカル接続を確立したり、Windows 認証を使用したリモート接続を確立するときに使用されます。  
  
        > [!NOTE]  
        >  サブスクリプションが <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> 固定サーバー ロールのメンバーにより作成される場合、 **P:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity** の設定は必須ではありませんが、推奨されます。 この場合、エージェントは SQL Server エージェントのアカウントを借用します。 詳細については、「 [レプリケーション エージェント セキュリティ モデル](../../relational-databases/replication/security/replication-agent-security-model.md)」を参照してください。  
  
    -   (省略可) ディストリビューターへの接続時に **true** allow_pull <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> を指定します。 **false** (既定値) を指定した場合、サブスクリプションはプログラムによってのみ同期できます。また、このオブジェクトに <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A> プロパティからアクセスする場合は、<xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> のプロパティを別途指定する必要があります。 詳細については、「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)」をご覧ください。  
  
    -   (省略可) SQL Server 認証を使ってディストリビューターに接続する場合は、 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> の <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (または <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> ) フィールドを設定します。  
  
    -   (省略可) SQL Server 認証を使用してパブリッシャーに接続する場合、 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> の <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (または <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> ) フィールドを設定します。  
  
8.  <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> メソッドを呼び出します。  
  
9. 手順 2. で作成した <xref:Microsoft.SqlServer.Replication.MergePublication> クラスのインスタンスを使用して、 <xref:Microsoft.SqlServer.Replication.MergePublication.MakePullSubscriptionWellKnown%2A> メソッドを呼び出し、パブリッシャーにプル サブスクリプションを登録します。 既に登録されている場合は、例外が発生します。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 次の例では、トランザクション パブリケーションに対するプル サブスクリプションを作成します。 ディストリビューション エージェント ジョブを作成するために使用する [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントの資格情報は実行時に渡されます。  
  
```csharp  
// Define the Publisher, publication, and databases.  
string publicationName = "AdvWorksProductTran";  
string publisherName = publisherInstance;  
string subscriberName = subscriberInstance;  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
  
//Create connections to the Publisher and Subscriber.  
ServerConnection subscriberConn = new ServerConnection(subscriberName);  
ServerConnection publisherConn = new ServerConnection(publisherName);  
  
// Create the objects that we need.  
TransPublication publication;  
TransPullSubscription subscription;  
  
try  
{  
    // Connect to the Publisher and Subscriber.  
    subscriberConn.Connect();  
    publisherConn.Connect();  
  
    // Ensure that the publication exists and that   
    // it supports pull subscriptions.  
    publication = new TransPublication();  
    publication.Name = publicationName;  
    publication.DatabaseName = publicationDbName;  
    publication.ConnectionContext = publisherConn;  
  
    if (publication.IsExistingObject)  
    {  
        if ((publication.Attributes & PublicationAttributes.AllowPull) == 0)  
        {  
            publication.Attributes |= PublicationAttributes.AllowPull;  
        }  
  
        // Define the pull subscription.  
        subscription = new TransPullSubscription();  
        subscription.ConnectionContext = subscriberConn;  
        subscription.PublisherName = publisherName;  
        subscription.PublicationName = publicationName;  
        subscription.PublicationDBName = publicationDbName;  
        subscription.DatabaseName = subscriptionDbName;  
  
        // Specify the Windows login credentials for the Distribution Agent job.  
        subscription.SynchronizationAgentProcessSecurity.Login = winLogin;  
        subscription.SynchronizationAgentProcessSecurity.Password = winPassword;  
  
        // Make sure that the agent job for the subscription is created.  
        subscription.CreateSyncAgentByDefault = true;  
  
        // By default, subscriptions to transactional publications are synchronized   
        // continuously, but in this case we only want to synchronize on demand.  
        subscription.AgentSchedule.FrequencyType = ScheduleFrequencyType.OnDemand;  
  
        // Create the pull subscription at the Subscriber.  
        subscription.Create();  
  
        Boolean registered = false;  
  
        // Verify that the subscription is not already registered.  
        foreach (TransSubscription existing  
            in publication.EnumSubscriptions())  
        {  
            if (existing.SubscriberName == subscriberName  
                && existing.SubscriptionDBName == subscriptionDbName)  
            {  
                registered = true;  
            }  
        }  
        if (!registered)  
        {  
            // Register the subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown(  
                subscriberName, subscriptionDbName,  
                SubscriptionSyncType.Automatic,  
                TransSubscriberType.ReadOnly);  
        }  
    }  
    else  
    {  
        // Do something here if the publication does not exist.  
        throw new ApplicationException(String.Format(  
            "The publication '{0}' does not exist on {1}.",  
            publicationName, publisherName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement the appropriate error handling here.  
    throw new ApplicationException(String.Format(  
        "The subscription to {0} could not be created.", publicationName), ex);  
}  
finally  
{  
    subscriberConn.Disconnect();  
    publisherConn.Disconnect();  
}  
  
```  
  
```vb  
' Define the Publisher, publication, and databases.  
Dim publicationName As String = "AdvWorksProductTran"  
Dim publisherName As String = publisherInstance  
Dim subscriberName As String = subscriberInstance  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
  
'Create connections to the Publisher and Subscriber.  
Dim subscriberConn As ServerConnection = New ServerConnection(subscriberName)  
Dim publisherConn As ServerConnection = New ServerConnection(publisherName)  
  
' Create the objects that we need.  
Dim publication As TransPublication  
Dim subscription As TransPullSubscription  
  
Try  
    ' Connect to the Publisher and Subscriber.  
    subscriberConn.Connect()  
    publisherConn.Connect()  
  
    ' Ensure that the publication exists and that   
    ' it supports pull subscriptions.  
    publication = New TransPublication()  
    publication.Name = publicationName  
    publication.DatabaseName = publicationDbName  
    publication.ConnectionContext = publisherConn  
  
    If publication.IsExistingObject Then  
        If (publication.Attributes And PublicationAttributes.AllowPull) = 0 Then  
            publication.Attributes = publication.Attributes _  
            Or PublicationAttributes.AllowPull  
        End If  
  
        ' Define the pull subscription.  
        subscription = New TransPullSubscription()  
        subscription.ConnectionContext = subscriberConn  
        subscription.PublisherName = publisherName  
        subscription.PublicationName = publicationName  
        subscription.PublicationDBName = publicationDbName  
        subscription.DatabaseName = subscriptionDbName  
        subscription.Description = "Pull subscription to " + publicationDbName _  
        + " on " + subscriberName + "."  
  
        ' Specify the Windows login credentials for the Distribution Agent job.  
        subscription.SynchronizationAgentProcessSecurity.Login = winLogin  
        subscription.SynchronizationAgentProcessSecurity.Password = winPassword  
  
        ' Make sure that the agent job for the subscription is created.  
        subscription.CreateSyncAgentByDefault = True  
  
        ' By default, subscriptions to transactional publications are synchronized   
        ' continuously, but in this case we only want to synchronize on demand.  
        subscription.AgentSchedule.FrequencyType = ScheduleFrequencyType.OnDemand  
  
        ' Create the pull subscription at the Subscriber.  
        subscription.Create()  
  
        Dim registered As Boolean = False  
  
        ' Verify that the subscription is not already registered.  
        For Each existing As TransSubscription In publication.EnumSubscriptions()  
            If existing.SubscriberName = subscriberName And _  
                existing.SubscriptionDBName = subscriptionDbName Then  
                registered = True  
            End If  
        Next existing  
        If Not registered Then  
            ' Register the subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown( _  
             subscriberName, subscriptionDbName, _  
             SubscriptionSyncType.Automatic, _  
             TransSubscriberType.ReadOnly)  
        End If  
    Else  
        ' Do something here if the publication does not exist.  
        Throw New ApplicationException(String.Format( _  
         "The publication '{0}' does not exist on {1}.", _  
         publicationName, publisherName))  
    End If  
Catch ex As Exception  
    ' Implement the appropriate error handling here.  
    Throw New ApplicationException(String.Format( _  
        "The subscription to {0} could not be created.", publicationName), ex)  
Finally  
    subscriberConn.Disconnect()  
    publisherConn.Disconnect()  
End Try  
  
```  
  
 次の例では、マージ パブリケーションに対するプル サブスクリプションを作成します。 マージ エージェント ジョブを作成するために使用する Windows アカウントの資格情報は実行時に渡されます。  
  
```cpp#  
// Define the Publisher, publication, and databases.  
string publicationName = "AdvWorksSalesOrdersMerge";  
string publisherName = publisherInstance;  
string subscriberName = subscriberInstance;  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
string hostname = @"adventure-works\garrett1";  
  
//Create connections to the Publisher and Subscriber.  
ServerConnection subscriberConn = new ServerConnection(subscriberName);  
ServerConnection publisherConn = new ServerConnection(publisherName);  
  
// Create the objects that we need.  
MergePublication publication;  
MergePullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    subscriberConn.Connect();  
  
    // Ensure that the publication exists and that   
    // it supports pull subscriptions.  
    publication = new MergePublication();  
    publication.Name = publicationName;  
    publication.DatabaseName = publicationDbName;  
    publication.ConnectionContext = publisherConn;  
  
    if (publication.LoadProperties())  
    {  
        if ((publication.Attributes & PublicationAttributes.AllowPull) == 0)  
        {  
            publication.Attributes |= PublicationAttributes.AllowPull;  
        }  
  
        // Define the pull subscription.  
        subscription = new MergePullSubscription();  
        subscription.ConnectionContext = subscriberConn;  
        subscription.PublisherName = publisherName;  
        subscription.PublicationName = publicationName;  
        subscription.PublicationDBName = publicationDbName;  
        subscription.DatabaseName = subscriptionDbName;  
        subscription.HostName = hostname;  
  
        // Specify the Windows login credentials for the Merge Agent job.  
        subscription.SynchronizationAgentProcessSecurity.Login = winLogin;  
        subscription.SynchronizationAgentProcessSecurity.Password = winPassword;  
  
        // Make sure that the agent job for the subscription is created.  
        subscription.CreateSyncAgentByDefault = true;  
  
        // Create the pull subscription at the Subscriber.  
        subscription.Create();  
  
        Boolean registered = false;  
  
        // Verify that the subscription is not already registered.  
        foreach (MergeSubscription existing  
            in publication.EnumSubscriptions())  
        {  
            if (existing.SubscriberName == subscriberName  
                && existing.SubscriptionDBName == subscriptionDbName  
                && existing.SubscriptionType == SubscriptionOption.Pull)  
            {  
                registered = true;  
            }  
        }  
        if (!registered)  
        {  
            // Register the local subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown(  
                subscriberName, subscriptionDbName,  
                SubscriptionSyncType.Automatic,  
                MergeSubscriberType.Local, 0);  
        }  
    }  
    else  
    {  
        // Do something here if the publication does not exist.  
        throw new ApplicationException(String.Format(  
            "The publication '{0}' does not exist on {1}.",  
            publicationName, publisherName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement the appropriate error handling here.  
    throw new ApplicationException(String.Format(  
        "The subscription to {0} could not be created.", publicationName), ex);  
}  
finally  
{  
    subscriberConn.Disconnect();  
    publisherConn.Disconnect();  
}  
  
```  
  
```vb  
' Define the Publisher, publication, and databases.  
Dim publicationName As String = "AdvWorksSalesOrdersMerge"  
Dim publisherName As String = publisherInstance  
Dim subscriberName As String = subscriberInstance  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
Dim hostname As String = "adventure-works\garrett1"  
  
'Create connections to the Publisher and Subscriber.  
Dim subscriberConn As ServerConnection = New ServerConnection(subscriberName)  
Dim publisherConn As ServerConnection = New ServerConnection(publisherName)  
  
' Create the objects that we need.  
Dim publication As MergePublication  
Dim subscription As MergePullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    subscriberConn.Connect()  
  
    ' Ensure that the publication exists and that   
    ' it supports pull subscriptions.  
    publication = New MergePublication()  
    publication.Name = publicationName  
    publication.DatabaseName = publicationDbName  
    publication.ConnectionContext = publisherConn  
  
    If publication.LoadProperties() Then  
        If (publication.Attributes And PublicationAttributes.AllowPull) = 0 Then  
            publication.Attributes = publication.Attributes _  
            Or PublicationAttributes.AllowPull  
        End If  
  
        ' Define the pull subscription.  
        subscription = New MergePullSubscription()  
        subscription.ConnectionContext = subscriberConn  
        subscription.PublisherName = publisherName  
        subscription.PublicationName = publicationName  
        subscription.PublicationDBName = publicationDbName  
        subscription.DatabaseName = subscriptionDbName  
        subscription.HostName = hostname  
  
        ' Specify the Windows login credentials for the Merge Agent job.  
        subscription.SynchronizationAgentProcessSecurity.Login = winLogin  
        subscription.SynchronizationAgentProcessSecurity.Password = winPassword  
  
        ' Make sure that the agent job for the subscription is created.  
        subscription.CreateSyncAgentByDefault = True  
  
        ' Create the pull subscription at the Subscriber.  
        subscription.Create()  
  
        Dim registered As Boolean = False  
  
        ' Verify that the subscription is not already registered.  
        For Each existing As MergeSubscription In _  
        publication.EnumSubscriptions()  
            If existing.SubscriberName = subscriberName Then  
                registered = True  
            End If  
        Next  
        If Not registered Then  
            ' Register the local subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown( _  
             subscriberName, subscriptionDbName, _  
             SubscriptionSyncType.Automatic, _  
             MergeSubscriberType.Local, 0)  
        End If  
    Else  
        ' Do something here if the publication does not exist.  
        Throw New ApplicationException(String.Format( _  
         "The publication '{0}' does not exist on {1}.", _  
         publicationName, publisherName))  
    End If  
Catch ex As Exception  
    ' Implement the appropriate error handling here.  
    Throw New ApplicationException(String.Format( _  
        "The subscription to {0} could not be created.", publicationName), ex)  
Finally  
    subscriberConn.Disconnect()  
    publisherConn.Disconnect()  
End Try  
```  
  
 次の例では、関連するエージェント ジョブやサブスクリプション メタデータを [MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)に作成せずに、マージ パブリケーションに対するプル サブスクリプションを作成しています。 マージ エージェント ジョブを作成するために使用する Windows アカウントの資格情報は実行時に渡されます。  
  
```csharp  
// Define the Publisher, publication, and databases.  
string publicationName = "AdvWorksSalesOrdersMerge";  
string publisherName = publisherInstance;  
string subscriberName = subscriberInstance;  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
  
//Create connections to the Publisher and Subscriber.  
ServerConnection subscriberConn = new ServerConnection(subscriberName);  
ServerConnection publisherConn = new ServerConnection(publisherName);  
  
// Create the objects that we need.  
MergePublication publication;  
MergePullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    subscriberConn.Connect();  
  
    // Ensure that the publication exists and that   
    // it supports pull subscriptions.  
    publication = new MergePublication();  
    publication.Name = publicationName;  
    publication.DatabaseName = publicationDbName;  
    publication.ConnectionContext = publisherConn;  
  
    if (publication.LoadProperties())  
    {  
        if ((publication.Attributes & PublicationAttributes.AllowPull) == 0)  
        {  
            publication.Attributes |= PublicationAttributes.AllowPull;  
        }  
  
        // Define the pull subscription.  
        subscription = new MergePullSubscription();  
        subscription.ConnectionContext = subscriberConn;  
        subscription.PublisherName = publisherName;  
        subscription.PublicationName = publicationName;  
        subscription.PublicationDBName = publicationDbName;  
        subscription.DatabaseName = subscriptionDbName;  
  
        // Specify that an agent job not be created for this subscription. The  
        // subscription can only be synchronized by running the Merge Agent directly.  
        // Subscripition metadata stored in MSsubscription_properties will not  
        // be available and must be specified at run time.  
        subscription.CreateSyncAgentByDefault = false;  
  
        // Create the pull subscription at the Subscriber.  
        subscription.Create();  
  
        Boolean registered = false;  
  
        // Verify that the subscription is not already registered.  
        foreach (MergeSubscription existing  
            in publication.EnumSubscriptions())  
        {  
            if (existing.SubscriberName == subscriberName  
                && existing.SubscriptionDBName == subscriptionDbName  
                && existing.SubscriptionType == SubscriptionOption.Pull)  
            {  
                registered = true;  
            }  
        }  
        if (!registered)  
        {  
            // Register the local subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown(  
                subscriberName, subscriptionDbName,  
                SubscriptionSyncType.Automatic,  
                MergeSubscriberType.Local, 0);  
        }  
    }  
    else  
    {  
        // Do something here if the publication does not exist.  
        throw new ApplicationException(String.Format(  
            "The publication '{0}' does not exist on {1}.",  
            publicationName, publisherName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement the appropriate error handling here.  
    throw new ApplicationException(String.Format(  
        "The subscription to {0} could not be created.", publicationName), ex);  
}  
finally  
{  
    subscriberConn.Disconnect();  
    publisherConn.Disconnect();  
}  
```  
  
```vb  
' Define the Publisher, publication, and databases.  
Dim publicationName As String = "AdvWorksSalesOrdersMerge"  
Dim publisherName As String = publisherInstance  
Dim subscriberName As String = subscriberInstance  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
  
'Create connections to the Publisher and Subscriber.  
Dim subscriberConn As ServerConnection = New ServerConnection(subscriberName)  
Dim publisherConn As ServerConnection = New ServerConnection(publisherName)  
  
' Create the objects that we need.  
Dim publication As MergePublication  
Dim subscription As MergePullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    subscriberConn.Connect()  
  
    ' Ensure that the publication exists and that   
    ' it supports pull subscriptions.  
    publication = New MergePublication()  
    publication.Name = publicationName  
    publication.DatabaseName = publicationDbName  
    publication.ConnectionContext = publisherConn  
  
    If publication.LoadProperties() Then  
        If (publication.Attributes And PublicationAttributes.AllowPull) = 0 Then  
            publication.Attributes = publication.Attributes _  
            Or PublicationAttributes.AllowPull  
        End If  
  
        ' Define the pull subscription.  
        subscription = New MergePullSubscription()  
        subscription.ConnectionContext = subscriberConn  
        subscription.PublisherName = publisherName  
        subscription.PublicationName = publicationName  
        subscription.PublicationDBName = publicationDbName  
        subscription.DatabaseName = subscriptionDbName  
  
        ' Specify that an agent job not be created for this subscription. The  
        ' subscription can only be synchronized by running the Merge Agent directly.  
        ' Subscripition metadata stored in MSsubscription_properties will not  
        ' be available and must be specified at run time.  
        subscription.CreateSyncAgentByDefault = False  
  
        ' Create the pull subscription at the Subscriber.  
        subscription.Create()  
  
        Dim registered As Boolean = False  
  
        ' Verify that the subscription is not already registered.  
        For Each existing As MergeSubscription In _  
        publication.EnumSubscriptions()  
            If existing.SubscriberName = subscriberName Then  
                registered = True  
            End If  
        Next  
        If Not registered Then  
            ' Register the local subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown( _  
             subscriberName, subscriptionDbName, _  
             SubscriptionSyncType.Automatic, _  
             MergeSubscriberType.Local, 0)  
        End If  
    Else  
        ' Do something here if the publication does not exist.  
        Throw New ApplicationException(String.Format( _  
         "The publication '{0}' does not exist on {1}.", _  
         publicationName, publisherName))  
    End If  
Catch ex As Exception  
    ' Implement the appropriate error handling here.  
    Throw New ApplicationException(String.Format( _  
     "The subscription to {0} could not be created.", publicationName), ex)  
Finally  
    subscriberConn.Disconnect()  
    publisherConn.Disconnect()  
End Try  
```  
  
 次の例では、Web 同期によるインターネットを介した同期が可能な、マージ パブリケーションに対するプル サブスクリプションを作成しています。 マージ エージェント ジョブを作成するために使用する Windows アカウントの資格情報は実行時に渡されます。 詳しくは、「 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)」をご覧ください。  
  
```csharp  
// Define the Publisher, publication, and databases.  
string publicationName = "AdvWorksSalesOrdersMerge";  
string publisherName = publisherInstance;  
string subscriberName = subscriberInstance;  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
string hostname = @"adventure-works\garrett1";  
string webSyncUrl = "https://" + publisherInstance + "/WebSync/replisapi.dll";  
  
//Create connections to the Publisher and Subscriber.  
ServerConnection subscriberConn = new ServerConnection(subscriberName);  
ServerConnection publisherConn = new ServerConnection(publisherName);  
  
// Create the objects that we need.  
MergePublication publication;  
MergePullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    subscriberConn.Connect();  
  
    // Ensure that the publication exists and that   
    // it supports pull subscriptions and Web synchronization.  
    publication = new MergePublication();  
    publication.Name = publicationName;  
    publication.DatabaseName = publicationDbName;  
    publication.ConnectionContext = publisherConn;  
  
    if (publication.LoadProperties())  
    {  
        if ((publication.Attributes & PublicationAttributes.AllowPull) == 0)  
        {  
            publication.Attributes |= PublicationAttributes.AllowPull;  
        }  
        if ((publication.Attributes & PublicationAttributes.AllowWebSynchronization) == 0)  
        {  
            publication.Attributes |= PublicationAttributes.AllowWebSynchronization;  
        }  
  
        // Define the pull subscription.  
        subscription = new MergePullSubscription();  
        subscription.ConnectionContext = subscriberConn;  
        subscription.PublisherName = publisherName;  
        subscription.PublicationName = publicationName;  
        subscription.PublicationDBName = publicationDbName;  
        subscription.DatabaseName = subscriptionDbName;  
        subscription.HostName = hostname;  
  
        // Specify the Windows login credentials for the Merge Agent job.  
        subscription.SynchronizationAgentProcessSecurity.Login = winLogin;  
        subscription.SynchronizationAgentProcessSecurity.Password = winPassword;  
  
        // Enable Web synchronization.  
        subscription.UseWebSynchronization = true;  
        subscription.InternetUrl = webSyncUrl;  
  
        // Specify the same Windows credentials to use when connecting to the  
        // Web server using HTTPS Basic Authentication.  
        subscription.InternetSecurityMode = AuthenticationMethod.BasicAuthentication;  
        subscription.InternetLogin = winLogin;  
        subscription.InternetPassword = winPassword;  
  
        // Ensure that we create a job for this subscription.  
        subscription.CreateSyncAgentByDefault = true;  
  
        // Create the pull subscription at the Subscriber.  
        subscription.Create();  
  
        Boolean registered = false;  
  
        // Verify that the subscription is not already registered.  
        foreach (MergeSubscription existing  
            in publication.EnumSubscriptions())  
        {  
            if (existing.SubscriberName == subscriberName  
                && existing.SubscriptionDBName == subscriptionDbName  
                && existing.SubscriptionType == SubscriptionOption.Pull)  
            {  
                registered = true;  
            }  
        }  
        if (!registered)  
        {  
            // Register the local subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown(  
                subscriberName, subscriptionDbName,  
                SubscriptionSyncType.Automatic,  
                MergeSubscriberType.Local, 0);  
        }  
    }  
    else  
    {  
        // Do something here if the publication does not exist.  
        throw new ApplicationException(String.Format(  
            "The publication '{0}' does not exist on {1}.",  
            publicationName, publisherName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement the appropriate error handling here.  
    throw new ApplicationException(String.Format(  
        "The subscription to {0} could not be created.", publicationName), ex);  
}  
finally  
{  
    subscriberConn.Disconnect();  
    publisherConn.Disconnect();  
}  
```  
  
```vb  
' Define the Publisher, publication, and databases.  
Dim publicationName As String = "AdvWorksSalesOrdersMerge"  
Dim publisherName As String = publisherInstance  
Dim subscriberName As String = subscriberInstance  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
Dim hostname As String = "adventure-works\garrett1"  
Dim webSyncUrl As String = "https://" + publisherInstance + "/WebSync/replisapi.dll"  
  
'Create connections to the Publisher and Subscriber.  
Dim subscriberConn As ServerConnection = New ServerConnection(subscriberName)  
Dim publisherConn As ServerConnection = New ServerConnection(publisherName)  
  
' Create the objects that we need.  
Dim publication As MergePublication  
Dim subscription As MergePullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    subscriberConn.Connect()  
  
    ' Ensure that the publication exists and that   
    ' it supports pull subscriptions and Web synchronization.  
    publication = New MergePublication()  
    publication.Name = publicationName  
    publication.DatabaseName = publicationDbName  
    publication.ConnectionContext = publisherConn  
  
    If publication.LoadProperties() Then  
        If (publication.Attributes And PublicationAttributes.AllowPull) = 0 Then  
            publication.Attributes = publication.Attributes _  
            Or PublicationAttributes.AllowPull  
        End If  
        If (publication.Attributes And PublicationAttributes.AllowWebSynchronization) = 0 Then  
            publication.Attributes = publication.Attributes _  
            Or PublicationAttributes.AllowWebSynchronization  
        End If  
  
        ' Define the pull subscription.  
        subscription = New MergePullSubscription()  
        subscription.ConnectionContext = subscriberConn  
        subscription.PublisherName = publisherName  
        subscription.PublicationName = publicationName  
        subscription.PublicationDBName = publicationDbName  
        subscription.DatabaseName = subscriptionDbName  
        subscription.HostName = hostname  
        subscription.CreateSyncAgentByDefault = True  
  
        ' Specify the Windows login credentials for the Merge Agent job.  
        subscription.SynchronizationAgentProcessSecurity.Login = winLogin  
        subscription.SynchronizationAgentProcessSecurity.Password = winPassword  
  
        ' Enable Web synchronization.  
        subscription.UseWebSynchronization = True  
        subscription.InternetUrl = webSyncUrl  
  
        ' Specify the same Windows credentials to use when connecting to the  
        ' Web server using HTTPS Basic Authentication.  
        subscription.InternetSecurityMode = AuthenticationMethod.BasicAuthentication  
        subscription.InternetLogin = winLogin  
        subscription.InternetPassword = winPassword  
  
        ' Create the pull subscription at the Subscriber.  
        subscription.Create()  
  
        Dim registered As Boolean = False  
  
        ' Verify that the subscription is not already registered.  
        For Each existing As MergeSubscription In _  
        publication.EnumSubscriptions()  
            If existing.SubscriberName = subscriberName Then  
                registered = True  
            End If  
        Next  
        If Not registered Then  
            ' Register the local subscription with the Publisher.  
            publication.MakePullSubscriptionWellKnown( _  
             subscriberName, subscriptionDbName, _  
             SubscriptionSyncType.Automatic, _  
             MergeSubscriberType.Local, 0)  
        End If  
    Else  
        ' Do something here if the publication does not exist.  
        Throw New ApplicationException(String.Format( _  
         "The publication '{0}' does not exist on {1}.", _  
         publicationName, publisherName))  
    End If  
Catch ex As Exception  
    ' Implement the appropriate error handling here.  
    Throw New ApplicationException(String.Format( _  
     "The subscription to {0} could not be created.", publicationName), ex)  
Finally  
    subscriberConn.Disconnect()  
    publisherConn.Disconnect()  
End Try  
```  
  
## <a name="see-also"></a>参照  
 [Replication Management Objects Concepts](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [プル サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [レプリケーション セキュリティの推奨事項](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
