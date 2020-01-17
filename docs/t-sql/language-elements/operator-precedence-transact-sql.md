---
title: 演算子の優先順位 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], precedence
- operator precedence [Transact-SQL]
- order of operator execution [Transact-SQL]
- precedence [SQL Server], operators
ms.assetid: f04d2439-6fff-4e4c-801f-cc62faef510a
author: rothja
ms.author: jroth
ms.openlocfilehash: 37c1bac44b4dff2be7735f89243b6e273eca0775
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121920"
---
# <a name="operator-precedence-transact-sql"></a>演算子の優先順位 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  複合式に複数の演算子がある場合は、演算子の優先順位によって、操作のシーケンスが決まります。 実行される順序により、結果の値は大きく変わります。  
  
 演算子には、次の表に示す優先順位レベルが定義されています。 優先順位が高い演算子は、優先順位が低い演算子よりも前に評価されます。 次の表では、1 が最も高いレベルで 8 が最も低いレベルです。
  
|Level|オペレーター|  
|-----------|---------------|  
|1|~ (ビットごとの NOT)|  
|2|* (乗算)、/ (除算)、% (剰余)|  
|3|+ (正号)、- (負号)、+ (追加)、+ (連結)、- (減算)、& (ビットごとの AND)、^ (ビットごとの排他的 OR)、&#124; (ビットごとの OR)|  
|4|=、>、\<、>=、<=、<>、!=、!>、!< (比較演算子)|  
|5|NOT|  
|6|AND|  
|7|ALL、ANY、BETWEEN、IN、LIKE、OR、SOME|  
|8|= (代入)|  
  
 式の中の 2 つの演算子が同じ優先順位レベルの場合は、式の中での位置に従って演算子は左から右へと評価されます。 たとえば、次の `SET` ステートメントで使用される式では、減算演算子が加算演算子よりも前に評価されます。  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 4 - 2 + 27;  
-- Evaluates to 2 + 27 which yields an expression result of 29.  
SELECT @MyNumber;  
```  
  
 式の中で演算子の定義済みの優先順位をオーバーライドするには、かっこを使用します。 1 つの値を生成するために、かっこ内のすべてのものが評価されます。 その値は、かっこ外の任意の演算子で使用できます。  
  
 たとえば、次の `SET` ステートメントで使用される式では、乗算演算子の優先順位は加算演算子よりも高くなります。 乗算演算が最初に評価され、式の結果は `13` です。  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * 4 + 5;  
-- Evaluates to 8 + 5 which yields an expression result of 13.  
SELECT @MyNumber;  
```  
  
 次の `SET` ステートメントで使用される式では、かっこにより、加算が先に評価されます。 式の結果は `18` になります。  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * (4 + 5);  
-- Evaluates to 2 * 9 which yields an expression result of 18.  
SELECT @MyNumber;  
```  
  
 式の中でかっこが入れ子になっている場合は、最も深い入れ子になった式が先に評価されます。 次の例ではかっこが入れ子になっており、かっこで囲まれている `5 - 3` という式が最も深い入れ子になっています。 この式の結果は `2` になります。 次に、加算演算子 (`+`) によって、この結果が `4` に加算され、結果は `6` の値になります。 最後に `6` に `2` が乗算され、式の最終的な結果は `12` になります。  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * (4 + (5 - 3) );  
-- Evaluates to 2 * (4 + 2) which then evaluates to 2 * 6, and   
-- yields an expression result of 12.  
SELECT @MyNumber;  
```  
  
## <a name="see-also"></a>参照  
 [論理演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/logical-operators-transact-sql.md)   
 [演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [組み込み関数 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
