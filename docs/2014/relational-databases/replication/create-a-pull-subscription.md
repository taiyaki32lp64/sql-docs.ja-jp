---
title: プル サブスクリプションの作成 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: f8868957d7c479de3a51a599deed42c34d6676eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721594"
---
# <a name="create-a-pull-subscription"></a>プル サブスクリプションの作成
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
  
     各エージェントで必要な権限の詳細については、「 [レプリケーション エージェント セキュリティ モデル](security/replication-agent-security-model.md)」を参照してください。  
  
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
  
1.  パブリッシャーで、 [sp_helppublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql) を実行することにより、パブリケーションがプル サブスクリプションをサポートしていることを確認します。  
  
    -   結果セットの **allow_pull** の値が **1**である場合、パブリケーションはプル サブスクリプションをサポートします。  
  
    -   場合の値**allow_pull**は**0**、実行[sp_changepublication &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)を指定して**allow_pull**の **@property** と`true`の **@value** します。  
  
2.  サブスクライバーで、[sp_addpullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql) を実行します。 **@publisher** および **@publication** を指定します。 サブスクリプションの更新の詳細については、「 [トランザクション パブリケーションの更新可能なサブスクリプションの作成](publish/create-an-updatable-subscription-to-a-transactional-publication.md)」を参照してください。  
  
3.  サブスクライバーで、[sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql) を実行します。 次の指定を行います。  
  
    -   手順 1. で作成した、サブスクライバーに対する **@publisher** 、 **@publisher_db** 、 **@publication** の各パラメーター。  
  
    -   手順 1. で作成した、サブスクライバーに対する [!INCLUDE[msCoName](../../includes/msconame-md.md)] @job_login **@job_login** @value **@job_password** 」を参照してください。  
  
        > [!NOTE]  
        >  Windows 統合認証を使用して行われる接続では、常に **@job_login** @value **@job_password** 」を参照してください。 ディストリビューション エージェントは、常に Windows 統合認証を使用してサブスクライバーへのローカル接続を作成します。 既定では、エージェントは Windows 統合認証を使用してディストリビューターに接続します。  
  
    -   (省略可能)値**0**の **@distributor_security_mode** と[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のログイン情報 **@distributor_login** と **@distributor_password** を使用する必要がある場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ディストリビューターに接続するときに認証します。  
  
    -   このサブスクリプションでのディストリビューション エージェント ジョブのスケジュール。 詳細については、「 [Specify Synchronization Schedules](specify-synchronization-schedules.md)」を参照してください。  
  
4.  パブリッシャー側で [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) を実行し、プル サブスクリプションを登録します。 **@publication** 、 **@subscriber** 、および **@destination_db** を指定します。 **@subscription_type** に **pull** を指定します。  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプル サブスクリプションを作成するには  
  
1.  パブリッシャーで、[sp_helpmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql) を実行することにより、パブリケーションがプル サブスクリプションをサポートしていることを確認します。  
  
    -   結果セットの **allow_pull** の値が **1**である場合、パブリケーションはプル サブスクリプションをサポートします。  
  
    -   場合の値**allow_pull**は**0**、実行[sp_changemergepublication &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)を指定して**allow_pull**の **@property** と`true`の **@value** します。  
  
2.  サブスクライバーで、[sp_addmergepullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql) を実行します。 **@publisher** 、 **@publisher_db** 、 **@publication** 、および以下のパラメーターを指定します。  
  
    -   **@subscriber_type** クライアント サブスクリプションには **local** を指定し、サーバー サブスクリプションには **global** を指定します。  
  
    -   **@subscription_priority** - サブスクリプションの優先度 (**0.00** - **99.99**) を指定します。 これは、サーバー サブスクリプションにのみ必要です。  
  
         詳細については、「 [マージ レプリケーションの競合検出および解決の詳細](merge/advanced-merge-replication-conflict-detection-and-resolution.md)」を参照してください。  
  
3.  サブスクライバーで、 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql) を実行します。 次のパラメーターを指定します。  
  
    -   **@publisher** 、 **@publisher_db** 、 **@publication** 」を参照してください。  
  
    -   **@job_login** および **@job_password** のサブスクライバーでマージ エージェントが実行されるときの Windows 資格情報。  
  
        > [!NOTE]  
        >  Windows 統合認証を使用して行われる接続では、常に **@job_login** 」および「 **@job_password** を使用して、SQL Server 以外のサブスクライバーのサブスクリプションを作成する方法について説明します。 マージ エージェントは、常に Windows 統合認証を使用してサブスクライバーへのローカル接続を作成します。 既定では、エージェントは Windows 統合認証を使用してディストリビューターおよびパブリッシャーに接続します。  
  
    -   (省略可) ディストリビューターへの接続時に **0** allow_pull **@distributor_security_mode** 0 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] @distributor_login **@distributor_login** @value **@distributor_password** に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン情報。  
  
    -   (省略可) ディストリビューターへの接続時に **0** allow_pull **@publisher_security_mode** 0 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] @distributor_login **@publisher_login** @value **@publisher_password** に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン情報。  
  
    -   このサブスクリプションでのマージ エージェント ジョブのスケジュール。 詳しくは、「 [トランザクション パブリケーションの更新可能なサブスクリプションの作成](publish/create-an-updatable-subscription-to-a-transactional-publication.md)」をご覧ください。  
  
