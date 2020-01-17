---
title: ^ (ビット演算排他的 OR) (SSIS 式)| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- ^ (bitwise exclusive OR operator)
- bitwise exclusive OR (^)
ms.assetid: 6ac53cab-29c4-4835-9f87-371b058b2f38
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3b5153a210c1d276b481cea240e1f28b77751ad4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62769508"
---
# <a name="-bitwise-exclusive-or-ssis-expression"></a>^ (ビット演算排他的 OR) (SSIS 式)
  2 つの整数値の排他的 OR 演算をビット単位で実行します。 最初のオペランドの各ビットを 2 番目のオペランドの対応するビットと比較します。 一方のビットが 0 でもう一方のビットが 1 の場合、対応する結果ビットは 1 に設定されます。 両方のビットが 0、また両方のビットが 1 の場合、対応する結果ビットは 0 に設定されます。  
  
 どちらの条件も符号付き整数データ型か、または、どちらの条件も符号なし整数データ型である必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
integer_expression1 ^ integer_expression2  
  
```  
  
## <a name="arguments"></a>引数  
 *integer_expression1、integer_ expression2*  
 符号付きまたは符号なし整数データ型の任意の有効な式です。 詳細については、「 [Integration Services Data Types](../data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="result-types"></a>戻り値の型  
 2 つの引数のデータ型によって決まります。 詳しくは、「 [式における Integration Services データ型](integration-services-data-types-in-expressions.md)」をご覧ください。  
  
## <a name="remarks"></a>コメント  
 条件のいずれかが NULL の場合、式の結果は NULL になります。  
  
## <a name="expression-examples"></a>式の例  
 この例では、変数 **NumberA** と **NumberB**間の排他的 OR 演算をビット単位で実行します。 **NumberA** には 3 (00000011) が、 **NumberB** には 7 (00000111) が含まれます。  
  
```  
@NumberA ^ @NumberB  
```  
  
 式は 4 (00000100) に評価されます。  
  
 00000011  
  
 00000111  
  
 ----------\-  
  
 00000100  
  
 この例では、 **ReorderPoint** 列と **SafetyStockLevel** 列の間の排他的 OR 演算をビット単位で実行します。  
  
```  
ReorderPoint ^ SafetyStockLevel  
```  
  
 **ReorderPoint** が 10 で **SafetyStockLevel** が 8 の場合、式は 2 (00000010) に評価されます。  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00000010  
  
 この例では、2 つの整数間の排他的 OR 演算をビット単位で実行します。  
  
```  
3 ^ 5   
```  
  
 式は 6 (00000110) に評価されます。  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000110  
  
## <a name="see-also"></a>参照  
 [&#124;&#124; (論理 OR) (SSIS 式)](logical-or-ssis-expression.md)   
 [&#124; (ビット演算包含的 OR) (SSIS 式)](bitwise-inclusive-or-ssis-expression.md)   
 [演算子の優先順位と結合規則](operator-precedence-and-associativity.md)   
 [演算子 &#40;SSIS 式&#41;](operators-ssis-expression.md)  
  
  
