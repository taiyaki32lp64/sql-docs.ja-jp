---
title: イベント通知に関する情報の取得 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], metadata
- status information [SQL Server], event notifications
- metadata [SQL Server], event notifications
ms.assetid: 8bc10867-66d6-4f57-ac32-a6c29f3327cd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9786faaf44724b1a2452bd5304b63deb2c9ea54e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63015314"
---
# <a name="get-information-about-event-notifications"></a>イベント通知に関する情報の取得
  次のカタログ ビューは、イベント通知に関するメタデータのクエリに使用できます。  
  
 **サーバー以外のレベルのイベント通知に関する情報を取得するには**  
  
-   [sys.event_notifications &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-event-notifications-transact-sql)  
  
> [!NOTE]  
>  任意のイベント通知に関するメタデータを表示する**sys.event_notifications**レベルには、少なくとも、データベースで作成された、次がある必要があります。制御、ALTER、TAKE OWNERSHIP、データベースに対する VIEW DEFINITION 権限またはイベント通知の所有者である、または ALTER ANY DATABASE EVENT NOTIFICATION 権限を持っています。 特定のキューの作成、イベント通知の最小値で以下が必要。制御、ALTER、TAKE OWNERSHIP、オブジェクトに対する VIEW DEFINITION 権限またはイベント通知の所有者である、または ALTER ANY DATABASE EVENT NOTIFICATION 権限を持っています。  
  
 **サーバーレベルのイベント通知に関する情報を取得するには**  
  
-   [sys.server_event_notifications &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql)  
  
> [!NOTE]  
>  少なくとも次が必要です。コントロールまたはサーバー上の任意の定義のアクセス許可の表示、ログオンまたはイベント通知の所有者であるまたは任意のイベント通知に関するメタデータを表示する ALTER ANY EVENT NOTIFICATION 権限を持っている**sys.server_event_notifications**.  
  
 **イベント通知を発生させることができるすべてのイベントに関する情報を取得するには**  
  
-   [sys.event_notification_event_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-event-notification-event-types-transact-sql)  
  
> [!NOTE]  
>  このカタログ ビューからイベント グループが返されることはありません。  
  
## <a name="see-also"></a>参照  
 [イベント通知](event-notifications.md)  
  
  
