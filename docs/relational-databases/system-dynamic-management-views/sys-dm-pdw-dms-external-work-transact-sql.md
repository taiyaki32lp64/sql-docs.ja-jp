---
title: sys.dm_pdw_dms_external_work (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 47345015-f861-451e-97c4-6e1cb81d1922
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: a1778cbb88fcd6a4142e800cd45109602509125d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899498"
---
# <a name="sysdmpdwdmsexternalwork-transact-sql"></a>sys.dm_pdw_dms_external_work (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 外部の操作のすべてのデータ移動サービス (DMS) ステップに関する情報を保持するシステム ビュー。  
  
|列名|データ型|説明|範囲|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|この DMS ワーカーを使用するクエリ。<br /><br /> request_id、step_index、および dms_step_index は、このビューのキーを形成します。|Request_id 内と同じ[sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)します。|  
|step_index|**int**|この DMS ワーカーを呼び出しているクエリの手順です。<br /><br /> request_id、step_index、および dms_step_index は、このビューのキーを形成します。|Step_index と同じ[sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)します。|  
|dms_step_index|**int**|DMS プランの現在を手順します。<br /><br /> request_id、step_index、および dms_step_index は、このビューのキーを形成します。|Dms___step_index として同じ[sys.dm_pdw_dms_workers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)します。|  
|pdw_node_id|**int**|DMS ワーカーを実行しているノードです。|Node_id 内と同じ[sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)します。|  
|type|**nvarchar(60)**|このノードが実行されている外部の操作の種類。<br /><br /> ファイルの分割は、複数の小さいまでに分割されている外部の Hadoop ファイルの操作です。|' ファイルの分割 '|  
|work_id|**int**|ファイルの分割の id。|大きいまたは 0。<br /><br /> コンピューティング ノードごとに一意です。|  
|input_name|**nvarchar(60)**|読み取られている入力の名前の文字列を指定します。|Hadoop ファイルの場合は、Hadoop のファイル名です。|  
|read_location|**bigint**|読み取り位置をオフセットします。||  
|estimated_bytes_processed|**bigint**|このワーカーによって処理されたバイト数。|大きいまたは 0。|  
|長さ|**bigint**|分割、ファイル内のバイト数。<br /><br /> Hadoop は、これは、HDFS ブロックのサイズです。|ユーザー定義です。 既定では 64 MB です。|  
|status|**nvarchar(32)**|ワーカーの状態。|保留中、処理、完了、失敗した、中止されました|  
|start_time|**datetime**|ワーカーの実行が開始された時刻。|以上のクエリのステップの開始時刻値にこのワーカーが属しています。 参照してください[sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)します。|  
|end_time|**datetime**|時間に実行が終了した、失敗、またはが取り消されました。|継続的なまたはキューに置かれた作業者の場合は NULL です。 それ以外の場合、start_time より大きい。|  
|total_elapsed_time|**int**|ミリ秒単位での実行にかかった合計時間。|大きいまたは 0。<br /><br /> Total_elapsed_time では、整数の最大値を超えると、total_elapsed_time 引き続き、最大値になります。 この状態が"、最大値を超過しました"警告を生成します。<br /><br /> 最大値をミリ秒単位は 24.8 日に相当します。|  
  
 このビューで保持される最大行数は、詳細については、メタデータ」セクションを参照してください、[容量制限](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)トピック。
  
## <a name="see-also"></a>関連項目  
 [システム ビュー &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
