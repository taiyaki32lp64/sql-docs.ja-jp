---
title: sys.dm_db_xtp_nonclustered_index_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_nonclustered_index_stats_TSQL
- dm_db_xtp_nonclustered_index_stats
- sys.dm_db_xtp_nonclustered_index_stats_TSQL
- sys.dm_db_xtp_nonclustered_index_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_nonclustered_index_stats
ms.assetid: d55ba31c-296c-419b-9c4b-c126e0a3d156
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 726fd7d44ed64dfee609ad29181a2077364d72e9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026789"
---
# <a name="sysdmdbxtpnonclusteredindexstats-transact-sql"></a>sys.dm_db_xtp_nonclustered_index_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  sys.dm_db_xtp_nonclustered_index_stats には、メモリ最適化テーブルの非クラスター化インデックスの操作に関する統計が含まれます。 sys.dm_db_xtp_nonclustered_index_stats の 1 行が、現在のデータベースのメモリ最適化テーブルに含まれる 1 つの非クラスター化インデックスに対応します。  
  
 sys.dm_db_xtp_nonclustered_index_stats に反映されている統計は、インメモリ インデックス構造の作成時に収集されます。 インメモリ インデックス構造は、データベースの再起動時に再作成されます。  
  
 sys.dm_db_xtp_nonclustered_index_stats を使用すると、DML 操作中およびデータベースがオンライン状態に移行した際のインデックス アクティビティを監視し、把握できます。 メモリ最適化テーブルを持つデータベースが再起動されると、メモリに 1 行ずつ挿入することによってインデックスが作成されます。 ページの分割、マージ、および統合のカウントは、データベースがオンライン状態に移行した際にインデックスを作成する作業が完了したかどうかを把握するために役立ちます。 また、一連の DML 操作の前後にこれらのカウントを確認することもできます。  
  
 再試行回数が多い場合は、コンカレンシーに問題がある可能性があります。[!INCLUDE[msCoName](../../includes/msconame-md.md)] サポートにお問い合わせください。  
  
 メモリ最適化非クラスター化インデックスの詳細については、次を参照してください。 [SQL Server インメモリ OLTP 内部概要](https://t.co/T6zToWc6y6)、17 ページです。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|object_id|**int**|オブジェクトの ID。|  
|xtp_object_id|**bigint**|メモリ最適化テーブルの ID です。|  
|index_id|**int**|インデックスの ID。|  
|delta_pages|**bigint**|ツリー内のこのインデックスに対するデルタ ページの合計数。|  
|internal_pages|**bigint**|内部使用です。 ツリー内のこのインデックスに対する内部ページの合計数。|  
|leaf_pages|**bigint**|ツリー内のこのインデックスに対するリーフ ページの合計数。|  
|outstanding_retired_nodes|**bigint**|内部使用です。 内部構造のこのインデックスに対するノードの合計数。|  
|page_update_count|**bigint**|インデックスのページを更新する操作の累積数。|  
|page_update_retry_count|**bigint**|インデックスのページを更新する操作の再試行の累積数。|  
|page_consolidation_count|**bigint**|インデックスのページ統合の累積数。|  
|page_consolidation_retry_count|**bigint**|ページ統合操作の再試行の累積数。|  
|page_split_count|**bigint**|インデックスのページ分割操作の累積数。|  
|page_split_retry_count|**bigint**|ページ分割操作の再試行の累積数。|  
|key_split_count|**bigint**|インデックスのキー分割の累積数。|  
|key_split_retry_count|**bigint**|キー分割操作の再試行の累積数。|  
|page_merge_count|**bigint**|インデックスのページ マージ操作の累積数。|  
|page_merge_retry_count|**bigint**|ページ マージ操作の再試行の累積数。|  
|key_merge_count|**bigint**|インデックスのキー マージ操作の累積数。|  
|key_merge_retry_count|**bigint**|キー マージ操作の再試行の累積数。|  
  
## <a name="permissions"></a>アクセス許可  
 現在のデータベースに対する VIEW DATABASE STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルの動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
