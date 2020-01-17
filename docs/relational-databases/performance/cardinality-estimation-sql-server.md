---
title: カーディナリティ推定 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- cardinality estimator
- CE (cardinality estimator)
- estimating cardinality
ms.assetid: baa8a304-5713-4cfe-a699-345e819ce6df
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0f9e7ef2d1503088cba081b931e09f1fb3536b56
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946994"
---
# <a name="cardinality-estimation-sql-server"></a>カーディナリティ推定 (SQL Server)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ オプティマイザーは、コストベースのオプティマイザーです。 つまり、実行のための推定処理コストが最も低いクエリ プランが選択されます。 クエリ オプティマイザーでは、主に次の 2 つの要素に基づいてクエリ プランを実行する際のコストが決定されます。

- クエリ プランの各レベルで処理される行の総数。これをプランのカーディナリティと呼びます。
- クエリ内の演算子で指示されているアルゴリズムのコスト モデル。

最初の要素であるカーディナリティは、2 番目の要素であるコスト モデルの入力パラメーターとして使用します。 そのため、カーディナリティが向上すると、推定コストが適切になり、その結果実行プランも高速化します。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でのカーディナリティ推定は、インデックスまたは統計を作成するときに手動か自動で作成されたヒストグラムから主に取得されます。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、クエリの制約情報および論理再書き込みを使用して、カーディナリティが決定されることもあります。

次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用してカーディナリティを正確に計算することができません。 その場合コストが正しく計算されないので、最適なクエリ プランが選択されない場合があります。 次に示す構造をクエリで使用しないようにすることで、クエリのパフォーマンスが向上する場合があります。 別のクエリ式や他の方法で代替できることがあるので、それについても記載してあります。

- 同一テーブルの異なる列どうしを比較する比較演算子を述語で使用しているクエリ。
- 次のいずれかの条件に該当し、演算子を述語で使用しているクエリ。
  - 演算子の一方の側で使用されている列の統計が存在しない。
  - 統計内の値の分布が不均一であるにもかかわらず、クエリにより選択度の高い値セットがシークされる。 これに該当するのは、主に演算子が等号 (=) 以外である場合です。
  - 等しくない (!=) 比較演算子または `NOT` 論理演算子を述語で使用している。
- SQL Server の組み込み関数、または引数が定数値でないスカラー値関数かユーザー定義関数を使用するクエリ。
- 算術連結演算子または文字列連結演算子によって結合した列を含んでいるクエリ。
- クエリのコンパイル時または最適化時に値が確定しない変数を比較するクエリ。

この記事では、ご利用のシステムに最適な CE 構成を評価して選択する方法を示しています。 最も正確なので、ほとんどのシステムで最新の CE のメリットを享受できます。 CE はクエリが返す可能性のある行の数を予測します。 クエリ オプティマイザーではカーディナリティ予測を使用して、最適なクエリ プランを生成します。 推定が正確であるほど、通常はクエリ オプティマイザーでより最適なクエリ プランを生成できます。  
  
アプリケーション システムには、新しい CE が原因で低速のプランに変更された重要なクエリが含まれている可能性があります。 そのようなクエリは、次のいずれかのようになります。  
  
- OLTP (オンライン トランザクション処理) クエリ。頻繁に実行され、その複数のインスタンスがしばしば同時に実行されます。  
- SELECT。OLTP 営業時間中に実行される大量の集計と一緒に実行されます。  
  
新規の CE で低速で実行するクエリを識別するための手法があります。 そして、パフォーマンスの問題に対処する方法のオプションもあります。
  
## <a name="versions-of-the-ce"></a>CE のバージョン

1998 年には、CE の主要な更新プログラムは、互換性レベルが 70 の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 の一部でした。 このバージョンの CE モデルは、次の 4 つの基本的な前提条件で設定されています。

