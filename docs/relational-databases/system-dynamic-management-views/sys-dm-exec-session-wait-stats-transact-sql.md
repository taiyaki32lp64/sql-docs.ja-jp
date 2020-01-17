---
title: dm_exec_session_wait_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_session_wait_stats
- sys.dm_exec_session_wait_stats_tsql
- dm_exec_session_wait_stats
- dm_exec_session_wait_stats_tsql
helpviewer_keywords:
- sys.dm_exec_session_wait_stats
ms.assetid: df84842a-71eb-4fda-b448-5953cf9985dc
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6fc51bec78cf01522e6731648bdb7870ea7d9fb0
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982606"
---
# <a name="sysdm_exec_session_wait_stats-transact-sql"></a>sys.dm_exec_session_wait_stats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  セッションごとに実行されたスレッドにより検出されたすべての待機に関する情報を返します。 このビューを使用すると、SQL Serverセッション[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパフォーマンスの問題や特定のクエリやバッチを診断することができます。  このビューは [sys.dm_os_wait_stats &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) に集計されたものと同じ情報を返しますが、 **session_id** 番号もあわせて提供します。  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降)。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|セッションの id です。|  
|wait_type|**nvarchar(60)**|待機の種類の名前。 詳細については、「[sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)」を参照してください。|  
|waiting_tasks_count|**bigint**|この待機の種類における待機の数。 このカウンターは、待機が開始するたび増加します。|  
|wait_time_ms|**bigint**|この待機の種類の合計待機時間 (ミリ秒単位)。 この時間には signal_wait_time_ms が含まれます。|  
|max_wait_time_ms|**bigint**|この待機の種類における最大待機時間。|  
|signal_wait_time_ms|**bigint**|待機スレッドがシグナルを受け取ってから実行を開始するまでの時間。|  
  
## <a name="remarks"></a>Remarks  
 この DMV は、セッションが開かれると、または、セッションがリセットされたときにセッションの情報をリセット (場合接続プール)、  
  
 待機の種類の詳細については、「 [sys. &#40;dm_os_wait_stats&#41;transact-sql](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーがサーバーに対する**VIEW SERVER STATE**権限を持っている場合、ユーザーには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスで実行中のすべてのセッションが表示されます。それ以外の場合、ユーザーには現在のセッションのみが表示されます。  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [オペレーティングシステム関連の動的管理ビュー &#40;の SQL Server transact-sql&#41; ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)  
 
