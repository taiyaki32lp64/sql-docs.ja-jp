---
title: クエリ ストアを使用する際のベスト プラクティス | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, best practices
ms.assetid: 5b13b5ac-1e4c-45e7-bda7-ebebe2784551
author: pmasl
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||= azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d35637b9452500caac680439bd1ef09442d9ef11
ms.sourcegitcommit: af6f66cc3603b785a7d2d73d7338961a5c76c793
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73142777"
---
# <a name="best-practices-with-query-store"></a>クエリ ストアを使用する際のベスト プラクティス
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  この記事では、ワークロードで SQL Server クエリ ストアを使用するためのベスト プラクティスについて説明します。
  
##  <a name="SSMS"></a> 最新の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用する  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] には、クエリ ストアを構成し、ワークロードに関する収集データを使用するための一連のユーザー インターフェイスが用意されています。 最新バージョンの [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] は[ここ](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)からダウンロードしてください。  
  
 トラブルシューティング シナリオでクエリ ストアを使用する方法の簡単な説明については、[\@Azure ブログのクエリ ストアに関する記事](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)を参照してください。  
  
##  <a name="Insight"></a> UseAzure SQL Database で Query Performance Insight を使用する  
 Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)] でクエリ ストアを実行する場合、**Query Performance Insight** を使用して、経時的に DTU 消費量を分析できます。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用して、CPU、メモリ、I/O など、すべてのクエリの詳細なリソース消費量を取得することができますが、Query Performance Insight を使用すると、データベースの DTU 全体の消費量に対する影響を簡単かつ効率的に確認できます。 詳細については、「 [Azure SQL Database Query Performance Insight](https://azure.microsoft.com/documentation/articles/sql-database-query-performance/)」を参照してください。

##  <a name="use-query-store-with-elastic-pool-databases"></a>エラスティック プール データベースでクエリ ストアを使用する
クエリ ストアは、すべてのデータベースで (高密度でパックされたプールであっても) 問題なく使用できます。 エラスティック プール内の多数のデータベースに対してクエリ ストアを有効にすると発生する可能性があった、リソースの過剰使用に関連するすべての問題は解決されました。

##  <a name="Configure"></a> ワークロードに合わせてクエリ ストアを調整する  
 ワークロードとパフォーマンスのトラブルシューティングの要件に基づいて、クエリ ストアを構成します。 始めは既定のパラメーターで十分ですが、時間の経過と共にクエリ ストアがどのように動作するかを監視し、それに応じて構成を調整する必要があります。  
  
 ![クエリ ストアのプロパティ](../../relational-databases/performance/media/query-store-properties.png "クエリ-ストア-プロパティ")  
  
 次に、パラメーター値を設定する際のガイドラインを示します。
  
 **最大サイズ (MB)** :クエリ ストアで使用されるデータベース内のデータ領域の制限を指定します。 これは、クエリ ストアの操作モードに直接影響する最も重要な設定です。  
  
 クエリ ストアでクエリ、実行プラン、および統計情報が収集されている間は、この制限に達するまでデータベース内のサイズが増え続けます。 サイズが制限に達すると、クエリ ストアの操作モードが自動的に読み取り専用に切り替わり、新しいデータの収集が停止します。以降、パフォーマンス分析は正確ではなくなります。  
  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] の既定値は 100 MB です。 ワークロードで多数の異なるクエリとプランが生成される場合や、クエリ履歴を長期間保持する必要がある場合、このサイズでは十分でない可能性があります。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降では、既定値は 1 GB です。 クエリ ストアが読み取り専用モードに移行しないように、現在の使用領域を追跡して **[最大サイズ (MB)]** の値を増やしてください。 
 
> [!IMPORTANT] 
> **[最大サイズ (MB)]** の制限は、厳密には適用されません。 ストレージ サイズは、クエリ ストアでディスクにデータが書き込まれる場合にのみ確認されます。 この間隔は、 **[データのフラッシュ間隔 (分)]** オプションによって設定されます。 クエリ ストアでストレージ サイズの確認の合間に最大サイズの制限を超えた場合は、読み取り専用モードに移行します。 **[サイズ ベースのクリーン アップモード]** が有効になっている場合は、最大サイズの制限を適用するクリーンアップ メカニズムもトリガーされます。
 
 クエリ ストアのサイズに関する最新の情報を取得するには、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用するか、次のスクリプトを実行します。  
  
