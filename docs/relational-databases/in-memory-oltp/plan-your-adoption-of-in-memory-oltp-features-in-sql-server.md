---
title: 'インメモリ OLTP の採用計画 '
ms.custom: seo-dt-2019
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 041b428f-781d-4628-9f34-4d697894e61e
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f899a8fc1ad5a316784a83cb13f29acb84a01b2b
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412552"
---
# <a name="plan-your-adoption-of-in-memory-oltp-features-in-sql-server"></a>SQL Server でのインメモリ OLTP 機能の採用計画
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


この記事では、インメモリ機能の採用がどのようにビジネス システムの他の側面に影響するかを説明します。



## <a name="a-adoption-of-in-memory-oltp-features"></a>A. インメモリ OLTP 機能の採用


次のサブセクションでは、インメモリ機能を採用して実装する計画を立てる場合に考慮する必要がある要因について説明します。 多くの説明情報を以下の場所で入手することができます。

- [インメモリ OLTP を使用して Azure SQL データベースのアプリケーション パフォーマンスを向上させる](https://azure.microsoft.com/documentation/articles/sql-database-in-memory-oltp-migration/)



### <a name="a1-prerequisites"></a>A.1 前提条件

インメモリ機能を使用するための前提条件の 1 つに、SQL 製品のエディションまたはサービス層が関係する場合があります。 この前提条件とその他の前提条件については、次の情報を参照してください。

- [メモリ最適化テーブルを使用するための要件](../../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)
    - [SQL Server 2016 のエディションとコンポーネント](../../sql-server/editions-and-components-of-sql-server-2016.md)
    - [SQL Database の価格レベルの提案](https://azure.microsoft.com/documentation/articles/sql-database-service-tier-advisor/)


### <a name="a2-forecast-the-amount-of-active-memory"></a>A.2 アクティブ メモリ量の予測

新しいメモリ最適化テーブルをサポートするのに十分なアクティブ メモリがシステムにありますか?

#### <a name="microsoft-sql-server"></a>Microsoft SQL Server

200 GB のデータを含むメモリ最適化テーブルには、サポート専用の 200 GB を超えるアクティブ メモリが必要です。 大量のデータを含むメモリ最適化テーブルを実装する前に、サーバー コンピューターへの追加が必要になる場合がある追加のアクティブ メモリの量を予測する必要があります。 推定のガイダンスについては、次の情報を参照してください。

- [メモリ最適化テーブルのメモリ必要量の推定](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)

#### <a name="azure-sql-database"></a>Azure SQL データベース

Azure SQL データベースのクラウド サービスでホストされているデータベースの場合、選択したサービス層が、データベースで消費可能なアクティブ メモリの量に影響します。 アラートを使用してデータベースのメモリ使用量を監視する計画を立てる必要があります。 詳細については、次の情報を参照してください。

- [価格レベル](https://docs.microsoft.com/azure/sql-database/sql-database-purchase-models)に対するインメモリ OLTP ストレージの制限を確認する
- [インメモリ OLTP ストレージの監視](https://azure.microsoft.com/documentation/articles/sql-database-in-memory-oltp-monitoring/)

#### <a name="memory-optimized-table-variables"></a>メモリ最適化テーブル変数

**tempdb** データベース内にある従来の #TempTable よりも、メモリ最適化として宣言されるテーブル変数の方が適していることがあります。 このようなテーブル変数の場合、大量のアクティブ メモリを使用することなく、パフォーマンスを大幅に改善することができます。

### <a name="a3-table-must-be-offline-to-convert-to-memory-optimized"></a>A.3 メモリ最適化に変換するにはテーブルをオフラインにする必要がある

いくつかの ALTER TABLE 機能をメモリ最適化テーブルで使用することができます。 ただし、ALTER TABLE ステートメントを実行して、ディスク ベース テーブルをメモリ最適化テーブルに変換することはできません。 代わりに、より手動的な一連の手順を使用する必要があります。 ディスク ベース テーブルをメモリ最適化テーブルに変換できるさまざまな方法を以下に示します。

#### <a name="manual-scripting"></a>手動でのスクリプト作成

ディスク ベース テーブルをメモリ最適化テーブルに変換する方法の 1 つとして、必要な Transact-SQL ステップを自分でコード化する方法があります。


1. アプリケーション アクティビティを中断します。

2. 完全バックアップを実行します。

3. ディスク ベース テーブルの名前を変更します。

4. CREATE TABLE ステートメントを実行して、新しいメモリ最適化テーブルを作成します。

5. ディスク ベース テーブルからサブ SELECT を指定してメモリ最適化テーブルへの挿入を行います。

6. ディスク ベース テーブルを削除します。

7. さらに完全バックアップを実行します。

8. アプリケーション アクティビティを再開します。


#### <a name="memory-optimization-advisor"></a>メモリ最適化アドバイザー

メモリ最適化アドバイザー ツールでは、ディスク ベース テーブルからメモリ最適化テーブルへの変換に役立つスクリプトを生成できます。 このツールは、SQL Server Data Tools (SSDT) の一部としてインストールされます。

- [メモリ最適化アドバイザー](../../relational-databases/in-memory-oltp/memory-optimization-advisor.md)
- [SQL Server Data Tools (SSDT) のダウンロード](../../ssdt/download-sql-server-data-tools-ssdt.md)


#### <a name="dacpac-file"></a>.dacpac ファイル

SSDT で管理される、.dacpac ファイルを使用してデータベースのインプレース更新を行うことができます。 SSDT では、.dacpac ファイルにエンコードされているスキーマの変更を指定できます。

*Database*型の Visual Studio プロジェクト コンテキストで .dacpac ファイルを操作します。

- [データ層アプリケーション](../../relational-databases/data-tier-applications/data-tier-applications.md) と .dacpac ファイル



### <a name="a4-guidance-for-whether-in-memory-oltp-features-are-right-for-your-application"></a>A.4 インメモリ OLTP 機能がアプリケーションに適しているかどうかに関するガイダンス

インメモリ OLTP 機能で特定のアプリケーションのパフォーマンスを改善できるかに関するガイダンスについては、次の情報を参照してください。

- [インメモリ OLTP (インメモリ最適化)](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)



## <a name="b-unsupported-features"></a>B. サポートされていない機能

特定のインメモリ OLTP シナリオでサポートされていない機能については、以下の情報を参照してください。

- [インメモリ OLTP に対してサポートされていない SQL Server の機能](../../relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)


次のサブセクションでは、より重要ないくつかのサポートされていない機能に重点を置きます。


### <a name="b1-snapshot-of-a-database"></a>B.1 データベースのスナップショット

メモリ最適化テーブルまたはモジュールを特定のデータベースで初めて作成した場合、データベースの [スナップショット](../../relational-databases/databases/database-snapshots-sql-server.md) を取得することはできません。 具体的な理由を以下に示します。

- 最初のメモリ最適化項目の場合、メモリ最適化ファイル グループから最後のファイルを削除することはできません。
- メモリ最適化ファイル グループのファイルがないデータベースではスナップショットをサポートできません。

通常、スナップショットは簡単なテスト イテレーションで役立ちます。


### <a name="b2-cross-database-queries"></a>B.2 複数データベースにまたがるクエリ

メモリ最適化テーブルで [複数データベース](../../relational-databases/in-memory-oltp/cross-database-queries.md) にまたがるトランザクションはサポートされません。 メモリ最適化テーブルにもアクセスする同じトランザクションまたは同じクエリから別のデータベースにアクセスすることはできません。

テーブル変数はトランザクション処理されません。 したがって、複数データベースにまたがるクエリでは [メモリ最適化テーブル変数](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md) を使用できます。


### <a name="b3-readpast-table-hint"></a>B.3 READPAST テーブル ヒント

クエリでは、READPAST [テーブル ヒント](../../t-sql/queries/hints-transact-sql-table.md) をどのメモリ最適化テーブルにも適用できません。

READPAST ヒントは、複数のセッションでそれぞれ、キューの処理時などに、同じ小さな行セットに対してアクセスおよび変更を行うシナリオで役立ちます。


### <a name="b4-rowversion-sequence"></a>B.4 RowVersion、Sequence

- メモリ最適化テーブルでは、 [RowVersion](../../t-sql/data-types/rowversion-transact-sql.md) の列にタグを付けることはできません。


- [SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md) はメモリ最適化テーブルの制約では使用できません。 たとえば、NEXT VALUE FOR 句では DEFAULT 制約を作成できません。 SEQUENCE は、INSERT および UPDATE ステートメントで使用できます。


## <a name="c-administrative-maintenance"></a>C. 管理メンテナンス


このセクションでは、メモリ最適化テーブルが使用されるデータベース管理の違いについて説明します。


### <a name="c1-identity-seed-reset-increment--1"></a>C.1 Identity シードのリセット、増分値が 1 より大きい

IDENTITY 列を再シードするために[DBCC CHECKIDENT](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)をメモリ最適化テーブルで使用することはできません。

メモリ最適化テーブルでは、IDENTITY 列に対する増分値はちょうど 1 に限定されます。


### <a name="c2-dbcc-checkdb-cannot-validate-memory-optimized-tables"></a>C.2 DBCC CHECKDB でメモリ最適化テーブルを検証することはできない

[DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) コマンドは、そのターゲットがメモリ最適化テーブルである場合、機能しません。 回避策として、次の手順を実行してください。


1. [トランザクション ログをバックアップします](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)。

2. メモリ最適化ファイル グループ内のファイルを null デバイスにバックアップします。 バックアップ プロセスでは、チェックサム検証を呼び出します。

    破損が見つかった場合は、次の手順に進みます。

3. メモリ最適化テーブルからディスク ベース テーブルにデータをコピーし、一時的に保存します。

4. メモリ最適化ファイル グループのファイルを復元します。

5. ディスク ベース テーブルに一時的に保存したデータをメモリ最適化テーブルに挿入します。

6. データを一時的に保存したディスク ベース テーブルを削除します。



## <a name="d-performance"></a>D. パフォーマンス

このセクションでは、メモリ最適化テーブルの優れたパフォーマンスが最大限に生かされないままになる可能性のある状況について説明します。


### <a name="d1-index-considerations"></a>D.1 インデックスに関する考慮事項

メモリ最適化テーブルのすべてのインデックスは、テーブル関連ステートメントの CREATE TABLE と ALTER TABLE で作成され、管理されます。 CREATE INDEX ステートメントではメモリ最適化テーブルを対象にすることはできません。

メモリ最大化テーブルを初めて実装する際に、多くの場合、従来の B ツリー非クラスター化インデックスを選択するのが賢明かつ簡単です。 後で、アプリケーションのパフォーマンスを確認してから、インデックスの別の種類への切り替えを検討できます。

次の特殊な 2 種類のインデックスでは、メモリ最適化テーブルのコンテキストでのディスカッションが必要になります:ハッシュ インデックスと列ストア インデックス。

メモリ最適化テーブルのインデックスの概要については、次の情報を参照してください。

- [メモリ最適化テーブルのインデックス](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)


#### <a name="hash-indexes"></a>ハッシュ インデックス

ハッシュ インデックスは、' **=** ' 演算子を使用して正確な主キー値で 1 つの特定の行に最も速くアクセスできる形式です。

- ' **!=** '、' **>** '、または '**BETWEEN**' などの不正確な演算子をハッシュ インデックスで使用すると、パフォーマンスが損なわれます。

- キー値の重複率が高くなる場合、ハッシュ インデックスは最良の選択とは言えないかもしれません。

- 個々のバケット内のチェーンが長くならないように、ハッシュ インデックスで必要になる可能性がある *バケット* 数を低く見積もらないでください。 詳細については、次の情報を参照してください。
    - [メモリ最適化テーブルのハッシュ インデックス](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md)


#### <a name="nonclustered-columnstore-indexes"></a>非クラスター化列ストア インデックス

メモリ最適化テーブルは、 *オンライン トランザクション処理* (つまり、 *OLTP*) と呼ばれるパラダイムにおいて、一般的なビジネス トランザクション データの高スループットを提供します。 列ストア インデックスは、集計と同様の処理 ( *分析*と呼ばれる) の高スループットを提供します。 OLTP と分析の両方のニーズを満たすために使用できるこれまでの最良の方法は、データの大量移動を行うテーブルと、ある程度のデータ重複を伴うテーブルを個別に使用する方法でした。 現在は、より簡単な **ハイブリッド ソリューション** を利用して、メモリ最適化テーブルに列ストア インデックスを作成することができます。


- [列ストア インデックス](../../relational-databases/indexes/columnstore-indexes-overview.md) は、クラスター化インデックスとしても、ディスク ベース テーブルに作成することができます。 ただし、メモリ最適化テーブルで列ストア インデックスをクラスター化することはできません。


- メモリ最適化テーブルに LOB または行外列がある場合、テーブルに列ストア インデックスを作成できません。


- テーブルに列ストア インデックスが存在する場合、メモリ最適化テーブルに対して ALTER TABLE ステートメントを実行することはできません。
    - 2016 年 8 月現在、Microsoft には列ストア インデックスの再作成パフォーマンスを改善するための短期的な計画があります。



### <a name="d2-lob-and-off-row-columns"></a>D.2 LOB および行外列

ラージ オブジェクト (LOB) は varchar(**max**) などの型の列です。 メモリ最適化テーブルで LOB 列をいくつか使用しても、おそらく、パフォーマンスにはそれほど悪影響はありません。 ただし、データで必要以上の LOB 列は使用しないでください。 行外列の場合も同様です。 varchar(512) で十分な場合は、列を nvarchar(3072) として定義しないでください。


LOB および行外列の詳細については、次の情報を参照してください。

- [メモリ最適化テーブルのテーブルと行のサイズ](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)
- [インメモリ OLTP に対してサポートされるデータ型](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md)



## <a name="e-limitations-of-native-procs"></a>E. ネイティブ プロシージャの制限事項


Transact-SQL の特定の要素は、ネイティブ コンパイル T-SQL モジュール (ストアド プロシージャを含む) ではサポートされていません。 サポートされている機能の詳細については、次の記事を参照してください。

- [ネイティブ コンパイル T-SQL モジュールでサポートされる機能](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)

サポートされていない機能を使用している Transact-SQL モジュールをネイティブ コンパイル モジュールに移行する際の考慮事項については、次の記事を参照してください。

- [ネイティブ コンパイル ストアド プロシージャの移行に関する問題](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)

Transact-SQL の特定の要素に対する制限事項に加えて、ネイティブ コンパイル T-SQL モジュールでサポートされているクエリ操作に対する制限事項もあります。 このような制限事項があるために、ネイティブ コンパイル ストアド プロシージャは大きなデータ セットを処理する分析クエリに適していません。

#### <a name="no-parallel-processing-in-a-native-proc"></a>ネイティブ プロシージャでは並列処理を使用できない

ネイティブ プロシージャのクエリ プランの一部として、並列処理を使用することはできません。 ネイティブ プロシージャは常にシングル スレッドです。


#### <a name="join-types"></a>結合の種類


ハッシュ結合やマージ結合を、ネイティブ プロシージャのクエリ プランの一部として使用することはできません。 入れ子になったループ結合が使用されます。


#### <a name="no-hash-aggregation"></a>ハッシュ集計を使用できない

ネイティブ プロシージャのクエリ プランで集計フェーズが必要な場合に使用できるのはストリーム集計のみです。 ネイティブ プロシージャのクエリ プランではハッシュ集計はサポートされていません。

- 多くの行からデータを集計する必要がある場合には、ハッシュ集計をお勧めします。



## <a name="f-application-design-transactions-and-retry-logic"></a>F. アプリケーション デザイン:トランザクションと再試行ロジック

メモリ最適化テーブルに関係するトランザクションは、同じテーブルに関係する別のトランザクションに依存できます。 従属トランザクション数が許容最大値を超えた場合、すべての従属トランザクションが失敗します。

SQL Server 2016 の場合

- 従属トランザクションの許容最大値は 8 です。 8 は、指定されたトランザクションが従属できるトランザクションの制限でもあります。
- エラー番号は 41839 です (SQL Server 2014 の場合、エラー番号は 41301 になります)。


スクリプトに *再試行ロジック* を追加することで、Transact-SQL スクリプトを考えられるトランザクション エラーに対してより堅牢にすることができます。 再試行ロジックは、UPDATE や DELETE 呼び出しが頻繁に行われる場合や、メモリ最適化テーブルが別のテーブルの外部キーによって参照される場合に特に役立つことがあります。 詳細については、次の情報を参照してください。

- [メモリ最適化テーブルでのトランザクション](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)
- [メモリ最適化テーブルでのトランザクション依存の制限 - エラー 41839](https://blogs.msdn.microsoft.com/sqlcat/2016/07/11/transaction-dependency-limits-with-memory-optimized-tables-error-41839/)



## <a name="related-links"></a>関連リンク

- [インメモリ OLTP (インメモリ最適化)](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)


