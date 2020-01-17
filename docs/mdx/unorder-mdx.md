---
title: Unorder (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 954a71c8ca2e96d905892d77ff12b7270deded5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097266"
---
# <a name="unorder-mdx"></a>Unorder (MDX)


  適用済みの順序指定されたセットから削除します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Unorder(Set_Expression)   
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) です。  
  
## <a name="remarks"></a>コメント  
 **Unorder**関数はセットに含まれる、その他の関数またはステートメントでなどの組に適用された順序設定を削除、[順序](../mdx/order-mdx.md)関数。 によって返されるセット内の組の順序、 **Unorder**関数が不定になります。  
  
 **Unorder**のセットを処理クエリの最適化のためのヒントとして関数を使用します。 使用してセット内の組の順序が計算処理またはクエリに重要ではない場合、 **Unorder**関数が提供できるは、このような場合、パフォーマンスが向上します。 など、 [NonEmpty (MDX)](../mdx/nonempty-mdx.md)関数パフォーマンスが向上この関数に指定されたセットがない場合に比べて順序付けられた[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、順序を保持する必要がで[!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]、クエリ プロセッサが、実行しようとしています。などの多くを自動的にこの関数関数**合計**と**集計**します。 使用するパフォーマンス メリット**Unorder**は数百万の組から成る大きなセットである可能性があります。  
  
## <a name="example"></a>例  
 次の擬似コードは、この関数の構文を示しています。  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