```sql 
USE [QueryStoreDB];  
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason  
FROM sys.database_query_store_options;  
```  
  
 次のスクリプトでは、 **[最大サイズ (MB)]** の新しい値を設定します。  
  
```sql  
ALTER DATABASE [QueryStoreDB]  
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);  
```  

 **データのフラッシュ間隔 (分)** :収集された実行時統計情報をディスクに保存する間隔を定義します。 グラフィカル ユーザー インターフェイス (GUI) では分単位で表されますが、[!INCLUDE[tsql](../../includes/tsql-md.md)] では秒単位で表されます。 既定値は 900 秒です。これは、グラフィカル ユーザー インターフェイスでは 15 分です。 ワークロードで生成される異なるクエリとプランの数が多くない場合、またはデータベースをシャットダウンする前にデータを長時間保持できる場合は、大きい値を使用することを検討してください。
 
> [!NOTE]
> トレース フラグ 7745 を使用すると、フェールオーバーまたはシャットダウン コマンドが発生した場合に、クエリ ストアのデータはディスクに書き込まれません。 詳しくは、「[ミッション クリティカルなサーバーにトレース フラグを使用して、障害からの回復を向上させる](#Recovery)」セクションをご覧ください。

**[データ フラッシュ間隔]** に別の値を設定するには、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用します。  
  
```sql  
ALTER DATABASE [QueryStoreDB] 
SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS = 900);  
```  

 **統計情報の収集間隔**:収集された実行時統計情報に対する粒度のレベルを定義します (分単位)。 既定値は 60 分です。 より細かい粒度が必要な場合、または問題を検出して軽減するための時間を短くする場合は、小さい値を使用することを検討してください。 値はクエリ ストア データのサイズに直接影響することに注意してください。 **[統計情報の収集間隔]** に別の値を設定するには、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用します。  
  
```sql  
ALTER DATABASE [QueryStoreDB] 
SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 60);  
```  
  
 **古いクエリのしきい値 (日)** :保存する実行時統計と非アクティブ クエリの保有期間を制御する、時間ベースのクリーンアップ ポリシーです (日単位)。 既定では、クエリ ストアはデータを 30 日間保持するよう構成されていますが、シナリオによっては必要以上に長い場合があります。  
  
 使用予定のない履歴データは保持しないようにしてください。 これにより、読み取り専用状態への移行を減らすことができます。 クエリ ストアのデータのサイズと、問題を検出して軽減するまでの時間を予測しやすくなります。 時間ベースのクリーンアップ ポリシーを構成するには、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] または次のスクリプトを使用します。  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 90));  
```  
  
 **サイズ ベースのクリーンアップ モード**:クエリ ストアのデータ サイズが制限に達したときに、データの自動クリーンアップを行うかどうかを指定します。 クエリ ストアが常に読み取り/書き込みモードで実行され、最新データが収集されるようにするには、サイズ ベースのクリーンアップを有効にします。  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);  
```  
  
 **クエリ ストアのキャプチャ モード**:クエリ ストアのクエリ キャプチャ ポリシーを指定します。  
  
-   **[すべて]** : すべてのクエリをキャプチャします。 これは [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] の既定のオプションです。
-   **Auto**:頻度の低いクエリと、コンパイルと実行時間の短いクエリは無視されます。 実行回数、コンパイル、実行時間のしきい値は内部的に決定されます。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降では、これは既定のオプションです。
-   **[なし]** :クエリ ストアで新しいクエリのキャプチャが停止されます。  
-   **Custom**:追加の制御と機能を使用して、データ収集ポリシーを微調整できます。 新しいカスタム設定では、内部キャプチャ ポリシーの時間のしきい値内で何が行われるかが定義されます。 これは、構成可能な条件が評価される時刻の境界であり、いずれかが true の場合、クエリがクエリ ストアによるキャプチャの対象となります。
  
 次のスクリプトでは、QUERY_CAPTURE_MODE を AUTO に設定します。
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);  
```  

### <a name="examples"></a>使用例
次の例では、QUERY_CAPTURE_MODE を AUTO に設定し、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] のその他の推奨オプションを設定します。
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      QUERY_CAPTURE_MODE = AUTO,
      MAX_STORAGE_SIZE_MB = 1000,
      INTERVAL_LENGTH_MINUTES = 60
    );
```  

