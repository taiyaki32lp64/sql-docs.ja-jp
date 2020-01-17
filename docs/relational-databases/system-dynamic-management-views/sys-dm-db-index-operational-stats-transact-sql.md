---
title: sys.dm_db_index_operational_stats (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_index_operational_stats
- sys.dm_db_index_operational_stats_TSQL
- sys.dm_db_index_operational_stats
- dm_db_index_operational_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_index_operational_stats dynamic management function
ms.assetid: 13adf2e5-2150-40a6-b346-e74a33ce29c6
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b8222454d5e016733abef3c086e38add777cd304
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004897"
---
# <a name="sysdm_db_index_operational_stats-transact-sql"></a>sys.dm_db_index_operational_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  データベースの現在の低レベルの I/O、ロック、ラッチ、およびテーブルまたはインデックスのパーティションごとのアクセス メソッドのアクティビティを返します。    
    
 メモリ最適化インデックスは、この DMV には表示されません。    
    
> [!NOTE]    
>  **sys.dm_db_index_operational_stats**メモリ最適化インデックスに関する情報は返されません。 メモリ最適化インデックスの使用方法については、[sys.dm_db_xtp_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md)を参照してください。    
        
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>構文    
    
```    
    
sys.dm_db_index_operational_stats (    
    { database_id | NULL | 0 | DEFAULT }    
  , { object_id | NULL | 0 | DEFAULT }    
  , { index_id | 0 | NULL | -1 | DEFAULT }    
  , { partition_number | NULL | 0 | DEFAULT }    
)    
```    
    
## <a name="arguments"></a>引数    
 *database_id* | NULL | 0 | DEFAULT    
 データベースの ID です。 *database_id*は**smallint**します。 有効な入力値は、データベースの ID 番号、NULL、0、または DEFAULT です。 既定値は 0 です。 このコンテキストでは、NULL、0、および DEFAULT は同じ値になります。    
    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのすべてのデータベースに関する情報を返すには NULL を指定します。 NULL を指定する場合*database_id*の場合は NULL を指定することも必要があります。 *object_id*、 *index_id*、および*partition_number*します。    
    
 組み込み関数[DB_ID](../../t-sql/functions/db-id-transact-sql.md)を指定できます。    
    
 *object_id* | NULL | 0 | DEFAULT    
 インデックスがあるテーブルまたはビューのオブジェクト ID を指定します。 *object_ID* は **int**です。    
    
 有効な入力値は、テーブルおよびビューの ID 番号、NULL、0、または DEFAULT です。 既定値は 0 です。 このコンテキストでは、NULL、0、および DEFAULT は同じ値になります。    
    
 NULL を指定すると、指定されたデータベース内にあるすべてのテーブルとビューに関するキャッシュされた情報が返されます。 NULL を指定する場合*object_id*の場合は NULL を指定することも必要があります。 *index_id*と*partition_number*します。    
    
 *index_id* | 0 | NULL | -1 | DEFAULT    
 インデックスの ID。 *index_id*は**int**します。場合、有効な値は 0、インデックスの ID 番号*object_id*ヒープ、NULL、-1、または DEFAULT です。 既定値は -1 です。このコンテキストでは、NULL、-1、および DEFAULT は同じ値になります。    
    
 NULL を指定すると、ベース テーブルまたはビューのすべてのインデックスに関するキャッシュされた情報が返されます。 NULL を指定する場合*index_id*の場合は NULL を指定することも必要があります。 *partition_number*します。    
    
 *partition_number* | NULL | 0 | DEFAULT    
 オブジェクト内のパーティション番号を指定します。 *partition_number*は**int**します。有効な値は、 *partion_number*のインデックスまたはヒープ、NULL、0、または DEFAULT です。 既定値は 0 です。 このコンテキストでは、NULL、0、および DEFAULT は同じ値になります。    
    
 NULL を指定すると、インデックスまたはヒープのすべてのパーティションについてキャッシュされた情報が返されます。    
    
 *partition_number*は 1 から始まります。 非パーティション インデックスまたはヒープに*partition_number*を 1 に設定します。    
    
## <a name="table-returned"></a>返されるテーブル    
    
|列名|データ型|説明|    
|-----------------|---------------|-----------------|    
|**database_id**|**smallint**|データベース ID。|    
|**object_id**|**int**|テーブルまたはビューの ID。|    
|**index_id**|**int**|インデックスまたはヒープの ID。<br /><br /> 0 = ヒープ| 
|**partition_number**|**int**|インデックスまたはヒープ内の、1 から始まるパーティション番号。| 
|**hobt_id**|**bigint**|**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から [現在のバージョンまで](https://go.microsoft.com/fwlink/p/?LinkId=299658))、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br /> データ ヒープまたは列ストア インデックスの内部データを追跡する B ツリーの行セットの ID。<br /><br /> NULL の場合、これは、内部列ストア行セットではありません。<br /><br /> 詳細については、[sys.internal_partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md) を参照してください。|       
|**leaf_insert_count**|**bigint**|リーフレベルの挿入の累積数。|    
|**leaf_delete_count**|**bigint**|リーフレベルの削除の累積数。 leaf_delete_count はまずゴーストとしてマークされない削除されたレコードだけ増加します。 最初に、非実体化が削除されたレコードの**leaf_ghost_count**は代わりにインクリメントされます。|    
|**leaf_update_count**|**bigint**|リーフレベルの更新の累積数。|    
|**leaf_ghost_count**|**bigint**|削除とマークされており、まだ削除されていないリーフレベルの行の累積数。 この数には、ゴーストとしてマークしなくてもすぐに削除されたレコードは含まれません。 このような行は、設定された間隔でクリーンアップ スレッドにより削除されます。 この値には、未処理のスナップショット分離トランザクションが原因で保持されている行の数は含まれません。|    
|**nonleaf_insert_count**|**bigint**|リーフ レベルより上の挿入の累積数。<br /><br /> 0 = ヒープまたは列ストア|    
|**nonleaf_delete_count**|**bigint**|リーフ レベルより上の削除の累積数。<br /><br /> 0 = ヒープまたは列ストア|    
|**nonleaf_update_count**|**bigint**|リーフ レベルより上の更新の累積数。<br /><br /> 0 = ヒープまたは列ストア|    
|**leaf_allocation_count**|**bigint**|インデックスまたはヒープにおけるリーフ レベルのページ割り当ての累積数。<br /><br /> インデックスの場合、ページ割り当てとページ分割は対応しています。|    
|**nonleaf_allocation_count**|**bigint**|リーフ レベルより上のページ分割によって発生したページ割り当ての累積数。<br /><br /> 0 = ヒープまたは列ストア|    
|**leaf_page_merge_count**|**bigint**|リーフ レベルでページをマージした累積数。 列ストア インデックスは常に 0 です。|    
|**nonleaf_page_merge_count**|**bigint**|リーフ レベルより上でページをマージした累積数。<br /><br /> 0 = ヒープまたは列ストア|    
|**range_scan_count**|**bigint**|インデックスまたはヒープで開始された範囲スキャンとテーブル スキャンの累積数。|    
|**singleton_lookup_count**|**bigint**|インデックスまたはヒープから取得した単一行の累積数。|    
|**forwarded_fetch_count**|**bigint**|前方向レコードを介してフェッチされた行の数。<br /><br /> 0 = インデックス|    
|**lob_fetch_in_pages**|**bigint**|LOB_DATA アロケーション ユニットから取得したラージ オブジェクト (LOB) ページの累積数。 これらのページには、型の列に格納されているデータが含まれて**text**、 **ntext**、**image**、 **varchar (max)**、 **nvarchar (max)**、 **varbinary (max)**、および**xml**します。 詳細については、「[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)」を参照してください。|    
|**lob_fetch_in_bytes**|**bigint**|取得した LOB データの累積バイト数。|    
|**lob_orphan_create_count**|**bigint**|一括操作用に作成された、孤立した LOB 値の累積数。<br /><br /> 0 = 非クラスター化インデックス|    
|**lob_orphan_insert_count**|**bigint**|一括操作中に挿入された、孤立した LOB 値の累積数。<br /><br /> 0 = 非クラスター化インデックス|    
|**row_overflow_fetch_in_pages**|**bigint**|ROW_OVERFLOW_DATA アロケーション ユニットから取得した行オーバーフロー データ ページの累積数。<br /><br /> これらのページには、型の列に格納されているデータが含まれて**varchar (n)**、 **nvarchar (n)**、 **varbinary (n)**、および**sql_variant**されました。行外にプッシュします。|    
|**row_overflow_fetch_in_bytes**|**bigint**|取得した行オーバーフロー データの累積バイト数。|    
|**column_value_push_off_row_count**|**bigint**|挿入または更新された行をページ内に収めるため、行外に出された LOB データおよび行オーバーフロー データに対する列値の累積数。|    
|**column_value_pull_in_row_count**|**bigint**|行内に取り込まれた LOB データおよび行オーバーフロー データに対する列値の累積数。 これは、更新操作によりレコード内の領域が解放され、LOB_DATA または ROW_OVERFLOW_DATA アロケーション ユニットから IN_ROW_DATA アロケーション ユニットに 1 つ以上の行外値を取り込めるようになったときに発生します。|    
|**row_lock_count**|**bigint**|要求された行ロックの累積数。|    
|**row_lock_wait_count**|**bigint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]が行ロックで待機した累積回数。|    
|**row_lock_wait_in_ms**|**bigint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]が行ロックで待機した合計ミリ秒数。|    
|**page_lock_count**|**bigint**|要求されたページ ロックの累積数。|    
|**page_lock_wait_count**|**bigint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]がページ ロックで待機した累積回数。|    
|**page_lock_wait_in_ms**|**bigint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]がページ ロックで待機した合計ミリ秒数。|    
|**index_lock_promotion_attempt_count**|**bigint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]がロックのエスカレートを試行した累積回数。|    
|**index_lock_promotion_count**|**bigint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]がロックをエスカレートした累積回数。|    
|**page_latch_wait_count**|**bigint**|ラッチ競合のために、[!INCLUDE[ssDE](../../includes/ssde-md.md)]が待機した累積回数。|    
|**page_latch_wait_in_ms**|**bigint**|ラッチ競合のために、[!INCLUDE[ssDE](../../includes/ssde-md.md)]が待機した累積ミリ秒数。|    
|**page_io_latch_wait_count**|**bigint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]がページ I/O ラッチで待機した累積回数。|    
|**page_io_latch_wait_in_ms**|**bigint**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]がページ I/O ラッチで待機した累積ミリ秒数。|    
|**tree_page_latch_wait_count**|**bigint**|サブセット**page_latch_wait_count**を上位レベルの B ツリー ページのみが含まれています。 ヒープまたは列ストア インデックスでは、常に 0 です。|    
|**tree_page_latch_wait_in_ms**|**bigint**|サブセット**page_latch_wait_in_ms**を上位レベルの B ツリー ページのみが含まれています。 ヒープまたは列ストア インデックスでは、常に 0 です。|    
|**tree_page_io_latch_wait_count**|**bigint**|サブセット**page_io_latch_wait_count**を上位レベルの B ツリー ページのみが含まれています。 ヒープまたは列ストア インデックスでは、常に 0 です。|    
|**tree_page_io_latch_wait_in_ms**|**bigint**|サブセット**page_io_latch_wait_in_ms**を上位レベルの B ツリー ページのみが含まれています。 ヒープまたは列ストア インデックスでは、常に 0 です。|    
|**page_compression_attempt_count**|**bigint**|テーブル、インデックス、またはインデックス付きビューの特定のパーティションで、ページ レベルの圧縮が評価されたページの数。 大幅な節減を実現できないため圧縮されなかったページも含まれます。 列ストア インデックスは常に 0 です。|    
|**page_compression_success_count**|**bigint**|テーブル、インデックス、またはインデックス付きビューの特定のパーティションで、ページの圧縮を使用して圧縮されたデータ ページの数。 列ストア インデックスは常に 0 です。|    
    
