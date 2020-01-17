---
title: データ フロー パフォーマンス機能 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- Integration Services packages, performance
- performance [Integration Services]
- data flow [Integration Services], troubleshooting
- SQL Server Integration Services packages, performance
- loading data
- control flow [Integration Services], troubleshooting
- SSIS packages, performance
- packages [Integration Services], performance
- queries [Integration Services], troubleshooting
- sorting data [Integration Services]
- aggregations [Integration Services]
ms.assetid: c4bbefa6-172b-4547-99a1-a0b38e3e2b05
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0c5c86d90536d1ba7c8acd5402317ff364ffdc67
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637956"
---
# <a name="data-flow-performance-features"></a>データ フロー パフォーマンス機能

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  このトピックでは、パフォーマンスに関する一般的な問題を [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのデザイン時に回避するための考え方を示します。 また、パッケージのパフォーマンスのトラブルシューティングに使用できる機能やツールについての情報も提供します。  
  
## <a name="configuring-the-data-flow"></a>データ フローの構成  
 パフォーマンスが向上するようにデータ フロー タスクを構成するには、タスクのプロパティの構成、バッファー サイズの調整、および並列実行用のパッケージの構成を行います。  
  
### <a name="configure-the-properties-of-the-data-flow-task"></a>データ フロー タスクのプロパティの構成  
  
> [!NOTE]  
>  ここで説明するプロパティは、パッケージ内のデータ フロー タスクごとに個別に設定する必要があります。  
  
 データ フロー タスクの次のプロパティを構成できます。これらのプロパティはすべてパフォーマンスに影響します。  
  
-   バッファー データの一時ストレージの場所 (BufferTempStoragePath プロパティ) とバイナリ ラージ オブジェクト (BLOB) データを含む列の一時ストレージの場所 (BLOBTempStoragePath プロパティ) を指定します。 既定では、これらのプロパティには TEMP および TMP 環境変数の値が含まれます。 一時ファイルを別のハード ディスク ドライブまたはより高速なハード ディスク ドライブに配置したり、複数のドライブに分散するために、他のフォルダーを指定する必要が生じることがあります。 ディレクトリ名をセミコロンで区切ることによって、複数のディレクトリを指定できます。  
  
-   タスクが使用するバッファーの既定のサイズを定義するには、DefaultBufferSize プロパティを設定します。各バッファーの最大行数を定義するには、DefaultBufferMaxRows プロパティを設定します。 AutoAdjustBufferSize プロパティを、バッファの既定のサイズが DefaultBufferMaxRows プロパティの値から自動的に計算されるかどうかを示すように設定します。 既定のバッファー サイズは 10 MB、最大のバッファー サイズは 2^31-1 バイトです。 既定の最大行数は 10,000 行です。  
  
-   EngineThreads プロパティを設定することによって、実行中にタスクが使用できるスレッド数を設定します。 このプロパティは、使用するスレッドの数に関する提案をデータ フロー エンジンに提供します。 既定値は 10 ですが、最小値は 3 です。 ただし、エンジンはこのプロパティの値に関係なく、必要以上のスレッドは使用しません。 また、エンジンは、コンカレンシーの問題が発生しないように、このプロパティで指定されている数を超えるスレッドを使用する場合もあります。  
  
-   データ フロー タスクを最適化モードで実行するかどうかを示します (RunInOptimizedMode プロパティ)。 最適化モードでは、未使用の列、出力、およびコンポーネントをデータ フローから削除することによって、パフォーマンスが向上します。  
  
    > [!NOTE]  
    >  同じ名前のプロパティ RunInOptimizedMode を [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] のプロジェクト レベルで設定すると、デバッグ中にデータ フロー タスクを最適化モードで実行するように指定できます。 このプロジェクト レベルのプロパティは、デザイン時のデータ フロー タスクの RunInOptimizedMode プロパティをオーバーライドします。  
  
### <a name="adjust-the-sizing-of-buffers"></a>バッファー サイズの調整  
 バッファー サイズを決定するため、データ フロー エンジンはまず、1 つのデータ行の推定サイズを計算します。 次に、推定行サイズに DefaultBufferMaxRows の値を乗算し、バッファー サイズの暫定値を求めます。  
  
-   AutoAdjustBufferSize が true に設定されている場合、データ フロー エンジンは、計算された値をバッファ サイズとして使用し、DefaultBufferSize は無視されます。  
  
-   AutoAdjustBufferSize が false に設定されている場合、データ フロー エンジンは、次のルールを使用してバッファ サイズを決定します。  
  
    -   計算結果が DefaultBufferSize の値を超える場合は、行数を減らします。  
  
    -   内部で計算された最小バッファー サイズより計算結果が小さい場合は、行数を増やします。  
  
    -   計算結果が最小バッファー サイズと DefaultBufferSize の値になる場合は、推定行サイズに DefaultBufferMaxRows の値を乗算した値にできるだけ近いバッファー サイズを設定します。  
  
 データ フロー タスクのパフォーマンスのテストを開始するときは、DefaultBufferSize と DefaultBufferMaxRows に既定値を使用します。 データ フロー タスクのログ記録を有効にし、BufferSizeTuning イベントを選択して、各バッファーに含まれる行数を監視します。  
  
 パフォーマンスを向上する場合は、バッファー サイズの調整を始める前に、不要な列を削除し、データ型を適切に構成して、データの各行のサイズを減らすことが最も重要です。  
  
 最適なバッファーの数とサイズを決定するには、BufferSizeTuning イベントで報告されるパフォーマンスや情報を監視しながら、DefaultBufferSize と DefaultBufferMaxRows の値を変更していきます。  
  
 ディスクへのページングが開始される大きさにまでバッファー サイズを増やさないでください。 ディスクへのページングが行われると、バッファー サイズが最適化されていない場合よりもパフォーマンスが低下します。 ページングが行われているかどうかを判断するには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理コンソール (MMC) のパフォーマンス スナップインで "Buffers spooled" パフォーマンス カウンターを監視します。  
  
### <a name="configure-the-package-for-parallel-execution"></a>並列実行用のパッケージの構成  
 並列実行を行うと、複数の物理プロセッサまたは論理プロセッサが搭載されているコンピューターのパフォーマンスが向上します。 パッケージ内で各種タスクの並列実行をサポートするには、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で次の 2 つのプロパティを使用します。**MaxConcurrentExecutables** と **EngineThreads**。  
  
#### <a name="the-maxconcurrentexcecutables-property"></a>MaxConcurrentExcecutables プロパティ  
 **MaxConcurrentExecutables** プロパティは、パッケージ自体のプロパティです。 このプロパティによって、同時に実行できるタスクの数が定義されます。 既定値は -1 です。これは、物理プロセッサまたは論理プロセッサの数に 2 を加えた数を示します。  
  
 このプロパティの動作を理解するために、3 つのデータ フロー タスクを含むサンプル パッケージについて考えてみます。 **MaxConcurrentExecutables** を 3 に設定すると、3 つすべてのデータ フロー タスクを同時に実行できます。 ただし、各データ フロー タスクに 10 個の変換元から変換先への実行ツリーが含まれているとすると、 **MaxConcurrentExecutables** を 3 に設定しても、各データ フロー タスク内の実行ツリーが並列実行されるかどうかは保証されません。  
  
#### <a name="the-enginethreads-property"></a>EngineThreads プロパティ  
 **EngineThreads** プロパティは、各データ フロー タスクのプロパティです。 このプロパティによって、データ フロー エンジンが作成および並列実行できるスレッドの数が定義されます。 **EngineThreads** プロパティは、データ フロー エンジンが変換元用に作成するソース スレッドと、変換および変換先用に作成するワーカー スレッドの両方に適用されます。 したがって、 **EngineThreads** を 10 に設定すると、エンジンはソース スレッドとワーカー スレッドをそれぞれ 10 個まで作成できます。  
  
 このプロパティの動作を理解するために、3 つのデータ フロー タスクを含むサンプル パッケージについて考えてみます。 各データ フロー タスクには、10 個の変換元から変換先への実行ツリーが含まれています。 各データ フロー タスクで EngineThreads を 10 に設定すると、30 個すべての実行ツリーを同時に実行できます。  
  
> [!NOTE]  
>  スレッド処理については、このトピックでは説明しません。 ただし、一般的な規則としては、並列実行するスレッドの数が使用可能なプロセッサ数を超えないようにします。 使用可能なプロセッサ数より多いスレッドを実行すると、スレッド間でコンテキストの切り替えが頻繁に行われるので、パフォーマンスが低下する可能性があります。  
  
## <a name="configuring-individual-data-flow-components"></a>個々のデータ フロー コンポーネントの構成  
 パフォーマンスが向上するように個々のデータ フロー コンポーネントを構成するには、いくつかの一般的なガイドラインに従います。 データ フロー コンポーネントの種類 (ソース、変換、変換先) ごとに特定のガイドラインもあります。  
  
### <a name="general-guidelines"></a>一般的なガイドライン  
 データ フロー コンポーネントの種類に関係なく、パフォーマンスを向上させるには、クエリの最適化と不必要な並べ替えの回避の 2 つの一般的なガイドラインに従う必要があります。  
  
#### <a name="optimize-queries"></a>クエリの最適化  
 データ フロー コンポーネントの多くは、ソースからデータを抽出したり、参照テーブルを作成するための参照操作を行うときにクエリを使用します。 既定のクエリでは、SELECT * FROM \<tableName> 構文が使用されます。 この種類のクエリは、ソース テーブル内のすべての列を返します。 デザイン時にすべての列を使用可能にしておくことで、参照列、パススルー列、またはソース列として、任意の列を選択できます。 ただし、目的の列を選択した後は、選択した列のみを含むようにクエリを修正します。 不必要な列を削除することで、パッケージ内のデータ フローが効率化されます。列数が少なくなると、行が小さくなるためです。 行が小さいほど 1 つのバッファーに収まる行が増え、データセット内のすべての行を処理する作業が減ります。  
  
 クエリを作成するには、手動で入力するか、クエリ ビルダーを使用することができます。  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]でパッケージを実行すると、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの [進行状況] タブに警告が表示されます。 これには、データ フローで利用できるが、それに続く下流のデータ フロー コンポーネントでは使用されないデータ列を示す警告も含まれます。 **RunInOptimizedMode** プロパティを使ってこのような列を自動的に削除できます。  
  
