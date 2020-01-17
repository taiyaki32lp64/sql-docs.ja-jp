---
title: 倍精度浮動小数点 (コメント) (DMX) をスラッシュ |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7f6e05ac728f6e1a9dda94dfcb07d26309b3e1f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061670"
---
# <a name="double-slash-comment-dmx"></a>2 つのスラッシュ (コメント) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  テキストを示す文字列を[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]は実行されません。 コメントは、データ マイニング拡張機能 (DMX) ステートメント内で入れ子にしたり、コード行の最後に含めたり、別の行に挿入したりすることができます。  
  
## <a name="syntax"></a>構文  
  
```  
  
// Comment_Text   
```  
  
#### <a name="parameters"></a>パラメーター  
 *Comment_Text*  
 コメントのテキストを含む文字列です。  
  
## <a name="remarks"></a>コメント  
 単一行のみのコメントには、// を使用します。 // を使用して挿入されたコメントは、改行文字によって分割されます。  
  
 コメントの長さには制限がありません。  
  
 DMX でさまざまな種類のコメントを使用する方法の詳細については、次を参照してください。[コメント&#40;DMX&#41;](../dmx/comments-dmx.md)します。  
  
## <a name="see-also"></a>参照  
 [スラッシュ アスタリスク&#40;コメント&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)   
 [--&#40;コメント&#41; &#40;DMX&#41;の概要](../dmx/comment-dmx-summary.md)   
 [データ マイニング拡張機能&#40;DMX&#41;演算子リファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [演算子&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
