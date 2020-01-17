---
title: sys.dm_column_store_object_pool (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a8a58ca7-0a7d-4786-bfd9-e8894bd345dd
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 83369736ee18c36b3967bbbd129e0fd64574a2ed
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265988"
---
# <a name="sysdmcolumnstoreobjectpool-transact-sql"></a>sys.dm_column_store_object_pool (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 列ストア インデックスのオブジェクトのオブジェクトのメモリ プールの使用方法のさまざまな種類の取得をカウントします。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|`database_id`|`int`|データベースの ID です。 SQL Server データベースまたは Azure SQL データベース サーバーのインスタンス内で一意です。 |  
|`object_id`|`int`|オブジェクトの ID。 オブジェクトは、object_types のです。 | 
|`index_id`|`int`|列ストア インデックスの ID。|  
|`partition_number`|`bigint`|インデックスまたはヒープ内の、1 から始まるパーティション番号。 すべてのテーブルまたはビューは、少なくとも 1 つのパーティションを持ちます。| 
|`column_id`|`int`|列ストア列の ID。 これは、DELETE_BITMAP の場合は NULL です。| 
|`row_group_id`|`int`|行グループの ID。|
|`object_type`|`smallint`|1 = COLUMN_SEGMENT<br /><br /> 2 = COLUMN_SEGMENT_PRIMARY_DICTIONARY<br /><br /> 3 = COLUMN_SEGMENT_SECONDARY_DICTIONARY<br /><br /> 4 = COLUMN_SEGMENT_BULKINSERT_DICTIONARY<br /><br /> 5 = COLUMN_SEGMENT_DELETE_BITMAP|  
|`object_type_desc`|`nvarchar(60)`|COLUMN_SEGMENT - 列セグメント。 `object_id` セグメント ID です。 セグメントは、1 つの行グループ内の 1 つの列のすべての値を格納します。 たとえば、テーブルに 10 個の列がある場合は、行グループあたり 10 個の列セグメントです。 <br /><br /> COLUMN_SEGMENT_PRIMARY_DICTIONARY - テーブルの列セグメントのすべての参照情報を格納しているグローバル ディクショナリ。<br /><br /> COLUMN_SEGMENT_SECONDARY_DICTIONARY - 1 つの列に関連付けられているローカルのディクショナリ。<br /><br /> COLUMN_SEGMENT_BULKINSERT_DICTIONARY - グローバル辞書の別の表現。 これは、dictionary_id に値を逆の外観を提供します。 組ムーバーまたは一括読み込みの一部として圧縮されたセグメントを作成するために使用されます。<br /><br /> COLUMN_SEGMENT_DELETE_BITMAP - セグメントを追跡するビットマップを削除します。 パーティションあたり 1 つの削除のビットマップがあります。|  
|`access_count`|`int`|読み取りまたは、このオブジェクトへのアクセスの書き込みの数。|  
|`memory_used_in_bytes`|`bigint`|オブジェクト プール内のこのオブジェクトによって使用されるメモリ。|  
|`object_load_time`|`datetime`|Object_id が、オブジェクト プールになったは、クロック時間。|  
  
## <a name="permissions"></a>アクセス許可  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   
 
## <a name="see-also"></a>関連項目  
  
 [インデックス関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  
