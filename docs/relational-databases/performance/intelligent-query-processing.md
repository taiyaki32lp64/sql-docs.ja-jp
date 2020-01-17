---
title: インテリジェントなクエリの処理
description: SQL Server および Azure SQL Database のクエリ パフォーマンスを向上させるためのインテリジェントなクエリ処理の機能です。
ms.custom: seo-dt-2019
ms.date: 11/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords: ''
author: joesackmsft
ms.author: josack
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 65b88c890dc16adf1a1b626dd0ddc91ad359505b
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74821977"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>SQL データベースでのインテリジェントなクエリ処理

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

インテリジェントなクエリ処理 (QP) 機能ファミリには、最小限の労力で実装できる、既存のワークロードのパフォーマンスを広範に改善する機能が含まれています。 

![インテリジェントなクエリ処理](./media/iqp-feature-family.png)

インテリジェントなクエリ処理の概要については、この 6 分間のビデオをご覧ください。
> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Overview-Intelligent-Query-processing-in-SQL-Server-2019/player?WT.mc_id=dataexposed-c9-niner]


データベースに対して適用可能なデータベース互換性レベルを有効にすることにより、自動的にワークロードをインテリジェントなクエリ処理の対象にすることができます。 これは [!INCLUDE[tsql](../../includes/tsql-md.md)] を使って設定できます。 次に例を示します。  

```sql
ALTER DATABASE [WideWorldImportersDW] SET COMPATIBILITY_LEVEL = 150;
```

以下の表で、すべてのインテリジェントなクエリ処理について詳しく説明します。これには、データベース互換性レベルに関する要件も含まれます。

