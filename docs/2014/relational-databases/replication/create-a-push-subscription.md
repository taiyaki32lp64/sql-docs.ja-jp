---
title: プッシュ サブスクリプションの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- push subscriptions [SQL Server replication], creating
- merge replication subscribing [SQL Server replication], push subscriptions
- subscriptions [SQL Server replication], push
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: adfbbc61-58d1-4330-9ad6-b14ab1142e2b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b571bec94c873b830654126e39d75d554599e5fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721734"
---
# <a name="create-a-push-subscription"></a>プッシュ サブスクリプションの作成
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、プッシュ サブスクリプションを作成する方法について説明します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーの詳細については、「[SQL Server 以外のサブスクライバーのサブスクリプションの作成](create-a-subscription-for-a-non-sql-server-subscriber.md)」を参照してください。  
  
  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 サブスクリプションの新規作成ウィザードを使用して、パブリッシャーまたはサブスクライバーでプッシュ サブスクリプションを作成します。 ウィザードのページに従って、次の操作を実行します。  
  
-   パブリッシャーとパブリケーションを指定します。  
  
-   レプリケーション エージェントが実行される場所を選択します。 プッシュ サブスクリプションでは、パブリケーションの種類に応じて、 **[ディストリビューション エージェントの場所]** ページまたは **[マージ エージェントの場所]** ページで **[ディストリビューター &lt;Distributor&gt; ですべてのエージェントを実行する (プッシュ サブスクリプション)]** を選択します。  
  
-   サブスクライバーとサブスクリプション データベースを指定します。  
  
-   レプリケーション エージェントによって作成された接続に対して使用されるログインとパスワードを指定します。  
  
    -   スナップショット パブリケーションとトランザクション パブリケーションに対するサブスクリプションでは、 **[ディストリビューション エージェント セキュリティ]** ページで資格情報を指定します。  
  
    -   マージ パブリケーションに対するサブスクリプションでは、 **[マージ エージェント セキュリティ]** ページで資格情報を指定します。  
  
     各エージェントで必要な権限の詳細については、「 [レプリケーション エージェント セキュリティ モデル](security/replication-agent-security-model.md)」を参照してください。  
  
-   同期スケジュール、およびサブスクライバーをいつ初期化するかを指定します。  
  
-   マージ パブリケーションの追加オプションとして、サブスクリプションの種類、およびパラメーター化されたフィルターの値を指定します。  
  
-   サブスクリプションの更新が許可されるトランザクション パブリケーションの追加オプションを指定します。サブスクライバーがパブリッシャーで変更をすぐにコミットするかどうか、変更をキューに書き込むかどうか、およびサブスクライバーからパブリッシャーへの接続に使用される資格情報を指定します。  
  
-   必要に応じて、サブスクリプションのスクリプトを作成します。  
  
#### <a name="to-create-a-push-subscription-from-the-publisher"></a>パブリッシャーからプッシュ サブスクリプションを作成するには  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。  
  
3.  1 つ以上のサブスクリプションを作成するパブリケーションを右クリックし、 **[新しいサブスクリプション]** をクリックします。  
  
4.  サブスクリプションの新規作成ウィザードのページに従って操作を実行します。  
  
#### <a name="to-create-a-push-subscription-from-the-subscriber"></a>サブスクライバーからプッシュ サブスクリプションを作成するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でサブスクライバーに接続して、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開します。  
  
3.  **[ローカル サブスクリプション]** フォルダーを右クリックし、 **[新しいサブスクリプション]** をクリックします。  
  
4.  サブスクリプションの新規作成ウィザードの **[パブリケーション]** ページで、 **[パブリッシャー]** ボックスの一覧から **[\<SQL Server パブリッシャーの検索>]** または **[\<Oracle パブリッシャーの検索>]** を選択します。  
  
5.  **[サーバーへの接続]** ダイアログ ボックスでパブリッシャーに接続します。  
  
6.  **[パブリケーション]** ページでパブリケーションを選択します。  
  
7.  サブスクリプションの新規作成ウィザードのページに従って操作を実行します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 プッシュ サブスクリプションは、レプリケーション ストアド プロシージャを使用してプログラムで作成できます。 使用するストアド プロシージャは、サブスクリプションが属するパブリケーションの種類によって変わります。  
  
