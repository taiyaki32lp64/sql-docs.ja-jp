---
title: クエリのストアを使用した、パフォーマンスの監視 | Microsoft Docs
ms.custom: ''
ms.date: 09/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store
- Query Store, described
ms.assetid: e06344a4-22a5-4c67-b6c6-a7060deb5de6
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f652fc8771162c81a7d86f0984eece90892e3cd3
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909310"
---
# <a name="monitoring-performance-by-using-the-query-store"></a>クエリのストアを使用した、パフォーマンスの監視
[!INCLUDE[appliesto-ss-asdb-xxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のクエリのストア機能により、クエリ プランの選択やパフォーマンスを把握できます。 これにより、クエリ プランの変更によって生じるパフォーマンスの違いがすばやくわかるようになり、パフォーマンス上のトラブルシューティングを簡略化できます。 クエリのストアは、自動的にクエリ、プラン、および実行時統計の履歴をキャプチャし、確認用に保持します。 データは時間枠で区分されるため、データベースの使用パターンを表示して、サーバー上でクエリ プランが変わった時点を確認することができます。 [ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md) オプションを使用してクエリ ストアを構成できます。 
  
 Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)] におけるクエリ ストアの運用について詳しくは、「[Azure SQL Database でクエリ ストアを運用する](https://azure.microsoft.com/documentation/articles/sql-database-operate-query-store/)」をご覧ください。  
 
> [!IMPORTANT]
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] の Just In Time ワークロード分析情報のためにクエリ ストアを使用している場合は、[KB 4340759](https://support.microsoft.com/help/4340759) におけるパフォーマンスのスケーラビリティの修正を、できるだけ早くインストールするよう計画します。 
  
##  <a name="Enabling"></a> クエリのストアを有効にする  
 既定では、クエリのストアは新しいデータベースに対してアクティブではありません。  
  
#### <a name="use-the-query-store-page-in-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の [クエリ ストア] ページを使う  
  
1.  オブジェクト エクスプローラーで、データベースを右クリックし、 **[プロパティ]** をクリックします。  
  
    > [!NOTE]  
    > [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] のバージョン 16 以降が必要です。  
  
2.  **[データベースのプロパティ]** ダイアログ ボックスで、 **[クエリのストア]** ページをクリックします。  
  
3.  **[操作モード (要求)]** ボックスで、 **[読み取り、書き込み]** を選択します。  

#### <a name="use-transact-sql-statements"></a>Transact-SQL ステートメントを使用する  
  
**ALTER DATABASE** ステートメントを使用してクエリのストアを有効にします。 例:  
  
```sql  
ALTER DATABASE AdventureWorks2012 
SET QUERY_STORE = ON (OPERATION_MODE = READ_WRITE); 
```  
  
クエリ ストアに関連する構文オプションの詳細については、「[ALTER DATABASE SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)」を参照してください。  
  
> [!NOTE]  
> **マスター** データベースまたは **tempdb** データベースに対しては、クエリ ストアを有効にできません。  
 
> [!IMPORTANT]
> クエリ ストアを有効にして、ワークロードに合わせて調整された状態を維持するための情報については、「[クエリ ストアを使用するときの推奨事項](../../relational-databases/performance/best-practice-with-the-query-store.md#Configure)」を参照してください。
 
## <a name="About"></a> クエリのストア内の情報  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のどの特定のクエリの実行プランも、通常、統計情報やスキーマの変更、インデックスの作成または削除などのさまざまな理由により、時間の経過とともに進化します。プロシージャ キャッシュ (ここにキャッシュされたクエリ プランが格納される) には、最新の実行プランのみ格納されます。 メモリ負荷が原因で、プランがプラン キャッシュから削除されることもあります。 その結果、実行プランの変更によるクエリ パフォーマンスの低下が深刻なレベルになり、解決に時間を要する場合があります。  
  
 クエリ ストアには、1 つのクエリにつき複数の実行プランが保持されるため、クエリの特定の実行プランを使用するようクエリ プロセッサに指示するポリシーを強制できます。 これをプラン強制と呼びます。 クエリのストアのプラン強制は、 [USE PLAN](../../t-sql/queries/hints-transact-sql-query.md) クエリ ヒントに似たメカニズムを使用して提供されますが、ユーザー アプリケーションを変更する必要はありません。 プラン強制を使用することで、プラン変更によるクエリ パフォーマンスの低下をきわめて短時間に解決できます。  

> [!NOTE]
> クエリ ストアでは、SELECT、INSERT、UPDATE、DELETE、MERGE、BULK INSERT などの DML ステートメントのプランが収集されます。

> [!NOTE]  
> 既定では、ネイティブ コンパイルされるストアド プロシージャのデータがクエリ ストアで収集されることはありません。 ネイティブ コンパイルされるストアド プロシージャのデータを収集するには、[sys.sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) を使用してください。

**待機統計**は、[!INCLUDE[ssde_md](../../includes/ssde_md.md)] のパフォーマンスのトラブルシューティングに役立つもう 1 つの情報源です。 長い間、待機統計はインスタンス レベルでしか使うことができず、待機を特定のクエリにバックトラックするのは困難でした。 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 以降、待機状態を追跡するディメンションがクエリ ストアに含まれます。次の例では、クエリ ストアで待機状態の収集が有効になります。

```sql
ALTER DATABASE AdventureWorks2012 
SET QUERY_STORE = ON ( WAIT_STATS_CAPTURE_MODE = ON );
```

このクエリのストアの機能を使用する一般的なシナリオは次のとおりです。  
  
-   前のクエリ プランを強制的に適用することにより、プラン パフォーマンスの低下をすばやく発見し修正します。 実行プランの変更によって最近パフォーマンスが低下したクエリを修正します。  
-   特定の時間枠内にクエリが実行された回数を確認し、パフォーマンス リソースの問題に関するトラブルシューティングにおいて DBA を支援します。  
-   上位 *n* クエリ (過去 *x* 時間内) を、実行時間やメモリ消費量などを基に識別します。  
-   指定したクエリのクエリ プランの履歴を監査します。  
-   特定のデータベースのリソース (CPU、I/O、メモリ) の使用パターンを分析します。  
-   リソースで待機している上位 n クエリを識別します。 
-   特定のクエリまたはプランの待機の性質を理解します。
  
クエリ ストアには 3 つのストアが含まれます。
- **プラン ストア**は、実行プラン情報の保存用です。     
- **ランタイム統計ストア**は、実行統計情報の保存用です    
- **待機統計ストア**は、待機統計情報の保存用です     
 
クエリのためにプラン ストア内に格納できる一意のプラン数は、 **max_plans_per_query** 構成オプションによって制限されています。 パフォーマンスを向上させるために、この情報はストアに非同期的に書き込まれます。 領域使用量を最小にするため、ランタイム統計情報ストアのランタイム実行統計情報は、一定の時間枠で集計されます。 これらのストア内の情報は、クエリのストアのカタログ ビューに対してクエリを実行することによって表示できます。  
  
次のクエリは、クエリのストア内のクエリとプランに関する情報を返します。  
  
```sql  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
INNER JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
INNER JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
 
##  <a name="Regressed"></a> 機能低下したクエリ機能を使用する  
クエリのストアを有効にしてから、[オブジェクト エクスプローラー] ペインのデータベースの部分を更新して、 **[クエリ ストア]** セクションを追加します。  
  
![SQL Server 2016 の SSMS オブジェクト エクスプローラーでのクエリ ストア ツリー](../../relational-databases/performance/media/objectexplorerquerystore.PNG "SQL Server 2016 の SSMS オブジェクト エクスプローラーでのクエリ ストア ツリー")   ![SQL Server 2017 の SSMS オブジェクト エクスプローラーでのクエリ ストア ツリー](../../relational-databases/performance/media/objectexplorerquerystore_sql17.PNG "SQL Server 2017 の SSMS オブジェクト エクスプローラーでのクエリ ストア ツリー") 
  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で **[機能低下したクエリ]** を選択し、 **[機能低下したクエリ]** ペインを開きます。 [機能低下したクエリ] ペインにクエリと、クエリのストア内のプランが表示されます。 上部のドロップダウン ボックスを使用し、さまざまな条件に基づいてクエリをフィルター処理します:**実行時間 (ミリ秒)** (既定)、CPU 時間 (ミリ秒)、論理読み取り (KB)、論理書き込み (KB)、物理読み取り (KB)、CLR 時間 (ミリ秒)、DOP、メモリ消費量 (KB)、行数、使用済みログ メモリ (KB)、使用済み一時 DB メモリ (KB)、待機時間 (ミリ秒)。  
プランを選択して、グラフィカルなクエリ プランを表示します。 ボタンを使用して、ソース クエリの表示、クエリ プランの強制と強制解除、グリッド形式とグラフ形式の切り替え、選択したプランの比較 (複数選択時)、表示の更新を行うことができます。  
  
![SQL Server 2016 の SSMS オブジェクト エクスプローラーでの低下したクエリ](../../relational-databases/performance/media/objectexplorerregressedqueries.PNG "SQL Server 2016 の SSMS オブジェクト エクスプローラーでの低下したクエリ")  
  
プランを強制的に適用するには、クエリとプランを選択してから、 **[プランの強制]** をクリックします。 強制できるプランは、クエリ プランの機能によって保存され、クエリ プランのキャッシュに保持されているプランのみです。

##  <a name="Waiting"></a> 待機クエリの検索
[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 以降では、クエリごとの時系列の待機統計情報をクエリ ストアで使用できます。 

クエリ ストアでは、待機の種類が**待機カテゴリ**に組み合わされます。 待機カテゴリから待機の種類へのマッピングは、[sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md#wait-categories-mapping-table) で使用できます。

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v18 以降では、 **[クエリ待機統計]** を選択して **[クエリ待機統計]** ペインを開きます。 [クエリ待機統計] ペインには、クエリ ストアで上位の待機カテゴリを含む棒グラフが表示されます。 上部のドロップダウンを使用して、待機時間の集計条件を選択します (平均、最大、最小、標準偏差、**合計** (既定値))。

 ![SQL Server 2017 の SSMS オブジェクト エクスプローラーでのクエリ待機統計](../../relational-databases/performance/media/query-store-waits.PNG "SQL Server 2017 の SSMS オブジェクト エクスプローラーでのクエリ待機統計")

棒をクリックして待機カテゴリを選択すると、選択した待機カテゴリの詳細ビューが表示されます。 この新しい棒グラフには、その待機カテゴリの原因になっているクエリが含まれます。 
  
 ![SQL Server 2017 の SSMS オブジェクト エクスプローラーでのクエリ待機統計の詳細ビュー](../../relational-databases/performance/media/query-store-waits-detail.PNG "SQL Server 2017 の SSMS オブジェクト エクスプローラーでのクエリ待機統計の詳細ビュー")

上部のドロップダウン ボックスを使用して、選択した待機カテゴリのさまざまな待機時間条件に基づいてクエリをフィルター処理します (平均、最大、最小、標準偏差、**合計**(既定値))。 プランを選択して、グラフィカルなクエリ プランを表示します。 ソース クエリの表示、クエリ プランの強制と強制解除、表示の更新に使用できるボタンが用意されています。  

**待機カテゴリ**では、異なる待機種類が性質の類似性によってバケットに組み合わされます。 問題の解決に必要なフォローアップ分析は待機カテゴリによって異なりますが、同じカテゴリの待機種類からは非常によく似たトラブルシューティング エクスペリエンスが得られ、待機の先頭に影響受けたクエリを提供することは、このような調査の大部分を正常に完了するために不足している部分です。

クエリ ストアに待機カテゴリが導入される前後でのワークロードの詳細情報の取得方法の例を次に示します。

|||| 
|-|-|-|  
|以前のエクスペリエンス|新しいエクスペリエンス|操作|
|データベースごとの高い RESOURCE_SEMAPHORE 待機|特定のクエリに対するクエリ ストアでの高いメモリ待機|クエリ ストアでメモリ消費量の多いクエリを探します。 これらのクエリは、影響を受けるクエリの進行をさらに遅らせる可能性があります。 これらのクエリまたは影響を受けるクエリに、MAX_GRANT_PERCENT クエリ ヒントを使うことを検討します。|
|データベースごとの高い LCK_M_X 待機|特定のクエリに対するクエリ ストアでの高いロック待機|影響を受けるクエリのクエリ テキストを確認し、ターゲット エンティティを明らかにします。 クエリ ストアで同じエンティティを変更している他のクエリを探します。これらは、頻繁に実行されていたり、実行時間が長くなったりします。 これらのクエリを特定した後、コンカレンシーが向上するようにアプリケーション ロジックを変更するか、制限の低い分離レベルを使うことを検討します。|
|データベースごとの高い PAGEIOLATCH_SH 待機|特定のクエリに対するクエリ ストアでの高いバッファー IO 待機|クエリ ストアで、物理読み取り数が多いクエリを検索します。 それらが IO 待機の長いクエリと一致する場合は、スキャンではなくシークを行うように基になるエンティティにインデックスを導入して、クエリの IO オーバーヘッドを最小限に抑えることを検討します。|
|データベースごとの高い SOS_SCHEDULER_YIELD 待機|特定のクエリに対するクエリ ストアでの高い CPU 待機|クエリ ストアで CPU 消費量の多いクエリを探します。 それらの中で、高い CPU 傾向が影響を受けるクエリの高い CPU 待機と関連性のあるクエリを特定します。 それらのクエリの最適化に注目します。プラン回帰または欠落インデックスが存在する可能性があります。|

##  <a name="Options"></a> 構成オプション 
次のオプションは、クエリ ストア パラメーターの構成に使用できます。

*OPERATION_MODE*  
**READ_WRITE** (既定値) または READ_ONLY。  
  
*CLEANUP_POLICY (STALE_QUERY_THRESHOLD_DAYS)*  
`STALE_QUERY_THRESHOLD_DAYS` 引数を構成して、クエリのストア内にデータを保持する日数を指定します。 既定値は、30 です。 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic エディションの場合、既定の日数は **7** 日です。
  
*DATA_FLUSH_INTERVAL_SECONDS*  
クエリ ストアに書き込まれるデータがディスクに永続化される頻度を決定します。 パフォーマンスを最適化するため、クエリ ストアで収集したデータは非同期的にディスクに書き込まれます。 この非同期転送が発生する頻度は `DATA_FLUSH_INTERVAL_SECONDS` で構成されています。 既定値は **900** (15 分) です。  
  
*MAX_STORAGE_SIZE_MB*  
クエリのストアの最大サイズを構成します。 クエリのストア内のデータが `MAX_STORAGE_SIZE_MB` の上限に達すると、クエリのストアは自動的に状態を読み取り/書き込みから読み取り専用に変更し、新しいデータの収集を停止します。 既定値は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] まで) の場合は **100 MB** です。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降では、既定値は **1 GB** です。 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Premium Edition の既定値は **1 GB**、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic エディションの既定値は **10 MB** です。
  
*INTERVAL_LENGTH_MINUTES*  
クエリのストアにランタイムの実行の統計データを集計する時間間隔を決定します。 領域使用量を最適化するため、ランタイム統計情報ストアのランタイム実行統計情報は、一定の時間枠で集計されます。 この固定された時間枠は、`INTERVAL_LENGTH_MINUTES` 引数を介して構成されます。 既定値は **60**です。 
  
*SIZE_BASED_CLEANUP_MODE*  
データの総量が最大サイズに近付いたときにクリーンアップ プロセスを自動的にアクティブにするかどうかを制御します。 **AUTO** (既定値) または OFF。  
  
*QUERY_CAPTURE_MODE*  
クエリのストアが、すべてのクエリをキャプチャするか、実行数とリソース消費量に基づいて関連するクエリをキャプチャするか、または新しいクエリの追加を停止して現在のクエリのみを追跡するかを指定します。 **ALL** (すべてのクエリをキャプチャする)、AUTO (不定期で、不必要なコンパイルと実行期間を持つクエリを無視する)、CUSTOM (ユーザー定義のキャプチャ ポリシー)、または NONE (新しいクエリのキャプチャを停止する) を指定できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] まで) の場合、既定値は **[ALL]** です。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降では、既定値は **AUTO** です。 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] の場合、既定値は **AUTO** です。
  
*MAX_PLANS_PER_QUERY*  
各クエリに対して保持の計画の最大数を表す整数。 既定値は **200** です。  
 
*WAIT_STATS_CAPTURE_MODE*  
クエリ ストアが待機統計情報をキャプチャするかどうかを制御します。 OFF または **ON** (既定値) にすることができます。  
 
**sys.database_query_store_options** ビューにクエリを実行し、クエリ ストアの現在のオプションを確認します。 値に関する詳細については、「[sys.database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)」を参照してください。  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用してオプションを設定する方法の詳細については、「 [オプション管理](#OptionMgmt)」をご覧ください。  
  
## <a name="Related"></a> 関連するビュー、関数、プロシージャ  
 クエリのストアは、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] か、次のビューとプロシージャを使用して表示および管理します。  

### <a name="query-store-functions"></a>クエリ ストア関数  
 関数は、クエリ ストアの操作に役立ちます。 
 
||| 
|-|-|  
|[sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)|| 
  
### <a name="query-store-catalog-views"></a>クエリのストアのカタログ ビュー  
 カタログ ビューはクエリのストアの情報を提供します。  

||| 
|-|-|  
|[sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)|[sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)|  
|[sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)|[sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)|  
|[sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)|[sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)|  
|[sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)|[sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)|  
  
### <a name="query-store-stored-procedures"></a>クエリのストアのストアド プロシージャ  
 ストアド プロシージャはクエリのストアを構成します。  

||| 
|-|-|  
|[sp_query_store_flush_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)|[sp_query_store_reset_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)|  
|[sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)|[sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)|  
|[sp_query_store_remove_plan &#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)|[sp_query_store_remove_query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)|  
|sp_query_store_consistency_check &#40;Transct-SQL&#41;||  
 
##  <a name="Scenarios"></a> 基本的な使用シナリオ  
  
###  <a name="OptionMgmt"></a> オプション管理  
 このセクションでは、クエリのストアの機能自体を管理する方法に関するガイドラインを示します。  
  
 **クエリのストアが現在アクティブか**  
  
 クエリのストアはユーザー データベース内にデータを格納するため、サイズに上限が設定されています (`MAX_STORAGE_SIZE_MB` で構成)。 クエリのストア内のデータがその上限に達すると、クエリのストアは自動的に状態を読み取り/書き込みから読み取り専用に変更し、新しいデータの収集を停止します。  
  
 [sys.database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md) のクエリを実行して、クエリのストアが現在アクティブであるか、また、ランタイム統計情報を現在収集しているかを確認します。  
  
```sql  
SELECT actual_state, actual_state_desc, readonly_reason,   
    current_storage_size_mb, max_storage_size_mb  
FROM sys.database_query_store_options;  
```  
  
 クエリのストアの状態は、actual_state 列によって決定されます。 目的の状態と異なる場合は、`readonly_reason` 列で詳しい情報が得られます。   
クエリのストアのサイズがクォータを超える場合、この機能は readon_only モードに切り替わります。  
  
 **クエリのストアのオプションを取得する**  
  
 クエリのストアの状態に関する詳細情報については、ユーザー データベースで次を実行します。  
  
```sql  
SELECT * FROM sys.database_query_store_options;  
```  
  
 **クエリのストアの時間間隔を設定する**  
  
 クエリのランタイム統計情報を集計する時間間隔 (既定では 60 分) をオーバーライドできます。  
  
```sql  
ALTER DATABASE <database_name>   
SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 15);  
```  
  
 > [!NOTE]
 > `INTERVAL_LENGTH_MINUTES` に任意の値を使用することはできません。 次のいずれかを使用します:1、5、10、15、30、60、1440 分。  
  
 間隔の新しい値は、 **sys.database_query_store_options** ビューで明らかになります。  
  
 **クエリのストアの使用領域**  
  
 現在のクエリのストアのサイズと制限をチェックするには、ユーザー データベースで次のステートメントを実行します。  
  
```sql  
SELECT current_storage_size_mb, max_storage_size_mb   
FROM sys.database_query_store_options;  
```  
  
 クエリのストアの記憶域がいっぱいの場合は、次のステートメントを使用して記憶域を拡張します。  
  
```sql  
ALTER DATABASE <database_name>   
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <new_size>);  
```  
  
 **クエリ ストアオプションの設定**  
  
 単一の ALTER DATABASE ステートメントで、クエリのストアの複数のオプションを一度にまとめて設定できます。  
  
```sql  
ALTER DATABASE <database name>   
SET QUERY_STORE (  
    OPERATION_MODE = READ_WRITE,  
    CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30),  
    DATA_FLUSH_INTERVAL_SECONDS = 3000,  
    MAX_STORAGE_SIZE_MB = 500,  
    INTERVAL_LENGTH_MINUTES = 15,  
    SIZE_BASED_CLEANUP_MODE = AUTO,  
    QUERY_CAPTURE_MODE = AUTO,  
    MAX_PLANS_PER_QUERY = 1000,
    WAIT_STATS_CAPTURE_MODE = ON 
);  
```  

  構成オプションの完全一覧は、「[ALTER DATABASE の SET オプション (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)」を参照してください。
  
 **領域のクリーンアップ**  
  
 クエリのストアの内部テーブルは、データベースの作成時に PRIMARY ファイル グループに作成され、その構成を後で変更することはできません。 領域が不足している場合は、次のステートメントを使用して、古いクエリのストアのデータを消去できます。  
  
```sql  
ALTER DATABASE <db_name> SET QUERY_STORE CLEAR;  
```  
  
 または、アドホック クエリ データはクエリの最適化やプラン分析との関連性が低く、ただ場所を占有するだけなので、アドホック クエリ データのみを削除することもできます。  
  
 **アドホック クエリの削除** 
 
 この操作は、24 時間以上前に 1 回実行しただけのクエリを削除します。  
  
```sql  
DECLARE @id int  
DECLARE adhoc_queries_cursor CURSOR   
FOR   
SELECT q.query_id  
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q   
    ON q.query_text_id = qt.query_text_id  
