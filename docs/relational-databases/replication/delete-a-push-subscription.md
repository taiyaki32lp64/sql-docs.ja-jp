---
title: プッシュ サブスクリプションの削除 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- removing subscriptions
- push subscriptions [SQL Server replication], deleting
- deleting subscriptions
- subscriptions [SQL Server replication], push
ms.assetid: 3c4847e2-aed9-4488-b45d-8164422bdb10
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 7fac24aec092ef65bb390d8df020999647f215c6
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908268"
---
# <a name="delete-a-push-subscription"></a>プッシュ サブスクリプションの削除
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、プッシュ サブスクリプションを削除する方法について説明します。  
  
 **このトピックの内容**  
  
-   **プッシュ サブスクリプションを削除するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [レプリケーション管理オブジェクト (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 パブリッシャーまたはサブスクライバーで、プッシュ サブスクリプションを削除します (パブリッシャーの場合は **の** [ローカル パブリケーション] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]フォルダーから、サブスクライバーの場合は **[ローカル サブスクリプション]** フォルダーから削除します)。 サブスクリプションを削除しても、サブスクリプションのオブジェクトやデータは削除されません。これらは手動で削除する必要があります。  
  
#### <a name="to-delete-a-push-subscription-at-the-publisher"></a>パブリッシャーでプッシュ サブスクリプションを削除するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。  
  
3.  削除するサブスクリプションに関連付けられているパブリケーションを展開します。  
  
4.  サブスクリプションを右クリックし、 **[削除]** をクリックします。  
  
5.  確認のダイアログ ボックスで、サブスクライバーに接続してサブスクリプション情報を削除するかどうかを選択します。 **[サブスクライバーへの接続]** チェック ボックスをオフにした場合は、後でサブスクライバーに接続してこの情報を削除する必要があります。  

#### <a name="to-delete-a-push-subscription-at-the-subscriber"></a>サブスクライバーでプッシュ サブスクリプションを削除するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でサブスクライバーに接続して、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル サブスクリプション]** フォルダーを展開します。  
  
3.  削除するサブスクリプションを右クリックし、 **[削除]** をクリックします。  
  
4.  確認のダイアログ ボックスで、パブリッシャーに接続してサブスクリプション情報を削除するかどうかを選択します。 **[パブリッシャーへの接続]** チェック ボックスをオフにした場合は、後でパブリッシャーに接続してこの情報を削除する必要があります。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 プッシュ サブスクリプションは、レプリケーション ストアド プロシージャを使用してプログラムで削除できます。 使用するストアド プロシージャは、サブスクリプションが属するパブリケーションの種類によって異なります。  
  
#### <a name="to-delete-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションに対するプッシュ サブスクリプションを削除するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、[sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md) を実行します。 **\@publication** と **\@subscriber** を指定します。 **\@article** に **all** を指定します。 (省略可能) ディストリビューターにアクセスできない場合、 **\@ignore_distributor** に **1** を指定して、ディストリビューターの関連オブジェクトを削除せずにサブスクリプションを削除します。  
  
2.  サブスクライバーのサブスクリプション データベースで [sp_subscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md) を実行して、サブスクリプション データベース内のレプリケーション メタデータを削除します。  
  
#### <a name="to-delete-a-push-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプッシュ サブスクリプションを削除するには  
  
1.  パブリッシャーで、 **\@publication**、 **\@subscriber**、 **\@subscriber_db** を指定して、[sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md) を実行します。 (省略可能) ディストリビューターにアクセスできない場合、 **\@ignore_distributor** に **1** を指定して、ディストリビューターの関連オブジェクトを削除せずにサブスクリプションを削除します。  
  
2.  サブスクライバー側のサブスクリプション データベースに対して、[sp_mergesubscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md) を実行します。 **\@publisher**、 **\@publisher_db**、 **\@publication** を指定します。 これにより、サブスクリプション データベースのマージ メタデータが削除されます。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 この例では、トランザクション パブリケーションへのプッシュ サブスクリプションを削除します。  
  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_1.sql)]  
  
 この例では、マージ パブリケーションへのプッシュ サブスクリプションを削除します。  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_2.sql)]  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 プッシュ サブスクリプションの削除に使用する RMO クラスは、プッシュ サブスクリプションをサブスクライブするパブリケーションの種類によって異なります。  
  
#### <a name="to-delete-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションに対するプッシュ サブスクリプションを削除するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、サブスクライバーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.TransSubscription> クラスのインスタンスを作成します。  
  
3.  <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> の各プロパティを設定します。  
  
4.  手順 1. の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに設定します。  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> プロパティをチェックして、サブスクリプションが存在することを確認します。 このプロパティの値が **false**の場合、手順 2. でサブスクリプション プロパティが不適切に定義されたか、サブスクリプションが存在していません。  
  
6.  <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> メソッドを呼び出します。  
  
#### <a name="to-delete-a-push-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプッシュ サブスクリプションを削除するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、サブスクライバーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeSubscription> クラスのインスタンスを作成します。  
  
3.  <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> の各プロパティを設定します。  
  
4.  手順 1. の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに設定します。  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> プロパティをチェックして、サブスクリプションが存在することを確認します。 このプロパティの値が **false**の場合、手順 2. でサブスクリプション プロパティが不適切に定義されたか、サブスクリプションが存在していません。  
  
6.  <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> メソッドを呼び出します。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 レプリケーション管理オブジェクト (RMO) を使用することで、プログラムによってプッシュ サブスクリプションを削除できます。  
  
 [!code-cs[HowTo#rmo_DropTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpushsub)]  
  
## <a name="see-also"></a>参照  
 [パブリケーションのサブスクライブ](../../relational-databases/replication/subscribe-to-publications.md)   
 [レプリケーション セキュリティの推奨事項](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
