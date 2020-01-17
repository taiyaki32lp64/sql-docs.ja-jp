---
title: パラメーター (TRANSACT-SQL) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- PARAMETERS_TSQL
- PARAMETERS
dev_langs:
- TSQL
helpviewer_keywords:
- PARAMETERS view
- INFORMATION_SCHEMA.PARAMETERS view
ms.assetid: 06ded0ca-7d21-4400-864a-b801e855b257
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e6d3880c4be8925e6b85a20af1324537e3977ecc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103283"
---
# <a name="parameters-transact-sql"></a>パラメーター (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  現在のデータベース内の、現在のユーザーがアクセスできるユーザー定義の関数またはストアド プロシージャのパラメーターごとに 1 行のデータを返します。 関数の場合は、戻り値情報の行も返します。  
  
 これらのビューから情報を取得するには、完全修飾名を指定**INFORMATION_SCHEMA** 。_view_name_します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**SPECIFIC_CATALOG**|**nvarchar(** 128 **)**|パラメーターの基になるルーチンのカタログ名。|  
|**SPECIFIC_SCHEMA**|**nvarchar(** 128 **)**|パラメーターの基になるルーチンのスキーマ名。<br /><br /> <strong>\*\* 重要な\* \*</strong> オブジェクトのスキーマを決定 INFORMATION_SCHEMA ビューを使用しないでください。 オブジェクトのスキーマを調べる唯一の信頼性のある方法は、sys.objects カタログ ビューに対するクエリを実行する方法です。|  
|**SPECIFIC_NAME**|**nvarchar(** 128 **)**|パラメーターの基になるルーチンの名前。|  
|**ORDINAL_POSITION**|**int**|1 から始まるパラメーターの序数位置。 関数の戻り値、値は 0 です。|  
|**PARAMETER_MODE**|**nvarchar (** 10 **)**|出力パラメーター、および入力/出力パラメーターの場合は INOUT は、入力パラメーターかどうかを場合に返されます。|  
|**IS_RESULT**|**nvarchar (** 10 **)**|場合は yes、関数では、ルーチンの結果を示します。 それ以外の場合、返しますいいえ。|  
|**AS_LOCATOR**|**nvarchar (** 10 **)**|ロケーターとして宣言されている場合は YES を返します。 それ以外の場合、返しますいいえ。|  
|**PARAMETER_NAME**|**nvarchar(** 128 **)**|パラメーターの名前。 関数の戻り値に対応する場合は NULL です。|  
|**DATA_TYPE**|**nvarchar(** 128 **)**|システム提供のデータ型。|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|バイナリまたは文字のデータ型の文字の最大長です。<br /><br /> 場合は-1 **xml**と大きな値型のデータ。 それ以外の場合、NULL を返します。|  
|**CHARACTER_OCTET_LENGTH**|**int**|バイナリ型または文字型の最大バイト数。<br /><br /> 場合は-1 **xml**と大きな値型のデータ。 それ以外の場合、NULL を返します。|  
|**COLLATION_CATALOG**|**nvarchar(** 128 **)**|常に NULL が返されます。|  
|**COLLATION_SCHEMA**|**nvarchar(** 128 **)**|常に NULL が返されます。|  
|**COLLATION_NAME**|**nvarchar(** 128 **)**|パラメーターの照合順序の名前。 存在しない場合、文字型の 1 つは NULL を返します。|  
|**CHARACTER_SET_CATALOG**|**nvarchar(** 128 **)**|パラメーターの文字セットのカタログ名。 存在しない場合、文字型の 1 つは NULL を返します。|  
|**CHARACTER_SET_SCHEMA**|**nvarchar(** 128 **)**|常に NULL が返されます。|  
|**CHARACTER_SET_NAME**|**nvarchar(** 128 **)**|パラメーターの文字セットの名前。 存在しない場合、文字型の 1 つは NULL を返します。|  
|**NUMERIC_PRECISION**|**tinyint**|概数データ、真数データ、整数データ、または通貨データの有効桁数。 それ以外の場合、NULL を返します。|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|概数データ、真数データ、整数データ、または通貨データの有効桁数の基数。 それ以外の場合、NULL を返します。|  
|**NUMERIC_SCALE**|**tinyint**|概数データ、真数データ、整数データ、または通貨データの小数点以下桁数。 それ以外の場合、NULL を返します。|  
|**DATETIME_PRECISION**|**smallint**|パラメーターの型がある場合の秒の小数部の有効桁数**datetime**または**smalldatetime**します。 それ以外の場合、NULL を返します。|  
|**INTERVAL_TYPE**|**nvarchar (** 30 **)**|NULL: 将来使用するために予約されています。|  
|**INTERVAL_PRECISION**|**smallint**|NULL: 将来使用するために予約されています。|  
|**USER_DEFINED_TYPE_CATALOG**|**nvarchar(** 128 **)**|NULL: 将来使用するために予約されています。|  
|**USER_DEFINED_TYPE_SCHEMA**|**nvarchar(** 128 **)**|NULL: 将来使用するために予約されています。|  
|**USER_DEFINED_TYPE_NAME**|**nvarchar(** 128 **)**|NULL: 将来使用するために予約されています。|  
|**SCOPE_CATALOG**|**nvarchar(** 128 **)**|NULL: 将来使用するために予約されています。|  
|**SCOPE_SCHEMA**|**nvarchar(** 128 **)**|NULL: 将来使用するために予約されています。|  
|**SCOPE_NAME**|**nvarchar(** 128 **)**|NULL: 将来使用するために予約されています。|  
  
## <a name="see-also"></a>関連項目  
 [システム ビュー &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [情報スキーマ ビュー &#40;TRANSACT-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  
