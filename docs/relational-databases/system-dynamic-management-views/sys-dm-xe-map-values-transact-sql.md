---
title: sys.dm_xe_map_values (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_xe_map_values
- dm_xe_map_values
- dm_xe_map_values_TSQL
- sys.dm_xe_map_values_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_map_values dynamic management view
- xe
ms.assetid: c0c5dd7e-9cee-47e2-b65a-88194c00aa1f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6eb770951e48f7145311fb75de18a17236a09d7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090320"
---
# <a name="sysdmxemapvalues-transact-sql"></a>sys.dm_xe_map_values (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ユーザーによる判読が可能なテキストに対する内部数値キーのマッピングを返します。  
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|NAME|**nvarchar (256)**|マップの名前。 名前は、ローカル システム全体で一意です。 NULL 値は許可されません。|  
|object_package_guid|**uniqueidentifier**|マップを含むパッケージの GUID。 NULL 値は許可されません。|  
|map_key|**int**|内部キー値。 NULL 値は許可されません。|  
|map_value|**nvarchar(3072)**|キーの値の説明。 NULL 値は許可されません。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
### <a name="relationship-cardinalities"></a>リレーションシップの基数  
  
|From|変換先|リレーションシップ|  
|----------|--------|------------------|  
|dm_xe_map_values.object_package_guid<br /><br /> dm_xe_map_values.name|sys.dm_xe_objects.package_guid<br /><br /> sys.dm_xe_objects.name|多対一| 
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューおよび関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

