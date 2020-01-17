---
title: EXP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EXP_TSQL
- EXP
dev_langs:
- TSQL
helpviewer_keywords:
- exponential functions
- EXP function
ms.assetid: 5a9b8c52-6fb6-4e33-8b02-a878785b2f51
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 638e9960af007710b7c9a891109597db14227092
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071591"
---
# <a name="exp-transact-sql"></a>EXP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定した指数値を返します **float** 式です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
EXP ( float_expression )  
```  
  
## <a name="arguments"></a>引数  
 *float_expression*  
 **float** 型、または暗黙的に **float** 型に変換できる[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。  
  
## <a name="return-types"></a>戻り値の型  
 **float**  
  
## <a name="remarks"></a>Remarks  
 定数 **e** (2.718281…) は、自然対数の底です。  
  
 数値の指数は、定数 **e** をその数値で累乗したものです。 たとえば、EXP(1.0) = e^1.0 = 2.71828182845905 および EXP(10) = e^10 = 22026.4657948067 になります。  
  
 数値の自然対数の指数は、その数値自体になります: EXP (LOG (*n*)) = *n*。 また、数値の指数の自然対数は、その数値自体になります: LOG (EXP (*n*)) = *n*。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-finding-the-exponent-of-a-number"></a>A. 数値の指数を計算する  
 次の例では、変数を宣言し、指定した変数 (`10`) の指数値とテキストの説明を返します。  
  
```  
DECLARE @var float  
SET @var = 10  
SELECT 'The EXP of the variable is: ' + CONVERT(varchar,EXP(@var))  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------------------------------------------------  
The EXP of the variable is: 22026.5  
(1 row(s) affected)  
```  
  
### <a name="b-finding-exponentials-and-natural-logarithms"></a>B. 指数と自然対数を計算する  
 次の例では、`20` の自然対数の指数値と、`20` の指数の自然対数を返します。 これらの関数は互いの逆関数なので、どちらの場合も戻り値は `20` です。  
  
```  
SELECT EXP( LOG(20)), LOG( EXP(20))  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------------------- ----------------------  
20                     20  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-finding-the-exponent-of-a-number"></a>C. 数値の指数を計算する  
 次の例では、指定された値 (`10`) の指数値を返します。  
  
```  
SELECT EXP(10);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------  
22026.4657948067  
```  
  
### <a name="d-finding-exponential-values-and-natural-logarithms"></a>D. 指数値と自然対数を計算する  
 次の例では、`20` の自然対数の指数値と、`20` の指数の自然対数を返します。 これらの関数は互いの逆関数なので、どちらの場合も戻り値は `20` です。  
  
```  
SELECT EXP( LOG(20)), LOG( EXP(20));  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------- -----------------  
20                  20  
```  
  
## <a name="see-also"></a>参照  
 [数学関数 &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [LOG &#40;Transact-SQL&#41;](../../t-sql/functions/log-transact-sql.md)   
 [LOG10 &#40;Transact-SQL&#41;](../../t-sql/functions/log10-transact-sql.md)  
  
  