> [!IMPORTANT]  
>  可能であれば、実行時にセキュリティ資格情報の入力を求めるメッセージをユーザーに対して表示します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
#### <a name="to-create-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションに対するプッシュ サブスクリプションを作成するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)を実行して、パブリケーションがプッシュ サブスクリプションをサポートしていることを確認します。  
  
    -   **allow_push** の値が **1**の場合、プッシュ サブスクリプションがサポートされます。  
  
    -   場合の値**allow_push**は**0**、実行[sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)を指定して**allow_push**の **@property** と`true`の **@value** します。  
  
2.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql)を実行します。 **@publication** 、 **@subscriber** 、および **@destination_db** を指定します。 **@subscription_type** に **push** を指定します。 サブスクリプションを更新する方法については、次を参照してください[Create an Updatable Subscription to Transactional Publication。](publish/create-an-updatable-subscription-to-a-transactional-publication.md)  
  
3.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addpushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql)を実行します。 次の指定を行います。  
  
    -   ディストリビューターで実行されるディストリビューション エージェントが使用する **@subscriber** 、 **@subscriber_db** パラメーター、および **@publication** パラメーター。  
  
    -   ディストリビューターで実行されるディストリビューション エージェントが使用する [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 資格情報。 **@job_login** に **@job_password** 」を参照してください。  
  
        > [!NOTE]  
        >  Windows 統合認証を使用して行われる接続では、常に **@job_login** 」および「 **@job_password** を使用して、SQL Server 以外のサブスクライバーのサブスクリプションを作成する方法について説明します。 ディストリビューション エージェントは、常に Windows 統合認証を使用してディストリビューターにローカル接続します。 既定では、エージェントは Windows 統合認証を使用してサブスクライバーに接続します。  
  
    -   (省略可) **0** を、 **@subscriber_security_mode** を指定し、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および **@subscriber_login** に **@subscriber_password** 」を参照してください。 サブスクライバーに接続するときに SQL Server 認証を使用する必要がある場合、これらのパラメーターを指定します。  
  
    -   このサブスクリプションでのディストリビューション エージェント ジョブのスケジュール。 詳細については、「 [Specify Synchronization Schedules](specify-synchronization-schedules.md)」を参照してください。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャー側でプッシュ サブスクリプションを作成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
#### <a name="to-create-a-push-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプッシュ サブスクリプションを作成するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql)を実行して、パブリケーションがプッシュ サブスクリプションをサポートしていることを確認します。  
  
    -   **allow_push** の値が **1**の場合、パブリケーションでプッシュ サブスクリプションがサポートされます。  
  
    -   場合の値**allow_push**ない**1**、実行[sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)を指定して**allow_push**の **@property** と`true`の **@value** します。  
  
2.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql)を実行します。次のパラメーターを指定します。  
  
    -   **@publication** 」を参照してください。 これはパブリケーションの名前です。  
  
    -   **@subscriber_type** 」を参照してください。 クライアント サブスクリプションの場合は **local** を指定し、サーバー サブスクリプションの場合は **global**を指定します。  
  
    -   **@subscription_priority** 」を参照してください。 サーバー サブスクリプションの場合、サブスクリプションの優先度 (**0.00** ～ **99.99**) を指定します。  
  
         詳細については、「 [Advanced Merge Replication Conflict Detection and Resolution](merge/advanced-merge-replication-conflict-detection-and-resolution.md)」を参照してください。  
  
