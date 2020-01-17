---
title: Forecasting 構造およびモデル (中級者向けデータ マイニング チュートリアル) の作成 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5f55cbf6-0db4-4cb4-a0f5-e27441873d4f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6e631a8983705d4f58e4b193823c9a255284f346
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63204813"
---
# <a name="creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial"></a>Forecasting 構造およびモデルの作成 (中級者向けデータ マイニング チュートリアル)
  次に、データ マイニング ウィザードを使用して、先ほど作成したデータ ソース ビューに基づく新しいマイニング構造とマイニング モデルを作成します。 この作業では、マイニング モデルで [!INCLUDE[msCoName](../includes/msconame-md.md)] タイム シリーズ アルゴリズムが使用されるように指定します。  
  
### <a name="to-create-a-forecasting-mining-structure"></a>予測マイニング構造を作成するには  
  
1.  ソリューション エクスプ ローラーで[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]を右クリックして**マイニング構造**選択**新しいマイニング構造の**します。  
  
2.  **[データ マイニング ウィザードへようこそ]** ページで **[次へ]** をクリックします。  
  
3.  **定義方法の選択**ことを確認します ページで、**既存のリレーショナル データベースまたはデータ ウェアハウスから**が選択されているし、をクリックし、 **次へ**します。  
  
4.  **データ マイニング構造の作成**] ページ [**を使用するデータ マイニング技法を指定しますか?** を選択します**Microsoft タイム シリーズ**、順にクリックします **[次へ]** します。  
  
5.  **データ ソース ビューの選択**] ページ [**使用可能なデータ ソース ビュー**を選択します**SalesByRegion**します。  
  
6.  **[次へ]** をクリックします。  
  
7.  **テーブルの種類の指定** ページで、チェック ボックス、**ケース**vTimeSeries テーブルの列が選択されているし、順にクリックします**次**。  
  
8.  **トレーニング データの指定** ページで、チェック ボックスをオン、**キー** ModelRegion 列および ReportingDate 列の列。  
  
     ReportingDate は既定でオンになります。これは、データ ソース ビューを作成したときに、この列を論理主キーとして指定したためです。 ModelRegion を 2 つ目のキーとして追加することで、このフィールドに表示されるモデルと領域の組み合わせごとに別々の時系列を作成するようにアルゴリズムに指示します。  
  
9. チェック ボックスをオン、**入力**と**予測可能**列、Quantity、列、およびクリックを**次**。  
  
     選択して**予測可能**、この列のデータに基づいて予測を作成することを指定します。 ただし、過去のデータに基づく予測にする必要があるため、列を入力として追加する必要もあります。  
  
10. ページ**指定列のコンテンツおよびデータ型**、選択内容を確認します。  
  
     ModelRegion 列は、として指定されて、**キー**列および ReportingDate 列として指定されて自動的に、 **Key Time**列。 キーの種類ごとにキーを 1 つだけ指定できます。  
  
11. **[次へ]** をクリックします。  
  
12. **ウィザードの完了** ページの**マイニング構造名**、型`Forecasting`します。  
  
    > [!NOTE]  
    >  時系列モデルでは、ドリルスルーを有効にするオプションは使用できません。  
  
13. **マイニング モデル名**、型`Forecasting`、 をクリックし、**完了**します。  
  
     データ マイニング デザイナーで開き、表示、`Forecasting`作成したマイニング構造です。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [Forecasting 構造の変更&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>参照  
 [Data Mining Designer](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Microsoft タイム シリーズ アルゴリズム](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
