---
title: クエリ ストアの使用シナリオ | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, usage scenarios
ms.assetid: f5309285-ce93-472c-944b-9014dc8f001d
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||= azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b01305a689f7dbe7937560350200d3e81a1785dd
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909817"
---
# <a name="query-store-usage-scenarios"></a>クエリ ストアの使用シナリオ
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  クエリ ストアは、予測可能なワークロードのパフォーマンスの追跡と確保が重要である幅広いシナリオで使用できます。 考慮できるいくつかの例を次に示します。  
  
-   プランの選択による後退が発生しているクエリを特定して修正する  
-   リソースを大量に消費しているクエリを識別して調整する  
-   A/B テストを実行する  
-   新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアップグレードするときにパフォーマンスの安定性を維持する  
-   アドホック ワークロードを識別して改善する  
  
## <a name="pinpoint-and-fix-queries-with-plan-choice-regressions"></a>プランの選択による後退が発生しているクエリを特定して修正する  
 通常のクエリの実行中に、重要な入力が変わったためにクエリ オプティマイザーが別のプランを採用することを決定する場合があります (データ カーディナリティの変化やインデックスの作成、変更、破棄、統計の更新など)。選択される新しいプランの大部分は、前に使用されていたプランよりも優れているか、同程度のパフォーマンスを提供します。 ただし、新しいプランでパフォーマンスが大幅に低下することがあります。この状況をプランの選択変更による後退と呼びます。 クエリ ストアが導入される前は、これは、識別して修正することが難しい問題でした。その理由は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、使用されていた実行プランをユーザーが調べるための組み込みのデータ ストアが提供されていなかったためです。  
  
 クエリ ストアを使って、次に示す操作を短時間で実行できます。  
  
-   特定の期間 (最後の 1 時間、1 日、1 週間など) にわたって実行メトリックが低下しているすべてのクエリを識別します。 分析をスピードアップさせるために、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 **[後退したクエリ]** を使用します。  
  
-   後退したクエリの中から、複数のプランがあり、プランの選択が不適切だったためにパフォーマンスが低下しているクエリを簡単に見つけ出します。 **[Regressed Queries]** (後退したクエリ) の **[プランの概要]** ウィンドウを使用して、後退したクエリのすべてのプランと一定期間のクエリのパフォーマンスを視覚化します。  
  
-   前のプランのほうがパフォーマンスが高いことが証明された場合は、そのプランを履歴から強制的に実行します。 **[低下したクエリ]** の **[プランの強制]** ボタンを使って、選んだプランをクエリで強制的に実行します。  
  
 ![query-store-usage-1](../../relational-databases/performance/media/query-store-usage-1.png "query-store-usage-1")  
  
 このシナリオの詳細な説明については、「[Query Store:A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)」 (クエリ ストア: データベースのためのフライト データ レコーダー) ブログを参照してください。  
  
## <a name="identify-and-tune-top-resource-consuming-queries"></a>リソースを大量に消費しているクエリを識別して調整する  
 ワークロードで数千のクエリが生成される可能性がありますが、通常は少数のクエリのみがシステム リソースの大半を実際に使用しています。このため、そのような少数のクエリに注目する必要があります。 ほとんどの場合、リソースを大量に消費しているクエリの中から、後退しているクエリか、調整を行うことで改善できるクエリを見つけることができます。  
  
 調査を開始する最も簡単な方法は、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] で **[Top Resource Consuming Queries]** (上位リソース消費クエリ) を開くことです。 ユーザー インターフェイスは、次の 3 つのウィンドウに分かれています。上位リソース消費クエリを表すヒストグラム (左側)、選択したクエリで使用されたプランの概要 (右側)、および選択したプランの視覚化されたクエリ プラン (下部)。 分析するクエリの数と関心のある期間を制御するには、 **[構成]** ボタンをクリックします。 異なるリソース消費ディメンション (期間、CPU、メモリ、IO、実行回数) とベースライン (平均、最小、最大、合計、標準偏差) も選択できます。  
  
 ![query-store-usage-2](../../relational-databases/performance/media/query-store-usage-2.png "query-store-usage-2")  
  
 右側のプランの概要を見て実行履歴を分析し、別のプランとそれらのランタイム統計を確認します。 下部ウィンドウで、別のプランを調べるか、別のプランを並べて ([比較] ボタンを使用します) それらを視覚的に比較します。  
  
パフォーマンスが低下したクエリを特定する際に必要なアクションは、問題の性質によって異なります。  
  
1.  複数のプランを使用して実行されたクエリで、最後のプランのパフォーマンスが前のプランに比べて大幅に悪化している場合は、プラン強制実行メカニズムを使用して、今後の実行で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が最適のプランを使用することを保証できます。  
  
