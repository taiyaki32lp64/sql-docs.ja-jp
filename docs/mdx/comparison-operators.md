---
title: 比較演算子 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4e3aa00334d98af02521005679174feb3b28c55f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001511"
---
# <a name="comparison-operators"></a>比較演算子


  比較演算子は、スカラー データと共に使用します。 任意の多次元式 (MDX) 式では、比較演算子を使用できます。  
  
 条件を確認するには、MDX ステートメントや MDX などの関数で比較演算子も使用できます[IIf](../mdx/iif-mdx.md)関数。 ただし、条件を満たしているかどうかを調べるために比較演算子を使用する場合は、その条件に基づいてデータの変更を試みる前に、適切な権限を持っていることを確認してください。 他のクエリで実際のデータにアクセスして、そのデータを照会することができるユーザーであれば比較演算子を使用できます。 しかし、このようにアクセスできることは、それらのユーザーがデータを変更するための適切な権限を持っている、あるいは持つ必要があるという意味ではありません。 また、データの整合性を維持するためにも、データに対してクエリを実行してデータを変更できるユーザーの数は制限してください。  
  
 比較演算子は Boolean データ型、TRUE を返すか、テストされた条件の結果に基づいて、FALSE に評価されます。  
  
 MDX には、次の表に示す比較演算子がサポートされています。  
  
|演算子|説明|  
|--------------|-----------------|  
|[= (等しい)](../mdx/equal-to-mdx.md)|Null 以外の引数の左辺の引数が右辺の引数に等しい場合に TRUE を返しますそれ以外の場合、FALSE です。<br /><br /> 場合を除き、いずれかまたは両方の引数は、null 値に評価される場合、演算子は、null 値を返します比較`0=null`が行われる場合、ブール値が TRUE が含まれます。|  
|[<> (等しくない)](../mdx/not-equal-to-mdx.md)|Null 以外の引数の右辺の引数に、左の引数がない場合に TRUE を返しますそれ以外の場合、FALSE です。<br /><br /> いずれかまたは両方の引数は、null 値に評価される、演算子は null 値を返します。|  
|[> (より大きい)](../mdx/greater-than-mdx.md)|Null 以外の引数の左辺の引数が右辺の引数よりも大きい値を持つ場合に TRUE を返しますそれ以外の場合、FALSE です。<br /><br /> いずれかまたは両方の引数は、null 値に評価される、演算子は null 値を返します。|  
|[>= (以上)](../mdx/greater-than-or-equal-to-mdx.md)|NULL 以外の引数について、左の引数の値が右の引数の値以上である場合に TRUE を返します。そうでない場合は、FALSE を返します。<br /><br /> いずれかまたは両方の引数は、null 値に評価される、演算子は null 値を返します。|  
|[< (より小さい)](../mdx/less-than-mdx.md)|Null 以外の引数の左辺の引数が右辺の引数より小さい値を持つ場合に TRUE を返しますそれ以外の場合、FALSE です。<br /><br /> いずれかまたは両方の引数は、null 値に評価される、演算子は null 値を返します。|  
|[<= (以下)](../mdx/less-than-or-equal-to-mdx.md)|NULL 以外の引数について、左の引数の値が右の引数の値以下である場合に TRUE を返します。そうでない場合は、FALSE を返します。<br /><br /> いずれかまたは両方の引数は、null 値に評価される、演算子は null 値を返します。|  
  
## <a name="see-also"></a>関連項目  
 [MDX 演算子リファレンス&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [演算子&#40;MDX 構文&#41;](../mdx/operators-mdx-syntax.md)  
  
  
