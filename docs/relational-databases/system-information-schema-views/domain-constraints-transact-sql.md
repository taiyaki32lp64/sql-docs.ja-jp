---
title: DOMAIN_CONSTRAINTS (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DOMAIN_CONSTRAINTS
- DOMAIN_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.DOMAIN_CONSTRAINTS view
- DOMAIN_CONSTRAINTS view
ms.assetid: 436c4480-f1e3-403f-b2bd-de04539afe3c
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7392edabcef2b1ff8348bab641380b6ab64cea0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950764"
---
# <a name="domainconstraints-transact-sql"></a>DOMAIN_CONSTRAINTS (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  ルールがバインドしているが、現在のデータベースで別名データ型ごとに 1 行を返しますは、現在のユーザーによってアクセスできます。  
  
 これらのビューから情報を取得するには、完全修飾名を指定**INFORMATION_SCHEMA** 。_view_name_します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar(** 128 **)**|データベースのルールが存在します。|  
|**CONSTRAINT_SCHEMA**|**nvarchar(** 128 **)**|制約を含むスキーマの名前です。<br /><br /> <strong>\*\* 重要な\* \*</strong> オブジェクトのスキーマを決定 INFORMATION_SCHEMA ビューを使用しないでください。 オブジェクトのスキーマを調べる唯一の信頼性のある方法は、sys.objects カタログ ビューに対するクエリを実行する方法です。|  
|**CONSTRAINT_NAME**|**sysname**|規則の名前。|  
|**DOMAIN_CATALOG**|**nvarchar(** 128 **)**|別名データ型が存在するデータベース。|  
|**DOMAIN_SCHEMA**|**nvarchar(** 128 **)**|別名データ型を含むスキーマの名前<br /><br /> <strong>\*\* 重要な\* \*</strong> データ型のスキーマを決定 INFORMATION_SCHEMA ビューを使用しないでください。 型のスキーマを調べる唯一信頼できる方法では、TYPEPROPERTY 関数を使用します。|  
|**ドメイン名**|**sysname**|別名データ型します。|  
|**IS_DEFERRABLE**|**varchar(** 2 **)**|制約チェックを遅延可能にするかどうかを指定します。 常に返しますいいえ。|  
|**INITIALLY_DEFERRED**|**varchar(** 2 **)**|制約チェックが最初に延期されているかどうかを示します。 常に返しますいいえ。|  
  
## <a name="see-also"></a>関連項目  
 [システム ビュー &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [情報スキーマ ビュー &#40;TRANSACT-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  
