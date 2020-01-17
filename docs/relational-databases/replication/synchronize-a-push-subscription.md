---
title: プッシュ サブスクリプションの同期 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- synchronization [SQL Server replication], push subscriptions
- subscriptions [SQL Server replication], push
- push subscriptions [SQL Server replication], synchronizing
ms.assetid: 0cfa7ae5-91d3-4a4f-9edf-a852d45783b5
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 4a6e56932ab54bc489000c98a29150df984f5991
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907869"
---
# <a name="synchronize-a-push-subscription"></a>プッシュ サブスクリプションの同期
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [レプリケーション エージェント](../../relational-databases/replication/agents/replication-agents-overview.md)、またはレプリケーション管理オブジェクト (RMO) を使用して、プッシュ サブスクリプションを同期する方法について説明します。  
  
[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]

##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 サブスクリプションは、ディストリビューション エージェント (スナップショット レプリケーションおよびトランザクション レプリケーションの場合) またはマージ エージェント (マージ レプリケーションの場合) で同期されます。 エージェントは継続的に実行、要求時に実行、またはスケジュールで実行できます。 同期スケジュールの指定の詳細については、「[同期スケジュールの指定](../../relational-databases/replication/specify-synchronization-schedules.md)」を参照してください。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の **[ローカル パブリケーション]** フォルダーと **[ローカル サブスクリプション]** フォルダー、およびレプリケーション モニターの **[すべてのサブスクリプション]** タブからは、要求時にサブスクリプションを同期します。 Oracle パブリケーションに対するサブスクリプションは、サブスクライバーから要求時に同期することはできません。 レプリケーション モニターの起動の詳細については、「[Start the Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)」 (レプリケーション モニターの開始) を参照してください。  
  
#### <a name="to-synchronize-a-push-subscription-on-demand-in-management-studio-at-the-publisher"></a>Management Studio で要求時にプッシュ サブスクリプションを同期するには (パブリッシャー側)  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。  
  
3.  サブスクリプションを同期するパブリケーションを展開します。  
  
4.  同期するサブスクリプションを右クリックし、 **[同期の状態の表示]** をクリックします。  
  
5.  **[同期の状態の表示 - \<Subscriber>:\<SubscriptionDatabase>]** ダイアログ ボックスで、 **[開始]** をクリックします。 同期が完了したら、" **同期処理が完了しました** " というメッセージが表示されます。  
  
6.  **[閉じる]** をクリックします。  

#### <a name="to-synchronize-a-push-subscription-on-demand-in-management-studio-at-the-subscriber"></a>Management Studio で要求時にプッシュ サブスクリプションを同期するには (サブスクライバー側)  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でサブスクライバーに接続して、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル サブスクリプション]** フォルダーを展開します。  
  
3.  同期するサブスクリプションを右クリックし、 **[同期の状態の表示]** をクリックします。  
  
4.  ディストリビューターへの接続の確立に関するメッセージが表示されます。 **[OK]** をクリックします。  
  
5.  **[同期の状態の表示 - \<Subscriber>:\<SubscriptionDatabase>]** ダイアログ ボックスで、 **[開始]** をクリックします。 同期が完了したら、" **同期処理が完了しました** " というメッセージが表示されます。  
  
6.  **[閉じる]** をクリックします。  
  
#### <a name="to-synchronize-a-push-subscription-on-demand-in-replication-monitor"></a>レプリケーション モニターで要求時にプッシュ サブスクリプションを同期するには  
  
1.  レプリケーション モニターで、左ペインのパブリッシャー グループを展開し、パブリッシャーを展開してパブリケーションをクリックします。  
  
2.  **[すべてのサブスクリプション]** タブをクリックします。  
  
3.  同期するサブスクリプションを右クリックし、 **[同期の開始]** をクリックします。  
  
4.  同期の進行状況を見るには、サブスクリプションを右クリックして **[詳細表示]** をクリックします。  
  
##  <a name="ReplProg"></a> レプリケーション エージェントの使用  
 コマンド プロンプトから適切なレプリケーション エージェント実行可能ファイルを呼び出すことにより、プッシュ サブスクリプションを要求時にプログラムで同期できます。 呼び出されるレプリケーション エージェント実行可能ファイルは、プッシュ サブスクリプションが属するパブリケーションの種類によって異なります。  
  
