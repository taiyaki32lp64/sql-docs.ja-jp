---
title: dm_xe_database_session_targets
titleSuffix: Azure SQL Database
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 7f353e2a-f8fc-4366-97e4-aa1c49eadaf4
author: MightyPen
ms.author: genemi
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: 860faaa6c9e574feda8d5c28be17a265707fd72e
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844434"
---
# <a name="sysdm_xe_database_session_targets-azure-sql-database"></a>sys.dm_xe_database_session_targets (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  セッション ターゲットに関する情報を返します。  
  
||  
|-|  
|**適用対象**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 および将来のバージョン。|  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary (8)**|イベントセッションのメモリアドレス。 には、dm_xe_database_sessions との多対一のリレーションシップがあります。 NULL 値は許可されません。|  
|target_name|**nvarchar(60)**|セッション内のターゲットの名前。 NULL 値は許可されません。|  
|target_package_guid|**uniqueidentifier**|ターゲットを含むパッケージの GUID。 NULL 値は許可されません。|  
|execution_count|**bigint**|セッションに対してターゲットが実行された回数。 NULL 値は許可されません。|  
|execution_duration_ms|**bigint**|ターゲットが実行された時間の合計 (ミリ秒単位)。 NULL 値は許可されません。|  
|target_data|**nvarchar(max)**|イベント集計情報など、ターゲットが保持するデータ。 NULL 値が許可されます。|  
  
## <a name="permissions"></a>アクセス許可  
 VIEW DATABASE STATE 権限が必要です。  
  
### <a name="relationship-cardinalities"></a>リレーションシップ基数  
  
|From|変換先|[リレーションシップ]|  
|----------|--------|------------------|  
|dm_xe_database_session_targets。 event_session_address|dm_xe_database_sessions. アドレス|多対一|  
  
  
