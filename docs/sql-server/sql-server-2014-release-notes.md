---
title: SQL Server 2014 リリース ノート | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2018
ms.prod: sql
ms.technology: install
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: bf4c4922-80b3-4be3-bf71-228247f97004
author: craigg-msft
ms.author: craigg
monikerRange: = sql-server-2014 || = sqlallproducts-allversions
ms.openlocfilehash: 94175594fe2539320941b5a83c1a7aa4b127783f
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155686"
---
# <a name="sql-server-2014-release-notes"></a>SQL Server 2014 リリース ノート
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]
この記事では、[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] のリリースおよび関連する Service Pack での既知の問題について説明します。

## <a name="sql-server-2014-service-pack-2-sp2"></a>SQL Server 2014 Service Pack 2 (SP2)

SQL Server 2014 SP2 には、SQL Server 2014 SP1 CU7 以降にリリースされた修正プログラムのロールアップが含まれています。 ユーザーや SQL コミュニティから寄せられたフィードバックに基づく、パフォーマンス、スケーラビリティ、診断を中心とする機能強化が含まれます。

### <a name="performance-and-scalability-improvements-in-sp2"></a>SP2 でのパフォーマンスとスケーラビリティに関する機能強化

|機能|[説明]|詳細情報|
|---|---|---|
|ソフト NUMA の自動パーティション分割|NUMA ノードあたり 8 個以上の CPU をレポートするシステムでは、ソフト NUMA を自動的に構成できます。|[ソフト NUMA (SQL Server)](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)|
|バッファー プール拡張|SQL Server のバッファー プールを 8 TB より大きく拡張できます。|[バッファー プール拡張](https://docs.microsoft.com/sql/database-engine/configure-windows/buffer-pool-extension)|
|メモリ オブジェクトの動的スケーリング| ノードとコアの数に基づいて、メモリ オブジェクトを動的にパーティション分割します。 この機能強化により、SQL 2014 SP2 以降ではトレース フラグ 8048 が必要なくなります。|[メモリ オブジェクトの動的スケーリング](https://blogs.msdn.microsoft.com/sql_server_team/dynamic-memory-object-scaling/)|
|DBCC CHECK * コマンドに対する MAXDOP ヒント|この機能強化は、MAXDOP を sp_configure 以外の値に設定して DBCC CHECKDB を実行する場合に役に立ちます。|[ヒント (Transact-SQL) - Query](https://docs.microsoft.com/sql/t-sql/queries/hints-transact-sql-query)|
|SOS_RWLock スピンロックの向上|SOS_RWLock に対するスピンロックの必要性をなくし、代わりにインメモリ OLTP に似たロック制御不要の手法を使います。 |[SOS_RWLock の再設計](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/)|
|空間のネイティブ実装|空間クエリのパフォーマンスが大幅に向上します。|[SQL Server 2012 および 2014 での空間パフォーマンスの向上](https://support.microsoft.com/help/3107399/spatial-performance-improvements-in-sql-server-2012-and-2014)

### <a name="supportability-and-diagnostics-improvements-in-sp2"></a>SP2 でのサポート性と診断の向上

|機能|[説明]|詳細情報|
|---|---|---|
|AlwaysON のタイムアウト ログ|リース タイムアウト メッセージに対する新しいログ機能が追加され、現在の時刻と予想される更新時刻がログに記録されるようになります。 |[AlwaysOn 可用性グループのリース タイムアウトの診断の向上](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/)
|AlwaysON XEvent とパフォーマンス カウンター|AlwaysON での待機時間の問題をトラブルシューティングするときの診断が向上する、新しい AlwaysON XEvent とパフォーマンス カウンター。 |[KB 3107172](https://support.microsoft.com/help/3107172/improve-tempdb-spill-diagnostics-by-using-extended-events-in-sql-serve) および [KB 3107400](https://support.microsoft.com/help/3107400/improved-tempdb-spill-diagnostics-in-showplan-xml-schema-in-sql-server)
|変更の追跡のクリーンアップ|新しいストアド プロシージャ sp_flush_CT_internal_table_on_demand は、要求があると変更の追跡の内部テーブルをクリーンアップします。|[KB 3173157](https://support.microsoft.com/help/3173157/adds-a-stored-procedure-for-the-manual-cleanup-of-the-change-tracking)
|データベースの複製|新しい DBCC コマンドを使って、データを除いてスキーマ、メタデータ、統計情報を複製することにより、既存の運用データベースのトラブルシューティングを行います。 複製されたデータベースは、運用環境で使うためのものではありません。|[KB 3177838](https://support.microsoft.com/help/3177838/how-to-use-dbcc-clonedatabase-to-generate-a-schema-and-statistics-only)
|DMF の追加|DMF の新しい sys.dm_db_incremental_stats_properties は、増分統計の情報をパーティションごとに公開します。|[KB 3170114](https://support.microsoft.com/help/3170114/update-to-add-dmf-sys-dm-db-incremental-stats-properties-in-sql-server)
|SQL Server の入力バッファーを取得するための DMF|セッション/要求の入力バッファーを取得するための新しい DMF (sys.dm_exec_input_buffer) を使用できるようになりました。 これは DBCC INPUTBUFFER と同等の機能です。|[sys.dm_exec_input_buffer](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql)
|DROP DDL によるレプリケーションのサポート|トランザクション レプリケーション パブリケーションにアーティクルとして含まれるテーブルを、データベースとパブリケーションから削除できます。|[KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactiona)
|SQL サービス アカウントに対する IFI 特権|SQL Server サービスの起動時にファイルの瞬時初期化 (IFI) が有効かどうかを判断します。|[データベース ファイルの初期化](https://docs.microsoft.com/sql/relational-databases/databases/database-instant-file-initialization)
|メモリ許可 - 問題の処理|メモリ許可を制限してメモリの競合を防ぐことにより、クエリ実行中に診断ヒントを利用できます。|[KB 3107401](https://support.microsoft.com/help/3107401/new-query-memory-grant-options-are-available-min-grant-percent-and-max)
|演算子ごとのクエリ実行軽量プロファイリング |実際の行数など、演算子ごとのクエリ実行統計の収集を最適化します。|[開発者の選択:クエリの進行状況 - いつでも、どこでも](https://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/)
|クエリ実行の診断|クエリ パフォーマンスのトラブルシューティング向上のため、読み取られた実際の行がクエリ実行プランで報告されるようになりました。|[KB 3107397](https://support.microsoft.com/help/3107397/improved-diagnostics-for-query-execution-plans-that-involve-residual-p)
|tempdb の書き込みに対するクエリ実行の診断|Hash Warning および Sort Warnings に、物理 I/O 統計、メモリ使用、および行への影響を追跡するための列が追加されました。 |[temptdb 書き込み診断の向上](https://support.microsoft.com/help/3107172/improve-tempdb-spill-diagnostics-by-using-extended-events-in-sql-serve)
|tempdb のサポート性 |サーバーの起動時に、tempdb ファイルの数および tempdb データ ファイルの変更に対して新しいエラー ログ メッセージを使います。|[KB 2963384](https://support.microsoft.com/help/2963384/fix-sql-server-crashes-when-the-log-file-of-tempdb-database-is-full-in)


さらに、次の修正に注意してください。
- Xevent の呼び出し履歴に、モジュール名と、絶対アドレスではなくオフセットが含まれるようになりました。
- 診断 XE および DMV 間の相関関係の向上 – クエリを一意に識別するために Query_hash と query_plan_hash が使用されます。 DMV はこれらを varbinary(8) として定義するのに対し、XEvent は UINT64 として定義します。 SQL Server に "符号なし bigint" がないため、キャストが機能しない場合があります。 この機能強化では、新しい XEvent アクション/フィルター列が導入されています。これは INT64 として定義されている点を除き、query_hash および query_plan_hash と同等です。 この修正は、XE と DMV 間の関連付けクエリに役立ちます。
- BULK INSERT と BCP での UTF-8 のサポート – BULK INSERT および BCP で、UTF-8 文字セットでエンコードされたデータをエクスポートおよびインポートできるようになりました。

### <a name="download-pages-and-more-information-for-sp2"></a>SP2 のダウンロード ページと詳細情報

- [Microsoft SQL Server 2014 用 Service Pack 2 のダウンロード](https://www.microsoft.com/download/details.aspx?id=53168)
- [SQL Server 2014 Service Pack 2 を使用する](https://www.microsoft.com/download/details.aspx?id=53167)
- [SQL Server 2012 SP2 Express](https://www.microsoft.com/download/details.aspx?id=53167)
- [SQL Server 2014 SP2 Feature Pack](https://www.microsoft.com/download/details.aspx?id=53164)
- [SQL Server 2014 SP2 レポート ビルダー](https://www.microsoft.com/download/details.aspx?id=53163)
- [Microsoft SharePoint 用 SQL Server 2014 SP2 Reporting Services アドイン](https://www.microsoft.com/download/details.aspx?id=53162)
- [SQL Server 2014 SP2 セマンティック言語統計](https://www.microsoft.com/download/details.aspx?id=53165)
- [SQL Server 2014 Service Pack 2 リリース情報](https://support.microsoft.com/help/3171021/sql-server-2014-service-pack-2-release-information)

## <a name="sql-server-2014-service-pack-1-sp1"></a>SQL Server 2014 Service Pack 1 (SP1)

SQL Server 2014 SP1 には、SQL Server 2014 CU 1 から CU 5 までで提供された修正プログラム、および SQL Server 2012 SP2 で以前に出荷された修正プログラムのロールアップが含まれます。

> [!NOTE]
> お使いの SQL Server インスタンスで SSISDB カタログが有効になっていて、SP1 にアップグレードするときにインストール エラーが発生する場合は、「[Error 912 or 3417 when you install SQL Server 2014 SP1](https://support.microsoft.com/help/3018269/error-912-or-3417-when-you-install-sql-server-2014-sp1-build-12-0-4050/)」(SQL Server 2014 SP1 をインストールするときのエラー 912 または 3417) でのこの問題に関する説明に従ってください。

### <a name="download-pages-and-more-information-for-sp1"></a>SP1 のダウンロード ページと詳細情報

- [Microsoft SQL Server 2014 用 Service Pack 1 のダウンロード](https://www.microsoft.com/download/details.aspx?id=46694)
- [SQL Server 2014 Service Pack 1 がリリースされました – 更新](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2014-service-pack-1-has-released-updated/)
- [Microsoft SQL Server 2014 SP1 Express](https://www.microsoft.com/download/details.aspx?id=42299)
- [Microsoft SQL Server 2014 SP1 Feature Pack](https://www.microsoft.com/download/details.aspx?id=46696)


## <a name="before-you-install-sql-server-2014-rtm"></a>SQL Server 2014 RTM をインストールする前に

### <a name="limitations-and-restrictions-in-sql-server-2014-rtm"></a>SQL Server 2014 RTM の制限事項と制約事項

1.  Microsoft SQL Server 2014 CTP 1 から Microsoft SQL Server 2014 RTM へのアップグレードはサポートされていません。  
2.  SQL Server 2014 CTP 1 と SQL Server 2014 RTM のサイド バイ サイド インストールはサポートされていません。  
3.  SQL Server 2014 RTM への SQL Server 2014 CTP 1 データベースのアタッチまたは復元はサポートされていません。  

**回避策:** [なし] :

#### <a name="upgrading-from-sql-server-2014-ctp-2-to-sql-server-rtm"></a>SQL Server 2014 CTP 2 から SQL Server RTM へのアップグレード
アップグレードは完全にサポートされています。 具体的には、次のことを実行できます。

1.  SQL Server 2014 RTM インスタンスに SQL Server 2014 CTP 2 データベースをアタッチ。    
2.  SQL Server 2014 CTP 2 で作成したデータベース バックアップを SQL Server 2014 RTM インスタンスに復元。    
3.  SQL Server 2014 RTM へのインプレース アップグレード。
4.  SQL Server 2014 RTM へのローリング アップグレード。 ローリング アップグレードを開始する前に、手動フェールオーバー モードに切り替える必要があります。 詳細については、「[ダウンタイムとデータ損失を最小限に抑えた可用性グループ サーバーのアップグレードおよび更新](https://msdn.microsoft.com/library/dn178483.aspx)」を参照してください。    
5.  SQL Server 2014 CTP 2 にインストールされたトランザクション パフォーマンス コレクション セットによって収集されたデータを、SQL Server 2014 RTM の SQL Server Management Studio で表示することはできません。その逆も同じです。
  
#### <a name="downgrading-from-sql-server-2014-rtm-to-sql-server-2014-ctp-2"></a>SQL Server 2014 RTM から SQL Server 2014 CTP 2 へのダウングレード  
この操作はサポートされていません。  
  
**回避策:** ダウングレードを実行するための回避策はありません。 SQL Server 2014 RTM にアップグレードする前に、データベースをバックアップすることをお勧めします。  
  
#### <a name="incorrect-version-of-streaminsight-client-on-sql-server-2014-mediaisocab"></a>SQL Server 2014 メディア/ISO/CAB 上の不正なバージョンの StreamInsight クライアント  
SQL Server メディア/ISO/CAB 上に間違ったバージョンの StreamInsight.msi および StreamInsightClient.msi があります (パスは StreamInsight\\\<Architecture\>\\\<Language ID\>)。  
  
**回避策:** [SQL Server 2014 Feature Pack のダウンロード ページ](https://go.microsoft.com/fwlink/?LinkID=306709)から正しいバージョンをダウンロードしてインストールします。  
  
### <a name="ProdDoc"></a>製品ドキュメント RTM
  
レポート ビルダーと PowerPivot のコンテンツが一部の言語で使用できません。 

**問題点:** レポート ビルダーのコンテンツは、次の言語では使用できません。  
  
-   ギリシャ語 (el-GR)  
-   ノルウェー語 (ボークモール) (nb-NO)  
-   フィンランド語 (fi FI)  
-   デンマーク語 (da DK)  
  
[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]では、このコンテンツは製品に付属する CHM ファイルから入手でき、上記の言語でも使用可能でした。 現在 CHM ファイルは製品に付属しておらず、レポート ビルダーのコンテンツは MSDN でのみ使用できます。 MSDN では、これらの言語はサポートされていません。 レポート ビルダーは TechNet からも削除され、上記のサポートされる言語では使用できなくなりました。  
  
**回避策:** [なし] :  
  
**問題点:** Power Pivot のコンテンツは、次の言語では使用できません。
  
-   ギリシャ語 (el-GR)  
-   ノルウェー語 (ボークモール) (nb-NO)  
-   フィンランド語 (fi FI)  
-   デンマーク語 (da DK)  
-   チェコ語 (cs-CZ)  
-   ハンガリー語 (hu-HU)  
-   オランダ語 (オランダ) (nl-NL)  
-   ポーランド語 (pl-PL)  
-   スウェーデン語 (sv-SE)  
-   トルコ語 (tr-TR)  
-   ポルトガル語 (ポルトガル) (pt-PT)  
  
[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]では、このコンテンツは TechNet から入手でき、上記の言語でも使用可能でした。 このコンテンツは TechNet から削除され、上記のサポートされる言語では使用できなくなりました。  
  
**回避策:** [なし] :  
  
### <a name="DBEngine"></a>データベース エンジン (RTM)
  
#### <a name="changes-made-for-standard-edition-in-sql-server-2014-rtm"></a>SQL Server 2014 RTM の Standard Edition に加えられた変更  
SQL Server 2014 Standard では、次の点が変更されています。  
  
-   バッファー プール拡張機能により、構成済みのメモリの最大 4 倍のサイズを使用できます。    
-   最大メモリは 64 GB から 128 GB に拡大されました。  
 
#### <a name="memory-optimization-advisor-flags-default-constraints-as-incompatible"></a>メモリ最適化アドバイザーは既定の制約に対して互換性なしのフラグを設定  
**問題点:** SQL Server Management Studio のメモリ最適化アドバイザーは、すべての既定の制約に対して、互換性なしというフラグを設定します。 既定の制約すべてが、メモリ最適化テーブルでサポートされているわけではありません。アドバイザーは、既定の制約のうち、サポートされている種類とサポートされていない種類を区別しません。 サポートされている既定の制約として、すべての定数や、ネイティブ コンパイル ストアド プロシージャ内でサポートされている式と組み込み関数を挙げることができます。 ネイティブ コンパイル ストアド プロシージャでサポートされる関数の一覧については、「 [ネイティブ コンパイル ストアド プロシージャでサポートされる構造](https://msdn.microsoft.com/library/dn452279(v=sql.120).aspx)」を参照してください。  
  
**回避策:** 障害となる問題を識別する目的でアドバイザーを使用する場合は、互換性のある既定の制約に関する表示を無視してください。 メモリ最適化アドバイザーを使用して、互換性のある既定の制約を含み、障害となる他の問題が存在しないテーブルを移行する場合は、次の手順を実行します:  
  
1.  テーブル定義から既定の制約を削除します。    
2.  アドバイザーを使用して、テーブル上で移行スクリプトを生成します。    
3.  移行スクリプトに、既定の制約を再度追加します。    
4.  移行スクリプトを実行します。  
  
#### <a name="informational-message-file-access-denied-incorrectly-reported-as-an-error-in-the-sql-server-2014-error-log"></a>情報メッセージ "ファイルのアクセスが拒否されました。" が、SQL Server 2014 のエラー ログに誤ってエラーとして報告される  
**問題点:** メモリ最適化テーブルを含むデータベースを持つサーバーを再起動すると、SQL Server 2014 のエラー ログに次の種類のエラー メッセージが出力されることがあります。  
  
```  
[ERROR]Unable to delete file C:\Program Files\Microsoft SQL   
Server\....old.dll. This error may be due to a previous failure to unload   
memory-optimized table DLLs.  
```  
実際は、このメッセージは情報提供だけを目的としており、ユーザーが対応する必要はありません。  
  
**回避策:** [なし] : これは情報メッセージです。  
  
#### <a name="missing-index-details-incorrectly-report-included-columns-for-memory-optimized-table"></a>欠落インデックスの詳細で、メモリ最適化テーブルに対応する付加列が誤って報告される  
**問題点:** SQL Server 2014 がメモリ最適化テーブルに対するクエリで欠落インデックスを検出した場合は、SHOWPLAN_XML 内で欠落インデックスが報告され、sys.dm_db_missing_index_details などでも欠落インデックス DMV が報告されます。 場合によっては、欠落インデックスの詳細に、付加列が含まれています。 メモリ最適化テーブルのすべてのインデックスにはすべての列が暗黙的に含まれているため、メモリ最適化インデックスで付加列を明示的に指定することは許可されません。  
  
**回避策:** メモリ最適化テーブルのインデックスでは、INCLUDE 句を指定しないでください。  
  
#### <a name="missing-index-details-omit-missing-indexes-when-a-hash-index-exists-but-is-not-suitable-for-the-query"></a>ハッシュ インデックスが存在していてもクエリに適していない場合は、欠落インデックスの詳細で欠落インデックスが省略される  
**問題点:** クエリ内で参照されているメモリ最適化テーブルの列でハッシュ インデックスを使用しているが、クエリでインデックスを使用できない場合は、SQL Server 2014 は SHOWPLAN_XML 内や DMV sys.dm_db_missing_index_details 内で欠落インデックスを常に報告するとは限りません。  
  
特に、インデックス キー列のサブセットが関係する等値述語がクエリに含まれている場合や、インデックス キー列が関係する不等値述語がクエリに含まれている場合は、HASH インデックスをそのまま使用することはできず、クエリを効率的に実行するために別のインデックスが必要になります。  
  
**回避策:** ハッシュ インデックスを使用している場合は、クエリとクエリ プランを検討し、インデックス キーのサブセットに対する Index Seek 操作や、不等値述語に対する Index Seek 操作によってクエリに利点がもたらされるかどうかを判断します。 インデックス キーのサブセットに対するシークを実行する必要がある場合は、NONCLUSTERED インデックスを使用するか、シークする必要のある正確な列に対応する HASH インデックスを使用します。 不等値述語に対するシークを実行する必要がある場合は、HASH の代わりに NONCLUSTERED インデックスを使用します。  
  
#### <a name="failure-when-using-a-memory-optimized-table-and-memory-optimized-table-variable-in-the-same-query-if-the-database-option-read_committed_snapshot-is-set-to-on"></a>データベース オプション READ_COMMITTED_SNAPSHOT を ON に設定した場合、メモリ最適化テーブルとメモリ最適化テーブル変数を同じクエリで使用したときにエラーが発生する  
**問題点:** データベース オプション READ_COMMITTED_SNAPSHOT を ON に設定し、ユーザー トランザクションのコンテキスト外にある同じステートメントで、メモリ最適化テーブルとメモリ最適化されたテーブル変数の両方にアクセスした場合は、このエラー メッセージが表示される可能性があります。  
  
```  
Msg 41359  
A query that accesses memory optimized tables using the READ COMMITTED  
isolation level, cannot access disk based tables when the database option  
READ_COMMITTED_SNAPSHOT is set to ON. Provide a supported isolation level  
for the memory optimized table using a table hint, such as WITH (SNAPSHOT).  
```  
  
**回避策:** テーブル変数と共にテーブル ヒント WITH (SNAPSHOT) を使用するか、データベース オプション MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT を ON に設定して、次のステートメントを使用します。  
  
```  
ALTER DATABASE CURRENT   
SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON  
```  
  
#### <a name="procedure-and-query-execution-statistics-for-natively-compiled-stored-procedures-record-worker-time-in-multiples-of-1000"></a>ネイティブ コンパイル ストアド プロシージャに関するプロシージャとクエリ実行の統計で、ワーカー時間が 1,000 の倍数で記録される  
**問題点:** sp_xtp_control_proc_exec_stats または sp_xtp_control_query_exec_stats を使用してネイティブ コンパイル ストアド プロシージャに対するプロシージャまたはクエリ実行の統計の収集を有効にした後、DMV sys.dm_exec_procedure_stats と sys.dm_exec_query_stats 内で、*_worker_time が 1,000 の倍数で報告されます。 ワーカー時間が 500 ミリ秒未満のクエリ実行では、worker_time として 0 が報告されます。  
  
**回避策:** [なし] : ネイティブ コンパイル ストアド プロシージャの実行時間が短いクエリに対応する実行統計 DMV 内で報告された worker_time を信頼しないでください。  
  
#### <a name="error-with-showplan_xml-for-natively-compiled-stored-procedures-that-contain-long-expressions"></a>長い式を含むネイティブ コンパイル ストアド プロシージャに対応する SHOWPLAN_XML にエラーが出力される  
**問題点:** ネイティブ コンパイル ストアド プロシージャに長い式が含まれていて、そのプロシージャに対応する SHOWPLAN_XML を取得する状況で、T-SQL オプション SET SHOWPLAN_XML ON を使用する場合、または Management Studio で "Display Estimated Execution Plan" オプションを使用する場合は、次のエラーが発生する可能性があります。  
  
```  
Msg 41322. MAT/PIT export/import encountered a failure for memory  
optimized table or natively compiled stored procedure with object ID  
278292051 in database ID 6. The error code was  
0xc00cee81.  
```  
  
**回避策:** 以下の 2 つの回避策があります。  
  
1.  次の例のように、式にかっこを追加します。  
  
    次の表記の代わりに、  
  
    ```  
    SELECT @v0 + @v1 + @v2 + ... + @v199  
    ```  
  
    次のように記述します。  
  
    ```  
    SELECT((@v0 + ... + @v49) + (@v50 + ... + @v99)) + ((@v100 + ... + @v149) + (@v150 + ... + @v199))  
    ```  
  
2.  SHOWPLAN を対象にして、わずかに簡略化した式を使用する 2 番目のプロシージャを作成します。プランの全般的な形式は同じままにします。 たとえば、次の表記の代わりに、  
  
    ```  
    SELECT @v0 +@v1 +@v2 +...+@v199  
    ```  
  
    次のように記述します。  
  
    ```  
    SELECT @v0 +@v1  
    ```  
  
#### <a name="using-a-string-parameter-or-variable-with-datepart-and-related-functions-in-a-natively-compiled-stored-procedure-results-in-an-error"></a>ネイティブ コンパイル ストアド プロシージャ内にある DATEPART とそれに関連する関数で文字列パラメーターまたは文字列変数を使用するとエラーが発生する  
**問題点:** ネイティブ コンパイル ストアド プロシージャ内の組み込み関数 DATEPART、DAY、MONTH、YEAR で文字列のパラメーターまたは変数を使うと、datetimeoffset はネイティブ コンパイル ストアド プロシージャでサポートされていないことを示すエラー メッセージが表示されます。  
  
**回避策:** 文字列パラメーターまたは文字列変数を、新しい変数型である datetime2 に代入し、その変数を DATEPART、DAY、MONTH、または YEAR 関数の中で使用します。 例:  
  
```  
DECLARE @d datetime2 = @string  
DATEPART(weekday, @d)  
```  
  
#### <a name="native-compilation-advisor-flags-delete-from-clauses-incorrectly"></a>ネイティブ コンパイル アドバイザーが DELETE FROM 句に対して誤ってフラグを設定する  
**問題点:** ネイティブ コンパイル アドバイザーが、ストアド プロシージャ内の DELETE FROM 句に対して互換性なしのフラグを誤って設定します。  
  
**回避策:** [なし] :  
  
#### <a name="register-through-ssms-adds-dac-meta-data-with-mismatched-instance-ids"></a>SSMS を使用して登録を行うと、不一致のインスタンス ID を持つ DAC メタデータが追加される  
**問題点:** SQL Server Management Studio を使用してデータ層アプリケーション パッケージ (.dacpac) を登録または削除すると、sysdac* テーブルが正しく更新されず、データベースに対して dacpac 履歴のクエリを実行できません。  sysdac_history_internal と sysdac_instances_internal の instance_id が一致せず、結合が許可されません。  
  
**回避策:** この問題は、[データ層アプリケーション フレームワーク](https://www.microsoft.com/download/details.aspx?id=42295)の Feature Pack の再配布で修正されています。  更新プログラムを適用した後、すべての新しい履歴エントリは sysdac_instances_internal テーブル内の instance_id の一覧に含まれる値を使用します。  
  
instance_id の値の不一致という問題が既に発生している場合は、不一致の値を修正する唯一の方法は、MSDB データベースへ書き込む特権を持つユーザーとしてサーバーに接続し、instance_id の値を更新して一致させることです。  同じデータベースから複数の登録イベントと登録解除イベントが発生する場合は、時刻と日付を参照し、どのレコードが現在の instance_id の値と一致しているかを確認する必要があります。  
  
1.  SQL Server Management Studio で、MSDB に対する更新権限を持つログインを使用して、サーバーに接続します。    
2.  MSDB データベースを使用して、新しいクエリを開きます。    
3.  次のクエリを実行し、すべてのアクティブな dac インスタンスを表示します。  修正対象のインスタンスを見つけ、instance_id を書き留めます。  
  
    `select * from` sysdac_instances_internal  
  
4.  次のクエリを実行し、すべての履歴エントリを表示します。  
  
    `select * from` sysdac_history_internal  
  
5.  修正するインスタンスに対応する行を特定します。 
6.  (sysdac_instances_internal テーブルで) sysdac_history_internal.instance_id の値を、手順 3 で書き留めた値に更新します。  
  
    `update` sysdac_history_internal `set` instance_id = '\<手順 3 で書き留めた値\>' `where` \<更新しようとする行に一致する式\>  
  
### <a name="SSRS"></a>Reporting Services (RTM)
  
#### <a name="the-sql-server-2012-reporting-services-native-mode-report-server-cannot-run-side-by-side-with-sql-server-2014-reporting-services-sharepoint-components"></a>SQL Server 2012 Reporting Services ネイティブ モード レポート サーバーを SQL Server 2014 Reporting Services SharePoint コンポーネントとサイド バイ サイドで実行できない  
**問題点:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint コンポーネントが同じサーバーにインストールされている場合、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ネイティブ モードの Windows サービス SQL Server Reporting Services (ReportingServicesService.exe) の起動に失敗します。  
  
**回避策:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint コンポーネントをアンインストールし、Microsoft SQL Server 2012 Reporting Services の Windows サービスを再起動します。  
  
**詳細情報:**  
  
[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ネイティブ モードは、次のいずれかの状況ではサイド バイ サイドで実行することはできません。  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 製品用アドイン    
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 共有サービス  
  
サイド バイ サイド インストールでは、 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ネイティブ モード Windows Service を起動することはできません。 次に示すようなエラー メッセージが Windows イベント ログに記録されます。  
  
```  
Log Name:   Application  
Source:          Report Server (<SQL instance ID>)  
Event ID:        117  
Task Category:   Startup/Shutdown  
Level:           Error  
Keywords:        Classic  
Description:     The report server database is an invalid version.  
  
Log Name:      Application  
Source:        Report Server (<SQL instance ID>)  
Event ID:      107  
Task Category: Management  
Level:         Error  
Keywords:      Classic  
Description:   Report Server (DENALI) cannot connect to the report server database.  
```  
  
詳細については、「 [SQL Server 2014 Reporting Services の役立つヒントおよびトラブルシューティング](https://go.microsoft.com/fwlink/?LinkID=391254)」を参照してください。  
  
#### <a name="required-upgrade-order-for-multi-node-sharepoint-farm-to-sql-server-2014-reporting-services"></a>SQL Server 2014 Reporting Services を使用する複数ノードの SharePoint ファームで必要なアップグレードの順序  
**問題点:** SharePoint 製品用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインのすべてのインスタンスをアップグレードする前に、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 共有サービスのインスタンスをアップグレードした場合は、複数ノード ファームでのレポートの表示に失敗します。  
  
**回避策:** 複数ノードの SharePoint ファームで、次の手順を行います。  
  
1.  最初に、SharePoint 製品用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインのすべてのインスタンスをアップグレードします。    
2.  次に、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 共有サービスのすべてのインスタンスをアップグレードします。  
  
詳細については、「 [SQL Server 2014 Reporting Services の役立つヒントおよびトラブルシューティング](https://go.microsoft.com/fwlink/?LinkID=391254)」を参照してください。  
  
### <a name="AzureVM"></a>Azure Virtual Machines 上の SQL Server 2014 RTM  
  
#### <a name="the-add-azure-replica-wizard-returns-an-error-when-configuring-an-availability-group-listener-in-azure"></a>Azure で可用性グループ リスナーを構成するときに Azure のレプリカ追加ウィザードでエラーが返される  
**問題点:** 可用性グループにリスナーが存在する場合は、Azure でリスナーを構成しようとしたときに、Azure のレプリカ追加ウィザードでエラーが返されます。  
  
Azure サブネットを含め、可用性グループのレプリカをホストしているすべてのサブネットで、可用性グループ リスナーに 1 つの IP アドレスを割り当てることが必要とされるのが、この問題の原因です。  
  
**回避策:**  
  
1.  リスナーのページで、可用性グループ レプリカをホストする Azure サブネット内にある未使用の静的 IP アドレスを、可用性グループ リスナーに割り当てます。  
  
    この回避策により、ウィザードは Azure 内でレプリカの追加を完了することができます。  
  
2.  ウィザードが完了した後、「[Azure での AlwaysOn 可用性グループに対するリスナーの構成](https://msdn.microsoft.com/library/dn376546.aspx)」で説明されているように、Azure でリスナーの構成を完了する必要があります  
  
### <a name="SSAS"></a>Analysis Services (RTM)
  
#### <a name="msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2010-new-farm-configured-with-sql-server-2014"></a>SQL Server 2014 で構成された SharePoint 2010 の新しいファーム用に MSOLAP.5 のダウンロード、インストール、および登録が必要  
**問題点:**  
  
-   SQL Server 2014 で構成された SharePoint 2013 の新しいファーム用に MSOLAP.5 をダウンロード、インストール、および登録する必要があります。SQL Server 2014 RTM の展開と組み合わせて SharePoint 2010 ファームを構成した場合は、接続文字列で参照されているプロバイダーがインストールされていないことが原因で、PowerPivot ブックをデータ モデルに接続できません。  
  
**回避策:**  
  
1.  [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] Feature Pack から MSOLAP.5 プロバイダーをダウンロードします。 Excel Services を実行しているアプリケーション サーバーにプロバイダーをインストールします。 詳細については、「[Microsoft SQL Server 2012 SP1 Feature Pack](https://www.microsoft.com/download/details.aspx?id=35580)」の「Microsoft Analysis Services OLE DB Provider for Microsoft SQL Server 2012 SP1」を参照してください。  
  
2.  MSOLAP.5 を信頼できるプロバイダーとして SharePoint Excel Services に登録します。 詳細については、「 [Excel Services で信頼できるデータ プロバイダーとして MSOLAP.5 を追加](https://technet.microsoft.com/library/hh758436.aspx)」を参照してください。  
  
**詳細情報:**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] には MSOLAP.6 が含まれます。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] と [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssGemini](../includes/ssgemini-md.md)] のブックでは MSOLAP.5 が使用されます。 Excel Services を実行しているコンピューターに MSOLAP.5 がインストールされていない場合は、Excel Services はデータ モデルを読み込むことができません。  
  
#### <a name="msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2013-new-farm-configured-with-sql-server-2014"></a>SQL Server 2014 で構成された SharePoint 2013 の新しいファーム用に MSOLAP.5 のダウンロード、インストール、および登録が必要  
**問題点:**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] の配置で構成された SharePoint 2013 ファームでは、接続文字列で参照されているプロバイダーがインストールされていないことが原因で、MSOLAP.5 プロバイダーを参照する Excel ブックから表形式のデータ モデルに接続することはできません。  
  
**回避策:**  
  
1.  [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] Feature Pack から MSOLAP.5 プロバイダーをダウンロードします。 Excel Services を実行しているアプリケーション サーバーにプロバイダーをインストールします。 詳細については、「[Microsoft SQL Server 2012 SP1 Feature Pack](https://www.microsoft.com/download/details.aspx?id=35580)」の「Microsoft Analysis Services OLE DB Provider for Microsoft SQL Server 2012 SP1」を参照してください。  
  
2.  MSOLAP.5 を信頼できるプロバイダーとして SharePoint Excel Services に登録します。 詳細については、「 [Excel Services で信頼できるデータ プロバイダーとして MSOLAP.5 を追加](https://technet.microsoft.com/library/hh758436.aspx)」を参照してください。  
  
**詳細情報:**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] には MSOLAP.6 が含まれます。 ただし、SQL Server 2014 PowerPivot ブックでは MSOLAP.5 が使用されます。 Excel Services を実行しているコンピューターに MSOLAP.5 がインストールされていない場合は、Excel Services はデータ モデルを読み込むことができません。  
  
#### <a name="corrupt-data-refresh-schedules-rtm"></a>データ更新スケジュールの破損 (RTM)
**問題点:**  
  
-   更新スケジュールを更新すると、スケジュールが壊れて使用できなくなります。  
  
**回避策:**  
  
1.  Microsoft Excel で、カスタムの詳細プロパティをクリアします。 サポート技術情報 [KB 2927748](https://support.microsoft.com/kb/2927748) の「回避策」を参照してください。  
  
**詳細情報:**  
  
-    更新スケジュールのシリアル化された長さが元のスケジュールより小さい場合、ブックのデータ更新スケジュールを更新すると、バッファー サイズが正しく更新されず、新しいスケジュール情報が古いスケジュール情報とマージされるため、スケジュールが破損します。  
  
### <a name="DQS"></a>Data Quality Services (RTM)
  
#### <a name="no-cross-version-support-for-data-quality-services-in-master-data-services"></a>バージョンの異なる Master Data Services での Data Quality Service はサポートされない  
**問題点:** 次のシナリオはサポートされていません。  
  
-   Data Quality Services 2012 がインストールされている SQL Server 2012 内にある SQL Server データベース エンジンのデータベースでの Master Data Services 2014 のホスティング。  
  
-   Data Quality Services 2014 がインストールされている SQL Server 2014 内にある SQL Server データベース エンジンのデータベースでの Master Data Services 2012 のホスティング。  
  
**回避策:** データベース エンジンのデータベース、および Data Quality Services と同じバージョンの Master Data Services を使用してください。  
  
### <a name="UA"></a>アップグレード アドバイザーの問題点 (RTM)
  
#### <a name="sql-server-2014-upgrade-advisor-reports-irrelevant-upgrade-issues-for-sql-server-reporting-services"></a>SQL Server 2014 アップグレード アドバイザーが SQL Server Reporting Services に関係のないアップグレードの問題点を報告する  
**問題点:** SQL Server 2014 メディアに収録されている SQL Server アップグレード アドバイザー (SSUA) が SQL Server Reporting Services サーバーを分析するときに、不適切な複数のエラーを報告します。  
  
**回避策:** この問題は、[SSUA 用の SQL Server 2014 Feature Pack](https://go.microsoft.com/fwlink/?LinkID=306709) の一部として提供される SQL Server アップグレード アドバイザーで解決できます。  
  
#### <a name="sql-server-2014-upgrade-advisor-reports-an-error-when-analyzing-sql-server-integration-services-server"></a>SQL Server 2014 アップグレード アドバイザーで SQL Server Integration Services サーバーを分析するときにエラーが報告される  
**問題点:** SQL Server 2014 メディアに収録されている SQL Server Upgrade Advisor (SSUA) により、SQL Server Integration Services サーバーを分析するときにエラーが報告されます。  ユーザーに対して表示されるエラーは、次のようなものです。  
  
```  
The installed version of Integration Services does not support Upgrade Advisor.   
The assembly information is "Microsoft.SqlServer.ManagedDTS, Version=11.0.0.0,   
Culture=neutral, PublicKeyToken=89845dcd8080cc91  
```  
  
**回避策:** この問題は、[SSUA 用の SQL Server 2014 Feature Pack](https://go.microsoft.com/fwlink/?LinkID=306709) の一部として提供される SQL Server アップグレード アドバイザーで解決できます。  
  
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
