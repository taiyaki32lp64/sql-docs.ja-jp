---
title: 変更と処理、マーケット バスケット モデル (中級者向けデータ マイニング チュートリアル) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b6019413-aebd-4ff7-831a-644572ad88b1
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4987e3497b7d52ff11f8f52bc403105340f7f508
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63301373"
---
# <a name="modifying-and-processing-the-market-basket-model-intermediate-data-mining-tutorial"></a>マーケット バスケット モデルの変更と処理 (中級者向けデータ マイニング チュートリアル)
  作成したアソシエーション マイニング モデルを処理する前に、2 つのパラメーターの既定値を変更する必要があります。*サポート*と*確率*します。  
  
-   *サポート*が有効と見なさ前に、のルールが存在するケースの割合を定義します。 ここでは、1% 以上のケースでルールが検出される必要があるように指定します。  
  
-   *確率*アソシエーションがどの程度必要がありますを定義する前に、有効と見なされます。 ここでは、確率が 10% 以上のアソシエーションを対象とします。  
  
 サポートと確率の増減による影響の詳細については、次を参照してください。 [Microsoft アソシエーション アルゴリズム テクニカル リファレンス](../../2014/analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)します。  
  
 構造とパラメーターを定義した後、**アソシエーション**マイニング モデル、モデルが処理されます。  
  
### <a name="to-adjust-the-parameters-of-the-association-model"></a>Association モデルのパラメーターを調整するには  
  
1.  開く、**マイニング モデル**データ マイニング デザイナーのタブ。  
  
2.  右クリックし、**アソシエーション**クリックし、デザイナーのグリッドの列で**アルゴリズムのパラメーターを開くアルゴリズム パラメーターの設定** ダイアログ ボックス。  
  
3.  **値**の列、**アルゴリズム パラメーター**  ダイアログ ボックスで、次のパラメーターを設定します。  
  
     MINIMUM_PROBABILITY = 0.1  
  
     MINIMUM_SUPPORT = 0.01  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-process-the-mining-model"></a>マイニング モデルを処理するには  
  
1.  **マイニング モデルの**のメニュー[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]を選択します**マイニング構造の処理とすべてのモデル。**  
  
2.  プロジェクトをビルドおよび配置するかどうかを確認する警告をクリックし、**はい**します。  
  
     **マイニング構造の処理 - アソシエーション** ダイアログ ボックスが表示されます。  
  
3.  **[実行]** をクリックします。  
  
     **処理の進行状況**モデルの処理に関する情報を表示するダイアログ ボックスが開きます。 新しい構造とモデルの処理には、時間がかかることがあります。  
  
4.  処理が完了したら、クリックして**閉じる**を終了する、**処理の進行状況** ダイアログ ボックス。  
  
5.  クリックして**閉じる**を終了するには、もう一度、**マイニング構造の処理 - アソシエーション** ダイアログ ボックス。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [マーケット バスケット モデルの検証&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/exploring-the-market-basket-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>参照  
 [処理の要件および注意事項 &#40;データ マイニング&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
