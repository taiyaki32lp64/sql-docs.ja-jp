---
title: マージ アーティクル間の結合フィルターの定義および変更
description: SQL Server Management Studio (SSMS) または Transact-SQL (T-SQL) を使用して、マージ アーティクル間で使用される結合フィルターを定義および変更する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server replication], join
- merge replication join filters [SQL Server replication]
- modifying filters, join
- join filters
ms.assetid: f7f23415-43ff-40f5-b3e0-0be1d148ee5b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 03911ae4b3addb7a3626b6c9bd0a2c195b719cef
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321567"
---
# <a name="define-and-modify-a-join-filter-between-merge-articles"></a>マージ アーティクル間の結合フィルターの定義および変更
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、マージ アーティクル間の結合フィルターを定義および変更する方法について説明します。 マージ レプリケーションでは結合フィルターがサポートされています。結合フィルターは、通常、テーブル分割を他の関連するテーブル アーティクルに拡張するために、パラメーター化されたフィルターと組み合わせて使用されます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Recommendations (推奨事項)](#Recommendations)  
  
-   **マージ アーティクル間の結合フィルターを定義および変更するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   結合フィルターを作成するには、パブリケーションに少なくとも 2 つの関連テーブルを含める必要があります。 結合フィルターは、行フィルターを拡張したものです。そのため、結合を使用して行フィルターを別のテーブルに拡張するには、先に 1 つのテーブルの行フィルターを定義する必要があります。 結合フィルターを 1 つ定義すると、パブリケーションに追加の関連テーブルが含まれている場合、この結合フィルターは別の結合フィルターを使用して拡張できます。  
  
-   パブリケーションに対するサブスクリプションが初期化された後に、結合フィルターを追加、変更、または削除した場合は、変更を行った後で、新しいスナップショットを生成し、すべてのサブスクリプションを再初期化する必要があります。 プロパティ変更の要件の詳細については、「[Change Publication and Article Properties](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)」(パブリケーションとアーティクルのプロパティの変更) をご覧ください。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   結合フィルターは、一連のテーブルに対して手動で作成できます。また、テーブルに定義された外部キーと主キーのリレーションシップに基づいて、レプリケーションによって自動的に生成することもできます。 一連の結合フィルターを自動的に生成する方法の詳細については、「[Automatically Generate a Set of Join Filters Between Merge Articles &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/automatically-generate-join-filters-between-merge-articles.md)」(マージ アーティクル間で一連の結合フィルターを自動的に生成する (SQL Server Management Studio)) をご覧ください。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページまたは **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[行のフィルター選択]** ページで、結合フィルターを定義、変更、または削除します。 ウィザードの使用およびダイアログ ボックスへのアクセスの詳細については、「[パブリケーションの作成](../../../relational-databases/replication/publish/create-a-publication.md)」および「[View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」 (パブリケーション プロパティの表示および変更) を参照してください。  
  
#### <a name="to-define-a-join-filter"></a>結合フィルターを定義するには  
  
1.  パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** の **[行のフィルター選択]** ページで、 **[フィルター選択されたテーブル]** ペイン内の既存の行フィルターまたは結合フィルターを選択します。  
  
2.  **[追加]** をクリックし、 **[選択したフィルターを拡張するために結合を追加する]** をクリックします。  
  
3.  JOIN ステートメントを作成します。 **[ビルダーを使用してステートメントを作成する]** または **[JOIN ステートメントを手動で作成する]** を選択します。  
  
    -   ビルダーの使用を選択した場合、グリッド内の列 ( **[結合]** 、 **[フィルター選択されたテーブルの列]** 、 **[演算子]** 、 **[結合テーブルの列]** ) を使用して JOIN ステートメントを作成します。  
  
         グリッド内の各列には、ドロップダウン コンボ ボックスが含まれており、2 つの列と 1 つの演算子 ( **=** 、 **<>** 、 **<=** 、 **\<** 、 **>=** 、 **>** 、 **[like]** ) を選択できます。 結果は **[プレビュー]** テキスト領域に表示されます。 結合に列のペアを複数個含める場合は、 **[結合]** 列から結合 (AND または OR) を選択し、さらに 2 つの列と 1 つの演算子を入力します。  
  
    -   ステートメントを手動で作成する場合、 **[JOIN ステートメント]** テキスト領域に JOIN ステートメントを入力します。 **[フィルター選択されたテーブルの列]** ボックスと **[結合テーブルの列]** ボックスを使用して、 **[JOIN ステートメント]** テキスト領域に列をドラッグ アンド ドロップします。  
  
    -   完成した JOIN ステートメントは、次のように表示されます。  
  
        ```  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] INNER JOIN [Sales].[SalesOrderDetail] ON [SalesOrderHeader].[SalesOrderID] = [SalesOrderDetail].[SalesOrderID]  
        ```  
  
         JOIN 句には、2 つの部分で構成されている名前を使用する必要があります。3 つまたは 4 つの部分で構成されている名前の使用はサポートされていません。  
  
4.  結合オプションを指定します。  
  
    -   フィルター選択されたテーブル (親テーブル) 内での結合先の列が一意である場合は、 **[一意キー]** を選択します。  
  
        > [!CAUTION]  
        >  このオプションを選択すると、結合フィルターにおける子テーブルと親テーブルのリレーションシップが一対一または一対多となるように指定されます。 子テーブル内で結合する列に制約があり、一意性が保証される場合にのみ、このオプションを選択します。 このオプションを適切に設定しなかった場合、データを収束できない可能性があります。  
  
    -   既定で、マージ レプリケーションでは同期中に行ごとに変化が処理されます。 フィルター選択されたテーブルと結合されたテーブルの両方の行内の関連する変更を 1 つの単位として処理するには、 **[論理レコード]** ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のバージョンのみ) を選択します。 このオプションは、論理レコードを使用するために必要なアーティクルとパブリケーションの要件が満たされている場合にのみ使用できます。 詳細については、「[Group Changes to Related Rows with Logical Records](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)」(論理レコードによる関連行への変更のグループ化) の「Considerations for Using Logical Records」(論理レコードの使用についての注意点) をご覧ください。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスが表示されている場合は、 **[OK]** をクリックして保存し、ダイアログ ボックスを閉じます。  

#### <a name="to-modify-a-join-filter"></a>結合フィルターを変更するには  
  
1.  パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** の **[行のフィルター選択]** ページで、 **[フィルター選択されたテーブル]** ペイン内のフィルターを選択し、 **[編集]** をクリックします。  
  
2.  **[結合の編集]** ダイアログ ボックスで、フィルターを変更します。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-join-filter"></a>結合フィルターを削除するには  
  
1.  パブリケーションの新規作成ウィザードの **[テーブル行のフィルター選択]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** の **[行のフィルター選択]** ページで、 **[フィルター選択されたテーブル]** ペイン内のフィルターを選択し、 **[削除]** をクリックします。 削除する結合フィルター自体が他の結合によって拡張されている場合は、それらの結合も削除されます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 この手順では、親アーティクルのパラメーター化されたフィルターと、親アーティクルと子アーティクルの結合フィルターを組み合わせて使用する方法について説明します。 結合フィルターは、レプリケーションのストアド プロシージャを使用してプログラムから定義したり変更したりできます。  
  
#### <a name="to-define-a-join-filter-to-extend-an-article-filter-to-related-articles-in-a-merge-publication"></a>アーティクル フィルターをマージ パブリケーションの関連アーティクルに拡張する結合フィルターを定義するには  
  
1.  結合先アーティクル (親アーティクル) のフィルターを定義します。  
  
    -   パラメーター化された行フィルターを使ったアーティクルのフィルター選択については、「 [マージ アーティクルのパラメーター化された行フィルターの定義および変更](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)」を参照してください。  
  
    -   静的行フィルターを使ったアーティクルのフィルター選択については、「 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)」を参照してください。  
  
