---
title: SQL Server 2016 リリース ノート | Microsoft Docs
ms.date: 04/25/2018
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- build notes
- release issues
ms.assetid: c64077a2-bec8-4c87-9def-3dbfb1ea1fb6
author: craigg-msft
ms.author: craigg
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 741aec40bf972ae6caedfc0301e7a3dcd080d593
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632918"
---
# <a name="sql-server-2016-release-notes"></a>SQL Server 2016 リリース ノート
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
  ここでは、SQL Server 2016 リリースでの制限事項と問題について説明します。Service Pack についても説明します。 新機能については、「 [SQL Server 2016 の新機能](https://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2016)」をご覧ください。

- [![Evaluation Center からダウンロードする](../includes/media/download2.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)  **[Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)** から SQL Server 2016 をダウンロードする
- [![Azure Virtual Machine のアイコン](../includes/media/azure-vm.png)](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftsqlserver.sql2016sp1-ws2016) Azure アカウントをすでにお持ちですか?  **[こちら](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftsqlserver.sql2016sp1-ws2016)** にアクセスして、SQL Server 2016 SP1 がインストール済みの仮想マシンをすぐにご利用いただけます。
- [![SSMS をダウンロードする](../includes/media/download2.png)](../ssms/download-sql-server-management-studio-ssms.md) 最新版の SQL Server Management Studio を入手するには、「 **[SQL Server Management Studio (SSMS) のダウンロード](../ssms/download-sql-server-management-studio-ssms.md)** 」をご覧ください。

## <a name="bkmk_2016sp2"></a>SQL Server 2016 Service Pack 2 (SP2)

![info_tip](../sql-server/media/info-tip.png) SQL Server 2016 SP2 には、2016 SP1 より後にリリースされた、CU8 まで (CU8 を含む) の累積的な更新プログラムがすべて含まれています。

- [![Microsoft ダウンロード センター](../includes/media/download2.png)](https://www.microsoft.com/download/details.aspx?id=56836) [SQL Server 2016 Service Pack 2 (SP2) をダウンロードする](https://www.microsoft.com/download/details.aspx?id=56836)
- 更新プログラムの完全な一覧については、「[SQL Server 2016 Service Pack 2 リリース情報 ](https://support.microsoft.com/help/4052908/sql-server-2016-service-pack-2-release-information)」を参照してください。

SQL Server 2016 SP2 のインストールでは、インストール後に再起動が必要な場合があります。 ベスト プラクティスとして、SQL Server 2016 SP2 インストール後の再起動を計画して実行することをお勧めします。

SQL Server 2016 SP2 にはパフォーマンスとスケールに関連する改善が含まれています。

|機能|[説明]|詳細情報|
|---|---|---|
|ディストリビューション DB のクリーンアップ プロシージャの向上 |   サイズ超過のディストリビューション データベース テーブルにより、ブロックとデッドロックの状況が発生していました。 クリーンアップ プロシージャの向上は、これらのブロックまたはデッドロックのシナリオの一部を排除することを目的としています。 |   [KB4040276](https://support.microsoft.com/help/4040276/fix-indirect-checkpoints-on-the-tempdb-database-cause-non-yielding)  |
|変更の追跡のクリーンアップ    |   変更の追跡のクリーンアップ パフォーマンスと、変更の追跡のサイド テーブルの効率性が向上しました。    |   [KB4052129](https://support.microsoft.com//help/4052129/update-for-manual-change-tracking-cleanup-procedure-in-sql-server-2016) |
|CPU のタイムアウトを使用したリソース ガバナーの要求の取り消し   |   要求の CPU しきい値に達した場合に実際に要求を取り消すことで、クエリ要求の処理が改善されます。 この動作は、トレース フラグ 2422 で有効です。 |   [KB4038419](https://support.microsoft.com/help/4038419/add-cpu-timeout-to-resource-governor-request-max-cpu-time-sec)   |
|SELECT INTO によるファイル グループへのターゲット テーブルの作成    |   SQL Server 2016 SP2 以降では、SELECT INTO の T-SQL 構文で ON <Filegroup name> キーワードを使用して、ユーザーの既定のファイル グループ以外のファイル グループにテーブルを読み込むことができるようになりました。 |       |
|TempDB の間接チェックポイントの改善    |   DPLists のスピンロックの競合を最小限に抑えるため、TempDB の間接チェックポイント処理が改善しました。 この機能強化により、TempDB の間接チェックポイント処理が ON になっている場合に、SQL Server 2016 の TempDB ワークロードが自由にスケールアウトできるようになります。    |   [KB4040276](https://support.microsoft.com/help/4040276) |
|大容量メモリのコンピューターでのデータベース バックアップ パフォーマンスの改善  |   SQL Server 2016 SP2 ではバックアップ中に進行している I/O のドレイン方法が最適化されるため、中小規模のデータベースのバックアップ パフォーマンスが大幅に改善されています。 2TB のコンピューターでシステム データベースのバックアップを実行した場合の改善度は、以前の 100 倍という結果が出ています。 バックアップするページが増加してデータベースのサイズが大きくなり、バッファー プールを繰り返す場合と比べ、バックアップ IO の時間が長くなると、バッファー プールのパフォーマンスの向上の幅が小さくなります。 この変更により、大容量メモリ搭載の大規模なハイ エンドサーバーで複数の小規模データベースをホストしている顧客のバックアップ パフォーマンスが改善します。    |       |
|TDE が有効なデータベースでの VDI バックアップの圧縮のサポート   |   SQL Server 2016 SP2 では、VDI バックアップ ソリューションが TDE が有効なデータベースで圧縮を利用できるようにする、VDI サポートが追加されています。 この改善により、TDE が有効なデータベースでバックアップの圧縮をサポートするための新しいバックアップ形式が導入されました。 SQL Server エンジンは、バックアップを復元するための新旧のバックアップ形式を透過的に処理します。   |       |
|レプリケーション エージェント プロファイルのパラメーターの動的な読み込み    |   この新しい機能強化により、エージェントを再起動しなくてもレプリケーション エージェントのパラメーターが動的に読み込まれるようになります。 この変更は、特に一般的に使用されるエージェント プロファイルのパラメーターにのみ適用されます。 |       |
|統計の作成/更新のための MAXDOP オプションのサポート |    この機能強化により、CREATE/UPDATE の STATISTICS ステートメントに MAXDOP オプションを指定できるだけでなく、作成または再構築の一環として統計が更新される場合にすべての型のインデックスで正しい MAXDOP 設定が使用されるようになります (MAXDOP オプションが存在する場合)   |   [KB4041809](https://support.microsoft.com/help/4041809) |
|増分統計の自動更新の改善 |    特定のシナリオでは、増分統計の合計変更数が自動更新のしきい値を超え、それでいて個々のパーティションのいずれもが自動更新のしきい値を超えないようにテーブルの複数のパーティションで多数のデータ変更が行われた場合、統計更新はテーブルでより多くの変更が行われるまで遅延する場合があります。 この動作は、トレース フラグ 11024 で修正されました。   |       |

SQL Server 2016 SP2 にはサポートと診断に関連する改善が含まれています。

|機能|[説明]|詳細情報|
|---|---|---|
|可用性グループ内のデータベースでの完全な DTC サポート    |   可用性グループの一部であるデータベースでの複数データベース間トランザクションは現在 SQL Server 2016 でサポートされていません。 SQL Server 2016 SP2 では、可用性グループ データベースでの分散トランザクションの完全なサポートを導入しています。   |       |
|TempDB の暗号化の状態を正確に反映するための sys.database の is_encrypted 列の更新 |   すべてのユーザー データベースの暗号化をオフにし、SQL Server を再起動した後でも、TempDB の sys.databases の is_encrypted 列の値は 1 です。 この状況では TempDB が暗号化されないため、この値が 0 になることが予想されます。 SQL Server 2016 SP2 以降では、sys.databases.is_encrypted で TempDB の暗号化の状態が正確に反映されます。  |       |
|検証済みのクローンとバックアップを生成するための新しい DBCC CLONEDATABASE オプション   |   SQL Server 2016 SP2 では、DBCC CLONEDATABASE によって、検証済みのクローンの作成、またはバックアップ クローンの作成という 2 つのオプションを使用できるようになります。 WITH VERIFY_CLONEDB オプションによってクローン データベースが作成されると、実稼働環境で Microsoft によってサポートされる一貫性のあるデータベース クローンが作成され、検証されます。 クローンが検証されるかどうかを検証する新しいプロパティ SELECT DATABASEPROPERTYEX('clone_database_name', 'IsVerifiedClone') が導入されています。 クローンが BACKUP_CLONEDB オプションで作成されると、顧客が簡単にクローンを別のサーバーに移動したり、トラブルシューティングのために Microsoft カスタマー サポート (CSS) に送信したりできるように、データ ファイルと同じフォルダーにバックアップが生成されます。  |       |
|DBCC CLONEDATABASE の Service Broker (SSB) のサポート    |   SSB オブジェクトのスクリプト作成を許可するように、DBCC CLONEDATABASE コマンドが拡張されました。  |   [KB4092075](https://support.microsoft.com/help/4092075) |
|TempDB のバージョン ストア領域の使用量を監視する新しい DMV    |   TempDB のバージョン ストア使用量の監視が可能になるように、SQL Server 2016 SP2 に新しい sys.dm_tran_version_store_space_usage の DMV が導入されました。 運用サーバーでの実行時にパフォーマンスのオーバーヘッドを発生させることなく、データベースごとのバージョン ストア使用量の要件に基づいて DBA で TempDB のサイズを事前に計画できるようになりました。 |       |
|レプリケーション エージェントの完全なダンプのサポート | 現在は、レプリケーション エージェントがハンドルされない例外に遭遇すると、既定により例外の現象のミニ ダンプが作成されます。 これにより、未処理の例外の問題のトラブルシューティングが非常に難しくなっています。 今回の変更では新しいレジストリ キーが導入され、レプリケーション エージェントの完全なダンプが作成できるようになっています。  |       |
|可用性グループのルーティング読み取りエラーの拡張イベントの機能強化 |   以前は、ルーティング リストが存在する場合、read_only_rout_fail の xEvent が起動していましたが、ルーティング リストのどのサーバーも、接続に使用できませんでした。 SQL Server 2016 SP2 には、トラブルシューティングに役立つ追加情報と、xEvent が起動するコード ポイントの拡張も含まれます。  |       |
|トランザクション ログを監視する新しい DMV |   概要レベルの属性とデータベースのトランザクション ログ ファイルに関する情報を返す新しい DMV sys.dm_db_log_stats を追加しました。 |       |
|VLF 情報を監視するための新しい DMV |   顧客が遭遇する可能性のある T-Log の問題を監視し、警告し、回避するための、DBCC LOGINFO に似た VLF 情報を公開する新しい DMV、sys.dm_db_log_info が SQL Server 2016 SP2 に導入されました。    |       |
|sys.dm_os_sys_info のプロセッサ情報|   socket_count や cores_per_numa などのプロセッサ関連情報を公開する新しい列が sys.dm_os_sys_info の DMV に追加されています。  |       |
|sys.dm_db_file_space_usage のエクステントの変更情報| 前回の完全バックアップから変更されたエクステントの数を追跡する新しい列が sys.dm_db_file_space_usage に追加されました。  |       |
|sys.dm_exec_query_stats のセグメント情報 |   total_columnstore_segment_reads、total_columnstore_segment_skips などの、スキップされた列ストア セグメントや読み取られた列ストア セグメントの数を追跡する新しい列が sys.dm_exec_query_stats に追加されました。   |   [KB4051358](https://support.microsoft.com/help/4051358) |
|ディストリビューション データベースの正しい互換性レベルの設定  |   Service Pack をインストールすると、ディストリビューション データベースの互換性レベルが 90 に変更されます。 これは、sp_vupgrade_replication ストアド プロシージャのコード パスが原因でした。 SP はディストリビューション データベースに正しい互換性レベルが設定されるように変更されています。   |       |
|最後に確認された適切な DBCC CHECKDB 情報の公開    |   最後に成功した DBCC CHECKDB 実行の日付がプログラムで自動的に返されるように、新しいデータベースのオプションが追加されました。 ユーザーはクエリ DATABASEPROPERTYEX([database], 'lastgoodcheckdbtime') を実行することで、指定したデータベースで最後に成功した DBCC CHECKDB 実行の日時を表す単一の値を取得することができます。  |       |
|Showplan XML の機能強化| 統計名、変更数、サンプリングの割合、統計の最終更新日時を含む、[クエリ プランのコンパイルに使用された統計に関する情報](https://blogs.msdn.microsoft.com/sql_server_team/sql-server-2017-showplan-enhancements/)。 これは CE モデル 120 以降でのみ追加されます。 たとえば、CE 70 ではサポートされません。| |
| |クエリ オプティマイザーが "row goal" のロジックを使用する場合、新しい属性 [EstimateRowsWithoutRowgoal](https://blogs.msdn.microsoft.com/sql_server_team/more-showplan-enhancements-row-goal/) が Showplan XML に追加されます。| |
| |実際の Showplan XML には、スカラー ユーザー定義関数 (UDF) に費やされた時間を追跡する新しいランタイム属性 [UdfCpuTime と UdfElapsedTime](https://blogs.msdn.microsoft.com/sql_server_team/more-showplan-enhancements-udfs/) が追加されています。| |
| |実際の Showplan XML には待機の種類 CXPACKET が[考えられる上位 10 の待機リスト](https://blogs.msdn.microsoft.com/sql_server_team/new-showplan-enhancements/)に追加されています。クエリの並列実行には頻繁に CXPACKET の待機が含まれますが、この種類の待機は実際の Showplan XML では報告されませんでした。 |       |
| |並列処理の演算子の書き込み中に TempDB に書き込まれたページ数を報告するためのランタイム書き込み警告が拡張されました。| |
|補助的な文字の照合を使用するデータベースのレプリケーションのサポート  |   補助的な文字の照合を使用するデータベースでレプリケーションがサポートされるようになりました。 |       |
|可用性グループのフェールオーバーを使用した Service Broker の適切な処理 |   現在の実装では、可用性グループのデータベースで Service Broker が有効になっていると、プライマリ レプリカで開始されたすべての Service Broker の接続は、AG フェールオーバー中に開いたままになります。 この機能強化は、AG フェールオーバー中、これらの開いたままの接続をすべて閉じることを目的としています。 |       |
|並列処理の待機のトラブルシューティングの改善 |   新しい [CXCONSUMER](https://blogs.msdn.microsoft.com/sql_server_team/making-parallelism-waits-actionable/) の待機が追加されたためです。   |       |
|同じ情報の DMV 間での一貫性が改善 |   sys.dm_exec_session_wait_stats の DMV と sys.dm_os_wait_stats の DMV の間で、CXPACKET と CXCONSUMER の待機の追跡が一貫して行われるようになりました。 |       |
|クエリ内並列処理のデッドロックのトラブルシューティングの向上 | 新しい exchange_spill の拡張イベントによって、xEvent のフィールド名 worktable_physical_writes での並列処理演算子の書き込み中に TempDB に書き込まれたページ数が報告されます。| |
| |sys.dm_exec_query_stats、sys.dm_exec_procedure_stats、sys.dm_exec_trigger_stats の各 DMV への書き込み列 (total_spills など) に並列処理演算子によって書き込まれたデータも含まれるようになりました。| |
| |並列処理のデッドロック シナリオで exchangeEvent リソースに属性が追加されたことで、XML デッドロック グラフが改善されました。| |
| |バッチモード演算子を伴うデッドロックで SyncPoint リソースに属性が追加されたことで、XML デッドロック グラフが改善されました。| |
|一部のレプリケーション エージェント プロファイルのパラメーターの動的な読み込み |   レプリケーション エージェントの現在の実装では、エージェント プロファイル パラメーターの変更には、必ずエージェントの停止と再起動が必要です。 この機能強化により、レプリケーション エージェントを再起動しなくてもパラメーターが動的に再読み込みされるようになりました。   |       |

![horizontal-bar.png](media/horizontal-bar.png)

## <a name="bkmk_2016sp1"></a>SQL Server 2016 Service Pack 1 (SP1)
![info_tip](../sql-server/media/info-tip.png) SQL Server 2016 SP1 には、SQL Server 2016 RTM CU3 までの累積的な更新プログラムがすべて含まれ、セキュリティ更新プログラム MS16-136 も含まれます。 2016 年 11 月 8 日にリリースされた最新の累積的な更新プログラム CU3 とセキュリティ更新プログラム MS16-136 までを含む、SQL Server 2016 の累積的な更新プログラムで提供された解決策のロールアップが含まれています。

次の機能は、SQL Server SP1 の Standard、Web、Express、および Local DB エディションで使用できます (注記されている例外を除きます)。
- Always Encrypted
- 変更データ キャプチャ (Express では使用できません)
- 列ストア
- 圧縮
- 動的なデータ マスキング
- 詳細な監査
- インメモリ OLTP (Local DB では使用できません)
- 複数の filestream コンテナー (Local DB では使用できません)
- [パーティション分割]
- PolyBase
- 行レベルのセキュリティ

次の表は、SQL Server 2016 SP1 で提供される主要な機能強化をまとめたものです。

|機能|[説明]|詳細情報|
|---|---|---|
|TF 715 での自動 TABLOCK によるヒープへの一括挿入| トレース フラグ 715 は、非クラスター化インデックスのないヒープへの一括読み込み操作用に、テーブル ロックを有効にします。|[SAP ワークロードを SQL Server に 2.5 倍の速さで移行する](https://blogs.msdn.microsoft.com/sql_server_team/migrating-sap-workloads-to-sql-server-just-got-2-5x-faster/)|
|CREATE または ALTER|ストアド プロシージャ、トリガー、ユーザー定義関数、ビューなどのオブジェクトを展開します。|[SQL Server データベース エンジンのブログ](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/11/17/create-or-alter-another-great-language-enhancement-in-sql-server-2016-sp1/)|
|DROP TABLE によるレプリケーションのサポート|レプリケーションに対する DROP TABLE DDL のサポートにより、レプリケーション アーティクルを削除できます。|[KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactiona)|
|Filestream RsFx ドライバーの署名|Windows ハードウェア デベロッパー センター ダッシュボード ポータル (開発ポータル) を使って Filestream RsFx ドライバーに署名して認定することで、SQL Server 2016 SP1 Filestream RsFx ドライバーを Windows Server 2016/Windows 10 に問題なくインストールできます。|[SAP ワークロードを SQL Server に 2.5 倍の速さで移行する](https://blogs.msdn.microsoft.com/sql_server_team/migrating-sap-workloads-to-sql-server-just-got-2-5x-faster/)|
|SQL サービス アカウントに対する LPIM - プログラムでの識別|DBA は、サービスの開始時に Lock Pages in Memory (LPIM) 特権が有効になっているかどうかをプログラムで識別できます。|[開発者の選択:SQL Server の LPIM および IFI 特権をプログラムで識別する](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-programmatically-identify-lpim-and-ifi-privileges-in-sql-server)|
|変更の追跡の手動クリーンアップ|新しいストアド プロシージャは、必要に応じて変更の追跡の内部テーブルをクリーンアップします。| [KB 3173157](https://support.microsoft.com/help/3173157/adds-a-stored-procedure-for-the-manual-cleanup-of-the-change-tracking)|
|ローカル一時テーブルの並列 INSERT..SELECT の変更|INSERT..SELECT 操作での新しい並列 INSERT。|[SQL Server Customer Advisory Team](https://blogs.msdn.microsoft.com/sqlcat/2016/07/21/real-world-parallel-insert-what-else-you-need-to-know/)|
|Showplan XML|クエリに対する許可の警告と最大メモリの有効化、トレース フラグの有効化、他の診断情報の表示など、診断機能の強化。 | [KB 3190761](https://support.microsoft.com/help/3190761/update-to-improve-diagnostics-by-expose-data-type-of-the-parameters-fo)|
|ストレージ クラス メモリ|Windows Server 2016 でストレージ クラス メモリを使ってトランザクション処理を支援することで、トランザクションのコミット時間が桁違いに高速化します。|[SQL Server データベース エンジンのブログ](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/12/02/transaction-commit-latency-acceleration-using-storage-class-memory-in-windows-server-2016sql-server-2016-sp1/)|
|USE HINT|クエリ オプションを `OPTION(USE HINT('<option>'))` を使って、サポートされているクエリ レベルのヒントを使うクエリ オプティマイザーの動作を変更します。 QUERYTRACEON とは異なり、USE HINT オプションでは sysadmin 特権は必要ありません。|[開発者の選択:USE HINT クエリ ヒント](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-use-hint-query-hints/)|
|XEvent の追加|新しい Xevent および Perfmon 診断機能により、待機時間のトラブルシューティングが向上します。|[拡張イベント](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)|

さらに、次の修正に注意してください。
- DBA と SQL コミュニティからのフィードバックに基づき、SQL 2016 SP1 以降では Hekaton のログ メッセージが最小限に減ります。
- 新しい[トレース フラグ](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)を確認してください。
- SQL Server 2016 SP1 以降では、WideWorldImporters サンプル データベースの完全バージョンが Standard Edition と Express Edition で動作するようになります。このサンプルは、[Github]( https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0) から入手できます。 サンプルを変更する必要はありません。 Enterprise Edition 用に RTM で作成されたデータベース バックアップが、SP1 の Standard と Express で動作します。

SQL Server 2016 SP1 のインストールでは、インストール後に再起動が必要な場合があります。 ベスト プラクティスとして、SQL Server 2016 SP1 インストール後の再起動を計画して実行することをお勧めします。

### <a name="download-pages-and-more-information"></a>ダウンロード ページと詳細情報

- [Microsoft SQL Server 2016 用 Service Pack 1 のダウンロード](https://www.microsoft.com/download/details.aspx?id=54276)
- [リリース済み SQL Server 2016 Service Pack 1 (SP1)](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/)
- [SQL Server 2016 Service Pack 1 リリース情報](https://support.microsoft.com/kb/3182545)
- ![info_tip](../sql-server/media/info-tip.png) [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] のサービス パックを含む、サポートされているすべてのバージョンのリンクと情報がまとめられている [SQL Server Update Center](https://msdn.microsoft.com/library/ff803383.aspx)

![horizontal-bar.png](media/horizontal-bar.png)

##  <a name="bkmk_2016_ga"></a>SQL Server 2016 Release - 一般公開 (GA)
-   [データベース エンジン (GA)](#bkmk_ga_instalpatch)
-   [Stretch Database (GA)](#bkmk_ga_stretch)
-   [クエリ ストア (GA)](#bkmk_ga_query_store)
-   [製品ドキュメント (GA)](#bkmk_ga_docs)

### ![repl_icon_warn](../database-engine/availability-groups/windows/media/repl-icon-warn.gif) <a name="bkmk_ga_instalpatch"></a> Install Patch Requirement (GA)
**問題およびユーザーへの影響:** SQL Server 2016 の前提条件としてインストールされる Microsoft VC++ 2013 ランタイム バイナリに影響を与える問題が見つかりました。 更新プログラムを利用してこの問題を修正できます。 VC ランタイム バイナリに対するこの更新プログラムをインストールしないと、特定のシナリオにおいて、SQL Server 2016 で安定性の問題が発生する可能性があります。 SQL Server 2016 をインストールする前に、 [KB 3164398](https://support.microsoft.com/kb/3164398)で説明されている修正プログラムがコンピューターに必要かどうかを確認してください。 修正プログラムは、[SQL Server 2016 RTM の累積的な更新プログラム パッケージ 1 (CU1)](https://www.microsoft.com/download/details.aspx?id=53338) にも含まれています。

**解決方法:** 次のいずれかのソリューションを使用します。

- [KB 3138367 - 2013 の Visual C++ および Visual C++ の再頒布可能パッケージ用の更新プログラム](https://support.microsoft.com/kb/3138367)をインストールします。 KB は推奨される解決方法です。 このインストールは、SQL Server 2016 のインストールの前でも後でも実行できます。

    SQL Server 2016 が既にインストール済みの場合は、次の順序で手順を実行します。

    1.  該当する *vcredist_\*exe* をダウンロードします。
    1.  データベース エンジンのすべてのインスタンスで SQL Server サービスを停止します。
    1.  **KB 3138367**をインストールします。
    1.  コンピューターを再起動します。


 - [KB 3164398 - SQL Server 2016 MSVCRT の必須コンポーネントの重要な更新プログラム](https://support.microsoft.com/kb/3164398)をインストールします。

    **KB 3164398**を使用する場合、SQL Server のインストール中、Microsoft Update の実行時、または Microsoft ダウンロード センターからインストールできます。

    - **SQL Server 2016 のインストール中:** SQL Server セットアップを実行するコンピューターからインターネットにアクセスできる場合、SQL Server セットアップにより、SQL Server インストール全体の一部として更新プログラムが調べられます。 更新を承認すると、インストール中にセットアップによりバイナリがダウンロードされて更新されます。

    - **Microsoft Update:** Microsoft Update から、セキュリティに関連しない重要な SQL Server 2016 更新プログラムとしてこの更新プログラムを入手できます。 SQL Server 2016 のインストール後に Microsoft Update を使用してインストールした場合には、更新後にサーバーの再起動が必要になります。

    - **ダウンロード センター:** 最後に、Microsoft ダウンロード センターから更新プログラムをダウンロードできます。 更新用のソフトウェアをダウンロードして、SQL Server 2016 がインストール済みのサーバーにインストールできます。


### <a name="bkmk_ga_stretch"></a>Stretch Database

#### <a name="problem-with-a-specific-character-in-a-database-or-table-name"></a>データベースやテーブルの名前に特定の文字が使用される場合の問題

**問題およびユーザーへの影響:** データベースまたはテーブルで Stretch Database を有効にしようとすると、エラーが発生して失敗します。 この問題は、オブジェクトの名前に、小文字から大文字に変換されるときに別の文字として扱われる文字が含まれている場合に発生します。 この問題が発生する文字の例には、"ƒ" 文字 (ALT+159 を入力すると作成される) があります。

**回避策:** データベースかテーブルに対して Stretch Database を有効にするには、オブジェクトの名前を変更して問題の文字を削除するオプションしかありません。

#### <a name="problem-with-an-index-that-uses-the-include-keyword"></a>INCLUDE キーワードを使用するインデックスの問題

**問題およびユーザーへの影響:** テーブルに対して Stretch Database を有効にしようとする場合に、INCLUDE キーワードを使用して追加の列を組み込んでいるインデックスがそのテーブルにあると、エラーが発生して失敗します。

**回避策:** INCLUDE キーワードを使用しているインデックスを削除し、そのテーブルに対して Stretch Database を有効にしてから、インデックスを再作成します。 その場合には、組織のメンテナンスのプラクティスやポリシーに従っているか確認して、影響を受けるテーブルのユーザーに対する反響をなくすか最小限に抑えるようにしてください。

### <a name="bkmk_ga_query_store"></a>Query Store

#### <a name="problem-with-automatic-data-cleanup-on-editions-other-than-enterprise-and-developer"></a>Enterprise や Developer 以外のエディションでのデータの自動クリーンアップに関する問題

 **問題およびユーザーへの影響:** Enterprise や Developer 以外のエディションでデータの自動クリーンアップが失敗します。
その結果、データを手動で消去しないと、クエリ ストアに使用される領域は構成済みの制限に達するまで時間の経過と共に増えます。 この問題を回避しないと、エラー ログ用に割り当てられたディスク領域もいっぱいになります。クリーンアップを実行しようとするたびにダンプ ファイルが生成されるからです。 クリーンアップをアクティブ化する期間はワークロードの頻度に応じて異なりますが、15 分以内です。

 **回避策:** Enterprise や Developer 以外のエディションでクエリ ストアを使用する計画の場合は、クリーンアップのポリシーを明示的にオフにする必要があります。 この作業は、SQL Server Management Studio ([データベースのプロパティ] ページ) から行うか、Transact SQL スクリプトを使用して行うことができます。

```ALTER DATABASE <database name> SET QUERY_STORE (OPERATION_MODE = READ_WRITE, CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 0), SIZE_BASED_CLEANUP_MODE = OFF)```

また、クエリ ストアが読み取り専用モードに移行しないように、手動クリーンアップのオプションを検討してください。 たとえば、次のクエリを実行して、データ領域全体を定期的にクリーンアップします。

```ALTER DATABASE <database name> SET QUERY_STORE CLEAR```

また、次のクエリ ストアのストアド プロシージャを定期的に実行して、ランタイム統計、特定のクエリ、または計画をクリーンアップします。

- `sp_query_store_reset_exec_stats`

- `sp_query_store_remove_plan`

- `sp_query_store_remove_query`


###  <a name="bkmk_ga_docs"></a> 製品ドキュメント (GA)
 **問題およびユーザーへの影響:** SQL Server 2016 のドキュメントのダウンロード可能なバージョンはまだありません。 ヘルプ ライブラリ マネージャーを使って **オンラインからコンテンツをインストール**しようとすると、SQL Server 2012 および SQL Sever 2014 のドキュメントは表示されますが、SQL Server 2016 のドキュメントのオプションはありません。

 **回避策:** 次のいずれかの回避策を使用してください。

 ![SQL Server のヘルプ設定の管理](../sql-server/media/docs-sql2016-managehelpsettings.png "SQL Server のヘルプ設定の管理")

-   **[オンラインまたはローカル ヘルプの選択]** オプションを使用し、[オンライン ヘルプを使用する] にヘルプを構成します。

-   **[オンラインからコンテンツをインストール]** オプションを使用し、SQL Server 2014 のコンテンツをダウンロードします。

 **F1 ヘルプ:** 仕様上、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] で F1 キーを押すと、ブラウザーでオンライン バージョンの F1 ヘルプ記事が表示されます。 この問題は、ブラウザー ベースのヘルプで、ローカル ヘルプのインストールを構成した場合でも発生します。

**コンテンツの更新:** SQL Server Management Studio と Visual Studio では、ドキュメントの追加プロセス中に、ヘルプ ビューアーのアプリケーションが応答を停止することがあります。 この問題を解決するには、次の手順を実行します。 この問題の詳細については、「 [Visual Studio ヘルプ ビューアーがフリーズする](https://msdn.microsoft.com/library/mt654096.aspx)」を参照してください。

* メモ帳で %LOCALAPPDATA%\Microsoft\HelpViewer2.2\HlpViewer_SSMS16_en-US.settings | HlpViewer_VisualStudio14_en-US.settings ファイルを開き、次のコード内の日付を将来の日付に変更します。

```
     Cache LastRefreshed="12/31/2017 00:00:00"
```

## <a name="additional-information"></a>追加情報
+ [SQL Server 2016 のインストール](../database-engine/install-windows/installation-for-sql-server-2016.md)
+ [SQL Server Update Center - サポート対象のすべてのバージョンのリンクと情報](https://msdn.microsoft.com/library/ff803383.aspx)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png "MS_Logo_X-Small")
