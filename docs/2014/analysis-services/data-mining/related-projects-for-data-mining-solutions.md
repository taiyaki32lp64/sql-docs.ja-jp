---
title: データ マイニング ソリューションの関連プロジェクト |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: dc26489a-4c27-4b89-8215-6d245427c350
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: af175693a93535b21b399cf4916ca4291fc94dfa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082986"
---
# <a name="related-projects-for-data-mining-solutions"></a>データ マイニング ソリューションの関連プロジェクト
  データ マイニング ソリューションに最低限必要なのは、データ ソース、データ ソース ビュー、マイニング構造、およびマイニング モデルを定義した、データ マイニング プロジェクトです。 ただし、データ マイニング モデルを日々の意志決定に使用する場合は、データ マイニングを予測分析ソリューションの他の部分と統合し、次のプロセスやコンポーネントを含めることが重要です。  
  
-   データと変数の準備および選択。 データ クレンジング、複数のデータ ソースのメタデータ管理と統合のほか、データの変換、マージ、およびデータ ウェアハウスへのアップロードが含まれます。  
  
-   分析のレポート、予測の提示、データ マイニング アクティビティの監査と追跡。  
  
-   多次元モデルまたはテーブル モデルを使用した、結果の調査。  
  
-   データ マイニング ソリューションの強化による新しいデータのサポート、最新の分析に基づくサポート インフラストラクチャの変更。  
  
 このトピックでは、データ準備とデータ マイニングのプロセスをサポートするため、または、分析と処理のためのツールを提供してユーザーをサポートするために、予測分析ソリューションに組み込まれることの多い [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のその他の機能について説明します。  
  
 [Integration Services](#bkmk_SSIS)  
  
 [Reporting Services](#bkmk_SSRS)  
  
 [Data Quality Services](#bkmk_DQSetc)  
  
 [フルテキスト検索](#bkmk_FTSetc)  
  
 [セマンティック インデックスの作成](#bkmk_SemSearch)  
  
##  <a name="bkmk_SSIS"></a> SQL Server Integration Services  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、データ マイニング プロジェクトのデータ準備とトレーニングのフェーズに必要なコンポーネントと機能が用意されています。 さまざまなデータ クレンジング タスクやデータ準備タスクには、スクリプトをはじめとする他のツールを使用することもできますが、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、データ マイニングに関して多数の利点があります。  
  
-   繰り返し、自動化、分岐、および拡張が可能なワークフローの一部としてタスクを表現できます。  
  
-   監査が幅広くサポートされており、複数の方法でエラーをキャプチャし、イベントをログに記録できます。  
  
     データ系列のキャプチャに加えて、データ変換パイプライン全体でデータへの変更を監視できます。  
  
     SQLServer の変更データ キャプチャ機能をサポートする機能に SSIS ワークフローを統合することもできます。  
  
-   データ マイニングを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のワークフローに組み込み、入力されたデータを複数のテーブルに適切に分割できます。 たとえば、予測クエリを使用して新しい顧客をさまざまなグループに分けることで、メーリング キャンペーンの対象者を絞り込むことができます。  
  
 データ マイニングのサポートで最も幅広く使用されている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントへのリンクを以下の一覧にまとめました。  
  
 **制御フロー コンポーネント**  
  
-   [Analysis Services DDL 実行タスク](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Analysis Services 処理タスク](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
-   [CDC 制御タスク](../../integration-services/control-flow/cdc-control-task.md)  
  
-   [データ クレンジング](../../data-quality-services/data-cleansing.md)  
  
-   [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md)  
  
-   [データ プロファイル タスク](../../integration-services/control-flow/data-profiling-task.md)  
  
 **データ フロー コンポーネント**  
  
-   [CDC フロー コンポーネント](../../integration-services/data-flow/cdc-flow-components.md)  
  
-   [条件分割変換](../../integration-services/data-flow/transformations/conditional-split-transformation.md)  
  
-   [データ変換の変換](../../integration-services/data-flow/transformations/data-conversion-transformation.md)  
  
-   [データ マイニング モデル トレーニング変換先](../../integration-services/data-flow/data-mining-model-training-destination.md)  
  
-   [データ マイニング クエリ変換](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)  
  
-   [派生列変換](../../integration-services/data-flow/transformations/derived-column-transformation.md)  
  
-   [比率サンプリング変換](../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)  
  
-   [用語抽出変換](../../integration-services/data-flow/transformations/term-extraction-transformation.md)  
  
-   [用語参照変換](../../integration-services/data-flow/transformations/lookup-transformation.md)  
  
##  <a name="bkmk_SSRS"></a> SQL Server Reporting Services (SQL Server Reporting Services)  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、データ マイニング ソリューションに欠かせないコンポーネントとは考えられていませんが、データ マイニング ソリューションのプレゼンテーションの面で役立つ次のような機能を備えています。  
  
-   複雑なレポートにおける、複数のソースからのデータの統合。 アナリスト用のモデル コンテンツに対するクエリや、エンド ユーザー用の予測と傾向を示すレポートを作成できます。  
  
-   ユーザーが既存のマイニング モデルに対して直接問い合わせできるレポートを作成する機能。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]との統合。これにより、OLAP モデルから作成されたデータ マイニング ディメンションとデータ マイニング キューブのドリルスルーと調査がサポートされます。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]に用意されているパラメーター化と書式設定の機能。  
  
 DMX クエリで Reporting Services をデータ ソースとして使用する方法の詳細については、以下のリンクを参照してください。  
  
 [データ マイニング モデル &#40;DMX&#41; からデータを取得する &#40;SSRS&#41;](../../reporting-services/report-data/retrieve-data-from-a-data-mining-model-dmx-ssrs.md)  
  
 [Analysis Services の DMX クエリ デザイナーのユーザー インターフェイス](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)  
  
 [DMX のための Analysis Services の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)  
  
 ただし、DMX をデータ ソースとして使用する必要はありません。 データ マイニング用の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントでは、予測クエリの結果をリレーショナル データベースに保存することもできます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]を使用して、モデルを更新するためのワークフローを確立している場合は、予測をはじめとするデータ マイニング クエリの結果を SQL Server で保持することで、レポート用の [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] や、DMX とやり取りしないその他のツールを使用できます。  
  
 Reporting Services をデータ ソースのプレゼンテーション層として使用する方法の詳細については、「 [Integrating Reporting Services into Applications](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)」を参照してください。  
  
##  <a name="bkmk_DQSetc"></a> Data Quality Services  
 Data Quality Services (DQS) は [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の新機能です。 データに問題があるとデータ マイニングが不可能になる可能性があるため、繰り返し分析を行ったり、大規模な組織で複雑なデータ ソースを扱ったりするデータ マイニング担当者は、DQS を使用する計画的なデータ プロジェクトの方が、 [!INCLUDE[tsql](../../includes/tsql-md.md)] やその他のスクリプトを使用した場当たり的なデータ クレンジングよりも、データ マイニングをサポートするうえで信頼性の高いソリューションであることを認識する必要があります。  
  
 データ マイニング ソリューションでのデータ準備とデータ整合性のために、DQS の次の機能を考慮する必要があります。  
  
 **ソース データを分析し変更を提案するコンピューター支援型データ クレンジング プロセス。**  
 DQS では、データ品質プロバイダーによって保守および保証されているクラウドベースの参照データとソース データを比較できます。  
  
 また、生のソース データを分析し、ユーザー データからナレッジ ベースを作成することもできます。 処理後のデータは分類されたうえでユーザーに表示され、さらに処理が行われます。 クレンジング プロセスは対話型です。つまり、データ スチュワードはコンピューター支援型データ クレンジング プロセスによって提案されたデータを承認、拒否、または変更できます。  
  
 プロセスの結果として、継続的に質を高めたり、複数のデータ強化フェーズで再利用したりできるナレッジ ベースを得ることができます。  
  
 詳しくは、「 [Data Cleansing](../../data-quality-services/data-cleansing.md)」をご覧ください。  
  
 **ソース データを分析し変更を提案する、コンピューター支援型の照合プロセス。**  
 データの重複を防ぐために、データ ソースの追加クレンジングを実行して、完全一致とあいまい一致を識別できます。 これらのコンポーネントでは、照合ルールに加えて、照合ルールを適用するしきい値を指定できます。  
  
 データの一致を検出することにより、データ マイニングの妨げとなり得る重複を削除できます。 データの重複除去は自動ではありません。データ スチュワードか IT プロフェッショナルが、ナレッジ ベース内のナレッジと、データに対する変更の両方を検証する必要があります。  
  
 初期 DQS プロジェクトを作成したら、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントを使用してタスクの多くを自動化できます。  
  
 詳しくは、「 [Data Matching](../../data-quality-services/data-matching.md)」をご覧ください。  
  
 データ品質プロジェクトでクレンジングおよび照合アクティビティを実行しながら、DQS で処理中のデータに関する統計と情報をリアルタイムに入手できます。 データ クレンジングまたは照合によりデータ品質がどの程度向上したかを評価したり、加えられた変更を把握したりするのには、データ プロファイルが役立ちます。 データ プロファイルと通知の詳細については、「 [Data Profiling and Notifications in DQS](../../data-quality-services/data-profiling-and-notifications-in-dqs.md)」を参照してください。  
  
 **3 種類のナレッジ (そのままの状態のナレッジ、DQS サーバーによって生成されるナレッジ、ユーザーが生成するナレッジ) があるナレッジ ベース。**  
 ナレッジ ベースを作成した後は、それを繰り返し使用して、他のデータのクレンジングと検証を行うことができます。  
  
 新しいデータを複数のソースからナレッジ ベース データにインポートできます。参照プロバイダーからの既知のクリーン データも、ナレッジ ベース内の既存のデータに一致する生のデータもインポート可能です。  
  
 データ品質プロジェクトでのクレンジング アクティビティの詳細については、「データ クレンジング (DQS)」を参照してください。  
  
 ナレッジ ベース内のナレッジを他のソースに適用して、他のプロセス内でデータ クレンジングを行うこともできます。 こうしたデータ クレンジングは、ユーザーの入力エラー、転送または格納時の破損、データ辞書定義の不一致などを見つけるのに役立ちます。  
  
 詳細については、「 [DQS Knowledge Bases and Domains](../../data-quality-services/dqs-knowledge-bases-and-domains.md)」をご覧ください。  
  
##  <a name="bkmk_FTSetc"></a> フルテキスト検索  
 SQL Server のフルテキスト検索により、アプリケーションとユーザーは、SQL Server テーブル内の文字ベースのデータに対してフルテキスト クエリを実行できます。 フルテキスト検索が有効であれば、語句のさまざまな形式に関する言語固有のルールに基づいて強化された検索を、テキスト データに対して実行できます。 また、複数の用語間の距離などの検索条件を構成することも、尤度の順に返される結果を制限する関数を使用することもできます。  
  
 フルテキスト クエリは SQL Server エンジンによって提供される機能なので、パラメーター化クエリを作成したり、テキスト データ ソースでフルテキスト検索機能を使用してカスタム データ セットや用語のベクトルを生成したりできるほか、これらのソースをデータ マイニングで使用することもできます。  
  
 フルテキスト クエリでフルテキスト インデックスを扱う方法の詳細については、「 [フルテキスト検索でのクエリ](../../relational-databases/search/query-with-full-text-search.md)」を参照してください。  
  
 SQL Server のフルテキスト検索機能の利点は、すべての SQL Server 言語で提供されるワード ブレーカーとステマーに含まれる言語インテリジェンスを活用できるという点です。 提供されたワード ブレーカーとステマーを使用すると、各言語に適した文字で単語を区切ることができるうえ、分音記号または表記のバリエーション (日本語における数の複数の形式など) に基づくシノニムを見落とさずに済みます。  
  
 単語の境界を決める言語インテリジェンスに加え、各言語のステマーでも、その言語の活用形や表記のバリエーションに関するルールのナレッジに基づいて、単語の変化形を 1 つの用語に絞り込むことができます。 言語分析のルールは言語ごとに異なり、実際のコーパスに関する幅広い研究に基づいて作成されます。  
  
 詳細については、「 [検索用のワード ブレーカーとステミング機能の構成と管理](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)」を参照してください。  
  
 フルテキスト インデックスの作成後に保存される単語のバージョンは、圧縮形式のトークンです。 フルテキスト インデックスに対する後続のクエリにより、その言語のルールに基づいて特定の単語の変化形が複数生成されるため、あいまい一致も漏らさず照合されます。 たとえばが格納されているトークンが"run"、クエリ エンジンも検索用語を"running"、"ran"、および"runner"これらは、定期的に派生原形の単語"run"のため、します。  
  
 ユーザー類義語辞典を作成および構築して、シノニムの格納、検索結果の精度の向上、用語の分類を行うこともできます。 フルテキスト データに合わせた類義語辞典を作成すると、そのデータのフルテキスト クエリのスコープを効果的に拡張できます。 詳細については、「 [フルテキスト検索に使用する類義語辞典ファイルの構成と管理](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)」を参照してください。  
  
 フルテキスト検索を使用するうえでの要件は次のとおりです。  
  
-   データベース管理者がテーブル上にフルテキスト インデックスを作成する必要があります。  
  
-   1 つのテーブルに対し、1 つのフルテキスト インデックスしか使用できません。  
  
-   インデックスを作成する列ごとに一意のキーが必要です。  
  
-   フルテキスト インデックスを作成できるのは、データ型が char、varchar、nchar、nvarchar、text、ntext、image、xml、varbinary、varbinary(max) の列のみです。 列が varbinary、varbinary(max)、image、または xml の場合は、インデックスを作成できるドキュメントのファイル拡張子 (.doc、.pdf、.xls など) を別の型列で指定する必要があります。  
  
##  <a name="bkmk_SemSearch"></a> セマンティック インデックスの作成  
 セマンティック検索は SQL Server の既存のフルテキスト検索機能を基にして構築されていますが、追加の機能と統計を使用して、自動キーワード抽出や関連ドキュメントの検出などにも対応できます。 たとえば、セマンティック検索を使用すると、編成用の基本分類を構築することも、ドキュメントのコーパスを分類することもできます。 また、クラスタリングまたはデシジョン ツリー モデルで、抽出した用語を組み合わせたものや、ドキュメントの類似スコアを使用することも可能です。  
  
 セマンティック検索を正しく実装し、データ列にインデックスを設定したら、セマンティック インデックスの作成にネイティブに備わる関数を使用して、以下の処理が可能です。  
  
-   スコアと共に 1 語のキー フレーズを返す。  
  
-   指定したキー フレーズを含むドキュメントを返す。  
  
-   類似性スコアと、そのスコアに関係する用語を返す。  
  
 詳細については、「 [セマンティック検索を使用したドキュメント内のキー フレーズの検索](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md) 」および「 [セマンティック検索による類似および関連したドキュメントの検索](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)」をご覧ください。  
  
 セマンティック インデックスの作成をサポートするデータベース オブジェクトの詳細については、「 [テーブルおよび列に対するセマンティック検索の有効化](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)」をご覧ください。  
  
 セマンティック検索を使用するための要件は次のとおりです。  
  
-   フルテキスト検索も有効である必要があります。  
  
-   セマンティック検索コンポーネントをインストールすると特殊なシステム データベースも作成されますが、名前の変更、修正、置き換えはできません。  
  
-   サービスを使用してインデックスを作成するドキュメントは、SQL Server を使用して、フルテキスト インデックスの作成に対応した、テーブルとインデックス付きビューを含む任意のデータベース オブジェクトに格納する必要があります。  
  
-   すべてのフルテキスト言語でセマンティック インデックスの作成がサポートされているわけではありません。 サポートされている言語の一覧については、「[sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [多次元モデル ソリューション &#40;SSAS&#41;](../multidimensional-models/multidimensional-model-solutions-ssas.md)   
 [テーブル モデル ソリューション &#40;SSAS テーブル&#41;](../tabular-model-solutions-ssas-tabular.md)  
  
  
