---
title: sys.spatial_indexes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.spatial_indexes_TSQL
- spatial_indexes
- spatial_indexes_TSQL
- sys.spatial_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_indexes catalog view
ms.assetid: 40e967d5-2e8d-45af-bf5e-5251493cf7cb
author: stevestein
ms.author: sstein
ms.openlocfilehash: f3b2172e48ec787c37fd9b3daab6cafb5c49f88f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078634"
---
# <a name="sysspatialindexes-transact-sql"></a>sys.spatial_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  空間インデックスの主インデックス情報を表します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|\<列を継承 >||列を継承[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)します。|  
|spatial_index_type|**tinyint**|空間インデックスの種類です。<br /><br /> 1 = 幾何学的空間インデックス<br /><br /> 2 = 地理的空間インデックス|  
|spatial_index_type_desc|**nvarchar(60)**|空間インデックスの説明を入力します。<br /><br /> GEOMETRY = 幾何学的空間インデックス<br /><br /> GEOGRAPHY = 地理的空間インデックス|  
|tessellation_scheme|**sysname**|テセレーション スキームの名前です。<br /><br /> GEOMETRY_GRID、GEOMETRY_AUTO_GRID、<br /><br /> GEOGRAPHY_GRID、GEOGRAPHY_AUTO_GRID<br /><br /> 注:テセレーション スキームについては、次を参照してください。[空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)します。|  
|\<列を継承 >||列を継承[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)します。<br /><br /> 継承された列 has_filter と filter_definition は、空間インデックスに固有である列の後に表示されます。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>関連項目  
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.spatial_index_tessellations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  