次の例では、QUERY_CAPTURE_MODE を AUTO に設定し、待機統計を含めるように [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] のその他の推奨オプションを設定します。

```sql
ALTER DATABASE [QueryStoreDB] 
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE, 
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      QUERY_CAPTURE_MODE = AUTO,
      MAX_STORAGE_SIZE_MB = 1000, 
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO, 
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
    );
```

次の例では、QUERY_CAPTURE_MODE を AUTO に設定し、[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] のその他の推奨オプションを設定します。また、*必要に応じて*、新しい既定の AUTO キャプチャ モードではなく、既定の設定で CUSTOM キャプチャ ポリシーを設定します。  

```sql
ALTER DATABASE [QueryStoreDB]  
SET QUERY_STORE = ON 
    (
      OPERATION_MODE = READ_WRITE, 
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      MAX_STORAGE_SIZE_MB = 1000, 
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO, 
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
      QUERY_CAPTURE_MODE = CUSTOM,
      QUERY_CAPTURE_POLICY = (
        STALE_CAPTURE_POLICY_THRESHOLD = 24 HOURS,
        EXECUTION_COUNT = 30,
        TOTAL_COMPILE_CPU_TIME_MS = 1000,
        TOTAL_EXECUTION_CPU_TIME_MS = 100 
      )
    );
```

## <a name="start-with-query-performance-troubleshooting"></a>クエリ パフォーマンスのトラブルシューティングを開始する  
 次の図に示すように、クエリ ストアでのトラブルシューティングのワークフローはシンプルです。  
  
 ![クエリ ストアのトラブルシューティング](../../relational-databases/performance/media/query-store-troubleshooting.png "クエリ-ストア-トラブルシューティング")  
  
 前のセクションで説明したように、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用してクエリ ストアを有効にするか、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行します。  
  
```sql  
ALTER DATABASE [DatabaseOne] SET QUERY_STORE = ON;  
```  

クエリ ストアで、ワークロードを正確に表すデータ セットが収集されるまで、しばらく時間がかかります。 通常は、非常に複雑なワークロードの場合でも 1 日で十分です。 ただし、機能を有効にした後すぐにデータの探索を開始して、注意が必要なクエリを特定することができます。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] のオブジェクト エクスプローラーでデータベース ノードの下にある Query Store サブフォルダーに移動し、特定のシナリオのトラブルシューティング ビューを開きます。

