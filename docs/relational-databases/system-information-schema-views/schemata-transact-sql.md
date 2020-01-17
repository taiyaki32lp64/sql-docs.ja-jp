---
title: スキーマ (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SCHEMATA_TSQL
- SCHEMATA
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.SCHEMATA view
- SCHEMATA view
ms.assetid: 69617642-0f54-4b25-b62f-5f39c8909601
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 16b2a23c696b4da405e4983689217abb15074f03
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078431"
---
# <a name="schemata-transact-sql"></a>スキーマ (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  現在のデータベース内の各スキーマの 1 つの行を返します。 これらのビューから情報を取得するには、完全修飾名を指定**INFORMATION_SCHEMA** 。_view_name_します。 インスタンスのすべてのデータベースに関する情報を取得する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、クエリ、 [sys.databases &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)カタログ ビューです。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**CATALOG_NAME**|**sysname**|現在のデータベースの名前|  
|**SCHEMA_NAME**|**nvarchar(** 128 **)**|スキーマの名前を返します。|  
|**SCHEMA_OWNER**|**nvarchar(** 128 **)**|スキーマの所有者の名前。<br /><br /> **&#42;&#42;重要な&#42; &#42;** オブジェクトのスキーマを決定 INFORMATION_SCHEMA ビューを使用しないでください。 オブジェクトのスキーマを調べる唯一信頼できる方法は、sys.objects カタログ ビューをクエリします。|  
|**DEFAULT_CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|常に NULL が返されます。|  
|**DEFAULT_CHARACTER_SET_SCHEMA**|**varchar(** 3 **)**|常に NULL が返されます。|  
|**DEFAULT_CHARACTER_SET_NAME**|**sysname**|既定の文字セットの名前を返します。|  

**例**  
次の例では、master データベースにスキーマについての情報を返します。  
```sql  
SELECT * FROM master.INFORMATION_SCHEMA.SCHEMATA;
```  

## <a name="see-also"></a>関連項目  
 [システム ビュー &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [情報スキーマ ビュー &#40;TRANSACT-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.schemas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [sys.syscharsets &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)  
  
  
