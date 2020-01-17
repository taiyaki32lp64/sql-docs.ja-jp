---
title: 列 (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- COLUMNS
- COLUMNS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- COLUMNS view
- INFORMATION_SCHEMA.COLUMNS view
ms.assetid: bbf7ac4a-7444-4351-a590-a9f71e0bc495
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 021e9e66b281a8bbca6d5c9e21e78ffa4069c5c9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950799"
---
# <a name="columns-transact-sql"></a>列 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  現在のデータベースの現在のユーザーによってアクセスできる列ごとに 1 つの行を返します。  
  
 これらのビューから情報を取得するには、完全修飾名を指定**INFORMATION_SCHEMA** _.view_name_します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar(** 128 **)**|テーブルの修飾子です。|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|テーブルを含むスキーマの名前です。<br /><br /> **&#42;&#42;重要な&#42; &#42;** オブジェクトのスキーマを決定 INFORMATION_SCHEMA ビューを使用しないでください。 オブジェクトのスキーマを調べる唯一の信頼性のある方法は、sys.objects カタログ ビューに対するクエリを実行する方法です。|  
|**TABLE_NAME**|**nvarchar(** 128 **)**|テーブル名です。|  
|**COLUMN_NAME**|**nvarchar(** 128 **)**|列名|  
|**ORDINAL_POSITION**|**int**|列の識別番号。|  
|**COLUMN_DEFAULT**|**nvarchar(** 4000 **)**|列の既定値です。|  
|**IS_NULLABLE**|**varchar(** 3 **)**|列の NULL 値の許容属性。 この列は NULL を許可している場合、この列は、[はい] を返します。 許容されない場合は NO が返されます。|  
|**DATA_TYPE**|**nvarchar(** 128 **)**|システム提供のデータ型。|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|文字、バイナリ データ、文字データ、またはテキストおよびイメージ データの最大長。<br /><br /> 場合は-1 **xml**と大きな値型のデータ。 それ以外の場合、NULL が返されます。 詳細については、「[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)」を参照してください。|  
|**CHARACTER_OCTET_LENGTH**|**int**|バイナリ データ、文字データ、またはテキスト/イメージ データの最大長 (バイト単位)。<br /><br /> 場合は-1 **xml**と大きな値型のデータ。 それ以外の場合、NULL が返されます。|  
|**NUMERIC_PRECISION**|**tinyint**|概数データ、真数データ、整数データ、または通貨データの有効桁数。 それ以外の場合、NULL が返されます。|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|概数データ、真数データ、整数データ、または通貨データの有効桁数の基数。 それ以外の場合、NULL が返されます。|  
|**NUMERIC_SCALE**|**int**|概数データ、真数データ、整数データ、または通貨データの小数点以下桁数。 それ以外の場合、NULL が返されます。|  
|**DATETIME_PRECISION**|**smallint**|サブタイプ コード**datetime**と ISO**間隔**データ型。 他のデータ型の場合は NULL が返されます。|  
|**CHARACTER_SET_CATALOG**|**nvarchar(** 128 **)**|返します**マスター**します。 列が文字データの場合、文字セットが置かれているデータベースを示しますまたは**テキスト**データ型。 それ以外の場合、NULL が返されます。|  
|**CHARACTER_SET_SCHEMA**|**nvarchar(** 128 **)**|常に NULL が返されます。|  
|**CHARACTER_SET_NAME**|**nvarchar(** 128 **)**|この列が文字データの場合、文字セットの一意の名前を返しますまたは**テキスト**データ型。 それ以外の場合、NULL が返されます。|  
|**COLLATION_CATALOG**|**nvarchar(** 128 **)**|常に NULL が返されます。|  
|**COLLATION_SCHEMA**|**nvarchar(** 128 **)**|常に NULL が返されます。|  
|**COLLATION_NAME**|**nvarchar(** 128 **)**|列が文字データの場合は、照合順序の一意の名前を返しますまたは**テキスト**データ型。 それ以外の場合、NULL が返されます。|  
|**DOMAIN_CATALOG**|**nvarchar(** 128 **)**|列が別名データ型の場合は、この列は、ユーザー定義データ型が作成されたデータベース名にします。 それ以外の場合、NULL が返されます。|  
|**DOMAIN_SCHEMA**|**nvarchar(** 128 **)**|列がユーザー定義データ型の場合、この列は、ユーザー定義データ型のスキーマの名前を返します。 それ以外の場合、NULL が返されます。<br /><br /> **&#42;&#42;重要な&#42; &#42;** データ型のスキーマを決定 INFORMATION_SCHEMA ビューを使用しないでください。 型のスキーマを調べる唯一信頼できる方法では、TYPEPROPERTY 関数を使用します。|  
|**ドメイン名**|**nvarchar(** 128 **)**|列がユーザー定義データ型の場合は、この列は、ユーザー定義データ型の名前です。 それ以外の場合、NULL が返されます。|  
  
## <a name="remarks"></a>コメント  
 **ORDINAL_POSITION**の列、 **INFORMATION_SCHEMA します。列**ビューは、COLUMNS_UPDATED 関数から返される列のビット パターンと互換性がありません。 COLUMNS_UPDATED と互換性があるビット パターンを取得するを参照する必要があります、 **ColumnID** COLUMNPROPERTY システム関数を照会する際のプロパティ、 **INFORMATION_SCHEMA します。列**ビュー。 以下に例を示します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TABLE_NAME, COLUMN_NAME, COLUMNPROPERTY(OBJECT_ID(TABLE_SCHEMA + '.' + TABLE_NAME), COLUMN_NAME, 'ColumnID') AS COLUMN_ID  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Person';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [システム ビュー &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [情報スキーマ ビュー &#40;TRANSACT-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.syscharsets &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [COLUMNS_UPDATED &#40;TRANSACT-SQL&#41;](../../t-sql/functions/columns-updated-transact-sql.md)  
  
  
