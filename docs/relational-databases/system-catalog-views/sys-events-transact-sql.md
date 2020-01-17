---
title: sys.events (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.events_TSQL
- sys.events
- events_TSQL
- events
dev_langs:
- TSQL
helpviewer_keywords:
- sys.events catalog view
ms.assetid: f245a97a-80fc-43fb-a6e4-139420c9a47a
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 15fac5b2449e90fe7d6500bca383a71bc73954f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68025795"
---
# <a name="sysevents-transact-sql"></a>sys.events (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  トリガーまたはイベント通知が起動されるイベントごとに行が含まれています。 これらのイベントを使用して、トリガーまたはイベント通知が作成されるときに指定されているイベントの種類を表す[CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md)または[CREATE EVENT NOTIFICATION](../../t-sql/statements/create-event-notification-transact-sql.md)します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|トリガーまたはイベント通知の ID。 この値は、と共に**型**を一意に、行を識別します。|  
|**type**|**int**|トリガーを起動するイベントです。|  
|**type_desc**|**nvarchar(60)**|トリガーを起動するイベントの説明。|  
|**is_trigger_event**|**bit**|1 = トリガー イベント。<br /><br /> 0 = 通知イベント。|  
|**event_group_type**|**int**|トリガーまたはイベント通知が作成されるイベント グループ、またはイベント グループを作成していない場合は null です。|  
|**event_group_type**|**nvarchar(60)**|トリガーまたはイベント通知を作成する対象のイベント グループの説明です。イベント グループが作成対象でない場合は NULL になります。|  
  
## <a name="see-also"></a>関連項目  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
