---
title: ValidMeasure (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b3bce4baf3dc3499621f67defd40a4579e9cd460
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037955"
---
# <a name="validmeasure-mdx"></a>ValidMeasure (MDX)


  適用できないディメンションをすべてのレベル (または集計できない場合は、既定のメンバー) にすることにより、キューブ内のメジャーの値をとき返します指定された組の結果を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
ValidMeasure(Tuple_Expression)   
```  
  
## <a name="arguments"></a>引数  
 *Tuple_Expression*  
 組を返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 **ValidMeasure**関数が組の値を返します、組が返す属性、メジャーのメジャー グループとは関係がない値を無視します。 属性にメジャーとの間のリレーションシップが存在しない理由は 2 つ考えられます。  
  
-   属性のディメンションには、タプル内のメジャーのメジャー グループとの関係がありません。  
  
-   属性のディメンションには、メジャーのメジャー グループとの関係はありませんが、粒度属性は、キー属性と粒度属性では、タプルでは、属性との直接的なリレーションシップはありません。  
  
 この関数によって指定される動作は既定のサーバー側動作であり、によって制御されます、 **IgnoreUnrelatedDimensions**メジャー グループ オブジェクトのプロパティ。  
  
 指定された組の各属性に粒度が指定されている場合 (つまり、組のメンバーが All メンバーでない場合)、各属性の現在の座標は次のように移動されます。  
  
-   指定された属性メンバーに関連する属性は、現在のメンバーと共存するメンバーに移動されます。  
  
-   指定された属性メンバーに関連する属性は、All メンバー (階層が集計可能でない場合は既定のメンバー) に移動されます。  
  
-   関連しない属性は、(メジャーに基づいて) All メンバーに移動されます。  
  
## <a name="example"></a>例  
 次のクエリでは、ValidMeasure 関数を使用して IgnoreUnrelatedDimensions プロパティの動作をオーバーライドする方法を示します。 Adventure Works キューブの Sales Targets メジャー グループが IgnoreUnrelatedDimensions に設定する場合は False。Date ディメンションに Calendar Quarter 粒度でこのメジャー グループに参加するためつまり Sales Quota メジャーは、既定では、返す Calendar Quarter の下に null (ただし、計算を下の値を割り当てる MDX スクリプトでもあります。月レベルも)。 計算されるメジャーで ValidMeasure 関数を使用すると、Sales Quota メジャーは IgnoreUnrelatedDimensions が True に設定されている場合と同じように動作し、Sales Quota が現在の Calendar Quarter の値を表示するように強制できます。  
  
```  
WITH MEMBER MEASURES.VTEST AS VALIDMEASURE([Measures].[Sales Amount Quota])  
SELECT {[Measures].[Sales Amount Quota], MEASURES.VTEST} ON 0,  
[Date].[Calendar].MEMBERS ON 1  
FROM [Adventure Works]  
```  
  
 同様に、Sales Targets メジャー グループがリレーションシップには Promotion ディメンションとプロモーションに任意の階層の All メンバーの下には null を返します。 ここでも、この動作は、ValidMeasure を使用して変更できます。  
  
 `WITH MEMBER MEASURES.VTEST AS VALIDMEASURE([Measures].[Sales Amount Quota])`  
  
 `SELECT {[Measures].[Sales Amount Quota], MEASURES.VTEST} ON 0,`  
  
 `[Promotion].[Promotions].members ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
