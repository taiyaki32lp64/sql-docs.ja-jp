---
title: LastPeriods (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6a9337e925da40f148bbe0d2c77fb1cf4f5f1a99
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905783"
---
# <a name="lastperiods-mdx"></a>LastPeriods (MDX)


  指定したメンバーを含むメンバーのセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
LastPeriods(Index [ ,Member_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Index*  
 期間の数を指定する有効な数値式です。  
  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 期間の指定した数が正の値の場合、 **LastPeriods**関数だけ後退したメンバーで始まるメンバーのセットを返します*インデックス*-1 から指定されたメンバー式、および末尾には、指定されたメンバー。 関数によって返されるメンバーの数が等しく*インデックス*します。  
  
 指定した期間の数が負の場合、 **LastPeriods**関数は、指定されたメンバーで始まるメンバーのセットを返し、潜在顧客をメンバーで終わる (-*インデックス*- 1) 指定された対象からメンバー。 関数によって返されるメンバーの数がの絶対値と等しい*インデックス*します。  
  
 指定した期間の数が 0 の場合、 **LastPeriods**関数は空のセットを返します。 これとは異なり、 **Lag** 0 が指定されている場合は、指定されたメンバーを返す関数。  
  
 メンバーが指定されていない場合、 **LastPeriods**関数は**Time.CurrentMember**します。 時間ディメンションとしてディメンションが設定されていない場合、関数が解析し、エラーなしで実行がクライアント アプリケーションでセルのエラーが発生します。  
  
## <a name="examples"></a>使用例  
 次の例では、2002 会計年度の第 2 の 3 番目、および第 4 会計四半期の既定のメジャー値を返します。  
  
```  
SELECT LastPeriods(3,[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]) ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  この例を使用して書き込むこともできます、: (コロン) 演算子。  
>   
>  `[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]: [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2002]`  
  
 次の例では、2002 会計年度の第 1 会計四半期の既定のメジャー値を返します。 指定された期間の数は 3 ですが、この会計年度より前の期間が存在しないため、返すことができる期間は 1 つだけです。  
  
```  
SELECT LastPeriods  
   (3,[Date].[Fiscal].[Fiscal Quarter].[Q1 FY 2002]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