3.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addmergepushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql)を実行します。 次の指定を行います。  
  
    -   手順 1. で作成した、サブスクライバーに対する **@subscriber** 、 **@subscriber_db** 、 **@publication** の各パラメーター。  
  
    -   ディストリビューターで実行されるマージ エージェントが使用する Windows 資格情報。 **@job_login** に **@job_password** 」を参照してください。  
  
        > [!NOTE]  
        >  Windows 統合認証を使用して行われる接続では、常に **@job_login** @value **@job_password** 」を参照してください。 マージ エージェントは、常に Windows 統合認証を使用してディストリビューターにローカル接続します。 既定では、エージェントは Windows 統合認証を使用してサブスクライバーに接続します。  
  
    -   (省略可) **0** を、 **@subscriber_security_mode** を指定し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および **@subscriber_login** に **@subscriber_password** 」を参照してください。 サブスクライバーに接続するときに SQL Server 認証を使用する必要がある場合、これらのパラメーターを指定します。  
  
    -   (省略可) **0** を、 **@publisher_security_mode** を指定し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および **@publisher_login** に **@publisher_password** 」を参照してください。 パブリッシャーに接続するときに SQL Server 認証を使用する必要がある場合、これらの値を指定します。  
  
    -   このサブスクリプションでのマージ エージェント ジョブのスケジュール。 詳細については、「 [Specify Synchronization Schedules](specify-synchronization-schedules.md)」を参照してください。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャー側でプッシュ サブスクリプションを作成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、トランザクション パブリケーションに対するプッシュ サブスクリプションを作成します。 ログインとパスワードの値は、実行時に **sqlcmd** スクリプト変数を使用して入力されます。  
  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpushsub.sql#sp_addtranpushsubscription_agent)]  
  
 次の例では、マージ パブリケーションに対するプッシュ サブスクリプションを作成します。 ログインとパスワードの値は、実行時に **sqlcmd** スクリプト変数を使用して入力されます。  
  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepushsub.sql#sp_addmergepushsubscriptionagent)]  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 レプリケーション管理オブジェクト (RMO) を使用することで、プログラムによってプッシュ サブスクリプションを作成できます。 プッシュ サブスクリプションを作成する際に使用する RMO クラスは、作成するサブスクリプションの対象となるパブリケーションの種類によって異なります。  
  
