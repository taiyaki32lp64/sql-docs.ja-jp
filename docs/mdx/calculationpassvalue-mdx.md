---
title: CalculationPassValue (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ae667d2cecb65f2525aaf855d3d1b70d40a59b21
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016874"
---
# <a name="calculationpassvalue-mdx"></a>CalculationPassValue (MDX)


  キューブに対して指定された計算パスを評価し、多次元式 (MDX) 式の数値または文字列値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
      Numeric syntax  
CalculationPassValue(Numeric_Expression,Pass_Value [, ABSOLUTE | RELATIVE [,ALL]])  
String syntax  
CalculationPassValue(String_Expression ,Pass_Value [, ABSOLUTE | RELATIVE [,ALL]])  
```  
  
## <a name="arguments"></a>引数  
 *Numeric_Expression*  
 有効な数値式は、通常、数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *String_Expression*  
 有効な文字列式であり、セルの有効な多次元式 (MDX) 式では通常は、文字列として表された数値を返すを調整します。  
  
 *Pass_Value*  
 計算パス番号を指定する有効な数値式です。  
  
 ABSOLUTE  
 指定するアクセス フラグ値、 *Pass_Value*パラメーターには、計算パスの 0 から始まるインデックスが含まれています。 アクセス フラグ値が指定されていない場合は、ABSOLUTE が既定のアクセス フラグ値になります。  
  
 RELATIVE  
 指定するアクセス フラグ値、 *Pass_Value*パラメーターには、トリガーを起動する計算の計算パスからの相対的なオフセットが含まれています。 このオフセットが 0 より小さい計算パス インデックスになる場合は、計算パス 0 が使用されます。したがって、エラーは発生しません。  
  
 ALL  
 このフラグを設定すると、すべての値は null 以外に、ストレージ エンジンによって読み込まれます。 このフラグが設定されていない場合は、何の計算も適用されずに値が集計されます。  
  
## <a name="remarks"></a>コメント  
 数値式が指定されると、この関数は、指定された計算パス内で指定されている (さらに、必要に応じてアクセス フラグとアクセス フラグ修飾子で修飾されている) MDX 数値式を評価し、数値を返します。  
  
 文字列式が指定されている場合、関数が、指定された計算パスで指定された MDX 文字列式を評価することによって文字列値を返し、必要に応じてアクセス フラグとアクセス フラグ修飾子で変更*します。*  
  
 再帰を自動解決[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、この関数は、小さな実際に使用します。  
  
> [!NOTE]  
>  管理者のみが使用できる、 **CalculationPassValue** MDX スクリプト内の関数。 エラーは、この関数を含む MDX スクリプトが管理者特権がないロールのコンテキストで実行される場合に発生します。  
  
## <a name="see-also"></a>関連項目  
 [CalculationCurrentPass (MDX)](../mdx/calculationcurrentpass-mdx.md)   
 [IIf &#40;MDX&#41;](../mdx/iif-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
