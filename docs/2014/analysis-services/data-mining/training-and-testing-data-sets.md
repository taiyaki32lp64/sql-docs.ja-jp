---
title: トレーニング セットとテスト データ セット |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- testing mining models
- holdout [data mining]
- testing data mining models
- accuracy testing [data mining]
ms.assetid: 5798fa48-ef3c-4e97-a17c-38274970fccd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 34aefc2895057c499e54c572340ca63dc28ed68f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082734"
---
# <a name="training-and-testing-data-sets"></a>トレーニング データ セットとテスト データ セット
  トレーニング セットとテスト セットにデータを分割することは、データ マイニング モデルの評価における重要な部分です。 通常、データセットをトレーニング セットとテスト セットに分割すると、ほとんどのデータはトレーニングに使用され、テストに使用されるデータは少量になります。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ではデータのサンプルがランダムに抽出されるため、テスト セットとトレーニング セットが同様になるように分割されます。 トレーニングとテストに類似データを使用すると、データの差異による影響を最小限に抑えることができ、モデルの特性をよりよく理解できます。  
  
 トレーニング セットを使用してモデルが処理された後、テスト セットに対する予測を実行してモデルをテストします。 テスト セット内のデータには予測対象の属性の既知の値が既に含まれているため、モデルの推測が正しいかどうかを簡単に判断できます。  
  
## <a name="creating-test-and-training-sets-for-data-mining-structures"></a>データ マイニング構造のテストとトレーニング セットの作成  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では、マイニング構造のレベルで元のデータセットを分割します。 トレーニングとテストのデータセットのサイズ、どの行がどのセットに属するかなどに関する情報は、構造に格納され、その構造に基づくすべてのモデルで、これらのセットを使用してトレーニングとテストを行うことができます。  
  
 マイニング構造のテスト データセットは、次の方法で定義できます。  
  
-   マイニング構造は、その作成時にデータ マイニング ウィザードを使用して分割します。  
  
-   データ マイニング デザイナーの **[マイニング構造]** タブで、構造のプロパティを変更します。  
  
-   分析管理オブジェクト (AMO) または XML データ定義言語 (DDL) を使用し、プログラムによって構造を作成および変更します。  
  
### <a name="using-the-data-mining-wizard-to-divide-a-mining-structure"></a>データ マイニング ウィザードを使用したマイニング構造の分割  
 既定では、マイニング構造のデータ ソースを定義した後、データ マイニング ウィザードによって、ソース データの 70% がモデルのトレーニング用、30% がモデルのテスト用に分割されます。 この既定設定は、データ マイニングでは 70-30 の比率がよく使用されるために選択されていますが、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、独自の要件に合わせてこの比率を変更することもできます。  
  
 また、トレーニング ケースの最大数を設定するようにウィザードを構成したり、指定したケースの最大数まで最大割合を許可するように制限を組み合わせたりすることもできます。 ケースの最大割合と最大数の両方を指定した場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって、2 つの制限のうちの小さい方がテスト セットのサイズとして使用されます。 たとえば、テスト ケースに 30% の提示データを指定し、テスト ケースの最大数を 1000 に指定した場合、テスト セットのサイズが 1000 ケースを超えることはありません。 これを利用すると、モデルにトレーニング データが追加されてもテスト セットのサイズが一定に保たれるようにすることができます。  
  
 複数のマイニング構造に同じデータ ソース ビューを使用する場合、すべてのマイニング構造とそのモデルでほぼ同じようにデータが分割されるようにするには、ランダム サンプリングの初期化に使用するシードを指定します。 `HoldoutSeed` の値を指定すると、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によるサンプリングの開始時にその値が使用されます。 指定しないと、サンプリング時に、マイニング構造の名前に対してハッシュ アルゴリズムを使用してシード値が作成されます。  
  
> [!NOTE]  
>  `EXPORT` ステートメントおよび `IMPORT` ステートメントを使用してマイニング構造のコピーを作成すると、新しいマイニング構造でも同じトレーニング データセットとテスト データセットが使用されます。エクスポート プロセスでは新しい ID が作成されますが、同じ名前が使用されるためです。 一方、2 つのマイニング構造の基になるデータ ソースが同じでも、名前が異なる場合は、それぞれのマイニング構造に作成されるセットも異なります。  
  
### <a name="modifying-structure-properties-to-create-a-test-data-set"></a>テスト データセットの作成のための構造のプロパティの変更  
 マイニング構造を作成および処理した後にテスト データセットを確保する場合は、マイニング構造のプロパティを変更できます。 データのパーティション分割方法を変更するには、次のプロパティを編集します。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|`HoldoutMaxCases`|テスト セットに含めるケースの最大数を指定します。|  
|`HoldoutMaxPercent`|テスト セットに含めるケースの数を、データセット全体に対する割合で指定します。 データセットを含めないようにするには、0 を指定します。|  
|`HoldoutSeed`|パーティションのデータをランダムに選択するときにシードとして使用する整数値を指定します。 この値は、トレーニング セット内のケース数には影響を与えずに、パーティションを反復可能にします。|  
  
 既存の構造でテスト データセットを追加または変更した場合、構造および関連するすべてのモデルを再処理する必要があります。 また、ソース データを分割すると、異なるデータ サブセットでモデルがトレーニングされるようになるため、モデルの結果が変化する場合があります。  
  
### <a name="specifying-holdout-programmatically"></a>プログラムによる HOLDOUT の指定  
 DMX ステートメント、AMO、または XML DDL を使用すると、データ マイニング構造でテスト データセットおよびトレーニング データセットを定義できます。 ALTER MINING STRUCTURE ステートメントは、提示パラメーターの使用をサポートしていません。  
  
