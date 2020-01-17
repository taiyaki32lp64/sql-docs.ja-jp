---
title: dm_exec_external_work (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_EXTERNAL_WORK
- DM_EXEC_EXTERNAL_WORK_TSQL
- SYS.DM_EXEC_EXTERNAL_WORK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_external_work management view
- dm_exec_external_work management view
- PolyBase,views
- PolyBase
ms.assetid: 7597d97b-1fde-4135-ac35-4af12968f300
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b0ba7eecc8e117e429f6992622d0c7bb2073f86a
ms.sourcegitcommit: 26868c8ac3217176b370d972a26d307598a10328
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74834335"
---
# <a name="sysdm_exec_external_work-transact-sql"></a>dm_exec_external_work (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  各コンピューティングノード上のワーカーごとのワークロードに関する情報を返します。  
  
 Dm_exec_external_work を照会して、外部データソース (Hadoop、外部 SQL Server など) と通信するためにスピンアップされる作業を識別します。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|`nvarchar(32)`|関連する PolyBase クエリの一意の識別子。|『 [Transact-sql&#41;&#40;dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)の*request_ID*を参照してください。|  
|step_index|`int`|このワーカーが実行している要求。|『 [Transact-sql&#41;&#40;dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)の*step_index*を参照してください。|  
|dms_step_index|`int`|このワーカーが実行している DMS プランのステップ。|「 [Sys. dm_exec_dms_workers &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)」を参照してください。|  
|compute_node_id|`int`|ワーカーが実行されているノード。|「 [Sys. dm_exec_compute_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)」を参照してください。|  
|型|`nvarchar(60)`|外部作業の種類。|' ファイル分割 '|  
|work_id|`int`|実際の分割の ID。|0以上。|  
|input_name|`nvarchar(4000)`|読み取る入力の名前|Hadoop を使用する場合のファイル名。|  
|read_location|`bigint`|オフセットまたは読み取り位置。|読み取るファイルのオフセット。|  
|bytes_processed|`bigint`|このワーカーによってデータを処理するために割り当てられた合計バイト数。 これは、必ずしもクエリによって返されるデータの合計を表しているとは限りません |0以上。|  
|length|`bigint`|Hadoop の場合は分割または HDFS ブロックの長さ|ユーザー定義可能。 既定値は64M です。|  
|status|`nvarchar(32)`|ワーカーの状態|保留中、処理中、完了、失敗、中止|  
|start_time|`datetime`|作業の開始||  
|end_time|`datetime`|作業の終了||  
|total_elapsed_time|`int`|合計時間 (ミリ秒)||
|compute_pool_id|`int`|プールの一意の識別子。|

## <a name="see-also"></a>参照  
 [動的管理ビューを使用した PolyBase のトラブルシューティング](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Transact-sql&#41;&#40;の動的管理ビューおよび関数](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;データベース関連の動的管理ビュー](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