JOIN sys.query_store_plan AS p   
    ON p.query_id = q.query_id  
JOIN sys.query_store_runtime_stats AS rs   
    ON rs.plan_id = p.plan_id  
GROUP BY q.query_id  
HAVING SUM(rs.count_executions) < 2   
AND MAX(rs.last_execution_time) < DATEADD (hour, -24, GETUTCDATE())  
ORDER BY q.query_id ;  
  
OPEN adhoc_queries_cursor ;  
FETCH NEXT FROM adhoc_queries_cursor INTO @id;  
WHILE @@fetch_status = 0  
    BEGIN   
        PRINT @id  
        EXEC sp_query_store_remove_query @id  
        FETCH NEXT FROM adhoc_queries_cursor INTO @id  
    END   
CLOSE adhoc_queries_cursor ;  
DEALLOCATE adhoc_queries_cursor;  
```  
  
 不要になったデータを消去する別のロジックを利用した独自のプロシージャを定義できます。  
  
 上記の例では、 **sp_query_store_remove_query** 拡張ストアド プロシージャを使用して不要なデータを削除しています。 次のプロシージャを使用することもできます。  
  
-   **sp_query_store_reset_exec_stats**。指定されたプランの実行時統計をクリアします。  
-   **sp_query_store_remove_plan**。1 つのプランを削除します。  
 
###  <a name="Peformance"></a> パフォーマンスの監査とトラブルシューティング  
 クエリのストアには、コンパイルの履歴とクエリの実行全体に関するランタイム メトリックスが保持されており、ワークロードに関連した質問の答えを見つけることができます。  
  
 **データベースで最近実行された *n* 個のクエリ。**  
  
```sql  
SELECT TOP 10 qt.query_sql_text, q.query_id,   
    qt.query_text_id, p.plan_id, rs.last_execution_time  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
