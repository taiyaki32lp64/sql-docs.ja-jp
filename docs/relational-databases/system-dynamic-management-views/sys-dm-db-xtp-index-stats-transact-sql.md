---
title: sys.dm_db_xtp_index_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_index_stats
- dm_db_xtp_index_stats
- sys.dm_db_xtp_index_stats_TSQL
- dm_db_xtp_index_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_index_stats dynamic management view
ms.assetid: 8d0a50b8-2015-4576-930f-e3307dfc888e
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6e6370f4cbfcbc38478e562c3b74ff24ffde962f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026832"
---
# <a name="sysdmdbxtpindexstats-transact-sql"></a>sys.dm_db_xtp_index_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  前回データベースが再起動されてから収集された統計が含まれます。  
  
 詳細については、次を参照してください。 [、インメモリ OLTP&#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)と[Guidelines for Using Indexes on Memory-Optimized Tables](https://msdn.microsoft.com/library/16ef63a4-367a-46ac-917d-9eebc81ab29b)します。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|object_id|**bigint**|インデックスが属しているオブジェクトの ID。|  
|xtp_object_id|**bigint**|オブジェクトの現在のバージョンに対応する内部の ID。<br /><br /> 注:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]に適用されます。|  
|index_id|**bigint**|インデックスの ID。 index_id は、オブジェクト内でのみ一意です。|  
|scans_started|**bigint**|実行されたインメモリ OLTP のインデックス スキャンの回数。 選択、挿入、更新、または削除を実行するたびに、インデックス スキャンが必要になります。|  
|scans_retries|**bigint**|再試行する必要のあるインデックス スキャンの回数。|  
|rows_returned|**bigint**|テーブルの作成後または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動後に返された行の累積数。|  
|rows_touched|**bigint**|テーブルの作成後または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動後にアクセスされた行の累積数。|  
|rows_expiring|**bigint**|内部使用のみです。|  
|rows_expired|**bigint**|内部使用のみです。|  
|rows_expired_removed|**bigint**|内部使用のみです。|  
|phantom_scans_started|**bigint**|内部使用のみです。|  
|phatom_scans_retries|**bigint**|内部使用のみです。|  
|phantom_rows_touched|**bigint**|内部使用のみです。|  
|phantom_expiring_rows_encountered|**bigint**|内部使用のみです。|  
|phantom_expired_rows_encountered|**bigint**|内部使用のみです。|  
|phantom_expired_removed_rows_encountered|**bigint**|内部使用のみです。|  
|phantom_expired_rows_removed|**bigint**|内部使用のみです。|  
|object_address|**varbinary(8)**|内部使用のみです。|  
  
## <a name="permissions"></a>アクセス許可  
 現在のデータベースに対する VIEW DATABASE STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルの動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
