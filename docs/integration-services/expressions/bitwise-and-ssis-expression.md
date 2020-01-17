---
title: '&amp; (ビット演算 AND) (SSIS 式) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- AND, bitwise AND
- '& (bitwise AND)'
- bitwise AND (&)
ms.assetid: 06d2958e-66a5-44d8-8bc4-56209ebe1ff2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 295affd0b03368d8156bec8e3b7193f3ce0684ac
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71290313"
---
# <a name="amp-bitwise-and-ssis-expression"></a>&amp; (ビット演算 AND) (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  2 つの整数値の AND 演算をビット単位で実行します。 最初のオペランドの各ビットを 2 番目のオペランドの対応するビットと比較します。 両方のビットが 1 の場合、対応する結果ビットは 1 に設定されます。 それ以外の場合、対応する結果ビットは 0 に設定されます。  
  
 条件はいずれも符号付き整数型であるか、いずれも符号なし整数型である必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
integer_expression1 & integer_expression2  
  
```  
  
## <a name="arguments"></a>引数  
 *integer_expression1、integer_ expression2*  
 符号付きまたは符号なし整数データ型の任意の有効な式です。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="result-types"></a>戻り値の型  
 2 つの引数のデータ型によって決まります。 詳しくは、「 [式における Integration Services データ型](../../integration-services/expressions/integration-services-data-types-in-expressions.md)」をご覧ください。  
  
## <a name="remarks"></a>Remarks  
 条件のいずれかが NULL の場合、式の結果は NULL になります。  
  
## <a name="expression-examples"></a>式の例  
 この例では、列 **NumberA** と **NumberB**の間でビット演算子 AND を実行します。 列**NumberA** には 3 (0000011) が含まれ、列 **NumberB** には 7 (00000111) が含まれています。  
  
```  
NumberA & NumberB  
```  
  
 式は 3 (00000011) に評価されます。  
  
 00000011  
  
 00000111  
  
 ----------\-  
  
 00000011  
  
 この例では、列 **ReorderPoint** と **SafetyStockLevel** の間でビット演算子 AND を実行します。  
  
```  
ReorderPoint & SafetyStockLevel  
```  
  
 **ReorderPoint** が 10 で **SafetyStockLevel** が 8 の場合、式は 8 (00001000) に評価されます。  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00001000  
  
 この例では、2 つの整数間でビット演算子 AND を実行します。  
  
```  
3 & 5   
```  
  
 式は 1 (00000001) に評価されます。  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000001  
  
## <a name="see-also"></a>参照  
 [&& (論理 AND) (SSIS 式)](../../integration-services/expressions/logical-and-ssis-expression.md)   
 [演算子の優先順位と結合規則](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [演算子 &#40;SSIS 式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
