---
title: CONCAT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CONCAT
- CONCAT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT function
ms.assetid: fce5a8d4-283b-4c47-95e5-4946402550d5
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6968766b2d7d447f21fccc6425935017a6943778
ms.sourcegitcommit: a1ddeabe94cd9555f3afdc210aec5728f0315b14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2019
ms.locfileid: "70122956"
---
# <a name="concat-transact-sql"></a>CONCAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

この関数は、連結の結果、またはエンド ツー エンドの方法で 2 つ以上の文字列値の結合の結果の文字列を返します。 (連結時に区切り値を追加するには、「[CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md)」をご覧ください。)
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
CONCAT ( string_value1, string_value2 [, string_valueN ] )  
```  
  
## <a name="arguments"></a>引数  
*string_value*  
他の値に連結する文字列値です。 `CONCAT` 関数では、2 個以上、254 個未満の *string_value*引数が必要です *。*
  
## <a name="return-types"></a>戻り値の型  
*string_value*  
長さと型を入力に依存する文字列値。
  
## <a name="remarks"></a>Remarks  
`CONCAT` は、文字列引数の可変数を取得して、1 つの文字列に連結 (または結合) します。 最小で 2 つの入力値が必要です。それ以外の場合は、`CONCAT` でエラーが発生します。 `CONCAT` は連結する前に、すべての引数を文字列型に暗黙的に変換します。 `CONCAT` は null 値を空の文字列に暗黙的に変換します。 `CONCAT` はすべて **NULL** 値の引数を受け取ると、**varchar**(1) 型の空の文字列を返します。 文字列への暗黙の変換は、データ型変換の既存の規則に従います。 データ型変換の詳細については、「[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)」を参照してください。
  
戻り値の型は、引数の種類によって異なります。 次の表に、マッピングを示します。
  
|入力型|出力型と長さ|  
|---|---|
|1.次の任意の引数<br><br />SQL-CLR システム型<br><br />SQL CLR UDT<br><br />内の複数の<br><br />`nvarchar(max)`|**nvarchar(max)**|  
|2.それ以外の場合、次の型の任意の引数<br><br />**varbinary(max)**<br><br />内の複数の<br><br />**varchar(max)**|**varchar(max)** 。ただし、いずれかのパラメーターが任意の長さの **nvarchar** である場合を除きます。 この場合、`CONCAT` は **nvarchar(max)** 型の結果を返します。|  
|3.それ以外の場合、最大 4,000 文字の **nvarchar** 型の任意の引数<br><br />( **nvarchar**(<= 4000) )|**nvarchar**(<= 4000)|  
|4.その他のすべての場合|**varchar**(<= 8000) (最大 8,000 文字の **varchar**)。ただし、いずれかのパラメーターが任意の長さの nvarchar である場合を除きます。 その場合、`CONCAT` は **nvarchar(max)** 型の結果を返します。|  
  
`CONCAT` が 4000 文字以下の長さの **nvarchar** 入力引数、または 8000 文字以下の長さの **varchar** 入力引数を受け取ると、暗黙的な変換が結果の長さに影響する可能性があります。 他のデータ型は、暗黙的に文字列に変換された場合は異なる長さになります。 たとえば、**int** (14) の文字列の長さは 12 ですが、**float** の長さは 32 です。 そのため、2 つの整数の連結は、24 以上の長さを持つ結果を返します。
  
入力引数がサポートされるラージ オブジェクト (LOB) の型ではない場合、戻り値の型に関係なく、戻り値の型は長さ 8000 文字に切り詰められます。 この切り捨てによりスペースが保持され、効率的なプラン生成をサポートします。
  
CONCAT 関数は、バージョン [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降のリンク サーバーでリモートで実行することができます。 古いバージョンのリンク サーバーでは、リンク サーバーが非連結された値を返した後で、CONCAT 操作がローカルに実行されます。
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-concat"></a>A. CONCAT を使用する  
  
```sql
SELECT CONCAT ( 'Happy ', 'Birthday ', 11, '/', '25' ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
-------------------------  
Happy Birthday 11/25  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-concat-with-null-values"></a>B. NULL 値を持つ CONCAT を使用する  
  
```sql
CREATE TABLE #temp (  
    emp_name nvarchar(200) NOT NULL,  
    emp_middlename nvarchar(200) NULL,  
    emp_lastname nvarchar(200) NOT NULL  
);  
INSERT INTO #temp VALUES( 'Name', NULL, 'Lastname' );  
SELECT CONCAT( emp_name, emp_middlename, emp_lastname ) AS Result  
FROM #temp;  
```  

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
------------------  
NameLastname  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>参照
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)   
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [文字列関数 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  


