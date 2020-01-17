---
title: LinRegR2 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2e38df1a24b76ee40aae3a5ab3c28dd9bca2b310
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905520"
---
# <a name="linregr2-mdx"></a>LinRegR2 (MDX)


  セットの線形回帰を計算し、R、決定係数を返します<sup>2</sup>します。  
  
## <a name="syntax"></a>構文  
  
```  
  
LinRegR2(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
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
  
 **LinRegR2**関数は指定した setagainst、y 軸の値を取得する最初の数値式を示します。 関数は、x 軸の値を取得する場合に、2 番目の数値式に対して指定されたセットを評価します。 2 番目の数値した式が指定されていない場合、関数は、x 軸の値として指定されたセット内のセルの現在のコンテキストを使用します。 X-axisargument を指定していない時間ディメンションでよく使用します。  
  
 点のセットを取得した後、 **LinRegR2**返します統計的係数 R<sup>2</sup>直線式が点に適合しているかを説明します。  
  
> [!NOTE]  
>  **LinRegR2**関数は空のセルまたはテキストや論理値を含むセルを無視します。 ただし、関数には、値が 0 のセルが含まれています。  
  
## <a name="example"></a>例  
 次の例は、統計的係数 R を返します<sup>2</sup>の売上数量と店舗売上メジャーのポイントに線形回帰式の適合度をについて説明します。  
  
```  
LinRegR2(LastPeriods(10), [Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
