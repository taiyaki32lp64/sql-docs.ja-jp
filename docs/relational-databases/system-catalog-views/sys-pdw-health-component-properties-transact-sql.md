---
title: sys.pdw_health_component_properties (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 66999c0c-dc43-4327-99fb-8366f465e69d
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c2bca7f0deef9a5cb137525e165670404cad65ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016553"
---
# <a name="syspdwhealthcomponentproperties-transact-sql"></a>sys.pdw_health_component_properties (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  デバイスを記述するプロパティを格納します。 一部のプロパティは、デバイスの状態を表示し、いくつかのプロパティは、デバイス自体を説明します。  
  
|列名|データ型|説明|範囲|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|コンポーネントのプロパティの一意の識別子。<br /><br /> property_id と component_id は、このビューのキーを形成します。|NOT NULL|  
|component_id|**int**|コンポーネントの ID。 参照してください[sys.pdw_health_components &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)します。<br /><br /> property_id と component_id は、このビューのキーを形成します。|NOT NULL|  
|property_name|**nvarchar (255)**|プロパティの名前です。|NOT NULL|  
|physical_name|**nvarchar(32)**|プロパティ名、製造元によって定義されています。|NOT NULL|  
|is_key|**bit**|デバイス インスタンスが一意または一意でないかどうかを判断します。|NOT NULL<br /><br /> 0 - デバイスのインスタンスは一意です。<br /><br /> 1-デバイスのインスタンスは一意ではありません。|  
  
## <a name="see-also"></a>関連項目  
 [SQL Data Warehouse と Parallel Data Warehouse カタログ ビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
