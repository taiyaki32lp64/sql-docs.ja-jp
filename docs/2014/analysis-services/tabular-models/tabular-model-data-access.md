---
title: 表形式モデルのデータ アクセス |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6ae74a8b-0025-450d-94a5-4e601831d420
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5bf8d4af44f7596bb632a05483c387752ba2e056
ms.sourcegitcommit: 0818f6cc435519699866db07c49133488af323f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284858"
---
# <a name="tabular-model-data-access"></a>テーブル モデル データ アクセス
  Analysis Services のテーブル モデル データベースは、多次元モデルからデータまたはメタデータを取得するときとほぼ同じクライアント、インターフェイス、および言語でアクセスできます。 詳細については、「[Multidimensional Model Data Access (Analysis Services - Multidimensional Data)](../multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)」(多次元モデルのデータ アクセス (Analysis Services - 多次元データ)) を参照してください。  
  
 このトピックでは、テーブル モデルを操作するクライアント、クエリ言語、およびプログラム インターフェイスについて説明します。  
  
## <a name="clients"></a>クライアント  
 次の Microsoft 製クライアント アプリケーションでは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のテーブル モデル データベースに対するネイティブ接続がサポートされます。  
  
### <a name="excel"></a>[エクスポート]  
 テーブル モデルのデータベースには Excel から接続できます。Excel にあるデータの視覚エフェクトと分析機能を使用してデータを操作することができます。 データにアクセスするには、Analysis Services のデータ接続を定義し、表形式サーバー モードで動作するサーバーを指定してから、使用するデータベースを選択します。 詳細については、「 [SQL Server Analysis Services のデータに接続する、または SQL Server Analysis Services のデータをインポートする](https://go.microsoft.com/fwlink/?linkID=215150)」を参照してください。  
  
 また、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]でテーブル モデルを参照する用途にも Excel は適しています。 このツールには、 **[Excel で分析]** というオプションがあります。このオプションを選択すると、新しい Excel インスタンスが起動して Excel ブックが作成され、そのブックからモデル ワークスペース データベースへのデータ接続が開きます。 Excel でテーブル モデル データを参照する際は、モデルに対するクエリが、Excel PivotTable クライアントを使用して実行される点に注意してください。 したがって、Excel ブック内の操作は、DAX クエリではなく、MDX クエリとしてワークスペース データベースに送信されます。 SQL Profiler などの監視ツールを使用してクエリを監視したとき、プロファイラー トレースに表示されるのは DAX ではなく MDX です。 "Excel で分析" 機能の詳細については、「[Excel で分析 (SSAS テーブル)](analyze-in-excel-ssas-tabular.md)」を参照してください。  
  
### <a name="power-view"></a>Power View  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] は、Reporting Services のレポート クライアント アプリケーションであり、SharePoint 2010 環境で動作します。 データ探索、クエリ デザイン、プレゼンテーション レイアウトが、アドホック レポート環境に統合されています。 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] は、テーブル モデルをデータ ソースとして使用することができます。そのモデルが、テーブル モードで動作する Analysis Services のインスタンスにホストされているか、DirectQuery モードを使用してリレーショナル データ ストアから取得されるかは関係ありません。 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]でテーブル モデルに接続するには、サーバーの場所とデータベース名を格納する接続ファイルを作成する必要があります。 Reporting Services の共有データ ソースまたは BI Semantic Model の接続ファイルは SharePoint で作成することができます。 BI セマンティック モデル接続の詳細については、次を参照してください。 [PowerPivot BI セマンティック モデル接続&#40;.bism&#41;](../power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)します。  
  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] クライアントは特定のモデルの構造を判断する際、指定されたデータ ソースに要求を送信し、データ ソースからスキーマを取得します。このスキーマを使用することで、データ ソースとしてのモデルに対するクエリを作成し、そのデータを基に処理を実行することができます。 以後、データのフィルター処理、計算や集計、関連付けられたデータの表示など、 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] ユーザー インターフェイスで実行される操作はクライアントによって制御され、プログラムから操作することはできません。  
  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] クライアントからモデルへと送信されるクエリは DAX ステートメントとして発行され、モデルにトレースを設定することによって監視できます。  クライアントは、概念スキーマ定義言語 (CSDL) に従って提示される初期スキーマ定義をサーバーに要求しますが、その際にも、サーバーに要求を送信します。 詳細については、「 [CSDL Annotations for Business Intelligence &#40;CSDLBI&#41;](https://docs.microsoft.com/bi-reference/csdl/csdl-annotations-for-business-intelligence-csdlbi)  
  
### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、テーブル モデルをホストするインスタンスの管理や、テーブル モデル内のメタデータおよびデータに対するクエリを行うことができます。 モデルやモデル内のオブジェクトの処理、パーティションの作成と管理、さらには、データ アクセスを管理するためのセキュリティの設定を行うこともできます。 詳細については、次の各トピックを参照してください。  
  
-   [Analysis Services インスタンスのサーバー モードの決定](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
-   [Analysis Services への接続](../instances/connect-to-analysis-services.md)  
  
-   [Analysis Services インスタンスの監視](../instances/monitor-an-analysis-services-instance.md)  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、MDX と XMLA の両方のクエリ ウィンドウを使用して、テーブル モデル データベースからデータやメタデータを取得することができます。 ただし、次の制限事項に注意してください。  
  
-   DirectQuery モードで配置されているモデルに対しては、MDX および DMX を使用したステートメントはサポートされません。したがって、DirectQuery モードのテーブル モデルに対するクエリを作成する必要がある場合は、 **[XMLA クエリ]** ウィンドウを使用する必要があります。  
  
-   **[クエリ]** ウィンドウを開いた後で、[XMLA クエリ] ウィンドウのデータベース コンテキストを変更することはできません。 したがって、異なるデータベースまたは異なるインスタンスにクエリを送信する必要がある場合は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してデータベースまたはインスタンスを開き、そのコンテキスト内で新しい **[XMLA クエリ]** ウィンドウを開く必要があります。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] テーブル モデルに対するトレースは、多次元ソリューションと同様に作成することができます。 このリリースの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] には、メモリ使用量やクエリ操作、処理中の操作、ファイルの使用状況を追跡するための新しいイベントが数多く用意されています。 詳細については、「 [Analysis Services トレース イベント](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)」を参照してください。  
  