ORDER BY rs.last_execution_time DESC;  
```  
  
 **各クエリの実行回数。**  
  
```sql  
SELECT q.query_id, qt.query_text_id, qt.query_sql_text,   
    SUM(rs.count_executions) AS total_execution_count  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
GROUP BY q.query_id, qt.query_text_id, qt.query_sql_text  
ORDER BY total_execution_count DESC;  
```  
  
 **去 時間で平均実行時間が長かったクエリの上位。**  
  
```sql  
SELECT TOP 10 rs.avg_duration, qt.query_sql_text, q.query_id,  
    qt.query_text_id, p.plan_id, GETUTCDATE() AS CurrentUTCTime,   
    rs.last_execution_time   
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
WHERE rs.last_execution_time > DATEADD(hour, -1, GETUTCDATE())  
ORDER BY rs.avg_duration DESC;  
```  
  
 **過去 24 時間で平均物理 I/O 読み取り数が多かったクエリの上位と、対応する平均行数および実行カウント。**  
  
```sql  
SELECT TOP 10 rs.avg_physical_io_reads, qt.query_sql_text,   
    q.query_id, qt.query_text_id, p.plan_id, rs.runtime_stats_id,   
    rsi.start_time, rsi.end_time, rs.avg_rowcount, rs.count_executions  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi   
    ON rsi.runtime_stats_interval_id = rs.runtime_stats_interval_id  
