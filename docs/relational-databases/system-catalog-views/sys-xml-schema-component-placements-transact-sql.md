---
title: sys.xml_schema_component_placements (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_component_placements
- xml_schema_component_placements_TSQL
- xml_schema_component_placements
- sys.xml_schema_component_placements_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_component_placements catalog view
ms.assetid: 2d3c8828-e4b3-423d-bf11-990464c1341b
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 0bab2cda409d5715e1f6b5519e1b760eb1cad9c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103371"
---
# <a name="sysxmlschemacomponentplacements-transact-sql"></a>sys.xml_schema_component_placements (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  配置の XML スキーマ コンポーネントごとに 1 行を返します。  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|この配置を所有する XML スキーマ コンポーネントの ID。|  
|**placement_id**|**int**|配置の ID。 配置を所有する XML スキーマ コンポーネント内で一意です。|  
|**placed_xml_component_id**|**int**|配置された XML スキーマ コンポーネントの ID。|  
|**is_default_fixed**|**bit**|1 = 既定値は固定値です。 XML インスタンスでは、この値をオーバーライドできません。<br /><br /> 0 = 値はオーバーライドされる場合があります (既定)|  
|**min_occurrences**|**int**|配置されたコンポーネントの最小数に発生します。|  
|**max_occurrences**|**int**|配置されたコンポーネントの最大数に発生します。|  
|**default_value**|**nvarchar (4000)**|提供されている場合は、既定値です。 既定値が指定されていない場合は NULL です。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML スキーマ&#40;XML 型システム&#41;カタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