## <a name="remarks"></a>コメント    
 この動的管理オブジェクトには、CROSS APPLY および OUTER APPLY からの相関パラメーターは受け入れられません。    
    
 使用することができます**sys.dm_db_index_operational_stats**または読み取り、テーブル、インデックス、またはパーティションを書き込み、およびテーブルまたはインデックスを重大な I/O 動作が発生しているまたはホット特定のユーザーが待つ必要がありますを時間の長さを追跡するには点。    
    
 競合について確認するには、次の列を使用します。    
    
 **テーブルまたはインデックス パーティションへの一般的なアクセス パターンを分析する**、これらの列を使用します。    
    
-   **leaf_insert_count**    
    
-   **leaf_delete_count**    
    
-   **leaf_update_count**    
    
-   **leaf_ghost_count**    
    
-   **range_scan_count**    
    
-   **singleton_lookup_count**    
    
 ラッチおよびロックの競合を特定する場合、次の列を使用します。    
    
-   **page_latch_wait_count**と**page_latch_wait_in_ms**    
    
     これらの列では、インデックスまたはヒープにラッチ競合があるかどうかが示されます。また競合の重大度も示されます。    
    
-   **場合は row_lock_count**と**page_lock_count**    
    
     これらの列では、[!INCLUDE[ssDE](../../includes/ssde-md.md)]で行とページ ロックの取得が何回試行されたかが示されます。    
    
