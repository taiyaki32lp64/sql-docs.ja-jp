---
title: DrilldownLevelTop (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 461c91d7261b42b5828e2c515a89e8203f40e357
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049267"
---
# <a name="drilldownleveltop-mdx"></a>DrilldownLevelTop (MDX)


  1 レベル下に、指定したレベル、セットの最上位メンバーをドリル ダウンします。  
  
## <a name="syntax"></a>構文  
  
```  
  
DrilldownLevelTop(<Set_Expression>, <Count> [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Count*  
 返す組の数を指定する有効な数値式です。  
  
 *Level_Expression*  
 レベルを返す有効な多次元式 (MDX) 式。  
  
 *Numeric_Expression*  
 有効な数値式は、通常、数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *Include_Calc_Members*  
 ドリルダウン結果に計算されるメンバーを追加するためのキーワードです。  
  
## <a name="remarks"></a>コメント  
 数値式が指定されている場合、 **DrilldownLevelTop**関数、子のセットに対して評価された数値式の値に基づいて指定されたセット内の各メンバーの子の順序を降順で並べ替えますメンバー。 数値式が指定されていない場合、指定されたセット内の各メンバーの子を、クエリ コンテキストから判別した子メンバーのセットが表すセルの値に基づいて、降順で並べ替えます。  
  
 並べ替えの後、 **DrilldownLevelTop**関数が、親メンバーと指定された子メンバーの数を含むセットを返します*数、* 最高値を使用します。  
  
 **DrilldownLevelTop**機能に似ています、 [DrilldownLevel](../mdx/drilldownlevel-mdx.md)関数が、指定されたレベルでは、各メンバーのすべての子ではなく、 **DrilldownLevelTop**関数は、子メンバーの最上位の数を返します。  
  
 XMLA プロパティの MdpropMdxDrillFunctions にクエリを実行、サーバーがドリル関数; が提供するサポートのレベルを確認することができます。参照してください[サポートされる XMLA プロパティ&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)詳細についてはします。  
  
## <a name="examples"></a>使用例  
 次の例を返します、製品カテゴリの上位 3 つの子レベルで既定のメジャーに基づきます。 Adventure Works サンプル キューブでは、[アクセサリ] の上位 3 つの子は、Bike Racks、Bike Stands、Bottles およびケージです。 Management studio で MDX クエリ ウィンドウでは製品に移動することができます |製品カテゴリ |メンバー |すべての製品 |完全な一覧を表示するアクセサリ。 複数のメンバーを返す Count 引数を増やすことができます。  
  
```  
SELECT DrilldownLevelTop   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 次の例を使用して、 **include_calc_members**フラグをドリル ダウン レベルで計算されるメンバーを含めるために使用します。 含まれているメジャー [Reseller Order Count]、 **DrilldownLevelTop**戻り値がそのメジャーで並べ替えられていることを確認するステートメント。  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELTOP(  
  [Product].[Product Categories].children ,  
  2,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
