---
title: DROP SET ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f4e31a687597e454b9afe38d6c6dd1c15af486d0
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893722"
---
# <a name="mdx-data-definition---drop-set"></a>MDX データ操作 - DROP SET


  名前付きセットを削除します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DROP [SESSION] SET   
   <Cube_Reference>.Set_Name   
               [,<Cube_Reference>.Set_Name ...n]  
  
<Cube_Reference> ::= {CURRENTCUBE | Cube_Name}  
  
```  
  
## <a name="arguments"></a>引数  
 *Cube_Name*  
 キューブの名前を指定する有効な文字列式です。  
  
 *Set_Name*  
 削除する名前付きセットの名前を提供する有効な文字列式です。  
  
## <a name="remarks"></a>コメント  
 名前付きセットの詳細については、「[MDX での名前付きセットの作成 &#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets)」をご覧ください。  
  
## <a name="see-also"></a>関連項目  
 [Mdx データ定義ステートメント&#40;mdx&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
