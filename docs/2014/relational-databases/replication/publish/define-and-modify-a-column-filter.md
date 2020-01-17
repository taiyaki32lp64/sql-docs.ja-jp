---
title: 列フィルターの定義および変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 7e00ceeae68ccc791c3680e029e13844fa6ec683
ms.sourcegitcommit: 0d89bcaebdf87db3bd26db2ca263be9c671b0220
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/02/2019
ms.locfileid: "68731067"
---
# <a name="define-and-modify-a-column-filter"></a>列フィルターの定義および変更
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、列フィルターを定義および変更する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
-   **列フィルターを定義または変更するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   一部の列はフィルター選択できません。詳細については、「[Filter Published Data](filter-published-data.md)」(パブリッシュされたデータのフィルター処理) をご覧ください。 サブスクリプションを初期化した後で列フィルターを変更する場合には、列フィルターの変更後、新規スナップショットを生成してすべてのサブスクリプションを再初期化する必要があります。 プロパティ変更の要件の詳細については、「[Change Publication and Article Properties](change-publication-and-article-properties.md)」(パブリケーションとアーティクルのプロパティの変更) をご覧ください。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 パブリケーションの新規作成ウィザードの **[アーティクル]** ページで列フィルターを定義します。 パブリケーションの新規作成ウィザードの詳細については、「[Create a Publication](create-a-publication.md)」(パブリケーションの作成) をご覧ください。  
  
 **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[アーティクル]** ページで列フィルターの定義および変更を行います。 パブリケーションとアーティクルのプロパティの詳細については、「[View and Modify Publication Properties](view-and-modify-publication-properties.md)」(パブリケーション プロパティの表示と変更) をご覧ください。  
  
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
>  次の手順は、基になるテーブルが変更されていないことが前提となっています。 パブリッシュされたテーブルにデータ定義言語 (DDL) の変更をレプリケートする方法の詳細については、「[Make Schema Changes on Publication Databases](make-schema-changes-on-publication-databases.md)」(パブリケーション データベースでのスキーマの変更) をご覧ください。  
  
#### <a name="to-define-a-column-filter-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションでパブリッシュされたアーティクルの列フィルターを定義するには  
  
1.  フィルターを適用するアーティクルを定義します。 詳細については、「 [Define an Article](define-an-article.md)」をご覧ください。  
  
2.  パブリッシャー側のパブリケーション データベースで、 [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql)を実行します。 これにより、アーティクルに含める列、またはアーティクルから削除する列を定義します。  
  
    -   多数の列を含むテーブルから少数の列をパブリッシュする場合は、追加する各列に対して [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql) を一度実行します。 **\@列**の列名と、 **add** for  **\@操作**の値を指定します。  
  
    -   多くの列を含むテーブルのほとんどの列をパブリッシュする場合は、 [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql)を実行します。この場合、  **\@列**には**null**を指定し、すべての列を追加するには**add** for  **\@operation**を指定します。 次に、除外する各列に対して[sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql)を1回実行します。これには、 **drop** for  **\@操作**の値と **\@column**の除外する列名を指定します。  
  
3.  パブリッシャー側のパブリケーション データベースで、 [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql)を実行します。 **\@パブリケーション**のパブリケーション名と **\@アーティクル**のフィルター選択されたアーティクルの名前を指定します。 これにより、フィルターを適用するアーティクルの同期オブジェクトが作成されます。  
  
#### <a name="to-change-a-column-filter-to-include-additional-columns-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションでパブリッシュされたアーティクルに対して、追加列を含めるための列フィルターを定義するには  
  
1.  パブリッシャー側のパブリケーション データベースで、追加する各列に対して [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql) を一度ずつ実行します。 **\@列**の列名と、 **add** for  **\@操作**の値を指定します。  
  
2.  パブリッシャー側のパブリケーション データベースで、 [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql)を実行します。 **\@パブリケーション**のパブリケーション名と **\@アーティクル**のフィルター選択されたアーティクルの名前を指定します。 パブリケーションに既存のサブスクリプションがある場合は、  **\@change_active**に値**1**を指定します。 これにより、フィルターを適用するアーティクルの同期オブジェクトが再作成されます。  
  
3.  パブリケーションに対してスナップショット エージェント ジョブを再実行し、更新済みスナップショットを生成します。  
  
4.  サブスクリプションを再初期化します。 詳細については、「 [サブスクリプションの再初期化](../reinitialize-subscriptions.md)」を参照してください。  
  
#### <a name="to-change-a-column-filter-to-remove-columns-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションでパブリッシュされたアーティクルに対して、列を削除するための列フィルターを定義するには  
  