-   **DMX** データ マイニング拡張機能 (DMX) 言語では CREATE MINING STRUCTURE ステートメントが拡張されており、WITH HOLDOUT 句を使用できます。  
  
-   **ASSL** [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] スクリプト言語 (ASSL) を使用すると、マイニング構造を新しく作成することも、既存のデータ マイニング構造にテスト データセットを追加することもできます。  
  
-   **AMO** また、AMO を使用して予約データセットを表示および変更することもできます。  
  
 データ マイニング スキーマ行セットに対してクエリを実行すると、既存のマイニング構造内の予約データセットに関する情報を表示できます。 これを行うには、DISCOVER ROWSET を呼び出すか、DMX クエリを使用できます。  
  
## <a name="retrieving-information-about-holdout-data"></a>予約データに関する情報の取得  
 既定では、トレーニング データセットとテスト データセットに関する情報はすべてキャッシュされるので、既存のデータを使用して新しいモデルをトレーニングし、テストできます。 データのサブセットに対してモデルを評価できるように、キャッシュ済みの予約データに適用するフィルターをユーザーが定義することもできます。  
  
 ケースがどのようにトレーニング データセットおよびテスト データセットに分割されるかは、予約データの構成方法、および指定したデータによって異なります。 トレーニングまたはテストに使用されるケース数を確認する場合、またはトレーニング セットとテスト セットに含まれているケースの詳細を調べる場合は、DMX クエリを作成してモデル構造でクエリを実行します。 たとえば、次のクエリでは、モデルのトレーニング セットで使用されたケースが返されます。  
  
```  
SELECT * from <structure>.CASES WHERE IsTrainingCase()  
```  
  
 テスト ケースのみを取得し、さらにマイニング構造内のいずれかの列でテスト ケースをフィルター処理するには、次の構文を使用します。  
  
```  
SELECT * from <structure>.CASES WHERE IsTestCase() AND <structure column name> = '<value>'  
```  
  
## <a name="limitations-on-the-use-of-holdout-data"></a>予約データの使用に関する制限事項  
  
-   提示データを使用するには、マイニング構造の <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> プロパティが既定値の `KeepTrainingCases` に設定されている必要があります。 `CacheMode` プロパティを `ClearAfterProcessing` に変更してマイニング構造を再処理すると、パーティションが失われます。  
  
-   タイム シリーズ モデルからデータを削除することはできません。したがって、ソース データをトレーニング セットとテスト セットに分割することはできません。 マイニング構造とモデルの作成を開始し、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] タイム シリーズ アルゴリズムを選択すると、予約データセットを作成するオプションは無効になります。 また、ケース テーブル レベルまたは入れ子になったテーブル レベルで、マイニング構造に KEY TIME 列が含まれている場合も、予約データの使用が無効になります。  
  
-   データセット全体がテストに使用され、トレーニング用のデータが残らなくなるように予約データセットが誤って構成されることもあります。 ただし、この問題を修正できるように、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によりエラーが生成されます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] により警告が表示されます。  
  
-   多くの場合、提示データの既定値である 30 を使用すると、トレーニング データとテスト データのバランスがとれます。 十分なトレーニングのためにデータセットをどの程度大きくするか、また、オーバーフィットを回避するためにトレーニング セットをどの程度小さくするかを、単純に算出する方法はありません。 ただし、モデルを作成した後、クロス検証を使用して、特定のモデルについてデータセットを評価できます。  
  
-   AMO と XML DDL には、前の表に示したプロパティに加えて、読み取り専用プロパティ `HoldoutActualSize` が用意されています。 ただし、構造が処理されるまではパーティションの実際のサイズを正確に知ることができないため、`HoldoutActualSize` プロパティの値を取得する前に、モデルが処理済みであるかどうかを確認する必要があります。  
  
## <a name="related-content"></a>関連コンテンツ  
  
|トピック|リンク|  
|------------|-----------|  
|モデルに対するフィルターとトレーニング データセットおよびテスト データセットとの間の対話方法について説明します。|[マイニング モデルのフィルター (Analysis Services - データ マイニング)](mining-models-analysis-services-data-mining.md)|  
|トレーニング データとテスト データの使用が相互検証に与える影響について説明します。|[相互検証 &#40;Analysis Services - データ マイニング&#41;](cross-validation-analysis-services-data-mining.md)|  
|マイニング構造でのトレーニング セットとテスト セットの操作のためのプログラム インターフェイスに関する情報を提供します。|[AMO の概念とオブジェクト モデル](https://docs.microsoft.com/bi-reference/amo/amo-concepts-and-object-model)<br /><br /> [MiningStructure 要素 (ASSL)](https://docs.microsoft.com/bi-reference/assl/objects/miningstructure-element-assl)|  
|提示セットを作成するための DMX 構文について説明します。|[CREATE MINING STRUCTURE (DMX)](/sql/dmx/create-mining-structure-dmx)|  
|トレーニング セットとテスト セットのケースに関する情報を取得します。|[データ マイニング スキーマ行セット](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)<br /><br /> [データ マイニング スキーマ行セット クエリ&#40;Analysis Services - データ マイニング&#41;](data-mining-schema-rowsets-ssas.md)|  
  
## <a name="see-also"></a>参照  
 [データ マイニング ツール](data-mining-tools.md)   
 [データ マイニングの概念](data-mining-concepts.md)   
 [データ マイニング ソリューション](data-mining-solutions.md)   
 [テストおよび検証 (データ マイニング)](testing-and-validation-data-mining.md)  
  
  
