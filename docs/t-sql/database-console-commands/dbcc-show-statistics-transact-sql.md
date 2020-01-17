---
title: DBCC SHOW_STATISTICS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SHOW_STATISTICS_TSQL
- DBCC SHOW_STATISTICS
- SHOW_STATISTICS
- DBCC_SHOW_STATISTICS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- query optimization statistics [SQL Server], densities
- histograms [SQL Server]
- statistical information [SQL Server], viewing statistics objects
- current distribution statistics
- query optimization statistics [SQL Server], histograms
- DBCC SHOW_STATISTICS statement
- distribution statistics
- statistical information [SQL Server], densities
- statistics objects
- statistical information [SQL Server], histograms
- query optimization statistics [SQL Server], viewing statistics objects
- statistical information [SQL Server], distribution
- densities [SQL Server]
- displaying distribution statistics
ms.assetid: 12be2923-7289-4150-b497-f17e76a50b2e
author: pmasl
ms.author: umajay
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 327b084471155c9e7d8451fc8dceec8e4c00496f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116478"
---
# <a name="dbcc-showstatistics-transact-sql"></a>DBCC SHOW_STATISTICS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

DBCC SHOW_STATISTICS では、テーブルまたはインデックス付きビューについての、現在のクエリの最適化に関する統計を表示します。 クエリ オプティマイザーでは、統計を使用してクエリ結果のカーディナリティや行数を推定することで、高品質のクエリ プランを作成できます。 たとえば、クエリ オプティマイザーでは、カーディナリティの推定に基づいて、クエリ プランで Index Scan 操作ではなく Index Seek 操作が使用される場合があります。この場合、リソースを大量に消費する Index Scan 操作を使用しないようにすることでパフォーマンスが向上します。
  
クエリ オプティマイザーでは、テーブルまたはインデックス付きビューの統計を統計オブジェクトに格納します。 テーブルの場合、インデックスまたはテーブル列のリストに関する統計オブジェクトが作成されます。 統計オブジェクトには、統計に関するメタデータが含まれるヘッダー、統計オブジェクトの最初のキー列の値の分布が含まれるヒストグラム、および列間の相関関係を測定する密度ベクトルが格納されています。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]では、統計オブジェクトの任意のデータを使用してカーディナリティの推定を計算できます。
  
DBCC SHOW_STATISTICS では、統計オブジェクトに格納されたデータに基づくヘッダー、ヒストグラム、および密度ベクトルを表示します。 この構文では、テーブルまたはインデックス付きビューを指定するときに、対象のインデックス名、統計名、または列名も指定することができます。 このトピックでは、統計の表示方法と表示される結果の意味について説明します。
  
詳細については、「 [Statistics](../../relational-databases/statistics/statistics.md)」を参照してください。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```
-- Syntax for SQL Server and Azure SQL Database  
  
DBCC SHOW_STATISTICS ( table_or_indexed_view_name , target )   
[ WITH [ NO_INFOMSGS ] < option > [ , n ] ]  
< option > :: =  
    STAT_HEADER | DENSITY_VECTOR | HISTOGRAM | STATS_STREAM  
```  
  
```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

DBCC SHOW_STATISTICS ( table_name , target )   
    [ WITH {STAT_HEADER | DENSITY_VECTOR | HISTOGRAM } [ ,...n ] ]  
[;]  
```  
  