1.  パブリッシャー側のパブリケーション データベースで、削除する各列に対して [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql) を一度実行します。 **\@列**の列名と **\@** **drop**の値を指定します。  
  
2.  パブリッシャー側のパブリケーション データベースで、 [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql)を実行します。 **\@パブリケーション**のパブリケーション名と **\@アーティクル**のフィルター選択されたアーティクルの名前を指定します。 パブリケーションに既存のサブスクリプションがある場合は、  **\@change_active**に値**1**を指定します。 これにより、フィルターを適用するアーティクルの同期オブジェクトが再作成されます。  
  
3.  パブリケーションに対してスナップショット エージェント ジョブを再実行し、更新済みスナップショットを生成します。  
  
4.  サブスクリプションを再初期化します。 詳細については、「 [サブスクリプションの再初期化](../reinitialize-subscriptions.md)」を参照してください。  
  
#### <a name="to-define-a-column-filter-for-an-article-published-in-a-merge-publication"></a>スナップショットまたはマージ パブリケーションでパブリッシュされたアーティクルの列フィルターを定義するには  
  
1.  フィルターを適用するアーティクルを定義します。 詳しくは、「 [アーティクルを定義](define-an-article.md)」をご覧ください。  
  
2.  パブリッシャー側のパブリケーション データベースで、 [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql)を実行します。 これにより、アーティクルに含める列、またはアーティクルから削除する列を定義します。  
  
    -   多数の列を含むテーブルから少数の列のみをパブリッシュする場合は、追加する各列に対して [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) を一度ずつ実行します。 **\@列**の列名と、 **add** for  **\@操作**の値を指定します。  
  
    -   多くの列を含むテーブルのほとんどの列をパブリッシュする場合は、 [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql)を実行します。  **\@**  **\@** 列には**null**を指定し、all を追加するには**add** to operation を指定します。欄. 次に、除外する各列に対して[sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql)を1回実行します。これには、 **drop** for  **\@操作**の値と **\@column**の除外する列名を指定します。  
  
#### <a name="to-change-a-column-filter-to-include-additional-columns-for-an-article-published-in-a-merge-publication"></a>マージ パブリケーションでパブリッシュされたアーティクルに対して、追加列を含めるための列フィルターを定義するには  
  
1.  パブリッシャー側のパブリケーション データベースで、追加する各列に対して [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) を一度ずつ実行します。 **\@列**の列名、for  **\@操作**の値、および **\@force_invalidate_snapshot**と  **\@force_reinit_ の両方に1を指定します。サブスクリプション**。  
  
2.  パブリケーションに対してスナップショット エージェント ジョブを再実行し、更新済みスナップショットを生成します。  
  
3.  サブスクリプションを再初期化します。 詳細については、「 [サブスクリプションの再初期化](../reinitialize-subscriptions.md)」を参照してください。  
  
#### <a name="to-change-a-column-filter-to-remove-columns-for-an-article-published-in-a-merge-publication"></a>マージ パブリケーションでパブリッシュされたアーティクルに対して、列を削除するための列フィルターを変更するには  
  
1.  パブリッシャー側のパブリケーション データベースで、削除する各列に対して [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) を一度ずつ実行します。 **\@列**の列名を指定し、値を**drop**に **\@** 設定し、  **\@force_invalidate_snapshot**と  **\@force_reinit_ の両方に1を指定します。サブスクリプション**。  
  
2.  パブリケーションに対してスナップショット エージェント ジョブを再実行し、更新済みスナップショットを生成します。  
  
3.  サブスクリプションを再初期化します。 詳細については、「 [サブスクリプションの再初期化](../reinitialize-subscriptions.md)」を参照してください。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次のトランザクション レプリケーション例では、 `DaysToManufacture` テーブルに基づく `Product` 列がアーティクルから削除されます。  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../snippets/tsql/SQL15/replication/howto/tsql/createtranpub.sql#sp_addtranarticle)]  
  
 次のマージ レプリケーション例では、 `CreditCardApprovalCode` テーブルに基づく `SalesOrderHeader` 列がアーティクルから削除されます。  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepub.sql#sp_addmergearticle)]  
  
## <a name="see-also"></a>関連項目  
 [パブリケーションとアーティクルのプロパティの変更](change-publication-and-article-properties.md)   
 [パブリッシュされたデータのフィルター処理](filter-published-data.md)   
 [マージ レプリケーション用にパブリッシュされたデータのフィルター処理](../merge/filter-published-data-for-merge-replication.md)  
  
  
