---
title: ToggleDrillState (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8d027a76a82de3fd82b6c0c81c54ace08167039b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036612"
---
# <a name="toggledrillstate-mdx"></a>ToggleDrillState (MDX)


  ドリル ダウンおよびドリルアップ モードの間でメンバーのドリル状態を切り替えます。  
  
## <a name="syntax"></a>構文  
  
```  
  
ToggleDrillState(Set_Expression1,Set_Expression2 [, [RECURSIVE] [,INCLUDE_CALC_MEMBERS] ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression1*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Set_Expression2*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *再帰*  
 (省略可)。 セットの再帰的な比較を示すキーワードです。 **ToggleDrillState**関数は、の組み合わせ、 **DrillupMember**と**DrilldownMember**関数。 再帰メンバーのときにのみ適用されます、 **DrilldownMember**状態。  
  
 *Include_calc_members*  
 (省略可)。 計算されるメンバーがドリルダウン レベルに存在する場合にそれらを含めるかどうかを示すフラグです。  
  
## <a name="remarks"></a>コメント  
 **ToggleDrillState**関数の最初のセットに存在する 2 番目のセットの各メンバーのドリル状態を切り替えます。 最初のセットは、任意の次元の組を含めることができますが、2 番目のセットが 1 つのディメンションのメンバーを含める必要があります。 **ToggleDrillState**関数は、の組み合わせ、 **DrillupMember**と**DrilldownMember**関数。 場合、メンバー *m*、2 番目のセットが最初のセットに存在して、そのメンバーをドリル ダウン (つまり、直下に子孫が)、`DrillupMember(Set_Expression1, {m})`最初のセット内の組またはメンバーに適用されます。 その場合*m*メンバーがドリル アップ (つまりの子孫がない*m*の直下*m*)、`DrilldownMember(Set_Expression1, {m}[, RECURSIVE])`最初のセットに適用されます。  
  
 場合、省略可能な**再帰**フラグが使用されて、ドリル アップおよびドリル ダウンが再帰的に適用します。 Recursive フラグの詳細については、次を参照してください。、 [DrillupMember](../mdx/drillupmember-mdx.md)と[DrilldownMember](../mdx/drilldownmember-mdx.md)関数。  
  
 XMLA プロパティの MdpropMdxDrillFunctions にクエリを実行、サーバーがドリル関数; が提供するサポートのレベルを確認することができます。参照してください[サポートされる XMLA プロパティ&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)詳細についてはします。  
  
 参照してください[データベース ジャーナル。MDX 設定関数。ToggleDrillState() 関数](https://go.microsoft.com/fwlink/?LinkId=517759)のシナリオと例をこの関数を含むです。  
  
## <a name="example"></a>例  
 次の例をドリル ダウン、先頭のオーストラリア メンバーは、設定、最初のセットの United States メンバーをドリル アップします。  
  
```  
SELECT ToggleDrillState  
   ({[Geography].[Geography].[Country].Members, [Geography].[Geography].[Country].&[United States].Children},  
      {[Geography].[Geography].[Country].[Australia]  
      , [Geography].[Geography].[Country].&[United States]}  
      --, recursive  
      --, include_calc_members  
   ) ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
