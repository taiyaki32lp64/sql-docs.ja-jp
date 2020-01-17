---
title: LinRegSlope (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6d43d2ccc961e465c5430c525fd6178d74e29ca9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905546"
---
# <a name="linregslope-mdx"></a>LinRegSlope (MDX)


  セットの線形回帰を計算し、回帰直線の傾きの値を返します y ax+b の a を = です。  
  
## <a name="syntax"></a>構文  
  
```  
  
LinRegSlope(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
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
  
 **LinRegSlope**関数は、y 軸の値を取得する最初の数値式に対して指定されたセットを評価します。 次に、2 番目の数値式が指定されている場合は、指定されているセット式をその数値式に対して評価し、X 軸の値を取得します。 2 番目の数値式が指定されていない場合、関数は、x 軸の値として指定されたセット内のセルの現在のコンテキストを使用します。 X 軸の引数を指定しない時間ディメンションでよく使用します。  
  
 点のセットを取得した後、 **LinRegSlope**関数は、回帰直線の傾きを返します (、上記の式)。  
  
> [!NOTE]  
>  **LinRegSlope**関数は空のセルまたはテキストや論理値を含むセルを無視します。 ただし、関数には、値が 0 のセルが含まれています。  
  
## <a name="example"></a>例  
 次の例では、売上数量と店舗売上のメジャーに関する回帰直線の傾きを返しています。  
  
```  
LinRegSlope(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
