---
title: DROP EVENT NOTIFICATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP EVENT NOTIFICATION
- DROP_EVENT_NOTIFICATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- event notifications [SQL Server], removing
- deleting event notifications
- dropping event notifications
- DROP EVENT NOTIFICATION statement
- removing event notifications
ms.assetid: 0ffd8f47-4ea3-4238-9e73-c318df710cf7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: befa0085a7fc1a52ae02ba9443617b0593bb14ec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910057"
---
# <a name="drop-event-notification-transact-sql"></a>DROP EVENT NOTIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のデータベースからイベント通知トリガーを削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
DROP EVENT NOTIFICATION notification_name [ ,...n ]  
ON { SERVER | DATABASE | QUEUE queue_name }  
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *notification_name*  
 削除するイベント通知の名前です。 複数のイベント通知を指定できます。 現在作成されているイベント通知の一覧を表示するには、「[sys.event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)」を参照してください。  
  
 SERVER  
 イベント通知のスコープが現在のサーバーに適用されることを示します。 イベント通知の作成時に SERVER を指定した場合は、SERVER を指定する必要があります。  
  
 DATABASE  
 イベント通知のスコープが現在のデータベースに適用されることを示します。 イベント通知の作成時に DATABASE を指定した場合は、DATABASE を指定する必要があります。  
  
 QUEUE *queue_name*  
 イベント通知のスコープが、*queue_name* で指定されたキューに適用されることを示します。 イベント通知の作成時に QUEUE を指定した場合は、QUEUE を指定する必要があります。 同様に、キューの名前である *queue_name* も指定する必要があります。  
  
## <a name="remarks"></a>Remarks  
 トランザクション内でイベント通知が開始され、同じトランザクション内で削除される場合は、イベント通知インスタンスが送信されてから、このイベント通知が削除されます。  
  
## <a name="permissions"></a>アクセス許可  
 データベース レベルのスコープを持つイベント通知を削除するには、少なくとも、イベント通知の所有者であるか、現在のデータベースに対する ALTER ANY DATABASE EVENT NOTIFICATION 権限を持っている必要があります。  
  
 サーバー レベルのスコープを持つイベント通知を削除するには、少なくとも、イベント通知の所有者であるか、そのサーバーに対する ALTER ANY EVENT NOTIFICATION 権限を持っている必要があります。  
  
 特定のキューのイベント通知を削除するには、ユーザーは少なくともベント通知の所有者であるか、親キューに対する ALTER 権限を持っている必要があります。  
  
## <a name="examples"></a>使用例  
 次の例では、データベース スコープのイベント通知を作成してから削除します。  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE 'NotifyService',  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
GO  
DROP EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE;  
```  
  
## <a name="see-also"></a>参照  
 [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-notification-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)   
 [sys.events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)  
  
  