#### <a name="avoid-unnecessary-sorting"></a>不必要な並べ替えの回避  
 並べ替えは本質的に低速な処理であり、不必要な並べ替えを回避することで、パッケージのデータ フローのパフォーマンスを向上させることができます。  
  
 ソース データは、下流コンポーネントで使用される前に既に並べ替えられている場合があります。 このような状況は、SELECT クエリで ORDER BY 句を使用した場合、またはデータが並べ替え順でソースに挿入された場合に発生することがあります。 このようにソース データが事前に並べ替えられている場合、データが並べ替え済みである旨のヒントを示すことで、並べ替え変換の使用を回避し、特定の下流変換の並べ替え要件を満たすことができます (たとえば、マージ変換およびマージ結合変換では、並べ替え済みの入力が必要です)。データが並べ替え済みである旨のヒントを示すには、次の作業を行う必要があります。  
  
-   上流データ フロー コンポーネントの出力の **IsSorted** プロパティを **True**に設定します。  
  
-   データを並べ替える並べ替えキー列を指定します。  
  
 詳細については、「 [マージ変換およびマージ結合変換用にデータを並べ替える](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)」を参照してください。  
  
 データ フロー内でデータを並べ替える必要がある場合は、並べ替え処理の回数を可能な限り少なくしたデータ フローをデザインすることで、パフォーマンスを向上させることができます。 たとえば、データ フローでマルチキャスト変換を使用してデータセットをコピーするとします。 この場合、変換後の複数の出力に対して並べ替えを行うのではなく、マルチキャスト変換の実行前に一度だけデータセットの並べ替えを行います。  
  
 詳細については、「 [Sort Transformation](../../integration-services/data-flow/transformations/sort-transformation.md)」、「 [Merge Transformation](../../integration-services/data-flow/transformations/merge-transformation.md)」、「 [Merge Join Transformation](../../integration-services/data-flow/transformations/merge-join-transformation.md)」、および「 [Multicast Transformation](../../integration-services/data-flow/transformations/multicast-transformation.md)」を参照してください。  
  
