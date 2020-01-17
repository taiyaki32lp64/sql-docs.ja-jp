---
title: 列フィルターの定義および変更 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server replication], column
- modifying filters, column
- modifying filters
- column filters [SQL Server replication]
ms.assetid: d7c3186a-9a8c-45d8-ab34-05beec4c26dd
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 761c6b6bd1c92e7dd22cc231e46417b4b971a614
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846605"
---
# <a name="define-and-modify-a-column-filter"></a>列フィルターの定義および変更
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、列フィルターを定義および変更する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
-   **列フィルターを定義または変更するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   一部の列はフィルター選択できません。詳細については、「[Filter Published Data](../../../relational-databases/replication/publish/filter-published-data.md)」(パブリッシュされたデータのフィルター処理) をご覧ください。 サブスクリプションを初期化した後で列フィルターを変更する場合には、列フィルターの変更後、新規スナップショットを生成してすべてのサブスクリプションを再初期化する必要があります。 プロパティ変更の要件の詳細については、「[Change Publication and Article Properties](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)」(パブリケーションとアーティクルのプロパティの変更) をご覧ください。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 パブリケーションの新規作成ウィザードの **[アーティクル]** ページで列フィルターを定義します。 パブリケーションの新規作成ウィザードの詳細については、「[Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)」(パブリケーションの作成) をご覧ください。  
  
 **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[アーティクル]** ページで列フィルターの定義および変更を行います。 パブリケーションとアーティクルのプロパティの詳細については、「[View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」(パブリケーション プロパティの表示と変更) をご覧ください。  
  
#### <a name="to-define-a-column-filter"></a>列フィルターを定義するには  
  
1.  パブリケーションの新規作成ウィザードの **[アーティクル]** ページにある **[パブリッシュするオブジェクト]** ペインで、フィルター選択するテーブルを展開します。  
  
2.  フィルター選択する列の隣にあるチェック ボックスをオフにします。  
  
#### <a name="to-modify-column-filtering"></a>列フィルターを変更するには  
  
1.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[アーティクル]** ページにある **[パブリッシュするオブジェクト]** ペインで、フィルター選択するテーブルを展開します。  
  
2.  フィルター選択する列の隣にあるチェック ボックスをオフにして、アーティクルに含める列のチェック ボックスをオンにします。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 テーブル アーティクルを作成するときに、アーティクルにどの列を含めるかを定義したり、アーティクルを定義した後で列を変更したりできます。 レプリケーション ストアド プロシージャを使用して、フィルターが適用された列をプログラムで作成および変更できます。  
  
> [!NOTE]  
>  次の手順は、基になるテーブルが変更されていないことが前提となっています。 パブリッシュされたテーブルにデータ定義言語 (DDL) の変更をレプリケートする方法の詳細については、「[Make Schema Changes on Publication Databases](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)」(パブリケーション データベースでのスキーマの変更) をご覧ください。  
  
#### <a name="to-define-a-column-filter-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションでパブリッシュされたアーティクルの列フィルターを定義するには  
  
1.  フィルターを適用するアーティクルを定義します。 詳細については、「 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
2.  パブリッシャー側のパブリケーション データベースで、 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)を実行します。 これにより、アーティクルに含める列、またはアーティクルから削除する列を定義します。  
  
    -   多数の列を含むテーブルから少数の列をパブリッシュする場合は、追加する各列に対して [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) を一度実行します。 **\@column** に列名を指定し、 **\@operation** に **add** を指定します。  
  
    -   多数の列を含むテーブルの列の多くをパブリッシュする場合は、[sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) を実行します。その場合、 **\@column** に **null** を指定し、 **\@operation** に **add** を指定してすべての列を追加します。 次に、除外する各列に [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) を一度ずつ実行します。その場合、 **\@operation** に **drop** を指定し、 **\@column** に除外する列名を指定します。  
  
3.  パブリッシャー側のパブリケーション データベースで、 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)を実行します。 **\@publication** にパブリケーション名を指定し、 **\@article** にフィルターを適用するアーティクルの名前を指定します。 これにより、フィルターを適用するアーティクルの同期オブジェクトが作成されます。  
  
#### <a name="to-change-a-column-filter-to-include-additional-columns-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションでパブリッシュされたアーティクルに対して、追加列を含めるための列フィルターを定義するには  
  
1.  パブリッシャー側のパブリケーション データベースで、追加する各列に対して [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) を一度ずつ実行します。 **\@column** に列名を指定し、 **\@operation** に **add** を指定します。  
  
2.  パブリッシャー側のパブリケーション データベースで、 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)を実行します。 **\@publication** にパブリケーション名を指定し、 **\@article** にフィルターを適用するアーティクルの名前を指定します。 パブリケーションに既存のサブスクリプションが存在する場合は、 **\@change_active** に **1** を指定します。 これにより、フィルターを適用するアーティクルの同期オブジェクトが再作成されます。  
  
