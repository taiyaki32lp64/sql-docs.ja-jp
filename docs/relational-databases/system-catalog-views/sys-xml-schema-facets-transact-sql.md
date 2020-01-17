---
title: sys.xml_schema_facets (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_facets
- xml_schema_facets_TSQL
- sys.xml_schema_facets_TSQL
- xml_schema_facets
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_facets catalog view
ms.assetid: 4402dde9-1877-4872-8550-140dc2a177d2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 41e00ca05205fcb1384d436de2f423c63e05ba5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103364"
---
# <a name="sysxmlschemafacets-transact-sql"></a>sys.xml_schema_facets (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Xml 型定義のファセット (制約) ごとに 1 行を返します (対応する**sys.xml_types**)。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|ID の XML コンポーネント (型) がこのファセットが所属します。|  
|**facet_id**|**int**|ファセット、コンポーネント id 内で一意の ID (1 から始まる序数) にします。|  
|**kind**|**char(2)**|ファセットの種類。<br /><br /> LG 長を =<br /><br /> LN = 最小の長さ<br /><br /> LX = 最大の長さ<br /><br /> PT = パターン (正規表現)<br /><br /> EU = 列挙<br /><br /> IN = 最小の包含値<br /><br /> IX = 最大の包含値<br /><br /> EN = 最小の排他値<br /><br /> EX = 最大の排他値<br /><br /> DT = 総桁数<br /><br /> DF 小数桁を =<br /><br /> WS = 空白の正規化|  
|**kind_desc**|**Nvarchar (60)**|ファセットの種類の説明。<br /><br /> LENGTH<br /><br /> MINIMUM_LENGTH<br /><br /> MAXIMUM_LENGTH<br /><br /> パターン<br /><br /> ENUMERATION<br /><br /> MINIMUM_INCLUSIVE_VALUE<br /><br /> MAXIMUM_INCLUSIVE_VALUE<br /><br /> MINIMUM_EXCLUSIVE_VALUE<br /><br /> MAXIMUM_EXCLUSIVE_VALUE<br /><br /> TOTAL_DIGITS<br /><br /> FRACTION_DIGITS<br /><br /> WHITESPACE_NORMALIZATION|  
|**is_fixed**|**bit**|1 = ファセットには事前に指定された固定値があります。<br /><br /> 0 = 固定値はありません (既定値)。|  
|**value**|**nvarchar (4000)**|ファセットの固定、事前に指定された値。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML スキーマ&#40;XML 型システム&#41;カタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
