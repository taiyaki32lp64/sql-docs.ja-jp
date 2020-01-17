---
title: マイニング モデルの表示のコピー |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clipboards [data mining]
- Mining Model Viewer [Analysis Services], clipboards
- copying mining models to clipboard
ms.assetid: 768372db-e5b4-4990-b459-03d854fd9a6d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 84abbb855673183910099f0a34d70702d34da7fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085597"
---
# <a name="copy-a-view-of-a-mining-model"></a>マイニング モデルの表示のコピー
  **のデータ マイニング デザイナーの** [マイニング モデル ビューアー] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] タブでは、マイニング モデルの種類ごとに異なるビューアーを使用します。 これらのビューアーの一部には、コンテンツをクリップボードにコピーし、そこからドキュメントやイメージ操作ソフトウェアに貼り付けるためのコンポーネントがあります。 この機能は次のコンポーネントで使用可能です。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] クラスター ビューアーのクラスター ダイアグラムと [!INCLUDE[msCoName](../../includes/msconame-md.md)] シーケンス クラスター ビューアー  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] ツリー ビューアーのデシジョン ツリーと [!INCLUDE[msCoName](../../includes/msconame-md.md)] タイム シリーズ ビューアー  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] シーケンス クラスター ビューアーの状態遷移  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] アソシエーション ルール ビューアーの依存関係ネットワーク、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes ビューアー、および [!INCLUDE[msCoName](../../includes/msconame-md.md)] ツリー ビューアー  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 汎用コンテンツ ツリー ビューアーの [ノードの詳細] ペインにあるマイニング モデル コンテンツ  
  
 マイニング モデル全体の表現をコピーすることも、ビューアーで表示している部分のみをコピーすることもできます。  
  
> [!WARNING]  
>  ビューアーを使用してモデルをコピーする場合、新しいモデル オブジェクトは作成されません。 新しいモデルを作成するには、ウィザードまたはデータ マイニング デザイナーを使用する必要があります。 詳細については、「 [マイニング モデルのコピーの作成](make-a-copy-of-a-mining-model.md)」を参照してください。  
  
### <a name="to-copy-the-complete-model-to-the-clipboard"></a>モデル全体をクリップボードにコピーするには  
  
1.  **[マイニング モデル ビューアー]** タブの **[マイニング モデル]** リストで、表示するマイニング モデルを選択します。  
  
2.  **[依存関係ネットワーク]** タブなど、適切なタブを選択してから、そのタブのツール バーで **[グラフ全体のコピー]** をクリックします。  
  
### <a name="to-copy-the-visible-piece-of-the-model-to-the-clipboard"></a>モデルの表示部分のみをクリップボードにコピーするには  
  
1.  **[マイニング モデル ビューアー]** タブの **[マイニング モデル]** リストで、表示するマイニング モデルを選択します。  
  
2.  **[依存関係ネットワーク]** タブなど、適切なタブを選択し、モデルを拡大または縮小して、希望のレベルで表示します。  
  
3.  選択したタブのツール バーで **[グラフ ビューのコピー]** をクリックします。  
  
### <a name="to-copy-the-mining-model-content-to-the-clipboard"></a>マイニング モデル内容をクリップボードにコピーするには  
  
1.  **[マイニング モデル ビューアー]** タブの **[マイニング モデル]** リストで、表示するマイニング モデルを選択します。  
  
2.  **[ビューアー]** ボックスの一覧で **[Microsoft 汎用コンテンツ ツリー ビューアー]** をクリックします。  
  
3.  **[ノードのキャプション (一意の ID)]** ペインでノードをクリックします。  
  
4.  **[ノードの詳細]** ペインを右クリックし、 **[すべて選択]** をクリックします。  
  
5.  **[ノードの詳細]** ペインをもう一度右クリックし、 **[コピー]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [マイニング モデル ビューアーのタスクと操作方法](mining-model-viewer-tasks-and-how-tos.md)  
  
  