2.  オプティマイザーが、XML プランに不足しているインデックスの有無を指示しているかどうかを確認します。 指示がある場合は、不足しているインデックスを作成し、インデックスの作成後にクエリ ストアを使用してクエリのパフォーマンスを評価します。  
  
3.  クエリで使用される基になるテーブルの統計が最新であることを確認します。  
  
4.  クエリで使用されるインデックスがデフラグされていることを確認します。  
  
5.  高コストのクエリの書き直しを検討します。 たとえば、クエリのパラメーター化を利用して、動的 SQL の使用率を下げます。 データを読み取るときに最適なロジックを実装します (アプリケーション側ではなく、データベース側でデータのフィルター処理を適用します)。  

## <a name="ab-testing"></a>A/B テストを実行する  
 クエリ ストアを使用して、予定しているアプリケーションの変更の導入前と導入後のワークロードのパフォーマンスを比較します。 次の一覧は、クエリ ストアを使用して、環境またはアプリケーションの変更がワークロードのパフォーマンスに与える影響を評価できるさまざまな例を示しています。  
  
-   新しいアプリケーションのバージョンのロールアウト。  
  
-   新しいハードウェアのサーバーへの追加。  
  
-   高コストのクエリによって参照されるテーブルで不足しているインデックスの作成。  
  
