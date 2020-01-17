---
title: LinRegPoint (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3719071beca4dbd8cc991befbb7b2b74f8982c89
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905574"
---
# <a name="linregpoint-mdx"></a>LinRegPoint (MDX)


  セットの線形回帰を計算しの値を返します、 *y 切片*回帰直線 y = ax+b の a x の特定の値。  
  
## <a name="syntax"></a>構文  
  
```  
  
LinRegPoint(Slice_Expression_x, Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>引数  
 *Slice_Expression_x*  
 有効な数値式は、通常、スライサー軸の値を表す数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Numeric_Expression_y*  
 有効な数値式です。通常は、Y 軸の値を表す数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *Numeric_Expression_x*  
 有効な数値式です。通常は、X 軸の値を表す数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 最小二乗法が使用する、線形回帰は、回帰直線 (点、一連の best-fit 行) の式を計算します。 回帰直線では、次の式では、場所は傾き、b は切片です。  
  
 y = ax+b  
  
 **LinRegPoint**関数は、y 軸の値を取得する 2 番目の数値式に対して指定されたセットを評価します。 関数は、x 軸の値を取得する場合に、3 番目の数値式に対して指定されたセットを評価します。 3 番目の数値式が指定されていない場合、関数は、x 軸の値として指定されたセット内のセルの現在のコンテキストを使用します。 X 軸の引数を指定しない時間ディメンションでよく使用します。  
  
 線型回帰直線が計算された後、1 番目の数値式に対して回帰直線式の値が計算され、返されます。  
  
> [!NOTE]  
>  **LinRegPoint**関数は空のセルまたはテキストを含むセルを無視します。 ただし、関数には、値が 0 のセルが含まれています。  
  
## <a name="example"></a>例  
 次の例では、売上数量と店舗売上の統計的関係に基づいて、過去 10 期間の予測売上数量を返しています。  
  
```  
LinRegPoint([Measures].[Unit Sales],LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
