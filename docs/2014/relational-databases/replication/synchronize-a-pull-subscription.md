---
title: プル サブスクリプションの同期 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- pull subscriptions [SQL Server replication], synchronizing
- synchronization [SQL Server replication], pull subscriptions
- subscriptions [SQL Server replication], pull
ms.assetid: 3ca24b23-fdc3-408e-8208-a2ace48fc8e3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c8a7a607221599d599438352eab5add1cc94e5d7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63186232"
---
# <a name="synchronize-a-pull-subscription"></a>プル サブスクリプションの同期
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [レプリケーション エージェント](agents/replication-agents-overview.md)、またはレプリケーション管理オブジェクト (RMO) を使用して、プル サブスクリプションを同期する方法について説明します。  
  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 サブスクリプションは、ディストリビューション エージェント (スナップショット レプリケーションおよびトランザクション レプリケーションの場合) またはマージ エージェント (マージ レプリケーションの場合) で同期されます。 エージェントは継続的に実行、要求時に実行、またはスケジュールで実行できます。 同期スケジュールの指定の詳細については、「[同期スケジュールの指定](specify-synchronization-schedules.md)」を参照してください。  
  
 **の** [ローカル サブスクリプション] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]フォルダーから、サブスクリプションを要求時に同期します。  
  
#### <a name="to-synchronize-a-pull-subscription-on-demand-in-management-studio"></a>Management Studio でプル サブスクリプションを要求時に同期するには  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でサブスクライバーに接続して、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル サブスクリプション]** フォルダーを展開します。  
  
3.  同期するサブスクリプションを右クリックし、 **[同期の状態の表示]** をクリックします。  
  
4.  **[同期の状態の表示 - \<Subscriber>:\<SubscriptionDatabase>]** ダイアログ ボックスで、 **[開始]** をクリックします。 同期が完了したら、" **同期処理が完了しました** " というメッセージが表示されます。  
  
5.  **[閉じる]** をクリックします。  
  
##  <a name="ReplProg"></a> Replication Agents  
 コマンド プロンプトから適切なレプリケーション エージェント実行可能ファイルを呼び出すことにより、プル サブスクリプションを要求時にプログラムで同期できます。 呼び出されるレプリケーション エージェント実行可能ファイルは、プル サブスクリプションが属するパブリケーションの種類によって異なります。 詳しくは、「 [Replication Agents](agents/replication-agents-overview.md)」をご覧ください。  
  
> [!NOTE]  
>  レプリケーション エージェントは、コマンド プロンプトからエージェントを起動したユーザーの Windows 認証資格情報を使ってローカル サーバーに接続します。 これらの Windows 資格情報は、Windows 統合認証でリモート サーバーに接続する際にも使用されます。  
  
#### <a name="to-start-the-distribution-agent-from-the-command-prompt-or-from-a-batch-file"></a>ディストリビューション エージェントをコマンド プロンプトまたはバッチ ファイルから起動するには  
  
1.  コマンド プロンプトまたはバッチ ファイルから、次のコマンド ライン引数を指定して [distrib.exe](agents/replication-distribution-agent.md) を実行し、 **レプリケーション ディストリビューション エージェント**を起動します。  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-Distributor**  
  
    -   **-DistributorSecurityMode** = **1**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriberSecurityMode** = **1**  
  
    -   **-SubscriptionType** = **1**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合は、さらに、次の引数を指定する必要があります。  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** =  **@publisher_security_mode**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode** = **0**  
  
#### <a name="to-start-the-merge-agent-from-the-command-prompt-or-from-a-batch-file"></a>マージ エージェントをコマンド プロンプトまたはバッチ ファイルから起動するには  
  
1.  コマンド プロンプトまたはバッチ ファイルから、次のコマンド ライン引数を指定して [replmerg.exe](agents/replication-merge-agent.md) を実行し、 **レプリケーション マージ エージェント**を起動します。  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-PublisherSecurityMode** = **1**  
  
    -   **-Publication**  
  
    -   **-Distributor**  
  
    -   **-DistributorSecurityMode** = **1**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberSecurityMode** = **1**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType** = **1**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合は、さらに、次の引数を指定する必要があります。  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** =  **@publisher_security_mode**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode** = **0**  
  
