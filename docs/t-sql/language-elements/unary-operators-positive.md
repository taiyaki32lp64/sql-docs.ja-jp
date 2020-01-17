---
title: + (単項プラス) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- + (positive)
- +
- positive
dev_langs:
- TSQL
helpviewer_keywords:
- + (positive operator)
- positive operator (+)
- positive values [SQL Server]
ms.assetid: 0f31c5cc-3078-4f6a-9870-7eb1a98053fb
author: rothja
ms.author: jroth
ms.openlocfilehash: f6c7f0ebb1960c763dead68443ed4ae0c4c397db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086155"
---
# <a name="unary-operators---positive"></a>単項演算子 - 正号
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

数値式の値を返します (単項演算子)。 単項演算子は、数値型に分類されるデータ型の 1 つの式に対してだけ操作を実行します。   
  
|演算子|意味|  
|--------------|-------------|  
|[+ (正号)](../../t-sql/language-elements/unary-operators-positive.md)|数値は正の値です。|  
|[- (負号)](../../t-sql/language-elements/unary-operators-negative.md)|数値は負の値です。|  
|[~ (ビット演算子 NOT)](../../t-sql/language-elements/bitwise-not-transact-sql.md)|値の 1 の補数を返します。|  
  
 \+ (正) 演算子と - (負) 演算子は、数値型カテゴリのいずれかのデータ型の任意の式で使用します。 ~ (ビットごとの NOT) 演算子を使用できるのは、整数型に分類されるデータ型の式だけです。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
+ numeric_expression  
```  
  
## <a name="arguments"></a>引数  
 *numeric_expression*  
 **datetime** および **smalldatetime** データ型を除く、数値データ型カテゴリ内のいずれかのデータ型の有効な[式](../../t-sql/language-elements/expressions-transact-sql.md)です。  
  
## <a name="result-types"></a>戻り値の型  
 データ型を返す *numeric_expression*です。  
  
## <a name="remarks"></a>Remarks  
 単項プラスは任意の数値式の前に付けることができますが、その式が返す値に対して何の操作も行いません。 つまり、負の式の値を正の値にして返すわけではありません。 負の式の値を正の値として返すには、[ABS](../../t-sql/functions/abs-transact-sql.md) 関数を使用します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-setting-a-variable-to-a-positive-value"></a>A. 変数に正の値を設定する  
 次の例では、変数を正の値に設定します。  
  
```  
DECLARE @MyNumber decimal(10,2);  
SET @MyNumber = +123.45;  
SELECT @MyNumber;  
GO  
```  
  
 結果セットは次のようになります。  
  
```  
-----------   
123.45            
  
(1 row(s) affected)  
```  
  
### <a name="b-using-the-unary-plus-operator-with-a-negative-value"></a>B. 単項プラス演算子を負の値と共に使用する  
 次の例では、単項プラス演算子を負の式と共に使用した場合と、同じ式に対して ABS() 関数を使用した場合とを示しています。 単項プラス演算子は式に影響を与えませんが、ABS 関数は式の値を正の値にして返します。  
  
```  
USE tempdb;  
GO  
DECLARE @Num1 int;  
SET @Num1 = -5;  
SELECT +@Num1, ABS(@Num1);  
GO  
```  
  
 結果セットは次のようになります。  
  
```  
----------- -----------  
-5          5  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>参照  
 [データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [演算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [ABS &#40;Transact-SQL&#41;](../../t-sql/functions/abs-transact-sql.md)  
  
  
