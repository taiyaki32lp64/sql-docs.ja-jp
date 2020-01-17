---
title: Order (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d540b299fd08aa78576b19040a4cfafb9046ae7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055680"
---
# <a name="order-mdx"></a>Order (MDX)


  保持したり、階層を変更するオプションで指定したセットのメンバーを並べ替えます。  
  
## <a name="syntax"></a>構文  
  
```  
  
Numeric expression syntax  
Order(Set_Expression, Numeric_Expression   
[ , { ASC | DESC | BASC | BDESC } ] )  
  
String expression syntax  
Order(Set_Expression, String_Expression   
[ , { ASC | DESC | BASC | BDESC } ] )  
  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Numeric_Expression*  
 有効な数値式は、通常、数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *String_Expression*  
 有効な文字列式であり、セルの有効な多次元式 (MDX) 式では通常は、文字列として表された数値を返すを調整します。  
  
## <a name="remarks"></a>コメント  
 **順序**関数は階層型にするか (を使用して指定された、 **ASC**または**DESC**フラグ) または非階層型 (を使用して指定された、 **BASC**または**BDESC**フラグ、 **B** 「break 階層」の略)。 場合**ASC**または**DESC**が指定されている、**順序**関数は、階層内の位置に基づいてメンバーが整列され、各レベルが整列します。 場合**BASC**または**BDESC**が指定されている、**順序**階層を無視してセット内のメンバーが整列します。 フラグなしでは、指定された**ASC**既定値です。  
  
 場合、**順序**関数は 2 つ以上の階層が、クロス結合は、set で使用し、 **DESC**フラグを使用すると、セット内の最後の階層のメンバーだけが注文は。 この点が Analysis Services 2000 とは異なります。Analysis Services 2000 では、セットのすべての階層が並べ替えられます。  
  
## <a name="examples"></a>使用例  
 次の例を返しますから、 **Adventure Works**キューブの Date ディメンションの Calendar 階層からのすべての Calendar Quarters の再販業者の注文の数。**順序**関数は ROWS 軸のセットを並べ替えます。 **順序**関数によって設定を注文する`[Reseller Order Count]`によって決定される階層の順序、降順、`[Calendar]`階層。  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 通知方法については、この例でときに、 **DESC**フラグを変更**BDESC**階層が切断され、Calendar Quarters のリストが階層に関係なく返されます。  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 次の例では、階層とは無関係に、Reseller Gross Profit に基づいて、売上が上位 5 番目までの製品のサブカテゴリに対応する Reseller Sales メジャーを返しています。 **サブセット**関数を使用してを使用して結果を並べ替えてから、セットの最初の 5 つの組のみを返す、**順序**関数。  
  
 `SELECT Subset`  
  
 `(Order`  
  
 `([Product].[Product Categories].[SubCategory].members`  
  
 `,[Measures].[Reseller Gross Profit]`  
  
 `,BDESC`  
  
 `)`  
  
 `,0`  
  
 `,5`  
  
 `) ON 0`  
  
 `FROM [Adventure Works]`  
  
 次の例では、**ランク**City 階層のメンバーにランクの関数は、Reseller Sales Amount メジャーに基づいてし、ランクの順序で表示されます。 使用して、**順序**City 階層のメンバーのセットを関数の最初の注文を 1 回だけ実行し、並べ替えた順で表示される前に後で線形スキャンには、並べ替え。  
  
```  
WITH   
SET OrderedCities AS Order  
   ([Geography].[City].[City].members  
   , [Measures].[Reseller Sales Amount], BDESC  
   )  
MEMBER [Measures].[City Rank] AS Rank  
   ([Geography].[City].CurrentMember, OrderedCities)  
SELECT {[Measures].[City Rank],[Measures].[Reseller Sales Amount]}  ON 0   
,Order  
   ([Geography].[City].[City].MEMBERS  
   ,[City Rank], ASC)  
    ON 1  
FROM [Adventure Works]  
```  
  
 次の例では、製品の数を返しますを使用して、一意のセットで、**順序**関数を使用する前に、空の組を順序付け、**フィルター**関数。 **CurrentOrdinal**を比較し、関係を排除する関数を使用します。  
  
```  
WITH MEMBER [Measures].[PrdTies] AS Count  
   (Filter  
      (Order  
        (NonEmpty  
          ([Product].[Product].[Product].Members  
          , {[Measures].[Reseller Order Quantity]}  
          )  
       , [Measures].[Reseller Order Quantity]  
       , BDESC  
       ) AS OrdPrds  
    , (OrdPrds.CurrentOrdinal < OrdPrds.Count   
       AND [Measures].[Reseller Order Quantity] =   
          ( [Measures].[Reseller Order Quantity]  
            , OrdPrds.Item  
               (OrdPrds.CurrentOrdinal  
               )  
            )  
         )  
         OR (OrdPrds.CurrentOrdinal > 1   
            AND [Measures].[Reseller Order Quantity] =   
               ([Measures].[Reseller Order Quantity]  
               , OrdPrds.Item  
                  (OrdPrds.CurrentOrdinal-2)  
                )  
             )  
          )  
       )  
SELECT {[Measures].[PrdTies]} ON 0  
FROM [Adventure Works]  
```  
  
 理解する方法、 **DESC**組のセットとの連携をフラグは、まず、次のクエリの結果を検討してください。  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 Rows 軸で、Sales Territory Groups が次のように Tax Amount で順序を降順で並べ替えを確認できます。北アメリカ、ヨーロッパ、太平洋、名 ここでは、どうを参照してください。、Sales Territory Groups のセットを Product Subcategories のセットとクロス結合し、適用、**順序**次のように、同じ方法で機能。  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
*  
{[Product].[Product Categories].[subCategory].Members}  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 Product Subcategories のセットが、階層の順序を降順に順序付けが完了中に、Sales Territory Groups が並べ替えられていないようになりましたされ、階層で表示される順序で表示されます。ヨーロッパ、NA、北米および Pacific です。 これは、Product Subcategories の組のセット内の最後の階層が並べ替えられているためにです。 Analysis Services 2000 の動作の再現を使用して、一連の入れ子になった**生成**関数は、クロス結合たとえばは前に、各セットを並べ替えます。  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
GENERATE(  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
,  
ORDER(  
[Sales Territory].[Sales Territory].CURRENTMEMBER  
*  
{[Product].[Product Categories].[subCategory].Members}  
,[Measures].[Tax Amount], DESC))  
ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
