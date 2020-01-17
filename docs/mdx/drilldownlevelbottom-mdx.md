---
title: DrilldownLevelBottom (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 83dc56056e6000a789c8944b38326c23d7632bb7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049284"
---
# <a name="drilldownlevelbottom-mdx"></a>DrilldownLevelBottom (MDX)


  1 レベル下に、指定したレベル、セットの最下位メンバーをドリル ダウンします。  
  
## <a name="syntax"></a>構文  
  
```  
DrilldownLevelBottom(Set_Expression, Count [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Count*  
 返す組の数を指定する有効な数値式です。  
  
 *Level_Expression*  
 レベルを返す有効な多次元式 (MDX) 式。  
  
 *Numeric_Expression*  
 任意。 有効な数値式は、通常、数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *Include_Calc_Members*  
 任意。 計算されるメンバーがドリルダウン結果に追加するキーワードです。  
  
## <a name="remarks"></a>コメント  
 数値式が指定されている場合、 **DrilldownLevelBottom**関数、子メンバーのセットに対して評価された指定の値に基づいて、指定されたセット内の各メンバーの子の順序の昇順で並べ替えます。 数値式が指定されていない場合、指定されたセット内の各メンバーの子を、クエリ コンテキストから判別した子メンバーのセットが表すセルの値に基づいて、昇順で並べ替えます。この動作は、並べ替えを行わずに自然な順序でメンバーのセットを返す、BottomCount および Tail (MDX) 関数に似ています。  
  
 並べ替えの後、 **DrilldownLevelBottom**関数が、親メンバーと指定された子メンバーの数を含むセットを返します*カウント*、最低の値。  
  
 **DrilldownLevelBottom**機能に似ています、 [DrilldownLevel](../mdx/drilldownlevel-mdx.md)関数が、指定されたレベルでは、各メンバーのすべての子ではなく、 **DrilldownLevelBottom**関数は、子メンバーの最下位の数を返します。  
  
 XMLA プロパティの MdpropMdxDrillFunctions にクエリを実行、サーバーがドリル関数; が提供するサポートのレベルを確認することができます。参照してください[サポートされる XMLA プロパティ&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)詳細についてはします。  
  
## <a name="examples"></a>使用例  
 次の例では、既定のメジャーに基づいて Product Category レベルの子を最小のものから 3 つ返します。 Adventure Works サンプル キューブで、[アクセサリ] の下の 3 つの子はタイヤと真空管、Pumps、Panniers です。 Management studio で MDX クエリ ウィンドウでは製品に移動することができます |製品カテゴリ |メンバー |すべての製品 |完全な一覧を表示するアクセサリ。 複数のメンバーを返す Count 引数を増やすことができます。  
  
```  
SELECT DrilldownLevelBottom   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 次の例を使用して、 **include_calc_members**フラグをドリル ダウン レベルで計算されるメンバーを含めるために使用します。 [Reseller Order Count] メジャーが追加、 **DrilldownLevelBottom**ステートメントをそのメジャーによって、結果が並べ替えられていることを確認します。 計算されるメンバーを表示するには、count を 9 以上にする必要があります。  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELBOTTOM(  
  [Product].[Product Categories].children ,  
  9,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
