---
title: プル サブスクリプションの削除 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- removing subscriptions
- deleting subscriptions
- pull subscriptions [SQL Server replication], deleting
- subscriptions [SQL Server replication], pull
ms.assetid: 997c0b8e-d8d9-4eed-85b1-6baa1f8594ce
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 74183916a438ea19536a7cac1abeb8d6cf7cc18a
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846690"
---
# <a name="delete-a-pull-subscription"></a>プル サブスクリプションの削除
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、プル サブスクリプションを削除する方法について説明します。  
  
 **このトピックの内容**  
  
-   **プル サブスクリプションを削除するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [レプリケーション管理オブジェクト (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 パブリッシャーまたはサブスクライバーで、プル サブスクリプションを削除します (パブリッシャーの場合は **の** [ローカル パブリケーション] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]フォルダーから、サブスクライバーの場合は **[ローカル サブスクリプション]** フォルダーから削除します)。 サブスクリプションを削除しても、サブスクリプションのオブジェクトやデータは削除されません。これらは手動で削除する必要があります。  
  
#### <a name="to-delete-a-pull-subscription-at-the-publisher"></a>パブリッシャーでプル サブスクリプションを削除するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。  
  
3.  削除するサブスクリプションに関連付けられているパブリケーションを展開します。  
  
4.  サブスクリプションを右クリックし、 **[削除]** をクリックします。  
  
5.  確認のダイアログ ボックスで、サブスクライバーに接続してサブスクリプション情報を削除するかどうかを選択します。 **[サブスクライバーへの接続]** チェック ボックスをオフにする場合は、後でサブスクライバーに接続してこの情報を削除する必要があります。  
  
#### <a name="to-delete-a-pull-subscription-at-the-subscriber"></a>サブスクライバーでプル サブスクリプションを削除するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でサブスクライバーに接続して、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル サブスクリプション]** フォルダーを展開します。  
  
3.  削除するサブスクリプションを右クリックし、 **[削除]** をクリックします。  
  
4.  確認のダイアログ ボックスで、パブリッシャーに接続してサブスクリプション情報を削除するかどうかを選択します。 **[パブリッシャーへの接続]** チェック ボックスをオフにした場合は、後でパブリッシャーに接続してこの情報を削除する必要があります。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 プル サブスクリプションは、レプリケーション ストアド プロシージャを使用してプログラムで削除できます。 使用するストアド プロシージャは、サブスクリプションが属するパブリケーションの種類によって変わります。  
  
#### <a name="to-delete-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションに対するプル サブスクリプションを削除するには  
  
1.  サブスクライバー側のサブスクリプション データベースに対して、[sp_droppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md) を実行します。 **\@publication**、 **\@publisher**、 **\@publisher_db** を指定します。  
  
2.  パブリッシャー側のパブリケーション データベースに対して、[sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md) を実行します。 **\@publication** と **\@subscriber** を指定します。 **\@article** に **all** を指定します。 (省略可能) ディストリビューターにアクセスできない場合、 **\@ignore_distributor** に **1** を指定して、ディストリビューターの関連オブジェクトを削除せずにサブスクリプションを削除します。  
  
#### <a name="to-delete-a-pull-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプル サブスクリプションを削除するには  
  
1.  サブスクライバー側のサブスクリプション データベースに対して、[sp_dropmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md) を実行します。 **\@publication**、 **\@publisher**、 **\@publisher_db** を指定します。  
  
2.  パブリッシャー側のパブリケーション データベースに対して、[sp_dropmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md) を実行します。 **\@publication**、 **\@subscriber**、 **\@subscriber_db** を指定します。 **\@subscription_type** には **pull** を指定します。 (省略可能) ディストリビューターにアクセスできない場合、 **\@ignore_distributor** に **1** を指定して、ディストリビューターの関連オブジェクトを削除せずにサブスクリプションを削除します。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、トランザクション パブリケーションへのプル サブスクリプションを削除します。 最初のバッチはサブスクライバーで実行され、次のバッチはパブリッシャーで実行されます。  
  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_1.sql)]  
  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_2.sql)]  
  
 次の例では、マージ パブリケーションに対するプル サブスクリプションを削除します。 最初のバッチはサブスクライバーで実行され、次のバッチはパブリッシャーで実行されます。  
  
 [!code-sql[HowTo#sp_dropmergepullsubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_3.sql)]  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_4.sql)]  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 レプリケーション管理オブジェクト (RMO) を使用することで、プログラムによってプル サブスクリプションを削除できます。 プル サブスクリプションの削除に使用する RMO クラスは、プル サブスクリプションをサブスクライブするパブリケーションの種類によって決まります。  
  
#### <a name="to-delete-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションに対するプル サブスクリプションを削除するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、サブスクライバーおよびパブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPullSubscription> クラスのインスタンスを作成し、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>、および <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> の各プロパティを設定します。 手順 1. のサブスクライバー接続を使用して、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティを設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> プロパティをチェックして、サブスクリプションが存在することを確認します。 このプロパティの値が **false**の場合、手順 2. でサブスクリプション プロパティが不適切に定義されたか、サブスクリプションが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.PullSubscription.Remove%2A> メソッドを呼び出します。  
  
5.  手順 1. のパブリッシャー接続を使用して、 <xref:Microsoft.SqlServer.Replication.TransPublication> クラスのインスタンスを作成します。 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 、および <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>を指定します。  
  
6.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出します。 このメソッドが **false**を返す場合、手順 5. で指定したプロパティが誤っているか、サーバーにパブリケーションが存在していません。  
  
7.  <xref:Microsoft.SqlServer.Replication.TransPublication.RemovePullSubscription%2A> メソッドを呼び出します。 *subscriber* パラメーターと *subscriberDB* パラメーターに、サブスクライバーの名前とサブスクリプション データベースを指定します。  
  
#### <a name="to-delete-a-pull-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプル サブスクリプションを削除するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、サブスクライバーおよびパブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePullSubscription> クラスのインスタンスを作成し、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>、および <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> の各プロパティを設定します。 手順 1. の接続を使用して、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティを設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> プロパティをチェックして、サブスクリプションが存在することを確認します。 このプロパティの値が **false**の場合、手順 2. でサブスクリプション プロパティが不適切に定義されたか、サブスクリプションが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.PullSubscription.Remove%2A> メソッドを呼び出します。  
  
5.  手順 1. のパブリッシャー接続を使用して、 <xref:Microsoft.SqlServer.Replication.MergePublication> クラスのインスタンスを作成します。 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 、および <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>を指定します。  
  
6.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出します。 このメソッドが **false**を返す場合、手順 5. で指定したプロパティが誤っているか、サーバーにパブリケーションが存在していません。  
  
7.  <xref:Microsoft.SqlServer.Replication.MergePublication.RemovePullSubscription%2A> メソッドを呼び出します。 *subscriber* パラメーターと *subscriberDB* パラメーターに、サブスクライバーの名前とサブスクリプション データベースを指定します。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 次の例では、トランザクション パブリケーションに対するプル サブスクリプションを削除し、パブリッシャー側のサブスクリプション登録を削除します。  
  
 [!code-cs[HowTo#rmo_DropTranPullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpullsub)]  
  
 次の例では、マージ パブリケーションに対するプル サブスクリプションを削除し、パブリッシャー側のサブスクリプション登録を削除します。  
  
 [!code-cs[HowTo#rmo_DropMergePullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropmergepullsub)]  
  
## <a name="see-also"></a>参照  
 [パブリケーションのサブスクライブ](../../relational-databases/replication/subscribe-to-publications.md)   
 [レプリケーション セキュリティの推奨事項](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
