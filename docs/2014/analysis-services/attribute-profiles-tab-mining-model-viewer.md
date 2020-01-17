---
title: 属性のプロファイル タブ (マイニング モデル ビューアー) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.naivebayse.profiles.f1
ms.assetid: 17c7e7ae-273c-4a6b-9a35-e8b9b8e65999
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b2bb75ec06d9b5c14ce5c2dcc85561412b362b40
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66063171"
---
# <a name="attribute-profiles-tab-mining-model-viewer"></a>[属性のプロファイル] タブ (マイニング モデル ビューアー)
  Naive Bayes モデルにおける入力値の分布と、結果の属性の状態との関係を確認するには、 **[属性のプロファイル]** タブを使用します。 値の分布はカラー ヒストグラムで表示され、すべての分布は値を簡単に比較できるように表形式で提示されます。  
  
 **詳細情報。** [Microsoft Naive Bayes アルゴリズム](data-mining/microsoft-naive-bayes-algorithm.md)、 [Microsoft Naive Bayes ビューアーを使用してモデルの参照](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
## <a name="options"></a>および  
 **ビューアーのコンテンツを更新します。**  
 ビューアーにマイニング モデルを再読み込みします。  
  
 **[マイニング モデル]**  
 現在のマイニング構造に含まれているマイニング モデルから、表示するものを選択します。 関連付けられているビューアーが開き、マイニング モデルが表示されます。  
  
 **ビューアー**  
 選択したマイニング モデルを調べるために使用するビューアーを選択します。 各マイニング モデル用に用意されているカスタム ビューアー、または [!INCLUDE[msCoName](../includes/msconame-md.md)] マイニング コンテンツ ビューアーを選択できます。 可能な場合プラグイン ビューアーを使用することもできます。  
  
 **凡例を表示します。**  
 **[状態]** 列の値と分布図で使用される色の対応を示すキーを表示するには、このオプションを選択します。  
  
 **[ヒストグラム バー]**  
 ヒストグラムに含めるバーの数を選択します。 選択したバーの数よりも多くのバーが存在する場合、重要度が最も高いバーが保持され、それ以外のバーは **[その他]** にまとめられます。  
  
 **予測可能です**  
 マイニング モデルの予測可能な列を選択します。  
  
 **属性のプロファイル**  
 表には次の列があります。  
  
|値|説明|  
|-----------|-----------------|  
|**Attributes**|マイニング モデルに含まれているマイニング モデル列が一覧表示されます。|  
|**状態**|対応する属性の行の色が表す状態を説明するオプションの列です。 追加または削除するには、 **[凡例の表示]** チェック ボックスを使用します。|  
|**[母集団]**|データセット全体における属性の分布が表示されます。|  
|**予測可能属性の状態の列**|予測可能な列の各状態を表す列が表示されます。各行が、モデル内の入力属性に対応しています。|  
  
## <a name="see-also"></a>参照  
 [データ マイニング アルゴリズム &#40;Analysis Services - データ マイニング&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [マイニング モデル ビューアー (データ マイニング モデル デザイナー)](mining-model-viewers-data-mining-model-designer.md)   
 [データ マイニング モデル ビューアー](data-mining/data-mining-model-viewers.md)  
  
  
