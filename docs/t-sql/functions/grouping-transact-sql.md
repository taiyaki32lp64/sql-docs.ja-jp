---
title: GROUPING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GROUPING
- GROUPING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- null values [SQL Server], GROUPING function
- grouping columns
- ROLLUP operator
- GROUP BY clause, GROUPING function
- GROUPING function
- CUBE operator
ms.assetid: 4efa3868-1fc4-4626-8fb1-e863cc03e422
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 018d8de6b8e5fd50109b8e55186c88bda058ea2f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2018
ms.locfileid: "47747470"
---
# <a name="grouping-transact-sql"></a>GROUPING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  GROUP BY リストの指定された列式が集計されるかどうかを示します。 GROUPING は、集計される場合に 1、集計されない場合に 0 を結果セットで返します。 GROUPING は、GROUP BY が指定されている場合に、\<SELECT <select> リスト、HAVING 句、および ORDER BY 句でのみ使用できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
GROUPING ( <column_expression> )  
```  
  
## <a name="arguments"></a>引数  
 \<column_expression>  
 [GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md) 句の列が含まれた列または式です。  
  
## <a name="return-types"></a>戻り値の型  
 **tinyint**  
  
## <a name="remarks"></a>Remarks  
 GROUPING を使用して、ROLLUP、CUBE、または GROUPING SETS から返される NULL 値と標準的な NULL 値を区別します。 ROLLUP、CUBE、または GROUPING SETS の演算結果として返される NULL 値は、NULL の特別な用途です。 結果セット内の列のプレースホルダーとして動作し、すべてという意味を持ちます。  
  
## <a name="examples"></a>使用例  
 次の例では、`SalesQuota` をグループ化し、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースの `SaleYTD` 額を集計します。 `GROUPING` 関数は、`SalesQuota` 列に適用されます。  
  
```  
SELECT SalesQuota, SUM(SalesYTD) 'TotalSalesYTD', GROUPING(SalesQuota) AS 'Grouping'  
FROM Sales.SalesPerson  
GROUP BY SalesQuota WITH ROLLUP;  
GO  
```  
  
 結果セットは、`SalesQuota` の下に 2 つの NULL 値を示します。 最初の `NULL` 値は、テーブル内のこの列からの NULL 値で構成されるグループを表します。 2 番目の `NULL` 値は、ROLLUP の演算によって追加された集計行にあります。 集計行は、すべての `SalesQuota` グループについての `TotalSalesYTD` の総量を表し、`Grouping` 列の `1` によって示されます。  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 SalesQuota     TotalSalesYTD       Grouping  
------------   -----------------   --------  
NULL           1533087.5999          0  
250000.00      33461260.59           0  
300000.00      9299677.9445          0  
NULL           44294026.1344         1  

(4 row(s) affected)
```  
  
## <a name="see-also"></a>参照  
 [GROUPING_ID &#40;Transact-SQL&#41;](../../t-sql/functions/grouping-id-transact-sql.md)   
 [GROUP BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md)  
  
  
