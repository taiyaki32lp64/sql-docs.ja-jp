---
title: RollupChildren (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 89f7545af0d98de2a6bd97630a893057aac36b12
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037048"
---
# <a name="rollupchildren-mdx"></a>RollupChildren (MDX)


  指定された単項演算子を使用して、指定したメンバーの子の値をロール アップによって生成された値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
RollupChildren(Member_Expression, Unary_Operator)   
```  
  
## <a name="arguments"></a>引数  
 *メンバー式*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
 *Unary_Operator*  
 単項演算子を指定する有効な文字列式です。  
  
## <a name="remarks"></a>コメント  
 **RollupChildren**関数が指定された単項演算子を使用して、指定されたメンバーの子の値をロールアップします。  
  
 次の表では、この関数の有効な単項演算子について説明します。  
  
|演算子|結果|  
|--------------|------------|  
|**+**|合計 = 合計 + 現在の子|  
|**-**|合計 = 合計 - 現在の子|  
|**\***|合計 = 合計 * 現在の子|  
|**/**|合計 = 合計 / 現在の子|  
|**%**|合計 = (合計/現在 child) * 100|  
|**~**|子は、プログラムのロールアップには使用されません。 その値は無視されます。|  
  
 メンバー プロパティ、演算子が一覧に表示されない場合は、エラーが発生します。 評価の順序は、演算子の優先順位ではなく、兄弟の順序によって決まります。  
  
## <a name="example"></a>例  
 次の例は、単項演算子の代替値が格納されている "Alternate Rollup Operator" というメンバー プロパティを使用して、Account ディメンションの Net Profit 階層の子メンバーを別の方法でロール アップします。 このメンバー プロパティは、Adventure Works キューブに存在しませんが、作成できませんできます。 このように使用、 **RollupChildren** what if 分析のため、予算アプリケーションで関数を使用できます。  
  
```  
RollupChildren  
   ( [Account].[Net Profit]  
   , [Account].CurrentMember.Properties ('Alternate Rollup Operator') )  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
