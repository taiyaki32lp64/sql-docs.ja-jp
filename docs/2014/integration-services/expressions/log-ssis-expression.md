---
title: LOG (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- base-10 logarithms
- LOG function
ms.assetid: f7fccace-c178-4e13-bde9-7dc4ef1d98fa
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fde9e5cdaea245fd0b99820a89a4466e2d669fdf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62769068"
---
# <a name="log-ssis-expression"></a>LOG (SSIS 式)
  数値式の常用対数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
LOG(numeric_expression)  
```  
  
## <a name="arguments"></a>引数  
 *numeric_expression*  
 0 以外で負ではない有効な数値式です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_R8  
  
## <a name="remarks"></a>コメント  
 この *数値式* は、対数の計算前に DT_R8 データ型にキャストされます。 詳細については、「 [Integration Services Data Types](../data-flow/integration-services-data-types.md)」を参照してください。  
  
 *numeric_expression* が 0 または負の値に評価される場合、返される結果は NULL になります。  
  
## <a name="expression-examples"></a>式の例  
 この例では、数値リテラルを使用しています。 この関数は、値 1.988291341907488 を返します。  
  
```  
LOG(97.34)  
```  
  
 この例では、列 **Length**を使用しています。 列の値が 101.24 の場合、この関数は 2.005352136486217 を返します。  
  
```  
LOG(Length)   
```  
  
 この例では、変数 **Length**を使用しています。 変数は数値データ型である必要があります。または式に、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 数値データ型への明示的なキャストが含まれている必要があります。 **Length** が 234.567 の場合、関数は 2.370266913465859 を返します。  
  
```  
LOG(@Length)   
```  
  
## <a name="see-also"></a>参照  
 [EXP &#40;SSIS 式&#41;](exp-ssis-expression.md)   
 [LN &#40;SSIS 式&#41;](ln-ssis-expression.md)   
 [関数 (SSIS 式)](functions-ssis-expression.md)  
  
  