#### <a name="to-start-the-distribution-agent-to-synchronize-a-push-subscription-to-a-transactional-publication"></a>ディストリビューション エージェントを開始してプッシュ サブスクリプションをトランザクション パブリケーションに同期するには  
  
1.  コマンド プロンプトから、またはディストリビューターからバッチ ファイルで、 **distrib.exe**を実行します。 次のコマンド ライン引数を指定します。  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-Distributor**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType = 0**  
  
     SQL Server 認証を使用する場合は、次の引数も指定する必要があります。  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode = 0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode = 0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode = 0**  
  
        > [!IMPORTANT]  
        >  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
#### <a name="to-start-the-merge-agent-to-synchronize-a-push-subscription-to-a-merge-publication"></a>マージ エージェントを開始してプッシュ サブスクリプションをマージ パブリケーションに同期するには  
  
1.  コマンド プロンプトから、またはディストリビューターからバッチ ファイルで、 **replmerg.exe**を実行します。 次のコマンド ライン引数を指定します。  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-Publication**  
  
    -   **-Distributor**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType = 0**  
  
     SQL Server 認証を使用する場合は、次の引数も指定する必要があります。  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode = 0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode = 0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode = 0**  
  
        > [!IMPORTANT]  
        >  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
###  <a name="TsqlExample"></a> 例 (レプリケーション エージェント)  
 次の例では、ディストリビューション エージェントを開始してプッシュ サブスクリプションを同期します。  
  
```  
  
REM -- Declare the variables.  
SET Publisher=%instancename%  
SET Subscriber=%instancename%  
SET PublicationDB=AdventureWorks2012  
SET SubscriptionDB=AdventureWorks2012Replica   
SET Publication=AdvWorksProductsTran  
  
REM -- Start the Distribution Agent with four subscription streams.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\120\COM\DISTRIB.EXE" -Subscriber %Subscriber%   
-SubscriberDB %SubscriptionDB% -SubscriberSecurityMode 1 -Publication %Publication%   
-Publisher %Publisher% -PublisherDB %PublicationDB% -Distributor %Publisher%   
-DistributorSecurityMode 1 -Continuous -SubscriptionType 0 -SubscriptionStreams 4  
  
```  
  
 次の例では、マージ エージェントを開始してプッシュ サブスクリプションを同期します。  
  
```  
  
REM -- Declare the variables.  
SET Publisher=%instancename%  
SET Subscriber=%instancename%  
SET PublicationDB=AdventureWorks2012  
SET SubscriptionDB=AdventureWorks2012Replica   
SET Publication=AdvWorksSalesOrdersMerge  
  
REM -- Start the Merge Agent.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\120\COM\REPLMERG.EXE"  -Publisher %Publisher%   
-Subscriber  %Subscriber%  -Distributor %Publisher% -PublisherDB  %PublicationDB%   
-SubscriberDB %SubscriptionDB% -Publication %Publication% -PublisherSecurityMode 1   
-OutputVerboseLevel 3  -Output -SubscriberSecurityMode 1  -SubscriptionType 0   
-DistributorSecurityMode 1  
  
```  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 レプリケーション管理オブジェクト (RMO) およびマネージド コードを使用してレプリケーション エージェント機能にアクセスすることで、プッシュ サブスクリプションをプログラムから同期できます。 プッシュ サブスクリプションを同期する際に使用するクラスは、サブスクリプションが属しているパブリケーションの種類によって異なります。  
  
> [!NOTE]
>  アプリケーションに影響を及ぼすことなく、自立的に実行される同期を開始するには、エージェントを非同期的に起動します。 ただし、同期処理中に同期の結果を監視し、エージェントからのコールバックを受け取る場合 (たとえば、進行状況バーを表示する場合)、エージェントを同期的に起動する必要があります。 For [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] サブスクライバーの場合、エージェントを同期的に起動する必要があります。  
  
#### <a name="to-synchronize-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションに対するプッシュ サブスクリプションを同期するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、ディストリビューターへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.TransSubscription> クラスのインスタンスを作成し、次のプロパティを設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>に、パブリケーション データベースの名前を設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>に、サブスクリプションが属しているパブリケーションの名前を設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>に、サブスクリプション データベースの名前を設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>に、サブスクリプションの名前を設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>に、手順 1. で作成した接続を設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、その他のサブスクリプション プロパティを取得します。 このメソッドが **false**を返す場合、サブスクリプションが存在するかどうかをご確認ください。  
  
