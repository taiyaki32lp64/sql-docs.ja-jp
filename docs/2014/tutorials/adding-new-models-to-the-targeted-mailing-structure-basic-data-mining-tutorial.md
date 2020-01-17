---
title: ターゲット メーリングの構造 (基本的なデータ マイニング チュートリアル) に新しいモデルの追加 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 512c6888-60f1-46e4-9639-bc448395b8d7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 285ee82110ffdef521d75fb43343f4889663e981
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62822641"
---
# <a name="adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>絞り込みメール配信構造への新しいモデルの追加 (基本的なデータ マイニング チュートリアル)
  このタスクを使用して追加の 2 つのモデルを定義、**マイニング モデル**データ マイニング デザイナーのタブ。 モデルの作成には、Microsoft クラスタリング アルゴリズムと Microsoft Naive Bayes アルゴリズムを使用します。 この 2 つのアルゴリズムを選択する理由は、不連続値 (自転車の購入) を予測できるためです。 これらのアルゴリズムの詳細については、次を参照してください[Microsoft クラスタ リング アルゴリズム](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)と[Microsoft Naive Bayes アルゴリズム。](../../2014/analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)  
  
### <a name="to-create-a-clustering-mining-model"></a>クラスター マイニング モデルを作成するには  
  
1.  切り替えて、**マイニング モデル** タブで、データ マイニング デザイナーで[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]します。  
  
     デザイナーが、マイニング構造に 1 つ 1、2 つの列を表示することに注意してください、`TM_Decision_Tree`前のレッスンで作成したマイニング モデルです。  
  
2.  右クリックし、**構造**列と select**マイニング モデルの新しい**します。  
  
3.  **マイニング モデルの新しい** ダイアログ ボックスで**モデル名**、型`TM_Clustering`します。  
  
4.  **アルゴリズム名**、 **Microsoft クラスタ リング**します。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 新しいモデルが表示されます、**マイニング モデル**データ マイニング デザイナーのタブ。 このモデルで構築された、[!INCLUDE[msCoName](../includes/msconame-md.md)]クラスタ リング アルゴリズムでは、クラスターに似た特性を持つ顧客をグループ化し、自転車の購買の各クラスターを予測します。 列の使用法と、新しいモデルに変更を加えるのプロパティを変更できますが、`TM_Clustering`モデルはこのチュートリアルでは必要です。  
  
### <a name="to-create-a-naive-bayes-mining-model"></a>Naive Bayes マイニング モデルを作成するには  
  
1.  **マイニング モデル**データ マイニング デザイナーのタブを右**構造**列、および選択**マイニング モデルの新しい**します。  
  
2.  **マイニング モデルの新しい**ダイアログ ボックスで、**モデル名**、型`TM_NaiveBayes`します。  
  
3.  **アルゴリズム名**を選択します**Microsoft Naive Bayes**、 をクリックし、 **OK**。  
  
     示すメッセージが表示されます、 [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes アルゴリズムはサポートしていません、**年齢**と**Yearly Income**が連続する列。  
  
4.  クリックして**はい**メッセージを無視して続行します。  
  
 新しいモデルに表示されます、**マイニング モデル**データ マイニング デザイナーのタブ。 列の使用法やこれですべてのモデルのプロパティを変更することができますのタブの変更は不要、`TM_NaiveBayes`モデルがこのチュートリアルでは必要です。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [ターゲット メーリングの構造でモデルを処理&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>参照  
 [マイニング モデルを構造体に追加&#40;Analysis Services - データ マイニング&#41;](../../2014/analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)   
 [Data Mining Designer](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [データ マイニング オブジェクトの移動](../../2014/analysis-services/data-mining/moving-data-mining-objects.md)  
  
  