[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] のクエリ ストア ビューの操作には、一連の実行メトリックを使用します。メトリックはそれぞれ、次のいずれかの統計関数で表されます。  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョン|実行メトリック|統計関数|  
|----------------------|----------------------|------------------------|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|CPU 時間、実行時間、実行回数、論理読み取り、論理書き込み、メモリ消費量、物理読み取り、CLR 時間、並列処理の次数 (DOP)、行数|Average、Maximum、Minimum、Standard Deviation、Total| 
|[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|CPU 時間、実行時間、実行回数、論理読み取り、論理書き込み、メモリ消費量、物理読み取り、CLR 時間、並列処理の次数、行数、ログ メモリ、TempDB メモリ、待機時間|Average、Maximum、Minimum、Standard Deviation、Total| 
  
 次の図は、クエリ ストアのビューの場所を示しています。  
  
   ![クエリ ストア ビュー](../../relational-databases/performance/media/objectexplorerquerystore_sql17.png "クエリ ストア ビュー")  
  
 次の表では、各クエリ ストア ビューの用途を説明します。  
  
|SQL Server Management Studio ビュー|シナリオ|  
|---------------|--------------|  
|**機能低下したクエリ**|実行メトリックが最近低下した (たとえば、悪化した) クエリを特定します。 <br />このビューを使用して、アプリケーションで確認されたパフォーマンスの問題と、修正や改善の必要がある実際のクエリを関連付けます。|  
|**全体的なリソース消費量**|実行メトリックのいずれかについて、データベースの全体的なリソース消費量を分析します。<br />このビューを使用して、リソースのパターン (日中または夜間のワークロード) を特定し、データベースの全体的な消費量を最適化します。|  
|**最もリソースを消費するクエリ**|対象となる実行メトリックを選択し、指定された期間で最も極端な値を持つクエリを特定します。 <br />このビューを使用して、データベースのリソース消費量に最も大きな影響を与えている最も関連性の高いクエリに焦点を絞ります。|  
|**強制適用されたプランのあるクエリ**|クエリ ストアを使って以前に強制適用されたプランを一覧表示します。 <br />このビューを使って、現在強制適用されているすべてのプランに簡単にアクセスします。|  
|**高バリエーションのクエリ**|目的の期間の、実行時間、CPU 時間、IO、メモリ使用量など、使用可能なディメンションのいずれかに関連して実行バリエーションが高いクエリを分析します。<br />このビューを使用して、アプリケーション全体のユーザー エクスペリエンスに影響する可能性のある、パフォーマンスの差異が大きいクエリを特定します。|  
|**クエリ待機統計**|データベースで最もアクティブな待機カテゴリ、および選択された待機カテゴリに対して最も影響を与えるクエリを分析します。<br />このビューを使用して、待機統計を分析し、アプリケーション全体のユーザー エクスペリエンスに影響する可能性のあるクエリを特定します。<br /><br />適用対象:[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v18.0 以降および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]。|  
|**追跡対象のクエリ**|最も重要なクエリの実行をリアルタイムで追跡します。 このビューは通常、強制適用されたプランを持つクエリがあり、クエリのパフォーマンスを安定させる必要がある場合に使用します。|
  
> [!TIP]
> [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用して最もリソースを消費するクエリを特定し、プラン変更により機能低下したクエリを修正する方法の詳細については、[Azure ブログのクエリ ストアに関する記事](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)を参照してください。\@Azure
  
 パフォーマンスが最適ではないクエリを特定する際のアクションは、問題の性質によって異なります。  
  
-   クエリの実行プランが複数あり、最後のプランのパフォーマンスが前のプランよりも大幅に悪いような場合は、プランの強制適用メカニズムを使用することができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がオプティマイザーのプランを強制しようとします。 プランの適用に失敗した場合、XEvent が発生し、オプティマイザーは通常の方法で最適化するように指示します。
  
       ![クエリ ストアの適用プラン](../../relational-databases/performance/media/query-store-force-plan.png "クエリ-ストア-適用-プラン")  

       > [!NOTE]
       > 前の図では特定のクエリ プランに異なる図形が使われている場合があり、考えられる各状態の意味を次に示します。<br />  
       > 
       > |図形|意味|  
       > |-------------------|-------------|
       > |Circle|クエリ完了。これは、通常の実行が正常に終了したことを意味します。|
       > |Square|キャンセル。これは、クライアントが開始した実行中止を意味します。|
       > |Triangle|失敗。これは、例外で実行が中止されたことを意味します。|
       > 
       > また、図形のサイズには、指定された期間内でのクエリ実行回数が反映されます。 実行回数が多いと、サイズが大きくなります。  

-   クエリに最適な実行のためのインデックスが欠落している場合があります。 この情報は、クエリの実行プラン内で確認できます。 欠落しているインデックスを作成し、クエリ ストアを使用してクエリのパフォーマンスを確認します。  
  
       ![クエリ ストアの表示プラン](../../relational-databases/performance/media/query-store-show-plan.png "クエリ-ストア-表示-プラン")
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]でワークロードを実行している場合、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Index Advisor にサインアップすると、推奨されるインデックスを自動的に取得できます。
  
-   実行プランの推定行数と実際の行数に大きな差がある場合は、統計情報を強制的に再コンパイルすることもできます。
-   たとえば、クエリのパラメーター化を利用したり、より最適なロジックを実装したりする場合は、問題のあるクエリを書き直します。
  
##  <a name="Verify"></a> クエリ ストアでクエリ データが収集されていることを継続的に確認する  
 クエリ ストアでは、操作モードが通知なしに変更されることがあります。 クエリ ストアの状態を定期的に監視して、クエリ ストアが動作していることを確認し、回避できたはずのエラーが発生しないようにしてください。 操作モードを確認して最も重要なパラメーターを表示するには、次のクエリを実行します。 
  
```sql
USE [QueryStoreDB];  
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
 `actual_state_desc` と `desired_state_desc` の違いは、操作モードが自動的に変更されたことを示します。 最も一般的な変更は、クエリ ストアが通知なしに読み取り専用モードに切り替わることです。 非常にまれな状況では、クエリ ストアが内部エラーにより、エラー状態になることがあります。  
  
 実際の状態が読み取り専用になっている場合は、 **readonly_reason** 列で根本原因を調べます。 通常は、サイズ クォータを超えたために、クエリ ストアが読み取り専用モードに移行したことがわかります。 その場合、**readonly_reason** は 65536 に設定されています。 他の理由については、「[sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)」を参照してください。  
  
 クエリ ストアを読み取り/書き込みモードに戻してデータの収集を再開するには、次の手順を実行します。  
  
-   **ALTER DATABASE** の **MAX_STORAGE_SIZE_MB**オプションを使用して、ストレージの最大サイズを増やします。
-   次のステートメントを使用して、クエリ ストアのデータをクリーンアップする。
  
    ```sql  
    ALTER DATABASE [QueryStoreDB] SET QUERY_STORE CLEAR;  
    ```  
  
操作モードを明示的に読み取り/書き込みモードに戻す次のステートメントを実行することで、これらの手順のいずれかまたは両方を適用できます。
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);  
```  
  
 操作モードが変更されないよう事前に対処するには、次の手順を実行します。
  
-   推奨事項を取り入れることで、操作モードが通知なしに変更されることを防ぐことができます。 クエリ ストアのサイズが許可される最大値を常に下回り、読み取り専用モードに移行される可能性が大幅に低くなるようにしてください。 [クエリ ストアの構成](#Configure)に関するセクションの説明に従って、サイズ ベースのポリシーを有効にし、クエリ ストアでサイズが制限に近づくと自動的にデータがクリーンアップされるようにします。
-   最新のデータを確実に保持するには、古くなった情報を定期的に削除するように時間ベースのポリシーを構成します。
-   最後に、**クエリ ストア キャプチャ モード**を **Auto** に設定することを検討してください。そうすることで、通常はワークロードにとってあまり関連性のないクエリが除外されるためです。
  
### <a name="error-state"></a>エラー状態
 クエリ ストアを復旧させるには、明示的に読み取り/書き込みモードに設定してみて、実際の状態を再度確認します。
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);    
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
 それでも問題が解決しない場合は、ディスクに破損したクエリ ストア データが保存されていることを示しています。
 
 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 以降では、影響を受けたデータベース内で **sp_query_store_consistency_check** ストアド プロシージャを実行することで、クエリ ストアを復旧させることができます。 復旧操作を試みる前にクエリ ストアを無効にする必要があります。 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] の場合は、示されているようにクエリ ストアからデータをクリアする必要があります。
 
 復旧に失敗した場合は、読み取り/書き込みモードを設定する前にクエリ ストアをクリアしてみてください。  
  