### <a name="sources"></a>変換元  
  
#### <a name="ole-db-source"></a>OLE DB ソース  
 OLE DB ソースを使用してビューからデータを取得する場合は、データ アクセス モードとして [SQL コマンド] を選択し、SELECT ステートメントを入力します。 SELECT ステートメントを使用してデータにアクセスすると、データ アクセス モードとして [テーブルまたはビュー] を選択する場合よりもパフォーマンスが向上します。  
  
### <a name="transformations"></a>変換  
 このセクションの推奨事項に従うと、集計変換、あいまい参照変換、あいまいグループ化変換、参照変換、マージ結合変換、および緩やかに変化するディメンション変換のパフォーマンスが向上します。  
  
#### <a name="aggregate-transformation"></a>集計変換  
 集計変換には、 **Keys**、 **KeysScale**、 **CountDistinctKeys**、および **CountDistinctScale** プロパティがあります。 これらのプロパティを使用すると、変換時にキャッシュされるデータに必要な量のメモリが事前に割り当てられるようになるため、パフォーマンスが向上します。 **グループ化** 操作の結果として予想されるグループの正確な数または概数がわかっている場合は、 **Keys** プロパティと **KeysScale** プロパティをそれぞれ設定します。 **個別のカウント** 操作の結果として予想される個別の値の正確な数または概数がわかっている場合は、 **CountDistinctKeys** プロパティと **CountDistinctScale** プロパティをそれぞれ設定します。  
  
 データ フロー内に複数の集計を作成する必要がある場合は、複数の変換を作成する代わりに、1 つの集計変換を使用した複数の集計を作成することを検討してください。 この方法は、集計が別の集計のサブセットである場合にパフォーマンスを向上させます。変換により内部ストレージを最適化でき、入力データのスキャンを一度だけ行えば済むためです。 たとえば、集計で GROUP BY 句と AVG 集計を使用する場合は、それらを 1 つの変換に結合することでパフォーマンスを向上させることができます。 ただし、1 つの集計変換内で複数の集計を実行すると集計操作がシリアル化されるので、複数の集計を個別に計算する必要がある場合は、パフォーマンスが向上しない可能性があります。  
  
