---
title: 手動によるサブスクリプションの初期化 | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
ms.assetid: 27a1bc38-e498-4fff-8082-04b52aa4b22c
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 37aecafd3506d2cd47b7b4efd93a89f50ce4ec2d
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72905208"
---
# <a name="initialize-a-subscription-manually"></a>手動によるサブスクリプションの初期化
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、サブスクリプションを手動で初期化する方法について説明します。 サブスクリプションを初期化する場合、一般には、初期スナップショットが使用されます。ただし、スキーマおよび初期データがサブスクライバー側に既に存在していれば、パブリケーションのサブスクリプションをスナップショットを使用せずに初期化できます。  
  

##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   データとスキーマをサブスクライバーにコピーしてからサブスクリプションが手動で初期化されるまでの間に、トランザクション レプリケーションを使ってパブリッシュされたデータベース上で処理が実行されると、この処理による変更がサブスクライバーにレプリケートされない場合があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 スキーマ (通常はデータも含まれます) をサブスクリプション データベースにコピーすることによって、パブリケーションに対するサブスクリプションを手動で初期化します。 スキーマとデータは、パブリケーション データベースと一致している必要があります。 その後、サブスクリプションの新規作成ウィザードの **[サブスクリプションの初期化]** ページで、サブスクリプションにスキーマとデータが必要ないことを指定します。 このウィザードへのアクセスの詳細については、「 [スナップショットを使用しないトランザクション サブスクリプションの初期化](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md) 」および「 [プル サブスクリプションの作成](../../relational-databases/replication/create-a-pull-subscription.md)を使用して、サブスクリプションを手動で初期化する方法について説明します。  
  
 初めてサブスクリプションを同期させたときに、レプリケーションに必要なオブジェクトとメタデータがサブスクリプション データベースにコピーされます。  
  
#### <a name="to-initialize-a-subscription-to-a-publication-manually"></a>パブリケーションに対するサブスクリプションを手動で初期化するには  
  
1.  スキーマとデータがサブスクリプション データベースにコピーされていることを確認します。  
  
2.  サブスクリプションの新規作成ウィザードの **[サブスクリプションの初期化]** ページで、 **[初期化]** チェック ボックスをオフにします。 この操作を、レプリケーション オブジェクトとメタデータのみをコピーする必要がある各サブスクリプションに対して行います。  

##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 サブスクリプションは、レプリケーションのストアド プロシージャを使用して手動で初期化できます。  
  
#### <a name="to-manually-initialize-a-pull-subscription-to-a-transactional-publication"></a>トランザクション パブリケーションのプル サブスクリプションを手動で初期化するには  
  
1.  スキーマとデータがサブスクリプション データベースに存在することを確認します。 詳細については、「 [スナップショットを使用しないトランザクション サブスクリプションの初期化](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)を使用して、サブスクリプションを手動で初期化する方法について説明します。  
  
2.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)を実行します。 **\@publication** **\@subscriber**、 **\@destination_db** にパブリッシュ済みのデータを格納するサブスクライバー側データベースの名前、 **\@subscription_type** に対する **pull** の値、 **\@sync_type** に対する **replication support only** の値を指定します。 詳細については、「 [プル サブスクリプションの作成](../../relational-databases/replication/create-a-pull-subscription.md)」をご覧ください。  
  