WHERE rsi.start_time >= DATEADD(hour, -24, GETUTCDATE())   
ORDER BY rs.avg_physical_io_reads DESC;  
```  
  
 **複数のプランを持つクエリ。** これらは、プラン選択の変更による機能低下の原因になりうるため、特に興味深いクエリです。 次のクエリは、これらのクエリとすべてのプランを識別します。  
  
```sql  
WITH Query_MultPlans  
AS  
(  
SELECT COUNT(*) AS cnt, q.query_id   
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q  
    ON qt.query_text_id = q.query_text_id  
JOIN sys.query_store_plan AS p  
    ON p.query_id = q.query_id  
GROUP BY q.query_id  
HAVING COUNT(distinct plan_id) > 1  
)  
  
SELECT q.query_id, object_name(object_id) AS ContainingObject,   
    query_sql_text, plan_id, p.query_plan AS plan_xml,  
    p.last_compile_start_time, p.last_execution_time  
FROM Query_MultPlans AS qm  
JOIN sys.query_store_query AS q  
    ON qm.query_id = q.query_id  
JOIN sys.query_store_plan AS p  
    ON q.query_id = p.query_id  
JOIN sys.query_store_query_text qt   
    ON qt.query_text_id = q.query_text_id  
ORDER BY query_id, plan_id;  
```  
  
 **最近パフォーマンスが低下したクエリ (別の時点との比較)。** 次のクエリの例では、プラン選択の変更により、過去 48 時間で実行時間が 2 倍になったすべてのクエリを返します。 次のクエリは、すべてのランタイム統計情報の時間間隔を並べて比較します。  
  
```sql  
SELECT   
    qt.query_sql_text,   
    q.query_id,   
    qt.query_text_id,   
    rs1.runtime_stats_id AS runtime_stats_id_1,  
    rsi1.start_time AS interval_1,   
    p1.plan_id AS plan_1,   
    rs1.avg_duration AS avg_duration_1,   
    rs2.avg_duration AS avg_duration_2,  
    p2.plan_id AS plan_2,   
    rsi2.start_time AS interval_2,   
    rs2.runtime_stats_id AS runtime_stats_id_2  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p1   
    ON q.query_id = p1.query_id   
