---
title: エイリアス化
description: SQL Data Warehouse と Parallel Data Warehouse で別名を利用します。
titleSuffix: Azure SQL Data Warehouse
ms.custom: seo-lt-2019
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
ms.assetid: 7b3a5c74-05cf-4385-8ee6-6176d003cb8a
author: shkale-msft
ms.author: shkale
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 3b548dd789bc7e234eb527ffe5766f433a06d77e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244758"
---
# <a name="aliasing-azure-sql-data-warehouse-parallel-data-warehouse"></a>別名 (Azure SQL Data Warehouse、Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  別名を利用すると、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)][!INCLUDE[DWsql](../../includes/dwsql-md.md)] クエリで、テーブルや列の名前の代わりに短くて覚えやすい文字列を一時的に代用できます。 テーブル別名は JOIN クエリで頻繁に使用されます。JOIN 構文では、列を参照するときに完全修飾のオブジェクト名が必要になるためです。  
  
 別名には、オブジェクトの名前付け規則に準拠した 1 つの言葉を指定する必要があります。 詳細については、[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] の "オブジェクトの名前付け規則" を参照してください。 別名には、空のスペースを含めることができません。別名は一重引用符や二重引用符で囲むことができません。  
  
## <a name="syntax"></a>構文  
  
```  
object_source [ AS ] alias  
```  
  
## <a name="arguments"></a>引数  
 *object_source*  
 ソース テーブルまたは列の名前。  
  
 AS  
 省略可能な別名の前置詞。 範囲変数の別名を使用するとき、AS キーワードは禁止されます。  
  
 *alias*  
 テーブルまたは列の目的の一時的な参照名。 あらゆる有効な名前を使用できます。 詳細については、[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] の "オブジェクトの名前付け規則" を参照してください。  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 次の例では、クリエに複数の結合が含まれています。 この例では、テーブルと列の両方の別名を確認できます。  
  
-   列の別名:この例では、列と選択リストに列を含む式の両方に別名が与えられています。 `SalesTerritoryRegion AS SalesTR` では、単純な列の別名を確認できます。 `Sum(SalesAmountQuota) AS TotalSales` では、式の別名を確認できます。  
  
-   テーブル別名: `dbo.DimSalesTerritory AS st` では、`dbo.DimSalesTerritory` テーブルに `st` という別名を作成しています。  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) AS TotalSales, SalesTerritoryRegion AS SalesTR,  
    RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) AS RankResult  
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory AS st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
  
```  
  
 AS キーワードは下の画像のように除外できますが、多くの場合、読みやすくするために除外しません。  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) TotalSales, SalesTerritoryRegion SalesTR,  
RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) RankResult  
FROM dbo.DimEmployee e  
INNER JOIN dbo.FactSalesQuota sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
```  
  
## <a name="see-also"></a>参照  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  
