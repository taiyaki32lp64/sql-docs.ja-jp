---
title: sys.dm_pdw_os_event_logs (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 819b38bce871bd1a43b3d259d23b2c95fb6dfdd3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086210"
---
# <a name="sysdmpdwoseventlogs-transact-sql"></a>sys.dm_pdw_os_event_logs (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  別の Windows イベントに関する情報がさまざまなノードでログを保持します。  
  
|列名|データ型|説明|範囲|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|アプライアンスのノードがこのログはからです。<br /><br /> pdw_node_id と log_name は、このビューのキーを形成します。||  
|log_name|**nvarchar (255)**|Windows イベント ログの名前です。<br /><br /> pdw_node_id と log_name は、このビューのキーを形成します。||  
|log_source|**nvarchar (255)**|Windows イベント ログ ソースの名前です。||  
|event_id|**int**|イベントの ID。 一意ではありません。||  
|event_type|**nvarchar (255)**|重大度を識別する、イベントの種類。|' 情報 '、'警告'、'Error'|  
|event_message|**nvarchar (4000)**|イベントの詳細。||  
|generate_time|**datetime**|イベントが作成された時刻。||  
|write_time|**datetime**|イベントがログに書き込まれた実際には時間です。||  
  
 このビューで保持される最大行数は、詳細については、メタデータ」セクションを参照してください、[容量制限](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)トピック。 
  
## <a name="see-also"></a>参照  
 [SQL Data Warehouse と Parallel Data Warehouse の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