3.  サブスクライバーで、 [sp_addpullsubscription](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)を実行します。 サブスクリプションの更新については、「 [Create an Updatable Subscription to a Transactional Publication](https://technet.microsoft.com/library/ms152769(v=sql.130).aspx)」を参照してください。  
  
4.  サブスクライバーで、 [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)を実行します。 詳細については、「 [プル サブスクリプションの作成](../../relational-databases/replication/create-a-pull-subscription.md)」をご覧ください。  
  
5.  ディストリビューション エージェントを起動して、パブリッシャーからレプリケーション オブジェクトを転送し、最新の変更をダウンロードします。 詳細については、「 [プル サブスクリプションの同期](../../relational-databases/replication/synchronize-a-pull-subscription.md)」をご覧ください。  
  
#### <a name="to-manually-initialize-a-push-subscription-to-a-transactional-publication"></a>トランザクション パブリケーションのプッシュ サブスクリプションを手動で初期化するには  
  
1.  スキーマとデータがサブスクリプション データベースに存在することを確認します。 詳細については、「 [スナップショットを使用しないトランザクション サブスクリプションの初期化](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)を使用して、サブスクリプションを手動で初期化する方法について説明します。  
  
2.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)を実行します。 **\@destination_db** にパブリッシュ済みのデータを格納するサブスクライバー側データベースの名前、 **\@subscription_type** に対する **push**の値、 **\@sync_type** に対する **replication support only** の値を指定します。 サブスクリプションの更新については、「 [Create an Updatable Subscription to a Transactional Publication](https://technet.microsoft.com/library/ms152769(v=sql.130).aspx)」を参照してください。  
  
3.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)を実行します。 詳細については、「 [プッシュ サブスクリプションの作成](../../relational-databases/replication/create-a-push-subscription.md)」をご覧ください。  
  
4.  ディストリビューション エージェントを起動して、パブリッシャーからレプリケーション オブジェクトを転送し、最新の変更をダウンロードします。 詳細については、「 [プッシュ サブスクリプションの同期](../../relational-databases/replication/synchronize-a-push-subscription.md)」をご覧ください。  
  
#### <a name="to-manually-initialize-a-pull-subscription-to-a-merge-publication"></a>マージ パブリケーションのプル サブスクリプションを手動で初期化するには  
  
1.  スキーマとデータがサブスクリプション データベースに存在することを確認します。 これは、サブスクライバーでパブリケーション データベースのバックアップを復元することによって行います。  
  
2.  パブリッシャーで [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)を実行します。 **\@publication**、 **\@subscriber**、 **\@subscriber_db**、 **\@subscription_type** に対する **pull** の値を指定します。 これにより、プル サブスクリプションが登録されます。  
  
3.  パブリッシュされたデータを格納するサブスクライバーのデータベースで [sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)を実行します。 **\@sync_type** には **none** の値を指定します。  
  
4.  サブスクライバーで、 [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)を実行します。 詳細については、「 [プル サブスクリプションの作成](../../relational-databases/replication/create-a-pull-subscription.md)」をご覧ください。  
  
5.  マージ エージェントを起動して、パブリッシャーからレプリケーション オブジェクトを転送し、最新の変更をダウンロードします。 詳細については、「 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)」をご覧ください。  
  
#### <a name="to-manually-initialize-a-push-subscription-to-a-merge-publication"></a>マージ パブリケーションのプッシュ サブスクリプションを手動で初期化するには  
  
1.  スキーマとデータがサブスクリプション データベースに存在することを確認します。 これは、サブスクライバーでパブリケーション データベースのバックアップを復元することによって行います。  
  
2.  パブリッシャー側のパブリケーション データベースに対し、 [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)を実行します。 **\@subscriber_db** にパブリッシュ済みのデータを格納するサブスクライバー側データベースの名前、 **\@subscription_type** に対する **push** の値、 **\@sync_type** に対する **none** の値を指定します。  
  
3.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)を実行します。 詳細については、「 [プッシュ サブスクリプションの作成](../../relational-databases/replication/create-a-push-subscription.md)」をご覧ください。  
  
4.  マージ エージェントを起動して、パブリッシャーからレプリケーション オブジェクトを転送し、最新の変更をダウンロードします。 詳細については、「 [プッシュ サブスクリプションの同期](../../relational-databases/replication/synchronize-a-push-subscription.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [スナップショットを使用しないトランザクション サブスクリプションの初期化](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)   
 [レプリケートされたデータベースのバックアップと復元](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [レプリケーション セキュリティの推奨事項](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