JOIN sys.query_store_runtime_stats AS rs1   
    ON p1.plan_id = rs1.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi1   
    ON rsi1.runtime_stats_interval_id = rs1.runtime_stats_interval_id   
JOIN sys.query_store_plan AS p2   
    ON q.query_id = p2.query_id   
JOIN sys.query_store_runtime_stats AS rs2   
    ON p2.plan_id = rs2.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi2   
    ON rsi2.runtime_stats_interval_id = rs2.runtime_stats_interval_id  
WHERE rsi1.start_time > DATEADD(hour, -48, GETUTCDATE())   
    AND rsi2.start_time > rsi1.start_time   
    AND p1.plan_id <> p2.plan_id  
    AND rs2.avg_duration > 2*rs1.avg_duration  
ORDER BY q.query_id, rsi1.start_time, rsi2.start_time;  
```  
  
 プラン選択の変更に関連するものだけでなく、パフォーマンス低下に関するすべての情報を表示する場合、前のクエリから条件 `AND p1.plan_id <> p2.plan_id` を削除します。  

 **最も待機時間の長いクエリ。**
このクエリは、待機が最も多い上位 10 個のクエリを返します。 
 
 ```sql 
  SELECT TOP 10
    qt.query_text_id,
    q.query_id,
    p.plan_id,
    sum(total_query_wait_time_ms) AS sum_total_wait_ms
