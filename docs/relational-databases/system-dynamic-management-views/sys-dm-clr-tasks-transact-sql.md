---
title: sys.dm_clr_tasks (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_clr_tasks
- sys.dm_clr_tasks_TSQL
- dm_clr_tasks
- dm_clr_tasks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_tasks dynamic management view
ms.assetid: 462b9061-09fa-4858-9707-03d6cc19c769
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 00b37550b9a5d121d395f94d4810a4a093c3125d
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266001"
---
# <a name="sysdmclrtasks-transact-sql"></a>sys.dm_clr_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  現在実行されているランタイム (CLR) タスクのすべての一般的な言語の行を返します。 A [!INCLUDE[tsql](../../includes/tsql-md.md)] CLR ルーチンへの参照を含むバッチをそのバッチのすべてのマネージ コードを実行するための別のタスクを作成します。 バッチ内に、マネージド コードの実行を必要とするステートメントが複数ある場合は、それらのステートメントで同じ CLR タスクが使用されます。 CLR タスクがオブジェクトと関連するマネージ コードの実行だけでなく、インスタンスの間の遷移状態を維持する責任を負います[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と共通言語ランタイム。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**task_address**|**varbinary(8)**|CLR タスクのアドレス。|  
|**sos_task_address**|**varbinary(8)**|基になるアドレス[!INCLUDE[tsql](../../includes/tsql-md.md)]バッチ タスクです。|  
|**appdomain_address**|**varbinary(8)**|このタスクが実行されているアプリケーション ドメインのアドレス。|  
|**state**|**nvarchar(128)**|タスクの現在の状態。|  
|**abort_state**|**nvarchar(128)**|Abort が現在の状態 (タスクが取り消された) 場合がある複数の状態関連するタスクを中止します。|  
|**type**|**nvarchar(128)**|タスクの種類。|  
|**affinity_count**|**int**|タスクの関係。|  
|**forced_yield_count**|**int**|タスクが強制的に解放された回数。|  
  
## <a name="permissions"></a>アクセス許可  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [共通言語ランタイム関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  

