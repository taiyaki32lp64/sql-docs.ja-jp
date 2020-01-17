---
title: しない (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b4a28c6be2c956636f303ccc561936f799c63b64
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008253"
---
# <a name="not-dmx"></a>しない (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  論理演算子には、数値式に対して論理否定を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Expression1*  
 数値の値を返す有効な DMX 式。  
  
## <a name="return-value"></a>戻り値  
 引数の結果が TRUE の場合は FALSE を返し、そうでない場合は TRUE を返すブール値です。  
  
## <a name="remarks"></a>コメント  
 引数がブール値として扱われます (0 FALSE の場合それ以外の場合 TRUE) 論理否定演算を実行します。 場合*Expression1* true の場合は、演算子は FALSE を返します。 場合*Expression1* FALSE が使用され、演算子は TRUE を返します。 次の表は、論理積を実行する方法を示しています。  
  
|Expression1|戻り値は|  
|-----------------------|---------------------|  
|TRUE|FALSE|  
|false|TRUE|  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング拡張機能&#40;DMX&#41;演算子リファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [論理演算子&#40;DMX&#41;](../dmx/operators-logical.md)   
 [演算子&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