-   **row_lock_wait_in_ms**と**page_lock_wait_in_ms**    
    
     これらの列では、インデックスまたはヒープにロック競合があるかどうかが示されます。また競合の重大度も示されます。    
    
 **インデックスまたはヒープ パーティションの物理 I/o の統計を分析するには**    
    
-   **page_io_latch_wait_count**と**page_io_latch_wait_in_ms**    
    
     これらの列では、インデックスまたはヒープ ページをメモリ内に移動するために、物理 I/O が発行されたかどうかが示されます。また I/O の発行回数も示されます。    
    
## <a name="column-remarks"></a>列の解説    
 内の値**lob_orphan_create_count**と**lob_orphan_insert_count**等しいは常にします。    
    
 列の値**lob_fetch_in_pages**と**lob_fetch_in_bytes**付加列として 1 つまたは複数の LOB 列を含む非クラスター化インデックスを 0 より大きくすることができます。 詳細については、「 [付加列インデックスの作成](../../relational-databases/indexes/create-indexes-with-included-columns.md)」を参照してください。 列の値では同様に、 **row_overflow_fetch_in_pages**と**row_overflow_fetch_in_bytes**インデックスにプッシュできるように列が含まれている場合に非クラスター化インデックスの場合は 0 より大きくすること行外です。    
    