3.  パブリケーションに対してスナップショット エージェント ジョブを再実行し、更新済みスナップショットを生成します。  
  
4.  サブスクリプションを再初期化します。 詳細については、「 [サブスクリプションの再初期化](../../../relational-databases/replication/reinitialize-subscriptions.md)」を参照してください。  
  
#### <a name="to-change-a-column-filter-to-remove-columns-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションでパブリッシュされたアーティクルに対して、列を削除するための列フィルターを定義するには  
  
1.  パブリッシャー側のパブリケーション データベースで、削除する各列に対して [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) を一度実行します。 **\@column** に列名を指定し、 **\@operation** に **drop** を指定します。  
  
2.  パブリッシャー側のパブリケーション データベースで、 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)を実行します。 **\@publication** にパブリケーション名を指定し、 **\@article** にフィルターを適用するアーティクルの名前を指定します。 パブリケーションに既存のサブスクリプションが存在する場合は、 **\@change_active** に **1** を指定します。 これにより、フィルターを適用するアーティクルの同期オブジェクトが再作成されます。  
  
3.  パブリケーションに対してスナップショット エージェント ジョブを再実行し、更新済みスナップショットを生成します。  
  
4.  サブスクリプションを再初期化します。 詳細については、「 [サブスクリプションの再初期化](../../../relational-databases/replication/reinitialize-subscriptions.md)」を参照してください。  
  
#### <a name="to-define-a-column-filter-for-an-article-published-in-a-merge-publication"></a>スナップショットまたはマージ パブリケーションでパブリッシュされたアーティクルの列フィルターを定義するには  
  
1.  フィルターを適用するアーティクルを定義します。 詳しくは、「 [アーティクルを定義](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
2.  パブリッシャー側のパブリケーション データベースで、 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md)を実行します。 これにより、アーティクルに含める列、またはアーティクルから削除する列を定義します。  
  
    -   多数の列を含むテーブルから少数の列のみをパブリッシュする場合は、追加する各列に対して [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) を一度ずつ実行します。 **\@column** に列名を指定し、 **\@operation** に **add** を指定します。  
  
    -   多数の列を含むテーブルの多くの列をパブリッシュする場合は、[sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) を実行します。この場合、 **\@column** に **null** を指定し、 **\@operation** に **add** を指定してすべての列を追加します。 次に、除外する各列に対して [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) を一度ずつ実行します。この場合、 **\@operation** に **drop** を指定し、 **\@column** に除外する列名を指定します。  
  
#### <a name="to-change-a-column-filter-to-include-additional-columns-for-an-article-published-in-a-merge-publication"></a>マージ パブリケーションでパブリッシュされたアーティクルに対して、追加列を含めるための列フィルターを定義するには  
  
1.  パブリッシャー側のパブリケーション データベースで、追加する各列に対して [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) を一度ずつ実行します。 **\@column** に列名を、 **\@operation** に **add**、 **\@force_invalidate_snapshot** と **\@force_reinit_subscription** の両方に **1** を指定します。  
  
2.  パブリケーションに対してスナップショット エージェント ジョブを再実行し、更新済みスナップショットを生成します。  
  
3.  サブスクリプションを再初期化します。 詳細については、「 [サブスクリプションの再初期化](../../../relational-databases/replication/reinitialize-subscriptions.md)」を参照してください。  
  
#### <a name="to-change-a-column-filter-to-remove-columns-for-an-article-published-in-a-merge-publication"></a>マージ パブリケーションでパブリッシュされたアーティクルに対して、列を削除するための列フィルターを変更するには  
  
1.  パブリッシャー側のパブリケーション データベースで、削除する各列に対して [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) を一度ずつ実行します。 **\@column** に列名を、 **\@operation** に **drop** を、 **\@force_invalidate_snapshot** と **\@force_reinit_subscription** の両方に **1** を指定します。  
  
2.  パブリケーションに対してスナップショット エージェント ジョブを再実行し、更新済みスナップショットを生成します。  
  
3.  サブスクリプションを再初期化します。 詳細については、「 [サブスクリプションの再初期化](../../../relational-databases/replication/reinitialize-subscriptions.md)」を参照してください。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次のトランザクション レプリケーション例では、 `DaysToManufacture` テーブルに基づく `Product` 列がアーティクルから削除されます。  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-colu_1.sql)]  
  
 次のマージ レプリケーション例では、 `CreditCardApprovalCode` テーブルに基づく `SalesOrderHeader` 列がアーティクルから削除されます。  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-colu_2.sql)]  
  
## <a name="see-also"></a>参照  
 [パブリケーションとアーティクルのプロパティの変更](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [パブリッシュされたデータのフィルター処理](../../../relational-databases/replication/publish/filter-published-data.md)   
 [マージ レプリケーション用にパブリッシュされたデータのフィルター処理](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  
