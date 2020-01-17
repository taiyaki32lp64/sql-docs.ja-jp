---
title: sys.database_event_session_events (Azure SQL データベース) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: f4c9eb0a-173c-4c66-8dd8-6f7176b2657f
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 959c595f4ac394bbaf50c07b27a4679d9a30556e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915131"
---
# <a name="sysdatabase_event_session_events-azure-sql-database"></a>sys.database_event_session_events (Azure SQL Database)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  イベント セッションのイベントごとに 1 行のデータを返します。  
  
||  
|-|  
|**適用対象**:[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 およびそれ以降のバージョン。|  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|イベント セッションの ID。 NULL 値は許可されません。|  
|event_id|**int**|イベントの ID。 この ID は、イベント セッション オブジェクト内で一意です。 NULL 値は許可されません。|  
|NAME|**sysname**|イベントの名前です。 NULL 値は許可されません。|  
|package|**sysname**|イベントを含むイベント パッケージの名前。 NULL 値は許可されません。|  
|module|**sysname**|イベントを含むモジュールの名前。 NULL 値は許可されません。|  
|predicate|**nvarchar(3000)**|イベントに適用される述語式。 NULL 値が許可されます。|  
|predicate_xml|**nvarchar(3000)**|イベントに適用される XML 述語式。 NULL 値が許可されます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW DATABASE STATE 権限が必要です。  
  
## <a name="remarks"></a>コメント  
 このビューには、次のリレーションシップの基数があります。  
  
||||  
|-|-|-|  
|From|変換先|リレーションシップ|  
|sys.database_event_session_events.event_session_id|sys.database_event_sessions.event_session_id|多対一|  
  
## <a name="see-also"></a>関連項目  
 [拡張イベント](../../relational-databases/extended-events/extended-events.md)  
  
  
