---
title: sys _db_page_info (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_db_page_info
- sys.dm_db_page_info_TSQL
- dm_db_page_info
- dm_db_page_info_TSQL
- dbcc page
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_page_info dynamic management view
author: bluefooted
ms.author: pamela
manager: amitban
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0802f3013af11814586634f890bb8ddddeadeec6
ms.sourcegitcommit: 9702dd51410dd610842d3576b24c0ff78cdf65dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68841597"
---
# <a name="sysdm_db_page_info-transact-sql"></a>sys _db_page_info (Transact-sql)

[!INCLUDE[tsql-appliesto-ssver15-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

データベース内のページに関する情報を返します。  関数は、 `object_id`、 `index_id`、 `partition_id`など、ページのヘッダー情報を含む1行を返します。  この関数を使用すると、ほとんどの場合に `DBCC PAGE` を使用する必要がなくなります。

> [!NOTE]
> `sys.dm_db_page_info`は、現在以降で[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]のみサポートされています。


## <a name="syntax"></a>構文   
```  
sys.dm_db_page_info ( DatabaseId, FileId, PageId, Mode )  
``` 

## <a name="arguments"></a>引数  
*DatabaseId* |NULL |標準     
データベースの ID を示します。 *DatabaseId*は**smallint**です。 有効な入力値は、データベースの ID 番号です。 既定値は NULL です。ただし、このパラメーターに NULL 値を指定すると、エラーが発生します。
 
*FileId* |NULL |標準   
ファイルの ID を指定します。 *FileId*は**int**です。有効な入力は、 *DatabaseId*によって指定されたデータベース内のファイルの ID 番号です。 既定値は NULL です。ただし、このパラメーターに NULL 値を指定すると、エラーが発生します。

*ページ id* |NULL |標準   
ページの ID を示します。  *ページ id*は**int**です。有効な入力値は、 *FileId*によって指定されたファイル内のページの ID 番号です。 既定値は NULL です。ただし、このパラメーターに NULL 値を指定すると、エラーが発生します。

*Mode* |NULL |標準   
関数の出力の詳細レベルを決定します。 ' 制限付き ' は、すべての説明列に対して NULL 値を返します。 ' DETAILED ' は説明列を設定します。  既定値は "制限されています" です。

## <a name="table-returned"></a>返されるテーブル  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|database_id |ssNoversion |データベース ID |
|file_id |ssNoversion |ファイル ID |
|page_id |ssNoversion |ページ ID |
|page_header_version |ssNoversion |ページヘッダーのバージョン |
|page_type |ssNoversion |ページの種類 |
|page_type_desc |nvarchar (64) |ページの種類の説明 |
|page_type_flag_bits |nvarchar (64) |ページヘッダーにフラグビットを入力 |
|page_type_flag_bits_desc |nvarchar (64) |ページヘッダーの型フラグのビットの説明 |
|page_flag_bits |nvarchar (64) |ページヘッダーのフラグビット |
|page_flag_bits_desc |nvarchar (256) |ページヘッダーのビットの説明にフラグを付ける |
|page_lsn |nvarchar (64) |ログシーケンス番号/タイムスタンプ |
|page_level |ssNoversion |インデックス内のページのレベル (リーフ = 0) |
|object_id |ssNoversion |ページを所有しているオブジェクトの ID |
|index_id |ssNoversion |インデックスの ID (ヒープデータページの場合は 0) |
|partition_id |BIGINT |パーティションの ID |
|alloc_unit_id |BIGINT |アロケーションユニットの ID |
|is_encrypted |bit |ページが暗号化されているかどうかを示すビット |
|has_checksum |bit |ページにチェックサム値があるかどうかを示すビット |
|チェックサム (checksum) |ssNoversion |データの破損を検出するために使用されるチェックサム値を格納します。 |
|is_iam_pg |bit |ページが IAM ページであるかどうかを示すビット  |
|is_mixed_ext |bit |混合エクステントで割り当てられているかどうかを示すビット |
|has_ghost_records |bit |ページにゴーストレコードが含まれているかどうかを示すビット <br> ゴーストレコードとは、削除対象としてマークされているものの、まだ削除されていないレコードのことです。|
|has_version_records |bit |ページに[データベースの高速復旧](../backup-restore/restore-and-recovery-overview-sql-server.md#adr)に使用されるバージョンレコードが含まれているかどうかを示すビット |
|pfs_page_id |ssNoversion |対応する PFS ページのページ ID |
|pfs_is_allocated |bit |対応する PFS ページでページが割り当て済みとしてマークされているかどうかを示すビット |
|pfs_alloc_percent |ssNoversion |対応する PFS バイトによって示される割り当て比率 |
|pfs_status |nvarchar (64) |PFS バイト |
|pfs_status_desc |nvarchar (64) |PFS バイトの説明 |
|gam_page_id |ssNoversion |対応する GAM ページのページ ID |
|gam_status |bit |GAM で割り当てられているかどうかを示すビット |
|gam_status_desc |nvarchar (64) |GAM ステータスビットの説明 |
|sgam_page_id |ssNoversion |対応する SGAM ページのページ ID |
|sgam_status |bit |SGAM で割り当てられているかどうかを示すビット |
|sgam_status_desc |nvarchar (64) |SGAM ステータスビットの説明 |
|diff_map_page_id |ssNoversion |対応する差分ビットマップページのページ ID |
|diff_status |bit |Diff の状態が変更されたかどうかを示すビット |
|diff_status_desc |nvarchar (64) |Diff ステータスビットの説明 |
|ml_map_page_id |ssNoversion |対応する最小ログ記録ビットマップページのページ ID |
|ml_status |bit |ページが最小ログ記録されるかどうかを示すビット |
|ml_status_desc |nvarchar (64) |最小ログ記録ステータスビットの説明 |
|prev_page_file_id |SMALLINT |前のページファイル ID |
|prev_page_page_id |ssNoversion |前のページページ ID |
|next_page_file_id |SMALLINT |次のページファイル ID |
|next_page_page_id |ssNoversion |次のページページ ID |
|fixed_length |SMALLINT |固定サイズの行の長さ |
|slot_count |SMALLINT |スロットの合計数 (使用済みおよび未使用) <br> データページの場合、この数値は行の数と同じです。 |
|ghost_rec_count |SMALLINT |ページでゴーストとしてマークされたレコードの数 <br> ゴーストレコードとは、削除対象としてマークされているものの、まだ削除されていないレコードのことです。 |
|free_bytes |SMALLINT |ページの空きバイト数 |
|free_data_offset |ssNoversion |データ領域の端にある空き領域のオフセット |
|reserved_bytes |SMALLINT |すべてのトランザクションで予約されている空きバイト数 (ヒープの場合) <br> ゴースト行の数 (インデックスのリーフの場合) |
|reserved_bytes_by_xdes_id |SMALLINT |M_xdesID によって m_reservedCnt に貢献する領域 <br> デバッグ目的のみ |
|xdes_id |nvarchar (64) |M_reserved によって提供される最新のトランザクション <br> デバッグ目的のみ |
||||

## <a name="remarks"></a>コメント
動的`sys.dm_db_page_info`管理関数は`page_id`、ページヘッダーに存在`file_id`する`index_id`、 `object_id` 、、などのページ情報を返します。 この情報は、さまざまなパフォーマンス (ロックとラッチの競合) と破損の問題に関するトラブルシューティングとデバッグに役立ちます。

`sys.dm_db_page_info`多くの場合、 `DBCC PAGE`ステートメントの代わりに使用できますが、ページの本文ではなくページヘッダー情報のみが返されます。 `DBCC PAGE`は、ページのコンテンツ全体が必要な場合にも必要になります。

## <a name="using-in-conjunction-with-other-dmvs"></a>を他の Dmv と組み合わせて使用する
の`sys.dm_db_page_info`重要なユースケースの1つは、ページ情報を公開する他の dmv と結合することです。  このユースケースを容易にするために、 `page_resource`という新しい列が追加されました。これにより、ページ情報が8バイトの16進形式で公開されます。 この列は、および`sys.dm_exec_requests` `sys.sysprocesses`に追加されており、必要に応じて今後他の dmv に追加されます。

新しい`sys.fn_PageResCracker`関数は、を入力`page_resource`として受け取り、、、 `file_id`および`page_id`を含む`database_id`1 行を出力します。  この関数は、または`sys.dm_exec_requests` `sys.sysprocesses`と`sys.dm_db_page_info`の間の結合を容易にするために使用できます。

## <a name="permissions"></a>アクセス許可  
データベースの`VIEW DATABASE STATE`権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-displaying-all-the-properties-of-a-page"></a>A. ページのすべてのプロパティを表示する
次のクエリでは、指定したのすべてのページ情報`database_id`を`file_id`含む`page_id` 1 行が返されます。既定のモード (' 制限付き ') と組み合わせて使用します。

```sql
SELECT *  
FROM sys.dm_db_page_info (5, 1, 15, DEFAULT)
```

### <a name="b-using-sysdm_db_page_info-with-other-dmvs"></a>B. 他の Dmv での _db_page_info の使用 

次のクエリは、行に`wait_resource` null 以外`sys.dm_exec_requests`のが含まれている場合に、によって公開される1行を返します。`page_resource`

```sql
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 'LIMITED') AS page_info
```

## <a name="see-also"></a>関連項目  
[動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[データベース関連の動的管理&#40;ビュー transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)     
[sys.fn_PageResCracker](../../relational-databases/system-functions/sys-fn-pagerescracker-transact-sql.md)


