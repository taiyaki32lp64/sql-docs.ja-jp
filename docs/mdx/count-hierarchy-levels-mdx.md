---
title: Count (階層レベル) (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 17fe804de8bf2c20581ca5c00bee3a28dbce4d55
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045207"
---
# <a name="count-hierarchy-levels-mdx"></a>Count (階層レベル) (MDX)


  階層内のレベル数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Hierarchy_Expression.Levels.Count  
```  
  
## <a name="arguments"></a>引数  
 *Hierarchy_Expression*  
 階層を返す有効な多次元式 (MDX) 式。  
  
## <a name="remarks"></a>コメント  
 階層内のレベル数を返します。`[All]` レベルがある場合はこれも含みます。  
  
> [!IMPORTANT]  
>  表示可能な階層がディメンション内に 1 つしかない場合は、ディメンション名がその 1 つしかない階層に解決されるため、その階層はディメンション名でも階層名でも参照できます。 たとえば、`Measures.Levels.Count`有効な MDX 式は、Measures ディメンション内の唯一の階層に解決されるためです。  
  
## <a name="example"></a>例  
 次の例では、Adventure Works キューブ内の Product Categories ユーザー定義階層のレベルの数を返します。  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Product Categories].Levels.Count   
Select Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [カウント&#40;ディメンション&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [カウント&#40;タプル&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [Count &#40;Set&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
