---
title: MeasureGroupMeasures (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 45d7adc5e1f4e103790d9d067bc4876fb5b134d2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033874"
---
# <a name="measuregroupmeasures-mdx"></a>MeasureGroupMeasures (MDX)


  指定されたメジャー グループに属しているメジャーのセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
MEASUREGROUPMEASURES(MeasureGroupName)  
```  
  
## <a name="arguments"></a>引数  
 *MeasureGroupName*  
 メジャーのセットの取得元となるメジャー グループの名前が格納されている有効な文字列式です。  
  
## <a name="remarks"></a>コメント  
 指定する文字列は、メジャー グループの名前と正確に一致する必要があります。 スペースを含むメジャー グループ名を角かっこで囲む必要はありません。  
  
## <a name="example"></a>例  
 次の例では、Adventure Works キューブ内の Internet Sales メジャー グループ内のすべてのメジャーを返します。  
  
```  
SELECT MeasureGroupMeasures('Internet Sales') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
