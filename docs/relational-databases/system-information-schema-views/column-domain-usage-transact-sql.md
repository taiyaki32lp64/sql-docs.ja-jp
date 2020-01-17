---
title: COLUMN_DOMAIN_USAGE (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- COLUMN_DOMAIN_USAGE_TSQL
- COLUMN_DOMAIN_USAGE
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.COLUMN_DOMAIN_USAGE view
- COLUMN_DOMAIN_USAGE view
ms.assetid: deb20037-6a51-47ae-9f49-7601698fafaf
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3cfc7b44672554fc810b54ef0c554d2a570b8325
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950861"
---
# <a name="columndomainusage-transact-sql"></a>COLUMN_DOMAIN_USAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  別名データ型が存在する現在のデータベースの列ごとに 1 行のデータを返します。 この情報スキーマ ビューでは、現在のユーザーがアクセス許可を持っているオブジェクトに関する情報を返します。  
  
 これらのビューから情報を取得するには、完全修飾名を指定**INFORMATION_SCHEMA** 。_view_name_します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**DOMAIN_CATALOG**|**nvarchar(** 128 **)**|別名データ型が存在するデータベース。|  
|**DOMAIN_SCHEMA**|**nvarchar(** 128 **)**|別名データ型を含むスキーマの名前<br /><br /> **&#42;&#42;重要な&#42; &#42;** データ型のスキーマを決定 INFORMATION_SCHEMA ビューを使用しないでください。 型のスキーマを調べる唯一信頼できる方法では、TYPEPROPERTY 関数を使用します。|  
|**ドメイン名**|**sysname**|別名データ型します。|  
|**TABLE_CATALOG**|**nvarchar(** 128 **)**|テーブルの修飾子です。|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|テーブル所有者<br /><br /> **&#42;&#42;重要な&#42; &#42;** オブジェクトのスキーマを決定 INFORMATION_SCHEMA ビューを使用しないでください。 オブジェクトのスキーマを調べる唯一の信頼性のある方法は、sys.objects カタログ ビューに対するクエリを実行する方法です。|  
|**TABLE_NAME**|**sysname**|別名データ型が使用されているテーブル。|  
|**COLUMN_NAME**|**sysname**|別名データ型を使用して列です。|  
  
## <a name="see-also"></a>関連項目  
 [システム ビュー &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [情報スキーマ ビュー &#40;TRANSACT-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  
