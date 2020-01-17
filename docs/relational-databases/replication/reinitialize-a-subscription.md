---
title: サブスクリプションの再初期化 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- initializing subscriptions [SQL Server replication], reinitializing
- subscriptions [SQL Server replication], reinitializing
- reinitializing subscriptions
ms.assetid: ca3625c5-c62e-4ab7-9829-d511f838e385
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 733e63f6dd01c09fd007a7176721533f7a1c57d3
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846508"
---
# <a name="reinitialize-a-subscription"></a>サブスクリプションの再初期化
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、サブスクリプションを再初期化する方法について説明します。 次回の同期で新しいスナップショットが適用されるように、個別のサブスクリプションに再初期化のマークを付けることができます。  
  
[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]


  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 サブスクリプションの再初期化には、2 段階の処理があります。  
  
1.  パブリケーションの単一のサブスクリプションまたはすべてのサブスクリプションが再初期化対象として *マーク* されます。 サブスクリプションの再初期化のマークを設定するには、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の **[ローカル パブリケーション]** フォルダーおよび **[ローカル サブスクリプション]** フォルダーから **[サブスクリプションの再初期化]** ダイアログ ボックスを使用します。 また、 **[すべてのサブスクリプション]** タブやレプリケーション モニターのパブリケーション ノードからマークを設定することもできます。 レプリケーション モニターの起動の詳細については、「[Start the Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)」 (レプリケーション モニターの開始) を参照してください。 サブスクリプションの再初期化の設定には、以下のオプションがあります。  
  
     **[現在のスナップショットを使用する]**  
     このオプションを選択すると、次にディストリビューション エージェントまたはマージ エージェントが実行されたときに、現在のスナップショットがサブスクライバーに適用されます。 有効なスナップショットが使用できない場合、このオプションは選択できません。  
  
     **[新しいスナップショットを使用する]**  
     このオプションを選択すると、新しいスナップショットによってサブスクリプションが再初期化されます。 スナップショットは、スナップショット エージェントによって生成された後にだけ、サブスクライバーに適用できます。 スナップショットがスケジュールに従って実行されるように設定している場合は、スナップショット エージェントが次回実行されて終了するまでサブスクリプションを再初期化できません。 スナップショット エージェントをすぐに開始するには、 **[今すぐ新しいスナップショットを生成する]** を選択します。  
  
     **[再初期化する前に、同期されていない変更をアップロード]**  
     マージ レプリケーションのみです。 このオプションを選択すると、サブスクライバーのデータがスナップショットで上書きされる前に、保留中の変更がサブスクリプション データベースからアップロードされます。  
  
     パラメーター化フィルターを追加、削除、変更する場合は、再初期化の際、サブスクライバーで保留中の変更をパブリッシャーにアップロードできません。 保留中の変更をアップロードしたい場合は、フィルターを変更する前にすべてのサブスクリプションを同期してください。  
  
2.  サブスクリプションは、次回同期されるときに再初期化されます。ディストリビューション エージェント (トランザクション レプリケーションの場合) またはマージ エージェント (マージ レプリケーションの場合) により、再初期化するように設定されている各サブスクライバーに最新のスナップショットが適用されます。 サブスクリプションの同期の詳細については、「 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md) 」および「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)ダイアログ ボックスを使用します。  
  
#### <a name="to-mark-a-single-push-or-pull-subscription-for-reinitialization-in-management-studio-at-the-publisher"></a>Management Studio で単一のプッシュ サブスクリプションまたはプル サブスクリプションに再初期化を設定するには (パブリッシャーで実行)  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。  
  
3.  再初期化するサブスクリプションが含まれているパブリケーションを展開します。  
  
4.  サブスクリプションを右クリックし、 **[再初期化]** をクリックします。  
  
5.  **[サブスクリプションの再初期化]** ダイアログ ボックスでオプションを選択し、 **[再初期化するように設定]** をクリックします。  
  
#### <a name="to-mark-a-single-pull-subscription-for-reinitialization-in-management-studio-at-the-subscriber"></a>Management Studio で単一のプル サブスクリプションに再初期化を設定するには (サブスクライバーで実行)  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でサブスクライバーに接続して、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル サブスクリプション]** フォルダーを展開します。  
  