-   行レベルのセキュリティのためのセキュリティ ポリシーの適用。 詳細については、「[Optimizing Row Level Security with Query Store](https://blogs.msdn.com/b/sqlsecurity/archive/2015/07/21/optimizing-rls-performance-with-the-query-store.aspx)」(クエリ ストアによる行レベルのセキュリティの最適化) を参照してください。  
  
-   OLTP アプリケーションによって頻繁に更新されるテーブルへの一時的なシステム バージョン管理の追加。  
  
どのシナリオでも、次のワークフローが適用されます。  
  
1.  予定している変更の前に、クエリ ストアでワークロードを実行して、パフォーマンスのベースラインを生成します。  
  
2.  管理された時間中に、アプリケーションの変更を適用します。  
  
3.  十分な時間をかけてワークロードを実行して、変更後のシステムのパフォーマンス イメージを生成します。  
  
4.  #1 と #3 の結果を比較します。  
  
    1.  **[Overall Database Consumption\(全体的なデータベースの消費\)]** を開いて、データベース全体に対する影響を判断します。  
  
    2.  **[リソースを消費するクエリの上位]** を開いて (または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して独自の分析を実行して)、最も重要なクエリに対する変更の影響を分析します。  
  
5.  変更を維持するか、ロールバックを実行する (新しいパフォーマンスが容認できない場合) かを決定します。  
  
次の図は、不足しているインデックスを作成した場合のクエリ ストアの分析 (手順 4) を示しています。 [プランの概要] ウィンドウにインデックスの作成による影響を受けたクエリのこのビューを取得するには、 **[リソースを消費するクエリの上位]** を開きます。  
  
![query-store-usage-3](../../relational-databases/performance/media/query-store-usage-3.png "query-store-usage-3")  
  
さらに、インデックス作成の前と後のプランを並べて表示して、それらを比較できます (ツールバーの赤い四角形でマークされている [選択したクエリのプランを、別々のウィンドウで比較します] ツールバー オプションを選択します)。  
  
![query-store-usage-4](../../relational-databases/performance/media/query-store-usage-4.png "query-store-usage-4")  
  
インデックス作成前のプラン (上段の plan_id = 1) にはインデックス不足ヒントがあるため、クラスター化インデックス スキャンがクエリの最も高コストの操作であることがわかります (赤色の四角形)。  
  
不足しているインデックスの作成後のプラン (下段の plan_id = 15) にはインデックス シーク (非クラスター化) があり、それによってクエリの全体的なコストが減少し、クエリのパフォーマンスが向上しています (緑色の四角形)。  
  
クエリのパフォーマンスが向上しているため、分析に基づいてこのインデックスを保持することができます。  
  
## <a name="CEUpgrade"></a> 新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアップグレードするときにパフォーマンスの安定性を維持する  
[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]の前のバージョンでは、最新バージョンのプラットフォームへのアップグレード中にパフォーマンスが後退するというリスクがありました。 それは、新しいビットがインストールされると、クエリ オプティマイザーの最新バージョンがすぐにアクティブになるためでした。  
  
[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降では、すべてのクエリ オプティマイザーの変更は最新の[データベース互換性レベル](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)と連携しているため、プランの変更は、アップグレードの時点ではなく、ユーザーが `COMPATIBILITY_LEVEL` を最新のものに変更した時点で発生します。 この機能とクエリ ストアの組み合わせによって、アップグレード プロセス中のクエリのパフォーマンスを高いレベルで制御できます。 推奨されるアップグレードのワークフローを次の図に示します。  
  
![query-store-usage-5](../../relational-databases/performance/media/query-store-usage-5.png "query-store-usage-5")  
  
1.  データベース互換性レベルを変更しないで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をアップグレードします。 最新のクエリ オプティマイザーの変更は公開されませんが、クエリ ストアなどの新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能は提供されます。  
  
2.  クエリ ストアを有効にします。 このトピックについて詳しくは、「[ワークロードに合わせてクエリ ストアを調整する](../../relational-databases/performance/best-practice-with-the-query-store.md#Configure)」をご覧ください。

3.  クエリ ストアがクエリとプランをキャプチャできるようにして、ソースおよび以前のデータベース互換性レベルでパフォーマンス ベースラインを確立します。 すべてのクエリをキャプチャし、安定したベースラインが取得されるまで、十分にこの手順を続けます。 運用ワークロードの通常のビジネス サイクルの期間でかまいません。  
  
4.  最新のデータベース互換性レベルに移動します。最新のクエリ オプティマイザーの変更にワークロードを公開し、必要に応じて新しいプランを作成できるようにします。  
  
5.  クエリ ストアを使って、分析と後退の修正を行います。大部分の新しいクエリ オプティマイザーの変更はより適切なプランを生成します。 ただし、クエリ ストアでは、簡単な方法でプランの選択による後退を特定し、プラン強制実行メカニズムを使用してそれらを修正できます。 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 以降、[自動プラン修正](../../relational-databases/automatic-tuning/automatic-tuning.md#automatic-plan-correction)機能を使用すると、この手順は自動になります。  

    A.  回帰がある場合は、クエリ ストアで、正常に機能していた前のプランを強制的に適用します。  
  
    B.  クエリ プランの適用に失敗した場合、またはパフォーマンスが依然として十分ではない場合は、[データベースの互換性レベル](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)を前の設定に戻し、Microsoft カスタマー サポートにお問い合わせください。  
    
> [!TIP]
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] *データベースのアップグレード* タスクを使用して、データベースの[データベース互換レベル](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-database-engine-upgrades)をアップグレードします。 詳細については、「[クエリ調整アシスタントを使用したデータベースのアップグレード](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)」を参照してください。
  
## <a name="identify-and-improve-ad-hoc-workloads"></a>アドホック ワークロードを識別して改善する  
一部のワークロードには、アプリケーション全体のパフォーマンスを向上させるために調整できる支配的なクエリはありません。 通常、これらのワークロードは、それぞれがシステムリソースの一部を消費する、比較的多数の異なるクエリに分類されます。 これらのクエリは非常にまれに実行される一意のクエリである (通常は 1 回のみ実行されます。このためアドホックという名前がついています) ため、それらのランタイム消費は重要ではありません。 一方で、アプリケーションが常に新しいクエリを生成する場合、システム リソースのかなりの部分がクエリのコンパイルで消費され、これは最適な状況ではありません。 このような状況はクエリ ストアにとって理想的ではなく、大量のクエリとプランが予約済みの領域に殺到した場合、クエリ ストアが非常に短時間で読み取り専用モードに至る可能性があることを意味します。 **サイズ ベース クリーンアップ ポリシー** がアクティブな場合 (クエリ ストアを常に稼働させるために[強くお勧めします](best-practice-with-the-query-store.md) )、バックグラウンド プロセスによってほぼ常にクエリ ストア構造がクリーンアップされますが、この動作もシステム リソースを大幅に消費します。  
  
 **[リソースを消費するクエリの上位]** ビューに、ワークロードのアドホックな性質の最初の兆候が表示されます。  
  
![query-store-usage-6](../../relational-databases/performance/media/query-store-usage-6.png "query-store-usage-6")  
  
**[実行回数]** メトリックを使用して、上位クエリがアドホックであるかどうかを分析します (クエリ ストアを `QUERY_CAPTURE_MODE = ALL`で実行する必要があります)。 上の図から、 **[リソースを消費するクエリの上位]** の 90% が 1 回だけ実行されていることがわかります。  
  
別の方法として、[!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトを実行して、システム内のクエリ テキスト、クエリ、およびプランの合計数を取得し、query_hash と plan_hash を比較することで、それらの違いを判別できます。  
  
```sql  
--Do cardinality analysis when suspect on ad hoc workloads
SELECT COUNT(*) AS CountQueryTextRows FROM sys.query_store_query_text;  
SELECT COUNT(*) AS CountQueryRows FROM sys.query_store_query;  
SELECT COUNT(DISTINCT query_hash) AS CountDifferentQueryRows FROM  sys.query_store_query;  
SELECT COUNT(*) AS CountPlanRows FROM sys.query_store_plan;  
SELECT COUNT(DISTINCT query_plan_hash) AS  CountDifferentPlanRows FROM  sys.query_store_plan;  
```  
  
ワークロードにアドホック クエリがある場合に取得できる可能性がある結果を次に示します。  
  
![query-store-usage-7](../../relational-databases/performance/media/query-store-usage-7.png "query-store-usage-7")  
  
クエリの結果は、クエリ ストアに大量のクエリとプランがあるにもかかわらず、それらの query_hash と query_plan_hash には実際は違いがないことを示しています。 一意のクエリ テキストと一意の query_hash の 1 を大きく上回る比率は、ワークロードがパラメーター化に適した候補であることの兆候です。これは、クエリ間の違いが、クエリ テキストの一部として提供されるリテラル定数 (パラメーター) のみであるためです。  
  
通常、この状況は、アプリケーションが (ストアド プロシージャまたはパラメーター化クエリを呼び出すのではなく) クエリを生成するか、クエリを既定で生成するオブジェクト リレーショナル マッピング フレームワークに依存している場合に発生します。  
  
アプリケーション コードを管理している場合は、データ アクセス レイヤーをストアド プロシージャまたはパラメーター化クエリを利用するように書き換えることを検討できます。 ただし、この状況は、データベース全体 (すべてのクエリ) または query_hash が同じ個別のクエリ テンプレートに対してクエリのパラメーター化を強制実行することで、アプリケーションの変更なしで大幅に改善することもできます。  
  
個別のクエリ テンプレートを使用するアプローチでは、プラン ガイドを作成する必要があります。  
  
```sql  
--Apply plan guide for the selected query template 
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'<your query text goes here>',  
    @stmt OUTPUT,   
    @params OUTPUT;  
  
EXEC sp_create_plan_guide   
    N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION (PARAMETERIZATION FORCED)';  
```  
  
プラン ガイドを使用するソリューションはより正確ですが、より多くの作業が必要です。  
  
すべてのクエリ (または多くのクエリ) が自動パラメーター化の候補である場合は、データベース全体の `FORCED PARAMETERIZATION` を変更するほうが適切な方法である可能性があります。  
  
```sql  
--Apply forced parameterization for entire database  
ALTER DATABASE <database name> SET PARAMETERIZATION FORCED;  
```  

> [!NOTE]
> このトピックの詳細については、「[強制パラメータ化使用のガイドライン](../../relational-databases/query-processing-architecture-guide.md#ForcedParamGuide)」を参照してください。

これらの手順のいずれかを適用した後、 **[Top Resource Consuming Queries]** (上位リソース消費クエリ) に、別のワークロードの図が表示されます。  
  
![query-store-usage-8](../../relational-databases/performance/media/query-store-usage-8.png "query-store-usage-8")  
  
アプリケーションで、自動パラメーター化の候補にならない大量の異なるクエリが生成される場合があります。 この場合、システムで大量のクエリが発生しているが、一意のクエリと一意の `query_hash` の比率が 1 に近い可能性があります。  
  
このような場合は、[**アドホック ワークロードの最適化**](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md)サーバー オプションを有効にして、再び実行される可能性がないクエリによるキャッシュ メモリの無駄使いを防ぐことができます。 クエリ ストアにこれらのクエリがキャプチャされないようにするには、 `QUERY_CAPTURE_MODE` を `AUTO`に設定します。  
  
```sql  
EXEC sys.sp_configure N'show advanced options', N'1' RECONFIGURE WITH OVERRIDE
GO
EXEC sys.sp_configure N'optimize for ad hoc workloads', N'1'
GO
RECONFIGURE WITH OVERRIDE
GO 
  
ALTER DATABASE [QueryStoreTest] SET QUERY_STORE CLEAR;  
ALTER DATABASE [QueryStoreTest] SET QUERY_STORE = ON   
    (OPERATION_MODE = READ_WRITE, QUERY_CAPTURE_MODE = AUTO);  
```  
  
## <a name="see-also"></a>参照  
 [クエリのストアを使用した、パフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [クエリ ストアを使用する際の推奨事項](../../relational-databases/performance/best-practice-with-the-query-store.md)         
 [クエリ調整アシスタントを使用したデータベースのアップグレード](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)           
  
