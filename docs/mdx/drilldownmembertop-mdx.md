---
title: DrilldownMemberTop (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1ebb3054ab25729ef5d75034dbee1d720f4dd928
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031242"
---
# <a name="drilldownmembertop-mdx"></a>DrilldownMemberTop (MDX)


  2 番目の指定されたセットに存在する、指定されたセット メンバーをドリルダウンするは、結果を制限することを指定したメンバーの設定。 また、この関数をドリル ダウン最初の組階層または必要に応じて指定した階層を使用して、組のセット。  
  
## <a name="syntax"></a>構文  
  
```  
  
DrillDownMemberTop(<Set_Expression1>, <Set_Expression2>, <Count> [,[<Numeric_Expression>] [,[<Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]]])  
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
 数値式が指定されている場合、 **DrilldownMemberTop**関数、子のセットに対して評価された数値式の値に基づいて最初のセット内の各メンバーの子の順序を降順で並べ替えますメンバー。 クエリ コンテキストから判別に、セルの値に基づいて最初のセット内の各メンバーの子の順序を降順で並べ替えますが、子メンバーのセットによって表される数値式が指定されていない場合。 この動作は、並べ替えを行わず、自然な順序でメンバーのセットを返す、TopCount および Head (MDX) 関数に似ています。  
  
 並べ替えの後、 **DrilldownMemberTop**関数が、親メンバーと指定された子メンバーの数を含むセットを返します*数、* 両方のセットに含まれている最も高い値とは.  
  
 場合**再帰**が指定されて、関数は、前述のように最初のセットを並べ替え、再帰的に 2 番目のセットに対して、階層に編成されている最初のセットのメンバーを比較します。 関数が 2 番目のセットに存在することも、最初のセット内の各メンバーの子の最上位の数を取得します。  
  
 最初のセットは、メンバーではなく組を含めることができます。 組のドリル ダウンでは、OLE DB の拡張機能し、メンバーではなく組のセットを返します。  
  
 **DrilldownMemberTop**機能に似ています、 [DrilldownMember](../mdx/drilldownmember-mdx.md)も最初のセット内の各メンバーのすべての子ではなく、 、2番目のセット内に存在しますが、機能**DrilldownMemberTop**関数は、各メンバーの子メンバーの最上位の数を返します。  
  
 XMLA プロパティの MdpropMdxDrillFunctions にクエリを実行、サーバーがドリル関数; が提供するサポートのレベルを確認することができます。参照してください[サポートされる XMLA プロパティ&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)詳細についてはします。  
  
## <a name="example"></a>例  
 次の例にドリル ダウン、衣料のカテゴリに出荷された注文の数量が最も多い衣料の 3 つのサブカテゴリを返します。  
  
```  
SELECT DrilldownMemberTop   ({[Product].[Product Categories].[All Products],        
[Product].[Product Categories].[Category].Bikes,        
[Product].[Product Categories].[Category].Clothing},     
{[Product].[Product Categories].[Category].Clothing},     
3,     
[Measures].[Reseller Order Quantity])     
ON 0     
FROM [Adventure Works]     
WHERE [Measures].[Reseller Order Quantity]  
  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
