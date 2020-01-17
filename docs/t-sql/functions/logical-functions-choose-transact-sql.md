---
title: CHOOSE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHOOSE
- CHOOSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHOOSE function
ms.assetid: 1c382c83-7500-4bae-bbdc-c1dbebd3d83f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a96f4e48c56be6558ecb6523ebd687e50d9f82a0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059743"
---
# <a name="logical-functions---choose-transact-sql"></a>論理関数 - CHOOSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の値の一覧から指定されたインデックスにある項目を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
CHOOSE ( index, val_1, val_2 [, val_n ] )  
```  
  
## <a name="arguments"></a>引数  
 *index*  
 後に続く項目のリストへの 1 から始まるインデックスを表す整数式を指定します。  
  
 入力されたインデックス値が **int** 以外の数値データ型である場合、暗黙的に値が整数に変換されます。 インデックス値が値の配列の境界を超えると、CHOOSE は NULL を返します。  
  
 *val_1 ... val_n*  
 任意のデータ型のコンマ区切り値のリスト。  
  
## <a name="return-types"></a>戻り値の型  
 関数に渡される一連の型の中から最も優先順位の高いデータ型を返します。 詳細については、「[データ型の優先順位 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)」を参照してください。  
  
## <a name="remarks"></a>Remarks  
 CHOOSE は、配列へのインデックスと同じように機能します。ここで、配列はインデックス引数の後に続く引数で構成されます。 インデックス引数は、後続の値のうちどの値が返されるのかを決定します。  
  
## <a name="examples"></a>使用例  

### <a name="a-simple-choose-example"></a>A. 単純な CHOOSE の例

 次の例では、入力される値のリストの 3 番目の項目が返されます。  
 
```  
SELECT CHOOSE ( 3, 'Manager', 'Director', 'Developer', 'Tester' ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
-------------  
Developer  
  
(1 row(s) affected)  
```  

### <a name="b-simple-choose-example-based-on-column"></a>B. 列に基づく単純な CHOOSE の例

 次の例では、`ProductCategoryID` 列の値に基づく単純な文字列が返されます。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductCategoryID, CHOOSE (ProductCategoryID, 'A','B','C','D','E') AS Expression1  
FROM Production.ProductCategory;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
ProductCategoryID Expression1  
----------------- -----------  
3                 C  
1                 A  
2                 B  
4                 D  
  
(4 row(s) affected)  
  
```  

### <a name="c-choose-in-combination-with-month"></a>C. MONTH と組み合わせた CHOOSE
  
 次の例では、従業員が採用された季節が返されます。 `HireDate` 列から月の値を返すために MONTH 関数が使用されています。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT JobTitle, HireDate, CHOOSE(MONTH(HireDate),'Winter','Winter', 'Spring','Spring','Spring','Summer','Summer',   
                                                  'Summer','Autumn','Autumn','Autumn','Winter') AS Quarter_Hired  
FROM HumanResources.Employee  
WHERE  YEAR(HireDate) > 2005  
ORDER BY YEAR(HireDate);  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
JobTitle                                           HireDate   Quarter_Hired  
-------------------------------------------------- ---------- -------------  
Sales Representative                               2006-11-01 Autumn  
European Sales Manager                             2006-05-18 Spring  
Sales Representative                               2006-07-01 Summer  
Sales Representative                               2006-07-01 Summer  
Sales Representative                               2007-07-01 Summer  
Pacific Sales Manager                              2007-04-15 Spring  
Sales Representative                               2007-07-01 Summer  
  
```  
  
## <a name="see-also"></a>参照  
 [IIF &#40;Transact-SQL&#41;](../../t-sql/functions/logical-functions-iif-transact-sql.md)  
  
  
