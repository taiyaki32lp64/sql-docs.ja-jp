---
title: データ プロファイル タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataprofilingtask.f1
helpviewer_keywords:
- Data Profiling task [Integration Services], about Data Profiling task
- data profiling
- profiling data
ms.assetid: 248ce233-4342-42c5-bf26-f4387ea152cf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0a895fd1dc3fe51296a110902fb1dd4c27d3d5a1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62831888"
---
# <a name="data-profiling-task"></a>データ プロファイル タスク
  データ プロファイル タスクでは、データ ソースについて詳細に理解し、解決する必要があるデータの問題を特定するために役立つさまざまなプロファイルが計算されます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ内のデータ プロファイル タスクを使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に格納されているデータをプロファイルし、発生する可能性のあるデータ品質の問題を特定することができます。  
  
> [!NOTE]  
>  このトピックでは、データ プロファイル タスクの機能と要件についてのみ説明します。 データ プロファイル タスクの使用方法のチュートリアルについては、「 [データ プロファイル タスクとビューアー](data-profiling-task-and-viewer.md)」を参照してください。  
  
## <a name="requirements-and-limitations"></a>要件と制限  
 データ プロファイル タスクは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に格納されているデータでのみ機能します。 このタスクは、サード パーティまたはファイル ベースのデータ ソースでは機能しません。  
  
 さらに、データ プロファイル タスクが含まれているパッケージを実行するには、tempdb データベースに対する Read/Write 権限 (CREATE TABLE 権限を含む) があるアカウントを使用する必要があります。  
  
## <a name="data-profiler-viewer"></a>Data Profile Viewer  
 このタスクを使用してデータ プロファイルを計算し、ファイルに保存したら、スタンドアロンの Data Profile Viewer を使用してプロファイル出力を確認できるようになります。 Data Profile Viewer では、プロファイル出力で特定されたデータ品質の問題を理解するために役立つドリル ダウン機能もサポートされています。 詳細については、「 [Data Profile Viewer](data-profile-viewer.md)」を参照してください。  
  
> [!IMPORTANT]  
>  出力ファイルには、データベースに関する機密データやデータベースに格納されているデータが含まれる場合があります。 このファイルの安全性を高める方法の推奨事項については、「 [パッケージで使用されるファイルへのアクセス](../access-to-files-used-by-packages.md)」を参照してください。  
>   
>  Data Profile Viewer に用意されているドリル ダウン機能は、元のデータ ソースにライブ クエリを送信します。  
  
## <a name="available-profiles"></a>使用可能なプロファイル  
 データ プロファイル タスクでは、8 つの異なるデータ プロファイルを計算できます。 これらのプロファイルのうち 5 つは個々の列を分析し、残りの 3 つは複数の列または列とテーブル間のリレーションシップを分析します。  
  
 次の 5 つのプロファイルで、個々の列を分析できます。  
  
|個々の列を分析するプロファイル|説明|  
|----------------------------------------------|-----------------|  
|列長分布プロファイル|選択された列に含まれる文字列値の長さごとに、その長さと、テーブル内におけるその長さの行の比率を報告します。<br /><br /> このプロファイルを使用すると、無効な値などのデータの問題を特定できます。 たとえば、2 文字の米国州コードの列をプロファイルし、3 文字以上の値を検出できます。|  
|列の NULL 比プロファイル|選択した列の NULL 値の比率を報告します。<br /><br /> このプロファイルを使用すると、列の NULL 値の比率が予想外に高いなどのデータの問題を特定できます。 たとえば、郵便番号列をプロファイルすると、許容範囲を超える欠落した郵便番号の比率を検出できます。|  
|列パターン プロファイル (Column Pattern Profile)|文字列型の列に含まれる指定された比率の値に対応する一連の正規表現を報告します。<br /><br /> このプロファイルを使用すると、無効な文字列などのデータの問題を特定できます。 また、このプロファイルには、新しい値を検証するために将来使用できる正規表現も提示されます。 たとえば、米国郵便番号列のパターン プロファイルでは、\d{5}-\d{4}、\d{5}、\d{9} という正規表現が生成されます。 その他の正規表現が示された場合、データに無効な値または形式が正しくない値が含まれている可能性があります。|  
|列統計プロファイル|数値型列の最小値、最大値、平均値、標準偏差や、`datetime` 列の最小値、最大値などの統計を報告します。<br /><br /> このプロファイルを使用すると、無効な日付などのデータの問題を特定できます。 たとえば、履歴の日付の列をプロファイルし、将来の日付の最大値を検出できます。|  
|列の値分布プロファイル|選択された列に含まれる値ごとに、その値と、テーブル内におけるその値の行の比率を報告します。 また、テーブル内の指定された比率を超えている行の値も報告できます。<br /><br /> このプロファイルを使用すると、列に含まれる個別の値の数が正しくないなどのデータの問題を特定できます。 たとえば、米国の州を想定している列をプロファイルし、50 個を超える個別の値を検出できます。|  
  
 次の 3 つのプロファイルで、複数の列または列とテーブル間のリレーションシップを分析できます。  
  
