---
title: (MDX) は、|Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aaf4151d8291ccd4249892c6ef8fce8a3d280f6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905979"
---
# <a name="is-mdx"></a>(MDX)


  2 つのオブジェクト式の論理比較を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Expression1 IS ( Expression2 | NULL )  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Expression1*  
 MDX オブジェクト参照を返す有効な多次元式 (MDX) 式です。  
  
 *Expression2*  
 MDX オブジェクト参照を返す有効な MDX 式です。  
  
## <a name="return-value"></a>戻り値  
 ブール値を返す**true**両方の引数が同じオブジェクトを参照している場合、それ以外の場合**false**します。 場合、 **NULL**キーワードを指定すると、演算子を返します**true**場合*Expression1*は**null**、それ以外の**false**.  
  
## <a name="remarks"></a>コメント  
 **IS**かどうか組やメンバーがべき等である、まったく同じですが意味を決定する多くの場合、演算子を使用します。  
  
## <a name="examples"></a>使用例  
 次の例は、使用する方法を示します、 **IS**演算子を軸上の現在のメンバーが特定のメンバーを確認します。  
  
 `With`  
  
 `//Returns TRUE if the currentmember is Bikes`  
  
 `Member [Measures].[IsBikes?] AS`  
  
 `[Product].[Category].CurrentMember IS [Product].[Category].&[1]`  
  
 `SELECT`  
  
 `{[Measures].[IsBikes?]} ON 0,`  
  
 `[Product].[Category].[Category].Members ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>関連項目  
 [MDX 演算子リファレンス&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
