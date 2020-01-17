---
title: SELECT @local_variable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- variable_TSQL
- '@loca_variable'
- '@local'
- variable
- '@loca_variable_TSQL'
- '@local_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- variables [SQL Server], assigning
- SELECT statement [SQL Server], @local_variable
- '@local_variable'
- local variables [SQL Server]
ms.assetid: 8e1a9387-2c5d-4e51-a1fd-a2a95f026d6f
author: rothja
ms.author: jroth
monikerRange: = azuresqldb-current ||>= sql-server-2016 ||= azure-sqldw-latest||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 6a274535d53b7eec57fdf257425f855eded5d046
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121781"
---
# <a name="select-localvariable-transact-sql"></a>SELECT @local_variable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  ローカル変数を式の値に設定します。  
  
 変数を割り当てるには、SELECT @*local_variable* ではなく、[SET @local_variable](../../t-sql/language-elements/set-local-variable-transact-sql.md) を使用することをお勧めします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
SELECT { @local_variable { = | += | -= | *= | /= | %= | &= | ^= | |= } expression } 
    [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>引数  
@*local_variable*  
 値を割り当てる宣言された変数です。  
  
{= | += | -= | \*= | /= | %= | &= | ^= | |= }   
右側の値を左側の変数に代入します。  
  
複合代入演算子です。  
  |演算子 (operator) |アクション (action) |   
  |-----|-----|  
  | = | 後続の式を変数に代入します。 |  
  | += | 加算して代入 |   
  | -= | 減算して代入 |  
  | \*= | 乗算して代入 |  
  | /= | 除算して代入 |  
  | %= | 剰余を代入 |  
  | &= | ビットごとの AND 演算を行って代入 |  
  | ^= | ビットごとの XOR 演算を行って代入 |  
  | \|= | ビットごとの OR 演算を行って代入 |  
  
 *式 (expression)*  
 任意の有効な[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。 これには、スカラー サブクエリが含まれます。  
  
## <a name="remarks"></a>Remarks  
 SELECT @*local_variable* は通常、変数に 1 つの値を返すときに使用します。 ただし、*expression* が列名の場合は、複数の値を返すことができます。 SELECT ステートメントが複数の値を返した場合は、最後に返された値が変数に割り当てられます。  
  
 SELECT ステートメントが行を返さない場合、変数は現在の値を保ちます。 *expression* が値を返さないスカラー サブクエリの場合、変数は NULL に設定されます。  
  
 1 つの SELECT ステートメントで複数のローカル変数を初期化できます。  
  
> [!NOTE]  
>  変数の割り当てを含む SELECT ステートメントを、同時に通常の結果セットの取得に使用することはできません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-use-select-localvariable-to-return-a-single-value"></a>A. SELECT @local_variable を使用して値を 1 つ返す  
 次の例では、変数 `@var1` には、その値として `Generic Name` が割り当てられています。 `Store` に指定した値は `CustomerID` テーブル内に存在しないため、このテーブルに対するクエリは行を返しません。 変数の値は `Generic Name` のままです。  
  
```sql  
-- Uses AdventureWorks    
  
DECLARE @var1 varchar(30);         
SELECT @var1 = 'Generic Name';         
SELECT @var1 = Name         
FROM Sales.Store         
WHERE CustomerID = 1000 ;        
SELECT @var1 AS 'Company Name';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 Company Name  
 ------------------------------  
 Generic Name  
 ```  
  
### <a name="b-use-select-localvariable-to-return-null"></a>B. SELECT @local_variable を使用して NULL を返す  
 次の例では、`@var1` に値を割り当てるのにサブクエリを使用しています。 `CustomerID` に要求された値が存在しないため、サブクエリは値を返しません。変数は `NULL` に設定されます。  
  
```sql  
-- Uses AdventureWorks  
  
DECLARE @var1 varchar(30)   
SELECT @var1 = 'Generic Name'   
SELECT @var1 = (SELECT Name   
FROM Sales.Store   
WHERE CustomerID = 1000)   
SELECT @var1 AS 'Company Name' ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Company Name  
----------------------------  
NULL  
```  
  
## <a name="see-also"></a>参照  
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [複合演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  
