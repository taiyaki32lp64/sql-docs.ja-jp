---
title: sys.sql_dependencies (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sql_dependencies
- sql_dependencies_TSQL
- sys.sql_dependencies_TSQL
- sys.sql_dependencies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_dependencies catalog view
ms.assetid: 1779aa87-a0b8-470a-a286-d7cc0b93ad2e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8742ebefab7a4b826eac0088a2d57f022a27715b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073183"
---
# <a name="syssqldependencies-transact-sql"></a>sys.sql_dependencies (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  参照先エンティティで参照されるように各依存関係の行を格納、[!INCLUDE[tsql](../../includes/tsql-md.md)]式またはその他の参照元オブジェクトを定義するステートメント。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)代わりにします。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|参照先エンティティのクラスを識別します。<br /><br /> 0 = オブジェクトまたは列 (非スキーマ バインド参照のみ)<br /><br /> 1 = オブジェクトまたは列 (スキーマ バインド参照)<br /><br /> 2 = 型 (スキーマ バインド参照)<br /><br /> 3 = XML スキーマ コレクション (スキーマ バインド参照)<br /><br /> 4 = パーティション関数 (スキーマ バインド参照)|  
|**class_desc**|**nvarchar(60)**|参照先エンティティのクラスの説明です。<br /><br /> **OBJECT_OR_COLUMN_REFERENCE_NON_SCHEMA_BOUND**<br /><br /> **OBJECT_OR_COLUMN_REFERENCE_SCHEMA_BOUND**<br /><br /> **TYPE_REFERENCE**<br /><br /> **XML_SCHEMA_COLLECTION_REFERENCE**<br /><br /> **PARTITION_FUNCTION_REFERENCE**|  
|**object_id**|**int**|参照元オブジェクトの ID。|  
|**column_id**|**int**|参照元の ID の列、ID 列を参照する場合それ以外の場合、0 を返します。|  
|**referenced_major_id**|**int**|クラスの値によって解釈される、参照先エンティティの ID による。<br /><br /> 0、1 = オブジェクトまたは列のオブジェクト ID。<br /><br /> 2 = 型 ID<br /><br /> 3 = XML スキーマ コレクション ID|  
|**referenced_minor_id**|**int**|次に示すように、クラスの値によって解釈される、参照先エンティティの補助 ID です。<br /><br /> この値は、class の値によって異なります。<br /><br /> 0、 **referenced_minor_id**列 ID、または列ではない場合は 0。<br /><br /> 1、 **referenced_minor_id**列 ID、または列ではない場合は 0。<br /><br /> それ以外の場合、 **referenced_minor_id** = 0。|  
|**is_selected**|**bit**|オブジェクトまたは列が選択されています。|  
|**is_updated**|**bit**|オブジェクトまたは列が更新されます。|  
|**is_select_all**|**bit**|オブジェクトが SELECT で使用されます * 句 (オブジェクト レベルのみ)。|  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [SQL Server システム カタログに対するクエリに関してよくあるご質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
