---
title: (コメント)(MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6eb4b54df98cfbf297e6347dac336aa7405d1347
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006290"
---
# <a name="comment-mdx-double-slash"></a>MDX 二重スラッシュのコメント


  ユーザーが入力したテキストを示します。  
  
## <a name="syntax"></a>構文  
  
```  
  
// Comment_Text   
```  
  
#### <a name="parameters"></a>パラメーター  
 *Comment_Text*  
 コメントのテキストを含む文字列です。  
  
## <a name="remarks"></a>コメント  
 コメントは、個別の行に挿入された、多次元式 (MDX) スクリプトの行の末尾で入れ子にまたは MDX ステートメント内で入れ子になったことができます。 サーバーはコメントを評価しません。  
  
 単一行のみのコメントには、// を使用します。 // を使用して挿入するコメントは、改行文字で区切ります。  
  
 コメントの長さには制限がありません。  
  
## <a name="examples"></a>使用例  
 次の例では、この演算子の使用を示します。  
  
```  
// This member returns the gross profit margin for product types  
// and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
      [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM // Select from the Adventure Works cube.  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>関連項目  
 [コメント &#40;MDX&#41;](../mdx/comment-mdx.md)   
 [-- &#40;コメント&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)   
 [MDX 演算子リファレンス&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