> [!IMPORTANT]  
>  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 資格情報を保存する必要がある場合は、 [Windows .NET&#xA0;Framework に用意されている](https://go.microsoft.com/fwlink/?LinkId=34733) 暗号化サービス [!INCLUDE[msCoName](../../includes/msconame-md.md)] を使用します。  
  
#### <a name="to-create-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションに対するプッシュ サブスクリプションを作成するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  手順 1. のパブリッシャー接続を使用して、 <xref:Microsoft.SqlServer.Replication.TransPublication> クラスのインスタンスを作成します。 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>、および <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>を指定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出します。 このメソッドが戻る場合`false`、手順 2. で指定したプロパティが正しくないか、パブリケーションがサーバーに存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> プロパティと <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush> のビットごとの論理積演算 (Visual C# では `&`、Visual Basic では `And`) を実行します。 結果が <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None> の場合、<xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> と <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> のビットごとの論理和演算 (Visual C# では `|`、Visual Basic では `Or`) の結果を <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush> に設定します。 次に、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> を呼び出してプッシュ サブスクリプションを有効にします。  
  
5.  サブスクリプション データベースが存在しない場合は、 <xref:Microsoft.SqlServer.Management.Smo.Database> クラスを使用して作成します。 詳細については、「[データベースの作成、変更、および削除](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)」を参照してください。  
  
6.  <xref:Microsoft.SqlServer.Replication.TransSubscription> クラスのインスタンスを作成します。  
  
7.  次のサブスクリプション プロパティを設定します。  
  
    -   手順 1. で作成した、パブリッシャーに対する <xref:Microsoft.SqlServer.Management.Common.ServerConnection> を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>に指定します。  
  
    -   サブスクリプション データベース名を <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>に指定します。  
  
    -   サブスクライバー名を <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>に指定します。  
  
    -   パブリケーション データベース名を <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>に指定します。  
  
    -   パブリケーション名を <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>に指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> の <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> (または <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>) フィールド。これにより、ディストリビューターでディストリビューション エージェントを実行するときに使用される [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントの資格情報が得られます。 このアカウントは、ディストリビューターとのローカル接続を確立したり、Windows 認証を使用したリモート接続を確立するときに使用されます。  
  
        > [!NOTE]  
        >  サブスクリプションが `sysadmin` 固定サーバー ロールのメンバーにより作成される場合、<xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> の設定は必須ではありませんが、推奨されます。 この場合、エージェントは SQL Server エージェントのアカウントを借用します。 詳細については、「 [レプリケーション エージェント セキュリティ モデル](security/replication-agent-security-model.md)」を参照してください。  
  
    -   (省略可) サブスクリプションを同期するために使用されるエージェント ジョブを作成する場合は、<xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> に `true` (既定値) を指定します。 `false` を指定した場合、サブスクリプションはプログラムでのみ同期が可能になります。  
  
    -   (省略可) SQL Server 認証を使用してサブスクライバーに接続する場合、 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> の <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (または <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> ) フィールドを設定します。  
  
8.  <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> メソッドを呼び出します。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャー側でプッシュ サブスクリプションを作成する場合は、 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>を含むすべてのプロパティに指定された値がディストリビューターにプレーン テキストとして送信されます。 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> メソッドを呼び出す前に、パブリッシャーとリモート ディストリビューター間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
#### <a name="to-create-a-push-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプッシュ サブスクリプションを作成するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  手順 1. のパブリッシャー接続を使用して、 <xref:Microsoft.SqlServer.Replication.MergePublication> クラスのインスタンスを作成します。 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>、および <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>を指定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出します。 このメソッドが戻る場合`false`、手順 2. で指定したプロパティが正しくないか、パブリケーションがサーバーに存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> プロパティと <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush> のビットごとの論理積演算 (Visual C# では `&`、Visual Basic では `And`) を実行します。 結果が <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None> の場合、<xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> と <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> のビットごとの論理和演算 (Visual C# では `|`、Visual Basic では `Or`) の結果を <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush> に設定します。 次に、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> を呼び出してプッシュ サブスクリプションを有効にします。  
  
5.  サブスクリプション データベースが存在しない場合は、 <xref:Microsoft.SqlServer.Management.Smo.Database> クラスを使用して作成します。 詳細については、「[データベースの作成、変更、および削除](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)」を参照してください。  
  
6.  <xref:Microsoft.SqlServer.Replication.MergeSubscription> クラスのインスタンスを作成します。  
  
7.  次のサブスクリプション プロパティを設定します。  
  
    -   手順 1. で作成した、パブリッシャーに対する <xref:Microsoft.SqlServer.Management.Common.ServerConnection> を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>に指定します。  
  
    -   サブスクリプション データベース名を <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>に指定します。  
  
    -   サブスクライバー名を <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>に指定します。  
  
    -   パブリケーション データベース名を <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>に指定します。  
  
    -   パブリケーション名を <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>に指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> の <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> (または <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>) フィールド。これにより、ディストリビューターでマージ エージェントを実行するときに使用される [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントの資格情報が得られます。 このアカウントは、ディストリビューターとのローカル接続を確立したり、Windows 認証を使用したリモート接続を確立するときに使用されます。  
  
        > [!NOTE]  
        >  サブスクリプションが `sysadmin` 固定サーバー ロールのメンバーにより作成される場合、<xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> の設定は必須ではありませんが、推奨されます。 この場合、エージェントは SQL Server エージェントのアカウントを借用します。 詳細については、「 [レプリケーション エージェント セキュリティ モデル](security/replication-agent-security-model.md)」を参照してください。  
  
    -   (省略可) サブスクリプションを同期するために使用されるエージェント ジョブを作成する場合は、<xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> に `true` (既定値) を指定します。 `false` を指定した場合、サブスクリプションはプログラムでのみ同期が可能になります。  
  
    -   (省略可) SQL Server 認証を使用してサブスクライバーに接続する場合、 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> の <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (または <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> ) フィールドを設定します。  
  
    -   (省略可) SQL Server 認証を使用してパブリッシャーに接続する場合、 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> の <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (または <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> ) フィールドを設定します。  
  
8.  <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> メソッドを呼び出します。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャー側でプッシュ サブスクリプションを作成する場合は、 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>を含むすべてのプロパティに指定された値がディストリビューターにプレーン テキストとして送信されます。 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> メソッドを呼び出す前に、パブリッシャーとリモート ディストリビューター間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 次の例では、トランザクション パブリケーションに対する新しいプッシュ サブスクリプションを作成します。 ディストリビューション エージェント ジョブを実行するために使用される Windows アカウントの資格情報は、実行時に渡されます。  
  
 [!code-csharp[HowTo#rmo_CreateTranPushSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createtranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPushSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createtranpushsub)]  
  
 次の例では、マージ パブリケーションに対する新しいプッシュ サブスクリプションを作成します。 マージ エージェント ジョブを実行するために使用される Windows アカウントの資格情報は、実行時に渡されます。  
  
 [!code-csharp[HowTo#rmo_CreateMergePushSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## <a name="see-also"></a>参照  
 [プッシュ サブスクリプションのプロパティの表示または変更](view-and-modify-push-subscription-properties.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [Create a Publication](publish/create-a-publication.md)   
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [プッシュ サブスクリプションの同期](synchronize-a-push-subscription.md)   
 [パブリケーションのサブスクライブ](subscribe-to-publications.md)   
 [sqlcmd でのスクリプト変数の使用](../scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
