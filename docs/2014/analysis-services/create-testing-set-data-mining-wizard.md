---
title: テスト セット (データ マイニング ウィザード) の作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.holdout.f1
ms.assetid: d0a44b59-ffbd-45fc-baa8-6b8046b1a2f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f0e4d1a384995c0c49c346102f8fddbcdf47f68
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086788"
---
# <a name="create-testing-set-data-mining-wizard"></a>テスト セットの作成 (データ マイニング ウィザード)
  **[テスト セットの作成]** ページを使用すると、トレーニングに使用するデータの量、およびテスト セットとして使用するために予約するデータの量を指定できます。 マイニング構造を作成する際にデータをトレーニングとテストのセットに分割すると、後で作成するマイニング モデルの精度をより簡単に評価できるようになります。  
  
 テスト データの量を割合で指定することも、テストに使用するケースの数を制限する数値を指定することもできます。 テストに使用するケースの最大数と割合の両方を指定すると、両方の設定が使用され、テスト データセットには小さい方の数のケースが含められます。 既定では、データの 30% がテストに、70% がトレーニングに使用され、テスト ケースの最大数はありません。  
  
 既定では、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] で、パーティション分割の開始に使用される数値シードが生成されます。 このシードはマイニング構造の名前に基づきます。 マイニング構造の名前を変更してもパーティションが変わらないようにするには、マイニング構造の HoldoutSeed プロパティを設定してシードの値を指定します。 提示されたシードを変更する場合は、構造を再処理する必要があります。  
  
 後でテスト データまたはトレーニング データの量を変更する場合は、変更、`HoldoutMaxCases`と`HoldoutMaxPercent`プロパティを使用してデータ マイニング構造、**プロパティ**ウィンドウ。 ただし、変更を行った後、マイニング構造および関連するすべてのマイニング モデルを再処理する必要があります。 また、次の制限事項が適用されます。  
  
-   データ マイニング構造のパーティション分割は、そのデータ マイニング構造が [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] に格納されている場合にのみサポートされます。 以前のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、マイニング構造のパーティション情報のキャッシュはサポートされません。  
  
-   タイム シリーズ マイニング モデルに必要な Key Time 列がマイニング構造に含まれている場合、そのマイニング構造をパーティション分割することはできません。  
  
-   入れ子になったテーブルに格納されている値を予測しようとしている場合、データをパーティション分割することはできません。  
  
 **詳細情報。** [テストと検証&#40;データ マイニング&#41;](data-mining/testing-and-validation-data-mining.md)、[リレーショナル マイニング構造を作成する](data-mining/create-a-relational-mining-structure.md)、[基本的なデータ マイニング チュートリアル](../../2014/tutorials/basic-data-mining-tutorial.md)  
  
## <a name="options"></a>および  
 **テスト用データの割合**  
 トレーニング セットとして使用するデータの割合を増減するには、上矢印および下矢印をクリックするか、テキスト ボックスに 0 ～ 100 の値を入力します。  
  
 **テスト データ セット内のケースの最大数**  
 テストに使用できるケースの数を制限する数値を入力します。  
  
 データの実際のケース数よりも大きな数値を指定すると、すべてのケースが使用されます。  
  
 既定値は NULL です。 これは制限がないことを示します。  
  
## <a name="see-also"></a>参照  
 [データ マイニング ウィザードの F1 ヘルプ&#40;Analysis Services - データ マイニング&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [関連列の提示&#40;データ マイニング ウィザード&#41;](suggest-related-columns-data-mining-wizard.md)   
 [テーブル型を指定&#40;データ マイニング ウィザード&#41;](specify-table-types-data-mining-wizard.md)   
 [列のコンテンツおよびデータ型の指定&#40;データ マイニング ウィザード&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
