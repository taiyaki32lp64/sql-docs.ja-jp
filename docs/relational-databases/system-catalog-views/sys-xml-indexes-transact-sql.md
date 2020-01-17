---
title: sys.xml_indexes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_indexes_TSQL
- xml_indexes_TSQL
- sys.xml_indexes
- xml_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_indexes catalog view
ms.assetid: 3408de72-b067-4fda-b5d5-8e856dfd9db3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16d474fc6274fd43b7ebc426445a0881181dcf79
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67895061"
---
# <a name="sysxmlindexes-transact-sql"></a>sys.xml_indexes (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XML インデックスごとに 1 行を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<列を継承 >**||列を継承[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)します。|  
|**using_xml_index_id**|**int**|NULL = プライマリ XML インデックス<br /><br /> Nonnull = セカンダリ XML インデックスです。<br /><br /> Null 以外には、プライマリ XML インデックスへの自己結合参照です。|  
|**secondary_type**|**char(1)**|セカンダリ インデックスの説明を入力します。<br /><br /> P = PATH セカンダリ XML インデックス<br /><br /> V = VALUE セカンダリ XML インデックス<br /><br /> R = PROPERTY セカンダリ XML インデックス<br /><br /> NULL = プライマリ XML インデックス|  
|**secondary_type_desc**|**nvarchar(60)**|セカンダリ インデックスの説明を入力します。<br /><br /> PATH = PATH セカンダリ XML インデックス<br /><br /> VALUE = VALUE セカンダリ XML インデックス<br /><br /> プロパティ = PROPERTY セカンダリ xml インデックスです。<br /><br /> NULL = プライマリ XML インデックス|  
|**xml_index_type**|**tinyint**|インデックスの種類:<br /><br /> 0 = プライマリ XML インデックス<br /><br /> 1 = セカンダリ XML インデックス<br /><br /> 2 = 選択的な XML インデックス<br /><br /> 3 = 選択的セカンダリ XML インデックス|  
|**xml_index_type_description**|**nvarchar(60)**|インデックスの種類の説明。<br /><br /> PRIMARY_XML<br /><br /> セカンダリ XML インデックス<br /><br /> 選択的な XML インデックス<br /><br /> セカンダリ選択的 XML インデックス|  
|**path_id**|**int**|セカンダリ選択的 XML インデックスを除くすべての XML インデックスの場合は NULL です。<br /><br /> それ以外の場合は、選択的セカンダリ XML インデックスを構築する上位変換されたパスの ID です。 この値は、sys.selective_xml_index_paths システム ビューからの path_id と同じ値です。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [オブジェクト カタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
