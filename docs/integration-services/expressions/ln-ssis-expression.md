---
title: LN (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- LN function
- natural logarithm of expression [Integration Services]
ms.assetid: 55d7b657-b5fd-4753-9c81-54ed7575e720
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4bbf59211c35a6048c715594d9c298ba041bcf15
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71289126"
---
# <a name="ln-ssis-expression"></a>LN (SSIS 式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  数値式の自然対数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
LN(numeric_expression)  
```  
  
## <a name="arguments"></a>引数  
 *numeric_expression*  
 0 でなく、かつ負の値でない有効な数値式です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
 この数値式は、対数の計算前に DT_R8 データ型にキャストされます。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
 *numeric_expression* が 0 または負の値に評価される場合、返される結果は NULL になります。  
  
## <a name="expression-examples"></a>式の例  
 この例では、数値リテラルを使用しています。 この関数は、値 3.737766961828337 を返します。  
  
```  
LN(42)  
```  
  
 この例では、列 **Length**を使用しています。 列の値が 53.99 の場合、この関数は 3.9887988442302 を返します。  
  
```  
LN(Length)   
```  
  
 この例では、変数 **Length**を使用しています。 変数は数値データ型である必要があります。または式に、数値データ型への明示的なキャストが含まれている必要があります。 **Length** が 234.567 の場合、関数は 5.45774126708797 を返します。  
  
```  
LN(@Length)   
```  
  
## <a name="see-also"></a>参照  
 [LOG (SSIS 式)](../../integration-services/expressions/log-ssis-expression.md)   
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
