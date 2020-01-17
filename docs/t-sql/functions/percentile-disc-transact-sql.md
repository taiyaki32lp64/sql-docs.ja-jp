---
title: PERCENTILE_DISC (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PERCENTILE_DISC
- PERCENTILE_DISC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PERCENTILE_DISC function
- analytic functions,PERCENTILE_DISC
ms.assetid: b545413d-c4f7-4c8e-8617-607599a26680
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ccd04bec4416fdf5bb5f2137dc2f86e69a9a2ab4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67914342"
---
# <a name="percentiledisc-transact-sql"></a>PERCENTILE_DISC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の行セット全体または行セットの別個のパーティション内で並べ替えられた値の特定の百分位数を計算します。 百分位数が *P* の場合、PERCENTILE_DISC は ORDER BY 句で式の値を並べ替えます。 次に、指定された CUME_DIST 値が最小となる *P* 以上の値を返します (並べ替え仕様は同じ)。たとえば、PERCENTILE_DISC (0.5) は式の 50 番目の百分位数 (つまり、中央値) を計算します。 PERCENTILE_DISC は、列値の離散型分布に基づく百分位数を計算します。 結果は列の特定の値と等しくなります。  
  
 ![記事リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
PERCENTILE_DISC ( numeric_literal ) WITHIN GROUP ( ORDER BY order_by_expression [ ASC | DESC ] )  
    OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>引数  
 *literal*  
 計算する百分位数です。 値は 0.0 ～ 1.0 で指定してください。  
  
 WITHIN GROUP **(** ORDER BY *order_by_expression* [ **ASC** | DESC)**  
 並べ替える値のリストを指定し、百分位数を計算します。 *order_by_expression* は 1 つだけ許可されます。 既定の並べ替え順は昇順です。 値のリストは、並べ替え操作に対して有効な任意のデータ型を指定できます。  
  
 OVER **(** \<partition_by_clause>)**  
 FROM 句の結果セットをパーティションに分割します。 百分位関数がこれらのパーティションに適用されます。 詳細については、[OVER 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)を参照してください。 \<ORDER BY clause> と \<rows or range clause> は PERCENTILE_DISC 関数では指定できません。  
  
## <a name="return-types"></a>戻り値の型  
 戻り値の型は *order_by_expression* の型によって決まります。  
  
## <a name="compatibility-support"></a>互換性サポート  
 互換性レベル 110 以上では、WITHIN GROUP は予約されたキーワードです。 詳細については、「[ALTER DATABASE 互換性レベル &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)」を参照してください。  
  
## <a name="general-remarks"></a>全般的な解説  
 データセット内の NULL はすべて無視されます。  
  
 PERCENTILE_DISC は非決定的です。 詳細については、「 [決定的関数と非決定的関数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="basic-syntax-example"></a>基本構文例  

 次の例では、PERCENTILE_CONT と PERCENTILE_DISC を使用して、各部門の従業員給与の中央値を検索します。 これらは同じ値を返さない可能性があります。
* PERCENTILE_CONT は、データ セットに存在しない場合でも適切な値を返します。
* PERCENTILE_DISC は、実際の設定値を返します。  
  
```  
USE AdventureWorks2012;  
  
SELECT DISTINCT Name AS DepartmentName  
      ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianCont  
      ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianDisc  
FROM HumanResources.Department AS d  
INNER JOIN HumanResources.EmployeeDepartmentHistory AS dh   
    ON dh.DepartmentID = d.DepartmentID  
INNER JOIN HumanResources.EmployeePayHistory AS ph  
    ON ph.BusinessEntityID = dh.BusinessEntityID  
WHERE dh.EndDate IS NULL;  
```  
  
 次に結果セットの一部を示します。  
  
 ```
DepartmentName        MedianCont    MedianDisc
--------------------   ----------   ----------
Document Control       16.8269      16.8269
Engineering            34.375       32.6923
Executive              54.32695     48.5577
Human Resources        17.427850    16.5865
```
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="basic-syntax-example"></a>基本構文例  

 次の例では、PERCENTILE_CONT と PERCENTILE_DISC を使用して、各部門の従業員給与の中央値を検索します。 これらは同じ値を返さない可能性があります。
* PERCENTILE_CONT は、データ セットに存在しない場合でも適切な値を返します。 
* PERCENTILE_DISC は、実際の設定値を返します。  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT DepartmentName  
       ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY BaseRate)  
        OVER (PARTITION BY DepartmentName) AS MedianCont  
       ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY BaseRate)  
        OVER (PARTITION BY DepartmentName) AS MedianDisc  
FROM dbo.DimEmployee;  
  
```  
  
 次に結果セットの一部を示します。  
  
 ```
DepartmentName        MedianCont    MedianDisc  
--------------------   ----------   ----------  
Document Control       16.826900    16.8269  
Engineering            34.375000    32.6923  
Human Resources        17.427850    16.5865  
Shipping and Receiving  9.250000     9.0000
```  
  
## <a name="see-also"></a>参照  
 [PERCENTILE_CONT &#40;Transact-SQL&#41;](../../t-sql/functions/percentile-cont-transact-sql.md)  
  
  


