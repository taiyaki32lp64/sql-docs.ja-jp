---
title: sys.dm_db_column_store_row_group_operational_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31b71c68-50a0-4fd8-a7fe-2d2292be1163
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 03e97e38eb396aa24c9779d07f269a60f117ab09
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005046"
---
# <a name="sysdmdbcolumnstorerowgroupoperationalstats-transact-sql"></a>sys.dm_db_column_store_row_group_operational_stats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  返します。 現在行レベルの I/O、ロック、および列ストア インデックスに圧縮された行グループのアクティビティをメソッドにアクセスします。 使用**sys.dm_db_column_store_row_group_operational_stats**時間の長さを追跡するためにユーザー クエリする必要があります、圧縮された行グループまたは列ストア インデックスのパーティションに対する読み取りまたは書き込みを待機し、発生している行グループを識別重大な I/O 動作やホット スポット。  
  
 メモリ内列ストア インデックスは、この DMV には表示されません。  
 
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|列ストア インデックスを持つテーブルの ID です。|  
|**index_id**|**int**|列ストア インデックスの ID。|  
|**partition_number**|**int**|インデックスまたはヒープ内の、1 から始まるパーティション番号。|  
|**row_group_id**|**int**|列ストア インデックスに行グループの ID です。 これは、パーティション内で一意です。|  
|**scan_count**|**int**|SQL の最後の再起動以降の行グループでのスキャンの数。|  
|**delete_buffer_scan_count**|**int**|Delete バッファーは、この行グループの削除された行の決定に使用された回数。 これには、メモリ内ハッシュ テーブルおよび基になる btree へのアクセスが含まれます。|  
|**index_scan_count**|**int**|列ストア インデックスのパーティションがスキャンされた回数。 これは、パーティション内のすべての行グループと同じです。|  
|**rowgroup_lock_count**|**bigint**|SQL の最後の再起動以降、この行グループのロック要求の累積数。|  
|**rowgroup_lock_wait_count**|**bigint**|SQL の最後の再起動以降、この行グループのロックで、データベース エンジン待機を累積回数。|  
|**rowgroup_lock_wait_in_ms**|**bigint**|SQL の最後の再起動以降のこの行グループのロックで待機したデータベース エンジンに累積ミリ秒数をします。|  
  
## <a name="permissions"></a>アクセス許可  
 次の権限が必要です。  
  
-   Object_id で指定されたテーブルに対する CONTROL 権限。  
  
-   @ のオブジェクトのワイルドカードを使用して、データベース内のすべてのオブジェクトに関する情報を返す VIEW DATABASE STATE 権限*object_id* = NULL  
  
 VIEW DATABASE STATE 権限を許可すると、特定のオブジェクトに対して CONTROL 権限が拒否されていたとしても、データベース内のすべてのオブジェクトを取得することができます。  
  
 VIEW DATABASE STATE 権限を拒否すると、特定のオブジェクトに対する CONTROL 権限が許可されていたとしても、そのデータベース内のどのオブジェクトも取得できません。 ときに、データベースのワイルドカード @*database_id*= NULL を指定すると、データベースを省略するとします。  
  
 詳細については、次を参照してください。[動的管理ビューおよび関数&#40;TRANSACT-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)します。  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [インデックス関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_usage_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)   
 [sys.dm_db_partition_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  

