---
title: 属性の識別 タブ (マイニング モデル ビューアー) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.naivebayse.discrimination.f1
ms.assetid: 68323f23-121e-44fc-be85-6f9915d6d3c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f7e8d9593cd45ec5a92ea07051fe424698d8ece6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66063131"
---
# <a name="attribute-discrimination-tab-mining-model-viewer"></a>[属性の識別] タブ (マイニング モデル ビューアー)
  入力属性の状態を比較して、それが結果属性とどのように関連しているかを確認するには、 **[属性の識別]** タブを使用します。 2 つの選択された予測可能属性の間で最も違いの大きい属性値が、一覧の先頭に表示されます。  
  
 **詳細情報。** [Microsoft Naive Bayes アルゴリズム](data-mining/microsoft-naive-bayes-algorithm.md)、 [Microsoft Naive Bayes ビューアーを使用してモデルの参照](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
## <a name="options"></a>および  
 **ビューアーのコンテンツを更新します。**  
 ビューアーにマイニング モデルを再読み込みします。  
  
 **[マイニング モデル]**  
 現在のマイニング構造に含まれているマイニング モデルから選択します。 マイニング モデルは、自動的に適切なカスタム ビューアーに表示されます。  
  
 **ビューアー**  
 選択したマイニング モデルを調べるために使用するビューアーを選択します。 モデルごとに、カスタム ビューアーまたは [!INCLUDE[msCoName](../includes/msconame-md.md)] マイニング コンテンツ ビューアーのいずれかを選択できます。 利用可能な場合プラグイン ビューアーを使用することもできます。  
  
 **属性**  
 予測可能な属性を選択します。  
  
 **値 1**  
 **[値 2]** に指定された状態と比較する予測可能な属性の状態を選択します。  
  
 **値 2**  
 **[値 1]** に指定された状態と比較する予測可能な属性の状態を選択します。 選択することも**その他のすべての状態**の値を比較する**値 1**その補数-以外の値 1 は、その他のすべての値。  
  
 **識別スコア\<値 1 > と\<値 2 >**  
 グラフには、対象となる属性が入力属性の特定の状態とどのように関係するかを記述する次の列が含まれます。  
  
|値|説明|  
|-----------|-----------------|  
|**Attributes**|マイニング モデルの入力属性です。|  
|**値**|**[属性]** に表示される属性の状態です。|  
|**優先\<値 1 >**|バーは、現在の属性と値が、 **[値 1]** で選択した対象となる結果を優先するかどうかを示します。|  
|**優先\<値 2 >**|バーは、現在の属性と値が、 **[値 2]** で選択した対象となる結果を優先するかどうかを示します。|  
  
## <a name="see-also"></a>参照  
 [データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [マイニング モデル ビューアー (データ マイニング モデル デザイナー)](mining-model-viewers-data-mining-model-designer.md)   
 [データ マイニング モデル ビューアー](data-mining/data-mining-model-viewers.md)  
  
  
