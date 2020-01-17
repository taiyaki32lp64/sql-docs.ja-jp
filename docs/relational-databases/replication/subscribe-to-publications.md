---
title: パブリケーションのサブスクライブ | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.conc.subtopubs.f1
helpviewer_keywords:
- subscriptions [SQL Server replication], about subscriptions
- pull subscriptions [SQL Server replication]
- subscriptions [SQL Server replication]
- push subscriptions [SQL Server replication], about push subscriptions
- merge replication subscribing [SQL Server replication]
- merge replication subscribing [SQL Server replication], about subscribing
- publications [SQL Server replication], subscribing
- push subscriptions [SQL Server replication]
- pull subscriptions [SQL Server replication], about pull subscriptions
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: 088ee30a-05ab-47c4-92ed-316b93e12445
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: e08891eb7cb9fb897b48e37d6d8caa0e12620d06
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768356"
---
# <a name="subscribe-to-publications"></a>パブリケーションのサブスクライブ
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  サブスクリプションとは、パブリケーションのデータとデータベース オブジェクトのコピーを要求することです。 サブスクリプションでは、受信するパブリケーションおよびパブリケーションの受信場所と受信時間が定義されます。 サブスクリプションを設計する場合は、エージェント処理を実行する場所を考慮してください。 選択するサブスクリプションの種類によって、エージェントが実行される場所が決まります。 プッシュ サブスクリプションではマージ エージェントまたはディストリビューション エージェントがディストリビューターで実行されるのに対し、プル サブスクリプションではサブスクライバーでエージェントが実行されます。 サブスクリプションの作成後にその種類を変更することはできません。  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
|サブスクリプション|特性|いつ使用するか|  
|------------------|---------------------|--------------|  
|プッシュ サブスクリプション|プッシュ サブスクリプションでは、サブスクライバーからの要求なしにパブリッシャーが変更をサブスクライバーに反映します。 変更は、要求時、連続的、スケジュールのいずれかの方法に基づいて、サブスクライバーにプッシュできます。 ディストリビューション エージェントまたはマージ エージェントはディストリビューターで実行されます。|連続的に、または定期的なスケジュールで頻繁にデータの同期をとる場合<br /><br /> パブリケーションがほぼリアルタイムのデータの移動を必要とする場合<br /><br /> ディストリビューターのプロセッサのオーバーヘッドが高くなってもパフォーマンスに影響しない場合<br /><br /> スナップショット レプリケーションとトランザクション レプリケーションで最も頻繁に使用する場合|  
|プル サブスクリプション|プル サブスクリプションでは、パブリッシャーで変更を行うようにサブスクライバーが要求します。 プル サブスクリプションでは、サブスクライバーのユーザーがデータの変更をいつ同期するかを指定できます。 ディストリビューション エージェントまたはマージ エージェントはサブスクライバーで実行されます。|連続的ではなく、要求時またはスケジュールに基づいてデータを同期する場合<br /><br /> パブリケーションに多くのサブスクライバーがある場合、またはリソースの消費が大きすぎてディストリビューターですべてのエージェントを実行できない場合 (またはその両方)<br /><br /> サブスクライバーが独立しているか、接続解除されているか、またはモバイルである場合。 サブスクライバーでは、いつ接続して変更を同期するかが決定されます。<br /><br /> マージ レプリケーションで最も頻繁に使用する場合|  
  
## <a name="merge-replication-subscription-types"></a>マージ レプリケーション サブスクリプションの種類  
 すべての種類のレプリケーションでプッシュ サブスクリプションとプル サブスクリプションが使用できます。 マージ レプリケーションでは、2 つのサブスクリプションを区別するために、クライアント サブスクリプションとサーバー サブスクリプションという語を使用します。 クライアント サブスクリプションとサーバー サブスクリプションのどちらの種類も、プッシュ サブスクリプションとプル サブスクリプションで使用できます。 クライアント サブスクリプションはほとんどのサブスクライバーに適していますが、サーバー サブスクリプションは通常、データを他のサブスクライバーに再パブリッシュするサブスクライバーで使用されます。 サブスクリプションの選択は、競合の解決にも影響します。  
  
## <a name="non-sql-server-subscribers"></a>Non-SQL Server Subscribers  
 Oracle および IBM DB2 は、プッシュ サブスクリプションを使用してスナップショット パブリケーションとトランザクション パブリケーションをサブスクライブできます。 詳細については、「 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)」を参照してください。  
  
## <a name="creating-subscriptions"></a>サブスクリプションの作成  
 サブスクリプションを作成するには、次の情報を指定します。  
  
-   パブリケーションの名前を指定します。  
  
-   サブスクライバーとサブスクリプション データベースの名前  
  
-   ディストリビューション エージェントまたはマージ エージェントをディストリビューターとサブスクライバーのどちらで実行するか  
  
-   ディストリビューション エージェントまたはマージ エージェントを、連続的、スケジュール、要求時のどの方法に基づいて実行するか  
  
-   スナップショット エージェントがサブスクリプションの初期スナップショットを作成するかどうか、およびディストリビューション エージェントまたはマージ エージェントがそのスナップショットをサブスクライバーで適用するかどうか  
  
-   ディストリビューション エージェントまたはマージ エージェントを実行するときに使用するアカウント  
  
-   マージ レプリケーションの場合、サブスクリプションの種類はサーバーとクライアントです。  
  
 **プッシュ サブスクリプションを作成するには**  
  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)  
  
 **プッシュ サブスクリプションのプロパティを表示または変更するには**  
  
 [プッシュ サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)  
  
 **プッシュ サブスクリプションを削除するには**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:[プッシュ サブスクリプションの削除](../../relational-databases/replication/delete-a-push-subscription.md)  
  
> [!NOTE]  
>  サブスクリプションを削除しても、パブリッシュされたオブジェクトはサブスクライバーから削除されません。  
  
 **プル サブスクリプションを作成するには**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:[Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)  
  
 **プル サブスクリプションのプロパティを表示または変更するには**  
  
 [プル サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)  
  
 **プル サブスクリプションを削除するには**  
  
 [プル サブスクリプションの削除](../../relational-databases/replication/delete-a-pull-subscription.md)  
  
## <a name="see-also"></a>参照  
 [サブスクライバーのセキュリティ保護](../../relational-databases/replication/security/secure-the-subscriber.md)   
 [サブスクリプションの有効期限と非アクティブ化](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
