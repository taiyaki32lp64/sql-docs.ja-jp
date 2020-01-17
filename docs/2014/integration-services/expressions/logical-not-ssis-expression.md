---
title: '! (論理 Not) (SSIS 式) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logical Not (!)
- '! (logical Not)'
ms.assetid: d5c4d1e1-7be4-4d25-bcd9-5b6ddb53b3b3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bfcd8337105766d91e097d35201d749c86ca840e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62769038"
---
# <a name="-logical-not-ssis-expression"></a>! (論理 Not) (SSIS 式)
  ブール型のオペランドを否定します。  
  
> [!NOTE]  
>  ! 演算子は、他の演算子と組み合わせて使用することはできません。 たとえば、! 演算子と > 演算子を組み合わせて !> 演算子にすることはできません。  
  
## <a name="syntax"></a>構文  
  
```  
  
!boolean_expression  
  
```  
  
## <a name="arguments"></a>引数  
 *boolean_expression*  
 ブール型に評価される任意の有効な式です。 詳細については、「 [Integration Services Data Types](../data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="result-types"></a>戻り値の型  
 DT_BOOL  
  
## <a name="remarks"></a>コメント  
 次の表は、! 指定します。  
  
|元のブール式|! 演算子の適用後 演算子 (operator)|  
|---------------------------------|------------------------------------|  
|TRUE|FALSE|  
|NULL|NULL|  
|FALSE|TRUE|  
  
## <a name="expression-examples"></a>式の例  
 **Color** 列の値が "red" の場合、この例は FALSE に評価されます。  
  
```  
!(Color == "red")  
```  
  
 **MonthNumber** 変数の値が現在の月を示す整数と同じ場合、この例は TRUE に評価されます。 詳細については、「[MONTH &#40;SSIS 式&#41;](month-ssis-expression.md)」および「[GETDATE &#40;SSIS 式&#41;](getdate-ssis-expression.md)」をご覧ください。  
  
```  
!(@MonthNumber != MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>参照  
 [演算子の優先順位と結合規則](operator-precedence-and-associativity.md)   
 [演算子 &#40;SSIS 式&#41;](operators-ssis-expression.md)  
  
  
