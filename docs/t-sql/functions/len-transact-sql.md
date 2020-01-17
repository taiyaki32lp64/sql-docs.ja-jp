---
title: LEN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/03/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- LEN
- LEN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- LEN function
- characters [SQL Server], number of
- number of characters
ms.assetid: fa20fee4-884d-4301-891a-c03e901345ae
author: pmasl
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c7fa3d9db220dcacf425399600166858300489dc
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798416"
---
# <a name="len-transact-sql"></a>LEN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

指定された文字列式の、末尾の空白を除いた文字数を返します。  
  
> [!NOTE]  
> 式の表記に使用されているバイト数を返すには、[DATALENGTH](../../t-sql/functions/datalength-transact-sql.md) 関数を使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
LEN ( string_expression )  
```  
  
## <a name="arguments"></a>引数  
 *string_expression*  
 評価される文字列[式](../../t-sql/language-elements/expressions-transact-sql.md)です。 *string_expression* には、文字データまたはバイナリ データの定数、変数、または列を使用できます。  
  
## <a name="return-types"></a>戻り値の型  
 *式*が **varchar(max)** 、**nvarchar(max)** 、または **varbinary(max)** データ型の場合は **bigint**。それ以外の場合は **int**。  
  
 SC の照合順序を使用する場合、返される整数値では、UTF-16 サロゲート ペアが 1 文字としてカウントされます。 詳細については、「 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。  
  
## <a name="remarks"></a>Remarks  
LEN では末尾の空白が除外されます。 これが問題の場合は、文字列が切り捨てられない [DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md) 関数の使用を検討してください。 Unicode 文字列を処理する場合、DATALENGTH では文字の数と等しくない値が返される場合があります。 次の例では、末尾のスペースを持つ LEN および DATALENGTH を示します。  
  
```sql  
DECLARE @v1 varchar(40),  
    @v2 nvarchar(40);  
SELECT   
@v1 = 'Test of 22 characters ',   
@v2 = 'Test of 22 characters ';  
SELECT LEN(@v1) AS [varchar LEN] , DATALENGTH(@v1) AS [varchar DATALENGTH];  
SELECT LEN(@v2) AS [nvarchar LEN], DATALENGTH(@v2) AS [nvarchar DATALENGTH];  
```  

> [!NOTE]
> [LEN](../../t-sql/functions/len-transact-sql.md) を使用して指定された文字列式のエンコードされた文字数を返す場合、または [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md) を使用して指定された文字列式のサイズをバイト単位で返す場合、その出力は、その列で使用されているデータ型およびエンコードの種類によって異なる場合があります。 異なる種類のエンコードでの記憶域の違いについて詳しくは、「[照合順序と Unicode のサポート](../../relational-databases/collations/collation-and-unicode-support.md)」をご覧ください。

## <a name="examples"></a>使用例  
 次の例では、`FirstName` に居住する人の `Australia` の文字数とデータを選択します。 この例では、AdventureWorks データベースを使用します。  
  
```sql  
SELECT LEN(FirstName) AS Length, FirstName, LastName   
FROM Sales.vIndividualCustomer  
WHERE CountryRegionName = 'Australia';  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 次の例では、列 `FirstName` の文字数と、`Australia` 内の従業員の名と姓を返します。  
  
```sql  
USE AdventureWorks2016  
GO  
SELECT DISTINCT LEN(FirstName) AS FNameLength, FirstName, LastName   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.DimGeography AS g   
    ON e.SalesTerritoryKey = g.SalesTerritoryKey   
WHERE EnglishCountryRegionName = 'Australia';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
FNameLength  FirstName  LastName  
-----------  ---------  ---------------  
4            Lynn       Tsoflias
```  
  
## <a name="see-also"></a>参照  
 [DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [CHARINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/charindex-transact-sql.md)  
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)  
 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)   
 [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [文字列関数 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
  
  