3.  サブスクリプションを右クリックし、 **[再初期化]** をクリックします。  
  
4.  表示される確認のダイアログ ボックスで、 **[はい]** をクリックします。  
  
#### <a name="to-mark-all-subscriptions-for-reinitialization-in-management-studio"></a>Management Studio ですべてのサブスクリプションに再初期化を設定するには  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。  
  
3.  サブスクリプションを再初期化するパブリケーションを右クリックし、 **[すべてのサブスクリプションの再初期化]** をクリックします。  
  
4.  **[サブスクリプションの再初期化]** ダイアログ ボックスでオプションを選択し、 **[再初期化するように設定]** をクリックします。  
  
#### <a name="to-mark-a-single-push-or-pull-subscription-for-reinitialization-in-replication-monitor"></a>レプリケーション モニターで単一のプッシュ サブスクリプションまたはプル サブスクリプションに再初期化を設定するには  
  
1.  レプリケーション モニターで、左ペインのパブリッシャー グループを展開し、パブリッシャーを展開してパブリケーションをクリックします。  
  
2.  **[すべてのサブスクリプション]** タブをクリックします。  
  
3.  再初期化するサブスクリプションを右クリックし、 **[サブスクリプションの再初期化]** をクリックします。  
  
4.  **[サブスクリプションの再初期化]** ダイアログ ボックスでオプションを選択し、 **[再初期化するように設定]** をクリックします。  
  
#### <a name="to-mark-all-subscriptions-for-reinitialization-in-replication-monitor"></a>レプリケーション モニターですべてのサブスクリプションに再初期化を設定するには  
  
1.  レプリケーション モニターの左ペインでパブリッシャー グループを展開し、パブリッシャーを展開します。  
  
2.  サブスクリプションを再初期化するパブリケーションを右クリックし、 **[すべてのサブスクリプションの再初期化]** をクリックします。  
  
3.  **[サブスクリプションの再初期化]** ダイアログ ボックスでオプションを選択し、 **[再初期化するように設定]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 サブスクリプションは、プログラムでレプリケーション ストアド プロシージャを使用して再初期化できます。 使用するストアド プロシージャは、サブスクリプションの種類 (プッシュまたはプル) およびサブスクリプションが属しているパブリケーションの種類によって変わります。  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-transactional-publication"></a>トランザクション パブリケーションに対するプル サブスクリプションを再初期化するには  
  
1.  サブスクライバー側のサブスクリプション データベースに対して、[sp_reinitpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-reinitpullsubscription-transact-sql.md) を実行します。 **\@publisher**、 **\@publisher_db**、 **\@publication** を指定します。 これにより、ディストリビューション エージェントの次回実行時に再初期化するようにサブスクリプションにマークが付けられます。  
  
2.  (省略可) サブスクライバーでディストリビューション エージェントを起動し、サブスクリプションを同期します。 詳細については、「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)」をご覧ください。  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-transactional-publication"></a>トランザクション パブリケーションに対するプッシュ サブスクリプションを再初期化するには  
  
1.  パブリッシャーで、[sp_reinitsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-reinitsubscription-transact-sql.md) を実行します。 **\@publication**、 **\@subscriber**、および **\@destination_db** を指定します。 これにより、ディストリビューション エージェントの次回実行時に再初期化するようにサブスクリプションにマークが付けられます。  
  
2.  (省略可) ディストリビューターでディストリビューション エージェントを起動し、サブスクリプションを同期します。 詳細については、「 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)」をご覧ください。  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプル サブスクリプションを再初期化するには  
  
1.  サブスクライバー側のサブスクリプション データベースに対して、[sp_reinitmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-reinitmergepullsubscription-transact-sql.md) を実行します。 **\@publisher**、 **\@publisher_db**、 **\@publication** を指定します。 再初期化が実行される前にサブスクライバーの変更をアップロードする場合は、 **\@upload_first** に **true** の値を指定します。 これにより、マージ エージェントの次回実行時に再初期化するようにサブスクリプションにマークが付けられます。  
  
    > [!IMPORTANT]  
    >  パラメーター化フィルターを追加、削除、変更する場合は、再初期化の際、サブスクライバーで保留中の変更をパブリッシャーにアップロードできません。 保留中の変更をアップロードしたい場合は、フィルターを変更する前にすべてのサブスクリプションを同期してください。  
  
