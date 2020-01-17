---
title: SQL Server 2014 | の新機能Microsoft Docs
ms.custom: ''
ms.date: 12/10/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- new features [SQL Server]
- SQL Server, what's new
- SQL Server 2008 what's new
- what's new [SQL Server]
- sql server 2014 sp1
- sql server 2014 sp2
ms.assetid: 6a428023-e3cc-4626-a88a-4c13ccbd7db0
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 23a1392256e103fa1bc112f11b5c5b97f5c398f1
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75237714"
---
# <a name="whats-new-in-sql-server-2014"></a>SQL Server 2014 の新機能

このトピックで[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]は、の新機能に関する詳細なリンクと、のサービスパックの概要について説明します。[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**試してみる:** ![azure Virtual Machine small](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png)に azure アカウントをお持ちですか?  にhttps://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2アクセスして、SQL Server 2014 Service Pack 1 (SP1) が既にインストールされている仮想マシンを起動します。

> [!TIP]
> SQL Server 2014 のホームドキュメントページについては、[ここをクリック](../2014-toc/index.yml)してください。

<!--
Do not let this file's filename fool you.
This filename contains "2016", but nevertheless...
This file, at this exact GitHub path, is dedicated to SQL Server version 2014.
-->

## <a name="whats-new-articles"></a>新機能に関する記事

-   [新機能 &#40;データベースエンジン&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [Analysis Services と Business Intelligence の新機能](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)  
  
-   [SQL Server インストールの新機能](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]では、次の機能に重要な新機能が導入されていません。**  
  
-   [新機能 &#40;Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [新機能 &#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="includesssql14includessssql14-mdmd-service-pack-1-sp1"></a>
  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)](SP1) では、重要な新機能は導入されませんでした。
-  [SQL Server 2014 Service Pack 1 のリリース情報](https://support.microsoft.com/kb/3058865)。
-  [Microsoft SQL Server 2014 の service pack 1 をダウンロードする Microsoft SQL Server 2014 用の service pack 1 をダウンロードします。 ![](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/download/details.aspx?id=46694) [](https://www.microsoft.com/download/details.aspx?id=46694)


## <a name="includesssql14includessssql14-mdmd-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Service Pack 2 (SP2)
- [SQL Server 2014 Service Pack 2 リリース情報](https://support.microsoft.com/kb/3171021)。
-  [Microsoft SQL Server 2014 の service pack 2 をダウンロードする Microsoft SQL Server 2014 用の service pack 2 をダウンロードします。 ![](./media/what-s-new-in-sql-server-2016/download.png)](https://go.microsoft.com/fwlink/?LinkID=821558) [](https://go.microsoft.com/fwlink/?LinkID=821558)
-  [SQL Server 2014 sp2 feature pack SQL Server 2014 sp2 feature pack をダウンロードします。 ![](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/download/details.aspx?id=53164) [](https://www.microsoft.com/download/details.aspx?id=53164)

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SMSでは、次の点が改善されています。

### <a name="performance-and-scalability-improvements"></a>パフォーマンスとスケーラビリティの向上 
-   **ソフト NUMA の自動パーティション分割:** SP2 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]では、インスタンスの起動時にトレースフラグ8079が有効になっていると、自動ソフト NUMA が有効になります。 起動時にトレースフラグ8079が有効になっ[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]ている場合、SP2 はハードウェアレイアウトを調査し、numa ノードあたり8個以上の cpu を報告するシステムでソフト NUMA を自動的に構成します。 ソフト NUMA の自動動作は、ハイパースレッド (HT/論理プロセッサ) に対応しています。 パーティション分割と追加ノードの作成により、リスナーの数の増加、スケーリング、およびネットワークと暗号化機能の向上により、バックグラウンド処理が拡張されます。 運用環境でチューニングする前に、自動ソフト NUMA を使用してパフォーマンスワークロードをテストすることをお勧めします。 [詳細については、ブログを参照してください](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/)。 
-  **動的メモリオブジェクトのスケーリング:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 では、最新のハードウェアに拡張するために、ノードとコアの数に基づいてメモリオブジェクトを動的に分割します。 動的な昇格の目的は、スレッドセーフメモリオブジェクト (CMEMTHREAD) がボトルネックになった場合に、そのオブジェクトを自動的にパーティション分割することです。 パーティション分割されていないメモリオブジェクトは、ノードによって動的にパーティション分割できます (パーティションの数は NUMA ノードの数と等しくなります)。 ノードによってパーティション分割されたメモリオブジェクトは、CPU (パーティションの数は Cpu の数と等しくなります) によってさらにパーティション分割できます。 [詳細については、ブログを参照してください](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/)。
-  **DBCC\* CHECK コマンドの MAXDOP ヒント:** この機能強化には、 [connect のフィードバック (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb)があります。 Sp_configure 値以外の MAXDOP 設定を使用して DBCC CHECKDB を実行できるようになりました。 MAXDOP では、Resource Governor で構成されている値を超えると、データベース エンジンは、「ALTER WORKLOAD GROUP (TRANSACT-SQL)」に記載のリソース ガバナーの MAXDOP 値を使用します。 MAXDOP クエリ ヒントを使用している場合は、max degree of parallelism 構成オプションで使用されるすべての意味ルールを適用できます。 詳細については、「 [DBCC CHECKDB (transact-sql)](https://msdn.microsoft.com/library/ms176064.aspx)」を参照してください。
-   **バッファープールに対して >8 tb を有効にする:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 では、バッファープールの使用に 128 tb の仮想アドレス空間が有効になります。 この機能強化により、最新のハードウェアで SQL Server バッファープールを 8 TB を超えて拡張できます。
-   **スピンロックの向上の SOS_RWLock:** SOS_RWLock は、SQL Server コードベースを通じてさまざまな場所で使用される同期プリミティブです。  名前が示すように、コードは複数の共有 (リーダー) または単一 (ライター) の所有権を持つことができます。 この機能強化により、SOS_RWLock のスピンロックが不要になり、代わりにインメモリ OLTP のようなロックフリーの手法が使用されます。 この変更により、多くのスレッドでは、SOS_RWLock によって保護されたデータ構造を相互にブロックすることなく、並列で読み取ることができます。 この並列処理により、スケーラビリティが向上します。 この変更の前に、スピンロックの実装では、データ構造を読み取る場合でも、一度に1つのスレッドで SOS_RWLock を取得できるようになりました。 [詳細については、ブログを参照してください](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/)。
-    **空間ネイティブ実装:** ネイティブ実装によって、SP2 で[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]は、空間クエリのパフォーマンスが大幅に向上しています。 詳細については、[サポート技術情報の記事 KB3107399](https://support.microsoft.com/kb/3107399)を参照してください。

### <a name="supportability-and-diagnostics-improvements"></a>サポートと診断の機能強化
-   **データベースの複製:** 複製データベースは、データなしでスキーマとメタデータを複製することで、既存の運用データベースのトラブルシューティングを強化する新しい DBCC コマンドです。 複製は、コマンド`DBCC clonedatabase('source_database_name', 'clone_database_name')`を使用して作成されます。  **注:** 複製されたデータベースは、運用環境では使用できません。 次のコマンドを使用して、複製されたデータベースからデータベースが`select DATABASEPROPERTYEX('clonedb', 'isClone')`生成されたかどうかを確認します。 戻り値**1**は、データベースが clonedatabase から作成されていることを示し、 **0**は複製ではないことを示します。
-   **Tempdb のサポート性:** Tempdb ファイルの数と tempdb のデータファイルのサイズと自動拡張の両方を開始時に示す新しいエラーログメッセージ。
-   **データベースのファイルの瞬時初期化ログ:** サーバーの起動時に、データベースのファイルの瞬時初期化の状態 (有効/無効) を示す新しいエラーログメッセージ。
-   **呼び出し履歴のモジュール名:** 拡張イベント (XEvent) の呼び出し履歴には、絶対アドレスではなく、モジュール名とオフセットが含まれるようになりました。
-   **増分統計用の新しい DMF:** この改善により、 [connect のフィードバック (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics)が、パーティションレベルで増分統計を追跡できるようになります。 新しい DMF の dm_db_incremental_stats_properties が導入され、増分統計のパーティションごとの情報を公開するようになりました。
-   **インデックス使用状況 DMV の動作が更新されました:** この改善により、インデックスを再構築しても、そのインデックスの dm_db_index_usage_stats からの既存の行エントリがクリアされ*ない*お客様からの[接続フィードバック (739566)](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats)が解決されます。 動作は、SQL 2008 および SQL Server 2016 と同じになります。 [詳細については、ブログを参照してください](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/)。
-   **診断の XE と dmv の相関関係が向上し**ました。この改善により、 [connect のフィードバック (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types)が解決します。 `Query_hash`と`query_plan_hash`は、クエリを一意に識別するために使用されます。 DMV はこれらを varbinary(8) として定義するのに対し、XEvent は UINT64 として定義します。 SQL server には "unsigned bigint" がないため、キャストは常に機能しません。 この機能強化により、新しい XEvent アクションとフィルター列が導入されました。 列は、と`query_hash` `query_plan_hash`に相当しますが、INT64 として定義されている点が異なります。 INT64 定義は、XE と Dmv 間のクエリを関連付けるのに役立ちます。
-   **BULK INSERT および BCP での utf-8 のサポート:** この改善により、 [connect のフィードバック (370419)](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001)が解決します。 BULK INSERT と BCP は、UTF-8 文字セットでエンコードされたデータをエクスポートまたはインポートできるようになりました。
-   **演算子ごとのクエリ実行の簡易プロファイリング:** Showplan は、プラン内の各オペレーターのコストに関する情報を提供します。 ただし、実際の実行時の統計情報は、CPU、i/o の読み取り、スレッドあたりの経過時間などに限定されます。 SQL Server 2014 SP2 では、プラン表示の操作ごとにこれらの追加のランタイム統計が導入されています。 R2 では、クエリの`query_thread_profile`パフォーマンスのトラブルシューティングを支援するために、という名前の XEvent も導入されています。 [詳細については、ブログを参照してください](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/)。
-   **Change Tracking のクリーンアップ:** 必要に応じて`sp_flush_CT_internal_table_on_demand`変更の追跡の内部テーブルをクリーンアップするために、新しいストアドプロシージャが導入されました。
-   **AlwaysON リースタイムアウトのログ**現在の時刻と予想される更新時刻がログに記録されるように、リースタイムアウトメッセージの新しいログ記録機能が追加されました。 また、タイムアウトに関して、SQL エラーログに新しいメッセージが導入されました。 [詳細については、ブログを参照してください](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/)。
-   **SQL Server で入力バッファーを取得するための新しい DMF。** セッション/要求 (sys. dm_exec_input_buffer) の入力バッファーを取得するための新しい DMF が使用できるようになりました。 この DMF は、機能的には DBCC INPUTBUFFER と同等です。 [詳細については、ブログを参照してください](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/)。
-   **過小使用および過剰推定メモリ許可の軽減策:** Resource Governor の新しいクエリヒントが MIN_GRANT_PERCENT と MAX_GRANT_PERCENT に追加されました。 この新しいクエリでは、メモリの競合を防ぐために、クエリの実行中にこれらのヒントを活用できます。 詳細については、[サポート技術情報の記事 KB310740](https://support.microsoft.com/kb/3107401)を参照してください。
-   **メモリ許可と使用状況の診断の向上:** という名前`query_memory_grant_usage`の新しい拡張イベントが SQL Server のトレース機能の一覧に追加されました。 このイベントは、要求および許可されたメモリ許可を追跡します。 このイベントにより、メモリ許可に関連するクエリ実行の問題をトラブルシューティングするためのトレースと分析の機能が向上します。 詳細については、[サポート技術情報の記事 KB3107173](https://support.microsoft.com/kb/3107173)を参照してください。
-   **Tempdb 書き込み用のクエリ実行診断:**-ハッシュ警告と並べ替えの警告に、物理 i/o 統計、使用されたメモリ、および影響を追跡する行を追加するための列が追加されました。 また、新しい hash_spill_details 拡張イベントも導入されました。 これで、ハッシュと並べ替えの警告 ([KB3107172](https://support.microsoft.com/kb/3107172)) の詳細情報を追跡できるようになりました。 この改善は、SpillToTempDbType 複合型 ([KB3107400](https://support.microsoft.com/kb/3107400)) に新しい属性の形式で XML クエリプランを通じて公開されるようになりました。 Set statistics `ON`に並べ替え作業テーブル統計が表示されるようになりました。
-   **残存述語のプッシュダウンが関係するクエリ実行プランの診断が向上しました。** 実際に読み取られた行は、クエリのパフォーマンスのトラブルシューティングを向上させるために、クエリ実行プランにレポートされるようになりました。 これらの行は、SET STATISTICS IO を個別にキャプチャする必要性を否定します。 これらの行を使用すると、クエリプランの残存述語のプッシュダウンに関連する情報を確認することもできます。 詳細については、[サポート技術情報の記事 KB3107397](https://support.microsoft.com/kb/3107397)を参照してください。


## <a name="additional-information"></a>追加情報  
 [SQL Server 2014 リソース](../2014-toc/index.yml)  
  
 [SQL Server 2014 リリースノート](https://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [SQL Server 2014 リソース センター](https://msdn.microsoft.com/sqlserver/dn135309)  
  
 [SQLCat Web サイト](https://go.microsoft.com/fwlink/p/?linkID=220963)  
