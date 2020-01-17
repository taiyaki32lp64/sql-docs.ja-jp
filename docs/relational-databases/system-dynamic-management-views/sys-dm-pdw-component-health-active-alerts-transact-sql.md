---
title: dm_pdw_component_health_active_alerts (Transact-sql
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: c53e4a36-b841-424a-b8e2-255b1878deb6
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 90531889d3e510d342ff39abdf069f75f3c371aa
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401710"
---
# <a name="sysdm_pdw_component_health_active_alerts-transact-sql"></a>dm_pdw_component_health_active_alerts (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  コンポーネントのアクティブな[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]アラートを格納します。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**通り**|[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]ノードの一意識別子。<br /><br /> pdw_node_id、component_id、component_instance_id、alert_id、および alert_instance_id を使用して、このビューのキーを形成します。|NOT NULL|  
|component_id|**通り**|コンポーネントの ID。 「 [Sys. pdw_health_components &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)」を参照してください。<br /><br /> pdw_node_id、component_id、component_instance_id、alert_id、および alert_instance_id を使用して、このビューのキーを形成します。|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id、component_id、component_instance_id、alert_id、および alert_instance_id を使用して、このビューのキーを形成します。|NOT NULL|  
|alert_id|**通り**|アラートの種類の ID。 「 [Sys. pdw_health_alerts &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)」を参照してください。<br /><br /> pdw_node_id、component_id、component_instance_id、alert_id、および alert_instance_id を使用して、このビューのキーを形成します。|NOT NULL|  
|alert_instance_id|**nvarchar (36)**|指定された警告のインスタンスを識別します。<br /><br /> pdw_node_id、component_id、component_instance_id、alert_id、および alert_instance_id を使用して、このビューのキーを形成します。|NOT NULL|  
|current_value|**nvarchar(255)**|アラートの種類が StatusChange の場合に使用します。 これは、現在のコンポーネントのステータスです。 種類がしきい値のアラートの値は NULL です。 アラートの種類の一覧については、「 [pdw_health_alerts &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) 」を参照してください。|NULL|  
|previous_value|**nvarchar(255)**|アラートの種類が StatusChange の場合に使用します。 これは、以前のコンポーネントの状態です。 種類がしきい値のアラートの値は NULL です。 アラートの種類の一覧については、「 [pdw_health_alerts &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) 」を参照してください。|NULL|  
|create_time|**/**|アラートが生成された日時。|NOT NULL|  
  
 このビューで保持される最大行数の詳細については[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]、「」の「最小値と最大値」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Data Warehouse および並列データウェアハウスの動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
