---
title: sys.xml_schema_attributes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xml_schema_attributes_TSQL
- xml_schema_attributes
- sys.xml_schema_attributes_TSQL
- sys.xml_schema_attributes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_attributes catalog view
ms.assetid: dd0c98aa-5e72-4df6-96d9-482786c8dbb1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ac0f23e73f67c3d95744d974366ab547d50672ea
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044845"
---
# <a name="sysxmlschemaattributes-transact-sql"></a>sys.xml_schema_attributes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  属性を表す XML スキーマ コンポーネントごとに 1 行を返します**symbol_space**の**A**します。  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<列を継承 >**|--|継承[sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)します。|  
|**is_default_fixed**|**bit**|1 = デフォルト値は固定値です。 XML インスタンスでは、この値をオーバーライドできません。<br /><br /> 0 = デフォルト値は属性の固定値ではありません  (既定値)。|  
|**must_be_qualified**|**bit**|1 = 属性には明示的に名前空間の修飾名を追加する必要があります。<br /><br /> 0 = 属性には暗黙的に名前空間の修飾名を追加できます  (既定値)。|  
|**default_value**|**nvarchar**<br /><br /> **(4000)**|属性の既定値。 既定値が提供されない場合は NULL になります。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [XML スキーマ&#40;XML 型システム&#41;カタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
