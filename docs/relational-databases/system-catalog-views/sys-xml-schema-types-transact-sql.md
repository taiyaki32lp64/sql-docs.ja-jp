---
title: sys.xml_schema_types (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_types_TSQL
- xml_schema_types_TSQL
- sys.xml_schema_types
- xml_schema_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_types catalog view
ms.assetid: 441ba49d-f778-4fa1-98c4-ced375a01a34
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a78730509cc1f9eeec83b8d9ff9cb0917e0ed99
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060434"
---
# <a name="sysxmlschematypes-transact-sql"></a>sys.xml_schema_types (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  型、XML スキーマ コンポーネントごとに 1 行を返します**symbol_space**の**T**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<列を継承 >**||列を継承[sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)します。|  
|**is_abstract**|**bit**|1 = 型が抽象型。 この型の要素のすべてのインスタンスを使用する必要があります**xsi:type**を抽象でない派生型を示します。<br /><br /> 0 = 型は abstract ではありません (既定値)。|  
|**allows_mixed_content**|**bit**|1 = 混合コンテンツを許可<br /><br /> 0 = 混合コンテンツは許可されません。 (既定値)。|  
|**is_extension_blocked**|**bit**|1 = block 属性、ときに、インスタンスで、型の拡張による置き換えはブロック、 **complexType**定義または**blockDefault**属性の先祖の\<スキーマ >要素情報項目は、"extension"または"#all"に設定されます。<br /><br /> 0 = 拡張による置き換えはブロックされません。|  
|**is_restriction_blocked**|**bit**|1 = block 属性、ときに、インスタンスで、型の制約による置き換えはブロック、 **complexType**定義または**blockDefault**属性の先祖の\<スキーマ >要素情報項目は、"restriction"または"#all"に設定されます。<br /><br /> 0 = 制約による置き換えはブロックされません (既定値)。|  
|**is_final_extension**|**bit**|1、型の拡張による派生を = がブロックされている場合、final 属性、 **complexType**定義または**finalDefault**の先祖の属性\<スキーマ > 要素情報項目は、"extension"または"#all"に設定されます。<br /><br /> 0 = 拡張は許可されます (既定値)。|  
|**is_final_restriction**|**bit**|1、型の制約による派生を = がブロックされている場合、単純な final 属性、または**complexType**定義または**finalDefault**属性の先祖の\<スキーマ > 要素情報項目は、"restriction"または"#all"に設定されます。<br /><br /> 0 = 制約は許可されます (既定値)。|  
|**is_final_list_member**|**bit**|1 = この単純型は、リスト項目の型として使用できません。<br /><br /> 0 = この型は複合型、またはリスト項目の型として使用できます (既定値)。|  
|**is_final_union_member**|**bit**|1 = この単純型を共用体型のメンバーの種類として使用することはできません。<br /><br /> 0 = この型は複合型。 または、その共用体メンバーの型として使用できます。 (既定値)。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML スキーマ&#40;XML 型システム&#41;カタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
