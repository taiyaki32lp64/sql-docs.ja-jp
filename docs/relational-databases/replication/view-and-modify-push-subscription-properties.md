---
title: プッシュ サブスクリプションのプロパティの表示または変更 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing replication properties
- push subscriptions [SQL Server replication], properties
- subscriptions [SQL Server replication], push
- push subscriptions [SQL Server replication], modifying
- modifying replication properties, push subscriptions
- modifying subscriptions, SQL Server Management Studio
ms.assetid: 801d2995-7aa5-4626-906e-c8190758ec71
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 84e3655fac042e213ad82ac02fb39969b4993026
ms.sourcegitcommit: 0ea19d8e3bd9d91a416311e00a5fb0267d41949e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2019
ms.locfileid: "71174233"
---
# <a name="view-and-modify-push-subscription-properties"></a>プッシュ サブスクリプションのプロパティの表示または変更
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、プッシュ サブスクリプションのプロパティを表示および変更する方法について説明します。  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]

  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 プッシュ サブスクリプション プロパティを表示および変更するには、以下の方法があります。  
  
-   **[サブスクリプションのプロパティ - \<Publisher>:\<PublicationDatabase>]** ダイアログ ボックスで表示できます。これは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] から使用できます。  
  
-   レプリケーション モニターの **[すべてのサブスクリプション]** タブ。 レプリケーション モニターの起動の詳細については、「[Start the Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)」(レプリケーション モニターの開始) をご覧ください。  
  
#### <a name="to-view-and-modify-push-subscription-properties-in-management-studio"></a>Management Studio でプッシュ サブスクリプション プロパティを表示および変更するには  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。  
  
3.  適切なパブリケーションを展開し、サブスクリプションを右クリックして、 **[プロパティ]** をクリックします。  
  
4.  必要に応じてプロパティを変更し、 **[OK]** をクリックします。  
  
#### <a name="to-view-and-modify-push-subscription-properties-in-replication-monitor"></a>レプリケーション モニターでプッシュ サブスクリプション プロパティを表示および変更するには  
  
1.  レプリケーション モニターの左ペインのパブリッシャー グループを展開し、パブリッシャーを展開して、パブリケーションをクリックします。  
  
2.  **[すべてのサブスクリプション]** タブをクリックします。  
  
3.  サブスクリプションを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  必要に応じてプロパティを変更し、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 プッシュ サブスクリプションのプロパティは、レプリケーションのストアド プロシージャを使用して、プログラムから変更できます。 使用するストアド プロシージャは、サブスクリプションが属するパブリケーションの種類によって異なります。  
  
#### <a name="to-view-the-properties-of-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションのプッシュ サブスクリプションのプロパティを表示するには  
  
1.  パブリッシャーのパブリケーション データベースで [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)を実行します。 **\@publication** と **\@subscriber** を指定し、 **\@article** に **all** を指定します。  
  
2.  パブリッシャーのパブリケーション データベースで、 **\@subscriber** を指定して [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md) を実行します。  
  
#### <a name="to-change-the-properties-of-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションのプッシュ サブスクリプションのプロパティを変更するには  
  
1.  パブリッシャーのパブリケーション データベースで [sp_changesubscriber](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md) を実行します。このとき、 **\@subscriber** を指定し、さらに、変更対象とするサブスクライバー プロパティのパラメーターをすべて指定します。  
  
2.  パブリッシャーのパブリケーション データベースで [sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)を実行します。 **\@publication**、 **\@subscriber**、 **\@destination_db** を指定し、 **\@article** には **all** を、 **\@property** には変更対象のサブスクリプション プロパティを、 **\@value** には新しい値を指定します。 これにより、プッシュ サブスクリプションのセキュリティ設定が変更されます。  
  
3.  (省略可) サブスクリプションのデータ変換サービス (DTS) パッケージのプロパティを変更するには、サブスクライバーのサブスクリプション データベースで [sp_changesubscriptiondtsinfo](../../relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql.md) を実行します。 **\@jobid** にディストリビューション エージェント ジョブの ID を指定し、さらに、次の DTS パッケージ プロパティを指定します。  
  
    -   **\@dts_package_name**  
  
    -   **\@dts_package_password**  
  
    -   **\@dts_package_location**  
  
     これにより、サブスクリプションの DTS パッケージ プロパティが変更されます。  
  
    > [!NOTE]  
    >  ジョブ ID は、 [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)を実行することで取得できます。  
  
#### <a name="to-view-the-properties-of-a-push-subscription-to-a-merge-publication"></a>マージ パブリケーションのプッシュ サブスクリプションのプロパティを表示するには  
  
1.  パブリッシャーのパブリケーション データベースで [sp_helpmergesubscription](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)を実行します。 **\@publication** と **\@subscriber** を指定します。  
  
2.  パブリッシャーで、 **\@subscriber** を指定して [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md) を実行します。  
  
#### <a name="to-change-the-properties-of-a-push-subscription-to-a-merge-publication"></a>マージ パブリケーションのプッシュ サブスクリプションのプロパティを変更するには  
  
1.  パブリッシャーのパブリケーション データベースで [sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)を実行します。 **\@publication**、 **\@subscriber**、 **\@subscriber_db** を指定し、さらに、変更対象のサブスクリプション プロパティを **\@property** に、新しい値を **\@value** に指定します。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 プッシュ サブスクリプション プロパティの表示や変更に使用する RMO クラスは、プッシュ サブスクリプションをサブスクライブするパブリケーションの種類によって異なります。  
  
#### <a name="to-view-or-modify-properties-of-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションに対するプッシュ サブスクリプションのプロパティを表示または変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.TransSubscription> クラスのインスタンスを作成します。  
  
3.  <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> の各プロパティを設定します。  
  
4.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> プロパティ設定に、手順 1. の <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> を設定します。  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドから **false**が返された場合、手順 3. で指定したサブスクリプションのプロパティが正しく定義されていないか、サブスクリプションが存在していません。  
  
6.  (省略可) プロパティを変更するには、 <xref:Microsoft.SqlServer.Replication.TransSubscription> の設定可能なプロパティに新しい値を設定し、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> メソッドを呼び出します。  
  
7.  (省略可) 新しい設定を表示するには、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> メソッドを呼び出して、サブスクリプションのプロパティを再読み込みします。  
  
#### <a name="to-view-or-modify-properties-of-a-push-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプッシュ サブスクリプションのプロパティを表示または変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、サブスクライバーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeSubscription> クラスのインスタンスを作成します。  
  
3.  <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> の各プロパティを設定します。  
  
4.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> プロパティ設定に、手順 1. の <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> を設定します。  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドから **false**が返された場合、手順 3. で指定したサブスクリプションのプロパティが正しく定義されていないか、サブスクリプションが存在していません。  
  
6.  (省略可) プロパティを変更するには、 <xref:Microsoft.SqlServer.Replication.MergeSubscription> の設定可能なプロパティに新しい値を設定し、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> メソッドを呼び出します。  
  
7.  (省略可) 新しい設定を表示するには、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> メソッドを呼び出して、サブスクリプションのプロパティを再読み込みします。  
  
## <a name="see-also"></a>参照  
 [レプリケーション モニターを使用して情報を表示し、タスクを実行する](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [パブリケーションのサブスクライブ](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