-  **非依存性:** 異なる列のデータ分布は、相関関係情報があって使用可能な場合を除き、相互に独立しているものと想定されます。
-  **統一性:** 個別の値は等間隔であり、すべて同じ頻度です。 具体的には、各[ヒストグラム](../../relational-databases/statistics/statistics.md#histogram) ステップ内では、個別の値は均等に分散し、各値は同じ頻度です。 
-  **コンテインメント (単純):** ユーザーは存在するデータをクエリします。 たとえば、2 つのテーブル間の等価結合では、結合の選択度を推定するためにヒストグラムを結合する前に、各入力のヒストグラムの述語選択度<sup>1</sup>を考慮します。 
-  **包含:** `Column = Constant` のフィルター述語では、定数が関連付けられた列に実際に存在すると想定されます。 対応するヒストグラム ステップが空ではない場合、ステップの個別値のいずれかは述語の値と一致するものと想定されます。

  <sup>1</sup> 述語を満たす行数。

以降の更新プログラムは [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以上 (互換性レベルが 120 以上) に含まれています。 レベル 120 以上の CE 更新プログラムには、最新のデータ ウェアハウスおよび OLTP ワークロードで適切に機能する更新された前提条件とアルゴリズムが組み込まれています。 CE 120 以降では、CE 70 の前提条件から次のモデル前提条件が変更されました。

-  **非依存性**が**相関関係**になります:異なる列の値の組み合わせは必ずしも独立していません。 これはより実際のデータ クエリと似ている可能性があります。
-  **単純なコンテインメント**は**ベース コンテインメント**になります:ユーザーは存在しないデータをクエリする可能性があります。 たとえば、2 つのテーブル間の等価結合では、ベース テーブル ヒストグラムを使用して結合の選択度を推定した後、述語選択度を考慮します。
  
**互換性レベル:** [COMPATIBILITY_LEVEL](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) に次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コードを使用して、データベースが特定のレベルであることを確認します。  

```sql  
SELECT ServerProperty('ProductVersion');  
GO  
  
ALTER DATABASE <yourDatabase>  
SET COMPATIBILITY_LEVEL = 130;  
GO  
  
SELECT d.name, d.compatibility_level  
FROM sys.databases AS d  
WHERE d.name = 'yourDatabase';  
GO  
```  
  
互換性レベルが 120 以上に設定されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの場合、[トレース フラグ 9481](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) をアクティブにすると、システムは強制的に CE バージョン 70 を使用します。  
  
**レガシ CE:** 互換性レベルが 120 以上に設定されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの場合、[ALTER DATABASE SCOPED CONFIGURATION](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) を使用して、データベース レベルで CE バージョン 70 をアクティブにすることができます。
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION 
SET LEGACY_CARDINALITY_ESTIMATION = ON;  
GO  
  
SELECT name, value  
FROM sys.database_scoped_configurations  
WHERE name = 'LEGACY_CARDINALITY_ESTIMATION';  
GO
```  
 
[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降の場合は、[クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md#use_hint) `USE HINT ('FORCE_LEGACY_CARDINALITY_ESTIMATION')` を使用します。
 
 ```sql  
SELECT CustomerId, OrderAddedDate  
FROM OrderTable  
WHERE OrderAddedDate >= '2016-05-01'
OPTION (USE HINT ('FORCE_LEGACY_CARDINALITY_ESTIMATION'));  
```
 
**クエリ ストア:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から導入されたクエリ ストアは、クエリのパフォーマンスを確認する場合に便利なツールです。 クエリ ストアを有効にすると、[!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] の**オブジェクト エクスプローラー**で、データベース ノード以下に**クエリ ストア** ノードが表示されます。  
  
```sql  
ALTER DATABASE <yourDatabase>  
SET QUERY_STORE = ON;  
GO  
  
SELECT q.actual_state_desc AS [actual_state_desc_of_QueryStore],  
        q.desired_state_desc,  
        q.query_capture_mode_desc  
FROM sys.database_query_store_options AS q;  
GO  
  
ALTER DATABASE <yourDatabase>  
SET QUERY_STORE CLEAR;  
```  
  
> [!TIP] 
> 最新リリースの [Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) をインストールし、頻繁に更新することをお勧めします。  
  
カーディナリティ推定処理を追跡するための別のオプションは、**query_optimizer_estimate_cardinality** という名前の拡張イベントを使用することです。 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コードを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で実行します。 これは `C:\Temp\` に .xel ファイルを書き込みます (ただし、パスを変更することができます)。 [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] で .xel ファイルを開くと、ユーザーにわかりやすい方法で詳細情報が表示されます。  
  
```sql  
DROP EVENT SESSION Test_the_CE_qoec_1 ON SERVER;  
go  
  
CREATE EVENT SESSION Test_the_CE_qoec_1  
ON SERVER  
ADD EVENT sqlserver.query_optimizer_estimate_cardinality  
    (  
        ACTION (sqlserver.sql_text)  
            WHERE (  
                sql_text LIKE '%yourTable%'  
                and sql_text LIKE '%SUM(%'  
            )  
    )  
ADD TARGET package0.asynchronous_file_target   
        (SET  
            filename = 'c:\temp\xe_qoec_1.xel',  
            metadatafile = 'c:\temp\xe_qoec_1.xem'  
        );  
GO  
  
ALTER EVENT SESSION Test_the_CE_qoec_1  
ON SERVER  
STATE = START;  --STOP;  
GO  
```  
  
[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 向けに拡張されたイベントの詳細については、「[SQL Database の拡張イベント](https://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)」を参照してください。  
  
## <a name="steps-to-assess-the-ce-version"></a>CE のバージョンを評価する手順  
  
次に示す手順を使用して、最も重要なクエリの中に、最新の CE で適切に機能しないものがあるかどうかを評価できます。 一部の手順は、前のセクションで説明されたコード サンプルを実行すると実行されます。  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]を開きます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースが、利用できる最も高い互換性レベルに設定されていることを確認してください。  
  
2.  次の準備作業を実行します。  
  
    1.  [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]を開きます。  
  
    2.  T-SQL を実行して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースが、利用できる最も高い互換性レベルに設定されていることを確認します。  
  
    3.  データベースの `LEGACY_CARDINALITY_ESTIMATION` 構成が OFF になっていることを確認します。  
  
    4.  クエリ ストアをクリアします。 もちろん、クエリ ストアが ON であることを確認します。  
  
    5.  `SET NOCOUNT OFF;` ステートメントを実行します。  
  
3.  `SET STATISTICS XML ON;` ステートメントを実行します。  
  
4.  重要なクエリを実行します。  
  
5.  **[メッセージ]** タブの結果ウィンドウで、影響を受けた行の実際の数を確認してください。  
  
6.  **[結果]** タブの結果ウィンドウで、XML 形式の統計情報を含むセルをダブルクリックします。 グラフィックのクエリ プランが表示されます。  
  
7.  グラフィックのクエリ プランで最初のボックスを右クリックし、 **[プロパティ]** をクリックします。  
  
8.  別の構成と後で比較するために、次のプロパティの値を記録してください:  
  
    -   **CardinalityEstimationModelVersion**。  
  
    -   **推定される行の数**。  
  
    -   **I/O の推定コスト**と、行数の予測ではなく、実際のパフォーマンスを含む *推定* プロパティ。  
  
    -   **論理操作** と **物理操作**。 *並列処理* は有効な値です。  
  
    -   **実際の実行モード**。 *バッチ* は、 *行*より適切で、有効な値です。  
  
9. 行の推定数と行の実際の数とを比較します。 CE は 1% (前後)、または 10% 程度、不正確ですか?  
  
10. `SET STATISTICS XML OFF;` を実行します。  
  
11. T-SQL を実行して、データベースの互換性レベルを 1 レベルずつ下げます (例: 130 から 120 に下げる)。  
  
12. すべての非準備ステップを再実行します。  
  
13. 2 つの実行からの CE プロパティ値を比較します。  
  
    - 最新の CE での不正確さの割合は、以前の CE での不正確さの割合より小さいですか?  
  
14. 最後に、2 つの実行からのさまざまなパフォーマンス プロパティ値を比較します。  
  
    -   クエリは 2 つの異なる CE 見積もりでの異なるプランを使用しましたか?  
  
    -   最新の CE でのクエリ実行速度は低速でしたか?  
  
    -   古い CE で別のプランを使用してクエリの動作が向上するのでない限り、恐らく最新の CE を使用したいと思われるでしょう。  
  
    -   ただし、クエリが古い CE でより高速なプランで実行している場合は、システムで高速なプランを強制的に使用し、CE を無視することを検討してください。 これが、1 つの例外で高速のプランを維持しながらも、すべてに対して最新の CE を保持できる方法です。  
  
## <a name="how-to-activate-the-best-query-plan"></a>最適なクエリ プランをアクティブにする方法  
  
CE 120 以降で効果の低いクエリ プランが、クエリで生成されるとします。 よりよいプランをアクティブにするいくつかのオプションを次に示します。  
  
1. データベース全体に対して、互換性レベルを利用可能な最新の値より低い値に設定できます。  
  
   - たとえば、互換性レベル 110 以下に設定すると CE 70 がアクティブ化しますが、すべてのクエリは以前の CE モデルの対象になります。  
  
   - さらに、低い互換性レベルに設定すると、最新バージョンのクエリ オプティマイザーの多数の機能強化も利用できません。  
  
2. `LEGACY_CARDINALITY_ESTIMATION` データベース オプションを使用すると、クエリ オプティマイザーの他の機能強化を維持したまま、データベース全体が古い CE を使用するようにできます。   

3. `LEGACY_CARDINALITY_ESTIMATION` クエリ ヒントを使用すると、クエリ オプティマイザーの他の機能強化を維持したまま、単一のクエリが古い CE を使用するようにできます。  
  
詳細に制御するために、システムがテスト中に CE 70 で生成されたプランを "*強制的に*" 使用するように指定できます。 優先するプランを *固定* した後、データベース全体が最新の互換性レベルと CE を使用するように設定できます。 このオプションについて、次に詳しく説明します。  
  
### <a name="how-to-force-a-particular-query-plan"></a>特定のクエリ プランを強制的に実行する方法  
  
クエリ ストアでは、特定のクエリ プランを使用するようシステムを強制するさまざまな方法を示します。  
  
- **sp_query_store_force_plan**を実行します。  
  
- [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] で、 **[クエリ ストア]** ノードを展開し、 **[トップ リソース コンシューマー ノード]** を右クリックして、 **[トップ リソース コンシューマー ノードの表示]** をクリックします。 **[プランの強制]** と **[プランを強制しない]** というラベルのボタンが表示されます。  
  
クエリ ストアの詳細については、「 [クエリのストアを使用した、パフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)」を参照してください。  
  
## <a name="examples-of-ce-improvements"></a>CE の強化機能の例  
  
このセクションでは、最近のリリースで CE に実装された拡張機能からメリットを享受できるクエリの例について説明します。 これは、ユーザー側で特定の操作が要求されていない背景情報です。  
  
### <a name="example-a-ce-understands-maximum-value-might-be-higher-than-when-statistics-were-last-gathered"></a>例 A。CE は、統計が最後に収集されたときよりも、最大値が高くなる可能性があることを理解しています  
  
統計は `2016-04-30` に `OrderTable` について最後に収集され、最大 `OrderAddedDate` は `2016-04-30` であったものとします。 CE 120 (およびより高いレベル) は、"*昇順*" データを持つ `OrderTable` の列が、統計によって記録された最大値よりも大きい値を持つ可能性があることを理解しています。 これを理解すると、次のような [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT ステートメントのクエリ プランの機能を改善できます。  
  
```sql  
SELECT CustomerId, OrderAddedDate  
FROM OrderTable  
WHERE OrderAddedDate >= '2016-05-01';  
```  
  
### <a name="example-b-ce-understands-that-filtered-predicates-on-the-same-table-are-often-correlated"></a>例 B。CE は、同じテーブル上のフィルターにかけられた述語が頻繁に関連付けられることを理解しています  
  
次の SELECT では、フィルターにかけられた述語が `Model` と `ModelVariant` に表示されます。 `Model` が "Xbox" である場合は、`ModelVariant` が "One" の可能性があることを直感的に理解できます (Xbox に One というバリアントがある場合)。  
  
CE 120 以降では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は同じテーブルの 2 つの列、`Model` と `ModelVariant` の間に相関関係がある可能性があることを理解します。 CE はクエリで返される行数のより正確な見積もりを行い、[クエリ オプティマイザー](../../relational-databases/query-processing-architecture-guide.md#optimizing-select-statements)がより最適なプランを生成します。  
  
```sql  
SELECT Model, Purchase_Price  
FROM dbo.Hardware  
WHERE Model = 'Xbox' AND  
      ModelVariant = 'One';  
```  
  
### <a name="example-c-ce-no-longer-assumes-any-correlation-between-filtered-predicates-from-different-tables"></a>例 C。CE は異なるテーブルからフィルターにかけられた述語の間に、もはや相関関係がないと想定します 
最近のワークロードと実際のビジネス データに関する最新の調査によって、異なるテーブルからの述語フィルターは、通常互いに関連していないことが明らかになりました。 次のクエリでは、CE は `s.type` と `r.date` 間の相関関係がないと想定します。 そのため CE は、返される行数の推定値を低く指定します。  
  
```sql  
SELECT s.ticket, s.customer, r.store  
FROM dbo.Sales    AS s  
CROSS JOIN dbo.Returns  AS r  
WHERE s.ticket = r.ticket AND  
      s.type = 'toy' AND  
      r.date = '2016-05-11';  
```  
  
## <a name="see-also"></a>参照  
 [パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [SQL Server 2014 のカーディナリティ推定機能によるクエリプランの最適化](https://msdn.microsoft.com/library/dn673537.aspx)  
 [クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md)     
 [USE HINT クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md#use_hint)       
 [クエリ調整アシスタントを使用したデータベースのアップグレード](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)           
 [クエリのストアを使用した、パフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)    
 [クエリ処理アーキテクチャ ガイド](../../relational-databases/query-processing-architecture-guide.md)   
