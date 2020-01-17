---
title: ROUTINE_COLUMNS (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- ROUTINE_COLUMNS_TSQL
- ROUTINE_COLUMNS
dev_langs:
- TSQL
helpviewer_keywords:
- ROUTINE_COLUMNS view
- INFORMATION_SCHEMA.ROUTINE_COLUMNS view
ms.assetid: 91dbc61b-e4c0-4826-976c-b2fce88b7793
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5b0ed500b1217ae70dca72ab6eab64ab661c22ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078534"
---
# <a name="routinecolumns-transact-sql"></a>ROUTINE_COLUMNS (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  現在のデータベース内の、現在のユーザーがアクセスできるテーブル値関数によって返される列ごとに、1 行のデータを返します。  
  
 このビューから情報を取得するには、完全修飾名を指定**INFORMATION_SCHEMA** 。_view_name_します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar(** 128 **)**|テーブル値関数のカタログやデータベースの名前。|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|テーブル値関数を含むスキーマの名前です。<br /><br /> <strong>\*\* 重要な\* \*</strong> オブジェクトのスキーマを決定 INFORMATION_SCHEMA ビューを使用しないでください。 オブジェクトのスキーマを調べる唯一の信頼性のある方法は、sys.objects カタログ ビューに対するクエリを実行する方法です。|  
|**TABLE_NAME**|**nvarchar(** 128 **)**|テーブル値関数の名前。|  
|**COLUMN_NAME**|**nvarchar(** 128 **)**|列名|  
|**ORDINAL_POSITION**|**int**|列の識別番号。|  
|**COLUMN_DEFAULT**|**nvarchar(** 4000 **)**|列の既定値です。|  
|**IS_NULLABLE**|**varchar(** 3 **)**|この列は NULL を許可している場合は YES を返します。 それ以外の場合、返しますいいえ。|  
|**DATA_TYPE**|**nvarchar(** 128 **)**|システム提供のデータ型。|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|文字、バイナリ データ、文字データ、またはテキストおよびイメージ データの最大長。<br /><br /> 場合は-1 **xml**と大きな値型のデータ。 それ以外の場合、NULL を返します。 詳細については、「[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)」を参照してください。|  
|**CHARACTER_OCTET_LENGTH**|**int**|バイナリ データ、文字データ、またはテキスト/イメージ データの最大長 (バイト単位)。<br /><br /> 場合は-1 **xml**と大きな値型のデータ。 それ以外の場合、NULL を返します。|  
|**NUMERIC_PRECISION**|**tinyint**|概数データ、真数データ、整数データ、または通貨データの有効桁数。 それ以外の場合、NULL を返します。|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|概数データ、真数データ、整数データ、または通貨データの有効桁数の基数。 それ以外の場合、NULL を返します。|  
|**NUMERIC_SCALE**|**tinyint**|概数データ、真数データ、整数データ、または通貨データの小数点以下桁数。 それ以外の場合、NULL を返します。|  
|**DATETIME_PRECISION**|**smallint**|サブタイプ コード**datetime**と ISO**整数**データ型。 他のデータ型は NULL を返します。|  
|**CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|返します**マスター**します。 これは、データベースの文字セットが配置されている場合は、列が文字データを示しますまたは**テキスト**データ型。 それ以外の場合、NULL を返します。|  
|**CHARACTER_SET_SCHEMA**|**varchar(** 3 **)**|常に NULL が返されます。|  
|**CHARACTER_SET_NAME**|**nvarchar(** 128 **)**|この列が文字データの場合、文字セットの一意の名前を返しますまたは**テキスト**データ型。 それ以外の場合、NULL を返します。|  
|**COLLATION_CATALOG**|**varchar (** 6 **)**|常に NULL が返されます。|  
|**COLLATION_SCHEMA**|**varchar(** 3 **)**|常に NULL が返されます。|  
|**COLLATION_NAME**|**nvarchar(** 128 **)**|列が文字データの場合は、並べ替え順序の一意の名前を返しますまたは**テキスト**データ型。 それ以外の場合、NULL を返します。|  
|**DOMAIN_CATALOG**|**nvarchar(** 128 **)**|列が別名データ型の場合は、この列は、ユーザー定義データ型が作成されたデータベース名にします。 それ以外の場合、NULL を返します。|  
|**DOMAIN_SCHEMA**|**nvarchar(** 128 **)**|列がユーザー定義データ型の場合は、この列は、ユーザー定義データ型を含むスキーマの名前にします。 それ以外の場合、NULL を返します。<br /><br /> <strong>\*\* 重要な\* \*</strong> オブジェクトのスキーマを決定 INFORMATION_SCHEMA ビューを使用しないでください。 オブジェクトのスキーマを調べる唯一の信頼性のある方法は、sys.objects カタログ ビューに対するクエリを実行する方法です。|  
|**ドメイン名**|**nvarchar(** 128 **)**|列がユーザー定義データ型の場合は、この列は、ユーザー定義データ型の名前です。 それ以外の場合、NULL を返します。|  
  
## <a name="see-also"></a>関連項目  
 [システム ビュー &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [情報スキーマ ビュー &#40;TRANSACT-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
