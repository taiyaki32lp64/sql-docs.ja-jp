---
title: 論理アーキテクチャの概要 (Analysis Services-多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- cubes [Analysis Services], examples
- cubes [Analysis Services], about cubes
ms.assetid: 1a547bce-dacf-4d32-bc0f-3829f4b026e1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b4eea3e75ed57dcf69c8d8c5bcaedf3aef1fa9f5
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797641"
---
# <a name="logical-architecture-overview-analysis-services---multidimensional-data"></a>論理アーキテクチャの概要 (Analysis Services - 多次元データ)
  Analysis Services は、さまざまな種類の Analysis Services モデルで使用されるメモリ アーキテクチャとランタイム環境を指定する、サーバー配置モードで動作します。 サーバー モードは、インストール時に決定されます。 **多次元およびデータマイニングモードで**は、従来の OLAP およびデータマイニングがサポートされます。 **表形式モード**では、テーブルモデルがサポートされます。 **SharePoint 統合モード**は、ブック内の Excel または PowerPivot データモデルの読み込みとクエリを実行するために使用される PowerPivot for SharePoint としてインストールされた Analysis Services のインスタンスを参照します。  
  
 このトピックでは、多次元モードとデータ マイニング モードで動作する場合の Analysis Services の基本アーキテクチャについて説明します。 他のモードの詳細については、「 [ &#40;テーブル&#41;モデリング ssas テーブル](../../tabular-models/tabular-models-ssas.md)」と「[テーブルソリューションと多次元ソリューション&#40;の比較 (ssas&#41;](https://docs.microsoft.com/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas))」を参照してください。  
  
## <a name="basic-architecture"></a>基本アーキテクチャ  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] のインスタンスには、複数のデータベースを含めることができます。また、1 つのデータベース内に OLAP オブジェクトとデータ マイニング オブジェクトを同時に格納できます。 アプリケーションは、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] の指定インスタンスおよび指定データベースに接続します。 サーバー コンピューターは [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] の複数のインスタンスをホストできます。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] のインスタンスには、"\<ServerName >\\< InstanceName\>" という名前が付けられます。 次の図は、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] オブジェクト間のすべての関係を示しています。  
  
 ![AMO 実行オブジェクトの関係](../../dev-guide/media/amo-runningobjects.gif "AMO 実行オブジェクトの関係")  
  
 基本クラスは、キューブの構築に必要な最小限のオブジェクト セットです。 この最小限のオブジェクト セットは、ディメンション、メジャー グループ、およびパーティションです。 集計は省略可能です。  
  
 ディメンションは、属性および階層から構築されます。 階層は、順序付けされた属性のセットで形成されます。セット内の各属性が、階層内の 1 つのレベルに対応します。  
  
 キューブは、ディメンションおよびメジャー グループから構築されます。 キューブのディメンション コレクション内のディメンションは、データベースのディメンション コレクションに属しています。 メジャー グループは、同じデータ ソース ビューおよびキューブのディメンションの同じサブセットを持つ、メジャーのコレクションです。 1 つのメジャー グループには、物理データを管理するパーティションが 1 つ以上あります。 メジャー グループには、既定の集計デザインを指定できます。 既定の集計デザインを、メジャー グループ内のすべてのパーティションに使用できます。また、各パーティションに独自の集計デザインを使用することもできます。  
  
 Server オブジェクト  
 AMO では、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] の各インスタンスが別個のサーバー オブジェクトとして認識されます。各インスタンスは、それぞれ異なる接続によって <xref:Microsoft.AnalysisServices.Server> オブジェクトに接続されます。 各サーバー オブジェクトには、1 つ以上のデータ ソース、データ ソース ビュー、データベース オブジェクト、アセンブリ、およびセキュリティ ロールが含まれています。  
  
 Dimension オブジェクト  
 各データベース オブジェクトには複数のディメンション オブジェクトが含まれています。 各ディメンション オブジェクトには 1 つ以上の属性が含まれ、属性は階層で構成されます。  
  
 [キューブ オブジェクト]  
 各データベース オブジェクトには 1 つ以上のキューブ オブジェクトが含まれています。 キューブは、メジャーとディメンションによって定義されます。 キューブのメジャーとディメンションは、そのキューブの基になっているか、またはメジャー定義とディメンション定義から生成されたデータ ソース ビュー内のテーブルおよびビューから派生します。  
  
## <a name="object-inheritance"></a>オブジェクトの継承  
 ASSL オブジェクト モデルには繰り返される多くの要素グループがあります。 たとえば、要素グループ "`Dimensions` には `Hierarchies` が含まれます" は、要素のディメンション階層を定義します。 `Cubes` と `MeasureGroups` のどちらにも、"`Dimensions` contain `Hierarchies`" という要素グループがあります。  
  
 明示的にオーバーライドされない限り、要素はこれらの繰り返される要素グループの詳細を上位レベルから継承します。 たとえば、`Translations` の `CubeDimension` は、先祖要素である `Translations` の `Cube` と同じです。  
  
 上位レベルのオブジェクトから継承されるプロパティを明示的にオーバーライドするには、オブジェクトで上位レベルのオブジェクトの構造全体およびプロパティを明示的に繰り返す必要はありません。 オブジェクトで明示的に記述する必要があるプロパティは、オーバーライドするプロパティだけです。 たとえば、`CubeDimension` では、`Hierarchies` で無効にする必要がある場合、表示と非表示を切り替える必要がある場合、または一部の `Cube` 詳細が `Level` レベルで指定されない場合にのみ、`Dimension` を一覧表示します。  
  
 オブジェクトで指定される一部のプロパティによって、子オブジェクトや子孫オブジェクトの同じプロパティの既定値が指定されます。 たとえば、`Cube.StorageMode` は `Partition.StorageMode` に既定値を提供します。 ASSL では、継承された既定値について次のルールが適用されます。  
  
-   子オブジェクトのプロパティが XML で NULL の場合、そのプロパティの既定値は継承された値になります。 ただし、サーバーから値をクエリする場合は、XML 要素の NULL 値が返されます。  
  
-   子オブジェクトのプロパティが子オブジェクトで直接設定されたか、または継承されたかをプログラムで判断することはできません。  
  
## <a name="example"></a>例  
 Imports キューブには、Packages と Last という 2 つのメジャーと、Route、Source、および Time という 3 つの関連ディメンションが含まれています。  
  
 ![Cube の例1](../../dev-guide/media/cubeintro1.gif "Cube の例1")  
  
 キューブの周囲の小さい英数字の値はディメンションのメンバーです。 この例のメンバーは、ground (Route ディメンションのメンバー)、Africa (Source ディメンションのメンバー)、および 1st quarter (Time ディメンションのメンバー) です。  
  
### <a name="measures"></a>メジャー グループ  
 キューブ セル内の値は、Packages と Last という 2 つのメジャーを表します。 Packages メジャーは輸入されるパッケージ数を表し、`Sum` 関数はファクトを集計するために使用されます。 Last メジャーは受入日を表し、`Max` 関数はファクトを集計するために使用されます。  
  
### <a name="dimensions"></a>Dimensions  
 Route ディメンションは、輸入品が宛先に搬送される手段を表します。 このディメンションのメンバーには、ground、nonground、air、sea、road、rail があります。 Source ディメンションは、Africa または Asia など、輸入品の製造場所を表します。 Time ディメンションは、年間の四半期と上半期または下半期を表します。  
  
### <a name="aggregates"></a>集計  
 キューブのビジネス ユーザーは、ディメンション内のメンバーのレベルに関係なく、すべてのディメンションのメンバーごとにすべてのメジャーの値を決定できます。これは、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] が必要に応じて上位レベルで値を集計するためです。 たとえば、前の図のメジャー値は、次の図に示すように、時間ディメンションの Calendar Time 階層を使用して、標準のカレンダー階層に従って集計できます。  
  
 ![時間ディメンションに従って編成されたメジャーのダイアグラム](../../dev-guide/media/cubeintro2.gif "時間ディメンションに従って編成されたメジャーのダイアグラム")  
  
 1 つのディメンションを使用してメジャーを集計するだけでなく、さまざまなディメンションのメンバーを組み合わせて使用し、メジャーを集計できます。 これにより、ビジネス ユーザーは複数のディメンション内で同時にメジャーを評価できます。 たとえば、ビジネス ユーザーが Eastern Hemisphere と Western Hemisphere から air によって搬送された輸入品を四半期別に分析する必要があれば、キューブ上でクエリを実行して次のデータセットを取得できます。  
  
