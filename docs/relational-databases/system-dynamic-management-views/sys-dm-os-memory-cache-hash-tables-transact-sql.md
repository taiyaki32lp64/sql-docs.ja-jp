---
title: sys.dm_os_memory_cache_hash_tables (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_hash_tables_TSQL
- sys.dm_os_memory_cache_hash_tables
- dm_os_memory_cache_hash_tables
- dm_os_memory_cache_hash_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_hash_tables dynamic management view
ms.assetid: 68b94f35-8f80-4d2b-bcde-7a21934219af
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d5a52fc7c614752cde43a1670f2fb299b35aa0ee
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265775"
---
# <a name="sysdmosmemorycachehashtables-transact-sql"></a>sys.dm_os_memory_cache_hash_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  インスタンスでアクティブなキャッシュごとに 1 行を返す[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_os_memory_cache_hash_tables**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|キャッシュ エントリのアドレス (主キー)。 NULL 値は許可されません。|  
|**name**|**nvarchar (256)**|キャッシュの名前。 NULL 値は許可されません。|  
|**type**|**nvarchar(60)**|キャッシュの型。 NULL 値は許可されません。|  
|**table_level**|**int**|ハッシュ テーブル番号。 キャッシュは、異なるハッシュ関数に対応する複数のハッシュ テーブルがあります。 NULL 値は許可されません。|  
|**buckets_count**|**int**|ハッシュ テーブル内のバケットの数。 NULL 値は許可されません。|  
|**buckets_in_use_count**|**int**|現在使用されているバケット数。 NULL 値は許可されません。|  
|**buckets_min_length**|**int**|バケットの最小キャッシュ エントリ数。 NULL 値は許可されません。|  
|**buckets_max_length**|**int**|バケット内のキャッシュ エントリの最大数。 NULL 値は許可されません。|  
|**buckets_avg_length**|**int**|各バケットの平均キャッシュ エントリ数。 NULL 値は許可されません。|  
|**buckets_max_length_ever**|**int**|サーバーが起動された後のハッシュ テーブルのハッシュ バケット内のキャッシュされたエントリの最大数。 NULL 値は許可されません。|  
|**hits_count**|**bigint**|キャッシュ ヒットの数。 NULL 値は許可されません。|  
|**misses_count**|**bigint**|キャッシュ ミスの数。 NULL 値は許可されません。|  
|**buckets_avg_scan_hit_length**|**int**|検索したアイテムが見つかるまでにバケットで検証したエントリの平均数。 NULL 値は許可されません。|  
|**buckets_avg_scan_miss_length**|**int**|検索が正常に終了する前に、バケットで検証したエントリの平均数。 NULL 値は許可されません。|  
|**pdw_node_id**|**int**|この配布であるノードの識別子。<br /><br /> **適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>アクセス許可 

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   

## <a name="see-also"></a>関連項目  
 
  [SQL Server オペレーティング システム関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