## <a name="arguments"></a>引数  
 *table_or_indexed_view_name*  
 統計情報を表示するテーブルまたはインデックス付きビューの名前。  
  
 *table_name*  
 表示する統計情報を含むテーブルの名前。 テーブルに外部テーブルを指定することはできません。  
  
 *移行先*  
 統計情報を表示するインデックス、統計、または列の名前。 *target* は、角かっこ、一重引用符、二重引用符で囲まれるか、または引用符を使用しません。 *target* がテーブルまたはインデックス付きビューの既存のインデックスまたは統計の名前である場合は、その target に関する統計情報が返されます。 *target* が既存の列の名前であり、自動的に作成された統計がその列にある場合は、その自動作成された統計に関する情報が返されます。 target 列に自動的に作成された統計が存在しない場合は、エラー メッセージ 2767 が返されます。  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] および[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] では、*target* を列名にすることはできません。  
  
 NO_INFOMSGS  
 重大度レベル 0 から 10 のすべての情報メッセージを表示しないようにします。  
  
 STAT_HEADER | DENSITY_VECTOR | HISTOGRAM | STATS_STREAM [ **,** _n_ ]  
 これらのオプションを 1 つ以上指定すると、ステートメントによって返される結果セットが、指定のオプションに合わせて制限されます。 オプションを指定しないと、すべての統計情報が返されます。  
  
 STATS_STREAM は[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="result-sets"></a>結果セット  
次の表は、STAT_HEADER を指定した場合に結果セットに返される列を示しています。
  
|列名|[説明]|  
|-----------------|-----------------|  
|[オブジェクト名]|統計オブジェクトの名前。|  
|[更新]|統計情報が最後に更新された日付と時刻。 [STATS_DATE](../../t-sql/functions/stats-date-transact-sql.md) 関数でこの情報を取得することもできます。 詳細については、このページの「[解説](#Remarks)」セクションを参照してください。|  
|[行]|統計情報が最後に更新された時点のテーブルまたはインデックス付きビューの行の総数。 統計がフィルター選択されている場合、またはフィルター選択されたインデックスに対応している場合は、行数がテーブルの行数よりも少なくなることがあります。 詳細については、「[統計情報](../../relational-databases/statistics/statistics.md)」を参照してください。|  
|[サンプリングされた行数]|統計の計算時にサンプリングされた行の合計数。 Rows Sampled < Rows の場合、表示されるヒストグラムおよび密度の結果は、サンプリングされた行に基づいて推定されます。|  
|手順|ヒストグラムの区間の数。 各区間の範囲には、上限の列値までの列値の範囲が含まれます。 ヒストグラムの区間は、統計の最初のキー列に基づいて定義されます。 区間の最大数は 200 です。|  
|[密度]|ヒストグラムの境界値を除く、統計オブジェクトの最初のキー列のすべての値について、"1 / *distinct values* " として計算されます。 この Density の値はクエリ オプティマイザーでは使用されません。[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] より前のバージョンとの互換性を維持するために表示されます。|  
|[キーの平均の長さ]|統計オブジェクトのすべてのキー列の、値ごとの平均バイト数。|  
|String Index|Yes の場合は、統計オブジェクトに文字列の統計概要が含まれています。これにより、LIKE 演算子を使用するクエリ述語 (`WHERE ProductName LIKE '%Bike'` など) に対するカーディナリティの推定が向上します。 文字列の統計概要は、ヒストグラムとは別に格納されます。この統計は、統計オブジェクトの最初のキー列について、その型が **char**、**varchar**、**nchar**、**nvarchar**、**varchar(max)** 、**nvarchar(max)** 、**text**、**ntext** である場合に作成されます。|  
|[フィルター式]|統計オブジェクトに含まれるテーブル行のサブセットの述語。 NULL = フィルター選択されていない統計情報です。 フィルター選択された述語の詳細については、「[フィルター選択されたインデックスの作成](../../relational-databases/indexes/create-filtered-indexes.md)」を参照してください。 フィルター選択された統計情報の詳細については、「[統計情報](../../relational-databases/statistics/statistics.md)」を参照してください。|  
|[フィルター処理なしの行数]|フィルター式を適用する前のテーブル内の行の合計数。 [フィルター式] が NULL の場合、[フィルター処理なしの行数] は [行数] と同じになります。|  
|永続化されたサンプルのパーセンテージ|サンプリングの割合を明示的に指定しない統計情報の更新に使用される永続化されたサンプルのパーセンテージです。 値がゼロの場合、永続化されたサンプルのパーセンテージがこの統計に設定されていません。<br /><br /> **適用対象:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4| 
  
次の表は、DENSITY_VECTOR を指定した場合に結果セットに返される列を示しています。
  
|列名|[説明]|  
|-----------------|-----------------|  
|[すべての密度]|密度は "1 / *distinct values*" です。 結果には、統計オブジェクトの列の各プレフィックスに対する密度が、密度ごとに 1 行表示されます。 個別の値は、行および列プレフィックスごとの列値の個別のリストです。 たとえば、統計オブジェクトにキー列 (A, B, C) が含まれる場合、結果では列プレフィックス (A)、(A, B)、(A, B, C) ごとに個別の値リストの密度が報告されます。 プレフィックス (A、B、C) を使用すると、これらの各リストは次の個別の値リストになります。(3, 5, 6)、(4, 4, 6)、(4, 5, 6)、(4, 5, 7)。 プレフィックス (A、B) を使用すると、同じ列値に次の個別の値リストが含まれます。(3, 5)、(4, 4) および (4, 5)|  
|[平均の長さ]|列プレフィックスの列値のリストを格納する平均の長さ (バイト単位)。 たとえば、リスト (3, 5, 6) の値ごとに 4 バイト必要な場合は、長さは 12 バイトになります。|  
|[列]|[すべての密度] および [平均の長さ] を表示するプレフィックスの列の名前。|  
  
次の表は、HISTOGRAM オプションを指定した場合に結果セットに返される列を示しています。
  
|列名|[説明]|  
|---|---|
|[RANGE_HI_KEY]|ヒストグラム区間の上限の列値。 この列値はキー値とも呼ばれます。|  
|RANGE_ROWS|ヒストグラム区間内 (上限は除く) に列値がある行の予測数。|  
|EQ_ROWS|ヒストグラム区間の上限と列値が等しい行の予測数。|  
|DISTINCT_RANGE_ROWS|ヒストグラム区間内 (上限は除く) にある個別の列値を持つ行の予測数。|  
|AVG_RANGE_ROWS|上限を除く、ヒストグラムのステップ内で重複する列の値を持つ行の数の平均値。 DISTINCT_RANGE_ROWS が 0 より大きいとき、RANGE_ROWS を DISTINCT_RANGE で割ることで AVG_RANGE_ROWS が計算されます。 DISTINCT_RANGE_ROWS が 0 のとき、AVG_RANGE_ROWS はヒストグラムのステップに対して 1 を返します。| 
  
## <a name="Remarks"></a> 解説 

統計の更新日付は、メタデータではなく[統計 BLOB オブジェクト](../../relational-databases/statistics/statistics.md#DefinitionQOStatistics)に[ヒストグラム](#histogram)および[密度ベクトル](#density)と共に格納されます。 統計データを生成するためのデータが読み取られていない場合、統計 BLOB は作成されず、日付は使用できず、*updated* 列は NULL になります。 これは、述語が行を返さないフィルター選択された統計情報や、新しい空のテーブルの場合です。
  
## <a name="histogram"></a> ヒストグラム  
ヒストグラムでは、データセットの個別の値ごとに出現頻度を測定します。 クエリ オプティマイザーでは、統計オブジェクトの最初のキー列の列値に基づいてヒストグラムを計算し、行を統計的にサンプリングするかテーブルまたはビュー内のすべての行でフル スキャンを実行することによって列値を選択します。 サンプリングされた行のセットからヒストグラムを作成する場合、格納される行の総数および個別の値の数は推定値であり、必ずしも整数にはなりません。
  
ヒストグラムを作成するには、クエリ オプティマイザーで列値を並べ替え、個別の列値ごとに一致する値の数を計算し、列値を最大 200 の連続したヒストグラム区間に集計します。 各区間には、上限の列値までの列値の範囲が含まれます。 この範囲には、境界値の間 (境界値自体は除く) のすべての有効な列値が含まれます。 格納される最小の列値は、最初のヒストグラム区間の上限境界値になります。
  
次の図は、6 つの区間があるヒストグラムを示しています。 最初の上限境界値の左側にある領域が最初の区間です。
  
![](../../relational-databases/system-dynamic-management-views/media/a0ce6714-01f4-4943-a083-8cbd2d6f617a.gif "a0ce6714-01f4-4943-a083-8cbd2d6f617a")
  
ヒストグラムの各区間は、以下のように表されます。
-   太線は、上限境界値 (RANGE_HI_KEY) およびその出現回数 (EQ_ROWS) を表します。  
-   RANGE_HI_KEY の左にある領域は、列値の範囲、およびそれぞれの列値の平均出現回数 (AVG_RANGE_ROWS) を表します。 最初のヒストグラム区間の AVG_RANGE_ROWS は常に 0 です。  
-   点線は、範囲内にある個別の値の総数 (DISTINCT_RANGE_ROWS) および範囲内の値の総数 (RANGE_ROWS) を推定するために使用されるサンプリングされた値を表します。 クエリ オプティマイザーでは、RANGE_ROWS および DISTINCT_RANGE_ROWS を使用して AVG_RANGE_ROWS を計算します。サンプリングされた値は格納されません。  
  
クエリ オプティマイザーでは、統計的有意性に応じてヒストグラム区間を定義します。 区間幅を最大にするアルゴリズムを使用して境界値の差を最大にし、ヒストグラムの区間の数を最小限に抑えます。 区間の最大数は 200 です。 ヒストグラムの区間の数は、境界点が 200 より少ない列でも、個別の値の数より少なくなることがあります。 たとえば、個別の値が 100 個ある列のヒストグラムの境界点が 100 より少なくなる場合もあります。
  
## <a name="density"></a> 密度ベクトル  
クエリ オプティマイザーでは、同一のテーブルまたはインデックス付きビューから複数の列を返すクエリに対するカーディナリティの推定を向上させるために密度を使用します。 密度ベクトルには、統計オブジェクトの列のプレフィックスごとに 1 つの密度が格納されます。 たとえば、統計オブジェクトに `CustomerId`、`ItemId`、`Price` というキー列がある場合、以下の列プレフィックスごとに密度が計算されます。
  
|列プレフィックス|密度の計算対象|  
|---|---|
|(CustomerId)|CustomerId の値が一致する行|  
|(CustomerId, ItemId)|CustomerId および ItemId の値が一致する行|  
|(CustomerId, ItemId, Price)|CustomerId、ItemId、および Price の値が一致する行|  
  
## <a name="restrictions"></a>制限  
 DBCC SHOW_STATISTICS では、空間インデックスおよび xVelocity メモリ最適化列ストア インデックスの統計情報は提供されません。  
  
## <a name="permissions-for-includessnoversionincludesssnoversion-mdmd-and-includesssdsincludessssds-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[ssSDS](../../includes/sssds-md.md)] のアクセス許可  
統計オブジェクトを表示するには、テーブルを所有しているか、固定サーバー ロール `sysadmin`、固定データベース ロール `db_owner`、または固定データベース ロール `db_ddladmin` のメンバーである必要があります。
  
[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 で、権限に関する制限が変更され、SELECT 権限でこのコマンドを使用できるようになりました。 SELECT 権限でコマンドを実行するときは、次の要件に注意してください。
-   統計オブジェクトのすべての列に対する権限が必要です。  
-   フィルター条件がある場合は、そのすべての列に対する権限が必要です。  
-   テーブルには、行レベルのセキュリティ ポリシーを持つことはできません。  
  
この動作を無効にするには、トレース フラグ 9485 を使用します。
  
## <a name="permissions-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] のアクセス許可  
DBCC SHOW_STATISTICS では、次のいずれかのメンバーシップまたはテーブルに対する SELECT 権限が必要です。
-   sysadmin 固定サーバー ロール  
-   db_owner 固定データベース ロール  
-   db_ddladmin 固定データベース ロール  
  
## <a name="limitations-and-restrictions-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] の制限事項と制約事項  
DBCC SHOW_STATISTICS では、コントロールのノード レベルでのシェル データベースに格納されている統計情報を表示します。 計算ノード上で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって自動的に作成される統計情報は表示されません。
  
DBCC SHOW_STATISTICS は、外部テーブルではサポートされません。
  
## <a name="examples-includessnoversionincludesssnoversion-mdmd-and-includesssdsincludessssds-mdmd"></a>例: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
### <a name="a-returning-all-statistics-information"></a>A. すべての統計情報を返す  
次の例は、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベース内の `AK_Address_rowguid` テーブルの `Person.Address` インデックスに関するすべての統計情報を表示します。
  
```sql
DBCC SHOW_STATISTICS ("Person.Address", AK_Address_rowguid);  
GO  
```  
  
### <a name="b-specifying-the-histogram-option"></a>B. HISTOGRAM オプションを指定する  
これによりを HISTOGRAM データ Customer_LastName を表示する統計情報が制限されます。
  
```sql
DBCC SHOW_STATISTICS ("dbo.DimCustomer",Customer_LastName) WITH HISTOGRAM;  
GO  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="c-display-the-contents-of-one-statistics-object"></a>C. 1 つの統計オブジェクトの内容を表示します。  
 次の例では、DimCustomer テーブル Customer_LastName 統計の内容を表示します。  
  
```sql
-- Uses AdventureWorks  
--First, create a statistics object  
CREATE STATISTICS Customer_LastName   
ON AdventureWorksPDW2012.dbo.DimCustomer (LastName);  
GO  
DBCC SHOW_STATISTICS ("dbo.DimCustomer",Customer_LastName);  
GO  
```  
  
結果は、ヘッダー、密度ベクトル、およびヒストグラムの一部を示します。
  
![DBCC SHOW_STATISTICS の結果](../../t-sql/database-console-commands/media/aps-sql-dbccshow-statistics.JPG "DBCC SHOW_STATISTICS の結果")
  
## <a name="see-also"></a>参照  
[統計](../../relational-databases/statistics/statistics.md)  
[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
[CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)  
[DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)  
[sp_autostats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)  
[sp_createstats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)  
[STATS_DATE &#40;Transact-SQL&#41;](../../t-sql/functions/stats-date-transact-sql.md)  
[UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)  
[sys.dm_db_stats_properties (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)  
[sys.dm_db_stats_histogram (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)   