||||パッケージ|||Last|||  
|-|-|-|--------------|-|-|----------|-|-|  
||||All Sources|Eastern Hemisphere|Western Hemisphere|All Sources|Eastern Hemisphere|Western Hemisphere|  
|All Time|||25110|6547|18563|Dec-29-99|Dec-22-99|Dec-29-99|  
||1st half||11173|2977|8196|Jun-28-99|6月 ~ 20-99|Jun-28-99|  
|||1st quarter|5108|1452|3656|Mar-30-99|3月 ~ 19-99|Mar-30-99|  
|||2nd quarter|6065|1525|4540|Jun-28-99|6月 ~ 20-99|Jun-28-99|  
||2nd half||13937|3570|10367|Dec-29-99|Dec-22-99|Dec-29-99|  
|||3rd quarter|6119|1444|4675|Sep-30-99|Sep-18-99|Sep-30-99|  
|||4th quarter|7818|2126|5692|Dec-29-99|Dec-22-99|Dec-29-99|  
  
 キューブを定義した後、新しい集計を作成したり、既存の集計を変更して、集計を処理時に事前計算するかクエリ時に計算するかなどを指定するオプションを設定することができます。 **関連トピック:** [集計と集計デザイン](../../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)。  
  
### <a name="mapping-measures-attributes-and-hierarchies"></a>メジャー、属性、および階層のマッピング  
 キューブの例のメジャー、属性、および階層は、キューブのファクト テーブルおよびディメンション テーブルの次の列から派生します。  
  
