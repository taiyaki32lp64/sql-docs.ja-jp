---
title: sys.dm_xe_database_sessions (Azure SQL データベース) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 33ea5179-16bb-4abd-96cc-9bc696e80987
author: MightyPen
ms.author: genemi
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: ab0d59026bd172cb1e3fd51a92c3e5bb8b83b2e1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090371"
---
# <a name="sysdmxedatabasesessions-azure-sql-database"></a>sys.dm_xe_database_sessions (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  セッション イベントに関する情報を返します。 イベントは、個別の実行ポイントです。 述語は、イベントに必要な情報が含まれていない場合に実行を中止するイベントに適用できます。  
  
||  
|-|  
|**適用対象**:[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 およびそれ以降のバージョン。|  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|イベント セッションのメモリ アドレス。 NULL 値は許可されません。|  
|event_name|**nvarchar(60)**|アクションにバインドされるイベントの名前。 NULL 値は許可されません。|  
|event_package_guid|**uniqueidentifier**|イベントを含むパッケージの GUID です。 NULL 値は許可されません。|  
|event_predicate|**nvarchar(2048)**|イベントに適用される述語ツリーの XML 表現。 NULL 値が許可されます。|  
  
## <a name="permissions"></a>アクセス許可  
 VIEW DATABASE STATE 権限が必要です。  
  
### <a name="relationship-cardinalities"></a>リレーションシップの基数  
2015-07-13 の時点では 'sys.dm_xe_objects' は、名前には ' (' _d) が含まれていないこれらの Xevent Dmv のいずれか。 入力ミスまたはエラーでは、次の表の右側にある列ではありません。 名前は、Microsoft SQL Server と Azure SQL Database で同じです。  
  
|From|変換先|リレーションシップ|  
|--------|------|----------------|  
|sys.dm_xe_database_session_events.event_session_address|sys.dm_xe_database_sessions.address|多対一|  
|sys.dm_xe_database_session_events.event_package_guid, sys.dm_xe_database_session_events.event_name|sys.dm_xe_objects.name、sys.dm_xe_objects.package_guid|多対一|  
  
## <a name="see-also"></a>関連項目  
[Azure SQL Database での拡張イベント](https://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)  
[拡張イベント](../../relational-databases/extended-events/extended-events.md)  
  
 