> [!WARNING]  
>  テーブル モデル データベースにトレースを設定した場合、DMX クエリとして分類されたイベントの存在に気付くことがあります。 しかし、テーブル モデル データでは、データ マイニングはサポートされません。データベースに対して実行する DMX クエリは、モデルのメタデータに対する SELECT ステートメントに限られます。 イベントが DMX として分類されるのは、単に同じパーサー フレームワークが MDX に使用されているためです。  
  
## <a name="query-languages"></a>クエリ言語  
 Analysis Services テーブル モデルは、多次元モデルへのアクセス用とほぼ同じクエリ言語をサポートします。 ただし、DirectQuery モードで配置されたテーブル モデルは例外です。この場合、データは、Analysis Services データ ストアからではなく、SQL Server データ ソースから直接取得されます。 これらのモデルは MDX を使用してクエリすることはできません。DAX 式から Transact-SQL ステートメントへの変換をサポートするクライアントを使用する必要があります ( [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] クライアントなど)。  
  
### <a name="dax"></a>DAX  
 DAX は、あらゆる種類のテーブル モデルで、式や数式を作成する際に使用できます。モデルが SharePoint 上に PowerPivot 対応 Excel ブックとして格納されているか、Analysis Services のインスタンス上に格納されているかは関係ありません。  
  
 また、XMLA EXECUTE コマンド ステートメントのコンテキスト内で DAX 式を使用し、DirectQuery モードで配置されているテーブル モデルにクエリを送信することもできます。  
  
 DAX を使用して表形式モデルに対するクエリの例についてを参照してください [DAX クエリ構文のリファレンス] (/dax dax の構文のリファレンス
  
### <a name="mdx"></a>MDX (MDX)  
 メモリ内キャッシュを優先クエリ方式とするテーブル モデル (DirectQuery モードで配置されていないモデル) に対しては、MDX を使用してクエリを作成できます。 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] などのクライアントでは、集計を実行する場合もモデルをデータ ソースとしてクエリする場合も DAX が使用されますが、MDX に慣れている方は、MDX の方が簡単にサンプル クエリを作成できる場合があります。「 [MDX 内でのメジャーの作成](../multidimensional-models/mdx/mdx-building-measures.md)」を参照してください。  
  
