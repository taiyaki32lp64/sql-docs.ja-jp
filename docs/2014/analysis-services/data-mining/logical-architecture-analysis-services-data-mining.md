---
title: 論理アーキテクチャ (Analysis Services - データ マイニング) |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], about mining structures
- logical architecture [Data Mining]
- architecture [Analysis Services], mining models
- mining models [Analysis Services], about data mining models
- architecture [Analysis Services]
ms.assetid: 4e0cbf46-cc60-4e91-a292-9a69f29746f0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5702e3e2e5b12edecff4dd6d6f46b632575d211d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084264"
---
# <a name="logical-architecture-analysis-services---data-mining"></a>論理アーキテクチャ (Analysis Services - データ マイニング)
  データ マイニングは、複数のコンポーネントの相互作用を伴うプロセスです。  
  
-   SQL Server データベース内のデータのソースまたはその他のデータ ソースにアクセスし、トレーニング、テスト、または予測に使用します。  
  
-   データ マイニング構造とデータ マイニング モデルは、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] または Visual Studio を使用して定義します。  
  
-   データ マイニング オブジェクトの管理および予測やクエリの作成には、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用します。  
  
-   ソリューションが完成したら、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスにそのソリューションを配置します。  
  
 これらのソリューション オブジェクトを作成するプロセスについては、既に他の場所で説明しています。 詳細については、「 [データ マイニング ソリューション](data-mining-solutions.md)」を参照してください。  
  

  
