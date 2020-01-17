---
title: LinRegIntercept (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 30d3fd98995c24498af9376db19087b2018394e3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905578"
---
# <a name="linregintercept-mdx"></a>LinRegIntercept (MDX)


  セットの線形回帰を計算し、回帰直線の x 切片の値を返す y ax+b の a を = です。  
  
## <a name="syntax"></a>構文  
  
```  
  
LinRegIntercept(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Numeric_Expression_y*  
 有効な数値式です。通常は、Y 軸の値を表す数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *Numeric_Expression_x*  
 有効な数値式です。通常は、X 軸の値を表す数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 最小二乗法が使用する、線形回帰は、回帰直線 (点、一連の best-fit 行) の式を計算します。 回帰直線では、次の式では、場所は傾き、b は切片です。  
  
 y = ax+b  
  
 **LinRegIntercept**関数は、y 軸の値を取得する最初の数値式に対して指定されたセットを評価します。 関数は、x 軸の値を取得する場合に、2 番目の数値式に対して指定されたセットを評価します。 2 番目の数値式が指定されていない場合、関数は、x 軸の値として指定されたセット内のセルの現在のコンテキストを使用します。 X 軸の引数を指定しない時間ディメンションでよく使用します。  
  
 点のセットを取得した後、 **LinRegIntercept**関数は、回帰直線 (上記の式 b) の切片を返します。  
  
> [!NOTE]  
>  **LinRegIntercept**関数は空のセルまたはテキストや論理値を含むセルを無視します。 ただし、関数には、値が 0 のセルが含まれています。  
  
## <a name="example"></a>例  
 次の例では、売上数量メジャーと店舗売上メジャーについて、回帰直線の切片を返しています。  
  
```  
LinRegIntercept(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
