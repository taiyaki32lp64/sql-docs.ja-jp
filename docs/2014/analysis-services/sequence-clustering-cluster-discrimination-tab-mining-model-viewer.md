---
title: シーケンス クラスターのクラスターの識別 タブ (マイニング モデル ビューアー) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.discrimination.f1
ms.assetid: 7dd16479-2633-4f4b-83bf-cf55972a2241
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 914629fca09d4bcffb5ac931316331bbb7e7eebe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069135"
---
# <a name="sequence-clustering-cluster-discrimination-tab-mining-model-viewer"></a>シーケンス クラスターの [クラスターの識別] タブ (マイニング モデル ビューアー)
  **Microsoft シーケンス クラスター ビューアー**の **[クラスターの識別]** タブでは、シーケンス クラスター モデルから選択した 2 つのクラスターを比較します。  
  
 2 つのクラスターを比較して、異なっている状態と遷移を確認するには、シーケンス クラスター モデルのこのビューを使用します。  
  
 **詳細情報。** [Microsoft シーケンス クラスター アルゴリズム](data-mining/microsoft-sequence-clustering-algorithm.md)、 [Microsoft シーケンス クラスター ビューアーを使用してモデルの参照](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>および  
 **ビューアーのコンテンツを更新します。**  
 ビューアーにマイニング モデルを再読み込みします。  
  
 **[マイニング モデル]**  
 現在のマイニング構造に含まれているマイニング モデルから、表示するモデルを選択します。 関連付けられているビューアーが開き、マイニング モデルが表示されます。  
  
 **ビューアー**  
 選択したマイニング モデルを調べるために使用するビューアーを選択します。 カスタム ビューアーまたは **Microsoft 汎用コンテンツ ツリー ビューアー**を使用できます。 利用可能な場合プラグイン ビューアーを使用することもできます。  
  
 **クラスター 1**  
 モデル内のクラスターから、クラスターを 1 つ選択します。  
  
 **クラスター 2**  
 **[クラスター 1]** と比較するために、マイニング モデル内のクラスターをもう 1 つ選択します。  
  
 別のクラスターを選択しなかった場合は、既定により、選択済みのクラスターとその補集合 (クラスター 1 に属さないモデル内のすべてのケース) が比較されます。  
  
 **識別スコア\<クラスター 1 > と\<クラスター 2 >**  
 選択したクラスターを詳細に比較したグラフを表示します。 通常、1 つのクラスター モデルが単一のクラスターに対して状態と値を排他的に割り当てることはめったにありません。 したがって、ビューアーは、特定の属性または状態が特定のクラスターで *優位である* ことを示すだけです。  
  
 全体的に見て、特定のクラスターに 1 つの状態の大半が含まれることがあります。例として、水筒と水筒ケースの購入というシーケンスの一般的な状態があります。 ただし、より重要な定義特性を持つ他のクラスターにこのシーケンスが存在する場合があります。 たとえば、別のクラスターが非常に短い取引時間によって定義された強力な特性を持っている場合、分析では、「水筒と水関連商品は通常はこのクラスターにグループ化されるが、常にそうであるわけではない」という結果が出る可能性があります。  
  
|値|説明|  
|-----------|-----------------|  
|**変数**|マイニング モデルの属性です。|  
|**値**|**[変数]** に一覧表示される属性の状態です。|  
|**優先\<クラスター 1 >**|**[変数]** および **[値]** に示された属性および状態が、 **[クラスター 1]** で選択されたクラスターでどの程度優位であるかを示す色つきのバーを表示します。|  
  
## <a name="see-also"></a>参照  
 [データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [マイニング モデル ビューアー (データ マイニング モデル デザイナー)](mining-model-viewers-data-mining-model-designer.md)   
 [データ マイニング モデル ビューアー](data-mining/data-mining-model-viewers.md)  
  
  
