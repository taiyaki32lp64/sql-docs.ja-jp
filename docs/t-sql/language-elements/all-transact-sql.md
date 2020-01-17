---
title: ALL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALL_TSQL
- ALL
dev_langs:
- TSQL
helpviewer_keywords:
- single-column set of values [SQL Server]
- ALL (Transact-SQL)
ms.assetid: 4b0c002e-1ffd-4425-a980-11fdc1f24af7
author: rothja
ms.author: jroth
ms.openlocfilehash: bf40ce38bf96ae4d31c9102290e74d5db2230240
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927383"
---
# <a name="all-transact-sql"></a>ALL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  スカラー値を単一列で構成される値のセットと比較します。  
  
 ![記事のリンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "記事のリンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
scalar_expression { = | <> | != | > | >= | !> | < | <= | !< } ALL ( subquery )  
```  
  
## <a name="arguments"></a>引数  
 *scalar_expression*  
 任意の有効な[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 比較演算子です。  
  
 *subquery*  
 1 列の結果セットを返すサブクエリです。 返される列のデータ型は、*scalar_expression* のデータ型と同じである必要があります。  
  
 制限された SELECT ステートメントです。ORDER BY 句および INTO キーワードは使用できません。  
  
## <a name="result-types"></a>戻り値の型  
 **Boolean**  
  
## <a name="result-value"></a>結果の値  
 指定された比較が (_scalar_expression_ **,** _x)_ の任意の組で TRUE の場合、TRUE を返します。ここで、*x* は単一列セットの中の値です。 それ以外の場合は、FALSE を返します。  
  
## <a name="remarks"></a>Remarks  
 ALL の場合、*scalar_expression* ではサブクエリによって返されるすべての値に対し肯定的な比較を行う必要があります。 たとえば、サブクエリによって値 2 と 3 が返される場合、*scalar_expression* <= ALL (subquery) は、*scalar_expression* が 2 の場合、TRUE と評価されます。 サブクエリによって値 2 と値 3 が返される場合、*scalar_expression* = ALL (subquery) は FALSE と評価されます。これは、サブクエリのいくつかの値 (値 3) が式の条件を満たさないためです。  
  
 サブクエリによって返される 1 つの値に対し肯定的な比較を行うために *scalar_expression* を必要とするステートメントについては、「[SOME &#124; ANY &#40;Transact-SQL&#41;](../../t-sql/language-elements/some-any-transact-sql.md)」を参照してください。  
  
 この記事では、ALL をサブクエリと共に使用する場合を想定しています。 ALL は [UNION](../../t-sql/language-elements/set-operators-union-transact-sql.md) および [SELECT](../../t-sql/queries/select-transact-sql.md) と共に使用できます。  
  
## <a name="examples"></a>使用例  
 次の例では、ストアド プロシージャを作成し、`SalesOrderID` データベース内にある指定した [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] のすべての部品が、指定した日数で製造できるかどうかを判定します。 この例では、サブクエリを使用して、特定の `SalesOrderID` のすべての部品に対する `DaysToManufacture` の値一覧を作成し、その中のすべての `DaysToManufacture` が指定した日数以内であることを確認します。  
  
```  
-- Uses AdventureWorks  
  
CREATE PROCEDURE DaysToBuild @OrderID int, @NumberOfDays int  
AS  
IF   
@NumberOfDays >= ALL  
   (  
    SELECT DaysToManufacture  
    FROM Sales.SalesOrderDetail  
    JOIN Production.Product   
    ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID   
    WHERE SalesOrderID = @OrderID  
   )  
PRINT 'All items for this order can be manufactured in specified number of days or less.'  
ELSE   
PRINT 'Some items for this order can''t be manufactured in specified number of days or less.' ;  
  
```  
  
 このプロシージャをテストするには、`SalesOrderID 49080` を使用してプロシージャを実行します。この注文内容には、必要な日数が `2` 日の部品が 1 つと 0 日の部品が 2 つが含まれています。 次に示す最初のステートメントは条件を満たします。 2 番目のクエリはそうではありません。  
  
```  
EXECUTE DaysToBuild 49080, 2 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `All items for this order can be manufactured in specified number of days or less.`  
  
```  
EXECUTE DaysToBuild 49080, 1 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Some items for this order can't be manufactured in specified number of days or less.`  
  
## <a name="see-also"></a>参照  
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [組み込み関数 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [IN &#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
