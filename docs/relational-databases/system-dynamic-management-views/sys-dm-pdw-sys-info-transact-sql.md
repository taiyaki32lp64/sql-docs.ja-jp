---
title: sys.dm_pdw_sys_info (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 686976b4-2d5d-4d64-bf12-56eba1dc59b1
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 0bc6c97f4d41023b822f42a6bbe4c5b193d42e45
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088751"
---
# <a name="sysdmpdwsysinfo-transact-sql"></a>sys.dm_pdw_sys_info (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  アプライアンスの全体的なアクティビティを反映するアプライアンス レベルのカウンターのセットを提供します。  
  
|列名|データ型|説明|範囲|  
|-----------------|---------------|-----------------|-----------|  
|total_sessions|**int**|システムの現在のセッションの数。|max_active_sessions (下記参照) に 0 を返します。|  
|idle_sessions|**int**|現在アイドル セッションの数。||  
|active_requests|**int**|現在実行中のアクティブな要求の数。||  
|queued_requests|**int**|現在キューに置かれた要求の数。||  
|active_loads|**int**|読み込みがシステムで現在実行中の数。||  
|queued_loads|**int**|実行を待機キューに登録された読み込みの数。||  
|active_backups|**int**|現在実行中のバックアップの数。||  
|active_restores|**int**|バックアップの数は、現在実行中を復元します。||  
  
## <a name="see-also"></a>関連項目  
 [SQL Data Warehouse と Parallel Data Warehouse の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
