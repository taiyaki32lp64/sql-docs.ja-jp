---
title: 複合演算子 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators
- compound operators, described
ms.assetid: 5072fe91-02d3-42a7-831f-756eff714a17
author: rothja
ms.author: jroth
ms.openlocfilehash: e81ef89165b3af5af0f8c48ca0338086c5c934a9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929537"
---
# <a name="compound-operators-transact-sql"></a>複合演算子 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  複合演算子では、いくつかの演算を実行し、元の値に演算の結果を設定します。 たとえば、変数 @x が 35 である場合、@x += 2 は @x の元の値を取得し、2 を加算して、@x にその新しい値 (37) を設定します。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] には、次の複合演算子があります。  
  
|演算子|詳細情報へのリンク|操作|  
|--------------|------------------------------|------------|  
|+=|[+= &#40;加算代入&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/add-equals-transact-sql.md)|いくつかの数値を元の値に加算し、元の値に結果を設定します。|  
|-=|[-= &#40;減算代入&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/subtract-equals-transact-sql.md)|いくつかの数値を元の値から減算し、元の値に結果を設定します。|  
|*=|[&#42;= &#40;乗算代入&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/multiply-equals-transact-sql.md)|1 つの数値で乗算し、元の値に結果を設定します。|  
|/=|[&#40;除算代入&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)|1 つの数値で除算し、元の値に結果を設定します。|  
|%=|[剰余代入 &#40;Transact-SQL&#41;](../../t-sql/language-elements/modulo-equals-transact-sql.md)|1 つの数値で除算し、元の値に剰余を設定します。|  
|&=|[&= &#40;ビットごとの AND 代入&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)|ビットごとの AND 演算を実行し、元の値に結果を設定します。|  
|^=|[^= &#40;ビットごとの排他的 OR 代入&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)|ビットごとの排他的 OR 演算を実行し、元の値に結果を設定します。|  
|&#124;=|[&#124;= &#40;ビットごとの OR 代入&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)|ビットごとの OR 演算を実行し、元の値に結果を設定します。|  
  
## <a name="syntax"></a>構文  
  
```  
  
expression operator expression  
```  
  
## <a name="arguments"></a>引数  
 *式 (expression)*  
 任意の数値型に分類されるデータ型を持つ有効な[式](../../t-sql/language-elements/expressions-transact-sql.md)です。  
  
## <a name="result-types"></a>戻り値の型  
 優先順位が高い引数のデータ型を返します。 詳細については、「[データ型の優先順位 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)」を参照してください。  
  
## <a name="remarks"></a>Remarks  
 詳細については、それぞれの演算子に関するトピックを参照してください。  
  
## <a name="examples"></a>使用例  
 複合演算の例を次に示します。  
  
```  
DECLARE @x1 int = 27;  
SET @x1 += 2 ;  
SELECT @x1 AS Added_2;  
  
DECLARE @x2 int = 27;  
SET @x2 -= 2 ;  
SELECT @x2 AS Subtracted_2;  
  
DECLARE @x3 int = 27;  
SET @x3 *= 2 ;  
SELECT @x3 AS Multiplied_by_2;  
  
DECLARE @x4 int = 27;  
SET @x4 /= 2 ;  
SELECT @x4 AS Divided_by_2;  
  
DECLARE @x5 int = 27;  
SET @x5 %= 2 ;  
SELECT @x5 AS Modulo_of_27_divided_by_2;  
  
DECLARE @x6 int = 9;  
SET @x6 &= 13 ;  
SELECT @x6 AS Bitwise_AND;  
  
DECLARE @x7 int = 27;  
SET @x7 ^= 2 ;  
SELECT @x7 AS Bitwise_Exclusive_OR;  
  
DECLARE @x8 int = 27;  
SET @x8 |= 2 ;  
SELECT @x8 AS Bitwise_OR;  
  
```  
  
## <a name="see-also"></a>参照  
 [演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [ビットごとの演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  
