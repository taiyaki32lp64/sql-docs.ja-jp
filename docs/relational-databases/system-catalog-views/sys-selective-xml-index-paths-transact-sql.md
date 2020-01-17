---
title: sys.selective_xml_index_paths (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
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
ms.assetid: 07a73d71-ec3e-4894-947a-5859ca62c606
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 9ff85273a1e970b3bb891d1816a96019dd4f3ae5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135190"
---
# <a name="sysselectivexmlindexpaths-transact-sql"></a>sys.selective_xml_index_paths (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  以降で使用できる[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]Service Pack 1 では、sys.selective_xml_index_paths の各行が特定の選択的 xml インデックスの 1 つの上位変換されたパスを表します。  
  
 次のステートメントを使用して、テーブル T の xmlcol に対して選択的 XML インデックスを作成すると、  
  
```  
CREATE SELECTIVE XML INDEX sxi1 ON T(xmlcol)   
FOR ( path1 = '/a/b/c' AS XQUERY 'xs:string',  
      path2 = '/a/b/d' AS XQUERY 'xs:double'  
    )  
```  
  
 インデックス sxi1 に対応する sys.selective_xml_index_paths の 2 つの新しい行があります。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|XML 列を持つテーブルの ID。|  
|**index_id**|**int**|選択的 xml インデックスの一意の id。|  
|**path_id**|**int**|上位変換された XML パス ID。|  
|**path**|**nvarchar (4000)**|上位変換されたパス。 たとえば、'/a と b/c//e'。|  
|**name**|**sysname**|パス名です。|  
|**path_type**|**tinyint**|0 = XQUERY<br /><br /> 1 = SQL|  
|**path_type_desc**|**sysname**|基づく**path_type** "XQUERY"または 'SQL' の値します。|  
|**xml_component_id**|**int**|データベース内の XML スキーマ コンポーネントの一意の ID。|  
|**xquery_type_description**|**nvarchar (4000)**|指定された XSD 型の名前。|  
|**is_xquery_type_inferred**|**bit**|1 = 型が推論されます。|  
|**xquery_max_length**|**smallint**|最大長 (XSD 型の文字で表される)。|  
|**is_xquery_max_length_inferred**|**bit**|1 = 最大長が推測されます。|  
|**is_node**|**bit**|0 = node() ヒントが存在しない。<br /><br /> 1 = node() 最適化ヒントを適用します。|  
|**system_type_id**|**tinyint**|列のシステム型の ID。|  
|**user_type_id**|**tinyint**|列のユーザーの種類の ID。|  
|**max_length**|**smallint**|型のバイト単位で最大長。<br /><br /> -1 の場合、列のデータ型は varchar(max)、nvarchar(max)、varbinary(max)、または xml です。|  
|**有効桁数 (precision)**|**tinyint**|型が数値型の場合は、最大有効桁数。 それ以外の場合 0 を返します。|  
|**scale**|**tinyint**|数値ベースである場合、型の最大小数点以下桁数。 それ以外の場合は、0 に設定されます。|  
|**collation_name**|**sysname**|型が文字型の場合は、照合順序名。 それ以外の場合は NULL です。|  
|**is_singleton**|**bit**|0 = SINGLETON ヒントが存在しません。<br /><br /> 1 = SINGLETON 最適化ヒントが適用される。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML スキーマ&#40;XML 型システム&#41;カタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
