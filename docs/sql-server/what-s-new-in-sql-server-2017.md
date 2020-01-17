---
title: SQL Server 2017 の新機能 | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 0b57f375-9242-4bb2-9d4b-c560d5a93524
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 87537979ab3459727f07aec460118a74e15561f9
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874825"
---
# <a name="whats-new-in-sql-server-2017"></a>SQL Server 2017 の新機能
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]
SQL Server 2017 は、SQL Server をプラットフォームとする方向に向けた大きな一歩を表します。そのプラットフォームは、SQL Server、Linux、Linux ベースの Docker コンテナー、および Windows の機能を利用することによって、開発言語、データ型、オンプレミスまたはクラウド、オペレーティング システムの選択肢を提供します。 このトピックは、特定の機能領域の新機能と、その詳細へのリンクをまとめたものです。 Linux 上の SQL Server の詳細については、[Linux 上の SQL Server に関するドキュメント](https://docs.microsoft.com/sql/linux/)をご覧ください

[![Evaluation Center からダウンロードする](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?LinkID=829477) **お試しください:** [SQL Server 2017 リリース (2017 年 10 月) をダウンロードする](https://go.microsoft.com/fwlink/?LinkID=829477)。

> [!NOTE]
> 以下の変更に加えて、GA リリースの後も累積的な更新プログラムが定期的にリリースされます。 これらの累積的な更新プログラムでは、多くの機能強化と修正が提供されます。 最新の CU リリースについては、[SQL Server 2017 の累積的な更新プログラム](https://aka.ms/sql2017cu)に関するページをご覧ください。

## <a name="sql-server-2017-database-engine"></a>SQL Server 2017 データベース エンジン

SQL Server 2017 には多くの新しいデータベース エンジン機能、機能強化、パフォーマンス向上が含まれています。 
- CTP 2.0 で説明されている `clr strict security` 機能の回避策として、**CLR アセンブリ**を信頼できるアセンブリの一覧に追加できるようになりました。 信頼できるアセンブリ (RC1) の一覧をサポートするために、[sp_add_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md)、[sp_drop_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md)、および [sys.trusted_asssemblies](../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md) が追加されました。  
- **再開可能なオンライン インデックス リビルド**は、障害 (レプリカへのフェールオーバーや、ディスク領域不足など) 発生後、一時停止した場所からオンライン インデックス リビルド操作を再開します。または、一時停止し、オンライン インデックス リビルド操作を後から再開します。 「[ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md)」と「[オンライン インデックス操作のガイドライン](../relational-databases/indexes/guidelines-for-online-index-operations.md)」を参照してください。 (CTP 2.0)
- ALTER DATABASE SCOPED CONFIGURATION の **IDENTITY_CACHE** オプションを使用すると、サーバーが予期せず再起動したときやセカンダリ サーバーにフェールオーバーしたときに、ID 列の値のギャップを回避できます。 「[ALTER DATABASE SCOPED CONFIGURATION (ALTER データベース スコープ ベースの構成)](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)」を参照してください。 (CTP 2.0)
- 新世代のクエリ処理では、最適化戦略がアプリケーション ワークロードの実行時条件に適用される点が改善されています。 **アダプティブ クエリ処理**機能ファミリのこの最初のバージョンでは、3 つの新しい改善点があります。**バッチ モード適応型結合**、**バッチ モード メモリ許可フィードバック**、そして複数ステートメントのテーブル値関数の**インターリーブ実行**です。  「[SQL データベースでのインテリジェントなクエリ処理](../relational-databases/performance/intelligent-query-processing.md)」を参照してください。
- **自動データベース チューニング**は、潜在的なクエリ パフォーマンスの問題に関する洞察を提供し、解決策を推奨して、特定された問題を自動的に解決できます。 「[自動調整](../relational-databases/automatic-tuning/automatic-tuning.md)」を参照してください。 (CTP 2.0)
- 多対多のリレーションシップをモデル化する新しい**グラフ データベース機能**には、ノードとエッジ テーブルを作成するための新しい [CREATE TABLE](../t-sql/statements/create-table-sql-graph.md) 構文と、クエリ用の [MATCH](../t-sql/queries/match-sql-graph.md) キーワードが含まれています。 「[Graph Processing with SQL Server 2017](../relational-databases/graphs/sql-graph-overview.md)」 (SQL Server 2017 でのグラフ処理) を参照してください。 (CTP 2.0)
- CLR アセンブリのセキュリティを強化する `clr strict security` という sp_configure オプションが既定で有効になります。 「[CLR strict security](../database-engine/configure-windows/clr-strict-security.md)」 (CLR の厳格なセキュリティ) を参照してください。 (CTP 2.0)
- セットアップ時に、ファイルあたり **256 GB** (262,144 MB) までの初期 tempdb ファイル サイズを指定できるようになりました。IFI が有効になっていない状態でファイル サイズが 1 GB より大きく設定される場合には警告が表示されます。 (CTP 2.0)
- [sys.dm_db_file_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md) の **modified_extent_page_count** 列は、各データベース ファイル内の差分変更を追跡します。これにより、データベース内の変更されたページの割合に基づいて差分バックアップまたは完全バックアップを実行するスマート バックアップ ソリューションが有効になります。 (CTP 2.0)
- [SELECT INTO](../t-sql/queries/select-into-clause-transact-sql.md) の T-SQL 構文で、**ON** キーワードを使用した、ユーザーの既定のファイル グループ以外のファイル グループへのテーブルの読み込みがサポートされました。 (CTP 2.0)
- **Always On 可用性グループ**の一部であるすべてのデータベースで、同じインスタンスの一部であるデータベースも含め、データベース間トランザクションがサポートされました。 「[Transactions - Always On Availability Groups and Database Mirroring](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)」 (トランザクション - Always On 可用性グループとデータベース ミラーリング) を参照してください。 (CTP 2.0)
- 新しい**可用性グループ**機能として、クラスターを使用しない読み取りスケールのサポート、最小レプリカ コミット可用性グループの設定、Windows と Linux の OS 間の移行とテストが含まれます。 (1.3 CTP)
- 新しい動的管理ビュー:
    - [sys.dm_db_log_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md) は、トランザクション ログの正常性監視に役立つ、トランザクション ログ ファイルに関する概要レベルの属性と情報を公開します。 (CTP 2.1)
    - [sys.dm_tran_version_store_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md) は、データベースごとのバージョン ストア使用量を追跡します。これは、データベースごとのデータベース ストア使用量に基づくプロアクティブな tempdb サイズ計画に役立ちます。 (CTP 2.0)
    - [sys.dm_db_log_info](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md) は、潜在的なトランザクション ログの問題を監視、通知、防止するための VLF 情報を公開します。 (CTP 2.0)
    - [sys.dm_db_stats_histogram](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) は、統計情報を確認するための新しい動的管理ビューです。 (1.3 CTP)
    - **sys.dm_os_host_info** は、Windows および Linux の両方について、オペレーティング システム情報を提供します。 (CTP 1.0)
- **データベース チューニング アドバイザー (DTA)** のオプションが追加され、パフォーマンスが向上しています。 (CTP 1.2)
- **メモリ内の機能強化**として、メモリ最適化テーブルでの計算列、ネイティブ コンパイル モジュールでの JSON 関数の完全なサポート、ネイティブ コンパイル モジュールでの CROSS APPLY 演算子が含まれます。 (CTP 1.1)
- 新しい**文字列関数**として CONCAT_WS、TRANSLATE、TRIM が追加され、WITHIN GROUP が STRING_AGG 関数でサポートされました。 (CTP 1.1)
- CSV および Azure BLOB ファイル用の新しい**一括アクセス オプション** (BULK INSERT および OPENROWSET(BULK...) ) があります。 (CTP 1.1)
- **メモリ最適化オブジェクトの機能強化**として、メモリ最適化テーブルでの 8 インデックス制限の廃止と sp_spaceused、メモリ最適化テーブルおよびネイティブ コンパイル T-SQL モジュールでの sp_rename、ネイティブ コンパイル T-SQL モジュールでの CASE と TOP (N) WITH TIES が含まれます。 メモリ最適化ファイル グループのファイルを Azure Storage に保存し、バックアップおよび復元できるようになりました。 (CTP 1.0)
- **DATABASE SCOPED CREDENTIAL** は新しいセキュリティ保護可能クラスで、CONTROL、ALTER、REFERENCES、TAKE OWNERSHIP、VIEW DEFINITION の各アクセス許可をサポートします。 ADMINISTER DATABASE BULK OPERATIONS が sys.fn_builtin_permissions から参照できるようになりました。 (CTP 1.0)
- データベースの **COMPATIBILITY_LEVEL 140** が追加されました。 (CTP 1.0)  

詳細については、「[What's new in SQL Server 2017 Database Engine](~/database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md)」 (SQL Server 2017 データベース エンジンの新機能) を参照してください。

## <a name="sql-server-2017-integration-services-ssis"></a>SQL Server 2017 Integration Services (SSIS)
- SSIS の新しい **Scale Out** 機能として、次のような新しい機能と変更された機能があります。 詳細については、「[SQL Server 2017 の Integration Services の新機能](~/integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)」を参照してください。 (RC1)
    -   スケール アウト マスターで高可用性を実現できるようになりました。
    -   スケール アウト ワーカーの実行ログのフェールオーバー処理が改善されました。
    -   ストアド プロシージャ **[catalog].[create_execution]** の *runincluster* パラメーターは、一貫性とわかりやすさを理由に、名前が *runinscaleout* に変更されました。
    -   SSIS カタログに、SSIS パッケージを実行する既定のモードを指定するための新しいグローバル プロパティが追加されました。
- 新しい **SSIS の Scale Out** 機能で、実行をトリガーするときに **Use32BitRuntime** パラメーターを使用できるようになりました。 (CTP 2.1)
- SQL Server 2017 Integration Services (SSIS) で **Linux 上の SQL Server** がサポートされ、新しいパッケージでは、コマンド ラインから Linux で SSIS パッケージを実行できます。 詳細については、[SSIS の Linux サポートをお知らせするブログの投稿](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)を参照してください。 (CTP 2.1)
- 新しい **SSIS の Scale Out**  機能を使用すると、複数のコンピューターでの SSIS の実行が大幅に簡単になります。 「[Integration Services Scale Out](~/integration-services/scale-out/integration-services-ssis-scale-out.md)」を参照してください。(CTP 1.0)
- OData ソースと OData 接続マネージャーで、Microsoft Dynamics AX Online と Microsoft Dynamics CRM Online の OData フィードに接続できるようになりました。 (CTP 1.0)

詳細については、「[SQL Server 2017 の Integration Services の新機能](~/integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)」を参照してください。

## <a name="sql-server-2017-master-data-services-mds"></a>SQL Server 2017 マスター データ サービス (MDS)
- SQL Server 2012、SQL Server 2014、および SQL Server 2016 から SQL Server 2017 マスター データ サービスにアップグレードすると、エクスペリエンスとパフォーマンスが向上します。 
- Web アプリケーションの**エクスプローラー** ページに、エンティティ、コレクション、階層の並べ替えられたリストを表示できるようになりました。
- ステージング ストアド プロシージャを使用した、数百万ものレコードのステージングのパフォーマンスが向上しました。
- モデル アクセス許可を割り当てる**グループの管理**ページの、**エンティティ**フォルダーを展開するときのパフォーマンスが改善されました。 **グループの管理**ページは、Web アプリケーションの**セキュリティ**セクション内にあります。 パフォーマンスの改善の詳細については、こちら ([https://support.microsoft.com/help/4023865?preview](https://support.microsoft.com/help/4023865?preview)) を参照してください。 権限の割り当ての詳細については、「[Assign Model Object Permissions (Master Data Services) (モデル オブジェクト権限を割り当てる (マスター データ サービス))](../master-data-services/assign-model-object-permissions-master-data-services.md)」を参照してください。

## <a name="sql-server-2017-analysis-services-ssas"></a>SQL Server 2017 Analysis Services (SSAS) 
SQL Server Analysis Services 2017 には、表形式モデルの多くの機能強化が導入されています。 たとえば、次のオブジェクトにアクセスできます。
- Analysis Services の既定のインストール オプションとしての表形式モード。 (CTP 2.0)
- 表形式モデルのメタデータをセキュリティで保護する、オブジェクト レベルのセキュリティ。 (CTP 2.0)
- 日付フィールドに基づくリレーションシップを簡単に作成する、日付リレーションシップ。 (CTP 2.0)
- 新しい**データ取得** (Power Query) のデータ ソースと、既存の DirectQuery データ ソースでの M クエリのサポート。 (CTP 2.0) 
- SSDT 用の DAX エディター。 (CTP 2.0)
- エンコードのヒント。これは、大規模なメモリ内表形式モデルのデータ更新を最適化するために使用される高度な機能です。 (1.3 CTP)
- 表形式モデルでの **1400 互換性レベル**のサポート。 新規の 1400 互換性レベルの表形式モデル プロジェクトを作成するか、既存の表形式モデル プロジェクトを 1400 互換性レベルにアップグレードするには、[SQL Server Data Tools (SSDT) 17.0 RC2](https://go.microsoft.com/fwlink?LinkId=837939) をダウンロードしてインストールします。 (CTP 1.1)
- 1400 互換性レベルの表形式モデルでの、最新の**データ取得**エクスペリエンス。 [分析サービス チームのブログ](https://blogs.msdn.microsoft.com/analysisservices/2016/12/16/introducing-a-modern-get-data-experience-for-sql-server-vnext-on-windows-ctp-1-1-for-analysis-services/)を参照してください。 (CTP 1.1)
- 不規則階層で空のメンバーを非表示にする、**メンバーを隠す**プロパティ。 (CTP 1.1)
- 集計情報の**詳細を表示**する、新しい**詳細行**エンドユーザー アクション。 詳細行の式を作成するための [SELECTCOLUMNS](/dax/selectcolumns-function-dax) および **DETAILROWS** 関数。 (CTP 1.1)
- 複数の値を指定するための DAX **IN** 演算子。 (CTP 1.1)

詳細については、「[What's new in SQL Server Analysis Services (SQL Server Analysis Services の新機能)](/analysis-services/what-s-new-in-analysis-services)」をご覧ください。

## <a name="sql-server-2017-reporting-services-ssrs"></a>SQL Server 2017 Reporting Services (SSRS)
SQL Server Reporting Services は、SQL Server セットアップでインストールできなくなりました。 Microsoft ダウンロード センターに移動し、[Microsoft SQL Server 2017 Reporting Services をダウンロード](https://www.microsoft.com/download/details.aspx?id=55252)してください。 
- レポートでコメントが使用できるようになり、分析観点の追加や、他のユーザーとの共同作業ができるようになりました。 コメントに添付ファイルを含めることもできます。
- レポート ビルダーと SQL Server Data Tools の最新リリースでは、クエリ デザイナーで必要なフィールドをドラッグ アンド ドロップすることで、サポートされている SQL Server Analysis Services 表形式データ モデルに対するネイティブの DAX クエリを作成できます。 [Reporting Services のブログ](https://blogs.msdn.microsoft.com/sqlrsteamblog/2017/03/09/query-designer-support-for-dax-now-available-in-report-builder-and-sql-server-data-tools/)を参照してください。
- 最新のアプリケーションとカスタマイズを開発できるようにするため、SSRS は OpenAPI に完全に対応する RESTful API をサポートするようになっています。 API の完全な仕様とドキュメントは、[swaggerhub](https://app.swaggerhub.com/apis/microsoft-rs/SSRS/2.0) で入手できます。

詳細については、「[What's new in SQL Server Reporting Services (SSRS)](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)」 (SQL Server Reporting Services (SSRS) の新機能) を参照してください。

## <a name="machine-learning-in-sql-server-2017"></a>SQL Server 2017 での Machine Learning 

R 言語に加えて Python がサポートされたことに合わせて、SQL Server R Services の名前が **SQL Server Machine Learning Services** に変更されました。 Machine Learning サービス (データベース内) を使用して、SQL Server で R または Python スクリプトを実行したり、**Microsoft Machine Learning Server (スタンドアロン)** をインストールして、SQL Server を必要としない R および Python のモデルを配置し、使用したりすることができます。 

SQL Server での開発者は、オープン ソース エコシステムで入手できるさまざまな Python ML および AI ライブラリと、Microsoft の最新技術を利用できるようになりました。

- **revoscalepy** - この Python と同等の RevoScaleR には、線形およびロジスティック回帰用並列アルゴリズム、デシジョン ツリー、ブースト ツリー、ランダム フォレストだけでなく、データ変換とデータ移動、リモート計算コンテキスト、およびデータ ソース用の豊富な API が含まれています。
- **microsoftml** - Python バインディングを使用したこの最新パッケージの機械学習アルゴリズムと変換には、深層ニューラル ネットワーク、高速なデシジョン ツリーとデシジョン フォレスト、線形およびロジスティック回帰用に最適化されたアルゴリズムが含まれています。 また、イメージの抽出や感情分析に使用できる ResNet モデルに基づくトレーニング済みモデルも用意されています。
- **T-SQL を使用した Python 運用可能化** - ストアド プロシージャを使用して、Python コードを簡単に展開できます`sp_execute_external_script`。 SQL から Python プロセスへデータをストリーミングし、MPI リングの並列化を使用して、パフォーマンスを向上することができます。
- **SQL Server 計算コンテキストでの Python** - データ サイエンティストと開発者は、データを移動することなく、開発環境からリモートで Python コードを実行し、データを探索してモデルを開発することができます。
- **ネイティブ スコアリング** -  R がインストールされていない場合でも、Transact-SQL のPREDICT 関数を使用して、SQL Server 2017 の任意のインスタンスでスコアリングを実行できます。 必要なのは、サポートされている RevoScaleR と revoscalepy アルゴリズムのいずれかを使用してモデルをトレーニングし、新しいコンパクトなバイナリ形式でモデルを保存することだけです。
- **パッケージの管理** - T-SQL では、DBA で R パッケージよりも優れた管理を実現する CREATE EXTERNAL LIBRARY ステートメントがサポートされるようになりました。 ロールを使用してプライベートまたは共有パッケージのアクセスを制御し、R パッケージをデータベースに格納して、ユーザー間で共有します。
- **パフォーマンスの向上** - 列ストア データのバッチ モード実行をサポートするために、ストアド プロシージャ`sp_execute_external_script`が最適化されました。


詳細については、「[What's new in SQL Server Machine Learning Services](~/advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)」 (SQL Server Machine Learning Services の新機能) を参照してください。

## <a name="next-steps"></a>次の手順
- [SQL Server 2017 リリース ノート](sql-server-2017-release-notes.md)を参照してください。
- 「[Linux 上の SQL Server 2017 の新機能](https://docs.microsoft.com/sql/linux/sql-server-linux-whats-new)」を参照してください。
- [SQL Server 2016 の新機能](what-s-new-in-sql-server-2016.md)を確認してください。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