#### <a name="fuzzy-lookup-and-fuzzy-grouping-transformations"></a>あいまい参照変換とあいまいグループ化変換  
 あいまい参照変換とあいまいグループ化変換のパフォーマンスの最適化については、ホワイト ペーパー「 [SQL Server Integration Services 2005 のあいまい参照とあいまいグループ化](https://go.microsoft.com/fwlink/?LinkId=96604)」を参照してください。  
  
#### <a name="lookup-transformation"></a>参照変換  
 必要な列のみを参照する SELECT ステートメントを入力することによって、メモリ内の参照データのサイズを最小限に抑えます。 この方法は、テーブルまたはビュー全体を選択して大量の不要なデータを返す場合に比べてパフォーマンスに優れています。  
  
#### <a name="merge-join-transformation"></a>Merge Join Transformation  
 マイクロソフトが行った変更により、マージ結合変換によってメモリが過度に消費されるリスクが軽減したため、 **MaxBuffersPerInput** プロパティの値を構成する必要はなくなりました。 この問題は、マージ結合の複数の入力からデータが不均一なレートで生成される場合に発生することがありました。  
  
#### <a name="slowly-changing-dimension-transformation"></a>緩やかに変化するディメンション変換  
 緩やかに変化するディメンション ウィザードおよび緩やかに変化するディメンション変換は、ほとんどのユーザーのニーズを満たす汎用ツールです。 ただし、ウィザードで生成されるデータ フローは、パフォーマンスのために最適化されていません。  
  
 通常、緩やかに変化するディメンション変換の中で最も低速なコンポーネントは、一度に 1 行に対して UPDATE を実行する OLE DB コマンド変換です。 したがって、緩やかに変化するディメンション変換のパフォーマンスを向上させる最も効果的な方法は、OLE DB コマンド変換を置き換えることです。 この変換は、更新するすべての行をステージング テーブルに保存する変換先コンポーネントに置き換えることができます。 その後、同時にすべての行に対して単一セット ベースの Transact-SQL UPDATE を実行する SQL 実行タスクを追加できます。  
  
 上級ユーザーは、大きなディメンションのために最適化された、緩やかに変化するディメンション処理用のカスタム データ フローをデザインできます。 この方法の説明と例については、ホワイト ペーパー「[Project REAL: Business Intelligence ETL Design Practices (プロジェクト REAL: ビジネス インテリジェンス ETL のデザイン方法)](https://www.microsoft.com/download/details.aspx?id=14582)」の「Unique dimension scenario, (固有のディメンション シナリオ)」をご覧ください。  
  
### <a name="destinations"></a>変換先  
 変換先のパフォーマンスを向上させるには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 変換先の使用と、変換先のパフォーマンスのテストを検討してください。  
  
#### <a name="sql-server-destination"></a>SQL Server 変換先  
 パッケージで同じコンピューター上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにデータを読み込む場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 変換先を使用します。 この変換先は、高速な一括読み込みのために最適化されています。  
  
#### <a name="testing-the-performance-of-destinations"></a>変換先のパフォーマンスのテスト  
 変換先でのデータの保存には予想以上の時間がかかります。 変換先でデータを迅速に処理できないことが原因で時間がかかっているかどうかを判断するには、変換先を行数変換と置き換えます。 スループットが大幅に改善する場合は、データを読み込んでいる変換先がスローダウンを引き起こしている可能性があります。  
  
### <a name="review-the-information-on-the-progress-tab"></a>[進行状況] タブでの情報のレビュー  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] でパッケージを実行すると、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]デザイナーで制御フローとデータ フローの両方に関する情報を得られます。 **[進行状況]** タブにはタスクとコンテナーが実行順に表示され、パッケージ自体を含め、タスクやコンテナーごとに開始時刻、終了時刻、警告、エラー メッセージが表示されます。 一覧にはデータ フロー コンポーネントも実行順に表示され、進捗についての情報、完了の割合、処理された行数も表示されます。  
  
 **[進行状況]** タブでのメッセージの表示を有効または無効にするには、 **[SSIS]** メニューの **[進行状況レポートのデバッグ]** オプションを切り替えます。 進行状況レポートを無効にすると、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で複雑なパッケージを実行する際のパフォーマンスを向上させることができます。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [マージ変換およびマージ結合変換用にデータを並べ替える](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 **記事とブログ投稿**  
  
-   technet.microsoft.com の技術記事、「[SQL Server 2005 Integration Services: パフォーマンスに関する戦略](https://go.microsoft.com/fwlink/?LinkId=98899)」  
  
-   technet.microsoft.com の技術記事、「[Integration Services のパフォーマンス チューニング技法](https://go.microsoft.com/fwlink/?LinkId=98900)」  
  
-   _BI と分析に関する SQLCAT のガイド_の技術資料「[同期変換を複数タスクに分割してパイプラインのスループットを向上](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/SQLCAT's%20Guide%20to%20BI%20and%20Analytics.pdf)」
  
-   msdn.microsoft.com の技術記事: [Integration Services のパフォーマンス チューニング技法](https://go.microsoft.com/fwlink/?LinkId=220816)  
  
-   msdn.microsoft.com の技術記事「 [SSIS なら 1 TB を 30 分で読み込むことが可能](https://go.microsoft.com/fwlink/?LinkId=220817)」  
  
-   sqlcat.com の技術記事「 [SQL Server Integration Services のベスト プラクティス ベスト 10](https://go.microsoft.com/fwlink/?LinkId=220818)」  
  
-   sqlcat.com の技術記事とサンプル「[SSIS の "Balanced Data Distributor"](https://go.microsoft.com/fwlink/?LinkId=220822)」  
  
-   blogs.msdn.com のブログ投稿「 [SSIS パッケージのパフォーマンスに関する問題のトラブルシューティング](https://go.microsoft.com/fwlink/?LinkId=238156)」  
  
 **ビデオ**  
  
-   ビデオ シリーズ [「Designing and Tuning for Performance your SSIS packages in the Enterprise (SQL Video Series) (企業における SSIS パッケージの設計とパフォーマンス チューニング (SQL ビデオ シリーズ))](https://go.microsoft.com/fwlink/?LinkId=400878)」  
  
-   mssqltips.com のビデオ「 [Tuning Your SSIS Package Data Flow in the Enterprise (SQL Server Video) (企業での SSIS パッケージ データ フローのチューニング (SQL Server ビデオ))](https://technet.microsoft.com/sqlserver/ff686901.aspx)」  
  
-   mssqltips.com のビデオ「 [Understanding SSIS Data Flow Buffers (SQL Server Video) (SSIS データ フロー バッファーについて (SQL Server ビデオ))](https://technet.microsoft.com/sqlserver/ff686905.aspx)」  
  
-   channel9.msdn.com のビデオ「 [Microsoft SQL Server Integration Services パフォーマンス デザイン パターン](https://go.microsoft.com/fwlink/?LinkID=233698&clcid=0x409)」  
  
-   sqlcat.com のプレゼンテーション「 [Microsoft IT による SQL Server 2008 SSIS データ フロー エンジンの機能強化の利用方法](https://go.microsoft.com/fwlink/?LinkId=217660)」  
  
-   technet.microsoft.com のビデオ「 [Balanced Data Distributor](https://go.microsoft.com/fwlink/?LinkID=226278&clcid=0x409)」  
  
## <a name="see-also"></a>参照  
 [パッケージ開発のトラブルシューティング ツール](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)   
 [パッケージ実行のトラブルシューティング ツール](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  
