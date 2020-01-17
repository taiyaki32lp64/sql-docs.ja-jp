---
title: + (加算) (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- + (add)
- add operator (+)
- adding expressions
ms.assetid: 44df4154-fed5-4e7f-9995-e703a0164f6a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9341cb3647db9e8e7061b1418b169c4ac4d158d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62769628"
---
# <a name="-add-ssis"></a>+ (加算) (SSIS)
  2 つの数値式を加算します。  
  
## <a name="syntax"></a>構文  
  
```  
  
numeric_expression1 + numeric_expression2  
  
```  
  
## <a name="arguments"></a>引数  
 *numeric_expression1、numeric_ expression2*  
 数値データ型の有効な式です。  
  
## <a name="result-types"></a>戻り値の型  
 2 つの引数のデータ型によって決まります。 詳細については、「 [Integration Services Data Types](../data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="remarks"></a>コメント  
 オペランドのいずれかが NULL の場合、結果は NULL になります。  
  
## <a name="expression-examples"></a>式の例  
 この例では、数値リテラルを加算します。  
  
```  
5 + 6.09 + 7.0  
```  
  
 この例では、 **VacationHours** 列と **SickLeaveHours** 列の値を加算します。  
  
```  
VacationHours + SickLeaveHours  
```  
  
 この例では、計算した値を **StandardCost** 列に加算します。 変数 **Profit%** は、名前に % 文字が含まれているため、角かっこで囲む必要があります。 詳細については、「[識別子 (SSIS)](identifiers-ssis.md)」を参照してください。  
  
```  
StandardCost + (StandardCost * @[Profit%])  
```  
  
## <a name="see-also"></a>関連項目  
 [演算子の優先順位と結合規則](operator-precedence-and-associativity.md)   
 [演算子 &#40;SSIS 式&#41;](operators-ssis-expression.md)  
  
  
