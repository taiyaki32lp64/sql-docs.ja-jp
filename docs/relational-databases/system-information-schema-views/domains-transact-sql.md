---
title: ドメイン (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DOMAINS_TSQL
- DOMAINS
dev_langs:
- TSQL
helpviewer_keywords:
- DOMAINS view
- INFORMATION_SCHEMA.DOMAINS view
ms.assetid: f0b734d5-816f-4b10-a60c-615931b515c2
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cb602bf26b20ea916a46655cf813f4c1a6ab4f1b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950734"
---
# <a name="domains-transact-sql"></a>DOMAINS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  現在のデータベースの現在のユーザーによってアクセスできる別名データ型ごとに 1 行を返します。  
  
 これらのビューから情報を取得するには、完全修飾名を指定**INFORMATION_SCHEMA** 。_view_name_します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**DOMAIN_CATALOG**|**nvarchar(** 128 **)**|別名データ型が存在するデータベース。|  
|**DOMAIN_SCHEMA**|**nvarchar(** 128 **)**|別名データ型を含むスキーマの名前。<br /><br /> **&#42;&#42;重要な&#42; &#42;** データ型のスキーマを決定 INFORMATION_SCHEMA ビューを使用しないでください。 型のスキーマを調べる唯一信頼できる方法では、TYPEPROPERTY 関数を使用します。|  
|**ドメイン名**|**sysname**|別名データ型します。|  
|**DATA_TYPE**|**sysname**|システム提供のデータ型。|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|文字、バイナリ データ、文字データ、またはテキストおよびイメージ データの最大長。<br /><br /> 場合は-1 **xml**と大きな値型のデータ。 それ以外の場合、NULL が返されます。 詳細については、「[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)」を参照してください。|  
|**CHARACTER_OCTET_LENGTH**|**int**|バイナリ データ、文字データ、またはテキスト/イメージ データの最大長 (バイト単位)。<br /><br /> 場合は-1 **xml**と大きな値型のデータ。 それ以外の場合、NULL が返されます。|  
|**COLLATION_CATALOG**|**varchar (** 6 **)**|常に NULL が返されます。|  
|**COLLATION_SCHEMA**|**varchar(** 3 **)**|常に NULL が返されます。|  
|**COLLATION_NAME**|**nvarchar(** 128 **)**|列が文字データの場合は、並べ替え順序の一意の名前を返しますまたは**テキスト**データ型。 それ以外の場合、NULL が返されます。|  
|**CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|返します**マスター**します。 列が文字データの場合、文字セットが置かれているデータベースを示しますまたは**テキスト**データ型。 それ以外の場合、NULL が返されます。|  
|**CHARACTER_SET_SCHEMA**|**varchar(** 3 **)**|常に NULL が返されます。|  
|**CHARACTER_SET_NAME**|**nvarchar(** 128 **)**|この列が文字データの場合、文字セットの一意の名前を返しますまたは**テキスト**データ型。 それ以外の場合、NULL が返されます。|  
|**NUMERIC_PRECISION**|**tinyint**|概数データ、真数データ、整数データ、または通貨データの有効桁数。 それ以外の場合、NULL が返されます。|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|概数データ、真数データ、整数データ、または通貨データの有効桁数の基数。 それ以外の場合、NULL が返されます。|  
|**NUMERIC_SCALE**|**tinyint**|概数データ、真数データ、整数データ、または通貨データの小数点以下桁数。 それ以外の場合、NULL が返されます。|  
|**DATETIME_PRECISION**|**smallint**|サブタイプ コード**datetime**と ISO**間隔**データ型。 その他のデータ型の場合は、NULL が返されます。|  
|**DOMAIN_DEFAULT**|**nvarchar(** 4000 **)**|実際のテキストの定義の[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメント。|  
  
## <a name="see-also"></a>関連項目  
 [システム ビュー &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [情報スキーマ ビュー &#40;TRANSACT-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.syscharsets &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  
