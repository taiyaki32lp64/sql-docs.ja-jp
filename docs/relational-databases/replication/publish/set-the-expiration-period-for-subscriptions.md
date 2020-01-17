---
title: サブスクリプションの有効期限の設定 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], expiration
- expiration [SQL Server replication]
- retention periods [SQL Server replication]
- deactivating subscriptions
ms.assetid: 542f0613-5817-42d0-b841-fb2c94010665
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 9f7948fa600f68b23f5279de8a286044c8f6b245
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846553"
---
# <a name="set-the-expiration-period-for-subscriptions"></a>サブスクリプションの有効期限の設定
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、サブスクリプションの有効期限を設定する方法について説明します。 サブスクリプションの期限が切れて削除されるまでの時間は、サブスクリプションの有効期限によって決定されます。 詳しくは、「 [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)」をご覧ください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [推奨事項](#Recommendations)  
  
-   **サブスクリプションの有効期限を設定するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 作業を開始する準備  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   サブスクリプションの有効期限は、 *パブリケーション保有期間*とも呼ばれます。 マージ レプリケーション メタデータのクリーンアップは、この設定に依存します。  
  
    -   保有期間が終了するまで、パブリケーションおよびサブスクリプション データベースでメタデータをクリーンアップすることはできません。 レプリケーション パフォーマンスを低下させる可能性があるため、保有期間に大きな値を指定する際は注意してください。 すべてのサブスクライバーが保有期間内で定期的に同期されることを確実に予測できる場合は、小さい値を使用することをお勧めします。  
  
         マージ パブリケーションの保有期間には、異なるタイム ゾーンのサブスクライバーに対応するため、24 時間の猶予期間があります。 たとえば、保有期間を 1 日に設定した場合、実際の保有期間は 48 時間となります。  
  
    -   サブスクリプションの期限が切れないように指定することは可能ですが、メタデータをクリーンアップできなくなるため、この値は使用しないことを強くお勧めします。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[全般]** ページで、サブスクリプションの有効期限を設定します。 このダイアログ ボックスへのアクセス方法の詳細については、「[パブリケーション プロパティの表示および変更](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」を参照してください。  
  
#### <a name="to-set-the-expiration-period-for-subscriptions"></a>サブスクリプションの有効期限を設定するには  
  
1.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[全般]** ページで、 **[サブスクリプションの有効期限]** セクションに、サブスクリプションに有効期限を設定するかどうかを指定します。  
  
2.  有効期限を設定する場合、有効期限の期間を指定します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 この値は、レプリケーションのストアド プロシージャを使用して、パブリケーションの作成時に設定することも、後で変更することもできます。  
  
#### <a name="to-set-the-expiration-period-for-a-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショットまたはトランザクション パブリケーションのサブスクリプションに対して有効期限を設定するには  
  
1.  パブリッシャーで [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)を実行します。 **\@retention** にサブスクリプションの有効期限を時間単位で指定します。 既定の有効期限は 336 時間です。 詳細については、「 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)」を参照してください。  
  
#### <a name="to-set-the-expiration-period-for-a-subscription-to-a-merge-publication"></a>マージ パブリケーションのサブスクリプションに対して有効期限を設定するには  
  
1.  パブリッシャーで [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)を実行します。 **\@retention** にサブスクリプションの有効期限を指定します。 **\@retention_period_unit** に有効期限の単位を指定します。指定できる値は次のいずれかです。  
  
    -   **1** = 週  
  
    -   **2** = 月  
  
    -   **3** = 年  
  
     既定の有効期限は 14 日です。 詳しくは、「 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)」をご覧ください。  
  
#### <a name="to-change-the-expiration-period-for-a-subscription-to-a-snapshot-or-transactional-publication"></a>スナップショットまたはトランザクション パブリケーションのサブスクリプションに対して有効期限を変更するには  
  
1.  パブリッシャーで [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)を実行します。 **\@property** に **retention** を、 **\@value** にサブスクリプションの新しい有効期限を時間単位で指定します。  
  
#### <a name="to-change-the-expiration-period-for-a-subscription-to-a-merge-publication"></a>マージ パブリケーションのサブスクリプションに対して有効期限を変更するには  
  
1.  パブリッシャーで [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md) を実行します。引数には **\@publication** と **\@publisher** を指定します。 結果セットの **retention_period_unit** の値 (次のいずれか) を確認します。  
  
    -   **0** = 日  
  
    -   **1** = 週  
  
    -   **2** = 月  
  
    -   **3** = 年  
  
2.  パブリッシャーで [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)を実行します。 **\@property** に **retention** を指定します。また、 **\@value** には、手順 1 の保有期間の単位に基づいて、サブスクリプションの新しい有効期限をテキストで指定します。  
  
3.  (省略可) パブリッシャーで [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)を実行します。 **\@property** に **retention_period_unit** を、 **\@value** には、サブスクリプション有効期限に使用する新しい単位を指定します。  
  
## <a name="see-also"></a>参照  
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
