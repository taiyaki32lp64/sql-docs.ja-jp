---
title: SQL Server または SQL Database に JSON ドキュメントを保存する
ms.description: This article describes why and how to store and index JSON documents in SQL Server or SQL Database, and how to optimize queries over the JSON documents.
ms.date: 01/04/2018
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
author: jovanpop-msft
ms.author: jovanpop
ms.custom: seo-dt-2019
ms.openlocfilehash: ea43d88fea017c723177e4b83c86b5c8165b734b
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096027"
---
# <a name="store-json-documents-in-sql-server-or-sql-database"></a>SQL Server または SQL Database に JSON ドキュメントを保存する
SQL Server と Azure SQL Database には、ネイティブ JSON 機能があります。標準 SQL 言語を利用し、JSON ドキュメントを解析できます。 SQL Server または SQL Database に JSON ドキュメントを保存したり、NoSQL データベースの場合のように JSON データを問い合わせたりできます。 この記事では、SQL Server または SQL Database に JSON ドキュメントを保存するためのオプションについて説明します。

## <a name="json-storage-format"></a>JSON ストレージの形式

最初のストレージ設計では、JSON ドキュメントをテーブルに格納する方法を決定します。 次の 2 つのオプションを使用できます。
- **LOB ストレージ** - JSON ドキュメントは、`NVARCHAR` 列にそのまま格納できます。 この方法では、読み込み速度が文字列型の列の読み込みに匹敵するため、データの読み込みと取り込みをすばやく行うのに最適です。 この方法では、クエリの実行中に未加工の JSON ドキュメントを解析する必要があるため、JSON 値のインデックス作成が実行されていない場合は、クエリ/分析時間のパフォーマンスがさらに低下する可能性があります。 
- **リレーショナル ストレージ** - JSON ドキュメントは、`OPENJSON`、`JSON_VALUE`、または `JSON_QUERY` 関数を使用してテーブルに挿入されるときに解析できます。 入力 JSON ドキュメントのフラグメントは、SQL データ型の列、または JSON サブ要素を含む NVARCHAR 列に格納できます。 この方法では、読み込み中に JSON の解析が行われるため読み込み時間が長くなります。ただし、クエリは、リレーショナル データに対する従来のクエリのパフォーマンスに匹敵します。

## <a name="classic-tables"></a>クラシック テーブル

SQL Server または SQL Database に JSON ドキュメントを保存する最も簡単な方法は、ドキュメントの ID とドキュメントのコンテンツが含まれる 2 列のテーブルを作成することです。 例:

```sql
create table WebSite.Logs (
    _id bigint primary key identity,
    log nvarchar(max)
);
```

この構造は、クラシック ドキュメント データベースで見られるコレクションと同じです。 プライマリ キー `_id` は自動的に増分される値であり、あらゆるドキュメントに一意の ID を与え、短時間の検索を可能にします。 ID でドキュメントを検索したり、保存されているドキュメントを ID 別に更新したりする、従来の NoSQL シナリオには、この構造が最適です。

nvarchar(max) データ型では、サイズが最大 2 GB の JSON ドキュメントを保存できます。 ただし、JSON ドキュメントが間違いなく 8 KB を超えない場合、パフォーマンス上の理由から、NVARCHAR(max) ではなく NVARCHAR(4000) を利用することをお勧めします。

先の例で作成したサンプル テーブルでは、有効な JSON ドキュメントが `log` 列に保存されているものと想定しています。 有効な JSON が `log` 列に間違いなく保存されている場合、その列で CHECK 制約を追加できます。 例:

```sql
ALTER TABLE WebSite.Logs
    ADD CONSTRAINT [Log record should be formatted as JSON]
                   CHECK (ISJSON(log)=1)
```

誰かがテーブルにドキュメントを挿入したり、テーブルのドキュメントを更新したりするたびに、JSON ドキュメントが正しく書式設定されていることがこの制約により検証されます。 制約がないとき、テーブルは挿入のために最適化されます。JSON ドキュメントは何の処理もなく列に直接追加されるためです。

