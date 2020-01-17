---
title: メモリ最適化テーブルの動的管理ビュー (Transact-sql)
ms.custom: seo-dt-2019
ms.date: 02/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ccd82fed-1a3f-47de-85c4-1c9bdd80b027
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4981203eb0712eb1989959af38117d12f05bf9cb
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412828"
---
# <a name="memory-optimized-table-dynamic-management-views-transact-sql"></a>メモリ最適化テーブルの動的管理ビュー (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  インメモリ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLTP では、次の動的管理ビュー (dmv) が使用されます。  
  
 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
|||  
|-|-|   
|[dm_db_xtp_checkpoint_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-stats-transact-sql.md)|[dm_db_xtp_checkpoint_files &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md)|
|[dm_db_xtp_gc_cycle_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-gc-cycle-stats-transact-sql.md)|[dm_db_xtp_hash_index_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-hash-index-stats-transact-sql.md)| 
|[dm_db_xtp_index_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md)|[dm_db_xtp_memory_consumers &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-memory-consumers-transact-sql.md)|
|[dm_db_xtp_merge_requests (Transact-sql)](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-merge-requests-transact-sql.md)|[dm_db_xtp_object_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-object-stats-transact-sql.md)|
|[dm_db_xtp_nonclustered_index_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-nonclustered-index-stats-transact-sql.md)|[dm_db_xtp_table_memory_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql.md)|  
|[dm_db_xtp_transactions &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-transactions-transact-sql.md)|[dm_xtp_gc_queue_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-queue-stats-transact-sql.md)|  
|[dm_xtp_gc_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-stats-transact-sql.md)|[dm_xtp_system_memory_consumers &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-system-memory-consumers-transact-sql.md)|
|[dm_xtp_transaction_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-transaction-stats-transact-sql.md)||

### <a name="object-catalog-views"></a>オブジェクト カタログ ビュー

次のオブジェクトカタログビューは、インメモリ OLTP で特に使用されます。

|||  
|-|-|   
|[hash_indexes &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-hash-indexes-transact-sql.md)|[memory_optimized_tables_internal_attributes &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-memory-optimized-tables-internal-attributes-transact-sql.md)|  

### <a name="internal-dmvs"></a>内部 Dmv

内部使用のみを目的とした追加の Dmv が用意されており、直接のドキュメントは提供されません。 メモリ最適化テーブルの領域では、ドキュメントに記載されていない Dmv には次のようなものがあります。

- dm_xtp_threads
- dm_xtp_transaction_recent_rows

