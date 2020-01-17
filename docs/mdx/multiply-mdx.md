---
title: '* (乗算)(MDX) |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 396dded86adfe8faa6b6ad58b5eb8174d4323726
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088420"
---
# <a name="-multiply-mdx"></a>* (乗算) (MDX)


  2 つの数値を乗算する算術演算を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Numeric_Expression * Numeric_Expression  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Numeric_Expression*  
 数値の値を返す有効な多次元式 (MDX) 式。  
  
## <a name="return-value"></a>戻り値  
 優先順位の高いパラメーターのデータ型の値。  
  
## <a name="remarks"></a>コメント  
 両方の式は、同じデータ型でなければなりません。または、一方の式をもう一方の式のデータ型に暗黙的に変換できる必要があります。 1 つの式が NULL 値と評価される場合は、NULL 値が返されます。  
  
## <a name="see-also"></a>関連項目  
 [MDX 演算子リファレンス&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
