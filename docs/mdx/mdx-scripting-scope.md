---
title: SCOPE ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2f355842999b505a97c3387ab9e51d3b651c3b7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138277"
---
# <a name="mdx-scripting---scope"></a>MDX スクリプティング - SCOPE


  指定された多次元式 (MDX) ステートメントのスコープを指定されたサブキューブに限定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SCOPE(Subcube_Expression)   
   [ MDX_Statement ]  
END SCOPE  
  
Subcube_Expression ::=(Auxiliary_Subcube [, Auxiliary_Subcube,...n])  
  
Auxiliary_Subcube ::=   
        Limited_Set   
    | Root([dimension_name])   
    | Leaves([dimension_name])  
  
Limited_Set ::=   
        single_tuple   
    | member   
    | Common_Grain_Members   
    | hierarchy.members   
    | level.members   
    | {}   
    | Descendants  
            (  
                  Member  
         , [level  
         [  
            , SELF   
             | AFTER   
                          | BEFORE   
                          | SELF_AND_AFTER   
                          | SELF_AND_BEFORE   
                          | SELF_BEFORE_AFTER   
                          | LEAVES  
                  ]  
            )   
[* <limited set>]  
```  
  
## <a name="arguments"></a>引数  
 *Subcube_Expression*  
 有効な MDX サブキューブ式です。  
  
 *MDX_Statement*  
 有効な MDX ステートメントです。  
  
 *Common_Grain_Members*  
 同じ粒度を持つメンバーに評価される有効な MDX ステートメントです。  
  
 *single_tuple*  
 1 つの組です。  
  
## <a name="remarks"></a>コメント  
 SCOPE ステートメントは、1 つまたは複数の MDX ステートメントの実行によって影響を受けるサブキューブを決定します。 MDX ステートメントが SCOPE ステートメント内で囲まれている場合を除き、MDX ステートメントの暗黙的なスコープはキューブ全体になります。  
  
> [!NOTE]  
>  SCOPE ステートメントは、非表示のメンバーも公開します。  
  
 SCOPE ステートメントに関係なく「ホール」を公開するサブキューブを作成、 **MDX Compatibility**設定します。 たとえば、次のようなステートメントがあると、`Scope( Customer.State.members )`国や地域の状態を含まないで状態を含めることができますが、どのそれ以外の場合に非表示のプレース ホルダーのメンバーを挿入します。  
  
 計算されるメンバー、および SCOPE ステートメント内で作成された名前付きセットは、SCOPE ステートメントによる影響を受けません。  
  
## <a name="example"></a>例  
 Adventure Works での MDX 計算スクリプトから、次の例のサンプル ソリューション、現在のスコープを 2005 会計年度と sales amount quota メジャー、会計四半期として定義および、を使用して、現在のスコープ内のセルに値を割り当てます**ParallelPeriod**関数。 例では、別の SCOPE ステートメントを使用してスコープを変更し、および別の割り当てを使用して、実行、 [This (MDX)](../mdx/this-mdx.md)関数。  
  
```  
Scope   
 (   
    [Date].[Fiscal Year].&[2005],  
    [Date].[Fiscal].[Fiscal Quarter].Members,  
    [Measures].[Sales Amount Quota]  
 ) ;     
  
   This = ParallelPeriod                               
          (   
             [Date].[Fiscal].[Fiscal Year], 1,  
             [Date].[Fiscal].CurrentMember   
          ) * 1.35 ;  
  
/*-- Allocate equally to months in FY 2002 -----------------------------*/  
  
  Scope   
  (   
     [Date].[Fiscal Year].&[2002],  
     [Date].[Fiscal].[Month].Members   
  ) ;     
  
    This = [Date].[Fiscal].CurrentMember.Parent / 3 ;     
  
  End Scope ;     
End Scope ;     
```  
  
## <a name="see-also"></a>関連項目  
 [MDX スクリプト ステートメント &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
