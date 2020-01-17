---
title: sp_datatype_info (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 05/25/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_datatype_info_TSQL
- sp_datatype_info
dev_langs:
- TSQL
helpviewer_keywords:
- sp_datatype_info
ms.assetid: 045f3b5d-6bb7-4748-8b4c-8deb4bc44147
author: stevestein
ms.author: sstein
ms.openlocfilehash: 39e8f688c23cffb1512be1cd1142d38c010668a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108301"
---
# <a name="spdatatypeinfo-transact-sql"></a>sp_datatype_info (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  現在の環境でサポートされるデータ型に関する情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_datatype_info [ [ @data_type = ] data_type ]   
     [ , [ @ODBCVer = ] odbc_version ]   
```  
  
## <a name="arguments"></a>引数  
`[ @data_type = ] data_type` 指定したデータ型のコード番号です。 すべてのデータ型の一覧を表示するには、このパラメーターを省略します。 *data_type*は**int**、既定値は 0。  
  
`[ @ODBCVer = ] odbc_version` 使用される ODBC のバージョンです。 *odbc_version*は**tinyint**、既定値は 2 です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|TYPE_NAME|**sysname**|DBMS に依存するデータを入力します。|  
|DATA_TYPE|**smallint**|このデータ型のすべての列がマップされる ODBC 型のコードです。|  
|PRECISION|**int**|データ ソースでのデータ型の最大有効桁数です。 有効桁数が適用されていないデータ型に NULL が返されます。 PRECISION 列の戻り値は 10 進表記です。|  
|LITERAL_PREFIX|**varchar(** 32 **)**|文字または文字定数の前に使用します。 単一引用符など ( **'** ) の文字型とバイナリ 0 x。|  
|LITERAL_SUFFIX|**varchar(** 32 **)**|文字または文字の定数を終了するために使用します。 単一引用符など ( **'** ) の文字型とバイナリには引用符です。|  
|CREATE_PARAMS|**varchar(** 32 **)**|このデータ型の作成パラメーターの説明です。 たとえば、 **10 進**は"precision, scale"、 **float**が null の場合と**varchar**は"max_length"。|  
|NULLABLE|**smallint**|Null 値許容属性を指定します。<br /><br /> 1 = null 値を許可します。<br /><br /> 0 = は null 値を許可します。|  
|CASE_SENSITIVE|**smallint**|大文字と小文字を区別するかどうかを示します。<br /><br /> 1 = この型のすべての列では、大文字と小文字を区別します (照合の場合)。<br /><br /> 0 = すべて大文字と小文字はこの型の列。|  
|SEARCHABLE|**smallint**|列の型の検索機能を示します。<br /><br /> 1 = 検索できません。<br /><br /> 2 = LIKE で検索できます。<br /><br /> 3 = WHERE で検索できます。<br /><br /> 4 = WHERE または LIKE で検索できます。|  
|UNSIGNED_ATTRIBUTE|**smallint**|データ型の符号を示します。<br /><br /> 1 = データ型が符号なし。<br /><br /> 0 = 符号付きのデータ型。|  
|MONEY|**smallint**|指定します、 **money**データ型。<br /><br /> 1 = **money**データ型。<br /><br /> 0 = なし、 **money**データ型。|  
|AUTO_INCREMENT|**smallint**|自動増分を指定します。<br /><br /> 1 = 自動インクリメントします。<br /><br /> 0 = 自動インクリメントを行いません。<br /><br /> NULL = この属性は適用できません。<br /><br /> アプリケーションは、この属性を持つ列に値を挿入することはできますが、その列の値を更新することはできません。 例外として、**ビット**データ型の場合は、AUTO_INCREMENT は、真数型または概数のデータ型カテゴリに属するデータ型に対してのみ有効です。|  
|LOCAL_TYPE_NAME|**sysname**|データ ソースに依存するデータ型のローカライズされた名前です。 たとえば、DECIMAL はフランス語で DECIMALE になります。 ローカライズされた名前がそのデータ ソースによってサポートされない場合は NULL が返されます。|  
|MINIMUM_SCALE|**smallint**|データ ソースでのデータ型の最小小数点以下桁数です。 データ型の小数点以下桁数が固定されている場合は、MINIMUM_SCALE 列および MAXIMUM_SCALE 列の両方にこの値が入ります。 小数点以下桁数が適用されない場合は NULL が返されます。|  
|MAXIMUM_SCALE|**smallint**|データ ソースでのデータ型の最大小数点以下桁数です。 最大の小数点以下桁数が、データ ソースでは別に定義されず、最大有効桁数と同じであると定義されている場合、この列には PRECISION 列と同じ値が含まれています。|  
|SQL_DATA_TYPE|**smallint**|記述子の TYPE フィールドでの SQL データ型の値です。 この列は、DATA_TYPE 列と同じ以外は、 **datetime**と ANSI**間隔**データ型。 このフィールドは、常に値を返します。|  
|SQL_DATETIME_SUB|**smallint**|**datetime**または ANSI**間隔**SQL_DATA_TYPE の値が SQL_DATETIME または SQL_INTERVAL の場合のサブコードします。 型のデータ型以外**datetime**と ANSI**間隔**、このフィールドは NULL です。|  
|NUM_PREC_RADIX|**int**|Bits または列が保持できる最大数を計算する桁の数字の数。 データ型が概数型である場合、この列に含まれる値は 2 で、複数のビットを示します。 正確な数値型では、この列に値 10 進数字をいくつかを示すために 10 にはが含まれます。 それ以外は、この列は NULL です。 アプリケーションは、基数と精度を組み合わせて、その列が保持できる最大数を計算できます。|  
|INTERVAL_PRECISION|**smallint**|間隔の場合は先頭の有効桁数の値*data_type*は**間隔**null それ以外の場合。|  
|USERTYPE|**smallint**|**usertype** systypes テーブルからの値。|  
  
## <a name="remarks"></a>コメント  
 sp_datatype_info は、odbc SQLGetTypeInfo と同じです。 結果は、まず DATA_TYPE の順序で、次にデータ型が対応する ODBC SQL データ型にどれだけ正確にマップされているのかに基づいて返されます。  
  
## <a name="permissions"></a>アクセス許可  
 public ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例の情報の取得、 **sysname**と**nvarchar**データ型を指定して、 *data_type*の値`-9`します。  
  
```  
USE master;  
GO  
EXEC sp_datatype_info -9;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
