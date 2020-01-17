---
title: または (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 45063e9f2aca6a924289d4d52434535d16c9a08e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055711"
---
# <a name="or-mdx"></a>または (MDX)


  2 つの数値式の論理和を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Expression1 OR Expression2   
```  
  
#### <a name="parameters"></a>パラメーター  
 Expression1  
 数値の値を返す有効な多次元式 (MDX) 式。  
  
 Expression2  
 数値の値を返す有効な MDX 式です。  
  
## <a name="return-value"></a>戻り値  
 ブール値を返す**true**にいずれかまたは両方の引数が評価される場合**true**、それ以外の**false**します。  
  
## <a name="remarks"></a>コメント  
 **または**演算子はブール値として両方の引数を処理 (つまり、0 として**false**、それ以外の**true**) 論理和演算を実行します。 次の表に示します、**または**演算子が論理和演算を実行します。  
  
|*Expression1*|*Expression2*|戻り値|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>例  
 次のクエリには、"MARRIED OR MALE"の現在の Customer ディメンションの Gender 階層のメンバーが Male または Customer ディメンションの Marital Status 階層の現在のメンバーである場合は、結婚; 文字列を返す計算されるメジャーが含まれています。それ以外の場合"UNMARRIED または FEMALE"文字列を返します。  
  
```  
WITH  
MEMBER MEASURES.ORDEMO AS  
IIF(  
([Customer].[Gender].CURRENTMEMBER IS [Customer].[Gender].&[M])  
OR  
([Customer].[Marital Status].CURRENTMEMBER IS [Customer].[Marital Status].&[M]),  
"MARRIED OR MALE",  
"UNMARRIED OR FEMALE")  
SELECT [Customer].[Gender].[Gender].MEMBERS ON 0,  
[Customer].[Marital Status].[Marital Status].MEMBERS ON 1  
FROM [Adventure Works]  
WHERE(MEASURES.ORDEMO)  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 演算子リファレンス&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