###  <a name="TsqlExample"></a> 例 (レプリケーション エージェント)  
 次の例では、ディストリビューション エージェントを起動して、プル サブスクリプションを同期します。 接続はすべて Windows 認証を使用して確立されます。  
  
 [!code-sql[HowTo#bat_synctranpullsub_10](../../snippets/tsql/SQL15/replication/howto/tsql/synctranpullsub_10.bat)]  
  
 次の例では、マージ エージェントを起動して、プル サブスクリプションを同期します。 接続はすべて Windows 認証を使用して確立されます。  
  
 [!code-sql[HowTo#bat_syncmergepullsub_10](../../snippets/tsql/SQL15/replication/howto/tsql/syncmergepullsub_10.bat)]  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 レプリケーション管理オブジェクト (RMO) およびマネージド コードを使用してレプリケーション エージェント機能にアクセスすることで、プル サブスクリプションをプログラムから同期できます。 プル サブスクリプションを同期する際に使用するクラスは、サブスクリプションが属しているパブリケーションの種類によって異なります。  
  
> [!NOTE]  
>  アプリケーションに影響を及ぼすことなく、自立的に実行される同期を開始するには、エージェントを非同期的に起動します。 ただし、同期処理中に同期の結果を監視し、エージェントからのコールバックを受け取る場合 (たとえば、進行状況バーを表示する場合)、エージェントを同期的に起動する必要があります。 For [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] サブスクライバーの場合、エージェントを同期的に起動する必要があります。  
  
#### <a name="to-synchronize-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションに対するプル サブスクリプションを同期するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、サブスクライバーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPullSubscription> クラスのインスタンスを作成し、次のプロパティを設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>に、サブスクリプション データベースの名前を設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>に、サブスクリプションが属しているパブリケーションの名前を設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>にパブリケーション データベース名を指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>に、パブリッシャーの名前を設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>に、手順 1. で作成した接続を設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、その他のサブスクリプション プロパティを取得します。 このメソッドが `false` を返す場合、サブスクリプションが存在するかどうかをご確認ください。  
  
4.  次のいずれかの方法で、サブスクライバーのディストリビューション エージェントを起動します。  
  
    -   手順 2. で作成した <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizeWithJob%2A> インスタンスの <xref:Microsoft.SqlServer.Replication.TransPullSubscription> メソッドを呼び出します。 このメソッドは、ディストリビューション エージェントを非同期的に起動するため、エージェント ジョブの実行中、制御が直ちにアプリケーションに返されます。 [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] サブスクライバーの場合、または、<xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> の値に `false` (既定値) を指定して作成されたサブスクリプションの場合、このメソッドを呼び出すことはできません。  
  
    -   <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> プロパティから <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A> クラスのインスタンスを取得し、 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Synchronize%2A> メソッドを呼び出します。 このメソッドにより、エージェントが同期的に起動され、制御は実行中のエージェント ジョブに残ります。 同期実行の間、エージェントの実行中に <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Status> イベントを処理できます。  
  
        > [!NOTE]  
        >  値が指定されている場合`false`の<xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A>(既定) も指定する必要があります、プル サブスクリプションを作成したときに<xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Distributor%2A>、 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorSecurityMode%2A>、および必要に応じて<xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorLogin%2A>と<xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorPassword%2A>エージェント ジョブに関連するので、サブスクリプションのメタデータが記載されていない[MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql)します。  
  
#### <a name="to-synchronize-a-pull-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプル サブスクリプションを同期するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、サブスクライバーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePullSubscription> クラスのインスタンスを作成し、次のプロパティを設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>に、サブスクリプション データベースの名前を設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>に、サブスクリプションが属しているパブリケーションの名前を設定します。  
  
    -   パブリッシュするデータベースの名前を <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>に指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>に、パブリッシャーの名前を設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>に、手順 1. で作成した接続を設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、その他のサブスクリプション プロパティを取得します。 このメソッドが `false` を返す場合、サブスクリプションが存在するかどうかをご確認ください。  
  
4.  次のいずれかの方法で、サブスクライバーのマージ エージェントを起動します。  
  
    -   手順 2. で作成した <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizeWithJob%2A> インスタンスの <xref:Microsoft.SqlServer.Replication.MergePullSubscription> メソッドを呼び出します。 このメソッドは、マージ エージェントを非同期的に起動するため、エージェント ジョブの実行中、制御が直ちにアプリケーションに返されます。 [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] サブスクライバーの場合、または、<xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> の値に `false` (既定値) を指定して作成されたサブスクリプションの場合、このメソッドを呼び出すことはできません。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> プロパティから <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A> クラスのインスタンスを取得し、 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Synchronize%2A> メソッドを呼び出します。 このメソッドにより、マージ エージェントが同期的に起動され、制御は実行中のエージェント ジョブに残ります。 同期実行の間、エージェントの実行中に <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Status> イベントを処理できます。  
  
        > [!NOTE]  
        >  値が指定されている場合`false`の<xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A>(既定) も指定する必要があります、プル サブスクリプションを作成したときに<xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Distributor%2A>、 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorSecurityMode%2A>、 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherSecurityMode%2A>、 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.HostName%2A>、 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.SubscriptionType%2A>、<xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.ExchangeType%2A>と必要に応じて<xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorLogin%2A>、 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorPassword%2A>、 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherLogin%2A>、および<xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherPassword%2A>エージェント ジョブに関連するメタデータ、サブスクリプションがで使用できないため、 [MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql)します。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 次の例では、トランザクション パブリケーションへのプル サブスクリプションを同期します。エージェントはエージェント ジョブを使用して非同期的に起動されます。  
  
 [!code-csharp[HowTo#rmo_SyncTranPullSub_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_synctranpullsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPullSub_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_synctranpullsub_withjob)]  
  
 次の例では、トランザクション パブリケーションへのプル サブスクリプションを同期します。エージェントは同期的に起動されます。  
  
 [!code-csharp[HowTo#rmo_SyncTranPullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_synctranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_synctranpullsub)]  
  
 次の例では、マージ パブリケーションへのプル サブスクリプションを同期します。エージェントはエージェント ジョブを使用して非同期的に起動されます。  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub_withjob)]  
  
 次の例では、マージ パブリケーションへのプル サブスクリプションを同期します。エージェントは同期的に起動されます。  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub)]  
  
 次の例では、Web 同期を使用してマージ パブリケーションのプル サブスクリプションを同期します。 エージェントを同期的に起動し、追加のサブスクリプション情報が提供されるように、サブスクリプションは、エージェント ジョブや、関連するサブスクリプション メタデータを使わずに作成されます。  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub_NoJobWebSync](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub_nojobwebsync)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub_NoJobWebSync](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub_nojobwebsync)]  
  
## <a name="see-also"></a>関連項目  
 [データの同期](synchronize-data.md)   
 [プル サブスクリプションの作成](create-a-pull-subscription.md)   
 [レプリケーション セキュリティの推奨事項](security/replication-security-best-practices.md)  
  
  
