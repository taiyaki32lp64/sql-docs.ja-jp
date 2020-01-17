---
title: CONSTRAINT_COLUMN_USAGE (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CONSTRAINT_COLUMN_USAGE_TSQL
- CONSTRAINT_COLUMN_USAGE
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.CONSTRAINT_COLUMN_USAGE view
- CONSTRAINT_COLUMN_USAGE view
ms.assetid: 0f3ae521-6b19-43ad-b2c4-3822adb19591
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e0936e74b3c48a2fe3298215107ae48d0c3b63cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950785"
---
# <a name="constraintcolumnusage-transact-sql"></a>CONSTRAINT_COLUMN_USAGE (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  現在のデータベース内にある、制約が定義されている列ごとに 1 行のデータを返します。 この情報スキーマ ビューでは、現在のユーザーがアクセス許可を持っているオブジェクトに関する情報を返します。  
  
 これらのビューから情報を取得するには、完全修飾名を指定**INFORMATION_SCHEMA** 。_view_name_します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar(** 128 **)**|テーブルの修飾子です。|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|テーブルの所有者を含むスキーマの名前<br /><br /> **&#42;&#42;重要な&#42; &#42;** オブジェクトのスキーマを決定 INFORMATION_SCHEMA ビューを使用しないでください。 オブジェクトのスキーマを調べる唯一の信頼性のある方法は、sys.objects カタログ ビューに対するクエリを実行する方法です。|  
|**TABLE_NAME**|**nvarchar(** 128 **)**|テーブル名です。|  
|**COLUMN_NAME**|**nvarchar(** 128 **)**|列名|  
|**CONSTRAINT_CATALOG**|**nvarchar(** 128 **)**|制約修飾子です。|  
|**CONSTRAINT_SCHEMA**|**nvarchar(** 128 **)**|制約を含むスキーマの名前です。<br /><br /> **&#42;&#42;重要な&#42; &#42;** オブジェクトのスキーマを決定 INFORMATION_SCHEMA ビューを使用しないでください。 オブジェクトのスキーマを調べる唯一の信頼性のある方法は、sys.objects カタログ ビューに対するクエリを実行する方法です。|  
|**CONSTRAINT_NAME**|**nvarchar(** 128 **)**|制約の名前。|  
  
## <a name="see-also"></a>関連項目  
 [システム ビュー &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [情報スキーマ ビュー &#40;TRANSACT-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [sys.check_constraints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [sys.key_constraints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [sys.foreign_keys &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)  
  
  