|複数の列を分析するプロファイル|説明|  
|--------------------------------------------|-----------------|  
|候補キー プロファイル|列または列のセットが、選択したテーブルのキーまたは近似キーであるかどうかを報告します。<br /><br /> このプロファイルを使用すると、キーとなる可能性がある列の重複値などのデータの問題を特定できます。|  
|機能依存プロファイル|ある列 (依存列) の値が別の列または列のセット (決定列) の値にどの程度依存しているかを報告します。<br /><br /> このプロファイルを使用すると、無効な値などのデータの問題を特定することもできます。 たとえば、米国郵便番号を含む列と米国の州を含む列の間の依存関係をプロファイルできます。 郵便番号によって州が一意に決定されますが、このプロファイルでは、この依存関係の違反を検出できます。|  
|値包含プロファイル|2 つの列間または列のセット間の値の重複を計算します。 このプロファイルでは、列または列のセットが、選択したテーブル間の外部キーとして適しているかどうかを判断できます。<br /><br /> このプロファイルを使用すると、無効な値などのデータの問題を特定することもできます。 たとえば、Sales テーブルの ProductID 列をプロファイルし、この列に Products テーブルの ProductID 列には存在しない値が含まれていることを検出できます。|  
  
## <a name="prerequisites-for-a-valid-profile"></a>有効なプロファイルの前提条件  
 空ではないテーブルおよび列を選択しない限り、プロファイルは無効です。また、列にプロファイルで有効なデータ型が含まれていない場合も、プロファイルは無効です。  
  
### <a name="valid-data-types"></a>有効なデータ型  
 使用可能なプロファイルの中には、特定のデータ型に対してのみ意味を持つものもあります。 たとえば、数値または `datetime` 値を含む列に対して列パターン プロファイルを計算しても意味がありません。 したがって、このようなプロファイルは無効です。  
  
|プロファイル|有効なデータ型*|  
|-------------|------------------------|  
|ColumnStatisticsProfile|数値型または `datetime` 型の列 (`mean` 列の `stddev` および `datetime` は除く)|  
|ColumnNullRatioProfile|すべての列**|  
|ColumnValueDistributionProfile|`integer` 型、`char` 型、および `datetime` 型の列|  
|ColumnLengthDistributionProfile|`char` 型の列|  
|ColumnPatternProfile|`char` 型の列|  
|CandidateKeyProfile|`integer` 型、`char` 型、および `datetime` 型の列|  
|FunctionalDependencyProfile|`integer` 型、`char` 型、および `datetime` 型の列|  
|InclusionProfile|`integer` 型、`char` 型、および `datetime` 型の列|  
  
 \* 有効なデータ型の場合は、前の表に、 `integer`、 `char`、`datetime`と`numeric`型が次の特定のデータ型が含まれます。  
  
 整数型には `bit`、`tinyint`、`smallint`、`int`、および `bigint` が含まれます。  
  
 文字型には `char`、`nchar`、`varchar`、および `nvarchar,` は含まれますが、`varchar(max)` および `nvarchar(max)` は含まれません。  
  
 日付/時刻型には `datetime`、`smalldatetime`、および `timestamp` が含まれます。  
  
 数値型には `integer` 型 (`bit` を除く)、`money`、`smallmoney`、`decimal`、`float`、`real`、および `numeric` が含まれます。  
  
 \*\* `image`、 `text`、 `XML`、 `udt`、および`variant`列の Null 比プロファイル以外のプロファイルの種類はサポートされていません。  
  
### <a name="valid-tables-and-columns"></a>有効なテーブルと列  
 テーブルまたは列が空の場合、データ プロファイル タスクで行われる処理は次のようになります。  
  
-   選択したテーブルまたはビューが空の場合、データ プロファイル タスクではプロファイルが計算されません。  
  
-   選択した列のすべての値が NULL の場合、データ プロファイル タスクでは列の NULL 比プロファイルのみが計算されます。 列長分布プロファイル、列パターン プロファイル、列統計プロファイル、または列の値分布プロファイルは計算されません。  
  
## <a name="features-of-the-data-profiling-task"></a>データ プロファイル タスクの機能  
 データ プロファイル タスクには、次のような便利な構成オプションがあります。  
  
-   **ワイルドカード列** プロファイル要求を構成する際、このタスクでは列名の代わりにワイルドカード **(\*)** を使用できます。 これによって構成が容易になり、十分に理解していないデータの特性を検出しやすくなります。 タスクの実行時に、適切なデータ型の列がすべてプロファイルされます。  
  
-   **クイック プロファイル** [クイック プロファイル] を選択すると、タスクをすばやく構成できます。 [クイック プロファイル] では、すべての既定のプロファイルおよび既定の設定を使用してテーブルまたはビューがプロファイルされます。  
  
