---
title: 静的行フィルターの定義および変更 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- modifying filters, static row
- static row filters
- filters [SQL Server replication], static row
ms.assetid: a6ebb026-026f-4c39-b6a9-b9998c3babab
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: c1e63f93a26765b63085f19d99d0bba327b69d55
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908548"
---
# <a name="define-and-modify-a-static-row-filter"></a>静的行フィルターの定義および変更
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、静的行フィルターを定義および変更する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
-   **静的行フィルターを定義または変更するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   パブリケーションに対するサブスクリプションが初期化された後に、静的行フィルターを追加、変更、または削除した場合は、変更を行った後で、新しいスナップショットを生成し、すべてのサブスクリプションを再初期化する必要があります。 プロパティ変更の要件の詳細については、「[Change Publication and Article Properties](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)」(パブリケーションとアーティクルのプロパティの変更) をご覧ください。  
  
-   パブリケーションでピア ツー ピア トランザクション レプリケーションが有効な場合、テーブルはフィルター選択できません。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   フィルターが静的であるため、すべてのサブスクライバーは同じデータのサブセットを受け取ることになります。 マージ パブリケーションに属しているテーブルのアーティクルから行を動的にフィルター選択して、各サブスクライバーが異なるデータ パーティションを受け取るようにする場合は、「 [マージ アーティクルのパラメーター化された行フィルターの定義および変更](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)」を参照してください。 マージ レプリケーションでは、既存の行フィルターに基づいて、関連する行をフィルター選択することもできます。 詳細については、「 [マージ アーティクル間の結合フィルターの定義および変更](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)」をご参照ください。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページまたは **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[行のフィルター選択]** ページで、静的行フィルターを定義、変更、削除します。 ウィザードの使用およびダイアログ ボックスへのアクセスの詳細については、「[パブリケーションの作成](../../../relational-databases/replication/publish/create-a-publication.md)」および「[View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」 (パブリケーション プロパティの表示および変更) を参照してください。  
  
#### <a name="to-define-a-static-row-filter"></a>静的行フィルターを定義するには  
  
1.  パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[行のフィルター選択]** ページで行う操作は、パブリケーションの種類によって異なります。  
  
    -   スナップショット パブリケーションまたはトランザクション パブリケーションの場合は、 **[追加]** をクリックします。  
  
    -   マージ パブリケーションの場合は、 **[追加]** をクリックしてから **[フィルターの追加]** をクリックします。  
  
2.  **[フィルターの追加]** ダイアログ ボックスで、ドロップダウン リスト ボックスからフィルター選択するテーブルを選択します。  
  
3.  **[フィルター ステートメント]** テキスト領域で、フィルター ステートメントを作成します。 テキスト領域に直接入力することも、 **[列]** ボックスから列をドラッグ アンド ドロップすることもできます。  
  
    > [!NOTE]  
    >  WHERE 句には、2 つの部分で構成されている名前を使用する必要があります。3 つまたは 4 つの部分で構成されている名前の使用はサポートされていません。 パブリケーションが Oracle パブリッシャーからのものである場合、WHERE 句は Oracle の構文に準拠する必要があります。  
  
    -   **[フィルター ステートメント]** テキスト領域には、次の形式の既定のテキストが表示されます。  
  
        ```sql  
        SELECT <published_columns> FROM [schema].[tablename] WHERE  
        ```  
  
    -   既定のテキストは変更できません。標準の SQL 構文を使用して WHERE キーワードの後にフィルター句を入力してください。 完成したフィルター句は、次のように表示されます。  
  
        ```sql  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE [LoginID] = 'adventure-works\ranjit0'  
        ```  
  
    -   静的行フィルターには、ユーザー定義関数を含めることができます。 ユーザー定義関数を指定して完成した静的行フィルターのフィルター句は、次のように表示されます。  
  
        ```sql  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] WHERE MyFunction([Freight]) > 100  
        ```  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスが表示されている場合は、 **[OK]** をクリックして保存し、ダイアログ ボックスを閉じます。  

#### <a name="to-modify-a-static-row-filter"></a>静的行フィルターを変更するには  
  
1.  パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[行のフィルター選択]** ページで、 **[フィルター選択されたテーブル]** ペイン内のフィルターを選択し、 **[編集]** をクリックします。  
  
2.  **[フィルターの編集]** ダイアログ ボックスで、フィルターを変更します。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-static-row-filter"></a>静的行フィルターを削除するには  
  
1.  パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[行のフィルター選択]** ページで、 **[フィルター選択されたテーブル]** ペイン内のフィルターを選択し、 **[削除]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 テーブルのアーティクルを作成するとき、WHERE 句を定義することで、アーティクルから特定の行をフィルター選択できます。 いったん行フィルターを定義した後で、そのフィルターを変更することもできます。 静的行フィルターは、レプリケーションのストアド プロシージャを使用してプログラムから作成したり変更したりできます。  
  
#### <a name="to-define-a-static-row-filter-for-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションの静的行フィルターを定義するには  
  
1.  フィルターを適用するアーティクルを定義します。 詳しくは、「 [アーティクルを定義](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
2.  パブリッシャー側のパブリケーション データベースに対して、[sp_articlefilter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) を実行します。 **\@article**、 **\@publication**、 **\@filter_name**、 **\@filter_clause** に、それぞれアーティクル名、パブリケーション名、フィルター名、フィルター句 (`WHERE` は含めない) を指定します。  
  
3.  列フィルターも定義する必要がある場合は、「 [列フィルターの定義および変更](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)」を参照してください。 それ以外の場合、[sp_articleview &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) を実行します。 **\@publication** にパブリケーション名を、 **\@article** にフィルター選択の対象アーティクル名を、 **\@filter_clause** に手順 2 で指定したフィルター句を指定します。 これにより、フィルターを適用するアーティクルの同期オブジェクトが作成されます。  
  
#### <a name="to-modify-a-static-row-filter-for-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションの静的行フィルターを変更するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、[sp_articlefilter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) を実行します。 **\@article**、 **\@publication**、 **\@filter_name**、 **\@filter_clause** に、それぞれアーティクル名、パブリケーション名、新しいフィルター名、新しいフィルター句 (`WHERE` は含めない) を指定します。 この変更によって既存のサブスクリプションのデータが無効になるため、 **\@force_reinit_subscription** の値に **1** を指定します。  
  
2.  パブリッシャー側のパブリケーション データベースで、[sp_articleview &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) を実行します。 **\@publication** にパブリケーション名を、 **\@article** にフィルター選択の対象アーティクル名を、 **\@filter_clause** に手順 1 で指定したフィルター句を指定します。 この結果、フィルター選択の対象アーティクルを定義するビューが再作成されます。  
  
3.  パブリケーションに対してスナップショット エージェント ジョブを再実行し、更新済みスナップショットを生成します。 詳細については、「 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」をご参照ください。  
  
4.  サブスクリプションを再初期化します。 詳細については、「 [サブスクリプションの再初期化](../../../relational-databases/replication/reinitialize-subscriptions.md)」を参照してください。  
  
#### <a name="to-delete-a-static-row-filter-for-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションの静的行フィルターを削除するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、[sp_articlefilter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) を実行します。 **\@article** にアーティクル名を、 **\@publication** にパブリケーション名を、 **\@filter_name** に NULL を、 **\@filter_clause** に NULL を指定します。 この変更によって既存のサブスクリプションのデータが無効になるため、 **\@force_reinit_subscription** の値に **1** を指定します。  
  
2.  パブリケーションに対してスナップショット エージェント ジョブを再実行し、更新済みスナップショットを生成します。 詳細については、「 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」をご参照ください。  
  
3.  サブスクリプションを再初期化します。 詳細については、「 [サブスクリプションの再初期化](../../../relational-databases/replication/reinitialize-subscriptions.md)」を参照してください。  
  
#### <a name="to-define-a-static-row-filter-for-a-merge-publication"></a>マージ パブリケーションの静的行フィルターを定義するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、[sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) を実行します。 **\@subset_filterclause** にフィルター句 (`WHERE` は含めない) を指定します。 詳しくは、「 [アーティクルを定義](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
2.  列フィルターも定義する必要がある場合は、「 [列フィルターの定義および変更](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)」を参照してください。  
  
#### <a name="to-modify-a-static-row-filter-for-a-merge-publication"></a>マージ パブリケーションの静的行フィルターを変更するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、[sp_changemergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) を実行します。 **\@publication**、 **\@article**、 **\@property**、 **\@value** に、それぞれパブリケーション名、フィルター選択の対象アーティクル名、**subset_filterclause**、新しいフィルター選択句 (`WHERE` は含めない) を指定します。 この変更によって既存のサブスクリプションのデータが無効になるため、 **\@force_reinit_subscription** の値に 1 を指定します。  
  
2.  パブリケーションに対してスナップショット エージェント ジョブを再実行し、更新済みスナップショットを生成します。 詳細については、「 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」をご参照ください。  
  
3.  サブスクリプションを再初期化します。 詳細については、「 [サブスクリプションの再初期化](../../../relational-databases/replication/reinitialize-subscriptions.md)」を参照してください。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次のトランザクション レプリケーションの例では、アーティクルを行方向でフィルター選択し、製造停止になった製品をすべて除外します。  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-stat_1.sql)]  
  
 次のマージ レプリケーションの例では、アーティクルを行方向でフィルター選択して、指定した営業担当者に属する行だけを取得します。 結合フィルターも使用されます。 詳しくは、「 [マージ アーティクル間の結合フィルターの定義および変更](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)」をご覧ください。  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-stat_2.sql)]  
  
## <a name="see-also"></a>参照  
 [マージ アーティクルのパラメーター化された行フィルターの定義および変更](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [パブリケーションとアーティクルのプロパティの変更](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [パブリッシュされたデータのフィルター処理](../../../relational-databases/replication/publish/filter-published-data.md)   
 [マージ レプリケーション用にパブリッシュされたデータのフィルター処理](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  