4.  次のいずれかの方法で、ディストリビューターのディストリビューション エージェントを起動します。  
  
    -   手順 2. で作成した <xref:Microsoft.SqlServer.Replication.TransSubscription.SynchronizeWithJob%2A> インスタンスの <xref:Microsoft.SqlServer.Replication.TransSubscription> メソッドを呼び出します。 このメソッドは、ディストリビューション エージェントを非同期的に起動するため、エージェント ジョブの実行中、制御が直ちにアプリケーションに返されます。 <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> に値 **false** を使用してサブスクリプションが作成された場合、このメソッドを呼び出すことはできません。  
  
    -   <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> プロパティから <xref:Microsoft.SqlServer.Replication.TransSubscription.SynchronizationAgent%2A> クラスのインスタンスを取得し、 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Synchronize%2A> メソッドを呼び出します。 このメソッドにより、エージェントが同期的に起動され、制御は実行中のエージェント ジョブに残ります。 同期実行の間、エージェントの実行中に <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Status> イベントを処理できます。  
  
#### <a name="to-synchronize-a-push-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプッシュ サブスクリプションを同期するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、ディストリビューターへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeSubscription> クラスのインスタンスを作成し、次のプロパティを設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>に、パブリケーション データベースの名前を設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>に、サブスクリプションが属しているパブリケーションの名前を設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>に、サブスクリプション データベースの名前を設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>に、サブスクリプションの名前を設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>に、手順 1. で作成した接続を設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、その他のサブスクリプション プロパティを取得します。 このメソッドが **false**を返す場合、サブスクリプションが存在するかどうかをご確認ください。  
  
4.  次のいずれかの方法で、ディストリビューターのマージ エージェントを起動します。  
  
    -   手順 2. で作成した <xref:Microsoft.SqlServer.Replication.MergeSubscription.SynchronizeWithJob%2A> インスタンスの <xref:Microsoft.SqlServer.Replication.MergeSubscription> メソッドを呼び出します。 このメソッドは、マージ エージェントを非同期的に起動するため、エージェント ジョブの実行中、制御が直ちにアプリケーションに返されます。 <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> に値 **false** を使用してサブスクリプションが作成された場合、このメソッドを呼び出すことはできません。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> プロパティから <xref:Microsoft.SqlServer.Replication.MergeSubscription.SynchronizationAgent%2A> クラスのインスタンスを取得し、 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Synchronize%2A> メソッドを呼び出します。 このメソッドにより、マージ エージェントが同期的に起動され、制御は実行中のエージェント ジョブに残ります。 同期実行の間、エージェントの実行中に <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Status> イベントを処理できます。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 次の例では、トランザクション パブリケーションへのプッシュ サブスクリプションを同期します。エージェントはエージェント ジョブを使用して非同期的に起動されます。  
  
 [!code-cs[HowTo#rmo_SyncTranPushSub_WithJob](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_synctranpushsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPushSub_WithJob](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_synctranpushsub_withjob)]  
  
 次の例では、トランザクション パブリケーションへのプッシュ サブスクリプションを同期します。エージェントは同期的に起動されます。  
  
 [!code-cs[HowTo#rmo_SyncTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_synctranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_synctranpushsub)]  
  
 次の例では、マージ パブリケーションへのプッシュ サブスクリプションを同期します。エージェントはエージェント ジョブを使用して非同期的に起動されます。  
  
 [!code-cs[HowTo#rmo_SyncMergePushSub_WithJob](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_syncmergepushsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePushSub_WithJob](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_syncmergepushsub_withjob)]  
  
 次の例では、マージ パブリケーションへのプッシュ サブスクリプションを同期します。エージェントは同期的に起動されます。  
  
 [!code-cs[HowTo#rmo_SyncMergePushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_syncmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_syncmergepushsub)]  
  
## <a name="see-also"></a>参照  
 [レプリケーション管理オブジェクトの概念](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [データの同期](../../relational-databases/replication/synchronize-data.md)   
 [レプリケーション セキュリティの推奨事項](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
