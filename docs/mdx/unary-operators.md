---
title: 単項演算子 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9ec9ac3eef28c4deae08d577487599575852c132
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893554"
---
# <a name="unary-operators"></a>単項演算子


  多次元式 (MDX) において、単項演算子は単一のオペランドに対する操作を実行します (たとえば、数値式の負または正の値を返します)。  
  
 MDX では、以下の表に示す単項演算子がサポートされます。  
  
|演算子|説明|  
|--------------|-----------------|  
|[- (負号)](../mdx/negative-mdx.md)|数値式の負の値を返します。|  
|[+ (正号)](../mdx/positive-mdx.md)|数値式の正の値を返します。|  
  
 次の例は、単項演算子を使用してメジャーの負の値を返す方法を示しています。  
  
```  
WITH   
   MEMBER [Measures].[NegDiscountAmount] AS  
   -[Measures].[Discount Amount]  
SELECT   
   {[Measures].[Discount Amount],[Measures].[NegDiscountAmount]} on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
 さらに、MDX では、特別な単項演算子を使用して、 [Rollupchildren](../mdx/rollupchildren-mdx.md)関数によって実行される集計操作を決定します。 これらの特別な単項演算子の詳細については、「[ディメンションへのカスタム集計の追加](https://docs.microsoft.com/analysis-services/multidimensional-models/bi-wizard-add-a-custom-aggregation-to-a-dimension)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [Operators &#40;MDX 構文&#41;](../mdx/operators-mdx-syntax.md)  
  
  
