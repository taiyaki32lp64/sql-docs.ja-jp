---
title: sys.dm_xe_session_events (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_xe_session_events
- sys.dm_xe_session_events_TSQL
- dm_xe_session_events
- dm_xe_session_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_session_events dynamic management view
- extended events [SQL Server], views
ms.assetid: 4f027b31-4e03-43a6-849d-1ba9d8d34ae8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4d8f796569eb8c4b524c0bc45b37ca8dc676ab45
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090244"
---
# <a name="sysdmxesessionevents-transact-sql"></a>sys.dm_xe_session_events (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  セッション イベントに関する情報を返します。 イベントは、個別の実行ポイントです。 述語は、イベントに必要な情報が含まれていない場合に実行を中止するイベントに適用できます。  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|イベント セッションのメモリ アドレス。 NULL 値は許可されません。|  
|event_name|**nvarchar (256)**|アクションにバインドされるイベントの名前。 NULL 値は許可されません。|  
|event_package_guid|**uniqueidentifier**|イベントを含むパッケージの GUID です。 NULL 値は許可されません。|  
|event_predicate|**nvarchar(3072)**|イベントに適用される述語ツリーの XML 表現。 NULL 値が許可されます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
### <a name="relationship-cardinalities"></a>リレーションシップの基数  
  
|From|変換先|リレーションシップ|  
|----------|--------|------------------|  
|sys.dm_xe_session_events.event_session_address|sys.dm_xe_sessions.address|多対一|  
|sys.dm_xe_session_events.event_package_guid、<br /><br /> sys.dm_xe_session_events.event_name|sys.dm_xe_objects.name、<br /><br /> sys.dm_xe_objects.package_guid|多対一|  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューおよび関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

