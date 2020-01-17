---
title: KEY_COLUMN_USAGE (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- KEY_COLUMN_USAGE_TSQL
- KEY_COLUMN_USAGE
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.KEY_COLUMN_USAGE view
- KEY_COLUMN_USAGE view
ms.assetid: ec1e18c2-63a1-4d2b-ba9a-c13857403782
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d38e6ae0eaf7ed6015834052067db28993cbcccd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948610"
---
# <a name="key_column_usage-transact-sql"></a>KEY_COLUMN_USAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  現在のデータベース内のキーとして制約されている各列の 1 つの行を返します。 この情報スキーマ ビューでは、現在のユーザーがアクセス許可を持っているオブジェクトに関する情報を返します。  
  
 これらのビューから情報を取得するには、**INFORMATION_SCHEMA.** _view_name_ の完全修飾名を指定します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar(** 128 **)**|制約修飾子です。|  
|**CONSTRAINT_SCHEMA**|**nvarchar(** 128 **)**|制約を含むスキーマの名前です。<br /><br /> <strong>\*\* 重要な\* \*</strong> オブジェクトのスキーマを決定 INFORMATION_SCHEMA ビューを使用しないでください。 オブジェクトのスキーマを調べる唯一の信頼性のある方法は、sys.objects カタログ ビューに対するクエリを実行する方法です。|  
|**CONSTRAINT_NAME**|**nvarchar(** 128 **)**|制約の名前。|  
|**TABLE_CATALOG**|**nvarchar(** 128 **)**|テーブルの修飾子です。|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|テーブルを含むスキーマの名前です。<br /><br /> <strong>\*\* 重要な\* \*</strong> オブジェクトのスキーマを決定 INFORMATION_SCHEMA ビューを使用しないでください。 オブジェクトのスキーマを調べる唯一の信頼性のある方法は、sys.objects カタログ ビューに対するクエリを実行する方法です。|  
|**TABLE_NAME**|**nvarchar(** 128 **)**|テーブル名です。|  
|**COLUMN_NAME**|**nvarchar(** 128 **)**|列名|  
|**ORDINAL_POSITION**|**int**|列の序数位置。|  
  
## <a name="see-also"></a>関連項目  
 [システム ビュー &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [情報スキーマ ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.foreign_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)   
 [sys.key_constraints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)  
  
  
