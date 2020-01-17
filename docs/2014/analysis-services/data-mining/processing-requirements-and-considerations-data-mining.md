---
title: 処理の要件および注意事項 (データ マイニング) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], objects
- mining structures [Analysis Services], processing
- mining models [Analysis Services], processing
ms.assetid: f7331261-6f1c-4986-b2c7-740f4b92ca44
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7bc06d5ece0b81ff3da9d41abb31e2c864a29f5e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083129"
---
# <a name="processing-requirements-and-considerations-data-mining"></a>処理の要件および注意事項 (データ マイニング)
  このトピックでは、データ マイニング オブジェクトを処理するときに注意するいくつかの技術的な考慮事項について説明します。 処理について、および処理がデータ マイニングに適用される方法に関する一般情報については、「 [データ マイニング オブジェクトの処理](processing-data-mining-objects.md)」を参照してください。  
  
 [リレーショナル ストアに対するクエリ](#bkmk_QueryReqs)  
  
 [マイニング構造の処理](#bkmk_ProcessStructures)  
  
 [マイニング モデルの処理](#bkmk_ProcessModels)  
  
##  <a name="bkmk_QueryReqs"></a> 処理中のリレーショナル ストアに対するクエリ  
 データ マイニングでの処理には、ソース データのクエリ、生の統計情報の特定、およびモデル定義とアルゴリズムを使用したマイニング モデルのトレーニングの 3 つの段階があります。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーは、生データを提供するデータベースに対してクエリを実行します。 そのデータベースは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 以前のバージョンの SQL Server データベース エンジンのインスタンスである場合もあります。 データ マイニング構造の処理時には、ソース内のデータがマイニング構造に転送され、圧縮形式でディスク上に新たに保存されます。 データ ソース内のすべての列が処理されるとは限りません。バインドの定義に従って、マイニング構造に含まれる列だけが処理されます。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] はそのデータを使用して、すべてのデータおよび離散化列のインデックスと、連続列のための別のインデックスを作成します。 入れ子になったテーブルごとに、インデックスを作成するためのクエリが実行され、入れ子になったテーブルとケース テーブルの各ペアの関係を処理するための追加のクエリが生成されます。 このように複数のクエリが作成されるのは、特殊な内部多次元データ ストアを処理するためです。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によってリレーショナル ストアに送信されるクエリの数を制限するには、サーバー プロパティの `DatabaseConnectionPoolMax` を設定します。 詳細については、「 [OLAP のプロパティ](../server-properties/olap-properties.md)」を参照してください。  
  
 モデルの処理時に、モデルは、データ ソースからデータを再度読み取るのではなく、マイニング構造からデータの概要を取得します。 サーバーは、作成されたキューブと、キャッシュされたインデックス データとケース データを使用して、モデルのトレーニングを行うための独立したスレッドを作成します。  
  
 各エディションの詳細については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]並列モデル処理をサポートするを参照してください[機能は、SQL Server 2012 の各エディションでサポートされている](https://go.microsoft.com/fwlink/?linkid=232473)(https://go.microsoft.com/fwlink/?linkid=232473) します。  
  
##  <a name="bkmk_ProcessStructures"></a> マイニング構造の処理  
 マイニング構造は、すべての依存モデルと一緒に処理することも、個別に処理することもできます。 処理に時間がかかると予想されるモデルがあり、その操作を保留する場合、モデルとは別にマイニング構造を処理すると便利です。  
  
 詳細については、「 [マイニング構造の処理](process-a-mining-structure.md)」を参照してください。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ではマイニング構造キャッシュがローカルに保持されるので、ハード ディスク領域を節約する場合は注意してください。 つまり、すべてのトレーニング データがローカル ハード ディスクに書き込まれます。 データをキャッシュしない場合は、マイニング構造の <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> プロパティを `ClearAfterProcessing` に設定することで、既定値を変更できます。 これにより、モデルを処理した後にキャッシュが破棄されます。また、マイニング構造のドリルスルーも無効になります。 詳細については、「[ドリルスルー クエリ &#40;データ マイニング&#41;](drillthrough-queries-data-mining.md)」を参照してください。  
  
 また、キャッシュを消去すると、提示されたテスト セット (定義している場合) を使用できなくなり、テスト セット パーティションの定義も失われます。 提示されたテスト セットの詳細については、「 [トレーニング データ セットとテスト データ セット](training-and-testing-data-sets.md)」を参照してください。  
  
##  <a name="bkmk_ProcessModels"></a> マイニング モデルの処理  
 関連付けられているマイニング構造とは別にマイニング モデルを処理することも、マイニング構造に基づくすべてのモデルをマイニング構造と共に処理することもできます。  
  
 詳細については、「 [マイニング モデルの処理](process-a-mining-model.md)」を参照してください。  
  
 ただし、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] および [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]では、マイニング構造と共に処理するマイニング モデルを複数選択することができません。 処理するモデルを制御する必要がある場合は、モデルを個別に選択するか、XMLA または DMX を使用してモデルを順番に処理する必要があります。  
  
## <a name="when-reprocessing-is-required"></a>再処理が必要な場合  
 モデルの操作を開始する前に、定義する [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] モデルを処理する必要があります。 また、マイニング モデル構造の変更、トレーニング データの更新、既存のマイニング モデルの変更、または構造への新しいマイニング モデルの追加を行った場合は、必ずマイニング モデルを再処理する必要があります。  
  
 マイニング モデルは、以下のシナリオでも処理されます。  
  
 **プロジェクトの配置**:によっては、プロジェクトの設定とプロジェクトの現在の状態の場合は、プロジェクトが配置されると、プロジェクト内のマイニング モデルを完全に処理されます通常。  
  
 配置を開始すると、以前に処理されたバージョンが [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーに存在して構造的に変更されていない場合を除き、処理が自動的に開始されます。 プロジェクトを配置するには、ドロップダウン リストから **[ソリューションの配置]** を選択するか、または F5 キーを押します。 次の操作を実行できます。  
  
 マイニング モデルの配置方法を制御する [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の配置プロパティの設定方法の詳細については、「 [データ マイニング ソリューションの配置](deployment-of-data-mining-solutions.md)」を参照してください。  
  
 **マイニング モデルの移動**:エクスポート コマンドを使用してマイニング モデルを移動すると、モデルにデータを提供する予定がマイニング構造の名前を含む、モデルの定義のみがエクスポートされます。  
  
 EXPORT コマンドと IMPORT コマンドを使用するシナリオとその再処理の要件を次に示します。  
  
-   移動先のインスタンスにマイニング構造が存在し、そのマイニング構造が未処理の状態にある場合。  
  
     構造とモデルの両方を再処理する必要があります。  
  
-   移動先のインスタンスにマイニング構造が存在し、そのマイニング構造が処理済みで、 マイニング モデルのみがエクスポートされた場合。  
  
     モデルは処理せずに使用できます。  
  
-   WITH DEENDENCIES キーワードを使用してマイニング構造の定義もエクスポートされた場合。  
  
     構造とモデルの両方を再処理する必要があります。  
  
 詳細については、「 [データ マイニング オブジェクトのエクスポートおよびインポート](export-and-import-data-mining-objects.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [マイニング構造 &#40;Analysis Services - データ マイニング&#41;](mining-structures-analysis-services-data-mining.md)   
 [マイニング構造 &#40;Analysis Services - データ マイニング&#41;](mining-structures-analysis-services-data-mining.md)   
 [多次元モデル オブジェクトの処理](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