2.  (省略可) サブスクライバーでマージ エージェントを起動し、サブスクリプションを同期します。 詳細については、「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)」をご覧ください。  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプッシュ サブスクリプションを再初期化するには  
  
1.  パブリッシャーで、[sp_reinitmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-reinitmergesubscription-transact-sql.md) を実行します。 **\@publication**、 **\@subscriber**、 **\@subscriber_db** を指定します。 再初期化が実行される前にサブスクライバーの変更をアップロードする場合は、 **\@upload_first** に **true** の値を指定します。 これにより、ディストリビューション エージェントの次回実行時に再初期化するようにサブスクリプションにマークが付けられます。  
  
    > [!IMPORTANT]  
    >  パラメーター化フィルターを追加、削除、変更する場合は、再初期化の際、サブスクライバーで保留中の変更をパブリッシャーにアップロードできません。 保留中の変更をアップロードしたい場合は、フィルターを変更する前にすべてのサブスクリプションを同期してください。  
  
2.  (省略可) ディストリビューターでマージ エージェントを起動し、サブスクリプションを同期します。 詳細については、「 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)」をご覧ください。  
  
#### <a name="to-set-the-reinitialization-policy-when-creating-a-new-merge-publication"></a>新しいマージ パブリケーションを作成するときに再初期化ポリシーを設定するには  
  
1.  パブリッシャー側のパブリケーション データベースで、[sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) を実行し、次のいずれかの値を **\@automatic_reinitialization_policy** に指定します。  
  
    -   **1** - パブリケーションに対する変更に応じてサブスクリプションが自動的に再初期化される前に、サブスクライバーの変更がアップロードされます。  
  
    -   **0** - パブリケーションに対する変更に応じてサブスクリプションが自動的に再初期化されるときに、サブスクライバーの変更は破棄されます。  
  
    > [!IMPORTANT]  
    >  パラメーター化フィルターを追加、削除、変更する場合は、再初期化の際、サブスクライバーで保留中の変更をパブリッシャーにアップロードできません。 保留中の変更をアップロードしたい場合は、フィルターを変更する前にすべてのサブスクリプションを同期してください。  
  
     詳しくは、「 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)」をご覧ください。  
  
#### <a name="to-change-the-reinitialization-policy-for-an-existing-merge-publication"></a>既存のマージ パブリケーションの再初期化ポリシーを変更するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して [sp_changemergepublication](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) を実行します。 **\@property** に **automatic_reinitialization_policy** を指定し、次のいずれかの値を **\@value** に指定します。  
  
    -   **1** - パブリケーションに対する変更に応じてサブスクリプションが自動的に再初期化される前に、サブスクライバーの変更がアップロードされます。  
  
    -   **0** - パブリケーションに対する変更に応じてサブスクリプションが自動的に再初期化されるときに、サブスクライバーの変更は破棄されます。  
  
    > [!IMPORTANT]  
    >  パラメーター化フィルターを追加、削除、変更する場合は、再初期化の際、サブスクライバーで保留中の変更をパブリッシャーにアップロードできません。 保留中の変更をアップロードしたい場合は、フィルターを変更する前にすべてのサブスクリプションを同期してください。  
  
     詳しくは、「 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」をご覧ください。  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 次回の同期で新しいスナップショットが適用されるように、個別のサブスクリプションに再初期化のマークを付けることができます。 レプリケーション管理オブジェクト (RMO) を使用することで、プログラムによってサブスクリプションを再初期化できます。 使用するクラスは、サブスクリプションが属するパブリケーションの種類と、サブスクリプションの種類 (プッシュ サブスクリプションまたはプル サブスクリプション) に応じて変わります。  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-transactional-publication"></a>トランザクション パブリケーションに対するプル サブスクリプションを再初期化するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、サブスクライバーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPullSubscription> クラスのインスタンスを作成し、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>を設定して、手順 1. の接続を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>に設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。  
  
    > [!NOTE]  
    >  このメソッドが **false**を返す場合、手順 2. でサブスクリプション プロパティを不適切に設定したか、プル サブスクリプションが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.TransPullSubscription.Reinitialize%2A> メソッドを呼び出します。 このメソッドにより、サブスクリプションを再初期化するようにマークされます。  
  
