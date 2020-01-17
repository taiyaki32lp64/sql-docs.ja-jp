---
title: StrToTuple (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 232d1e94892165430867ec5217f8c87ccd625b48
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036715"
---
# <a name="strtotuple-mdx"></a>StrToTuple (MDX)


  MDX 形式の文字列によって指定されたタプルを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
StrToTuple(Tuple_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>引数  
 *Tuple_Specification*  
 直接的または間接的にタプルを指定する有効な文字列式です。  
  
## <a name="remarks"></a>コメント  
 **StrToTuple**関数は、指定されたセットを返します。 **StrToTuple**関数は通常、外部関数からタプル仕様を MDX ステートメントに返すためにユーザー定義関数と共に使用されます。  
  
-   CONSTRAINED フラグを使用するときは、タプル指定に修飾されているメンバー名または修飾されていないメンバー名を含める必要があります。 このフラグは、指定された文字列によるインジェクション攻撃のリスク軽減のために使用されます。 文字列が指定されている場合は、修飾名または修飾されていないに直接解決できないメンバー名は次のエラーが表示されます。"CONSTRAINED によって設定された制限 STRTOTUPLE 関数でフラグに違反しました"。  
  
-   CONSTRAINED フラグを使用しない場合、タプルを返す有効な MDX 式に解決されるタプルを指定できます。  
  
## <a name="examples"></a>使用例  
 次の例では、2004 年の Bayern メンバーの Reseller Sales Amount メジャーを返します。 タプルの指定には、有効な MDX タプル式が含まれています。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 次の例では、2004 年の Bayern メンバーの Reseller Sales Amount メジャーを返します。 提供されているタプルの指定には、CONSTRAINED フラグによって必要に応じて、修飾されたメンバー名が含まれています。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
  
```  
  
 次の例では、2004 年の Bayern メンバーの Reseller Sales Amount メジャーを返します。 タプルの指定には、有効な MDX タプル式が含まれています。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].&[2003].NEXTMEMBER, [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 次の例では、CONSTRAINED フラグによってエラーを返します。 指定されたタプルの指定には、有効な MDX タプル式が含まれますが、CONSTRAINED フラグには、タプル仕様内の修飾名または修飾されていないメンバー名が必要です。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].&[2003].NEXTMEMBER, [Measures].[Reseller Sales Amount])', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
