---
title: sys.assembly_types (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- assembly_types
- sys.assembly_types
- sys.assembly_types_TSQL
- assembly_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_types catalog view
ms.assetid: 35f0384f-7a6d-41b1-9461-f1406d68f317
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8a5358b75da914919cb4db567dc7eae6ad8617f1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118107"
---
# <a name="sysassemblytypes-transact-sql"></a>sys.assembly_types (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  CLR アセンブリによって定義されるユーザー定義型ごとに 1 行のデータを保持します。 次**sys.assembly_types**継承された列の一覧に表示されます (を参照してください[sys.types &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)) 後**rule_object_id**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|この型の作成元であるアセンブリの ID です。|  
|**assembly_class**|**sysname**|この型を定義しているアセンブリ内のクラスの名前です。|  
|**is_binary_ordered**|**bit**|この型のバイトの並べ替えは、型の比較演算子を使用した並べ替えと同じです。|  
|**is_fixed_length**|**bit**|型の長さは、常に max_length と同じです。|  
|**prog_id**|**nvarchar(40)**|COM に公開される型の progID|  
|**assembly_qualified_name**|**nvarchar (4000)**|アセンブリ修飾型名。 名前は、Type.GetType() に渡すに適した形式では。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [スカラー型カタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)  
  
  