### <a name="csdl"></a>CSDL  
 概念スキーマ定義言語そのものはクエリ言語ではありませんが、モデルやモデルのメタデータに関する情報を取得することはできます。後でその情報を使用して、レポートを作成したり、モデルに対するクエリを作成したりすることができます。  
  
 テーブル モデルで CSDL を使用する方法については、「[ビジネス インテリジェンス向けの CSDL 注釈 (CSDLBI)](https://docs.microsoft.com/bi-reference/csdl/csdl-annotations-for-business-intelligence-csdlbi)」を参照してください。  
  
## <a name="programmatic-interfaces"></a>プログラミング インターフェイス  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] テーブル モデルを操作する際の要となるインターフェイスには、スキーマ行セットと XMLA のほか、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] および [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]に備わっているクエリ クライアントとクエリ ツールがあります。  
  
### <a name="data-and-metadata"></a>データとメタデータ  
 マネージド アプリケーションでは、ADOMD.NET を使用して、テーブル モデルからデータおよびメタデータを取得できます。 テーブル モデルでオブジェクトを作成したり変更したりするアプリケーションの例については、次のリソースを参照してください。  
  
-   Codeplex のテーブル モデル AMO サンプル  
  
-   [動的管理ビュー (DMV) を使用した Analysis Services の監視](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
 アンマネージ クライアント アプリケーションでは Analysis Services 9.0 OLE DB プロバイダーを使用して、テーブル モデルに対する OLE DB アクセスをサポートできます。 テーブル モデル アクセスを有効にするには、最新バージョンの Analysis Services OLE DB プロバイダーが必要です。 テーブル モデルで使用するプロバイダーの詳細については、「 [SharePoint サーバーへの Analysis Services OLE DB プロバイダーのインストール](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md) 」を参照してください。  
  
 XML ベース形式のデータを Analysis Services インスタンスから直接取得することもできます。 テーブル モデルのスキーマは DISCOVER_CSDL_METADATA 行セットを使用して取得できます。また、EXECUTE コマンドまたは DISCOVER コマンドを既存の ASSL 要素、オブジェクト、またはプロパティと組み合わせて使用することもできます。 詳細については、次のリソースを参照してください。  
  
-   [ビジネス インテリジェンス向けの CSDL 注釈 (CSDLBI)](https://docs.microsoft.com/bi-reference/csdl/csdl-annotations-for-business-intelligence-csdlbi)  
  
### <a name="manipulate-analysis-services-objects"></a>Analysis Services オブジェクトの操作  
 テーブル モデルとそこに含まれるオブジェクト (テーブル、列、パースペクティブ、メジャー、パーティションなど) の作成、変更、削除、処理は、XMLA コマンドまたは AMO を使用して行うことができます。 AMO と XMLA は、テーブル モデルで使用される追加のプロパティをサポートするために更新され、レポートとモデリングの機能が強化されています。  
  
 AMO および XMLA を使用してテーブル オブジェクトをスクリプト化する例については、次のリソースを参照してください。  
  
-   Codeplex のテーブル モデル AMO サンプル  
  
-   CodePlex の AdventureWorks サンプル  
  
 PowerShell を使用して、Analysis Services のインスタンスを管理、監視できるほか、テーブル モデル アクセスに必要なセキュリティを形成、監視することができます。 詳細については、次を参照してください。 [Analysis Services PowerShell](../analysis-services-powershell.md)します。  
  
### <a name="schema-rowsets"></a>スキーマ行セット  
 クライアント アプリケーションは、スキーマ行セットを使用してテーブル モデルのメタデータを分析し、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーからサポート情報および監視情報を取得することができます。 このリリースの SQL Server では、テーブル モデルに関連した機能をサポートし、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]全体の監視とパフォーマンス分析を強化するために、新しいスキーマ行セットが追加され、既存のスキーマ行セットが拡張されています。  
  
-   [DISCOVER_CALC_DEPENDENCY 行セット](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-calc-dependency-rowset)  
  
     テーブル モデルの列と参照における依存関係を追跡するための新しいスキーマ行セット  
  
-   [DISCOVER_CSDL_METADATA 行セット](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-csdl-metadata-rowset)  
  
     テーブル モデルの CSDL 表現を取得するための新しいスキーマ行セット  
  
-   [DISCOVER_XEVENT_TRACE_DEFINITION 行セット](../dev-guide/discover-xevent-trace-definition-rowset.md)  
  
     SQL Server 拡張イベントを監視するための新しいスキーマ行セット。 詳細については、次を参照してください。[使用して SQL Server 拡張イベント&#40;Xevent&#41; Analysis Services の監視に](../instances/monitor-analysis-services-with-sql-server-extended-events.md)します。  
  
-   [DISCOVER_TRACES 行セット](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-traces-rowset)  
  
     新しい `Type` 列を使用すると、トレースをカテゴリ別にフィルター選択できます。 詳細については、「[再生用のプロファイラー トレースの作成 (Analysis Services)](../instances/create-profiler-traces-for-replay-analysis-services.md)」を参照してください。  
  
-   [MDSCHEMA_HIERARCHIES 行セット](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset)  
  
     新しい `STRUCTURE_TYPE` 列挙体は、テーブル モデルで作成されたユーザー定義階層の識別をサポートします。 詳細については、「[階層 (SSAS テーブル)](hierarchies-ssas-tabular.md)」を参照してください。  
  
 このリリースでは、データ マイニング スキーマ行セットの OLE DB に対する更新はありません。  
  
> [!WARNING]  
>  DirectQuery モードで配置されているデータベースでは MDX クエリや DMX クエリは使用できません。したがって、DirectQuery モデルに対し、スキーマ行セットを使用してクエリを実行する必要がある場合は、関連する DMV ではなく、XMLA を使用する必要があります。 SELECT * from $system.DBSCHEMA_CATALOGS (または DISCOVER_TRACES) など、サーバー全体の結果を返す DMV の場合、キャッシュ モードで配置されたデータベースの内容のクエリを実行できます。  
  
## <a name="see-also"></a>参照  
 [テーブル モデル データベースへの接続 (SSAS)](connect-to-a-tabular-model-database-ssas.md)   
 [PowerPivot データ アクセス](../power-pivot-sharepoint/power-pivot-data-access.md)   
 [Analysis Services への接続](../instances/connect-to-analysis-services.md)  
  
  