FROM sys.query_store_wait_stats ws
JOIN sys.query_store_plan p ON ws.plan_id = p.plan_id
JOIN sys.query_store_query q ON p.query_id = q.query_id
JOIN sys.query_store_query_text qt ON q.query_text_id = qt.query_text_id
GROUP BY qt.query_text_id, q.query_id, p.plan_id
ORDER BY sum_total_wait_ms DESC
 ```
 
 **最近パフォーマンスが低下したクエリ (最近の実行と履歴の実行を比較)。** 次のクエリは、実行期間に基づいてクエリの実行を比較します。 この例では、クエリは、最近の期間 (1 時間) と履歴の期間 (過去1日間) とで実行を比較し、 `additional_duration_workload`の原因となったものを識別します。 このメトリックは、最近の平均実行と履歴の平均実行に最近実行の数を掛けた値の間の差として計算されます。 これは、履歴と比較して、最近の実行でどれほどの期間が追加されたかを表します。  
  
```sql  
--- "Recent" workload - last 1 hour  
DECLARE @recent_start_time datetimeoffset;  
DECLARE @recent_end_time datetimeoffset;  
SET @recent_start_time = DATEADD(hour, -1, SYSUTCDATETIME());  
SET @recent_end_time = SYSUTCDATETIME();  
  
