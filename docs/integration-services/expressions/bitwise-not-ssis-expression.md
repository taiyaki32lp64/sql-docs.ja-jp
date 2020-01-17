---
title: ~ (ビット演算 Not) (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: e4413ddd-0d0e-40c3-9c76-b5ce323218ec
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b9ac40997cd2d9962d067d181a66e9614de477d1
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297691"
---
# <a name="-bitwise-not-ssis-expression"></a>~ (ビット演算 Not) (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  整数の否定のビット演算を実行します。 この演算子は、符号付きおよび符号なし整数データ型に適用できます。  
  
## <a name="syntax"></a>構文  
  
```  
  
~integer_expression  
  
```  
  
## <a name="arguments"></a>引数  
 *integer_expression*  
 整数データ型の任意の有効な式を指定します。 *integer*_*expression* は整数で、ビット演算用に 2 進数に変換されます。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="result-types"></a>戻り値の型  
 データ型を返す *integer_expression*です。  
  
## <a name="remarks"></a>Remarks  
 なし  
  
## <a name="expression-examples"></a>式の例  
 この例では、数値 170 (0000 0000 1010 1010) に対し、ビット演算 ~ (NOT) を実行します。 この数値は符号付き整数です。  
  
```  
  
~ 170  
```  
  
 式は -170 (1111111101010101) に評価されます。  
  
 0000000010101010  
  
 ---------------------\-  
  
 1111111101010101  
  
## <a name="see-also"></a>参照  
 [演算子の優先順位と結合規則](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [演算子 &#40;SSIS 式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
