---
title: T-SQL のパフォーマンスの高速化のためのインメモリ OLTP
ms.custom: seo-dt-2019
ms.date: 09/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 1c25a164-547d-43c4-8484-6b5ee3cbaf3a
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ca32d98270a6eea4bd918c12c6b45279a05628e5
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412503"
---
# <a name="survey-of-initial-areas-in-in-memory-oltp"></a>インメモリ OLTP での初期領域の調査

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  
この記事は、Microsoft SQL Server と Azure SQL データベースのインメモリ OLTP パフォーマンス機能の基本を短時間で学習する開発者を対象にしています。  
  
この記事では、インメモリ OLTP の以下のことについて説明します。  
  
- 機能の概要。  
- 機能を実装する主なコード サンプル。  
  
  
SQL Server および SQL データベースにおけるインメモリ テクノロジのサポートにはわずかな違いしかありません。  
  
  
インメモリ OLTP は、一部のブログでは *Hekaton*と呼ばれています。  
  
  
<a name="benefits-of-in-memory-features-21a"></a>  
  
## <a name="benefits-of-in-memory-features"></a>インメモリ機能の利点  
  
SQL Server では、多くのアプリケーション システムのパフォーマンスを大幅に改善できるインメモリ機能が提供されます。 この記事では考慮事項を簡単に説明します。  
  
  
### <a name="features-for-oltp-online-transactional-processing"></a>OLTP (オンライン トランザクション処理) の機能  
  
  
多数の SQL INSERT を同時に処理する必要があるシステムには OLTP 機能が最適です。  
  
- ベンチマークでは、インメモリ機能を導入することで速度が 5 倍から 20 倍に向上することが示されています。  
  
  
Transact-SQL で大量の計算を処理するシステムには最適です。  
  
- 大量計算専用のストアド プロシージャでは、実行速度が最大 99 倍になります。  
  
  
後で、インメモリ OLTP によるパフォーマンスの向上を実証する以下の記事を参照してください。  
  
- 「[実証: インメモリ OLTP によるパフォーマンスの向上](../../relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp.md)」には、大幅なパフォーマンス向上が望める小規模なデモが用意されています。  
- 「[Sample Database for In-Memory OLTP](../../relational-databases/in-memory-oltp/sample-database-for-in-memory-oltp.md)」 (インメモリ OLTP のサンプル データベース) には、より大規模なデモが用意されています。  
  
  
  
### <a name="features-for-operational-analytics"></a>運用分析の機能  
  
インメモリ分析では、通常、GROUP BY 句を含めることによってトランザクション データを集計する SQL SELECT を参照します。 運用分析では主に *列ストア* というインデックスの種類が使用されます。  
  
2 つの主なシナリオを以下に示します。  
  
- *バッチ運用分析* では、営業時間後に実行されるか、トランザクション データのコピーを持つセカンダリ ハードウェアに対して実行される集計処理を参照します。  
  - [Azure SQL データ ウェアハウス](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-overview-what-is/) もバッチ運用分析に関連します。  
- *リアルタイム運用分析* では、営業時間内およびトランザクション ワークロードに使用されるプライマリ ハードウェアで実行される集計処理を参照します。  
  
  
この記事では分析ではなく OLTP に焦点を当てています。 列ストア インデックスを使用した SQL での分析の詳細については、次の項目を参照してください。  
  