##  <a name="bkmk_SourceData"></a> データ マイニング ソース データ  
 データ マイニングで使用するデータは、データ マイニング ソリューションに格納されません。バインドのみが格納されます。 データは前のバージョンの SQL Server、CRM システム、またはフラット ファイルで作成されたデータベースにも存在する場合があります。 処理によって構造またはモデルをトレーニングすると、データの統計サマリーが作成され、キャッシュに格納されます。そのサマリーは、後の操作で使用するために保持することも、処理後に削除することもできます。 詳細については、「[マイニング構造 (Analysis Services - データ マイニング)](mining-structures-analysis-services-data-mining.md)」を参照してください。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ ソース ビュー (DSV) オブジェクト内のさまざまなデータを組み合わせることで、データ ソースの上に抽象化レイヤーが提供されます。 テーブル間の結合を指定できます。また、多対一のリレーションシップを持つテーブルを追加して、入れ子になったテーブル列を作成することができます。 これらのオブジェクト (データ ソースおよびデータ ソース ビュー) の定義は、*.ds および \*.dsv というファイル名拡張子でソリューション内に保存されます。 作成と使用の詳細については[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]データ ソースおよびデータ ソース ビューを参照してください。[サポートされるデータ ソース&#40;SSAS 多次元&#41;](../multidimensional-models/supported-data-sources-ssas-multidimensional.md)します。  
  
 AMO または XMLA を使用して、データ ソースおよびデータ ソース ビューを定義および変更することもできます。 プログラムによってこれらのオブジェクトを操作する方法の詳細については、「[論理アーキテクチャの概要 (Analysis Services - 多次元データ)](../multidimensional-models/olap-logical/logical-architecture-overview-analysis-services-multidimensional-data.md)」を参照してください。  
  

  
##  <a name="bkmk_Structures"></a> Mining Structures  
 データ マイニング構造は、マイニング モデルの作成元のデータ ドメインを定義する論理データ コンテナーです。 1 つのマイニング構造で複数のマイニング モデルをサポートできます。  
  
 データ マイニング ソリューションでデータを使用する必要がある場合、Analysis Services ではソースからデータを読み込み、集計およびその他の情報のキャッシュを生成します。 既定では、トレーニング データを再利用して追加のモデルをサポートできるように、このキャッシュは保持されます。 キャッシュを削除する必要がある場合は、マイニング構造オブジェクトの `CacheMode` プロパティを値 `ClearAfterProcessing` に変更します。 詳細については、「 [AMO データ マイニング クラス](https://docs.microsoft.com/bi-reference/amo/amo-data-mining-classes)」を参照してください。  
  
 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] には、データをトレーニングおよびテスト データ セットに分割する機能もあります。この機能を使用して、代表的な、ランダムに選択したデータのセットでマイニング モデルをテストできます。 データは、実際には別々に格納されません。構造キャッシュ内のケース データには、その特定のケースがトレーニングに使用されるかテストに使用されるかを示すプロパティが設定されます。 キャッシュを削除すると、その情報を取得できなくなります。  
  
 詳細については、「[マイニング構造 (Analysis Services - データ マイニング)](mining-structures-analysis-services-data-mining.md)」を参照してください。  
  
 データ マイニング構造には、入れ子になったテーブルを含めることができます。 入れ子になったテーブルは、プライマリ データ テーブルでモデル化されているケースに関する追加の詳細情報を提供します。 詳細については、「[入れ子になったテーブル &#40;Analysis Services - データ マイニング&#41;](nested-tables-analysis-services-data-mining.md)」をご覧ください。  
  
 
  
##  <a name="bkmk_Models"></a> Mining Models  
 処理前のデータ マイニング モデルは、メタデータのプロパティの組み合わせにすぎません。 これらのプロパティでは、マイニング構造とデータ マイニング アルゴリズムを指定し、データの処理方法に影響するパラメーターとフィルター設定のコレクションを定義します。 詳細については、「[入れ子になったテーブル (Analysis Services - データ マイニング)](mining-models-analysis-services-data-mining.md)」を参照してください。  
  
 モデルを処理すると、マイニング構造のキャッシュに格納されたトレーニング データを使用して、データの統計プロパティと、アルゴリズムおよびそのパラメーターによって定義されたヒューリスティックの両方に基づいたパターンが生成されます。 これは、モデルの *トレーニング* と呼ばれます。  
  
 トレーニングの結果は、見つかったパターンを表し、予測を生成するルールを提供する一連の概要データで、*モデル コンテンツ*に格納されます。 詳細については、「[マイニング モデル コンテンツ (Analysis Services - データ マイニング)](mining-model-content-analysis-services-data-mining.md)」を参照してください。  
  
 限られた状況では、標準形式である Predictive Model Markup Language (PMML) に従ってモデルの数式とデータ バインドを表すファイルにモデルの論理構造をエクスポートすることもできます。 PMML を使用する他のシステムにこの論理構造をインポートし、そのモデルを予測に使用することができます。 詳細については、「 [DMX 選択ステートメントについて](/sql/dmx/understanding-the-dmx-select-statement)」を参照してください。  
  

  
##  <a name="bkmk_CustomObjects"></a> カスタム データ マイニング オブジェクト  
 精度チャート、予測クエリなど、データ マイニング プロジェクトのコンテキストで使用するその他のオブジェクトは、ソリューション内に保存されませんが、ASSL を使用してスクリプト化することや、AMO を使用して作成することができます。  
  
 また、これらのカスタム オブジェクトを追加することで、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスで利用可能なサービスと機能を拡張することもできます。  
  
 **カスタム アセンブリ**  
 .NET アセンブリは、CLR または COM に準拠した任意の言語を使用して定義した後、SQL Server のインスタンスに登録できます。 アセンブリ ファイルは、アプリケーションで定義された場所から読み込まれ、コピーは、データと共にサーバーに保存されます。 アセンブリ ファイルのコピーは、サービスが開始されるたびにアセンブリを読み込むために使用されます。  
  
 詳細については、「 [多次元モデルのアセンブリの管理](../multidimensional-models/multidimensional-model-assemblies-management.md)」を参照してください。  
  
 **カスタム ストアド プロシージャ**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のデータ マイニングでは、ストアド プロシージャを使用して、データ マイニング オブジェクトを操作できます。 独自のストアド プロシージャを作成して、機能を拡張し、予測クエリおよびコンテンツ クエリから返されるデータをより簡単に操作できます。  
  
 [ストアド プロシージャの定義](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
 次のストアド プロシージャを使用して、クロス検証を実行できます。  
  
 [データ マイニングのストアド プロシージャ (Analysis Services - データ マイニング)](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)  
  
 また、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] には、内部でデータ マイニングに使用されるシステム ストアド プロシージャが多数用意されています。 システム ストアド プロシージャは内部で使用するためのものですが、それらを応用することもできます。 これらのストアド プロシージャは、マイクロソフトによって随時変更される場合があります。そのため、実際の運用では、DMX、AMO、または XMLA を使用してクエリを作成することをお勧めします。  
  
 **カスタム プラグイン アルゴリズム**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] には、独自のアルゴリズムを作成し、そのアルゴリズムを新しいデータ マイニング サービスとしてサーバー インスタンスに追加するためのメカニズムが用意されています。  
  
 Analysis Services では、COM インターフェイスを使用して、プラグイン アルゴリズムと通信します。 新しいアルゴリズムの実装方法の詳細については、「 [プラグイン アルゴリズム](plugin-algorithms.md)」を参照してください。  
  
 新しいアルゴリズムはそれぞれ使用する前に登録する必要があります。 アルゴリズムを登録するには、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]インスタンスの .ini ファイルにアルゴリズムに必要なメタデータを追加します。 新しいアルゴリズムを使用する各インスタンスに情報を追加する必要があります。 アルゴリズムを追加したら、インスタンスを再起動し、MINING_SERVICES スキーマ行セットを使用して、新しいアルゴリズムを表示し、そのアルゴリズムでサポートされているオプション、プロバイダーなどを確認できます。  
  

  
## <a name="see-also"></a>参照  
 [多次元モデル オブジェクトの処理](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; リファレンス](/sql/dmx/data-mining-extensions-dmx-reference)  
  
  
