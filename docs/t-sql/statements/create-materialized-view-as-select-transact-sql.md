---
title: CREATE MATERIALIZED VIEW AS SELECT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: data-warehouse
ms.topic: language-reference
f1_keywords:
- CREATE VIEW
- VIEW_TSQL
- VIEW
- CREATE_VIEW_TSQL
- SCHEMABINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table creation [SQL Server], CREATE VIEW
- views [SQL Server], creating
- CREATE VIEW statement
- updatable partitioned views
- tables [SQL Server], virtual
- updatable views
- modifying partitioned views
- virtual tables [SQL Server]
- number of columns per view
- partitioned views [SQL Server], creating
- WITH ENCRYPTION clause
- WITH CHECK OPTION clause
- partitioned views [SQL Server], modifying
- partitioned views [SQL Server], replication
- distributed partitioned views [SQL Server]
- views [SQL Server], indexed views
- maximum number of columns per view
ms.assetid: aecc2f73-2ab5-4db9-b1e6-2f9e3c601fb9
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: e8acc3ef73c51ccbbf195f9d18dc5f12d661931f
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75226742"
---
# <a name="create-materialized-view-as-select-transact-sql"></a>CREATE MATERIALIZED VIEW AS SELECT (Transact-SQL)  

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

この記事では、ソリューション開発用の Azure SQL Data Warehouse の CREATE MATERIALIZED VIEW AS SELECT T-SQL ステートメントについて説明します。 この記事には、コード例も記載されています。

具体化されたビューでは、ビュー定義クエリから返されるデータを保持し、基になるテーブルのデータが変更されると自動的に更新されます。   これによって、複雑なクエリ (一般に結合と集計を含むクエリ) のパフォーマンスが向上すると共に、メンテナンス操作が簡単になります。   実行プランの自動一致機能により、置換するビューをオプティマイザーで検討する際、具体化されたビューをクエリで参照する必要はありません。  これにより、データ エンジニアは、クエリを変更せずにクエリの応答時間を短縮するメカニズムとして、具体化されたビューを実装できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
CREATE MATERIALIZED VIEW [ schema_name. ] materialized_view_name
    WITH (  
      <distribution_option>
    )
    AS <select_statement>
[;]

<distribution_option> ::=
    {  
        DISTRIBUTION = HASH ( distribution_column_name )  
      | DISTRIBUTION = ROUND_ROBIN  
    }

<select_statement> ::=
    SELECT select_criteria
