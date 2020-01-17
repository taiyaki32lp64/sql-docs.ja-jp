---
title: sys.dm_pdw_errors (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 944eac31-5691-432b-b9f5-f1e11c05191f
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 06f905b4750801080c6b645601261bfe96f1ee0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899437"
---
# <a name="sysdmpdwerrors-transact-sql"></a>sys.dm_pdw_errors (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  要求またはクエリの実行中に発生したすべてのエラーに関する情報を保持します。  
  
|列名|データ型|説明|範囲|  
|-----------------|---------------|-----------------|-----------|  
|error_id|**nvarchar(36)**|このビューのキー。<br /><br /> エラーに関連付けられている一意の数値 id です。|システム内のすべてのクエリ エラーの間で一意です。|  
|source|**nvarchar(64)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|type|**nvarchar (4000)**|発生したエラーの種類です。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|create_time|**datetime**|エラーが発生した時刻。|小さいまたは現在の時刻に等しい。|  
|pwd_node_id|**int**|特定のノードが存在する場合は、関連の識別子。 ノード id の詳細については、次を参照してください。 [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)します。||  
|session_id|**nvarchar(32)**|存在する場合は、関連のセッションの識別子。 セッション id の詳細については、次を参照してください。 [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)します。||  
|request_id|**nvarchar(32)**|存在する場合は、関連の要求の識別子。 要求 id の詳細については、次を参照してください。 [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)します。||  
|spid|**int**|存在する場合は、関連の SQL Server セッションの spid。||  
|thread_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|詳細情報|**nvarchar (4000)**|完全なエラーの説明テキストを保持します。||  
  
 このビューで保持される最大行数は、詳細については、メタデータ」セクションを参照してください、[容量制限](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)トピック。  
  
## <a name="see-also"></a>参照  
 [SQL Data Warehouse と Parallel Data Warehouse の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