|メジャーまたは属性 (レベル)|メンバー|基になるテーブル|基になる列|サンプル列の値|  
|------------------------------------|-------------|------------------|-------------------|-------------------------|  
|パッケージメジャー|適用なし|ImportsFactTable|パッケージ|12|  
|Last メジャー|適用なし|ImportsFactTable|Last|May-03-99|  
|Route ディメンションの Route_Category レベル|nonground、ground|RouteDimensionTable|Route_Category|Nonground|  
|Route ディメンションの Route 属性|air、sea、road、rail|RouteDimensionTable|Route|Sea|  
|Source ディメンションの Hemisphere 属性|Eastern Hemisphere、Western Hemisphere|SourceDimensionTable|Hemisphere|Eastern Hemisphere|  
|Source ディメンションの Continent 属性|Africa,Asia,AustraliaEurope,N. America,S. America|SourceDimensionTable|Continent|Europe|  
|Time ディメンションの Half 属性|1st half、2nd half|TimeDimensionTable|Half|2nd half|  
|Time ディメンションの Quarter 属性|1st quarter、2nd quarter、3rd quarter、4th quarter|TimeDimensionTable|Quarter|3rd quarter|  
  
 通常、1 つのキューブ セルのデータは、ファクト テーブルの複数行から派生します。 たとえば、air メンバー、アフリカメンバー、第1四半期のメンバーの交差部分にあるキューブセルには、 **ImportsFactTable**ファクトテーブル内の次の行を集計することによって得られる値が含まれています。  
  
|||||||  
|-|-|-|-|-|-|  
|Import_ReceiptKey|RouteKey|SourceKey|TimeKey|パッケージ|Last|  
|3516987|@shouldalert|6|@shouldalert|15|Jan-10-99|  
|3554790|@shouldalert|6|@shouldalert|40|Jan-19-99|  
|3572673|@shouldalert|6|@shouldalert|34|Jan-27-99|  
|3600974|@shouldalert|6|@shouldalert|45|Feb-02-99|  
|3645541|@shouldalert|6|@shouldalert|20|Feb-09-99|  
|3674906|@shouldalert|6|@shouldalert|36|Feb-17-99|  
  
 上の表では、行ごとに、 **Routekey**、 **sourcekey**、および**timekey**列の値が同じで、これらの行が同じキューブセルに寄与することを示しています。  
  
 ここで示す例は、非常に単純なキューブを表します。つまり、キューブに 1 つのメジャー グループがあり、すべてのディメンション テーブルがスター スキーマのファクト テーブルに結合されています。 別の一般的なスキーマとして、スノーフレーク スキーマがあります。このスキーマでは、1 つ以上のディメンション テーブルがファクト テーブルに直接結合されるのではなく、それぞれ別のディメンション テーブルに結合されます。 **関連トピック:** [ディメンション&#40;Analysis Services-多次元データ&#41;](../../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)。  
  
 ここで示す例には、1 つのファクト テーブルだけが含まれています。 キューブに複数のファクト テーブルがある場合、各ファクト テーブルからのメジャーはメジャー グループに編成され、メジャー グループは定義済みのディメンション リレーションシップによって、特定のセットのディメンションに関連付けられます。 これらのリレーションシップは、データ ソース ビューの参加テーブルとリレーションシップの粒度を指定することによって定義します。 **関連トピック:** [ディメンションリレーションシップ](../../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)。  
  
## <a name="see-also"></a>「  
 [多次元モデル データベース &#40;SSAS&#41;](../multidimensional-model-databases-ssas.md)  
  
  
