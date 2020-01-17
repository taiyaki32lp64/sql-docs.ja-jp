---
title: データ マイニング クエリ インターフェイス |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- predictions [Analysis Services], DMX prediction queries
- predictions [DMX]
- DMX [Analysis Services], prediction queries
- prediction queries [DMX]
- predictions [Analysis Services]
- queries [DMX], prediction queries
- mining models [Analysis Services], DMX
ms.assetid: a8952427-fd8c-4300-8f62-25f57ac1be0c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7c59d3a18c1fd36f82e8ea60e42d1b9f6e2f34c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084978"
---
# <a name="data-mining-query-interfaces"></a>データ マイニング クエリ インターフェイス
  データ マイニング クエリは、データ マイニング拡張機能 (DMX) の言語に基づいています。 DMX は、分類、リスク分析、推奨設定の生成、線形回帰などのすべての予測およびモデリングのタスクに使用できます。 またモデル処理時に生成されたパターンおよび統計を取得することもできます。  
  
 DMX を使用した予測クエリの構文は、[!INCLUDE[tsql](../../includes/tsql-md.md)] でのクエリの構文に似ています。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] と [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] のどちらにも、DMX 予測クエリの作成に便利なツールが用意されています。  
  
 このトピックでは、DMX によりデータ マイニング クエリを作成および実行するために使用するインターフェイスについて説明します。  
  
 [クエリ ツール](#bkmk_Tools)  
  
-   [予測クエリ ビルダー](#bkmk_Builder)  
  
-   [クエリ エディター](#bkmk_QueryEditor)  
  
-   [[DMX テンプレート]](#bkmk_Templates)  
  
-   [Integration Services](#bkmk_SSIS)  
  
 [アプリケーション プログラミング インターフェイス](#bkmk_API)  
  
##  <a name="bkmk_Tools"></a> データ マイニング クエリ ツール  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、データ マイニング オブジェクトに対する、予測クエリ、コンテンツ クエリ、およびデータ定義クエリのビルドに使用できる次のツールが用意されています。  
  
-   予測クエリ ビルダー  
  
-   クエリ エディター  
  
-   DMX テンプレート  
  
-   Integration Services データ マイニング コンポーネント  
  
###  <a name="bkmk_Builder"></a> 予測クエリ ビルダー  
 予測クエリ ビルダーは、データ マイニング デザイナーの **[マイニング モデル予測]** タブに含まれ、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]および [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で入手できます。  
  
 クエリ ビルダーでは、グラフィカルなツールを使用して、マイニング モデルの選択、新しいケース データの追加、予測関数の追加などの操作を実行できます。 テキスト エディター、クエリを手動で変更するために使用できると、単純な予測クエリ ビルダーが含まれます**結果**クエリの結果を表示するウィンドウ。  
  
###  <a name="bkmk_QueryEditor"></a> クエリ エディター  
 クエリ エディターでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]をビルドして DMX クエリの実行に使用できるツールを提供します。 SQL Server Analysis Services のインスタンスに接続して、データベース、マイニング構造列、およびマイニング モデルを選択できます。 **メタデータ エクスプ ローラー** には、参照できる予測関数の一覧が含まれています。  
  
###  <a name="bkmk_Templates"></a> [DMX テンプレート]  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、DMX クエリの作成に使用できる対話型の DMX クエリ テンプレートが提供されます。 テンプレートの一覧を表示するには、ツール バーの **[表示]** をクリックし、 **[テンプレート エクスプローラー]** を選択します。 DMX、MDX、および XMLA のテンプレートを含むすべての Analysis Services テンプレートを表示するには、キューブ アイコンをクリックします。  
  
 テンプレートを使用してクエリをビルドするには、開いているクエリ ウィンドウにテンプレートをドラッグするか、テンプレートをダブルクリックして新しい接続と新しいクエリ ペインを開きます。  
  
 テンプレートから予測クエリを作成する方法の例については、「 [テンプレートからの単一予測クエリの作成](create-a-singleton-prediction-query-from-a-template.md)」を参照してください。  
  
> [!WARNING]  
>  Microsoft Office Excel データ マイニング アドインにも多くのクエリ テンプレートが含まれ、複雑な DMX ステートメントを作成するための対話形式のクエリ ビルダーも提供されます。 テンプレートを使用するには、データ マイニング クライアントで **[クエリ]** と **[詳細設定]** を順にクリックします。  
  
###  <a name="bkmk_SSIS"></a> Integration Services データ マイニング コンポーネント  
 予測クエリを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの一部として含めることもできます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の次のタスクおよび変換では、DMX 予測クエリと DMX ステートメントの作成と実行がサポートされます。  
  
|コンポーネント|説明|  
|---------------|-----------------|  
|データ マイニング クエリ タスク|DMX クエリおよびその他の DMX ステートメントを制御フローの一部として実行します。<br /><br /> タスク エディターには、予測クエリ ビルダーと、手動で DMX クエリを変更するためのテキスト ボックスがあります。 ただし、タスク エディターでは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ソリューションでのオブジェクトに対するクエリを検証できません。 このため、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] または [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] でクエリを作成してから、ステートメントまたはクエリのテキストをタスク エディターに貼り付けることをお勧めします。|  
|データ マイニング クエリ変換|データ フロー ソースから渡されるデータを使用してデータ フロー内で予測クエリを実行します。<br /><br /> タスク エディターには、予測クエリ ビルダーと、手動で DMX クエリを変更するためのテキスト ボックスがあります。<br /><br /> 変換を使用できるのは、データ フローのデータを使用するクエリ (つまり、PREDICTION JOIN 構文を使用するクエリ) を作成する場合のみです。 このコンポーネントは、コンテンツ クエリまたはその他の種類の DMX ステートメントの実行には使用できません。|  
  
##  <a name="bkmk_API"></a> アプリケーション プログラミング インターフェイス  
 さまざまなプログラミング言語を使用し、OLE DB、Analysis Services ADOMD クライアントなどのサーバー プロトコルを組み合わせ、データ マイニング モデルに対してクエリを実行するカスタム アプリケーションを作成できます。 詳細については、「 [データ マイニングのプログラミング](../dev-guide/data-mining-programming.md)」を参照してください。  
  
 ただし、XMLA は、Analysis Service サーバーとのすべてのやり取りのもとになるメッセージ形式を構成します。 XMLA メッセージ内では、DMX に基づく予測クエリ、コンテンツ クエリ、またはデータ マイニング スキーマ行セットを使用してモデル メタデータを取得するクエリのどれを送信しているかにより、クエリの表示の方法が異なります。  
  
-   **予測クエリ** (および他のすべての DMX ステートメント) のテキストは、[Execute (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) メソッドを使用し、XMLA [Command (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/command-element-xmla) 要素の [Statement (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) 要素内のテキストとして配置される DMX クエリと共に、XMLA で送信されます。  
  
-   クラスター数、デシジョン ツリーで使用される属性、モデルの最終処理日、モデル作成時に使用されるアルゴリズム パラメーターなどの**モデル コンテンツ**および**モデル メタデータ**を取得するには、[Discover (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) メソッドを使用し、[RequestType (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla) ヘッダーでデータ マイニング スキーマ行セットの 1 つを指定します。 クエリの範囲を絞り込むには、基準を [RestrictionList (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictionlist-element-xmla) 要素の制限として入力します。  
  
## <a name="see-also"></a>参照  
 [データ マイニング拡張機能 (DMX) リファレンス](/sql/dmx/data-mining-extensions-dmx-reference)   
 [データ マイニング ソリューション](data-mining-solutions.md)   
 [DMX 選択ステートメントについて](/sql/dmx/understanding-the-dmx-select-statement)   
 [構造と DMX 予測クエリの使用](/sql/dmx/structure-and-usage-of-dmx-prediction-queries)   
 [予測クエリ ビルダーを使用した予測クエリの作成](create-a-prediction-query-using-the-prediction-query-builder.md)   
 [SQL Server Management Studio で DMX クエリを作成する](create-a-dmx-query-in-sql-server-management-studio.md)  
  
  