| **IQP の機能** | **Azure SQL Database でのサポート** | **SQL Server でのサポート** |**説明** |
| --- | --- | --- |--- |
| [適応型結合 (バッチ モード)](#batch-mode-adaptive-joins) | あり (互換性レベル 140 未満)| あり ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 以降、互換性レベル 140 未満)|適応型結合では、実際の入力行に基づき、実行時に結合の種類が動的に選択されます。|
| [個別の概算数](#approximate-query-processing) | はい| あり ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降)|高パフォーマンスと小さいメモリ占有領域の利点がある、ビッグ データシナリオに対して、おおよその COUNT DISTINCT を指定します。 |
| [行ストアでのバッチ モード](#batch-mode-on-rowstore) | あり (互換性レベル 150 未満)| あり ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降、互換性レベル 150 未満)|列ストア インデックスを必要としない、CPU にバインドされたリレーショナル DW ワークロードに対してバッチ モードを指定します。  | 
| [インターリーブ実行](#interleaved-execution-for-mstvfs) | あり (互換性レベル 140 未満)| あり ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 以降、互換性レベル 140 未満)|固定推定値ではなく、最初のコンパイルで発生した複数ステートメントのテーブル値関数の実際のカーディナリティを使用します。|
| [メモリ許可フィードバック (バッチ モード)](#batch-mode-memory-grant-feedback) | あり (互換性レベル 140 未満)| あり ([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 以降、互換性レベル 140 未満)|バッチ モード クエリにディスクへの書き込み操作がある場合は、連続実行のためにさらにメモリを追加します。 クエリで 50% を超える、割り当てられたメモリが浪費される場合は、連続実行のためにメモリ許可側を減らします。|
| [メモリ許可フィードバック (行モード)](#row-mode-memory-grant-feedback) | あり (互換性レベル 150 未満)| あり ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降、互換性レベル 150 未満)|行モード クエリにディスクへの書き込み操作がある場合は、連続実行のためにさらにメモリを追加します。 クエリで 50% を超える、割り当てられたメモリが浪費される場合は、連続実行のためにメモリ許可側を減らします。|
| [スカラー UDF のインライン化](#scalar-udf-inlining) | いいえ | あり ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降、互換性レベル 150 未満)|スカラー UDF は同等のリレーショナル式に変換され、この式は呼び出し側クエリに "インライン化" されます。これにより、多くの場合、パフォーマンスが大幅に向上します。|
| [テーブル変数の遅延コンパイル](#table-variable-deferred-compilation) | あり (互換性レベル 150 未満)| あり ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降、互換性レベル 150 未満)|固定推定値ではなく、最初のコンパイルで発生したテーブル変数の実際のカーディナリティを使用します。|

## <a name="batch-mode-adaptive-joins"></a>バッチ モード適応型結合
バッチ モード適応型結合機能を使うと、最初の入力のスキャンが **終わる** まで、[ハッシュ結合方法または入れ子になったループ結合](../../relational-databases/performance/joins.md)方法のどちらを選ぶかを、単一のキャッシュされたプランを使用して遅延することができます。 アダプティブ結合演算子は、入れ子になったループ プランに切り替えるタイミングを決定するために使われるしきい値を定義します。 したがって、実行中により適切な結合方法に動的に切り替えることができます。

互換性レベルを変更せずにアダプティブ結合を無効にする方法など、詳細については、「[アダプティブ結合について](../../relational-databases/performance/joins.md#adaptive)」を参照してください。

## <a name="batch-mode-memory-grant-feedback"></a>バッチ モード メモリ許可フィードバック
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でのクエリの実行プランには、実行に最低限必要なメモリと、すべての行をメモリに収めるのに最適なメモリ許可サイズが含まれます。 メモリ許可サイズが正しくない場合、パフォーマンスが低下します。 メモリ許可が多すぎると、メモリが無駄になり、コンカレンシーが制限されます。 メモリ許可が少なすぎると、負荷の高いディスクへの書き込みが発生する原因になります。 繰り返されるワークロードを処理することにより、バッチ モード メモリ許可フィードバックはクエリに実際に必要なメモリ量を再計算し、キャッシュされたプランの許可値を更新します。 同じクエリ ステートメントを実行するとき、クエリは、修正されたメモリ許可サイズを使うことで、コンカレンシーに影響を与える過剰なメモリ許可を減らし、負荷の高いディスクへの書き込みが発生する過少なメモリ許可を修正します。
次のグラフでは、バッチ モード アダプティブ メモリ許可フィードバックを使用する 1 つの例を示します。 最初のクエリ実行の場合、ディスクへの書き込みが多いため所要時間は "**88 秒**" でした。   

```sql
DECLARE @EndTime datetime = '2016-09-22 00:00:00.000';
DECLARE @StartTime datetime = '2016-09-15 00:00:00.000';
SELECT TOP 10 hash_unique_bigint_id
FROM dbo.TelemetryDS
WHERE Timestamp BETWEEN @StartTime and @EndTime
GROUP BY hash_unique_bigint_id
ORDER BY MAX(max_elapsed_time_microsec) DESC;
```

![ディスクへの書き込みが多い](./media/2_AQPGraphHighSpills.png)

メモリ許可フィードバックを有効にした 2 番目の実行では、所要時間は "**1 秒**" で (88 秒から短縮)、ディスクへの書き込みはまったくなくなり、許可は高くなっています。 

![ディスクへの書き込みがない](./media/3_AQPGraphNoSpills.png)

### <a name="memory-grant-feedback-sizing"></a>メモリ許可フィードバックのサイズ決定
メモリ許可条件が過剰な場合、許可されるメモリが実際に使われるメモリ サイズの 2 倍より多いと、メモリ許可フィードバックはメモリ許可を再計算して、キャッシュされるプランを更新します。 メモリ許可が 1 MB 未満のプランについては、超過分の再計算は行われません。
メモリ許可条件が過少な場合、バッチ モード演算子でディスクへの書き込みが発生すると、メモリ許可フィードバックはメモリ許可の再計算をトリガーします。 ディスク書き込みイベントがメモリ許可フィードバックに報告され、*spilling_report_to_memory_grant_feedback* xEvent で表示できます。 このイベントは、プランのノード ID と、そのノードの書き込まれたデータ サイズを返します。

### <a name="memory-grant-feedback-and-parameter-sensitive-scenarios"></a>メモリ許可フィードバックとパラメーター依存シナリオ
最適化のためには、クエリ プランによってパラメーター値を変えることが必要な場合もあります。 この種のクエリは "パラメーター依存" と定義されます。 パラメーター依存プランでは、メモリ要件が不安定な場合、メモリ許可フィードバック自体がクエリで無効になります。 クエリが数回繰り返し実行された後でプランは無効になり、このことは *memory_grant_feedback_loop_disabled* xEvent で監視できます。 パラメーター スニッフィングとパラメーターの感度の詳細については、「[Query Processing Architecture Guide](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)」(クエリ処理アーキテクチャ ガイド) を参照してください。

### <a name="memory-grant-feedback-caching"></a>メモリ許可フィードバックのキャッシュ
フィードバックは、1 回の実行に対してキャッシュされるプランに格納できます。 ただし、メモリ許可フィードバックの調整によってメリットがあるのは、そのステートメントを連続して実行する場合です。 この機能は、ステートメントの反復実行に適用されます。 メモリ許可フィードバックが変更するのはキャッシュされたプランのみです。 現在、変更はクエリ ストアではキャプチャされません。
プランがキャッシュから削除された場合、フィードバックは保持されません。 フェールオーバーが発生した場合もフィードバックは失われます。 `OPTION (RECOMPILE)` を使うステートメントでは、新しいプランが作成されますが、プランはキャッシュされません。 キャッシュされないため、メモリ許可フィードバックは生成されず、そのコンパイルおよび実行に対して格納されません。 ただし、`OPTION (RECOMPILE)` を "**使わない**" 同等のステートメント (つまり、クエリ ハッシュが同じ) がキャッシュされて再実行された場合、連続するステートメントでメモリ許可フィードバックのメリットがある場合があります。

### <a name="tracking-memory-grant-feedback-activity"></a>メモリ許可フィードバック アクティビティの追跡
*memory_grant_updated_by_feedback* xEvent を使って、メモリ許可フィードバック イベントを追跡することができます。 このイベントは、現在の実行カウント履歴、メモリ許可フィードバックによってプランが更新された回数、変更前の最適な追加メモリ許可、およびメモリ許可フィードバックによってキャッシュされたプランが変更された後の最適な追加メモリ許可を追跡します。

### <a name="memory-grant-feedback-resource-governor-and-query-hints"></a>メモリ許可フィードバック、リソース ガバナー、クエリ ヒント
実際に許可されるメモリは、リソース ガバナーまたはクエリ ヒントによって決定されるクエリ メモリ制限に従います。

### <a name="disabling-batch-mode-memory-grant-feedback-without-changing-the-compatibility-level"></a>互換性レベルを変更せず、バッチ モード メモリ許可フィードバックを無効にする
メモリ許可フィードバックは、データベースの互換性レベル 140 以上を維持しながら、データベースまたはステートメント範囲で無効にできます。 データベースを発生源とするすべてのクエリ実行に対してバッチ モード メモリ許可フィードバックを無効にするには、該当するデータベースとの関連で次を実行します。

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK = ON;

-- Starting with SQL Server 2019, and in Azure SQL Database
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_MEMORY_GRANT_FEEDBACK = OFF;
```

有効になっているとき、この設定は [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) で有効として表示されます。

データベースを発生源とするすべてのクエリ実行に対してバッチ モード メモリ許可フィードバックを再有効化するには、該当するデータベースとの関連で次を実行します。

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK = OFF;

-- Azure SQL Database, SQL Server 2019 and higher
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_MEMORY_GRANT_FEEDBACK = ON;
```

`DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK` を [USE HINT クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md#use_hint)として指定することで、特定のクエリのバッチ モード メモリ許可フィードバックを無効にすることもできます。 次に例を示します。

```sql
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (USE HINT ('DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK')); 
```

USE HINT クエリ ヒントは、データベース スコープ構成またはトレース フラグ設定に優先します。

## <a name="row-mode-memory-grant-feedback"></a>行モード メモリ許可フィードバック

**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降)、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

行モード メモリ許可フィードバックは、バッチ モードと行モード両方の演算子のメモリ許可サイズを調整することで、バッチ モード メモリ許可フィードバックの機能を拡張します。  

[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] で行モード メモリ許可フィードバックを有効にするには、クエリを実行する際に接続されるデータベースのデータベース互換レベル 150 を有効にします。

行モード メモリ許可フィードバックのアクティビティは、**memory_grant_updated_by_feedback** XEvent を通じて確認できます。 

行モード メモリ許可フィードバック以降では、実際の実行プランのために 2 つの新しいクエリ プラン属性 (***IsMemoryGrantFeedbackAdjusted*** および ***LastRequestedMemory***) が表示されます。これらは *MemoryGrantInfo* クエリ プランの XML 要素に追加されます。 

*LastRequestedMemory* では、前のクエリの実行から許可されたメモリがキロバイト (KB) で表示されます。 *IsMemoryGrantFeedbackAdjusted* 属性を使用すると、実際のクエリ実行プラン内のステートメントに対するメモリ許可フィードバックの状態を確認できます。 この属性に表示される値は次のとおりです。

| IsMemoryGrantFeedbackAdjusted の値 | [説明] |
|---|---|
| No:First Execution | メモリ許可フィードバックは、最初のコンパイルとそれに関連付けられた実行ではメモリを調整しません。  |
| No:Accurate Grant | ディスクへの書き込みが存在せず、許可されたメモリの少なくとも 50% がステートメントによって使用されている場合、メモリ許可フィードバックはトリガーされません。 |
| No:Feedback disabled | メモリ許可フィードバックが継続的にトリガーされ、メモリを増加させる操作と減少させる操作の間で変動している場合、ステートメントのメモリ許可フィードバックは無効にされます。 |
| Yes:Adjusting | メモリ許可フィードバックが適用されています。また、次の実行に向けてさらに調整される可能性があります。 |
| Yes:Stable | メモリ許可フィードバックが適用されています。また、許可されたメモリが安定しています (つまり、前回の実行で許可されたメモリと今回の実行で許可されたメモリが同じです)。 |

### <a name="disabling-row-mode-memory-grant-feedback-without-changing-the-compatibility-level"></a>互換性レベルを変更せず、行モード メモリ許可フィードバックを無効にする
行モード メモリ許可フィードバックは、データベースの互換性レベル 150 以上を維持しながら、データベースまたはステートメント範囲で無効にできます。 データベースを発生源とするすべてのクエリ実行に対して行モード メモリ許可フィードバックを無効にするには、該当するデータベースとの関連で次を実行します。

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ROW_MODE_MEMORY_GRANT_FEEDBACK = OFF;
```

データベースを発生源とするすべてのクエリ実行に対して行モード メモリ許可フィードバックを再び有効にするには、該当するデータベースとの関連で次を実行します。

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ROW_MODE_MEMORY_GRANT_FEEDBACK = ON;
```

`DISABLE_ROW_MODE_MEMORY_GRANT_FEEDBACK` を [USE HINT クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md#use_hint)として指定することで、特定のクエリの行モード メモリ許可フィードバックを無効にすることもできます。 次に例を示します。

```sql
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (USE HINT ('DISABLE_ROW_MODE_MEMORY_GRANT_FEEDBACK')); 
```

USE HINT クエリ ヒントは、データベース スコープ構成またはトレース フラグ設定に優先します。

## <a name="interleaved-execution-for-mstvfs"></a>MSTVF のインターリーブ実行
インターリーブ実行では、関数に基づく実際の行数を使用して、より正確なダウンストリーム クエリ プランを決定します。 複数ステートメントのテーブル値関数 (MSTVF) の詳細については、「[テーブル値関数](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)」を参照してください。

インターリーブ実行は、単一クエリ実行の最適化フェーズと実行フェーズの間の一方向境界を変更し、修正されたカーディナリティ推定に基づいてプランが適応できるようにします。 最適化中に、インターリーブ実行の候補を検出した場合 (現在は**複数ステートメント テーブル値関数 (MSTVF)** )、最適化を一時停止し、該当するサブツリーを実行し、正確なカーディナリティの推定をキャプチャし、ダウンストリームの演算に対する最適化を再開します。   

MSTVF の固定のカーディナリティの推定は、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降のバージョンでは 100、それより前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョンでは 1 となります。 インターリーブ実行は、MSTVF に関するこれらの固定カーディナリティ推定によるワークロードのパフォーマンスの問題に役立ちます。 MSTVF の詳細については、「[ユーザー定義関数の作成 (データベース エンジン)](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)」を参照してください。

次の図では、MSTVF からの固定カーディナリティ推定の影響を示す全体実行プランのサブセットである[ライブ クエリ統計](../../relational-databases/performance/live-query-statistics.md)出力を示します。 実際の行フローと推定行数を比較できます プランの 3 つの注目すべき領域があります (フローは右から左)。
1. MSTVF テーブル スキャンの推定行数は 100 の固定です。 ただし、この例では、この MSTVF テーブル スキャンを通過したのはライブ クエリ統計が示すように 527,597 であるのに対し、実際の推定は *527597 of 100* であり、固定の推定に大きな非対称があります。
1. Nested Loops 操作では、結合の外側によって返されるものと推定されたのは 100 行だけです。 MSTVF によって実際に返される行数が多いと、そっくり異なる結合アルゴリズムにした方がよくなると思われます。
1. Hash Match 操作では、小さい警告シンボルに注意してください。これはここではディスクへの書き込みを示します。

![行フローと推定行数](./media/7_AQPFlowThreeAreas.png)

前のプランと、インターリーブ実行を有効にして生成された実際のプランを比較します。

![インターリーブ プラン](./media/8_AQPInterleavedEnabledPlan.png)

1. MSTVF テーブル スキャンに正確なカーディナリティ推定が反映されるようになったことに注意してください。 また、このテーブル スキャンと他の操作の順序の変更に注意してください。
1. 結合アルゴリズムに関しては、Nested Loop 操作から Hash Match 操作に切り替えました。これは、多くの行が関係する場合に、より適しています。
1. また、MSTVF テーブル スキャンからフローする実際の行数に基づいて多くのメモリを許可しているので、ディスク書き込み警告は表示されなくなっています。

### <a name="interleaved-execution-eligible-statements"></a>インターリーブ実行に適したステートメント
インターリーブ実行内のステートメントを参照する MSTVF は、現在は読み取り専用でなければならず、データ変更操作の一部であってはなりません。 また、MSTVF は、ランタイム定数を使用していない場合は、インターリーブ実行には適しません。

### <a name="interleaved-execution-benefits"></a>インターリーブ実行の利点
一般に、推定行数と実際の行数の非対称が大きいほど、ダウンストリーム プラン操作の数との組み合わせで、パフォーマンスへの影響が大きくなります。
一般に、インターリーブ実行は次の場合にクエリに対して利点があります。
1. 中間結果セット (この例では MSTVF) で推定行数と実際の行数の非対称が大きい。
1. かつ、全体的なクエリが中間結果のサイズの変化による影響を受けやすい。 これは通常、クエリ プランのそのサブツリーの上に複雑なツリーが存在する場合に発生します。
MSTVF のシンプルな `SELECT *` では、インターリーブ実行によるメリットはありません。

### <a name="interleaved-execution-overhead"></a>インターリーブ実行のオーバーヘッド
オーバーヘッドは最小限か、ありません。 MSTVF はインターリーブ実行導入前に既に具体化されていましたが、違いは、今では最適化を延期でき、具体化された行セットのカーディナリティの推定を利用できることです。
変更に影響を与える他のプランと同様に、一部のプランでは、サブツリーのカーディナリティがよくなることで、クエリ全体が悪いプランになることがあります。 軽減策は、互換性レベルを元に戻すか、またはクエリ ストアを使ってプランの非機能低下バージョンを強制します。

### <a name="interleaved-execution-and-consecutive-executions"></a>インターリーブ実行と連続実行
インターリーブ実行プランがキャッシュされると、最初の実行の推定を修正されたプランが、インターリーブ実行を再インスタンス化することなく連続する実行に使われます。

### <a name="tracking-interleaved-execution-activity"></a>インターリーブ実行アクティビティの追跡
実際のクエリ実行プランで使用法属性を確認できます。

| 実行プラン属性 | [説明] |
| --- | --- |
| ContainsInterleavedExecutionCandidates | *QueryPlan* ノードに適用します。 *true* の場合、プランにインターリーブ実行候補が含まれることを意味します。 |
| IsInterleavedExecuted | TVF ノードの RelOp 以下にある *RuntimeInformation* 要素の属性。 *true* の場合、操作がインターリーブ実行操作の一部としてマテリアル化されたことを意味します。 |

次の xEvent を使って、インターリーブ実行の発生を追跡することもできます。

| xEvent | [説明] |
| ---- | --- |
| interleaved_exec_status | このイベントは、インターリーブ実行が発生すると発生します。 |
| interleaved_exec_stats_update | このイベントは、インターリーブ実行によって更新されたカーディナリティの推定を記述します。 |
| Interleaved_exec_disabled_reason | このイベントは、インターリーブ実行の候補を含むクエリが実際にはインターリーブ実行されなかったときに発生します。 |

インターリーブ実行が MSTVF カーディナリティ推定を修正できるようにするには、クエリを実行する必要があります。 ただし、`ContainsInterleavedExecutionCandidates` showplan 属性によるインターリーブ実行候補がある場合は、推定実行プランがまだ表示されます。    

### <a name="interleaved-execution-caching"></a>インターリーブ実行のキャッシュ
プランがキャッシュからクリアまたは消去された場合、クエリ実行時に、インターリーブ実行を使う新しいコンパイルが行われます。
`OPTION (RECOMPILE)` を使うステートメントは、インターリーブ実行を使う新しいプランを作成し、それをキャッシュしません。     

### <a name="interleaved-execution-and-query-store-interoperability"></a>インターリーブ実行とクエリ ストアの相互運用性
インターリーブ実行を使うプランは強制的に実行できます。 プランは、最初の実行に基づいてカーディナリティの推定を修正されたバージョンです。    

### <a name="disabling-interleaved-execution-without-changing-the-compatibility-level"></a>互換性レベルを変更せず、インターリーブ実行を無効にする
インターリーブ実行は、データベースの互換性レベル 140 以上を維持しながら、データベースまたはステートメント範囲で無効にできます。  データベースを発生源とするすべてのクエリ実行に対してインターリーブ実行を無効にするには、該当するデータベースとの関連で次を実行します。

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_INTERLEAVED_EXECUTION_TVF = ON;

-- Starting with SQL Server 2019, and in Azure SQL Database
ALTER DATABASE SCOPED CONFIGURATION SET INTERLEAVED_EXECUTION_TVF = OFF;
```

有効になっているとき、この設定は [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) で有効として表示されます。
データベースを発生源とするすべてのクエリ実行に対してインターリーブ実行を再有効化するには、該当するデータベースとの関連で次を実行します。

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_INTERLEAVED_EXECUTION_TVF = OFF;

-- Starting with SQL Server 2019, and in Azure SQL Database
ALTER DATABASE SCOPED CONFIGURATION SET INTERLEAVED_EXECUTION_TVF = ON;
```

[USE HINT](../../t-sql/queries/hints-transact-sql-query.md#use_hint) クエリ ヒントとして `DISABLE_INTERLEAVED_EXECUTION_TVF` を指定することで、特定のクエリでインターリーブ実行を無効にすることもできます。 次に例を示します。

```sql
SELECT [fo].[Order Key], [fo].[Quantity], [foo].[OutlierEventQuantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Fact].[WhatIfOutlierEventQuantity]('Mild Recession',
                            '1-01-2013',
                            '10-15-2014') AS [foo] ON [fo].[Order Key] = [foo].[Order Key]
                            AND [fo].[City Key] = [foo].[City Key]
                            AND [fo].[Customer Key] = [foo].[Customer Key]
                            AND [fo].[Stock Item Key] = [foo].[Stock Item Key]
                            AND [fo].[Order Date Key] = [foo].[Order Date Key]
                            AND [fo].[Picked Date Key] = [foo].[Picked Date Key]
                            AND [fo].[Salesperson Key] = [foo].[Salesperson Key]
                            AND [fo].[Picker Key] = [foo].[Picker Key]
OPTION (USE HINT('DISABLE_INTERLEAVED_EXECUTION_TVF'));
```

USE HINT クエリ ヒントは、データベース スコープ構成またはトレース フラグ設定に優先します。

## <a name="table-variable-deferred-compilation"></a>テーブル変数の遅延コンパイル

**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降)、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

**テーブル変数の遅延コンパイル**を使用すると、テーブル変数を参照するクエリのプランの品質および全体的なパフォーマンスが向上します。 最適化と最初のプランのコンパイルの実行中に、この機能は実際テーブル変数の行数に基づくカーディナリティの推定を反映します。 この正確な行数の情報は、ダウンストリーム プラン操作を最適化するために使用されます。

テーブル変数の遅延コンパイルを使用すると、テーブル変数を参照するステートメントのコンパイルは、そのステートメントが最初に実際に実行されるまで遅延されます。 この遅延コンパイルの動作は、一時テーブルの動作と同じです。 この変更によって、元の 1 行の推定値ではなく、実際のカーディナリティを使用できるようになります。 

テーブル変数の遅延コンパイルを有効にするには、クエリを実行する際に接続されるデータベースに対してデータベース互換レベル 150 を有効にします。

テーブル変数の遅延コンパイルを使用することで、テーブル変数のその他の特性が変更されることは**ありません**。 たとえば、この機能はテーブル変数に列統計を追加しません。

テーブル変数の遅延コンパイルによって**再コンパイルの頻度が増加することはありません**。 最初のコンパイルを行った場所でシフトします。 結果として得られるキャッシュされたプランは、最初の遅延コンパイルのテーブル変数の行数に基づいて生成されます。 キャッシュされたプランは、連続するクエリによって再利用されます。 プランが削除されるか、再コンパイルされるまで再利用されます。 

最初のプランのコンパイルに使用される table 変数の行数で示される標準値は、固定行数の推定値とは異なる場合があります。 異なる場合、ダウンストリーム操作が役立ちます。 テーブル変数の行数が実行全体で大幅に変化する場合は、この機能を使用してもパフォーマンスが改善しない可能性があります。

### <a name="disabling-table-variable-deferred-compilation-without-changing-the-compatibility-level"></a>互換性レベルを変更することなく、テーブル変数の遅延コンパイルを無効にする
table 変数の遅延コンパイルは、データベースの互換性レベル 150 以上を維持しながら、データベースまたはステートメント範囲で無効にします。 データベースを発生源とするすべてのクエリ実行に対してテーブル変数の遅延コンパイルを無効にするには、該当するデータベースとの関連で次のサンプルを実行します。

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DEFERRED_COMPILATION_TV = OFF;
```

データベースを発生源とするすべてのクエリ実行に対してテーブル変数の遅延コンパイルを再度有効にするには、該当するデータベースとの関連で次のサンプルを実行します。

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DEFERRED_COMPILATION_TV = ON;
```

DISABLE_DEFERRED_COMPILATION_TV を USE HINT クエリ ヒントとして割り当てることで、特定のクエリに対してテーブル変数の遅延コンパイル無効にすることもできます。  次に例を示します。

```sql
DECLARE @LINEITEMS TABLE 
    (L_OrderKey INT NOT NULL,
     L_Quantity INT NOT NULL
    );

INSERT @LINEITEMS
SELECT L_OrderKey, L_Quantity
FROM dbo.lineitem
WHERE L_Quantity = 5;

SELECT  O_OrderKey,
    O_CustKey,
    O_OrderStatus,
    L_QUANTITY
FROM    
    ORDERS,
    @LINEITEMS
WHERE   O_ORDERKEY  =   L_ORDERKEY
    AND O_OrderStatus = 'O'
OPTION (USE HINT('DISABLE_DEFERRED_COMPILATION_TV'));
```

## <a name="scalar-udf-inlining"></a>スカラー UDF のインライン化

**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降)

スカラー UDF のインライン化によって、[スカラー UDF](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar) は関係式に自動的に変換されます。 これらは呼び出し元の SQL クエリに埋め込まれます。 この変換により、スカラー UDF を利用するワークロードのパフォーマンスが向上します。 スカラー UDF のインライン化によって、UDF 内の操作をコストベースで簡単に最適化できるようになります。 その結果、非効率的で反復的な直列の実行プランではなく、効率的でセット指向の並列処理になります。 この機能は、データベース互換性レベル 150 では既定で有効です。

詳細については、「[スカラー UDF のインライン化](../user-defined-functions/scalar-udf-inlining.md)」を参照してください。

## <a name="approximate-query-processing"></a>概数クエリ処理

**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降)、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

概数クエリ処理は新しい機能ファミリです。 絶対的な精度よりも応答性が重要となる場合に、大規模なデータ セット全体が集計されます。 たとえば、ダッシュボードに表示するために、100 億の行に対する **COUNT(DISTINCT())** を計算する場合などです。 この場合、重要なのは絶対的な精度ではなく、応答性です。 新しい集計関数 **APPROX_COUNT_DISTINCT** は、グループ内の一意の非 null 値の概数を返します。

詳細については、「[APPROX_COUNT_DISTINCT (Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md)」をご覧ください。

## <a name="batch-mode-on-rowstore"></a>行ストアでのバッチ モード 

**適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降)、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

行ストアのバッチ モードでは、列ストア インデックスを要求せず、分析ワークロードをバッチ モードで実行できます。  この機能は、ディスク上のヒープと B ツリー インデックスに対するバッチ モード実行とビットマップ フィルターをサポートしています。 行ストアのバッチ モードでは、既存のすべてのバッチ モード対応演算子のサポートが有効になります。

### <a name="background"></a>バックグラウンド
[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] では、分析ワークロードを促進する新機能である列ストア インデックスが導入されました。 後続の各リリースでユース ケースを拡張し、列ストア インデックスのパフォーマンスを向上させました。 これまでは、これらすべての機能を 1 つの機能として浮上させ、文書化しました。 テーブルに列ストア インデックスを作成します。 すると、分析ワークロードが高速になります。 ただし、関連しているが異なる 2 つのテクノロジ セットがあります。
- **列ストア** インデックスでは、分析クエリは必要な列のデータにのみアクセスできます。 列ストア形式のページ圧縮は、従来の**行ストア** インデックスの圧縮よりもはるかに効果的でもあります。 
- **バッチ モード**処理では、クエリ演算子によってデータがより効率的に処理されます。 一度に 1 行ずつではなく、複数行がバッチ処理されます。 他のいくつかのスケーラビリティの向上がバッチ モード処理に関連付けられています。 バッチ モードの詳細については、「[実行モード](../../relational-databases/query-processing-architecture-guide.md#execution-modes)」を参照してください。

2 セットの機能が連携して、入力/出力 (I/O) と CPU の使用率が向上します。
- 列ストア インデックスを使用すると、より多くのデータがメモリに格納されます。 これにより、I/O ワークロードが減少します。
- バッチ モード処理では、CPU がより効率的に使用されます。

2 つのテクノロジは可能な限り相互活用されます。 たとえば、バッチ モード集計は、列ストア インデックス スキャンの一部として評価できます。 また、圧縮された列ストア データも、バッチ モード結合とバッチ モード集計により、ラン レングス エンコードを使用してはるかに効率的に処理されます。 
 
しかし、この 2 つの機能は独立していることを理解しておくことが重要です。
* 列ストア インデックスを使用する行モード プランを利用できます。
* 行ストア インデックスのみを使用するバッチ モード プランを利用できます。 

通常、2 つの機能を一緒に使用すると、最適な結果が得られます。 そのため、これまで SQL Server のクエリ オプティマイザーは、列ストア インデックスのあるテーブルが少なくとも 1 つ関係するクエリに対してのみバッチ モード処理を検討しました。

一部のアプリケーションには、列ストア インデックスが適していない可能性があります。 列ストア インデックスではサポートされていない他の機能を使用するアプリケーションもあります。 たとえば、インプレースの変更は列ストアの圧縮と互換性がありません。 そのため、クラスター化列ストア インデックスがあるテーブルでは、トリガーはサポートされません。 さらに重要なことに、列ストア インデックスによって **DELETE** および **UPDATE** ステートメントにオーバーヘッドが増えます。 

一部のトランザクションと分析のハイブリッド ワークロードでは、トランザクションのワークロードでのオーバーヘッドが列ストア インデックスを使用することから得られるメリットを上回ります。 このようなシナリオでは、バッチ モードの処理だけを採用することにより、CPU 使用率を向上させることができます。 このため、行ストアでのバッチ モード機能では、関連するインデックスの種類に関係なく、すべてのクエリにバッチ モードが検討されます。

### <a name="workloads-that-might-benefit-from-batch-mode-on-rowstore"></a>行ストアでバッチ モードの恩恵を受ける可能性があるワークロード
次のワークロードは、行ストアでのバッチ モードの恩恵を受ける可能性があります。
* ワークロードの大部分が分析クエリで構成されています。 通常、このようなクエリでは、数十万行以上を処理する結合や集計などの演算子を使用します。
* ワークロードが CPU バウンドです。 ボトルネックが I/O の場合は、可能であれば列ストア インデックスを検討することを引き続きお勧めします。
* 列ストア インデックスを作成すると、ワークロードのトランザクション部分に過剰なオーバーヘッドがかかります。 または、列ストア インデックスの作成が実行不可能です。アプリケーションは列ストア インデックスでまだサポートされていない機能に依存しているためです。


> [!NOTE]
> 行ストアでのバッチ モードは、CPU 使用量を減らすことでのみ支援できます。 ボトルネックが I/O に関連し、データがまだキャッシュされていない場合 ("コールド" キャッシュ)、行ストアでのバッチ モードではクエリ経過時間が向上しません。 同様に、すべてのデータをキャッシュするための十分なメモリがマシンにない場合、パフォーマンスは向上しない可能性があります。

### <a name="what-changes-with-batch-mode-on-rowstore"></a>行ストアでのバッチ モードによる変化

データベースの互換性レベルを 150 に設定します。 他の変更は必要ありません。

クエリで列ストア インデックスのあるテーブルにアクセスしない場合でも、ヒューリスティックを使用するクエリ プロセッサでは、バッチ モードを検討するかどうかが決定されます。 ヒューリスティックは以下のチェックから構成されます。
1. テーブル サイズ、使用される演算子、入力クエリの推定カーディナリティの初期チェック。
2. オプティマイザーによってクエリに対する新しい低コストのプランが検出されたときの追加のチェックポイント。 これらの代替プランがバッチ モードを大いに利用しない場合、オプティマイザーではバッチ モードの代替手段の探索が停止されます。


行ストアでバッチ モードが使用されている場合、実際の実行モードはクエリ プランで **[バッチ モード]** と表示されます。 scan 演算子では、ディスク上のヒープと B ツリー インデックスにバッチ モードを使用します。 このバッチ モード スキャンでは、バッチ モードのビットマップ フィルターを評価できます。 また、プラン内の他のバッチ モード演算子も表示されることがあります。 たとえば、ハッシュ結合、ハッシュ ベースの集計、並べ替え、ウィンドウ集計、フィルター、連結、Compute Scalar 演算子などです。

### <a name="remarks"></a>解説

クエリ プランは常にバッチ モードを使用するわけではありません。 クエリ オプティマイザーでは、クエリがバッチ モードの恩恵を受けないと判断される場合があります。 

クエリ オプティマイザーの検索スペースは変化しています。 そのため、行モード プランを取得する場合、それがより低い互換性レベルで取得するプランと同じではない可能性があります。 また、バッチ モード プランを取得する場合、それが列ストア インデックスを使用して取得したプランと同じではない可能性があります。 

新しいバッチ モード行ストア スキャンが原因で、プランは、列ストア インデックスと行ストア インデックスが混在するクエリに対して変化する可能性もあります。

現在、行ストア スキャンには、新しいバッチ モードに対して制限事項があります。 
- インメモリ OLTP テーブル、またはディスク上のヒープと B ツリー以外のインデックスに対しては開始されません。 
- 大規模なオブジェクト (LOB) 列がフェッチまたはフィルター処理された場合にも開始されません。 この制限には、スパース列セットと XML 列が含まれます。

列ストア インデックスでもバッチ モードが使用されないクエリがあります。 たとえば、カーソルを含むクエリです。 これと同様の例外は、行ストアのバッチ モードにも適用されます。

### <a name="configure-batch-mode-on-rowstore"></a>行ストアにバッチ モードを構成する
**BATCH_MODE_ON_ROWSTORE** データベース スコープ構成は、既定で有効です。 データベースの互換性レベルを変更せずに、行ストアのバッチ モードを無効にすることができます。

```sql
-- Disabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = OFF;

-- Enabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = ON;
```

データベース スコープ構成を使用して行ストアのバッチ モードを無効にすることができます。 ただし、その場合でも **ALLOW_BATCH_MODE** クエリ ヒントを使用してクエリ レベルで設定をオーバーライドできます。 次の例では、データベース スコープ構成を使用して無効になっている行ストアでのバッチ モードを有効にします。

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('ALLOW_BATCH_MODE'));
```

**DISALLOW_BATCH_MODE** クエリ ヒントを使用して、特定のクエリに対して行ストアでのバッチ モードを無効にすることもできます。 次の例を参照してください。

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('DISALLOW_BATCH_MODE'));
```

## <a name="see-also"></a>参照
[SQL Server データベース エンジンと Azure SQL Database のパフォーマンス センター](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[クエリ処理アーキテクチャ ガイド](../../relational-databases/query-processing-architecture-guide.md)    
[プラン表示の論理操作と物理操作のリファレンス](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[結合](../../relational-databases/performance/joins.md)    
[アダプティブ クエリ処理のデモンストレーション](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/intelligent-query-processing)       
[インテリジェントなクエリ処理のデモ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/intelligent-query-processing)   
