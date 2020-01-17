---
title: StrToValue (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cad8fec605a56a60cfcc7024739225e474fd42f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036692"
---
# <a name="strtovalue-mdx"></a>StrToValue (MDX)


  MDX 形式の文字列によって指定された数値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
StrToValue(MDX_Expression [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>引数  
 *MDX_Expression*  
 直接的または間接的に 1 つのセルに解決される有効な文字列式です。  
  
## <a name="remarks"></a>コメント  
 **StrToValue**関数が MDX 式で指定された値を返します。 **StrToValue**を 1 つのセルに解決される MDX ステートメントを外部関数から MDX 式を返す関数は通常使用のユーザー定義関数。  
  
-   CONSTRAINED フラグを使用する場合、MDX 式にはスカラー値のみを含める必要があります。 CONSTRAINED フラグは、指定された文字列によるインジェクション攻撃の危険性を軽減するために使用します。 MDX 式は、スカラー値に直接解決ではありませんが、次のエラーが表示されます。"CONSTRAINED によって設定された制限 STRTOVALUE 関数でフラグに違反しました"。  
  
-   CONSTRAINED フラグを使用しない場合は、1 つのセルを返す有効な多次元式 (MDX) 式に解決される範囲で複雑な MDX 式を指定できます。  
  
> [!NOTE]  
>  数値の値として、MDX 式の結果を返すことは、値はテキストとして格納され、返される値に対して算術演算を実行する場合役立ちます。  
  
## <a name="example"></a>例  
 次の例では、 **StrToValue**値として、各自転車の重量を返す関数。  
  
```  
WITH MEMBER Measures.x AS   
StrToValue   
   ([Product].[Product].CurrentMember.Properties ('Weight')  
   ,CONSTRAINED  
   )  
SELECT Measures.x ON 0  
,[Product].[Product].[Product].Members ON 1  
FROM [Adventure Works]  
WHERE [Product].[Product Categories].[Bikes]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
