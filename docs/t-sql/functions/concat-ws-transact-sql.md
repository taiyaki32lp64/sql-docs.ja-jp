---
title: CONCAT_WS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/25/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- CONCAT_WS
- CONCAT_WS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT_WS function
ms.assetid: f1375fd7-a2fd-48bf-922a-4f778f0deb1f
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fcdbb300bbc9209f284cd5a92d192a219f79052d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075334"
---
# <a name="concatws-transact-sql"></a>CONCAT_WS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-asdw-xxx-md.md)]

この関数は、連結の結果、またはエンド ツー エンドの方法で 2 つ以上の文字列値の結合の結果の文字列を返します。 これらの連結文字列値を、最初の関数の引数に指定された区切り記号で区切ります。 (`CONCAT_WS` は "*区切りを使用した連結*" を示します。)

##  <a name="syntax"></a>構文   
```sql
CONCAT_WS ( separator, argument1, argument2 [, argumentN]... )
```

## <a name="arguments"></a>引数   
separator  
任意の文字型の式です (`char`、`nchar`、`nvarchar`、または `varchar`)。

argument1, argument2, argument*N*  
任意のデータ型の式。

## <a name="return-types"></a>戻り値の型
長さと型を入力に依存する文字列値。

## <a name="remarks"></a>Remarks   
`CONCAT_WS` は、文字列引数の可変数を取得して、1 つの文字列に連結 (または結合) します。 これらの連結文字列値を、最初の関数の引数に指定された区切り記号で区切ります。 `CONCAT_WS` には、separator 引数と、他の 2 つの文字列値引数の最小値が必要です。指定しないと、`CONCAT_WS` でエラーが発生します。 `CONCAT_WS` は連結する前に、すべての引数を文字列型に暗黙的に変換します。 

文字列への暗黙の変換は、データ型変換の既存の規則に従います。 動作とデータ型変換の詳細について、「[CONCAT (Transact-SQL)](../../t-sql/functions/concat-transact-sql.md)」を参照してください。

### <a name="treatment-of-null-values"></a>NULL 値の処理方法

`CONCAT_WS` は `SET CONCAT_NULL_YIELDS_NULL {ON|OFF}` 設定を無視します。

`CONCAT_WS` はすべて NULL 値の引数を受け取ると、varchar(1) 型の空の文字列を返します。

`CONCAT_WS` は連結時に null 値を無視し、null 値間に区切りを追加しません。 そのため、`CONCAT_WS` は値が空の文字列、たとえば 2 つ目のアドレス フィールドの連結を適切に処理できます。 詳細については、例 B を参照してください。

区切り記号で区切られた null 値があるシナリオの場合は、`ISNULL` 関数の使用を検討してください。 詳細については、例 C を参照してください。

## <a name="examples"></a>使用例   

### <a name="a--concatenating-values-with-separator"></a>A.  区切りで値を連結する
この例では、値を `-` で区切って、sys.databases テーブルの 3 つの列を連結します。   

```sql
SELECT CONCAT_WS( ' - ', database_id, recovery_model_desc, containment_desc) AS DatabaseInfo
FROM sys.databases;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

|DatabaseInfo |  
|---------|
|1 - SIMPLE - NONE |
|2 - SIMPLE - NONE |
|3 - FULL - NONE |
|4 - SIMPLE - NONE |


### <a name="b--skipping-null-values"></a>B.  Null 値をスキップする
この例では、引数リスト内の `NULL` 値は無視されます。

```sql
SELECT CONCAT_WS(',','1 Microsoft Way', NULL, NULL, 'Redmond', 'WA', 98052) AS Address;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
Address
------------   
1 Microsoft Way,Redmond,WA,98052
```

### <a name="c--generating-csv-file-from-table"></a>C.  テーブルから CSV ファイルを生成する
この例では、区切り値としてコンマ `,` を使用し、復帰文字 `char(13)` を追加して、結果セットの列区切り値形式にします。

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, recovery_model_desc, containment_desc), char(13)) AS DatabaseInfo
FROM sys.databases
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
DatabaseInfo
------------   
1,SIMPLE,NONE
2,SIMPLE,NONE
3,FULL,NONE 
4,SIMPLE,NONE 
```

CONCAT_WS は、列の NULL 値を無視します。 `ISNULL` 関数を使用して null 許容の列をラップし、既定値を指定します。 詳細については、次の例を参照してください。

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, ISNULL(recovery_model_desc,''), ISNULL(containment_desc,'N/A')), char(13)) AS DatabaseInfo
FROM sys.databases;
```

## <a name="see-also"></a>参照
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [文字列関数 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  