## <a name="how-the-counters-in-the-metadata-cache-are-reset"></a>メタデータ キャッシュ内のカウンターのリセット方法    
 によって返されるデータ**sys.dm_db_index_operational_stats**ヒープまたはインデックスを表すメタデータ キャッシュ オブジェクトが使用可能な限りのみ存在します。 このデータは持続性はなく、トランザクション上の一貫性もありません。 つまり、これらのカウンターを使って、インデックスが使用されているかどうかや、インデックスが最後に使用されたのはいつであるかを判断することはできません。 これについては、次を参照してください。 [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)します。    
    
 ヒープまたはインデックスに対するメタデータがメタデータ キャッシュに組み込まれるたび、各列の値はゼロに設定されます。統計値は、キャッシュ オブジェクトがメタデータ キャッシュから削除されるまで累積されます。 したがって、キャッシュにはアクティブなヒープまたはインデックスのメタデータが常に存在し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが最後に開始してからの動作が累積数として反映されます。 アクティブになる頻度が低いヒープやインデックスのメタデータは、使用状況に応じてキャッシュ内外に移動されます。 その結果、使用できる値が存在する場合と、存在しない場合が発生します。 インデックスを削除すると、対応する統計はメモリから削除され、この関数ではレポートされなくなります。 インデックスに対するその他の DDL 操作によって、統計の値がゼロにリセットされる場合もあります。    
    
