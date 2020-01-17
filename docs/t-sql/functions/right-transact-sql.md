---
title: RIGHT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RIGHT_TSQL
- RIGHT
dev_langs:
- TSQL
helpviewer_keywords:
- rightmost character of expression
- RIGHT function
- character strings [SQL Server], RIGHT
ms.assetid: 43f1fe1f-aa18-47e3-ba20-e03e32254a6d
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 66627b7b430d15afe73ec823c0af90e2d19d9a39
ms.sourcegitcommit: a1ddeabe94cd9555f3afdc210aec5728f0315b14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2019
ms.locfileid: "70123183"
---
# <a name="right-transact-sql"></a>RIGHT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  文字列の右端から指定された数の文字を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
RIGHT ( character_expression , integer_expression )  
```  
  
## <a name="arguments"></a>引数  
 *character_expression*  
 文字データまたはバイナリ データの[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。 *character_expression* には、定数、変数、または列を使用できます。 *character_expression* には、**text** または **ntext** を除く任意のデータ型 (暗黙的に **varchar** または **nvarchar** に変換できるデータ型) を使用できます。 それ以外の場合は、[CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) 関数を使用して *character_expression* を明示的に変換します。  
  
 *integer_expression*  
 返される *character_expression* の文字数を指定する正の整数です。 *integer_expression* が負の場合、エラーが返されます。 *integer_expression* が **bigint** 型で、値が大きい場合、*character_expression* には **varchar(max)** などのラージ データ型を使用する必要があります。  
  
## <a name="return-types"></a>戻り値の型  
 *character_expression* が非 Unicode 文字データ型の場合は、**varchar** を返します。  
  
 *character_expression* が Unicode 文字データ型の場合は、**nvarchar** を返します。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補助文字 (サロゲート ペア)  
 SC の照合順序を使用する場合、RIGHT 関数では、UTF-16 のサロゲート ペアが 1 文字としてカウントされます。 詳細については、「 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-right-with-a-column"></a>A:列を指定して RIGHT を使用する  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベース内の各担当者の名前の右端から 5 文字が返されます。  
  
```  
SELECT RIGHT(FirstName, 5) AS 'First Name'  
FROM Person.Person  
WHERE BusinessEntityID < 5  
ORDER BY FirstName;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
First Name  
----------  
Ken  
Terri  
berto  
Rob  
  
(4 row(s) affected)  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-right-with-a-column"></a>B. 列を指定して RIGHT を使用する  
 次の例では、`DimEmployee` テーブル内の各姓の右端から 5 文字が返されます。  
  
```  
-- Uses AdventureWorks  
  
SELECT RIGHT(LastName, 5) AS Name  
FROM dbo.DimEmployee  
ORDER BY EmployeeKey;  
```  
  
 次に結果セットの一部を示します。  
  
 ```
Name
-----
lbert
Brown
rello
lters
 ```  
  
### <a name="c-using-right-with-a-character-string"></a>C. 文字列を指定して RIGHT を使用する  
 次の例では、`RIGHT` を使用して `abcdefg` という文字列の右端の 2 文字を返します。  
  
```  
SELECT RIGHT('abcdefg', 2); 
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-------  
fg
```  
  
## <a name="see-also"></a>参照  
 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [文字列関数 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

