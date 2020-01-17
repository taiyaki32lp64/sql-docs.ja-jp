---
title: sys.xml_schema_components (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xml_schema_components
- sys.xml_schema_components_TSQL
- sys.xml_schema_components
- xml_schema_components_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_components catalog view
ms.assetid: 70142d3a-f8b5-4ee2-8287-3935f0f67aa2
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 7b9ab66e0a25067440a496c6c5eb04b5d8b61e64
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039283"
---
# <a name="sysxmlschemacomponents-transact-sql"></a>sys.xml_schema_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XML スキーマのコンポーネントごとに 1 行のデータを返します。 ペア (**collection_id**、 **namespace_id**) が含まれる名前空間に対する複合外部キーです。 名前付きコンポーネントの値は、 **symbol_space**、**name**、 **scoping_xml_component_id**、 **is_qualified**、 **xml_namespace_id**、 **xml_collection_id**は一意です。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|データベース内の XML スキーマ コンポーネントの一意の ID。|  
|**xml_collection_id**|**int**|コンポーネントの名前空間を含む XML スキーマ コレクションの ID。|  
|**xml_namespace_id**|**int**|コレクション内の XML 名前空間の ID。|  
|**is_qualified**|**bit**|1 = このコンポーネントには明示的な名前空間の修飾子があります。<br /><br /> 0 = これはローカル スコープのコンポーネントです。 この場合は、ペア**namespace_id**、 **collection_id**、「ない名前空間」を指す**targetNamespace**します。<br /><br /> ワイルドカード コンポーネントでは、この値は 1 になります。|  
|**name**|**nvarchar**<br /><br /> **(4000)**|XML スキーマ コンポーネントの一意の名前。 コンポーネントに名前が付けられていない場合は NULL です。|  
|**symbol_space**|**char(1)**|**kind**に基づいてこの記号名が一意にする領域:<br /><br /> N = なし<br /><br /> T = 種類<br /><br /> E = 要素<br /><br /> M = モデル - グループ<br /><br /> A = 属性<br /><br /> G = 属性 - グループ|  
|**symbol_space_desc**|**nvarchar**<br /><br /> **(60)**|**kind**に基づいてこの記号名が一意にする空間の説明が:<br /><br /> なし<br /><br /> TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP|  
|**kind**|**char(1)**|XML スキーマ コンポーネントの種類。<br /><br /> N = 任意の型 (特殊な固有コンポーネント)<br /><br /> Z = 任意の単純型 (特殊な固有コンポーネント)<br /><br /> P = プリミティブ型 (固有の型)<br /><br /> S = 単純型<br /><br /> L = リスト型<br /><br /> U = union 型<br /><br /> C = 複合単純型 (単純型から派生)<br /><br /> K = 複合型<br /><br /> E = 要素<br /><br /> M = モデル - グループ<br /><br /> W = 要素 - ワイルドカード<br /><br /> A = 属性<br /><br /> G = 属性 - グループ<br /><br /> V = 属性 - ワイルドカード|  
|**kind_desc**|**nvarchar**<br /><br /> **(60)**|XML スキーマ コンポーネントの種類の説明。<br /><br /> ANY_TYPE<br /><br /> ANY_SIMPLE_TYPE<br /><br /> PRIMITIVE_TYPE<br /><br /> SIMPLE_TYPE<br /><br /> LIST_TYPE<br /><br /> UNION_TYPE<br /><br /> COMPLEX_SIMPLE_TYPE<br /><br /> COMPLEX_TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ELEMENT_WILDCARD<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP<br /><br /> ATTRIBUTE_WILDCARD|  
|**derivation**|**char(1)**|派生型の派生メソッド。<br /><br /> N = なし (派生なし)<br /><br /> X = 拡張<br /><br /> R = 制約<br /><br /> S = 代替|  
|**derivation_desc**|**nvarchar**<br /><br /> **(60)**|派生型の派生メソッドの説明。<br /><br /> なし<br /><br /> EXTENSION<br /><br /> RESTRICTION<br /><br /> SUBSTITUTION|  
|**base_xml_component_id**|**int**|コンポーネントの派生元となるコンポーネントの ID。 存在しない場合は NULL です。|  
|**scoping_xml_component_id**|**int**|スコープを決定するコンポーネントの一意の ID。 存在しない場合は NULL です (グローバル スコープ)。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML スキーマ&#40;XML 型システム&#41;カタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
