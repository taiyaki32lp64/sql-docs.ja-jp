---
title: 連結演算子 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7298f80a7d3f61b5b00692be8fbc480429487454
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892461"
---
# <a name="concatenation-operators"></a>連結演算子


  連結演算子はプラス記号 (+) です。 複数の文字列を1つの文字列に結合したり、連結したりすることができます。 バイナリ文字列も連結できます。  
  
 製品名と製品の一意の名前を組み合わせる連結演算子の例を次のコードに示します。  
  
```  
WITH MEMBER Measures.ProductName AS   
   Product.Product.CurrentMember.Name + " (" + Product.Product.CurrentMember.UniqueName + ")"  
SELECT   
   {Measures.ProductName} ON COLUMNS,  
   Product.Product.Members ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="language-considerations"></a>言語に関する注意点  
 連結対象の複数の文字列の照合順序が同じである場合、連結結果の文字列は、入力と同じ照合順序になります。 連結で使用される文字列の照合順序が異なる場合、照合順序の優先順位の規則によって、結果として得られる文字列の照合順序が決まります。 詳細については、「[言語および照合順序 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/languages-and-collations-analysis-services)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [MDX 演算子リファレンス&#40;mdx&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operators &#40;MDX 構文&#41;](../mdx/operators-mdx-syntax.md)  
  
  