テーブルに JSON ドキュメントを保存するとき、標準の Transact-SQL 言語を使用し、ドキュメントにクエリを実行できます。 例:

```sql
SELECT TOP 100 JSON_VALUE(log, '$.severity'), AVG( CAST( JSON_VALUE(log,'$.duration') as float))
 FROM WebSite.Logs
 WHERE CAST( JSON_VALUE(log,'$.date') as datetime) > @datetime
 GROUP BY JSON_VALUE(log, '$.severity')
 HAVING AVG( CAST( JSON_VALUE(log,'$.duration') as float) ) > 100
 ORDER BY AVG( CAST( JSON_VALUE(log,'$.duration') as float) ) DESC
```

*あらゆる* T-SQL 関数とクエリ句を利用して JSON ドキュメントにクエリを実行できることは大きな利点です。 SQL Server と SQL Database のクエリには、JSON ドキュメントの分析に利用できる制約がありません。 `JSON_VALUE` 関数で JSON ドキュメントから値を抽出し、それを他の値と同様にクエリで利用できます。

このように豊富な T-SQL クエリ構文を使用できることが、SQL Server および SQL Database と従来の NoSQL データベースの大きな違いです。Transact-SQL では、ほとんどの場合、JSON データの処理に必要なすべての関数を使用できます。

## <a name="indexes"></a>インデックス

クエリを実行する際、一部のプロパティでドキュメントが検索されることがよくある場合 (JSON ドキュメントの `severity` プロパティなど)、そのプロパティに従来の NONCLUSTERED インデックスを追加し、クエリを速めることができます。

指定のパスで (つまり、パス `$.severity` で) JSON 列から JSON 値を公開する計算列を作成し、この計算列で標準インデックスを作成できます。 例:

```sql
create table WebSite.Logs (
    _id bigint primary key identity,
    log nvarchar(max),

    severity AS JSON_VALUE(log, '$.severity'),
    index ix_severity (severity)
);
```

この例で使用されている計算列は永続ではない列または仮想の列であり、テーブルにスペースを追加しません。 インデックス `ix_severity` で使用され、次の例のようなクエリのパフォーマンスを改善します。

```sql
SELECT log
FROM Website.Logs
WHERE JSON_VALUE(log, '$.severity') = 'P4'
```

このインデックスの重要な特性の 1 つは、それが照合順序対応であることです。 元の NVARCHAR 列に COLLATION プロパティ (大文字小文字の区別や日本語など) がある場合、インデックスは言語ルールまたは NVARCHAR 列に関連付けられている大文字小文字の区別ルールに基づいて整理されます。 JSON ドキュメントの処理時にカスタムの言語ルールを使用する必要があるアプリケーションを世界市場向けに開発する場合、この照合順序対応は重要な機能かもしれません。

## <a name="large-tables--columnstore-format"></a>大きなテーブルと列ストア形式

コレクションに大量の JSON ドキュメントが予想される場合、コレクションに CLUSTERED COLUMNSTORE インデックスを追加することをお勧めします。次の例をご覧ください。

```sql
create sequence WebSite.LogID as bigint;
go
create table WebSite.Logs (
    _id bigint default(next value for WebSite.LogID),
    log nvarchar(max),

    INDEX cci CLUSTERED COLUMNSTORE
);
```

CLUSTERED COLUMNSTORE インデックスはデータの圧縮率が高く (最大 25x)、ストレージの領域要件を大幅に減らし、ストレージ コストを下げ、ワークロードの I/O パフォーマンスを増やします。 また、CLUSTERED COLUMNSTORE インデックスは JSON ドキュメントのテーブル スキャンと分析のために最適化されるため、この種のインデックスはログ分析には最適な選択肢かもしれません。

先の例ではシーケンス オブジェクトを利用し、値を `_id` 列に割り当てています。 ID 列では、シーケンスと ID はいずれも有効なオプションです。

## <a name="frequently-changing-documents--memory-optimized-tables"></a>頻繁に変更されるドキュメントとメモリ最適化テーブル