4.  パブリッシャーで [sp_addmergesubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql) を実行します。 **@publication** 、 **@subscriber** 、 **@subscriber_db** 、および **@subscription_type** に **pull** 値を指定します。 これにより、プル サブスクリプションが登録されます。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、トランザクション パブリケーションに対するプル サブスクリプションを作成します。 最初のバッチはサブスクライバーで実行され、2 番目のバッチはパブリッシャーで実行されます。 ログインとパスワードの値は、実行時に sqlcmd スクリプト変数を使用して入力されます。  
  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpullsub.sql#sp_addtranpullsubscriptionagent)]  
  
 [!code-sql[HowTo#sp_addtranpullsubscription](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpullsub.sql#sp_addtranpullsubscription)]  
  
 次の例では、マージ パブリケーションに対するプル サブスクリプションを作成します。 最初のバッチはサブスクライバーで実行され、2 番目のバッチはパブリッシャーで実行されます。 ログインとパスワードの値は、実行時に **sqlcmd** スクリプト変数を使用して入力されます。  
  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsub.sql#sp_addmergepullsubscriptionagent)]  
  
 [!code-sql[HowTo#sp_addmergepullsubscription](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsub.sql#sp_addmergepullsubscription)]  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 プル サブスクリプションの作成に使用する RMO のクラスは、サブスクリプションが属しているパブリケーションの種類によって異なります。  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションに対するプル サブスクリプションを作成するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、サブスクライバーおよびパブリッシャーへの接続を作成します。  
  
2.  手順 1. のパブリッシャー接続を使用して、 <xref:Microsoft.SqlServer.Replication.TransPublication> クラスのインスタンスを作成します。 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 、および <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>を指定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出します。 このメソッドが `false` を返す場合、手順 2. で指定したプロパティが誤っているか、サーバーにパブリケーションが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> プロパティと <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull> のビットごとの論理積演算 (Visual C# では `&`、Visual Basic では `And`) を実行します。 結果が <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None> の場合、<xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> と <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> のビットごとの論理和演算 (Visual C# では `|`、Visual Basic では `Or`) の結果を <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull> に設定します。 続けて、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> を呼び出して、プル サブスクリプションを有効にします。  
  
5.  サブスクリプション データベースが存在しない場合は、 <xref:Microsoft.SqlServer.Management.Smo.Database> クラスを使用して作成します。 詳細については、「[データベースの作成、変更、および削除](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)」を参照してください。  
  
6.  <xref:Microsoft.SqlServer.Replication.TransPullSubscription> クラスのインスタンスを作成します。  
  
7.  次のサブスクリプション プロパティを設定します。  
  
    -   手順 1. で作成した、サブスクライバーに対する <xref:Microsoft.SqlServer.Management.Common.ServerConnection> を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>に指定します。  
  
    -   サブスクリプション データベース名を <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>に指定します。  
  
    -   パブリッシャー名を <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>に指定します。  
  
    -   パブリケーション データベース名を <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>に指定します。  
  
    -   パブリケーション名を <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>に指定します。  
  
    -   サブスクライバーで実行されるディストリビューション エージェントが使用するための [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントの資格情報を <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> の <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> (または <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>) フィールドに指定します。 このアカウントは、サブスクライバーとのローカル接続を確立したり、Windows 認証を使用したリモート接続を確立するときに使用されます。  
  
        > [!NOTE]  
        >  サブスクリプションが `sysadmin` 固定サーバー ロールのメンバーにより作成される場合、<xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> の設定は必須ではありませんが、推奨されます。 この場合、エージェントは SQL Server エージェントのアカウントを借用します。 詳細については、「 [レプリケーション エージェント セキュリティ モデル](security/replication-agent-security-model.md)」を参照してください。  
  
    -   (省略可) サブスクリプションを同期するためのエージェント ジョブを作成する場合は、<xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> の値に `true` を指定します。 `false` (既定値) を指定した場合、サブスクリプションはプログラムによってのみ同期できます。また、このオブジェクトに <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> プロパティからアクセスする場合は、<xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A> のプロパティを別途指定する必要があります。 詳細については、「 [プル サブスクリプションの同期](synchronize-a-pull-subscription.md)」をご覧ください。  
  
        > [!NOTE]  
        >  SQL Server エージェントは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]」を参照してください。 エディションでサポートされている機能の一覧については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[機能は、SQL Server 2014 の各エディションでサポートされている](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。 Express のサブスクライバーに対して値 `true` を指定しても、エージェント ジョブは作成されません。 ただし、サブスクリプション関連の重要なメタデータについてはサブスクライバーに保存されます。  
  
    -   (省略可) SQL Server 認証を使ってディストリビューターに接続する場合は、 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> の <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (または <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> ) フィールドを設定します。  
  
8.  <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> メソッドを呼び出します。  
  
9. 手順 2. で作成した <xref:Microsoft.SqlServer.Replication.TransPublication> クラスのインスタンスを使用して、 <xref:Microsoft.SqlServer.Replication.TransPublication.MakePullSubscriptionWellKnown%2A> メソッドを呼び出し、パブリッシャーにプル サブスクリプションを登録します。 既に登録されている場合は、例外が発生します。  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプル サブスクリプションを作成するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、サブスクライバーとパブリッシャーの両方に対する接続を作成します。  
  
2.  手順 1. のパブリッシャー接続を使用して、 <xref:Microsoft.SqlServer.Replication.MergePublication> クラスのインスタンスを作成します。 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>、および <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>を指定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出します。 このメソッドが `false` を返す場合、手順 2. で指定したプロパティが誤っているか、サーバーにパブリケーションが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> プロパティと <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull> のビットごとの論理積演算 (Visual C# では `&`、Visual Basic では `And`) を実行します。 結果が <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None> の場合、<xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> と <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> のビットごとの論理和演算 (Visual C# では `|`、Visual Basic では `Or`) の結果を <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull> に設定します。 続けて、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> を呼び出して、プル サブスクリプションを有効にします。  
  
5.  サブスクリプション データベースが存在しない場合は、 <xref:Microsoft.SqlServer.Management.Smo.Database> クラスを使用して作成します。 詳細については、「[データベースの作成、変更、および削除](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)」を参照してください。  
  
6.  <xref:Microsoft.SqlServer.Replication.MergePullSubscription> クラスのインスタンスを作成します。  
  
7.  次のサブスクリプション プロパティを設定します。  
  
    -   手順 1. で作成した、サブスクライバーに対する <xref:Microsoft.SqlServer.Management.Common.ServerConnection> を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>に指定します。  
  
    -   サブスクリプション データベース名を <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>に指定します。  
  
    -   パブリッシャー名を <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>に指定します。  
  
    -   パブリケーション データベース名を <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>に指定します。  
  
    -   パブリケーション名を <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>に指定します。  
  
    -   サブスクライバーで実行されるマージ エージェントが使用するための [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントの資格情報を <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> の <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> (または <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>) フィールドに指定します。 このアカウントは、サブスクライバーとのローカル接続を確立したり、Windows 認証を使用したリモート接続を確立するときに使用されます。  
  
        > [!NOTE]  
        >  サブスクリプションが `sysadmin` 固定サーバー ロールのメンバーにより作成される場合、<xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> の設定は必須ではありませんが、推奨されます。 この場合、エージェントは SQL Server エージェントのアカウントを借用します。 詳細については、「 [レプリケーション エージェント セキュリティ モデル](security/replication-agent-security-model.md)」を参照してください。  
  
    -   (省略可) サブスクリプションを同期するためのエージェント ジョブを作成する場合は、<xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> の値に `true` を指定します。 `false` (既定値) を指定した場合、サブスクリプションはプログラムによってのみ同期できます。また、このオブジェクトに <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> プロパティからアクセスする場合は、<xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A> のプロパティを別途指定する必要があります。 詳細については、「 [プル サブスクリプションの同期](synchronize-a-pull-subscription.md)」をご覧ください。  
  
    -   (省略可) SQL Server 認証を使ってディストリビューターに接続する場合は、 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> の <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (または <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> ) フィールドを設定します。  
  
    -   (省略可) SQL Server 認証を使用してパブリッシャーに接続する場合、 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> の <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (または <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> ) フィールドを設定します。  
  
8.  <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> メソッドを呼び出します。  
  
9. 手順 2. で作成した <xref:Microsoft.SqlServer.Replication.MergePublication> クラスのインスタンスを使用して、 <xref:Microsoft.SqlServer.Replication.MergePublication.MakePullSubscriptionWellKnown%2A> メソッドを呼び出し、パブリッシャーにプル サブスクリプションを登録します。 既に登録されている場合は、例外が発生します。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 次の例では、トランザクション パブリケーションに対するプル サブスクリプションを作成します。 ディストリビューション エージェント ジョブを作成するために使用する [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントの資格情報は実行時に渡されます。  
  
 [!code-csharp[HowTo#rmo_CreateTranPullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createtranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createtranpullsub)]  
  
 次の例では、マージ パブリケーションに対するプル サブスクリプションを作成します。 マージ エージェント ジョブを作成するために使用する Windows アカウントの資格情報は実行時に渡されます。  
  
 [!code-csharp[HowTo#rmo_CreateMergePullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepullsub)]  
  
 次の例では、関連するエージェント ジョブやサブスクリプション メタデータを [MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql)に作成せずに、マージ パブリケーションに対するプル サブスクリプションを作成しています。 マージ エージェント ジョブを作成するために使用する Windows アカウントの資格情報は実行時に渡されます。  
  
 [!code-csharp[HowTo#rmo_CreateMergePullSub_NoJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepullsub_nojob)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePullSub_NoJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepullsub_nojob)]  
  
 次の例では、Web 同期によるインターネットを介した同期が可能な、マージ パブリケーションに対するプル サブスクリプションを作成しています。 マージ エージェント ジョブを作成するために使用する Windows アカウントの資格情報は実行時に渡されます。 詳しくは、「 [Configure Web Synchronization](configure-web-synchronization.md)」をご覧ください。  
  
 [!code-csharp[HowTo#rmo_CreateMergePullSub_WebSync](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepullsub_websync)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePullSub_WebSync](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepullsub_websync)]  
  
## <a name="see-also"></a>参照  
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [プル サブスクリプションのプロパティの表示または変更](view-and-modify-pull-subscription-properties.md)   
 [Configure Web Synchronization](configure-web-synchronization.md)   
 [Subscribe to Publications](subscribe-to-publications.md)   
 [レプリケーション セキュリティの推奨事項](security/replication-security-best-practices.md)  
  
  