## <a name="custom-logging-messages-available-on-the-data-profililng-task"></a>データ プロファイル タスクで使用できるカスタム ログ メッセージ  
 次の表は、データ プロファイル タスクのカスタム ログ エントリの一覧です。 詳細については、「[Integration Services (SSIS) のログ記録](../performance/integration-services-ssis-logging.md)」と「[ログ記録用のカスタム メッセージ](../custom-messages-for-logging.md)」を参照してください。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|**DataProfilingTaskTrace**|タスクの状態に関する説明情報を提供します。 メッセージには次の情報が含まれます。<br /><br /> 処理要求の開始<br /><br /> クエリの開始<br /><br /> クエリの終了<br /><br /> 計算要求の完了|  
  
## <a name="output-and-its-schema"></a>出力とそのスキーマ  
 データ プロファイル タスクでは、選択したプロファイルは DataProfile.xsd スキーマに従って構造化された XML に出力されます。 この XML 出力をファイルに保存するかパッケージ変数に保存するかを指定できます。 [https://schemas.microsoft.com/sqlserver/2008/DataDebugger/](https://schemas.microsoft.com/sqlserver/2008/DataDebugger/) でこのスキーマをオンラインで表示できます。 この Web ページから、スキーマのローカル コピーを保存できます。 その後、スキーマのローカル コピーを Microsoft [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] やその他のスキーマ エディター、XML エディター、またはメモ帳などのテキスト エディターで表示できます。  
  
 データ品質情報に関するこのスキーマは、次の場合に役立ちます。  
  
-   組織内および組織間でデータ品質情報を交換する場合  
  
-   データ品質情報を処理するカスタム ツールを作成する場合  
  
 ターゲットの名前空間は、スキーマで [https://schemas.microsoft.com/sqlserver/2008/DataDebugger/](https://schemas.microsoft.com/sqlserver/2008/DataDebugger/) として識別されます。  
  
## <a name="output-in-the-conditional-workflow-of-a-package"></a>パッケージの条件ワークフローでの出力  
 データ プロファイル コンポーネントには、データ プロファイル タスクの出力に基づいて [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのワークフローに条件ロジックを実装する機能は組み込まれていません。 ただし、スクリプト タスクで最小限のプログラミングを行って、このロジックを簡単に追加することができます。 このコードでは、XML 出力に対して XPath クエリを実行し、その結果をパッケージ変数に保存します。 スクリプト タスクを後続のタスクに接続する優先順位制約では、ワークフローを決定する式を使用できます。 たとえば、スクリプト タスクによって、列の NULL 値の比率が特定のしきい値を超えていることを検出できます。 この条件が満たされた場合は、パッケージを中断し、問題を解決してから続行することができます。  
  
## <a name="configuration-of-the-data-profiling-task"></a>データ プロファイル タスクの構成  
 データ プロファイル タスクを構成するには、 **[データ プロファイル タスク エディター]** を使用します。 このエディターには、次の 2 つのページがあります。  
  
 [[全般] ページ](../general-page-of-integration-services-designers-options.md)  
 **[全般]** ページでは、出力ファイルまたは変数を指定します。 また、 **[クイック プロファイル]** を選択し、既定の設定を使用してプロファイルを計算するようにタスクをすばやく構成することもできます。 詳細については、「 [単一テーブル クイック プロファイル フォーム &#40;データ プロファイル タスク&#41;](data-profiling-task.md)」を参照してください。  
  
 [[プロファイル要求] ページ](data-profiling-task-editor-profile-requests-page.md)  
 **[プロファイル要求]** ページでは、データ ソースを指定して、計算するデータ プロファイルを選択および構成します。 構成できる各種プロファイルの詳細については、次のトピックを参照してください。  
  
-   [[候補キー プロファイル要求] のオプション (データ プロファイル タスク)](candidate-key-profile-request-options-data-profiling-task.md)  
  
-   [[列長分布プロファイル要求] のオプション (データ プロファイル タスク)](column-length-distribution-profile-request-options-data-profiling-task.md)  
  
-   [[列の NULL 比プロファイル要求] のオプション (データ プロファイル タスク)](column-null-ratio-profile-request-options-data-profiling-task.md)  
  
-   [[列パターン プロファイル要求] のオプション (データ プロファイル タスク)](column-pattern-profile-request-options-data-profiling-task.md)  
  
-   [[候補キー プロファイル要求] のオプション (データ プロファイル タスク)](column-statistics-profile-request-options-data-profiling-task.md)  
  
-   [[列の値分布プロファイル要求] のオプション (データ プロファイル タスク)](column-value-distribution-profile-request-options-data-profiling-task.md)  
  
-   [[機能依存プロファイル要求] のオプション (データ プロファイル タスク)](functional-dependency-profile-request-options-data-profiling-task.md)  
  
-   [[値包含プロファイル要求] のオプション (データ プロファイル タスク)](value-inclusion-profile-request-options-data-profiling-task.md)  
  
  