--- "History" workload  
DECLARE @history_start_time datetimeoffset;  
DECLARE @history_end_time datetimeoffset;  
SET @history_start_time = DATEADD(hour, -24, SYSUTCDATETIME());  
SET @history_end_time = SYSUTCDATETIME();  
  
WITH  
hist AS  
(  
    SELECT   
        p.query_id query_id,   
        CONVERT(float, SUM(rs.avg_duration*rs.count_executions)) total_duration,   
        SUM(rs.count_executions) count_executions,  
        COUNT(distinct p.plan_id) num_plans   
     FROM sys.query_store_runtime_stats AS rs  
        JOIN sys.query_store_plan p ON p.plan_id = rs.plan_id  
    WHERE  (rs.first_execution_time >= @history_start_time   
               AND rs.last_execution_time < @history_end_time)  
        OR (rs.first_execution_time <= @history_start_time   
               AND rs.last_execution_time > @history_start_time)  
        OR (rs.first_execution_time <= @history_end_time   
               AND rs.last_execution_time > @history_end_time)  
    GROUP BY p.query_id  
),  
recent AS  
(  
    SELECT   
        p.query_id query_id,   
        CONVERT(float, SUM(rs.avg_duration*rs.count_executions)) total_duration,   
        SUM(rs.count_executions) count_executions,  
        COUNT(distinct p.plan_id) num_plans   
    FROM sys.query_store_runtime_stats AS rs  
        JOIN sys.query_store_plan p ON p.plan_id = rs.plan_id  
    WHERE  (rs.first_execution_time >= @recent_start_time   
               AND rs.last_execution_time < @recent_end_time)  
        OR (rs.first_execution_time <= @recent_start_time   
               AND rs.last_execution_time > @recent_start_time)  
        OR (rs.first_execution_time <= @recent_end_time   
               AND rs.last_execution_time > @recent_end_time)  
    GROUP BY p.query_id  
)  
SELECT   
    results.query_id query_id,  
    results.query_text query_text,  
    results.additional_duration_workload additional_duration_workload,  
    results.total_duration_recent total_duration_recent,  
    results.total_duration_hist total_duration_hist,  
    ISNULL(results.count_executions_recent, 0) count_executions_recent,  
    ISNULL(results.count_executions_hist, 0) count_executions_hist   
