---
title: DrilldownMemberBottom (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 79bea49705c4f2fb66b8c9866be335433cbb783f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049259"
---
# <a name="drilldownmemberbottom-mdx"></a>DrilldownMemberBottom (MDX)


  2 番目の指定されたセットに存在する、指定されたセット メンバーをドリルダウンするは、結果を制限することを指定したメンバーの設定。 または、この関数をドリル ダウン組のセットを最初の組階層または必要に応じて指定した階層を使用しています。  
  
## <a name="syntax"></a>構文  
  
```  
  
DrillDownMemberBottom(<Set_Expression1>, <Set_Expression2>, <Count> [,[<Numeric_Expresion>] [,[<Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression1*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Set_Expression2*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Count*  
 返す組の数を指定する有効な数値式です。  
  
 *Numeric_Expression*  
 有効な数値式は、通常、数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *Hierarchy*  
 階層を返す有効な多次元式 (MDX) 式。  
  
 *再帰*  
 セットの再帰的な比較を示すキーワードです。  
  
 *Include_Calc_Members*  
 計算されるメンバーがドリルダウン結果に含まれるようにするキーワード。  
  
## <a name="remarks"></a>コメント  
 数値式が指定されている場合、 **DrilldownMemberBottom**関数、子のセットに対して評価された数値式の値に基づいて、最初のセット内の各メンバーの子の順序の昇順で並べ替えますメンバー。 クエリ コンテキストから判別に、セルの値に基づいて最初のセット内の各メンバーの子の順序の昇順で並べ替えますが、子メンバーのセットによって表される数値式が指定されていない場合。 この動作は、並べ替えを行わず、自然な順序でメンバーのセットを返す、BottomCount および Tail (MDX) 関数に似ています。  
  
 並べ替えの後、 **DrilldownMemberBottom**関数が、親メンバーと指定された子メンバーの数を含むセットを返します*数、* 両方に含まれる最小値とは設定します。  
  
 場合**再帰**が指定されて、関数は、前述のように最初のセットを並べ替え、再帰的に 2 番目のセットに対して、階層に編成されている最初のセットのメンバーを比較します。 この関数は、最初のセットのメンバーのうち、2 番目のセット内にも存在する各メンバーの子を、最小のものから指定されている数だけ取得します。  
  
 最初のセットは、メンバーではなく組を含めることができます。 組のドリル ダウンでは、OLE DB の拡張機能し、メンバーではなく組のセットを返します。  
  
 **DrilldownMemberBottom**機能に似ています、 [DrilldownMember](../mdx/drilldownmember-mdx.md)も最初のセット内の各メンバーのすべての子ではなく、 、2番目のセット内に存在しますが、機能**DrilldownMemberBottom**関数は、最下位の子メンバーの各メンバーの数を返します。  
  
 XMLA プロパティの MdpropMdxDrillFunctions にクエリを実行、サーバーがドリル関数; が提供するサポートのレベルを確認することができます。参照してください[サポートされる XMLA プロパティ&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)詳細についてはします。  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