```  
  
## <a name="arguments"></a>引数

*schema_name*     
 ビューが所属するスキーマの名前を指定します。  
  
*materialized_view_name*   
ビューの名前です。 ビュー名は、識別子のルールに従っている必要があります。 ビューの所有者名の指定は省略可能です。  

*distribution option*     
サポートされる分布は、HASH および ROUND_ROBIN のみです。

*select_statement*   
具体化されたビューの定義の SELECT リストでは、以下の 2 つの条件の 1 つ以上が満たされている必要があります。
- SELECT リストに集計関数が含まれています。
- 具体化されたビューの定義で GROUP BY が使用されており、GROUP BY 内のすべての列が SELECT リストに含まれています。  GROUP BY 句では、最大 32 列使用できます。

具体化されたビューの定義の SELECT リストには、集計関数が必要です。  サポートされる集計には、MAX、MIN、AVG、COUNT、COUNT_BIG、SUM、VAR、STDEV が含まれます。

具体化されたビューの定義の SELECT リストで MIN/MAX 集計が使用される場合、以下の要件が適用されます。
 
- FOR_APPEND が必要です。  次に例を示します。
  ```sql 
  CREATE MATERIALIZED VIEW mv_test2  
  WITH (distribution = hash(i_category_id), FOR_APPEND)  
  AS
  SELECT MAX(i.i_rec_start_date) as max_i_rec_start_date, MIN(i.i_rec_end_date) as min_i_rec_end_date, i.i_item_sk, i.i_item_id, i.i_category_id
  FROM syntheticworkload.item i  
  GROUP BY i.i_item_sk, i.i_item_id, i.i_category_id
  ```

- 参照されるベース テーブルで UPDATE または DELETE が実行されると、具体化されたビューが無効になります。  この制限は、INSERT には適用されません。  具体化されたビューを再度有効にするには、REBUILD を指定して ALTER MATERIALIZED INDEX を実行します。
  
## <a name="remarks"></a>解説

Azure データ ウェアハウスの具体化されたビューは、SQL Server のインデックス付きビューによく似ています。  具体化されたビューで集計関数がサポートされる点を除き、インデックス付きビューとほぼ同じ制限が共有されています (詳細については、「[Create Indexed Views (インデックス付きビューを作成する)](/sql/relational-databases/views/create-indexed-views)」 を参照してください)。   ここでは、具体化されたビューのその他の考慮事項について説明します。  
 
具体化されたビューでは、CLUSTERED COLUMNSTORE INDEX のみがサポートされます。 

具体化されたビューでは、他のビューを参照できません。  
 
具体化されたビューは、パーティション テーブル上で作成できます。  具体化されたビューで参照されるテーブル上では、SPLIT/MERGE 操作がサポートされます。  具体化されたビューで参照されるテーブル上では、SWITCH はサポートされません。 試行した場合、`Msg 106104, Level 16, State 1, Line 9` というエラーが表示されます
 
具体化されたビューで参照されるテーブル上では、ALTER TABLE SWITCH はサポートされません。 ALTER TABLE SWITCH を使用する前に、具体化されたビューを無効にするか、ドロップします。 以下のシナリオでは、具体化されたビューを作成する際、このビューに新しい列を追加する必要があります。

|シナリオ|具体化されたビューに追加する新しい列|解説|  
|-----------------|---------------|-----------------|
|COUNT_BIG() は、具体化されたビューの定義の SELECT リストで欠落しています| COUNT_BIG (*) |具体化されたビューを作成する際に自動的に追加されます。  ユーザーによる操作は不要です。|
|具体化されたビューの定義の SELECT リストでユーザーが SUM(a) を指定しています。また、"a" は null 許容式です |COUNT_BIG (a) |ユーザーは、具体化されたビューの定義で式 "a" を手動で追加する必要があります。|
|具体化されたビューの定義の SELECT リストでユーザーが AVG(a) を指定しています。ここで "a" は式です。|SUM(a), COUNT_BIG(a)|具体化されたビューを作成する際に自動的に追加されます。  ユーザーによる操作は不要です。|
|具体化されたビューの定義の SELECT リストでユーザーが STDEV(a) を指定しています。ここで "a" は式です。|SUM(a), COUNT_BIG(a), SUM(square(a))|具体化されたビューを作成する際に自動的に追加されます。  ユーザーによる操作は不要です。 |
| | | |

具体化されたビューは、一度作成されると、SQL Server Management Studio 内の Azure SQL Data Warehouse インスタンスのビュー フォルダーの下に表示されます。

[SP_SPACEUSED](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql?view=azure-sqldw-latest) および [DBCC PDW_SHOWSPACEUSED](/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql?view=azure-sqldw-latest) を実行すると、具体化されたビューで使用されるスペースを決定できます。  

具体化されたビューは、DROP VIEW でドロップできます。  ALTER MATERIALIZED VIEW を使用して、具体化されたビューを無効にしたり、リビルドしたりできます。   

SQL Server Management Studio 内の説明プランとグラフィカルな推定実行プランを見ると、クエリ実行の際、具体化されたビューがクエリ オプティマイザーで考慮されるかどうかがわかります。 SQL Server Management Studio 内のグラフィカルな推定実行プランを見ると、クエリ実行の際、具体化されたビューがクエリ オプティマイザーで考慮されるかどうかがわかります。

新しい具体化されたビューから SQL ステートメントでメリットが得られるかどうかを確認するには、`WITH_RECOMMENDATIONS` を指定して `EXPLAIN` コマンドを実行します。  詳細については、「[EXPLAIN (Transact-SQL)](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)」を参照してください。

## <a name="permissions"></a>アクセス許可

データベースの CREATE VIEW 権限と、ビューが作成されているスキーマの ALTER 権限が必要です。 
  
## <a name="see-also"></a>参照

[具体化されたビューを使用したパフォーマンス チューニング](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)      
[EXPLAIN &#40;Transact-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[SQL Data Warehouse and Parallel Data Warehouse Catalog Views (SQL Data Warehouse および Parallel Data Warehouse のカタログ ビュー)](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[System views supported in Azure SQL Data Warehouse (Azure SQL Data Warehouse でサポートされるシステム ビュー)](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[T-SQL statements supported in Azure SQL Data Warehouse (Azure SQL Data Warehouse でサポートされる T-SQL ステートメント)](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