FROM  
(  
    SELECT  
        hist.query_id query_id,  
        qt.query_sql_text query_text,  
        ROUND(CONVERT(float, recent.total_duration/  
                   recent.count_executions-hist.total_duration/hist.count_executions)  
               *(recent.count_executions), 2) AS additional_duration_workload,  
        ROUND(recent.total_duration, 2) total_duration_recent,   
        ROUND(hist.total_duration, 2) total_duration_hist,  
        recent.count_executions count_executions_recent,  
        hist.count_executions count_executions_hist     
    FROM hist   
        JOIN recent   
            ON hist.query_id = recent.query_id   
        JOIN sys.query_store_query AS q   
            ON q.query_id = hist.query_id  
        JOIN sys.query_store_query_text AS qt   
            ON q.query_text_id = qt.query_text_id      
) AS results  
WHERE additional_duration_workload > 0  
ORDER BY additional_duration_workload DESC  
OPTION (MERGE JOIN);  
```  
 
###  <a name="Stability"></a> クエリ パフォーマンスの安定性を維持する  
複数回実行されるクエリでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が異なるプランを使用した結果、リソースの使用の仕方や期間が異なっていることに気付く場合があります。 クエリのストアを使用すると、クエリ パフォーマンスが低下している時点を検出し、対象期間の最適なプランを特定できます。 こうすることで、将来のクエリの実行で最適なプランを強制的に適用できます。  
  
パラメーターを持つクエリ (自動的にパラメーター化されたもの、または手動でパラメーター化されたもののいずれか) に関して、クエリ パフォーマンスが一定ではないものを特定することもできます。 さまざまなプランの中で、ほとんどすべてのパラメーター値に対して高速で最適なプランを特定し、そのプランを強制的に適用できます。これにより、より一層多様なユーザー シナリオに対して、予測可能なパフォーマンスを維持できます。  
  
### <a name="force-a-plan-for-a-query-apply-forcing-policy"></a>クエリに対してプランを強制する (強制ポリシーの適用)

特定のクエリに対してプランを強制すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のオプティマイザーでプランの強制が試みられます。 プランの適用に失敗した場合、XEvent が発生し、オプティマイザーは通常の方法で最適化するように指示します。

```sql  
EXEC sp_query_store_force_plan @query_id = 48, @plan_id = 49;  
```  
  
**sp_query_store_force_plan** を使用する場合は、クエリ ストアによってそのクエリのプランとして記録されたプランのみを強制できます。 つまり、クエリで使用できるプランは、クエリのストアがアクティブであったときにそのクエリを実行するために既に使用されているプランのみです。  

#### <a name="a-namectp23a-plan-forcing-support-for-fast-forward-and-static-cursors"></a><a name="ctp23"><a/> 高速順方向カーソルと静的カーソルのサポートを強制するプラン
  
[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.3 以降、クエリ ストアでは、高速順方向カーソルおよび [!INCLUDE[tsql](../../includes/tsql-md.md)] と API の静的カーソルに対してクエリ実行プランを強制する機能がサポートされます。 強制は、`sp_query_store_force_plan` か [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] クエリ ストア レポートの利用によりサポートされます。

### <a name="remove-plan-forcing-for-a-query"></a>クエリに対するプランの強制を解除する

もう一度 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ オプティマイザーを利用して最適なクエリ プランを計算するには、クエリに対して選択されていたプランの強制を **sp_query_store_unforce_plan** を使用して解除します。  
  
```sql  
EXEC sp_query_store_unforce_plan @query_id = 48, @plan_id = 49;  
```  

## <a name="see-also"></a>参照  
 [クエリ ストアを使用する際の推奨事項](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [インメモリ OLTP でのクエリ ストアの使用](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)   
 [クエリ ストアの使用シナリオ](../../relational-databases/performance/query-store-usage-scenarios.md)   
 [クエリ ストアがデータを収集するしくみ](../../relational-databases/performance/how-query-store-collects-data.md)   
 [クエリ ストアのストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [クエリ ストアのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [パフォーマンス監視およびチューニング ツール](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)   
 [利用状況モニターを開く方法 &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)   
 [ライブ クエリ統計](../../relational-databases/performance/live-query-statistics.md)   
 [利用状況モニター](../../relational-databases/performance-monitor/activity-monitor.md)   
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)  
 [Azure SQL Database でクエリ ストアを運用する](https://azure.microsoft.com/documentation/articles/sql-database-operate-query-store/) 
  
