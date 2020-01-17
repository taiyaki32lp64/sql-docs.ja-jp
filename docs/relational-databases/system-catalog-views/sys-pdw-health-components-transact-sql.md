---
title: sys.pdw_health_components (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: d5c7589b-09b0-4f12-ab84-feb3ec3fbaaa
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5205c1ac6248f5aadee01410b4ba5e8f00332a73
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127485"
---
# <a name="syspdwhealthcomponents-transact-sql"></a>sys.pdw_health_components (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  すべてのコンポーネントと、システム内に存在するデバイスに関する情報を格納します。 これらには、ハードウェア、ストレージ デバイス、およびネットワーク デバイスが含まれます。  
  
|列名|データ型|説明|範囲|  
|-----------------|---------------|-----------------|-----------|  
|component_id|**int**|コンポーネントまたはデバイスの一意の識別子。<br /><br /> このビューのキー。|NOT NULL|  
|group_id|**Int**|このコンポーネントが所属するコンポーネントの論理グループです。 参照してください[sys.pdw_health_components (並列データ ウェアハウス)](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)します。|NOT NULL|  
|component_name|**nvarchar (255)**|コンポーネント名。|NOT NULL|  
  
## <a name="see-also"></a>参照  
 [SQL Data Warehouse と Parallel Data Warehouse カタログ ビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
