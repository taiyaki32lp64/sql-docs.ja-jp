---
title: sys.xml_schema_elements (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_elements
- sys.xml_schema_elements_TSQL
- xml_schema_elements
- xml_schema_elements_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_elements catalog view
ms.assetid: 190ed0cd-0c5e-4607-9db4-9e77cacf17d7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d43f30f15502a41882190dcdd19984d9ec042d4a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037393"
---
# <a name="sysxmlschemaelements-transact-sql"></a>sys.xml_schema_elements (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  型、XML スキーマ コンポーネントごとに 1 行を返します**symbol_space**の**E**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<列を継承 >**|**--**|列を継承[sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)します。|  
|**is_default_fixed**|**bit**|1 = 既定値は固定値です。 XML インスタンスでは、この値をオーバーライドできません。<br /><br /> 0 = 既定値は、要素の固定値ではありません。 (既定値)。|  
|**is_abstract**|**bit**|1 = 要素は abstract であり、インスタンス ドキュメント内では使用できません。 要素の代替グループのメンバーは、インスタンス ドキュメント内に表示される必要があります。<br /><br /> 0 = 要素は abstract ではありません。 (既定値)。|  
|**is_nillable**|**bit**|1 = 要素は nillable です。<br /><br /> 0 = 要素は nillable ではありません (既定値)。|  
|**must_be_qualified**|**bit**|1 = 要素する必要があります明示的に名前空間修飾できます。<br /><br /> 0 = 要素には暗黙的に名前空間の修飾名が追加されます (既定値)。|  
|**is_extension_blocked**|**bit**|1 = 拡張型のインスタンスへの置換はブロックされます。<br /><br /> 0 = 置換拡張子を持つ型を使用します。 (既定値)。|  
|**is_restriction_blocked**|**bit**|1 = 制限型のインスタンスへの置換はブロックされます。<br /><br /> 0 = 置換制限の種類は許可されます。 (既定値)。|  
|**is_substitution_blocked**|**bit**|1 = 代替グループのインスタンスは使用できません。<br /><br /> 0 = 置換の置換グループは許可されています。 (既定値)。|  
|**is_final_extension**|**bit**|1 = 拡張型のインスタンスへの置換は許可されません。<br /><br /> 0 = 拡張型のインスタンスへの置換は許可されます (既定値)。|  
|**is_final_restriction**|**bit**|1 = 置換制限のインスタンスの種類は許可されません。<br /><br /> 0 = 置換制限のインスタンス型が許可されます。 (既定値)。|  
|**default_value**|**nvarchar (4000)**|要素の既定値。 既定値が指定されていない場合は NULL です。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML スキーマ&#40;XML 型システム&#41;カタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
