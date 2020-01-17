---
title: sys.dm_exec_external_operations (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_EXTERNAL_OPERATIONS_TSQL
- DM_EXEC_EXTERNAL_OPERATIONS
- SYS.DM_EXEC_EXTERNAL_OPERATIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- sys.dm_exec_external_operations management view
- dm_exec_external_operations management view
ms.assetid: d268217a-85b8-4b7f-9cd1-87865eba2be1
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d410afc256f0a1c12694f826bc73570cfee84172
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097765"
---
# <a name="sysdmexecexternaloperations-transact-sql"></a>sys.dm_exec_external_operations (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  外部の PolyBase 操作に関する情報をキャプチャします。  
  
|列名|データ型|説明|範囲|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|PolyBase クエリに関連付けられているクエリの一意の識別子|内の ID を参照してください[sys.dm_exec_requests &#40;TRANSACT-SQL。&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|  
|step_index|**int**|クエリ ステップのインデックス|Step_index を参照してください[sys.dm_exec_distributed_request_steps &#40;TRANSACT-SQL。&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)|  
|処理の種類|**nvarchar(128)**|Hadoop 操作またはその他の外部の操作について説明します|' 外部 Hadoop Operation'|  
|処理の名前|**nvarchar (4000)**|示す方法 (量は、入力を使用) の割合で、ジョブの状態|0-1 - 率 100 (完了) を掛けた値|  
|map _ の進行状況|**float**|存在する場合、パーセンテージで示した、reduce の状態のジョブを示します|0-1 - 率 100 (完了) を掛けた値|  
  
## <a name="see-also"></a>関連項目  
 [PolyBase 動的管理ビューでのトラブルシューティング](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [データベース関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