```sql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE CLEAR;  
GO  
  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);    
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
## <a name="set-the-optimal-query-store-capture-mode"></a>最適なクエリ ストア キャプチャ モードを設定する 
 最も重要なデータをクエリ ストアに保存します。 次の表では、各クエリ ストア キャプチャ モードの一般的なシナリオについて説明します。  
  
|Query Store Capture Mode (クエリ ストアのキャプチャ モード)|シナリオ|  
|------------------------|--------------|  
|**すべて**|すべてのクエリの図形とその実行頻度やその他の統計情報の観点から、ワークロードを詳しく分析します。<br /><br /> ワークロードの新しいクエリを特定します。<br /><br /> ユーザーまたは自動パラメーター化の機会を識別するためにアドホック クエリが使用されているかどうかを検出します。<br /><br />注:これは、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] と [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] の既定のキャプチャ モードです。|
|**Auto**|関連するクエリと実用的なクエリに焦点を絞ります。 たとえば、定期的に実行されるクエリや、大量のリソースを消費するクエリなどがあります。<br /><br />注:[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降では、これが既定のキャプチャ モードです。|  
|**なし**|実行時に監視する必要があるクエリ セットを既にキャプチャしており、他のクエリによって生じる可能性のある、集中を妨げるものを取り除きたいと考えています。<br /><br /> None は、テストおよびベンチマーク環境に適しています。<br /><br /> このモードは、アプリケーションのワークロードを監視するよう構成したクエリ ストアの構成を販売するソフトウェア ベンダーにも適しています。<br /><br /> 重要な新しいクエリを追跡して最適化する機会を見逃す可能性があるため、None を使用する際は注意してください。 シナリオで必要な特別な場合を除き、このモードは使用しないでください。|  
|**Custom**|[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] では、`ALTER DATABASE SET QUERY_STORE` コマンドの下に Custom キャプチャ モードが導入されています。 有効にすると、新しいクエリ ストア キャプチャ ポリシーの設定で追加のクエリ ストア構成を使用して、特定のサーバーでのデータ収集を微調整することができます。<br /><br />新しいカスタム設定では、内部キャプチャ ポリシーの時間のしきい値内で何が行われるかが定義されます。 これは、構成可能な条件が評価される時刻の境界であり、いずれかが true の場合、クエリがクエリ ストアによるキャプチャの対象となります。 詳細については、「[ALTER DATABASE の SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)」を参照してください。|  

> [!NOTE]
> クエリ ストア キャプチャ モードが **All**、**Auto**、または **Custom** に設定されている場合、カーソル、ストアド プロシージャ内のクエリ、ネイティブ コンパイル済みのクエリは常にキャプチャされます。 ネイティブ コンパイル済みのクエリをキャプチャするには、[sys.sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) を使用して、クエリごとの統計情報の収集を有効にします。 

## <a name="keep-the-most-relevant-data-in-query-store"></a>最も重要なデータをクエリ ストアに保存する  
関連データのみを含むようにクエリ ストアを構成して、継続的に実行されるようにし、通常のワークロードへの影響を最小限に抑えながら、優れたトラブルシューティング エクスペリエンスを提供します。  
次の表に、推奨事項を示します。  
  
|ベスト プラクティス|設定|  
|-------------------|-------------|  
|保存する履歴データに制限を設ける。|自動クリーンアップを有効にするように時間ベースのポリシーを構成します。|  
|関連しないクエリを除外する。|**[クエリ ストア キャプチャ モード]** を **Auto** に設定します。|  
|最大サイズに達したときに、関連性の低いクエリを削除する。|サイズ ベースのクリーンアップ ポリシーを有効にします。|  
  
##  <a name="Parameterize"></a> パラメーター化されていないクエリを使用しない  
パラメーター化されていないクエリを必要でないときに使用することは、ベスト プラクティスではありません。 たとえば、アドホック分析の場合です。 キャッシュされたプランは再利用できません。再利用すると、クエリ オプティマイザーによって一意のクエリ テキストごとにクエリが強制的にコンパイルされます。 詳細については、「[Guidelines for using forced parameterization](../../relational-databases/query-processing-architecture-guide.md#ForcedParamGuide)」 (強制パラメーター化使用のガイドライン) をご覧ください。  

また、さまざまなクエリ テキストが多数ある可能性があり、その結果として、同じような形のさまざまな実行プランが多数存在することになるため、クエリ ストアでサイズ クォータがすぐに制限を超える可能性があります。 その結果、ワークロードのパフォーマンスが最適でなくなり、クエリ ストアが読み取り専用モードに切り替わったり、後続のクエリへの対応を試みるためにデータが常に削除されるようになる可能性があります。  
  
次のオプションを検討してください。  

-   必要に応じて、クエリをパラメーター化します。 たとえば、ストアド プロシージャまたは sp_executesql 内にクエリをラップします。 詳細については、「[パラメーターと実行プランの再利用](../../relational-databases/query-processing-architecture-guide.md#PlanReuse)」をご覧ください。  
-   ワークロードに 1 回限りのアドホック バッチが多数含まれており、そこで異なるクエリ プランが使用されている場合は、[アドホック ワークロードの最適化](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md)オプションを使用します。  
    -   個々の query_hash 値の数と、sys.query_store_query 内のエントリの総数を比較します。 この比率が 1 に近い場合、アドホック ワークロードで異なるクエリが生成されます。  
-   異なるクエリ プランの数が多くない場合は、データベースまたはクエリのサブセットに対して[強制パラメーター化](../../relational-databases/query-processing-architecture-guide.md#ForcedParam)を適用します。  
    -   選択したクエリに対してのみパラメータ化を強制するには、[プラン ガイド](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)を使用します。
    -   ワークロード内の異なるクエリ プランの数が少ない場合は、[パラメーター化データベース オプション](../../relational-databases/databases/database-properties-options-page.md#miscellaneous) コマンドを使用して、強制パラメーター化を構成します。 たとえば、個々の query_hash の数と sys.query_store_query 内のエントリの総数の比率が 1 よりもかなり小さい場合です。  
-   リソース消費の少ないアドホック クエリを自動的に除外するには、QUERY_CAPTURE_MODE を AUTO に設定します。  
  
##  <a name="Drop"></a> オブジェクトを格納するために DROP と CREATE のパターンを使用しない
クエリ ストアでは、クエリ エントリと親オブジェクト (ストアド プロシージャ、関数、トリガー) を関連付けます。 親オブジェクトを再作成すると、同じクエリ テキストに対して新しいクエリ エントリが生成されます。 これにより、そのクエリのパフォーマンス統計情報を経時的に追跡し、プランの強制適用メカニズムを使用できなくなります。 この状況を回避するには、可能な限り、`ALTER <object>` プロセスを使用して親オブジェクトの定義を変更します。  
  
##  <a name="CheckForced"></a> 強制適用されたプランの状態を定期的に確認する
プランの強制適用は、重要なクエリのパフォーマンスを修正してより正確な予測を可能にするための便利なメカニズムです。 プラン ヒントやプラン ガイドと同様に、プランの強制適用は、今後の実行で使用されることを保証するものではありません。 通常、実行プランによって参照されるオブジェクトが変更または削除されるような方法でデータベース スキーマが変更された場合、プランを強制的に適用できません。 その場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はクエリの再コンパイルに戻りますが、強制適用が失敗した実際の理由は [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) に示されます。 次のクエリは、強制適用されたプランに関する情報を返します。  
  
```sql  
USE [QueryStoreDB];  
GO  
  