5.  プル サブスクリプションを同期します。 詳細については、「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)」をご覧ください。  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-transactional-publication"></a>トランザクション パブリケーションに対するプッシュ サブスクリプションを再初期化するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.TransSubscription> クラスのインスタンスを作成し、 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>を設定して、手順 1. の接続を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>に設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。  
  
    > [!NOTE]  
    >  このメソッドが **false**を返す場合、手順 2. でサブスクリプション プロパティを不適切に設定したか、プッシュ サブスクリプションが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.TransSubscription.Reinitialize%2A> メソッドを呼び出します。 このメソッドにより、サブスクリプションを再初期化するようにマークされます。  
  
5.  プッシュ サブスクリプションを同期します。 詳しくは、「 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)」をご覧ください。  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプル サブスクリプションを再初期化するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、サブスクライバーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePullSubscription> クラスのインスタンスを作成し、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>を設定して、手順 1. の接続を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>に設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。  
  
    > [!NOTE]  
    >  このメソッドが **false**を返す場合、手順 2. でサブスクリプション プロパティを不適切に設定したか、プル サブスクリプションが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.MergePullSubscription.Reinitialize%2A> メソッドを呼び出します。 再初期化の前に **true** を渡してサブスクライバーの変更をアップロードするか、 **false** を渡して再初期化し、サブスクライバーの保留中の変更をすべて破棄します。 このメソッドにより、サブスクリプションを再初期化するようにマークされます。  
  
    > [!NOTE]  
    >  サブスクリプションの有効期限が切れると、変更をアップロードできません。 詳しくは、「 [Set the Expiration Period for Subscriptions](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)」をご覧ください。  
  
5.  プル サブスクリプションを同期します。 詳しくは、「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)」をご覧ください。  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプッシュ サブスクリプションを再初期化するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeSubscription> クラスのインスタンスを作成し、 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>を設定して、手順 1. の接続を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>に設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。  
  
    > [!NOTE]  
    >  このメソッドが **false**を返す場合、手順 2. でサブスクリプション プロパティを不適切に設定したか、プッシュ サブスクリプションが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.MergeSubscription.Reinitialize%2A> メソッドを呼び出します。 再初期化の前に **true** を渡してサブスクライバーの変更をアップロードするか、 **false** を渡して再初期化し、サブスクライバーの保留中の変更をすべて破棄します。 このメソッドにより、サブスクリプションを再初期化するようにマークされます。  
  
    > [!NOTE]  
    >  サブスクリプションの有効期限が切れると、変更をアップロードできません。 詳しくは、「 [Set the Expiration Period for Subscriptions](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)」をご覧ください。  
  
5.  プッシュ サブスクリプションを同期します。 詳しくは、「 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)」をご覧ください。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 次の例では、トランザクション パブリケーションに対するプル サブスクリプションを再初期化します。  
  
 [!code-cs[HowTo#rmo_ReinitTranPullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_reinittranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_ReinitTranPullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_reinittranpullsub)]  
  
 次の例では、最初にサブスクライバーの保留中の変更をアップロードした後、マージ パブリケーションに対するプル サブスクリプションを初期化します。  
  
 [!code-cs[HowTo#rmo_ReinitMergePullSub_WithUpload](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_reinitmergepullsub_withupload)]  
  
 [!code-vb[HowTo#rmo_vb_ReinitMergePullSub_WithUpload](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_reinitmergepullsub_withupload)]  
  
## <a name="see-also"></a>参照  
 [サブスクリプションの再初期化](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Replication Management Objects Concepts](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
