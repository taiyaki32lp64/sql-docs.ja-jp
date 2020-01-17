---
title: SOME | ANY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SOME
- SOME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- scalar values
- comparing scalar with single-column set
- ANY operator
- SOME | ANY keyword
- single-column set of values [SQL Server]
ms.assetid: 1f717ad6-f67b-4980-9397-577ecb0e5789
author: rothja
ms.author: jroth
ms.openlocfilehash: a5b722f37fb6a5e30a50307a5d7828868ecd1fba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072262"
---
# <a name="some--any-transact-sql"></a>SOME | ANY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  スカラー値を単一列で構成される値のセットと比較します。 SOME と ANY は等価です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
scalar_expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }   
     { SOME | ANY } ( subquery )   
```  
  
## <a name="arguments"></a>引数  
 *scalar_expression*  
 任意の有効な[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 有効な比較演算子です。  
  
 SOME | ANY  
 比較を行うことを指定します。  
  
 *subquery*  
 1 列の結果セットを返すサブクエリです。 返される列のデータ型は、*scalar_expression* のデータ型と同じである必要があります。  
  
## <a name="result-types"></a>戻り値の型  
 **Boolean**  
  
## <a name="result-value"></a>結果の値  
 指定された比較が (_scalar_expression_ **,** _x_) の任意の組で **TRUE** の場合、SOME または ANY から TRUE が返されます。ここで、*x* は単一列セットの中の値です。それ以外の場合は、**FALSE** が返されます。  
  
## <a name="remarks"></a>Remarks  
 SOME の場合、*scalar_expression* ではサブクエリによって返される 1 つ以上の値に対し肯定的な比較を行う必要があります。 サブクエリによって返されるすべての値に対し肯定的な比較を行うために *scalar_expression* を必要とするステートメントについては、「[ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md).」を参照してください。 たとえば、*scalar_express* を 2 とすると、サブクエリによって値 2 と 3 が返される場合、*scalar_expression* = SOME (subquery) は TRUE と評価されます。 サブクエリによって値 2 と 3 が返される場合、*scalar_expression* = ALL (subquery) は FALSE と評価されます。これは、サブクエリのいくつかの値 (値 3) が式の条件を満たさないためです。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-running-a-simple-example"></a>A. 簡単な例を実行する  
 次のステートメントでは、簡単なテーブルを作成し、`1` 列に値 `2`、`3`、`4`、`ID` を追加します。  
  
```  
CREATE TABLE T1  
(ID int) ;  
GO  
INSERT T1 VALUES (1) ;  
INSERT T1 VALUES (2) ;  
INSERT T1 VALUES (3) ;  
INSERT T1 VALUES (4) ;  
```  
  
 テーブルには`3` より大きい値があるため、次のクエリは `TRUE` を返します。  
  
```  
IF 3 < SOME (SELECT ID FROM T1)  
PRINT 'TRUE'   
ELSE  
PRINT 'FALSE' ;  
```  
  
 `FALSE` はテーブル内の値の中で最も小さい値ではないため、次のクエリは `3` を返します。  
  
```  
IF 3 < ALL (SELECT ID FROM T1)  
PRINT 'TRUE'   
ELSE  
PRINT 'FALSE' ;  
```  
  
### <a name="b-running-a-practical-example"></a>B. 実用的な例を実行する  
 次の例では、ストアド プロシージャを作成し、`SalesOrderID` データベース内にある指定した `AdventureWorks2012` のすべての部品が、指定した日数で製造できるかどうかを判定します。 この例では、サブクエリを使用して、特定の `DaysToManufacture` のすべての部品に対する `SalesOrderID` の値一覧を作成し、その中に指定した日数よりも大きいものがないかどうか調べます。 返された `DaysToManufacture` のすべての値が指定した数値より小さい場合、条件式は TRUE となり、最初のメッセージが出力されます。  
  
```  
-- Uses AdventureWorks  
  
CREATE PROCEDURE ManyDaysToComplete @OrderID int, @NumberOfDays int  
AS  
IF   
@NumberOfDays < SOME  
   (  
    SELECT DaysToManufacture  
    FROM Sales.SalesOrderDetail  
    JOIN Production.Product   
    ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID   
    WHERE SalesOrderID = @OrderID  
   )  
PRINT 'At least one item for this order can't be manufactured in specified number of days.'  
ELSE   
PRINT 'All items for this order can be manufactured in the specified number of days or less.' ;  
  
```  
  
 このプロシージャをテストするには、`SalesOrderID``49080` を使用してプロシージャを実行します。この注文内容には、必要な日数が `2` 日の部品が 1 つと 0 日の部品が 2 つ含まれています。 最初のステートメントは条件を満たしますが、 2 番目のクエリはそうではありません。  
  
```  
EXECUTE ManyDaysToComplete 49080, 2 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `All items for this order can be manufactured in the specified number of days or less.`  
  
```  
EXECUTE ManyDaysToComplete 49080, 1 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `At least one item for this order can't be manufactured in specified number of days.`  
  
## <a name="see-also"></a>参照  
 [ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [組み込み関数 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [IN &#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
