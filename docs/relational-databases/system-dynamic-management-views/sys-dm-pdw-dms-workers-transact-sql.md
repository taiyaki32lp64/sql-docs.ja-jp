---
title: sys.dm_pdw_dms_workers (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0a284d18-3c46-4ffa-bcc9-689e660ee8b4
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 6e5f295637db0e138caf324e3126707b9e0ea774
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899506"
---
# <a name="sysdmpdwdmsworkers-transact-sql"></a>sys.dm_pdw_dms_workers (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  DMS の手順を完了するすべての作業者に関する情報を保持します。  
  
|列名|データ型|説明|範囲|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|この DMS ワーカーの一部であるクエリ。<br /><br /> request_id、step_index、および dms_step_index は、このビューのキーを形成します。|Request_id 内を参照してください。 [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)します。|  
|step_index|**int**|この DMS ワーカーの一部であるステップをクエリします。<br /><br /> request_id、step_index、および dms_step_index は、このビューのキーを形成します。|Step_index を参照してください。 [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)します。|  
|dms_step_index|**int**|このワーカーが実行されている DMS プランのステップします。<br /><br /> request_id、step_index、および dms_step_index は、このビューのキーを形成します。||  
|pdw_node_id|**int**|ワーカーが実行されているノードです。|Node_id を参照してください。 [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)します。|  
|distribution_id|**Int**|存在する場合に、ワーカーで実行されている配布します。|Distribution_id を参照してください。 [sys.pdw_distributions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)します。|  
|type|**nvarchar(32)**|このエントリが表す DMS のワーカー スレッドの種類です。|'DIRECT_CONVERTER'、'DIRECT_READER'、'FILE_READER'、'HASH_CONVERTER'、'HASH_READER'、'ROUNDROBIN_CONVERTER'、'EXPORT_READER'、'EXTERNAL_READER'、'EXTERNAL_WRITER'、'PARALLEL_COPY_READER'、'REJECT_WRITER'、'ライター'|  
|status|**nvarchar(32)**|DMS ワーカーの状態です。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|bytes_per_sec|**bigint**|最後の 1 秒間の読み取りまたは書き込みのスループット。|大きいまたは 0。 クエリが取り消されたまたは、ワーカーが実行前に、失敗した場合は NULL します。|  
|bytes_processed|**bigint**|このワーカーによって処理された合計バイト数。|大きいまたは 0。 クエリが取り消されたまたは、ワーカーが実行前に、失敗した場合は NULL します。|  
|rows_processed|**bigint**|行の読み取りまたは書き込みのワーカーの数。|大きいまたは 0。 クエリが取り消されたまたは、ワーカーが実行前に、失敗した場合は NULL します。|  
|start_time|**datetime**|ワーカーの実行が開始された時刻。|以上のクエリのステップの開始時刻値にこのワーカーが属しています。 参照してください[sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)します。|  
|end_time|**datetime**|時間に実行が終了した、失敗、またはが取り消されました。|継続的なまたはキューに置かれた作業者の場合は NULL です。 それ以外の場合、start_time より大きい。|  
|total_elapsed_time|**int**|ミリ秒単位での実行にかかった合計時間。|大きいまたは 0。<br /><br /> システムを起動または再起動後の経過時間の合計です。 Total_elapsed_time では、整数値 (ミリ秒単位で 24.8 日) の最大値を超えるをオーバーフローしました期日の実体化エラーが発生します。<br /><br /> 最大値をミリ秒単位は 24.8 日に相当します。|  
|cpu_time|**bigint**|ミリ秒単位で、このワーカーによって消費される CPU 時間。|大きいまたは 0。|  
|query_time|**int**|SQL までの期間は、ミリ秒単位でのスレッドに行を返すを開始します。|大きいまたは 0。|  
|buffers_available|**int**|使用されていないバッファーの数。| クエリが取り消されたまたは、ワーカーが実行前に、失敗した場合は NULL します。|  
|sql_spid|**int**|この DMS ワーカーの処理を実行する SQL Server インスタンス上のセッション id。||  
|dms_cpid|**int**|実際に実行しているスレッドのプロセス ID。||  
|error_id|**nvarchar(36)**|存在する場合、このワーカーの実行中に発生したエラーの一意の識別子。|Error_id を参照してください。 [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)します。|  
|source_info|**nvarchar (4000)**|リーダー、ソース テーブルと列を指定します。||  
|destination_info|**nvarchar (4000)**|ライターの場合、変換先テーブルの仕様。||  
  
 このビューで保持される最大行数は、詳細については、メタデータ」セクションを参照してください、[容量制限](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)トピック.  
  
## <a name="see-also"></a>関連項目  
 [SQL Data Warehouse と Parallel Data Warehouse の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
