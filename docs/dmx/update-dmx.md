---
title: 更新プログラム (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2d28df68512f9c97faebf3ee00b2aa34a2b8d1a5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028672"
---
# <a name="update-dmx"></a>更新プログラム (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  変更、 **NODE_CAPTION**データ マイニング モデル内の列。  
  
## <a name="syntax"></a>構文  
  
```  
  
UPDATE <model>.CONTENT  
SET NODE_CAPTION='new caption'  
[WHERE <condition expression>]  
```  
  
## <a name="arguments"></a>引数  
 *model*  
 モデル識別子です。  
  
 *新しいキャプション*  
 新しい名前を含む文字列、 **NODE_CAPTION**列。  
  
 *条件式*  
 任意。 列のリストから返される値を制限する条件です。  
  
## <a name="examples"></a>使用例  
 次の例では、 **UPDATE**ステートメントは、既定の名前を変更`Cluster 1`、クラスターの`001`、わかりやすい名前に`Likely Customers`します。  
  
```  
UPDATE [TM Clustering].CONTENT  
SET NODE_CAPTION= 'Likely Customers'  
WHERE NODE_UNIQUE_NAME = '001'  
```  
  
## <a name="see-also"></a>関連項目  
 [データ マイニング拡張機能&#40;DMX&#41;データ定義ステートメント](../dmx/dmx-statements-data-definition.md)   
 [データ マイニング拡張機能&#40;DMX&#41;データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
