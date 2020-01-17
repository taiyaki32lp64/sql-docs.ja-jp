---
title: VAR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- VAR
- VAR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statistical variances
- expressions [SQL Server], statistical variance
- VAR function [Transact-SQL]
ms.assetid: 71dfc339-16c8-42f9-8555-ad45400f7f9b
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9d80c74338ad69cc2ba0fdc0f3cbcf5b452ae4f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927583"
---
# <a name="var-transact-sql"></a>VAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定された式のすべての値の統計的変位を返します。 続くことがあります、 [OVER 句](../../t-sql/queries/select-over-clause-transact-sql.md)です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```    
-- Aggregate Function Syntax   
VAR ( [ ALL | DISTINCT ] expression )  
  
-- Analytic Function Syntax  
VAR ([ ALL ] expression) OVER ( [ partition_by_clause ] order_by_clause)  
```  
  
## <a name="arguments"></a>引数  
 **ALL**  
 すべての値にこの関数を適用します。 ALL が既定値です。  
  
 DISTINCT  
 重複する値は 1 つだけカウントします。  
  
 *式 (expression)*  
 **bit** データ型を除く、真数または概数データ型カテゴリの[式](../../t-sql/language-elements/expressions-transact-sql.md)です。 集計関数とサブクエリは使用できません。  
  
 OVER **(** [ _partition\_by\_clause_ ] _order\_by\_clause_ **)**  
 *partition_by_clause* は、FROM 句で生成された結果セットをパーティションに分割します。このパーティションに関数が適用されます。 指定しない場合、関数ではクエリ結果セットのすべての行を 1 つのグループとして扱います。 _order\_by\_clause_ は、操作が実行される論理的順序を決定します。 _order\_by\_clause_は必須です。 詳細については、「[OVER 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)」を参照してください。  
  
## <a name="return-types"></a>戻り値の型  
 **float**  
  
## <a name="remarks"></a>Remarks  
 SELECT ステートメントのすべてのアイテムで VAR を使用する場合、結果セットの各値は計算に含められます。 VAR は、数値型列に対して使用できます。 NULL 値は無視されます。  
  
 VAR は、OVER 句や ORDER BY 句なしで使用される場合は決定的関数です。 OVER 句や ORDER BY 句と共に使用される場合は、非決定的関数です。 詳細については、「 [決定的関数と非決定的関数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-var"></a>A: VAR を使用する  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースの `SalesPerson` テーブルにあるすべてのボーナス値の分散を返します。  
  
```  
SELECT VAR(Bonus)  
FROM Sales.SalesPerson;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-var"></a>B: VAR を使用する  
 次の例は、テーブル `dbo.FactSalesQuota` の販売ノルマの値の統計的分散を返します。 最初の列にはすべての個別値の分散が含まれ、2 番目の列には重複値を含むすべての値の分散が含まれます。  
  
```  
-- Uses AdventureWorks  
  
SELECT VAR(DISTINCT SalesAmountQuota)AS Distinct_Values, VAR(SalesAmountQuota) AS All_Values  
FROM dbo.FactSalesQuota;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Distinct_Values   All_Values
----------------  ----------------
159180469909.18   158762853821.10
 ```  
  
### <a name="c-using-var-with-over"></a>C. OVER での VAR の使用  
 次の例は、暦年の各四半期に対する販売ノルマの値の統計的分散を返します。 OVER 句の ORDER BY は統計的分散を並べ替え、SELECT ステートメントの ORDER BY は結果セットを並べ替えることに注意してください。  
  
```  
-- Uses AdventureWorks  
  
SELECT CalendarYear AS Year, CalendarQuarter AS Quarter, SalesAmountQuota AS SalesQuota,  
       VAR(SalesAmountQuota) OVER (ORDER BY CalendarYear, CalendarQuarter) AS Variance  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear = 2002  
ORDER BY CalendarQuarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Year  Quarter  SalesQuota              Variance
----  -------  ----------------------  -------------------
2002  1         91000.0000             null
2002  2        140000.0000             1200500000.00
2002  3         70000.0000             1290333333.33
2002  4        154000.0000             1580250000.00
 ```  
  
## <a name="see-also"></a>参照  
 [集計関数 &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [OVER 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  