## <a name="using-system-functions-to-specify-parameter-values"></a>システム関数によるパラメーター値の指定    
 使用することができます、[!INCLUDE[tsql](../../includes/tsql-md.md)]関数[DB_ID](../../t-sql/functions/db-id-transact-sql.md)と[OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md)の値を指定する、 *database_id*と*object_id*パラメーター。 ただし、これらの関数に無効な値を渡すと、意図しない結果が生じる可能性があります。 DB_ID または OBJECT_ID を使用する場合は、必ず有効な ID が返されるようにしてください。 詳細については、「解説」セクションを参照してください。 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)します。    
    
## <a name="permissions"></a>アクセス許可    
 次の権限が必要です。    
    
-   データベース内の指定したオブジェクトに対する CONTROL 権限。    
    
-   @ のオブジェクトのワイルドカードを使用して指定したデータベース内のすべてのオブジェクトに関する情報を返す VIEW DATABASE STATE 権限*object_id* = NULL    
    
-   データベースのワイルドカード @ を使用して、すべてのデータベースに関する情報を返す VIEW SERVER STATE 権限*database_id* = NULL    
    
 VIEW DATABASE STATE 権限を許可すると、特定のオブジェクトに対して CONTROL 権限が拒否されていたとしても、データベース内のすべてのオブジェクトを取得することができます。    
    
 VIEW DATABASE STATE 権限を拒否すると、特定のオブジェクトに対する CONTROL 権限が許可されていたとしても、そのデータベース内のどのオブジェクトも取得できません。 ときに、データベースのワイルドカード @*database_id*= NULL を指定すると、データベースを省略するとします。    
    
 詳細については、次を参照してください。[動的管理ビューおよび関数&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)します。    
    
## <a name="examples"></a>使用例    
    
### <a name="a-returning-information-for-a-specified-table"></a>A. 指定したテーブルについての情報を返す    
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベース内にある `Person.Address` テーブルのすべてのインデックスとパーティションについて、情報を返します。 このクエリを実行して、少なくとも、CONTROL 権限が必要で`Person.Address`テーブル。    
    
> [!IMPORTANT]    
>  [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数 DB_ID および OBJECT_ID を使ってパラメーター値を返すときには、有効な ID が返されることを常に確認してください。 データベースまたはオブジェクト名が存在しないか、スペルが間違っていることが原因で見つからない場合は、両方の関数で NULL が返されます。 **sys.dm_db_index_operational_stats** 関数では、NULL 値はすべてのデータベースまたはすべてのオブジェクトを指定するワイルドカード値として解釈されます。 これによって意図しない操作が実行される可能性があるので、この例では安全な方法を使用してデータベース ID とオブジェクト ID を特定します。    
    
```    
DECLARE @db_id int;    
DECLARE @object_id int;    
SET @db_id = DB_ID(N'AdventureWorks2012');    
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');    
IF @db_id IS NULL     
  BEGIN;    
    PRINT N'Invalid database';    
  END;    
ELSE IF @object_id IS NULL    
  BEGIN;    
    PRINT N'Invalid object';    
  END;    
ELSE    
  BEGIN;    
    SELECT * FROM sys.dm_db_index_operational_stats(@db_id, @object_id, NULL, NULL);    
  END;    
GO    
    
```    
    
### <a name="b-returning-information-for-all-tables-and-indexes"></a>B. すべてのテーブルとインデックスの情報を返す    
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内のすべてのテーブルとインデックスについて情報を返します。 このクエリを実行するには、VIEW SERVER STATE 権限が必要です。    
    
```    
SELECT * FROM sys.dm_db_index_operational_stats( NULL, NULL, NULL, NULL);    
GO    
    
```    
    
## <a name="see-also"></a>参照    
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)     
 [インデックス関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)     
 [パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)     
 [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)     
 [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)     
 [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)     
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)     
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)    
    
  