- [列ストアを使用したリアルタイム運用分析の概要](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
- [列ストア インデックスの説明](../../relational-databases/indexes/columnstore-indexes-overview.md)  
  
  
> [!NOTE]
> 「 [Azure SQL Database - In-Memory Technologies](https://channel9.msdn.com/Blogs/Windows-Azure/Azure-SQL-Database-In-Memory-Technologies)」 (Azure SQL Database - インメモリ テクノロジ) では、インメモリ機能に関する 2 分間のビデオをご覧いただけます。 ビデオの制作日は 2015 年 12 月です。  


### <a name="columnstore"></a>列ストア

お勧めのブログの投稿を参照しながら、さまざまな観点から列ストア インデックスについて説明します。 多くの投稿では、列ストアがサポートしているリアルタイム運用分析の概念について詳しく説明します。  これらの投稿は、2016 年 3 月に Microsoft のプログラム マネージャーである Sunil Agarwal が書いたものです。

#### <a name="real-time-operational-analytics"></a>リアルタイム運用分析

1. [インメモリ テクノロジを使用したリアルタイム運用分析](https://blogs.technet.microsoft.com/dataplatforminsider/2015/12/09/real-time-operational-analytics-using-in-memory-technology/)
2. [リアルタイム運用分析 - 非クラスター化列ストア インデックス (NCCI) の概要](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/29/real-time-operational-analytics-using-nonclustered-columnstore-index/)
3. [リアルタイム運用分析: SQL Server 2016 で非クラスター化列ストア インデックス (NCCI) を使用するシンプルな例](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/29/real-time-operational-analytics-simple-example-using-nonclustered-clustered-columnstore-index-ncci/)
4. [リアルタイム運用分析: SQL Server 2016 の DML 運用と非クラスター化列ストア インデックス (NCCI)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/04/real-time-operational-analytics-dml-operations-and-nonclustered-columnstore-index-ncci-in-sql-server-2016/)
5. [リアルタイム運用分析: フィルターした非クラスター化列ストア インデックス (NCCI)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-filtered-nonclustered-columnstore-index-ncci/)
6. [リアルタイム運用分析: 非クラスター化列ストア インデックス (NCCI) の圧縮遅延オプション](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-for-nonclustered-columnstore-index-ncci/)
7. [リアルタイム運用分析: NCCI とパフォーマンスを使用した圧縮遅延オプション](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-with-ncci-and-the-performance/)
8. [リアルタイム運用分析: メモリ最適化テーブルと列ストア インデックス](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/real-time-operational-analytics-memory-optimized-table-and-columnstore-index/)

#### <a name="defragment-a-columnstore-index"></a>列ストア インデックスを最適化する

1. [REORGANIZE コマンドを使用した列ストア インデックスの最適化](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/columnstore-index-defragmentation-using-reorganize-command/)
2. [REORGANIZE の列ストア インデックス マージ ポリシー](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/08/columnstore-index-merge-policy-for-reorganize/)

#### <a name="bulk-importation-of-data"></a>データの一括インポート

1. [クラスター化列ストア: 一括読み込み](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2014/07/27/clustered-column-store-index-bulk-loading-the-data/)
2. [クラスター化列ストア インデックス: データ読み込みの最適化 - 最小ログ記録](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/10/clustered-columnstore-index-data-load-optimizations-minimal-logging/)
3. [クラスター化列ストア インデックス: データ読み込みの最適化 - 並行一括インポート](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/28/clustered-columnstore-index-parallel-bulk-import/)





<a name="features-on-in-memory-oltp-13b"></a>  
  
## <a name="features-of-in-memory-oltp"></a>インメモリ OLTP の機能  
  
インメモリ OLTP での主な機能を見てみましょう。  
  
  
#### <a name="memory-optimized-tables"></a>メモリ最適化テーブル  
  
CREATE TABLE ステートメントの T-SQL キーワード MEMORY_OPTIMIZED は、ディスクではなく、アクティブ メモリに存在するテーブルの作成方法を示します。  
  
  
[メモリ最適化テーブル](../../relational-databases/in-memory-oltp/memory-optimized-tables.md) はアクティブ メモリ内に存在し、ディスク上にセカンダリ コピーを保持します。  
  
- ディスク上のコピーは、サーバーまたはデータベースがシャットダウンして再起動した後の日常的な復旧に使用されます。 このメモリとディスクの二重性はユーザーとユーザー コードに対して完全に非表示になります。  
  
  
#### <a name="natively-compiled-modules"></a>ネイティブ コンパイル モジュール  
  
CREATE PROCEDURE ステートメントの T-SQL キーワード NATIVE_COMPILATION は、ネイティブでコンパイルしするストアド プロシージャの作成方法を示します。 T-SQL ステートメントは、データベースがオンラインで循環されるたびにネイティブ プロシージャの初回使用時にコンピューター語コードにコンパイルされます。 T-SQL 命令がそれぞれ解釈されるまで長時間待つ必要はなくなりました。  
  
- ネイティブ コンパイル ストアド プロシージャの結果は、解釈されたストアド プロシージャの 1/100 の時間で得られます。  
  
  
ネイティブ モジュールが参照できるのはメモリ最適化テーブルのみで、ディスク ベース テーブルを参照することはできません。  
  
ネイティブ コンパイル モジュールには次の 3 種類があります。  
  
- [ネイティブ コンパイル ストアド プロシージャ](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)。  
- スカラーのネイティブ コンパイル ユーザー定義関数 (UDF)。  
- ネイティブ コンパイル トリガー。  
  
  
#### <a name="availability-in-azure-sql-database"></a>Azure SQL Database での提供状況  
  
インメモリ OLTP および列ストアは、Azure SQL Database で使用できます。 詳細については、「[Optimize Performance using In-Memory Technologies in SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-in-memory)」 (SQL データベースでのインメモリ テクノロジを使用したパフォーマンスの最適化) を参照してください。
  
  
<a name="ensure-compatibility-level-gteq-130-99c"></a>  
  
## <a name="1-ensure-compatibility-level--130"></a>1.互換性レベルを 130 以上に設定する  
  
  
このセクションと以降のセクションでは、インメモリ OLTP 機能の実装に使用できる Transact-SQL 構文をまとめて示します。  
  
  
まず、データベースの互換性レベルを少なくとも 130 に設定することが重要です。 ここでは、現在のデータベースに設定されている現在の互換性レベルを表示する T-SQL コードを示します。  
  
```sql
SELECT d.compatibility_level
    FROM sys.databases as d
    WHERE d.name = Db_Name();
```
  
  
  
次は、必要に応じて互換性レベルを更新するための T-SQL コードを示します。  
  
  
  
```sql
ALTER DATABASE CURRENT
    SET COMPATIBILITY_LEVEL = 130;
```
  
  
  
<a name="elevate-to-snapshot-26n"></a>  
  
## <a name="2-elevate-to-snapshot"></a>2.スナップショットに昇格させる  
  
  
トランザクションがディスク ベース テーブルとメモリ最適化テーブルの両方に関与することを、*複数のコンテナーにまたがるトランザクション*といいます。 このようなトランザクションの場合、トランザクションのメモリ最適化部分が、SNAPSHOT と呼ばれるトランザクション分離レベルで動作する必要があります。  
  
複数のコンテナーにまたがるトランザクションでメモリ最適化テーブルを確実にこのレベルで動作させるには、次の T-SQL を実行して[データベース設定を変更](../../t-sql/statements/alter-database-transact-sql-set-options.md)します。  
  
  
  
```sql
ALTER DATABASE CURRENT
    SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
```
  
  
  
<a name="create-an-optimized-filegroup-24r"></a>  
  
## <a name="3-create-an-optimized-filegroup"></a>3.最適化ファイル グループを作成する  
  
  
Microsoft SQL Server では、メモリ最適化テーブルを作成する前に、CONTAINS MEMORY_OPTIMIZED_DATA を宣言するファイルグループを作成する必要があります。 作成したファイルグループはデータベースに割り当てられます。 詳細については、次の項目を参照してください。  
  
- [メモリ最適化ファイルグループ](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)  
  
  
Azure SQL Database では、このようなファイルグループを作成する必要はありません (作成できません)。  

次のサンプルの T-SQL スクリプトでは、インメモリ OLTP のデータベースを有効にし、すべての推奨設定を構成します。 SQL Server と Azure SQL Database の両方で機能します: [enable-in-memory-oltp.sql](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/in-memory-database/in-memory-oltp/t-sql-scripts/enable-in-memory-oltp.sql)。

MEMORY_OPTIMIZED_DATA ファイル グループのデータベースでは、サポートされていない SQL Server 機能もあります。 制限の詳細については、次を参照してください: [インメモリ OLTP に対してサポートされていない SQL Server の機能](unsupported-sql-server-features-for-in-memory-oltp.md)
  
<a name="create-a-memory-optimized-table-26y"></a>  
  
## <a name="4-create-a-memory-optimized-table"></a>4.メモリ最適化テーブルを作成する  
  
重要な Transact-SQL キーワードは MEMORY_OPTIMIZED です。  
  
  
  
```sql
CREATE TABLE dbo.SalesOrder
    (
        SalesOrderId   integer   not null   IDENTITY
            PRIMARY KEY NONCLUSTERED,
        CustomerId   integer    not null,
        OrderDate    datetime   not null
    )
        WITH
            (MEMORY_OPTIMIZED = ON,
            DURABILITY = SCHEMA_AND_DATA);
```
  
  
  
メモリ最適化テーブルに対する Transact SQL の INSERT ステートメントと SELECT ステートメントは、通常のテーブルの場合と同じです。  
  
#### <a name="alter-table-for-memory-optimized-tables"></a>メモリ最適化テーブルの ALTER TABLE  
  
ALTER TABLE...ADD/DROP では、メモリ最適化テーブルの列またはインデックスを追加または削除できます。  
  
- メモリ最適化テーブルに対して CREATE INDEX や DROP INDEX を実行することはできません。代わりに、ALTER TABLE ...ADD/DROP INDEX を使用してください。  
- 詳細については、「 [メモリ最適化テーブルの変更](../../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md)」を参照してください。  
  
  
#### <a name="plan-your-memory-optimized-tables-and-indexes"></a>メモリ最適化テーブルとインデックスの計画  
  
  
- [メモリ最適化テーブルのインデックス](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)  
- [インメモリ OLTP でサポートされていない Transact-SQL の構造](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
  
<a name="create-a-natively-compiled-stored-procedure-native-proc-29u"></a>  
  
## <a name="5-create-a-natively-compiled-stored-procedure-native-proc"></a>5.ネイティブ コンパイル ストアド プロシージャ (ネイティブ プロシージャ) を作成する  
  
  
重要なキーワードは NATIVE_COMPILATION です。  
  
  
  
```sql
CREATE PROCEDURE ncspRetrieveLatestSalesOrderIdForCustomerId  
        @_CustomerId   INT  
        WITH  
            NATIVE_COMPILATION,  
            SCHEMABINDING  
    AS  
    BEGIN ATOMIC  
        WITH  
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'us_english')  
      
        DECLARE @SalesOrderId int, @OrderDate datetime;
      
        SELECT TOP 1  
                @SalesOrderId = s.SalesOrderId,  
                @OrderDate    = s.OrderDate  
            FROM dbo.SalesOrder AS s  
            WHERE s.CustomerId = @_CustomerId  
            ORDER BY s.OrderDate DESC;  
      
        RETURN @SalesOrderId;  
    END;  
```
  
  
  
SCHEMABINDING キーワードは、ネイティブ プロシージャで参照されているテーブルを削除するには、先にネイティブ プロシージャを削除しておく必要があることを意味します。 詳細については、「[ネイティブ コンパイル ストアド プロシージャの作成](../../relational-databases/in-memory-oltp/creating-natively-compiled-stored-procedures.md)」を参照してください。  
  
メモリ最適化テーブルにアクセスするために、ネイティブでコンパイルされたストアド プロシージャを作成する必要はありません。 従来のストアド プロシージャとアドホック バッチからメモリ最適化テーブルを参照することもできます。
  
<a name="execute-the-native-proc-31e"></a>  
  
## <a name="6-execute-the-native-proc"></a>6.ネイティブ プロシージャを実行する  
  
  
テーブルにデータを 2 行挿入します。  
  
  
  
```sql
INSERT into dbo.SalesOrder  
        ( CustomerId, OrderDate )  
    VALUES  
        ( 42, '2013-01-13 03:35:59' ),
        ( 42, '2015-01-15 15:35:59' );
```
  
  
  
EXECUTE によるネイティブ コンパイル ストアド プロシージャの呼び出しが後に続きます。  
  
  
  
```sql
DECLARE @LatestSalesOrderId int, @mesg nvarchar(128);
      
EXECUTE @LatestSalesOrderId =  
    ncspRetrieveLatestSalesOrderIdForCustomerId 42;
      
SET @mesg = CONCAT(@LatestSalesOrderId,  
    ' = Latest SalesOrderId, for CustomerId = ', 42);
PRINT @mesg;  
```
      
    -- Here is the actual PRINT output:  
    -- 2 = Latest SalesOrderId, for CustomerId = 42  
  
  
  
  
<a name="guide-to-the-documentation-and-next-steps-32w"></a>  
  
### <a name="guide-to-the-documentation-and-next-steps"></a>ドキュメント ガイドと次のステップ  
  
  
上記の簡単な例では、インメモリ OLTP の高度な機能を学習するための基礎を示しました。 以降のセクションでは、特に考慮する必要がある事項と、その詳細について説明した参照先を示します。  
  
  
  
<a name="how-do-in-memory-oltp-features-work-so-much-faster-33v"></a>  
  
## <a name="how-in-memory-oltp-features-work-so-much-faster"></a>インメモリ OLTP 機能が高速で動作するしくみ  
  
  
以降のサブセクションでは、インメモリ OLTP 機能が内部でどのように動作してパフォーマンスを向上させているかについて、簡単に説明します。  
  
  
<a name="how-do-memory-optimized-tables-perform-faster-34q"></a>  
  
### <a name="how-memory-optimized-tables-perform-faster"></a>メモリ最適化テーブルが高速で動作するしくみ  
  
  
**デュアル構成:** メモリ最適化テーブルはデュアル構成になっており、アクティブ メモリ内とハード ディスク上に 1 つずつ存在します。 各トランザクションは両方のテーブルに対してコミットされます。 トランザクションは、より高速なアクティブ メモリ内のテーブルに対して操作を行います。 そのためメモリ最適化テーブルは、ディスクよりも高速なアクティブ メモリの恩恵を受けることになります。 さらに、アクティブ メモリは非常に敏捷なので、速度に関して最適化されたより高度なテーブル構造も使用できます。 高度なテーブル構造はページレスでもあるため、ラッチやスピンロックのオーバーヘッドや競合を回避できます。  
  
  
**ロックなし:** メモリ最適化テーブルは*オプティミスティックな*アプローチにより、データの整合性と、コンカレンシーおよび高スループットとのバランスを取っています。 トランザクションの間、更新されたデータ行のどのバージョンもロックすることはありません。 これにより、特に大規模システムでは大幅に競合を減らすことができます。  
  
  
**行のバージョン:** メモリ最適化テーブルは、更新された行をロックする代わりに、更新された行の新しいバージョンを (tempdb ではなく) テーブルに追加します。 元の行は、トランザクションがコミットされるまで保持されます。 トランザクションの間も、他のプロセスが行の元のバージョンを読み取ることができます。  
  
- ディスク ベース テーブルの行に複数のバージョンが作成されると、行のバージョンは一時的に tempdb に格納されます。  
  
  
**ログ記録の削減:** 行の更新前と更新後のバージョンは、メモリ最適化テーブルに保持されます。 この行のペアによって、従来はログ ファイルに書き込まれていた情報の多くが提供されるので、 システムが書き込むログの量も頻度も少なくて済むようになります。 ログの量と頻度が減っても、トランザクションの整合性は保証されます。  
  
  
<a name="how-do-native-procs-perform-faster-35x"></a>  
  
### <a name="how-native-procs-perform-faster"></a>ネイティブ プロシージャが高速で動作するしくみ  
  
通常の解釈されたストアド プロシージャをネイティブ コンパイル ストアド プロシージャに変換すると、実行時の命令の数が大幅に減少します。  
  
  
<a name="trade-offs-of-in-memory-features-36j"></a>  
  
## <a name="trade-offs-of-in-memory-features"></a>インメモリ機能のトレードオフ  
  
  
コンピューター サイエンスの世界では一般的なことですが、インメモリ機能によるパフォーマンスの向上にはトレードオフがあります。 優れた機能にはよりコストがかかりますが、それに見合うだけの有益な利点がもたらされます。 トレードオフに関する包括的なガイドは次の場所にあります。

- [SQL Server でのインメモリ OLTP 機能の採用計画](../../relational-databases/in-memory-oltp/plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)

このセクションの残りの部分では、主要な計画とトレードオフの考慮事項の一部を示します。
  
<a name="trade-offs-of-memory-optimized-tables-37d"></a>  
  
### <a name="trade-offs-of-memory-optimized-tables"></a>メモリ最適化テーブルのトレードオフ  
  
  
**メモリの推定:** メモリ最適化テーブルが消費するアクティブ メモリの量を見積もる必要があります。 コンピューター システムに、メモリ最適化テーブルをホストするのに十分なメモリ容量が必要です。 詳細については、次の項目を参照してください。  
  
- [メモリ使用量の監視とトラブルシューティング](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)  
- [メモリ最適化テーブルのメモリ必要量の推定](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)  
- [メモリ最適化テーブルのテーブルと行のサイズ](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)  
  
  
**大規模テーブルのパーティション分割:** 大量のアクティブ メモリの需要を満たす方法の 1 つは、大規模なテーブルをパーティション分割して、*使用中の最近の*データ行を格納する部分 (メモリ内) と、出荷済みや完了済みの注文など、*使用していない古い*行を格納する部分 (ディスク上) に分けることです。 このパーティション分割は、手動で設計して実装します。 参照:  
  
- [アプリケーション レベルのパーティション分割](../../relational-databases/in-memory-oltp/application-level-partitioning.md)  
- [メモリ最適化テーブルのパーティション分割に関するアプリケーションのパターン](../../relational-databases/in-memory-oltp/application-pattern-for-partitioning-memory-optimized-tables.md)  
  
<a name="trade-offs-of-native-procs-38p"></a>  
  
### <a name="trade-offs-of-native-procs"></a>ネイティブ プロシージャのトレードオフ  
  
- ネイティブ コンパイル ストアド プロシージャは、ディスク ベース テーブルにアクセスできません。 ネイティブ プロシージャは、メモリ最適化テーブルにのみアクセスできます。  
- サーバーまたはデータベースがオンラインに戻った後、初めてネイティブ プロシージャを実行するときは、そのネイティブ プロシージャを一度再コンパイルする必要があります。 そのため、ネイティブ プロシージャが実行するまでに遅延が発生します。  
  
<a name="advanced-considerations-for-memory-optimized-tables-39n"></a>  
  
## <a name="advanced-considerations-for-memory-optimized-tables"></a>メモリ最適化テーブルに関する高度な考慮事項  
  
[メモリ最適化テーブルのインデックス](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md) は、従来のディスク上のテーブルのインデックスとはいくつかの点が異なります。 ハッシュ インデックスは、メモリ最適化テーブルでのみ使用できます。
    
- [メモリ最適化テーブルのハッシュ インデックス](../../relational-databases/sql-server-index-design-guide.md#hash_index)
- [メモリ最適化テーブル用の非クラスター化インデックス](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index) 
  
計画したメモリ最適化テーブルとインデックスのための十分なアクティブ メモリがあることを確認する必要があります。 参照:  
  
- [メモリ最適化オブジェクト用ストレージの作成と管理](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
メモリ最適化テーブルは DURABILITY = SCHEMA_ONLY で宣言できます。  
  
- この構文は、データベースがオフラインになったときにメモリ最適化テーブルからすべてのデータを破棄するようシステムに指示します。 テーブル定義のみが保持されます。  
- データベースがオンラインに復帰すると、メモリ最適化テーブルがアクティブ メモリに読み込まれ、データは空になります。  
- 数千の行が含まれている場合は、tempdb の [#temporary テーブルよりも](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md) SCHEMA_ONLY テーブルの方が適していることがあります。  
  
テーブル変数をメモリ最適化として宣言することもできます。 参照:  
  
- [メモリ最適化を使用した一時テーブルとテーブル変数の高速化](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)  
  
<a name="advanced-considerations-for-natively-compiled-modules-40k"></a>  
  
## <a name="advanced-considerations-for-natively-compiled-modules"></a>ネイティブ コンパイル モジュールに関する高度な考慮事項  
  
Transact-SQL で使用可能なネイティブ コンパイル モジュールの種類:  
  
- ネイティブ コンパイル ストアド プロシージャ (ネイティブ プロシージャ)。  
- スカラーのネイティブ コンパイル [ユーザー定義関数](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)。  
- ネイティブ コンパイル トリガー (ネイティブ トリガー)。  
  - メモリ最適化テーブルでは、ネイティブ コンパイル トリガーのみが許可されます。  
- ネイティブ コンパイル [テーブル値関数](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)。  
  - [Improving temp table and table variable performance using memory optimization](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/21/improving-temp-table-and-table-variable-performance-using-memory-optimization/)  
  
ネイティブ コンパイルのユーザー定義関数 (UDF) は、解釈された UDF よりも高速で実行されます。 UDF に関するいくつかの考慮事項を以下に示します。  
  
- T-SQL SELECT で UDF を使用する場合は、返される行ごとに常に 1 回 UDF が呼び出されます。  
  - UDF はインラインで実行されることはなく、常に呼び出されます。  
  - コンパイル済みであるかどうかは、すべての UDF で繰り返される呼び出しのオーバーヘッドに比べると、あまり重要ではありません。  
  - それでも、UDF 呼び出しのオーバーヘッドは、多くの場合、実用レベルでは許容可能です。  
  
ネイティブ UDF のパフォーマンスに関するテスト データと説明については、以下を参照してください。  
  
  - [Soften the RBAR impact with Native Compiled UDFs in SQL Server 2016](https://blogs.msdn.microsoft.com/sqlcat/2016/02/17/soften-the-rbar-impact-with-native-compiled-udfs-in-sql-server-2016/)  
  - 2016 年 1 月、Gail Shaw 氏によるブログ投稿「[Natively Compiled User Defined Functions](https://sqlinthewild.co.za/index.php/2016/01/12/natively-compiled-user-defined-functions/)」 (ネイティブ コンパイル ユーザー定義関数)。  
  
<a name="documentation-guide-for-memory-optimized-tables-41z"></a>  
  
## <a name="documentation-guide-for-memory-optimized-tables"></a>メモリ最適化テーブルのドキュメント ガイド  
  
メモリ最適化テーブルの特別な考慮事項について説明した以下の記事も参照してください。  
  
- [インメモリ OLTP への移行](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  - [テーブルまたはストアド プロシージャをインメモリ OLTP に移植する必要があるかどうかの確認](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)  
  - SQL Server Management Studio のトランザクション パフォーマンス分析レポートは、インメモリ OLTP によってデータベース アプリケーションのパフォーマンスが向上するかどうかを評価するために役立ちます。  
  - [メモリ最適化アドバイザー](../../relational-databases/in-memory-oltp/memory-optimization-advisor.md) を使用すると、ディスク ベース データベース テーブルをインメモリ OLTP に簡単に移行できます。   
- [メモリ最適化テーブルのバックアップ、復元、復旧](https://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  
  - メモリ最適化テーブルで使用されるストレージはメモリ内にあるときのサイズを大きく上回ることがあり、データベースのバックアップのサイズに影響します。  
- [メモリ最適化テーブルでのトランザクション](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)  
  - メモリ最適化テーブルでのトランザクションに関する、T-SQL の再試行ロジックの情報が含まれます。  
- [Transact-SQL によるインメモリ OLTP のサポート](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  - メモリ最適化テーブルとネイティブ プロシージャでの T-SQL とデータ型のサポート状況を示します。  
- [Bind a Database with Memory-Optimized Tables to a Resource Pool](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)(メモリ最適化テーブルを持つデータベースのリソース プールへのバインド) - オプションの高度な考慮事項について説明しています。  

<a name="documentation-guide-for-native-procs-42b"></a>  
  
## <a name="documentation-guide-for-native-procs"></a>ネイティブ プロシージャのドキュメント ガイド  

目次にある次の記事とその子記事は、ネイティブにコンパイルされたストアド プロシージャについて詳しく説明しています。

- [ネイティブ コンパイル ストアド プロシージャ](natively-compiled-stored-procedures.md)
  
<a name="related-links-43f"></a>  
  
## <a name="related-links"></a>関連リンク  
  
- 最初の記事: [インメモリ OLTP (インメモリ最適化)](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
    
インメモリ OLTP を使用して実現できるパフォーマンスの向上を実証するためのコードを提供する記事は以下のとおりです。  
  
- 「[実証: インメモリ OLTP によるパフォーマンスの向上](../../relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp.md)」には、大幅なパフォーマンス向上が望める小規模なデモが用意されています。  
- 「[Sample Database for In-Memory OLTP](../../relational-databases/in-memory-oltp/sample-database-for-in-memory-oltp.md)」 (インメモリ OLTP のサンプル データベース) には、より大規模なデモが用意されています。  
