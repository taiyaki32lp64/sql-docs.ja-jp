---
title: DBCC INDEXDEFRAG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- INDEXDEFRAG
- DBCC INDEXDEFRAG
- DBCC_INDEXDEFRAG_TSQL
- INDEXDEFRAG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- defragmenting indexes
- DBCC INDEXDEFRAG statement
- leaf level defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
ms.assetid: 3c7df676-4843-44d0-8c1c-a9ab7e593b70
author: pmasl
ms.author: umajay
ms.openlocfilehash: 7372051d8dfb23430f834ca159125822c6892956
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116534"
---
# <a name="dbcc-indexdefrag-transact-sql"></a>DBCC INDEXDEFRAG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

指定されたテーブルまたはビューのインデックスをデフラグします。
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 代わりに [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) を使用してください。  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DBCC INDEXDEFRAG  
(  
    { database_name | database_id | 0 }   
    , { table_name | table_id | view_name | view_id }   
    [ , { index_name | index_id } [ , { partition_number | 0 } ] ]  
)  
    [ WITH NO_INFOMSGS ]   
```  
  
## <a name="arguments"></a>引数  
 *database_name* | *database_id* | 0  
 断片化を解消するインデックスが含まれているデータベースを指定します。 0 を指定すると、現在のデータベースが選択されます。 データベース名は、[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。  
  
 *table_name* | *table_id* | *view_name* | *view_id*  
 断片化を解消するインデックスが含まれているテーブルまたはビューを指定します。 テーブル名とビュー名は、識別子の規則に従っている必要があります。  
  
 *index_name* | *index_id*  
 断片化を解消するインデックスの ID または名前を指定します。 インデックス ID を指定しないと、ステートメントは指定されたテーブルまたはビューのすべてのインデックスをデフラグします。 インデックス名は、識別子の規則に従っている必要があります。  
  
 *partition_number* | 0  
 デフラグするインデックスのパーティション番号です。 パーティション番号を指定しない場合、またはパーティション番号に 0 を指定した場合、ステートメントは指定されたインデックス内のすべてのパーティションをデフラグします。  
  
 WITH NO_INFOMSGS  
 重大度レベル 0 から 10 のすべての情報メッセージを表示しないようにします。  
  
## <a name="remarks"></a>Remarks  
DBCC INDEXDEFRAG は、リーフ ページの物理順序がリーフ ノードでの左から右への論理順序と一致するように、インデックスのリーフ レベルをデフラグするので、インデックスのスキャンのパフォーマンスが向上します。
  
> [!NOTE]  
>  DBCC INDEXDEFRAG が実行されると、インデックスの断片化解消が直列に実行されます。 つまり、単一のスレッドを使用して、単一のインデックスについて操作が実行されます。 並列処理は実行されません。 また、同じ DBCC INDEXDEFRAG ステートメントからの複数のインデックスについての操作は、1 つのインデックスについて同時に実行されます。  
  
また、DBCC INDEXDEFRAG は、インデックス作成時に指定された FILL FACTOR を考慮しながら、インデックスのページの圧縮も行います。 この圧縮によって作成された空のページは削除されます。 詳細については、「 [インデックスの FILL FACTOR の指定](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)」を参照してください。
  
インデックスが複数のファイルにわたる場合は、DBCC INDEXDEFRAG は一度に 1 つのファイルに対して断片化の解消を行います。 ページがファイル間を移動することはありません。
  
DBCC INDEXDEFRAG は、5 分ごとに、完了した割合の予測値をレポートします。 DBCC INDEXDEFRAG は、プロセスのどの時点でも停止することができ、停止時に完了していた作業は保持されます。
  
DBCC DBREINDEX (または一般のインデックス構築操作) とは異なり、DBCC INDEXDEFRAG はオンライン操作です。 この操作では、長期間にわたってロックを保持することはありません。 したがって、DBCC INDEXDEFRAG はクエリまたは更新の実行をブロックしません。 デフラグの所要時間は断片化のレベルに関係するため、比較的断片化されていないインデックスのデフラグは、新しいインデックスの構築にかかる時間よりも短時間で済む場合があります。 断片化がかなり進んでいるインデックスの場合、デフラグすると、再構築するよりも所用時間が著しく長くなる場合があります。
  
デフラグは、データベース復旧モデルの設定にかかわらず、常にすべてログに記録されます。 詳細については、「[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)」を参照してください。 断片化がかなり進んだインデックスをデフラグした場合、インデックスの作成をすべてログに記録したときよりも多くのログが生成される可能性があります。 ただし、ログのバックアップが頻繁に作成されているか、または復旧モデルに SIMPLE が設定されている場合、断片化の解消は一連の短いトランザクションとして実行されるため大量のログは必要なくなります。
  
## <a name="restrictions"></a>制限  
DBCC INDEXDEFRAG は、インデックス リーフ ページの再編成を行います。 したがって、特定のインデックスがディスク上の他のインデックスと交互に配置されている場合は、そのインデックスに対して DBCC INDEXDEFRAG を実行すると、隣接するインデックス内では一部のリーフ ページが作成されません。 ページが連続して配置されるようにするには、インデックスを再構築します。
DBCC INDEXDEFRAG を使用して次のインデックスの断片化を解消することはできません。
-   無効化されたインデックス。  
-   ページ ロックが OFF に設定されたインデックス。  
-   空間インデックスです。  
  
DBCC INDEXDEFRAG は、システム テーブルに対して使用できません。
  
## <a name="result-sets"></a>結果セット  
DBCC INDEXDEFRAG は、(WITH NO_INFOMSGS が指定されている場合を除き) インデックスがステートメント内で指定されている場合に、次の結果セットを返します (値は異なることがあります)。
  
```sql
Pages Scanned Pages Moved Pages Removed  
------------- ----------- -------------  
359           346         8  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>アクセス許可  
呼び出し元はテーブルまたはインデックス付きビューを所有しているか、固定サーバー ロール **sysadmin**、固定データベース ロール **db_owner**、または固定データベース ロール **db_ddladmin** のメンバーである必要があります。
  
