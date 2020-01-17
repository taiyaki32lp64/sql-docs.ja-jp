---
title: Mtd (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e604f66e48c8c8bb93ff5fd4abb174449f0fcdd9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088439"
---
# <a name="mtd-mdx"></a>Mtd (MDX)


  時間ディメンションの年 (Year) レベルという制約の中で、指定されたメンバーと同じレベルにある兄弟メンバーのセットを返します。先頭は最初の兄弟、末尾は指定されたメンバーになります。  
  
## <a name="syntax"></a>構文  
  
```  
  
Mtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 メンバー式が指定されていない、既定値は最初の階層の現在のメンバーの種類のレベルを持つ*か月間*型の最初の次元の*時間*メジャー グループ内。  
  
 **Mtd**関数のショートカット関数では、 [PeriodsToDate](../mdx/periodstodate-mdx.md)レベルを基になる属性階層の Type プロパティ設定されている場合に機能*か月間*します。 つまり、`Mtd(Member_Expression)`と等価`PeriodsToDate(Month_Level_Expression,Member_Expression)`します。  
  
## <a name="example"></a>例  
 次の例では、2002 年 7 月 20 日目から年 7 月、月のインターネット販売の運送料の日付を月の合計を返します。  
  
```  
WITH MEMBER Measures.x AS SUM   
   (  
      MTD([Date].[Calendar].[Date].[July 20, 2002])  
     , [Measures].[Internet Freight Cost]  
     )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [合計&#40;MDX&#41;](../mdx/sum-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
