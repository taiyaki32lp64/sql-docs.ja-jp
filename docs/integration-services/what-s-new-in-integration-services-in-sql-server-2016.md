---
title: SQL Server 2016 の Integration Services の新機能 | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 09/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, what's new
- what's new [Integration Services]
ms.assetid: da6999c7-e5e3-4a59-a284-1da635995af1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8a6bd6207df7d0e93c1b6d360643a9d549e90af9
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295042"
---
# <a name="what39s-new-in-integration-services-in-sql-server-2016"></a>SQL Server 2016 の Integration Services の新機能

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



このトピックでは、SQL Server 2016 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] で追加または更新された機能について説明します。 これには、SQL Server 2016 のタイム フレーム中に [Integration Services &#40;SSIS&#41; 用の Azure Feature Pack](../integration-services/azure-feature-pack-for-integration-services-ssis.md) で追加または更新された機能も含まれます。  

## <a name="new-for-ssis-in-azure-data-factory"></a>Azure Data Factory での SSIS の新機能

2017 年 9 月リリースの Azure Data Factory バージョン 2 のパブリック プレビュー版を使用すると、次の処理ができるようになります。
-   Azure SQL Database 上の SSIS カタログ データベース (SSISDB) にパッケージを展開する。
-   Azure に展開されているパッケージを、Azure-SSIS Integration Runtime (Azure Data Factory バージョン 2 のコンポーネント) で実行する。

詳細については、「[Lift and shift SQL Server Integration Services workloads to the cloud](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)」 (SQL Server Integration Services ワークロードをクラウドにリフト アンド シフトする) を参照してください。

これらの新機能では、SQL Server Data Tools (SSDT) のバージョン 17.2 以降が必要ですが、SQL Server 2017 または SQL Server 2016 は必要ありません。 パッケージを Azure に展開すると、常に最新のパッケージ形式となるように、パッケージの展開ウィザードによってパッケージがアップグレードされます。

## <a name="2016-improvements-by-category"></a>カテゴリ別の 2016 の機能強化  
  
-   **管理の容易性**  
  
    -   配置の強化  
  
        -   [SSISDB アップグレード ウィザード](#ssisdbupgrwiz)  
  
        -   [SSIS カタログでの Always On 機能のサポート](#AlwaysOn)  
  
        -   [パッケージの増分配置](#IncrementalDeployment)  
  
        -   [SSIS カタログでの Always Encrypted のサポート](#encrypted)  
  
    -   デバッグの強化  
  
        -   [SSIS カタログの新しい ssis_logreader データベース レベルのロール](#LogReader)  
  
        -   [SSIS カタログの新しい RuntimeLineage ログ記録レベル](#RuntimeLineage)  
  
        -   [SSIS カタログでの新しいカスタム ログ レベル](#CustomLogging)  
  
        -   [データ フロー内のエラー列の名前](#ErrorColumn)  
  
        -   [エラー列名の拡張サポート](#getidstring)  
  
        -   [サーバー全体の既定のログ記録レベルのサポート](#ServerLogLevel)  
  
        -   [API の新しい IDTSComponentMetaData130 インターフェイス](#CMD130)  
  
    -   パッケージ管理の強化  
  
        -   [プロジェクトをアップグレードするためのエクスペリエンスの向上](#ProjectUpgrade)  
  
        -   [AutoAdjustBufferSize プロパティによるデータフローのバッファー サイズの自動計算](#BufferSize)  
  
        -   [再利用できる制御フロー テンプレート](#Templates)  
  
        -   [パーツとして名前が変更された新しいテンプレート](#Parts)  
  
-   **接続**  
  
    -   オンプレミスでの接続性の拡張  
  
        -   [OData v4 データ ソースのサポート](#ODatav4)  
  
        -   [Excel 2013 データ ソースの明示的なサポート](#Excel2013)  
  
        -   [Hadoop ファイル システム (HDFS) のサポート](#HDFS)  
  
        -   [Hadoop と HDFS の拡張サポート](#more_hadoop)  
  
        -   [HDFS ファイル変換先での ORC ファイル形式のサポート](#hdfsORC)  
  
        -   [SQL Server 2016 での ODBC コンポーネントの更新](#odbc2016)  
  
        -   [Excel 2016 データ ソースの明示的なサポート](#Excel2016)  
  
        -   [Connector for SAP BW for SQL Server 2016 のリリース](#SAPBW)
        
        -   [Connector v4.0 for Oracle および Connector v4.0 for Teradata のリリース](#oracleteradata)
        
        -   [Connectors for Analytics Platform System (PDW) Appliance Update 5 のリリース](#pdwau5)
  
    -   クラウドへの接続性の拡張  
  
        -   Azure のストレージ コネクタと HDInsight の Hive と Pig タスク - [SQL Server 2016 用の Azure Feature Pack for SSIS のリリース](#AFP2016)
        
        -   [Service Pack 1 でリリースされた Microsoft Dynamics オンライン リソースのサポート](#dynamics)
        
        -   [Azure Data Lake Store のサポートをリリース](#datalakestore)
        
        -   [Azure SQL Data Warehouse のサポートをリリース](#sqldwupload)
  
-   **使いやすさと生産性**  
  
    -   インストール エクスペリエンスの強化  
  
        -   [SSISDB が可用性グループに属する場合のアップグレードのブロック](#Upgrade)  
  
    -   設計エクスペリエンスの強化  
  
        -   [SSIS デザイナーによる SQL Server 2016、2014、または 2012 用のパッケージの作成と管理](#OneDesigner)  
  
        -   複数のデザイナーの強化とバグの修正。  
  
    -   SQL Server Management Studio の管理エクスペリエンスの強化
  
        -   [SSIS カタログ ビューのパフォーマンスの向上](#CatViews)  
  
    -   その他の機能強化  
  
        -   [SSIS の一部になった Balanced Data Distributor 変換](#BDDinbox)  
  
        -   [SSIS の一部になったデータ フィード パブリッシング コンポーネント](#ComplexFeedinbox)  
  
        -   [SQL Server インポートおよびエクスポート ウィザードでの Azure BLOB Storage のサポート](#AzureBlob)  
  
        -   [Change Data Capture Designer と Service for Oracle for Microsoft SQL Server 2016 のリリース](#CDCOracle)  
  
        -   [SQL Server 2016 での CDC コンポーネントの更新](#cdc2016)  
  
        -   [Analysis Services DDL 実行タスクの更新](#ASDDL)  
  
        -   [Analysis Services タスクによる表形式モデルのサポート](#ssasrc0)  
  
        -   [組み込み R Services のサポート](#builtinR)  
  
        -   [XML タスクでの XML 検証の詳細な出力](#ValidateXML)  
  
## <a name="manageability"></a>管理の容易性  

### <a name="better-deployment"></a>配置の強化

####  <a name="ssisdbupgrwiz"></a> SSISDB アップグレード ウィザード  
 データベースが SQL Server インスタンスの現在のバージョンよりも古い場合、SSISDB アップグレード ウィザードを実行して、SSIS カタログ データベース (SSISDB) をアップグレードしてください。 この状況は、次のいずれかの条件が該当した場合に発生します。  
  
-   古いバージョンの SQL Server からデータベースを復元した場合。  
  
-   SQL Server インスタンスをアップグレードする前に Always On 可用性グループからデータベースを削除しなかった場合。 この場合、データベースは自動アップグレードされません。 詳細については、「 [Upgrading SSISDB in an availability group](../integration-services/catalog/ssis-catalog.md#Upgrade)」を参照してください。  
  
 詳細については、[SSIS カタログ &#40;SSISDB&#41;](../integration-services/catalog/ssis-catalog.md) に関するページを参照してください。 

####  <a name="AlwaysOn"></a> SSIS カタログでの Always On 機能のサポート  
 Always On 可用性グループ機能は、データベース ミラーリングに代わる、高可用性と災害復旧のためのエンタープライズ レベルのソリューションです。 可用性グループは、可用性データベースとして知られる、ひとまとまりでフェールオーバーされる別々のユーザー データベース セットのためのフェールオーバー環境をサポートします。 詳細については、「 [AlwaysOn 可用性グループ (SQL Server)](../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)」を参照してください。  
  
 SQL Server 2016 では、一元化された SSIS カタログ (つまり SSISDB ユーザー データベース) を簡単に配置できる新しい機能が SSIS に導入されています。 SSISDB データベースとそのコンテンツ (プロジェクト、パッケージ、実行ログなど) の高可用性を提供するために、SSISDB データベースを (他のユーザー データベースと同じように) AlwaysOn 可用性グループに追加できます。 フェールオーバーが発生すると、セカンダリ ノードのいずれかが自動的に新しいプライマリ ノードになります。  
  
 Always On 機能の詳細と SSISDB に対して有効にするための手順については、「[SSIS Catalog](../integration-services/catalog/ssis-catalog.md)」(SSIS カタログ) を参照してください。  

####  <a name="IncrementalDeployment"></a> パッケージの増分配置  
パッケージの増分配置機能によって、プロジェクト全体を配置することなく、既存または新規のプロジェクトに 1 つ以上のパッケージを配置できます。 パッケージは、次のツールを使用して増分配置できます。  
  
-   配置ウィザード  
  
-   SQL Server Management Studio (配置ウィザードを使用します)  
  
-   SQL Server Data Tools (Visual Studio) (同様に配置ウィザードを使用します)  
  
-   ストアド プロシージャ  
  
-   管理オブジェクト モデル (MOM) API  
  
 詳細については、「[Integration Services (SSIS) プロジェクトとパッケージの配置](../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)」を参照してください。  

####  <a name="encrypted"></a> SSIS カタログでの Always Encrypted のサポート  
 SSIS は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の Always Encrypted 機能を既にサポートしています。 詳細については、次のログの投稿を参照してください。  
  
-   [SSIS with Always Encrypted (SSIS と Always Encrypted)](https://blogs.msdn.com/b/ssis/archive/2015/12/18/ssis-with-always.aspx)  
  
-   [Lookup transformation with Always Encrypted (参照変換と Always Encrypted)](https://blogs.msdn.com/b/ssis/archive/2015/12/18/lookup-transformation-with-always-encrypted.aspx)  

### <a name="better-debugging"></a>デバッグの強化

####  <a name="LogReader"></a> SSIS カタログの新しい ssis_logreader データベース レベルのロール  
 SSIS カタログの以前のバージョンでは、 **ssis_admin** ロールのユーザーだけが、ログ出力を含むビューにアクセスできます。 管理者でないユーザーに対してログ出力を含むビューにアクセスするためのアクセス権を付与する、新しい **ssis_logreader** データベース レベルのロールが追加されました。  
  
 また、新しい **ssis_monitor** ロールも追加されました。 このロールは Always On 機能をサポートし、SSIS カタログによって内部的にのみ使用されます。  

####  <a name="RuntimeLineage"></a> SSIS カタログの新しい RuntimeLineage ログ記録レベル  
 SSIS カタログの新しい **RuntimeLineage** ログ記録レベルは、データ フローの系列情報を追跡するために必要な情報を収集します。 この系列情報を解析して、タスク間の系列の関係をマッピングできます。 ISV と開発者は、この情報を利用して、カスタム系列マッピング ツールを構築できます。 

####  <a name="CustomLogging"></a> SSIS カタログでの新しいカスタム ログ レベル  
 SSIS カタログの以前のバージョンでは、パッケージを実行するときに、4 つの組み込みログ記録レベル (**なし、基本、パフォーマンス、または詳細**) から選択できました。 SQL Server 2016 では、**RuntimeLineage** ログ記録レベルが追加されています。 さらに、複数のカスタム ログ記録レベルを作成して SSIS カタログに保存し、パッケージを実行するときに、毎回ログ記録レベルを選択できるようになりました。 カスタム ログ記録レベルでは、キャプチャする統計とイベントのみを選択します。 必要に応じて、変数の値、接続文字列、およびタスクのプロパティを確認するために、イベント コンテキストを含めます。 詳細については、「 [SSIS サーバーでのパッケージ実行のログ記録を有効にする](../integration-services/performance/integration-services-ssis-logging.md#server_logging)」を参照してください。 

####  <a name="ErrorColumn"></a> データ フロー内のエラー列の名前  
 エラー出力にエラーが含まれるデータ フロー内の行をリダイレクトすると、出力には、エラーが発生したが列の名前が表示されない列の数値識別子が含まれています。 エラーが発生した列の名前を、さまざまな方法で検索または表示できるようになりました。  
  
-   ログ記録を構成するときに、記録する **DiagnosticEx** イベントを選択します。 このイベントは、データ フロー列マップをログに書き込みます。 次に、エラー出力でキャプチャされた列識別子を使用して、この列マップで列名を検索できます。 詳細については、「[データのエラー処理](../integration-services/data-flow/error-handling-in-data.md)」を参照してください。  
  
-   高度なエディターでは、データ フロー コンポーネントの入力列または出力列のプロパティを表示したときに、上流列の列名を確認できます。  
  
-   エラーが発生した列の名前を表示するには、データ ビューアーをエラー出力にアタッチします。  これで、データ ビューアーに、エラーの説明とエラーが発生した列の名前の両方が表示されます。  
  
-   スクリプト コンポーネントまたはカスタムデータフロー コンポーネントで、IDTSComponentMetadata100 インターフェイスの新しい <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A> メソッドを呼び出します。  
  
 この機能強化の詳細については、SSIS 開発者である Bo Fan による次のブログの投稿を参照してください: [Error Column Improvements for SSIS Data Flow](https://blogs.msdn.com/b/ssis/archive/2015/11/27/error-column-improvement-for-ssis-data-flow.aspx) (SSIS データ フローのエラー列の機能強化)。  
  
> [!NOTE]  
>  (このサポートはその後のリリースで拡張されています。 詳細については、「 [エラー列名の拡張サポート](#getidstring) 」および「 [API の新しい IDTSComponentMetaData130 インターフェイス](#CMD130)」を参照してください。)  

####  <a name="getidstring"></a> エラー列名の拡張サポート  
 **DiagnosticEx** イベントで、系列列だけではなく、すべての入力列と出力列の列情報を記録するようになりました。 その結果、パイプライン系列マップの代わりに出力パイプライン列マップを呼び出すことができるようになりました。  
  
 GetIdentificationStringByLineageID メソッドの名前が <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A>で追加または更新された機能について説明します。 詳細については、「 [データ フロー内のエラー列の名前](#ErrorColumn)」を参照してください。  
  
 この変更とエラー列の強化の詳細については、次の更新されたブログの投稿を参照してください。 [Error Column Improvements for SSIS Data Flow (Updated for CTP3.3) (Error Column Improvements for SSIS データ フローでのエラー列の強化 (CTP3.3 での更新))](https://blogs.msdn.com/b/ssis/archive/2015/11/27/error-column-improvement-for-ssis-data-flow.aspx)  
  
> [!NOTE]  
>  (RC0 では、このメソッドは、新しい <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130> インターフェイスに移動されています。 詳細については、「 [API の新しい IDTSComponentMetaData130 インターフェイス](#CMD130)」を参照してください。)  

####  <a name="ServerLogLevel"></a> サーバー全体の既定のログ記録レベルのサポート  
 SQL Server の **[サーバーのプロパティ]** の **[サーバーのログ記録レベル]** プロパティで、既定のサーバー全体のログ記録レベルを選択できるようになりました。 組み込みのログ記録レベル (基本、なし、詳細、パフォーマンス、またはランタイムの系列) のいずれかを選択するか、既存のカスタマイズしたログ記録レベルを選択できます。 選択したログ記録レベルは、SSIS カタログに配置されているすべてのパッケージに適用されます。 また、既定で SSIS パッケージを実行する SQL エージェント ジョブにも適用されます。  

####  <a name="CMD130"></a> API の新しい IDTSComponentMetaData130 インターフェイス  
 SSIS カタログの新しい <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130> インターフェイスにより、既存の <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> インターフェイス、特に <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A> メソッドに新しい機能が追加されます ( **GetIdentificationStringByID Method** メソッドは、 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> インターフェイスからこの新しいインターフェイスに移動されました)。また、新しい <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInputColumn130> 」および「 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn130> インターフェイスも追加されました。これらのインターフェイスは、いずれも **LineageIdentificationString** プロパティを提供します。 詳細については、「 [データ フロー内のエラー列の名前](#ErrorColumn)」を参照してください。  

### <a name="better-package-management"></a>パッケージ管理の強化

####  <a name="ProjectUpgrade"></a> プロジェクトをアップグレードするためのエクスペリエンスの向上  
 SSIS プロジェクトを以前のバージョンから現在のバージョンにアップグレードするとき、プロジェクト レベルの接続マネージャーが期待どおりに動作を続行し、パッケージのレイアウトと注釈が保持されます。  

####  <a name="BufferSize"></a> AutoAdjustBufferSize プロパティによるデータフローのバッファー サイズの自動計算  
 新しい **AutoAdjustBufferSize** プロパティの値を **true**に設定すると、データ フロー エンジンによって、データ フローのバッファー サイズが自動的に計算されます。 詳細については、「 [Data Flow Performance Features](../integration-services/data-flow/data-flow-performance-features.md)」を参照してください。  

####  <a name="Templates"></a> 再利用できる制御フロー テンプレート  
 よく使用される制御フロー タスクまたはコンテナーをスタンドアロン テンプレート ファイルに保存し、制御フロー テンプレートを使用するプロジェクト内の 1 つまたは複数のパッケージで複数回再利用できます。 この再利用可能性によって、SSIS パッケージの設計と管理を容易に実行できます。 詳細については、「 [制御フロー パッケージ パーツを使用することによりパッケージ間で制御フローを再利用する](../integration-services/reuse-control-flow-across-packages-by-using-control-flow-package-parts.md)」を参照してください。  

####  <a name="Parts"></a> パーツとして名前が変更された新しいテンプレート  
 CTP 3.0 でリリースされた新しい再利用できる制御フロー テンプレートが、制御フロー パーツまたはパッケージ パーツとしてその名前が変更されました。 この機能の詳細については、「 [制御フロー パッケージ パーツを使用することによりパッケージ間で制御フローを再利用する](../integration-services/reuse-control-flow-across-packages-by-using-control-flow-package-parts.md)」を参照してください。  

## <a name="connectivity"></a>接続  

### <a name="expanded-connectivity-on-premises"></a>オンプレミスでの接続性の拡張

####  <a name="ODatav4"></a> OData v4 データ ソースのサポート  
 OData ソースと OData 接続マネージャーで OData v3 と v4 のプロトコルがサポートされるようになりました。  
  
-   OData V3 プロトコルでは、ATOM データ形式と JSON データ形式をサポートします。  
  
-   OData V4 プロトコルでは、コンポーネントは JSON データ形式をサポートします。  
  
 詳細については、「 [OData Source](../integration-services/data-flow/odata-source.md)」を参照してください。  

####  <a name="Excel2013"></a> Excel 2013 データ ソースの明示的なサポート  
 Excel 接続マネージャー、Excel ソース、Excel 変換先、および SQL Server インポートおよびエクスポート ウィザードで、Excel 2013 データソースの明示的なサポートが提供されるようになりました。 

####  <a name="HDFS"></a> Hadoop ファイル システム (HDFS) のサポート  
 HDFS のサポートに、Hadoop クラスターとタスクに接続して、HDFS の一般的な操作を実行するための接続マネージャーが含まれています。 詳細については、「[Integration Services &#40;SSIS&#41; での Hadoop と HDFS のサポート](../integration-services/hadoop-and-hdfs-support-in-integration-services-ssis.md)」を参照してください。  

####  <a name="more_hadoop"></a> Hadoop と HDFS の拡張サポート  
  
-   Hadoop 接続マネージャーが、基本認証と Kerberos 認証の両方をサポートするようになりました。 詳細については、「 [Hadoop Connection Manager](../integration-services/connection-manager/hadoop-connection-manager.md)」を参照してください。  
  
-   HDFS ファイル ソースと HDFS ファイル変換先で、テキスト形式と Avro 形式の両方をサポートするようになりました。 詳細については、「  [HDFS File Source](../integration-services/data-flow/hdfs-file-source.md) 」と「  [HDFS File Destination](../integration-services/data-flow/hdfs-file-destination.md)」を参照してください。  
  
-   Hadoop ファイル システムで、CopyToHadoop オプションと CopyFromHadoop オプションに加え、CopyWithinHadoop オプションもサポートするようになりました。 詳細については、「 [Hadoop File System Task](../integration-services/control-flow/hadoop-file-system-task.md)」を参照してください。  

####  <a name="hdfsORC"></a> HDFS ファイル変換先での ORC ファイル形式のサポート  
 HDFS ファイル変換先で、テキストと Avro に加え、ORC ファイル形式もサポートするようになりました (HDFS ファイル ソースは、テキストと Avro のみをサポートします)。このコンポーネントの詳細については、「 [HDFS File Destination](../integration-services/data-flow/hdfs-file-destination.md)」を参照してください。  

####  <a name="odbc2016"></a> SQL Server 2016 での ODBC コンポーネントの更新  
 ODBC のソース コンポーネントと変換先コンポーネントが SQL Server 2016 との完全互換を提供するように更新されています。 新しい機能の追加も動作の変更もありません。  

####  <a name="Excel2016"></a> Excel 2016 データ ソースの明示的なサポート  
 Excel 接続マネージャー、Excel ソース、および Excel 変換先で、Excel 2016 データ ソースの明示的なサポートが提供されるようになりました。  

####  <a name="SAPBW"></a> Connector for SAP BW for SQL Server 2016 のリリース  
 MicrosoftÂ® Connector for SAP BW for Microsoft SQL ServerÂ® 2016 は、SQL Server 2016 Feature Pack の一部としてリリースされています。 Feature Pack のコンポーネントをダウンロードするには、「[MicrosoftÂ® SQL ServerÂ® 2016 Feature Pack](https://go.microsoft.com/fwlink/?LinkID=746297)」を参照してください。
 
#### <a name="oracleteradata"></a> Connector v4.0 for Oracle および Connector v4.0 for Teradata のリリース
Microsoft Connector v4.0 for Oracle および Microsoft Connector v4.0 Teradata がリリースされています。 これらのコネクタをダウンロードするには、「 [Microsoft Connectors v4.0 for Oracle and Teradata](https://www.microsoft.com/download/details.aspx?id=52950)」を参照してください。

### <a name="pdwau5"></a> Connectors for Analytics Platform System (PDW) Appliance Update 5 のリリース
AU5 の PDW にデータを読み込むための変換先アダプターがリリースされています。 このアダプターをダウンロードするには、「 [Analytics Platform System Appliance Update 5 Documentation and Client Tools](https://www.microsoft.com/download/details.aspx?id=51610)」(Analytics Platform System Appliance Update 5 のドキュメントとクライアント ツール) を参照してください。

### <a name="expanded-connectivity-to-the-cloud"></a>クラウドへの接続性の拡張

####  <a name="AFP2016"></a> SQL Server 2016 用の Azure Feature Pack for SSIS のリリース  
 SQL Server 2016 用の Azure Feature Pack for Integration Services がリリースされています。 この機能パックには、Azure データソースとタスクに接続して、Azure の一般的な操作を実行するための接続マネージャーが含まれています。 詳細については、「[Azure Feature Pack for Integration Services &#40;SSIS&#41; (Integration Services 用の Azure Feature Pack &#40;SSIS&#41;)](../integration-services/azure-feature-pack-for-integration-services-ssis.md)」を参照してください。  

#### <a name="dynamics"></a> Service Pack 1 でリリースされた Microsoft Dynamics オンライン リソースのサポート

SQL Server 2016 Service Pack 1 がインストールされている場合、OData ソースと OData 接続マネージャーで、Microsoft Dynamics AX Online と Microsoft Dynamics CRM Online の OData フィードに接続できるようになりました。

#### <a name="datalakestore"></a> Azure Data Lake Store のサポートをリリース

最新バージョンの Azure Feature Pack には、接続マネージャーと、Azure Data Lake Store との間でデータを移動するときの移動元および移動先が含まれています。 詳細については、「[Integration Services (SSIS) 用の Azure Feature Pack](../integration-services/azure-feature-pack-for-integration-services-ssis.md)」を参照してください。

#### <a name="sqldwupload"></a> Azure SQL Data Warehouse のサポートをリリース

最新バージョンの Azure Feature Pack には、SQL Data Warehouse にデータを取り込む Azure SQL DW Upload タスクが含まれています。 詳細については、「[Integration Services (SSIS) 用の Azure Feature Pack](../integration-services/azure-feature-pack-for-integration-services-ssis.md)」を参照してください。

## <a name="usability-and-productivity"></a>使いやすさと生産性  
 
### <a name="better-install-experience"></a>インストール エクスペリエンスの強化

####  <a name="Upgrade"></a> SSISDB が可用性グループに属する場合のアップグレードのブロック  
 SSIS カタログ データベース (SSISDB) が Always On 可用性グループに属する場合は、SSISDB を可用性グループから削除し、SQL Server をアップグレードした後、SSISDB を可用性グループに再び追加する必要があります。 詳細については、「 [Upgrading SSISDB in an availability group](../integration-services/catalog/ssis-catalog.md#Upgrade)」を参照してください。  

### <a name="better-design-experience"></a>設計エクスペリエンスの強化

####  <a name="OneDesigner"></a> SSIS デザイナーでの複数ターゲットと複数バージョンのサポート  
 Visual Studio 2015 用の SQL Server Data Tools (SSDT) で SSIS デザイナーを使用して、SQL Server 2016、SQL Server 2014、または SQL Server 2012 をターゲットとするパッケージを作成、管理、および実行できるようになりました。 SSDT を入手する方法については、「 [最新の SQL Server Data Tools のダウンロード](../ssdt/download-sql-server-data-tools-ssdt.md)」を参照してください。 

 ソリューション エクスプローラーで Integration Services プロジェクトを右クリックし、 **[プロパティ]** を選択すると、そのプロジェクトのプロパティ ページが開きます。 **[構成プロパティ]** の **[全般]** タブで、 **[TargetServerVersion]** プロパティを選択した後、[SQL Server 2016]、[SQL Server 2014]、または [SQL Server 2012] を選択します。  
   
 ![[プロジェクトのプロパティ] ダイアログ ボックスの TargetServerVersion プロパティ](../integration-services/media/targetserverversion2.png "[プロジェクトのプロパティ] ダイアログ ボックスの TargetServerVersion プロパティ")  

> [!IMPORTANT]
> SSIS 用のカスタム拡張機能を開発する場合は、「 [Support multi-targeting in your custom components](../integration-services/extending-packages-custom-objects/support-multi-targeting-in-your-custom-components.md) 」(カスタム コンポーネントでの複数ターゲットのサポート) および「 [Getting your SSIS custom extensions to be supported by the multi-version support of SSDT 2015 for SQL Server 2016](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)」(SSIS のカスタム拡張機能を SSDT 2015 for SQL Server 2016 用 SSDT 2015 の複数バージョン サポートでサポートされるようにする) を参照してください。  

### <a name="better-management-experience-in-sql-server-management-studio"></a>SQL Server Management Studio の管理エクスペリエンスの強化

####  <a name="CatViews"></a> SSIS カタログ ビューのパフォーマンスの向上  
 ほとんどの SSIS カタログ ビューで、ssis_admin ロールのメンバー以外のユーザーが実行したときのパフォーマンスが向上しています。  

### <a name="other-enhancements"></a>その他の機能強化

####  <a name="BDDinbox"></a> SSIS の一部になった Balanced Data Distributor 変換  
 Balanced Data Distributor 変換は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の前のバージョンでは別にダウンロードする必要がありましたが、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]のインストール時にインストールされるようになりました。 詳細については、「 [Balanced Data Distributor Transformation](../integration-services/data-flow/transformations/balanced-data-distributor-transformation.md)」を参照してください。  
  
####  <a name="ComplexFeedinbox"></a> SSIS の一部になったデータ フィード パブリッシング コンポーネント  
 データ フィード パブリッシング コンポーネントは [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の前のバージョンでは別にダウンロードする必要がありましたが、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]のインストール時にインストールされるようになりました。 詳細については、「 [Data Streaming Destination](../integration-services/data-flow/data-streaming-destination.md)」を参照してください。  

####  <a name="AzureBlob"></a> SQL Server インポートおよびエクスポート ウィザードでの Azure BLOB Storage のサポート  
 SQL Server インポートおよびエクスポート ウィザードで、データの読み込み元と保存先として Azure BLOB Storage を使用できるようになりました。 詳細については、「[[データ ソースの選択] &#40;SQL Server インポートおよびエクスポート ウィザード&#41;](../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)」および「[[変換先の選択] &#40;SQL Server インポートおよびエクスポート ウィザード&#41;](../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)」を参照してください。 

####  <a name="CDCOracle"></a> Change Data Capture Designer と Service for Oracle for Microsoft SQL Server 2016 のリリース  
 MicrosoftÂ® Change Data Capture Designer と Service for Oracle by Attunity for Microsoft SQL ServerÂ® 2016 は、SQL Server 2016 Feature Pack の一部としてリリースされています。  これらのコンポーネントで、Oracle 12c のクラシック インストールをサポートできるようになりました (マルチテナント インストールはサポートされません)。Feature Pack のコンポーネントをダウンロードするには、「[MicrosoftÂ® SQL ServerÂ® 2016 Feature Pack](https://go.microsoft.com/fwlink/?LinkID=746297)」を参照してください。  
  
####  <a name="cdc2016"></a> SQL Server 2016 での CDC コンポーネントの更新  
 CDC (Change Data Capture) Control Task、Source、および Splitter Transformation コンポーネントが、SQL Server 2016 との完全互換性を提供するように更新されています。 新しい機能の追加も動作の変更もありません。  
  
####  <a name="ASDDL"></a> Analysis Services DDL 実行タスクの更新  
 Analysis Services DDL 実行タスクが、表形式モデルのスクリプト言語コマンドも受け入れるように更新されています。

####  <a name="ssasrc0"></a> Analysis Services タスクによる表形式モデルのサポート  
 SQL Server Analysis Services (SSAS) をサポートするすべての SSIS タスクと変換先を、SQL Server 2016 の表形式モデルで使用できるようになりました。 SSIS タスクは、多次元オブジェクトではなく表形式オブジェクトを表すように更新されています。 たとえば、処理するオブジェクトを選択すると、Analysis Services 処理タスクによって表形式モデルが自動的に検出され、メジャー グループやディメンションではなく、表形式オブジェクトの一覧が表示されます。 Partition Processing Destination でも表形式オブジェクトが表示され、パーティションへのデータのプッシュをサポートします。  
  
 Dimension Processing Destination は、SQL 2016 互換レベルの表形式モデルでは機能しません。  表形式処理で必要なのは、Analysis Services 処理タスクと Partition Processing Destination だけです。 

####  <a name="builtinR"></a> 組み込み R Services のサポート  
 SSIS は、組み込み R services を [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]で既にサポートしています。 SSIS を使用して、データの抽出と分析の出力の読み込みだけではなく、R モデルの構築、実行、定期的な保持も実行できます。 詳細については、次のログの投稿を参照してください。 [Operationalize your machine learning project using SQL Server 2016 SSIS and R Services](https://blogs.msdn.com/b/ssis/archive/2016/01/12/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services.aspx)(SQL Server 2016 SSIS と R Services を使用した機械学習を運用可能にする)。 

####  <a name="ValidateXML"></a> XML タスクでの XML 検証の詳細な出力  
 XML タスクの **ValidationDetails** プロパティを有効にして、XML ドキュメントを検証し、詳細なエラー出力を取得します。 **ValidationDetails** プロパティが利用できるようになる前は、XML タスクによる XML 検証では、true や false のみの結果が返され、エラーやその場所に関する情報は返されませんでした。 現在は、 **ValidationDetails** を true に設定すると、出力ファイルに各エラーの行番号と位置を含む詳しい情報が出力されます。 この情報を使って、XML ドキュメントのエラーを把握、特定、修正できます。 詳細については、「 [Validate XML with the XML Task](../integration-services/control-flow/validate-xml-with-the-xml-task.md)」を参照してください。  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] では、 **Service Pack 2 で** ValidationDetails [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] プロパティが導入されました。 その時点では、この新しいプロパティは発表されることも文書化されることもありませんでした。 **ValidationDetails** プロパティは、 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] と [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]でも利用できます。   

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

## <a name="see-also"></a>参照  
 [SQL Server 2016 の新機能](../sql-server/what-s-new-in-sql-server-2016.md)   
 [SQL Server 2016 の各エディションとサポートされる機能](../sql-server/editions-and-supported-features-for-sql-server-2016.md)