コレクションで多数の更新、挿入、削除操作が予想される場合、メモリ最適化テーブルに JSON ドキュメントを保存できます。 メモリ最適化 JSON コレクションでは、データが常にメモリ内に保持されます。そのため、ストレージの I/O オーバーヘッドがありません。 また、メモリ最適化 JSON コレクションにはロック制御がまったくありません。つまり、ドキュメントを操作したとき、他の操作がブロックされることはありません。

クラシック コレクションをメモリ最適化コレクションに変換しなければならない場合は、次の例に示すように、テーブル定義の後に **with (memory_optimized=on)** オプションを指定します。 これで JSON コレクションがメモリ最適化されます。

```sql
create table WebSite.Logs (
  _id bigint identity primary key nonclustered,
  log nvarchar(4000)
) with (memory_optimized=on)
```

メモリ最適化テーブルは、頻繁に変更するドキュメントに最適な選択肢です。 メモリ最適化テーブルの利用を検討するとき、パフォーマンスについても考慮してください。 メモリ最適化コレクションでは、可能であれば、JSON ドキュメントに NVARCHAR(max) ではなく NVARCHAR(4000) を使用してください。パフォーマンスが劇的に改善されることがあります。

クラシック テーブルの場合と同様に、計算列を使用して、メモリ最適化テーブルで公開するフィールドでインデックスを追加できます。 例:

```sql
create table WebSite.Logs (

  _id bigint identity primary key nonclustered,
  log nvarchar(4000),

  severity AS cast(JSON_VALUE(log, '$.severity') as tinyint) persisted,
  index ix_severity (severity)

) with (memory_optimized=on)
```

パフォーマンスを最大化するために、プロパティの値を保持できるよう、JSON 値をできるだけ小さい型にキャスト変換します。 先の例では、**tinyint** が使用されていました。

また、ストアド プロシージャに JSON ドキュメントを更新する SQL クエリを置き、ネイティブ コンパイルの利点を活かすことができます。 例:

```sql
CREATE PROCEDURE WebSite.UpdateData(@Id int, @Property nvarchar(100), @Value nvarchar(100))
WITH SCHEMABINDING, NATIVE_COMPILATION

AS BEGIN
    ATOMIC WITH (transaction isolation level = snapshot,  language = N'English')

    UPDATE WebSite.Logs
    SET log = JSON_MODIFY(log, @Property, @Value)
    WHERE _id = @Id;

END
```

ネイティブ コンパイルされたこのプロシージャはクエリを受け取り、それを実行する .DLL コードを作成します。 ネイティブ コンパイルされたプロシージャを使用することで、データのクエリ実行と更新が速くなります。

## <a name="conclusion"></a>まとめ

SQL Server と SQL Database でネイティブ JSON 関数を利用すると、NoSQL データベースの場合と同様に JSON ドキュメントを処理できます。 リレーショナルであれ、NoSQL であれ、JSON データの処理に関しては、あらゆるデータベースに良し悪しがあります。 SQL Server または SQL Database に JSON ドキュメントを保存することの主な利点は SQL 言語の完全サポートにあります。 充実した Transact-SQL 言語を利用し、さまざまストレージ オプションを構成できます (圧縮率の高い列ストア インデックス、高速の分析によるロックのない処理を可能にするメモリ最適化テーブルなど)。 同時に、発展したセキュリティ機能や国際化機能の利点が得られ、これらの機能は NoSQL シナリオで簡単に再利用できます。 この記事で説明されている理由は、SQL Server または SQL Database に JSON ドキュメントを保存する十分な理由となります。

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server と Azure SQL Database の JSON の詳細情報  
  
### <a name="microsoft-videos"></a>Microsoft ビデオ

SQL Server と Azure SQL Database に組み込まれている JSON のサポートの視覚的な紹介は、次のビデオをご覧ください。

-   [SQL Server 2016 と JSON のサポート](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 と Azure SQL Database での JSON の使用](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL とリレーショナル環境間の架け橋としての JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