SELECT p.plan_id, p.query_id, q.object_id as containing_object_id,  
    force_failure_count, last_force_failure_reason_desc  
FROM sys.query_store_plan AS p  
JOIN sys.query_store_query AS q on p.query_id = q.query_id  
WHERE is_forced_plan = 1;  
```  
  
 理由の一覧については、「[sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)」を参照してください。 **query_store_plan_forcing_failed** XEvent を使用して、プラン強制の失敗を追跡してトラブルシューティングすることもできます。  
  
##  <a name="Renaming"></a> プランが強制適用されたクエリの場合はデータベースの名前を変更しない  

実行プランでは、`database.schema.object` のような 3 つの部分で構成される名前を使用して、オブジェクトを参照します。

データベース名を変更すると、プランの強制適用が失敗し、その後のすべてのクエリ実行で再コンパイルが発生します。  

##  <a name="Recovery"></a> ミッション クリティカルなサーバーでトレース フラグを使用する
 
グローバル トレース フラグ 7745 と 7752 を使用すると、クエリ ストアを使ってデータベースの可用性を向上させることができます。 詳しくは、「[トレース フラグ](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)」をご覧ください。
  
-  トレース フラグ 7745 では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がシャットダウンされる前に、クエリ ストアによってディスクにデータを書き込む既定の動作が行われないようにします。 つまり、`DATA_FLUSH_INTERVAL_SECONDS` で定義された時間枠まで、収集されたもののディスクにはまだ保存されていないクエリ ストア データは失われます。 
-  トレース フラグ 7752 では、クエリ ストアの非同期読み込みが有効になります。 これにより、データベースをオンラインにすることができ、クエリ ストアが完全に復旧される前にクエリを実行できます。 既定の動作では、クエリ ストアの同期読み込みが行われます。 既定の動作では、クエリ ストアが復旧される前にクエリを実行することはできませんが、データ コレクションでクエリが失われることもありません。

   > [!NOTE]
   > [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降では、この動作はエンジンによって制御されるようになり、トレース フラグ 7752 に効力はありません。

   > [!IMPORTANT]
   > [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] で適宜、ワークロードを洞察するためにクエリ ストアを使用する場合は、[KB 4340759](https://support.microsoft.com/help/4340759) のパフォーマンス スケーラビリティの修正プログラムをできるだけ早くインストールするように計画してください。

## <a name="see-also"></a>参照  
- [ALTER DATABASE SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)     
- [クエリ ストアのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)     
- [クエリ ストアのストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)     
- [インメモリ OLTP でのクエリ ストアの使用](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)     
- [クエリ ストアを使用したパフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)      
- [クエリ処理アーキテクチャ ガイド](../../relational-databases/query-processing-architecture-guide.md)     
  