2.  パブリッシャーのパブリケーション データベースで [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) を実行し、関連アーティクル (パブリケーションの子アーティクル) を少なくとも 1 つ定義します。 詳しくは、「 [アーティクルを定義](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
3.  パブリッシャー側のパブリケーション データベースに対して、[sp_addmergefilter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) を実行します。 `@publication` を指定し、`@filtername` にはこのフィルターの一意の名前を、`@article` には手順 2 で作成した子アーティクルの名前を、`@join_articlename` には結合対象の親アーティクルの名前を指定し、`@join_unique_key` に次のいずれかの値を指定します。  
  
    -   **0** - 親アーティクルと子アーティクル間の多対一または多対多の結合を示します。  
  
    -   **1** - 親アーティクルと子アーティクル間の一対一または一対多の結合を示します。  
  
     これにより、2 つのアーティクル間の結合フィルターが定義されます。  
  
    > [!CAUTION]  
    >  親アーティクルの基になるテーブルで、結合する列に一意性を保証する制約が割り当てられている場合にのみ、`@join_unique_key` を **1** に設定します。 `@join_unique_key` を **1** に正しく設定しなかった場合は、データの非収束が発生する可能性があります。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、マージ パブリケーションのアーティクルを定義しています。 `SalesOrderDetail` テーブルのアーティクルが、 `SalesOrderHeader` テーブルと比較されてフィルター選択されます (このテーブル自体が静的行フィルターを使ってフィルター選択されています)。 詳しくは、「 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)」をご覧ください。  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-join_1.sql)]  
  
 次の例では、マージ パブリケーションでアーティクル グループを定義しています。アーティクルは、 `Employee` テーブルと比較されて、一連の結合フィルターを使ってフィルター選択されます (このテーブル自体が、 [LoginID](../../../t-sql/functions/host-name-transact-sql.md) 列の **HOST_NAME** の値に対するパラメーター化された行フィルターを使ってフィルター選択されています)。 詳しくは、「 [マージ アーティクルのパラメーター化された行フィルターの定義および変更](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)」をご覧ください。  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-join_2.sql)]  
  
## <a name="see-also"></a>参照  
 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [パブリケーションとアーティクルのプロパティの変更](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [マージ レプリケーション用にパブリッシュされたデータのフィルター処理](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)   
 [方法: マージ アーティクル間の結合フィルターを定義および変更する (SQL Server Management Studio)](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Define a Logical Record Relationship Between Merge Table Articles](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [マージ アーティクルのパラメーター化された行フィルターの定義および変更](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
  