## <a name="examples"></a>使用例  
### <a name="a-using-dbcc-indexdefrag-to-defragment-an-index"></a>A. DBCC INDEXDEFRAG を使用してインデックスの断片化を解消する  
次の例では、`AdventureWorks` データベースの `Production.Product` テーブルにある `PK_Product_ProductID` インデックスのすべてのパーティションをデフラグします。
  
```sql  
DBCC INDEXDEFRAG (AdventureWorks2012, 'Production.Product', PK_Product_ProductID);  
GO  
```  
  
### <a name="b-using-dbcc-showcontig-and-dbcc-indexdefrag-to-defragment-the-indexes-in-a-database"></a>B. DBCC SHOWCONTIG と DBCC INDEXDEFRAG を使用してデータベース内のインデックスの断片化を解消する  
 次の例では、宣言されたしきい値を超えて断片化しているデータベースのインデックスすべての断片化を解消する、簡単な方法を示しています。  
  
```sql  
/*Perform a 'USE <database name>' to select the database in which to run the script.*/  
-- Declare variables  
SET NOCOUNT ON;  
DECLARE @tablename varchar(255);  
DECLARE @execstr   varchar(400);  
DECLARE @objectid  int;  
DECLARE @indexid   int;  
DECLARE @frag      decimal;  
DECLARE @maxfrag   decimal;  
  
-- Decide on the maximum fragmentation to allow for.  
SELECT @maxfrag = 30.0;  
  
-- Declare a cursor.  
DECLARE tables CURSOR FOR  
   SELECT TABLE_SCHEMA + '.' + TABLE_NAME  
   FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_TYPE = 'BASE TABLE';  
  
-- Create the table.  
CREATE TABLE #fraglist (  
   ObjectName char(255),  
   ObjectId int,  
   IndexName char(255),  
   IndexId int,  
   Lvl int,  
   CountPages int,  
   CountRows int,  
   MinRecSize int,  
   MaxRecSize int,  
   AvgRecSize int,  
   ForRecCount int,  
   Extents int,  
   ExtentSwitches int,  
   AvgFreeBytes int,  
   AvgPageDensity int,  
   ScanDensity decimal,  
   BestCount int,  
   ActualCount int,  
   LogicalFrag decimal,  
   ExtentFrag decimal);  
  
-- Open the cursor.  
OPEN tables;  
  
-- Loop through all the tables in the database.  
FETCH NEXT  
   FROM tables  
   INTO @tablename;  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
-- Do the showcontig of all indexes of the table  
   INSERT INTO #fraglist   
   EXEC ('DBCC SHOWCONTIG (''' + @tablename + ''')   
      WITH FAST, TABLERESULTS, ALL_INDEXES, NO_INFOMSGS');  
   FETCH NEXT  
      FROM tables  
      INTO @tablename;  
END;  
  
-- Close and deallocate the cursor.  
CLOSE tables;  
DEALLOCATE tables;  
  
-- Declare the cursor for the list of indexes to be defragged.  
DECLARE indexes CURSOR FOR  
   SELECT ObjectName, ObjectId, IndexId, LogicalFrag  
   FROM #fraglist  
   WHERE LogicalFrag >= @maxfrag  
      AND INDEXPROPERTY (ObjectId, IndexName, 'IndexDepth') > 0;  
  
-- Open the cursor.  
OPEN indexes;  
  
-- Loop through the indexes.  
FETCH NEXT  
   FROM indexes  
   INTO @tablename, @objectid, @indexid, @frag;  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
   PRINT 'Executing DBCC INDEXDEFRAG (0, ' + RTRIM(@tablename) + ',  
      ' + RTRIM(@indexid) + ') - fragmentation currently '  
       + RTRIM(CONVERT(varchar(15),@frag)) + '%';  
   SELECT @execstr = 'DBCC INDEXDEFRAG (0, ' + RTRIM(@objectid) + ',  
       ' + RTRIM(@indexid) + ')';  
   EXEC (@execstr);  
  
   FETCH NEXT  
      FROM indexes  
      INTO @tablename, @objectid, @indexid, @frag;  
END;  
  
-- Close and deallocate the cursor.  
CLOSE indexes;  
DEALLOCATE indexes;  
  
-- Delete the temporary table.  
DROP TABLE #fraglist;  
GO  
```  
  
## <a name="see-also"></a>参照  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)
  
  

