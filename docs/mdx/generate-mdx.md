---
title: Generate (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c7a6008129d6b0a4c59412428c31f6e5de625f1f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005908"
---
# <a name="generate-mdx"></a>Generate (MDX)


  あるセットを別のセットの各メンバーに適用し、その結果セットを和集合で結合します。 また、この関数は、セットに対して文字列式を評価することによって作成される連結文字列を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set expression syntax  
Generate( Set_Expression1 ,  Set_Expression2 [ , ALL ]  )  
  
String expression syntax  
Generate( Set_Expression1 ,  String_Expression [ ,Delimiter ]  )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression1*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Set_Expression2*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *String_Expression*  
 有効な文字列式です。通常は、指定されたセット内の各組の現在のメンバーの名前 (CurrentMember.Name) です。  
  
 *区切り記号*  
 文字列式として表された有効な区切り記号です。  
  
## <a name="remarks"></a>コメント  
 2 番目のセットが指定されている場合、**Generate**関数は、2 番目のセット内の組を最初のセット内の各組に適用することによって生成されるセットを返し、その結果を結合するセットを和集合。 場合**すべて**を指定すると、結果セット内の重複部分を保持します。  
  
 文字列式が指定されている場合、**Generate**関数は、最初のセット内の各組に対して指定された文字列式を評価し、結果を連結して生成される文字列を返します。 必要に応じて、文字列は連結結果の文字列では、各結果を分離すること、区切られてすることができます。  
  
## <a name="examples"></a>使用例  
  
### <a name="set"></a>Set  
 次の例では、クエリは、セット [Date] に 4 つのメンバーがあるために 4 回、Internet Sales amount メジャーを格納しているセットを返します。[Calendar Year] です。[Calendar Year] です。メンバー:  
  
```  
SELECT   
GENERATE( [Date].[Calendar Year].[Calendar Year].MEMBERS  
, {[Measures].[Internet Sales Amount]}, ALL)  
ON 0  
FROM [Adventure Works]  
```  
  
 ALL を削除すると、クエリが変更され、Internet Sales Amount が 1 回だけ返されるようになります。  
  
```  
SELECT   
GENERATE( [Date].[Calendar Year].[Calendar Year].MEMBERS  
, {[Measures].[Internet Sales Amount]})  
ON 0  
FROM [Adventure Works]  
```  
  
 実際の最も一般的な使用**Generate**はセット評価する、複雑なメンバーのセットに対して TopCount などの式。 次のクエリの例では、行の Calendar Year ごとの上位 10 製品が表示されます。  
  
```  
SELECT   
{[Measures].[Internet Sales Amount]}  
ON 0,  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS  
, TOPCOUNT(  
[Date].[Calendar Year].CURRENTMEMBER  
*  
[Product].[Product].[Product].MEMBERS  
,10, [Measures].[Internet Sales Amount]))  
ON 1  
FROM [Adventure Works]  
```  
  
 それぞれの年とする別の上位 10 個が表示されることに注意してください。 の使用**Generate**この結果を取得する唯一の方法です。 単に年ごとの年と上位 10 製品のセットが表示されます上位 10 製品、全期間の次の例に示すように、各年に対して繰り返されます。  
  
```  
SELECT   
{[Measures].[Internet Sales Amount]}  
ON 0,  
[Date].[Calendar Year].[Calendar Year].MEMBERS  
*   
TOPCOUNT(  
[Product].[Product].[Product].MEMBERS  
,10, [Measures].[Internet Sales Amount])  
ON 1  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>String  
 次の例は、の使用を示しています。**Generate**文字列を返します。  
  
```  
WITH   
MEMBER MEASURES.GENERATESTRINGDEMO AS  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS,  
[Date].[Calendar Year].CURRENTMEMBER.NAME)  
MEMBER MEASURES.GENERATEDELIMITEDSTRINGDEMO AS  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS,  
[Date].[Calendar Year].CURRENTMEMBER.NAME, " AND ")  
SELECT   
{MEASURES.GENERATESTRINGDEMO, MEASURES.GENERATEDELIMITEDSTRINGDEMO}  
ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  この形式の**Generate**関数場合に利用でき、計算のデバッグ、セット内のすべてのメンバーの名前を表示する文字列を返すことができるためです。 一連の厳密な MDX 表記よりも読みやすいことが考えられますが、 [SetToStr &#40;MDX&#41; ](../mdx/settostr-mdx.md)関数が返される。  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
