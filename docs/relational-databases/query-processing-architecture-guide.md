---
title: クエリ処理アーキテクチャ ガイド | Microsoft Docs
ms.custom: ''
ms.date: 02/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- guide, query processing architecture
- query processing architecture guide
- row mode execution
- batch mode execution
ms.assetid: 44fadbee-b5fe-40c0-af8a-11a1eecf6cb5
author: rothja
ms.author: jroth
ms.openlocfilehash: bb6463efe0b4b4f5d7b009eae6f9a4a612cf5e7e
ms.sourcegitcommit: 722f2ec5a1af334f5bcab8341bc744d16a115273
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74866079"
---
# <a name="query-processing-architecture-guide"></a>クエリ処理アーキテクチャ ガイド
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] は、ローカル テーブル、パーティション テーブル、複数のサーバーに分散されたテーブルなどさまざまなデータ ストレージ アーキテクチャでクエリを処理します。 以下のトピックでは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] でクエリを処理して、実行プランのキャッシュによりクエリの再利用を最適化する方法について説明します。

## <a name="execution-modes"></a>実行モード
[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] は、2 つの異なる処理モードで [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを処理できます。
- 行モード実行
- バッチ モード実行

### <a name="row-mode-execution"></a>行モード実行
*行モード実行*は、データが行形式で格納される、従来の RDMBS テーブルで使用されるクエリ処理方法です。 クエリが実行され、行ストア テーブルのデータにアクセスするとき、実行ツリーの演算子と子演算子は、テーブル スキーマに指定されている列全体で、必要な行をそれぞれ読み取ります。 SELECT ステートメント、JOIN 述語、フィルター述語で参照される結果セットに必要な列を [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は読み取られる各行から取得します。

> [!NOTE]
> 行モード実行は OLTP シナリオで非常に効率的ですが、データ ウェアハウスのシナリオなど、大量のデータをスキャンするときは効率性が下がることがあります。

### <a name="batch-mode-execution"></a>バッチ モード実行  
*バッチ モード実行*は、複数の行をまとめて処理するためのクエリ処理方法です (そのため、バッチという言葉が使われています)。 バッチ内の各列は、別個のメモリ領域のベクトルとして格納されています。そのため、バッチ モード処理はベクトル基準となります。 バッチ モード処理ではまた、マルチコア CPU 向けに最適化されており、最新ハードウェアでメモリ スループットを上げるアルゴリズムが使用されています。      

バッチ モード実行は、列ストア ストレージ形式と緊密に統合され、このストレージ形式に合わせて最適化されています。 バッチ モードの処理は、可能な場合は圧縮データに対して行われるので、行モード実行で使用される[交換操作](../relational-databases/showplan-logical-and-physical-operators-reference.md#exchange)が不要になります。 結果的に、並行処理の向上と高速なパフォーマンスが得られます。    

クエリがバッチ モードで実行され、列ストア インデックスのデータにアクセスするとき、実行ツリーの演算子と子演算子は、列セグメントにある複数の行をまとめて読み取ります。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は、SELECT ステートメント、JOIN 述語、フィルター述語で参照される結果に必要な列のみ読み取ります。    
列ストア インデックスの詳細については、「[列ストア インデックスのアーキテクチャ](../relational-databases/sql-server-index-design-guide.md#columnstore_index)」を参照してください。  

> [!NOTE]
> バッチ モード実行は、大量のデータが読み取られ、集計される、データ ウェアハウス シナリオで非常に効率的となります。

## <a name="sql-statement-processing"></a>SQL ステートメントの処理
単一の [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの処理は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] で [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを実行する最も基本的な方法です。 ローカルのベース テーブルだけを参照する (ビューやリモート テーブルは参照しない) 単一の `SELECT` ステートメントを処理する手順が、この基本的な処理の良い例です。

### <a name="logical-operator-precedence"></a>論理演算子の優先順位
1 つのステートメントで複数の論理演算子を使用すると、最初に `NOT` が評価され、次に `AND`、最後に `OR` が評価されます。 算術演算子、およびビット演算子は論理演算子より前に処理されます。 詳細については、「[Operator Precedence (Transact-SQL)](../t-sql/language-elements/operator-precedence-transact-sql.md)」 (演算子の順位 (Transact-SQL)) を参照してください。

次の例では、色の条件が製品モデル 21 には該当しますが、製品モデル 20 には該当しません。これは、`AND` が `OR` よりも優先されるためです。

```sql
SELECT ProductID, ProductModelID
FROM Production.Product
WHERE ProductModelID = 20 OR ProductModelID = 21
  AND Color = 'Red';
GO
```

`OR` が必ず最初に評価されるように、かっこを付け加えることでクエリの意味を変えることができます。 次のクエリでは、モデル 20 とモデル 21 で赤色の製品のみが検索されます。

```sql
SELECT ProductID, ProductModelID
FROM Production.Product
WHERE (ProductModelID = 20 OR ProductModelID = 21)
  AND Color = 'Red';
GO
```

必要でない場合でもかっこを使用すると、クエリが読みやすくなり、演算子の優先順位が原因の微妙な間違いを犯す可能性が減少します。 かっこを使用することでパフォーマンスが大幅に低下することはありません。 次の例は、元の例と構文は同じですが、元の例よりも読みやすくなっています。

```sql
SELECT ProductID, ProductModelID
FROM Production.Product
WHERE ProductModelID = 20 OR (ProductModelID = 21
  AND Color = 'Red');
GO
```

### <a name="optimizing-select-statements"></a>SELECT ステートメントの最適化
`SELECT` ステートメントは非手続き型であり、要求したデータを取得するときにデータベース サーバーで使用する手順が細かく指定されません。 つまり、データベース サーバーが SELECT ステートメントを分析して、要求したデータを抽出する最も効率的な方法を決定する必要があります。 これを、 `SELECT` ステートメントの最適化と呼びます。 また、最適化を行うコンポーネントをクエリ オプティマイザーと呼びます。 クエリ オプティマイザーへの入力は、クエリ、データベース スキーマ (テーブル定義やインデックスの定義)、およびデータベース統計で構成されます。 クエリ オプティマイザーの出力がクエリ実行プランです。これは、クエリ プランや単にプランと呼ばれることもあります。 クエリ プランの内容については、このトピックの後半で説明します。

単一の `SELECT` ステートメントを最適化する場合のクエリ オプティマイザーの入出力は、次の図のようになります。

![query_processor_io](../relational-databases/media/query-processor-io.gif)

`SELECT` ステートメントは次の事項だけを定義します。  
* 結果セットの形式。 ほとんどの場合、選択リスト内で指定します。 ただし、 `ORDER BY` や `GROUP BY` などの句も結果セットの最終形式に影響します。
* 取得するデータが含まれているテーブル。 これは `FROM` 句で指定します。
* `SELECT` ステートメントを実行するためにテーブルを論理的に関連付ける方法。 `WHERE` の後に指定する `ON` 句や `FROM`句などで指定する結合により定義します。
* 基になるテーブルの行が `SELECT` ステートメントの対象になるために満たす必要がある条件。 `WHERE` 句と `HAVING` 句で指定します。

クエリ実行プランは、次の事項を定義しています。 

* 基になるテーブルにアクセスする順序  
  通常、データベース サーバーからベース テーブルにアクセスして結果セットを構築する順序は何とおりもあります。 たとえば、 `SELECT` ステートメントが 3 つのテーブルを参照している場合、データベース サーバーは最初に `TableA`にアクセスし、 `TableA` のデータを使用して `TableB`から一致する行を抽出します。次に、 `TableB` のデータを使用して `TableC`のデータを抽出することができます。 データベースがテーブルにアクセスする際に可能な順序には、次の組み合わせがあります。  
  `TableC`、 `TableB`、 `TableA`、または  
  `TableB`、 `TableA`、 `TableC`、または  
  `TableB`、 `TableC`、 `TableA`、または  
  `TableC`、`TableA`、`TableB`  

* 各テーブルからデータを取り出す方法  
  通常、各テーブルのデータにアクセスする方法にも何とおりかあります。 特定のキー値を持つ数行だけが必要な場合、データベース サーバーではインデックスを使用できます。 テーブル内のすべての行が必要な場合は、インデックスを無視してテーブル スキャンを実行できます。 テーブル内のすべての行が必要で、 `ORDER BY`で指定されたキー列のインデックスがある場合、テーブル スキャンではなくインデックス スキャンを行うと、結果セットの並べ替えを個別に行わずに済みます。 テーブルが非常に小さい場合は、テーブルにどのようにアクセスするときでもテーブル スキャンが最も効率的な方法です。

可能性のある多数のプラン候補の中から実行プランを 1 つ選択する処理を最適化と呼びます。 クエリ オプティマイザーは、SQL データベース システムで最も重要なコンポーネントの 1 つです。 クエリ オプティマイザーはクエリの分析やプランの選択を行うため、オーバーヘッドが発生します。ただし、クエリ オプティマイザーが効率的な実行プランを選択すれば、このオーバーヘッドの数倍の負荷を削減することができます。 たとえば、2 つの建築会社が一軒の住宅に同じ青写真を提供する場合について考えてみます。 一方の会社は数日かけて建築プランを立て、他方の会社はプランを立てずに建築を開始するとします。ほとんどの場合、プロジェクトのプランに時間をかけた会社の方が先に完成します。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クエリ オプティマイザーは、コストベースのオプティマイザーです。 実行プラン候補ごとに、計算に使用するリソースの量の観点から関連するコストが異なります。 クエリ オプティマイザーでは、候補のプランを分析し、算出コストが最も低いプランを選択する必要があります。 複雑な `SELECT` ステートメントの場合、何千もの実行プラン候補があります。 このような場合、クエリ オプティマイザーはすべての組み合わせを分析するわけではありません。 複雑なアルゴリズムを使用して、理論上の最低コストに最も近い実行プランを迅速に見つけ出します。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クエリ オプティマイザーは、リソース コストが最も低い実行プランに限定して選択するわけではありません。妥当なリソース コストで、最も迅速に結果を返すプランを選択します。 たとえば、クエリを並列に処理すれば、直列に処理するよりもリソースを多く使用します。ただし、クエリの完了時間は短縮されます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クエリ オプティマイザーは、サーバー側の負荷に悪影響がない限り、並列実行プランを使用して結果を返します。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クエリ オプティマイザーは、テーブルやインデックスから情報を取り出す複数の方法のリソース コストを算出する場合、分布統計に大きく依存します。 列とインデックスに対する分布統計が保持されます。この分布統計では、基になるデータの密度 <sup>1</sup> に関する情報が保持されます。 これは、特定のインデックスまたは列内の値の選択度を表すために使用されます。 たとえば、車を表すテーブルの場合、同メーカーの車がいくつもあります。ただし、VIN (車両番号) はそれぞれの車両固有のものです。 VIN 上のインデックスは、製造元でのインデックスより選択度が高くなります。これは VIN の密度が製造元の場合より低いからです。 インデックス統計が最新でない場合、クエリ オプティマイザーはテーブルの現在の状態に対して最適な選択ができないことがあります。 密度の詳細については、「[統計](../relational-databases/statistics/statistics.md#density)」を参照してください。 

<sup>1</sup>密度では、データ内に存在する一意の値の分布、または特定の列における重複値の平均数が定義されます。 密度が減少するにつれて、値の選択度が高くなります。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クエリ オプティマイザーを使用すると、プログラマやデータベース管理者が入力しなくても、データベース内の状態の変化に合わせてデータベース サーバーを動的に調整できるので、クエリ オプティマイザーは不可欠です。 これにより、プログラマはクエリの最終結果の記述だけに重点を置くことができます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クエリ オプティマイザーは、ステートメントを実行するたびに、データベースの状態に合わせて効率的な実行プランを構築します。

### <a name="processing-a-select-statement"></a>SELECT ステートメントの処理
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] が単一の SELECT ステートメントを処理する基本的な手順は次のとおりです。 

1. パーサーが `SELECT` ステートメントをスキャンし、キーワード、式、演算子、識別子などの論理単位に分解します。
2. 基になるデータを結果セットで必要な形式に変換する論理手順を記述するクエリ ツリーが構築されます。クエリ ツリーはシーケンス ツリーとも呼ばれます。
3. クエリ オプティマイザーでは、基になるテーブルにアクセスできるさまざまな方法が分析されます。 その中から、使用するリソースが最も少なく、最も短時間で結果を返す一連の手順が選択されます。 クエリ ツリーが更新され、この一連の手順が正確に記録されます。 この最終的に得られた最適化済みのクエリ ツリーを実行プランと呼びます。
4. リレーショナル エンジンによって、実行プランの実行が開始されます。 リレーショナル エンジンは、ベース テーブルからのデータを必要とする手順を処理するときに、要求した行セットのデータを渡すようにストレージ エンジンに要求します。
5. リレーショナル エンジンでは、ストレージ エンジンから返されたデータが結果セット用に定義された形式に変換され、結果セットをクライアントに返します。

### <a name="ConstantFolding"></a> 定数のたたみ込みと式の評価 
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ではクエリのパフォーマンスを向上するために、いくつかの定数式を前もって評価します。 これを定数のたたみ込みと呼びます。 定数は、3、'ABC'、'2005-12-31'、1.0e3、0x12345678 のような [!INCLUDE[tsql](../includes/tsql-md.md)] リテラルです。

#### <a name="foldable-expressions"></a>たたみ込み可能な式
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、次の種類の式に定数のたたみ込みを適用します。
- 定数のみから構成される数式 (1+1、5/3*2 など)。
- 定数のみから構成される論理式 (1=1、1>2 AND 3>4 など)。
- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] によってたたみ込み可能と判断された組み込み関数 (`CAST`、`CONVERT` など)。 固有の関数は、通常はたたみ込み可能です。ただし結果が関数への入力のみによって決まらず、SET オプション、言語設定、データベース オプション、暗号化キーなどの、状況によって変わりうる他の情報を交えて決まる場合は例外です。 非決定的関数はたたみ込み不可能です。 組み込みの決定的関数はたたみ込み可能ですが、一部例外があります。

> [!NOTE] 
> 例外の 1 つは LOB 型です。 たたみ込み処理の出力が LOB 型 (text、image、nvarchar(max)、varchar(max)、または varbinary(max) のいずれか) である場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では式はたたみ込まれません。

#### <a name="nonfoldable-expressions"></a>たたみ込み不可能な式
その他の種類の式は、すべてたたみ込み不可能です。 具体的には、次に示す種類の式です。
- 定数ではない式 (結果が列の値によって変わる式など)。
- 結果がローカル変数またはパラメーター (@x など) によって変わる式。
- 非決定的関数。
- ユーザー定義関数 ([!INCLUDE[tsql](../includes/tsql-md.md)] および CLR)
- 結果が言語設定によって変わる式。
- 結果が SET オプションによって変わる式。
- 結果がサーバー構成オプションによって変わる式。

#### <a name="examples-of-foldable-and-nonfoldable-constant-expressions"></a>たたみ込み可能/不可能な定数式の例
次のクエリを考えてみます。

```sql
SELECT *
FROM Sales.SalesOrderHeader AS s 
INNER JOIN Sales.SalesOrderDetail AS d 
ON s.SalesOrderID = d.SalesOrderID
WHERE TotalDue > 117.00 + 1000.00;
```

このクエリの `PARAMETERIZATION` データベース オプションが `FORCED` に設定されていない場合、クエリをコンパイルする前に式 `117.00 + 1000.00` が評価され、その結果である `1117.00` に置き換えられます。 定数のたたみ込みには、次に示す利点があります。
- 実行時に式を繰り返し評価する必要がありません。
- クエリ `TotalDue > 117.00 + 1000.00` の部分の結果セットのサイズをクエリ オプティマイザーで推定するときは、評価後の式の値が使用されます。

一方、ユーザー定義関数を含んだ式は決定的関数であってもたたみ込まれないので、`dbo.f` をスカラー値のユーザー定義関数とした場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、式 `dbo.f(100)` はたたみ込まれません。 パラメーター化の詳細については、この記事で後述する「[強制パラメーター化](#ForcedParam)」を参照してください。

#### <a name="ExpressionEval"></a>式の評価 
また、定数のたたみ込みは行われませんが、引数がコンパイル時に確定する式は、引数がパラメーターと定数のどちらでも、最適化のときにクエリ オプティマイザーのカーディナリティ (結果セットのサイズ) 推定機能によって評価されます。

具体的には、次の組み込み関数と特殊演算子は、入力がすべて確定する場合コンパイル時に評価されます: `UPPER`、`LOWER`、`RTRIM`、`DATEPART( YY only )`、`GETDATE`、`CAST`、`CONVERT`。 次に示す演算子も、入力がすべて確定する場合コンパイル時に評価されます。
- 算術演算子 : +、-、\*、/、単項演算子の -
- 論理演算子: `AND`、`OR`、`NOT`
- 比較演算子: <、>、<=、>=、<>、`LIKE`、`IS NULL`、`IS NOT NULL`

上記以外の関数および演算子は、カーディナリティを推定するときにはクエリ オプティマイザーによって評価されません。

#### <a name="examples-of-compile-time-expression-evaluation"></a>コンパイル時の式の評価の例
次のストアド プロシージャについて考えてみましょう。

```sql
USE AdventureWorks2014;
GO
CREATE PROCEDURE MyProc( @d datetime )
AS
SELECT COUNT(*)
FROM Sales.SalesOrderHeader
WHERE OrderDate > @d+1;
```

このストアド プロシージャの `SELECT` ステートメントを最適化するとき、条件 `OrderDate > @d+1` に対する結果セットの予測カーディナリティがクエリ オプティマイザーによって評価されます。 式 `@d+1` は `@d` がパラメーターであるために定数がたたみ込まれません。 しかし、最適化のときにはパラメーターの値が確定しています。 したがって結果セットのサイズがクエリ オプティマイザーによって正確に推定できるので、適切なクエリ プランが選択されます。

次は、上記のクエリの `@d2` をローカル変数 `@d+1` に置き換え、クエリではなく SET ステートメントで式を評価するストアド プロシージャの例を考えてみます。

```sql 
USE AdventureWorks2014;
GO
CREATE PROCEDURE MyProc2( @d datetime )
AS
BEGIN
DECLARE @d2 datetime
SET @d2 = @d+1
SELECT COUNT(*)
FROM Sales.SalesOrderHeader
WHERE OrderDate > @d2
END;
```

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] で *MyProc2* の `SELECT` ステートメントを最適化するとき、`@d2` の値は確定していません。 そのため、クエリ オプティマイザーでは `OrderDate > @d2` の選択度に対して既定の推定が使用されます (この場合は 30%)。

### <a name="processing-other-statements"></a>その他のステートメントの処理
`SELECT` ステートメントの処理で説明した基本的な手順は、[!INCLUDE[tsql](../includes/tsql-md.md)]、`INSERT`、`UPDATE` などの `DELETE` ステートメントにも適用されます。 `UPDATE` ステートメントと `DELETE` ステートメントは、いずれも変更または削除する行セットを対象とする必要があります。 これらの行を特定する処理は、 `SELECT` ステートメントの結果セットを得るために使用された、基になる行を特定する処理と同じです。 `UPDATE` ステートメントと `INSERT` ステートメントのどちらにも、更新または挿入するデータ値を指定する `SELECT` ステートメントを埋め込むことができます。

`CREATE PROCEDURE` または `ALTER TABLE` などの DDL (データ定義言語) ステートメントも、最終的には、システム カタログ テーブル上の一連のリレーショナル操作になります。また、場合によっては `ALTER TABLE ADD COLUMN` など、データ テーブルに対する一連のリレーショナル操作になります。

### <a name="worktables"></a>作業テーブル
リレーショナル エンジンでは、[!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントで指定された論理操作を行う際に、作業テーブルの作成を必要とする場合があります。 作業テーブルとは、中間結果を格納するための内部テーブルです。 作業テーブルは、特定の `GROUP BY`クエリ、 `ORDER BY`クエリ、 `UNION` クエリで生成されます。 たとえば、インデックスの対象になっていない列を `ORDER BY` 句が参照している場合、要求された順番に結果セットを並べ替えるための作業テーブルが生成されることがあります。 また、クエリ プランの一部を実行した結果を一時的に格納するためのスプールとして作業テーブルが使用されることもあります。 作業テーブルは tempdb に作成され、不要になると自動的に削除されます。

### <a name="view-resolution"></a>ビューの解決
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クエリ プロセッサでは、インデックス付きビューとインデックスなしのビューの処理方法が異なります。 

* インデックス付きビューの行は、テーブルと同じ形式でデータベースに格納されます。 クエリ オプティマイザーでクエリ プランにインデックス付きビューを使用することが決定されると、インデックス付きビューはベース テーブルと同じ方法で処理されます。
* インデックスなしのビューでは、ビューの行ではなく、定義のみが格納されます。 クエリ オプティマイザーにより、ロジックがビューの定義から、インデックスなしのビューを参照する [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントに対して作成された実行プランに組み込まれます。 

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のクエリ オプティマイザーでは、いつインデックス付きビューを使用するかを決定するときに、テーブルのインデックスをいつ使用するかを決定するのとよく似たロジックが使用されます。 インデックス付きビューに含まれるデータが [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの一部またはすべてを対象としており、クエリ オプティマイザーによってビュー上のインデックスが低コストのアクセス パスであると判断された場合、クエリ内でビューが名前で参照されるかどうかにかかわらず、クエリ オプティマイザーではインデックスが選択されます。

[!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントからインデックスなしのビューが参照されるときは、パーサーとクエリ オプティマイザーで [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントとビューのソースが両方分析され、それらが 1 つの実行プランに解決されます。 [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの実行プランとビューの実行プランに別々に解決されるわけではありません。

たとえば、次のビューがあるとします。

```sql
USE AdventureWorks2014;
GO
CREATE VIEW EmployeeName AS
SELECT h.BusinessEntityID, p.LastName, p.FirstName
FROM HumanResources.Employee AS h 
JOIN Person.Person AS p
ON h.BusinessEntityID = p.BusinessEntityID;
GO
```

次の 2 つの [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントはどちらも、このビューに基づいてベース テーブルに同じ操作を行い、同じ結果を生成します。

```sql
/* SELECT referencing the EmployeeName view. */
SELECT LastName AS EmployeeLastName, SalesOrderID, OrderDate
FROM AdventureWorks2014.Sales.SalesOrderHeader AS soh
JOIN AdventureWorks2014.dbo.EmployeeName AS EmpN
ON (soh.SalesPersonID = EmpN.BusinessEntityID)
WHERE OrderDate > '20020531';

/* SELECT referencing the Person and Employee tables directly. */
SELECT LastName AS EmployeeLastName, SalesOrderID, OrderDate
FROM AdventureWorks2014.HumanResources.Employee AS e 
JOIN AdventureWorks2014.Sales.SalesOrderHeader AS soh
ON soh.SalesPersonID = e.BusinessEntityID
JOIN AdventureWorks2014.Person.Person AS p
ON e.BusinessEntityID =p.BusinessEntityID
WHERE OrderDate > '20020531';
```

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Studio のプラン表示機能では、リレーショナル エンジンがこの 2 つの `SELECT` ステートメントのどちらに対しても同じ実行プランを構築することが示されます。

### <a name="using-hints-with-views"></a>ビューでのヒントの使用
クエリのビューに設定されるヒントは、ベース テーブルにアクセスするためにビューを展開するときに検出される他のヒントと競合することがあります。 この競合が発生すると、クエリはエラーを返します。 たとえば、定義にテーブル ヒントが含まれている、次のビューについて考えてみます。

```sql
USE AdventureWorks2014;
GO
CREATE VIEW Person.AddrState WITH SCHEMABINDING AS
SELECT a.AddressID, a.AddressLine1, 
    s.StateProvinceCode, s.CountryRegionCode
FROM Person.Address a WITH (NOLOCK), Person.StateProvince s
WHERE a.StateProvinceID = s.StateProvinceID;
```

ここで次のクエリを入力したとします。

```sql
SELECT AddressID, AddressLine1, StateProvinceCode, CountryRegionCode
FROM Person.AddrState WITH (SERIALIZABLE)
WHERE StateProvinceCode = 'WA';
```

このクエリは失敗します。その理由として、ビューが展開されるときに、クエリ内の `SERIALIZABLE` ビューに適用される `Person.AddrState` ヒントが、ビューの `Person.Address` テーブルと `Person.StateProvince` テーブルの両方に反映されます。 しかし、ビューを展開することで、 `NOLOCK` の `Person.Address`ヒントも公開されます。 その結果、 `SERIALIZABLE` ヒントと `NOLOCK` ヒントが競合するので、クエリ結果は正しくありません。 

`PAGLOCK`、 `NOLOCK`、 `ROWLOCK`、 `TABLOCK`、 `TABLOCKX` の各テーブル ヒントが競合するのと同様に、 `HOLDLOCK`、 `NOLOCK`、 `READCOMMITTED`、 `REPEATABLEREAD`、 `SERIALIZABLE` の各テーブル ヒントも互いに競合します。

ヒントは、入れ子になったビュー全体に反映されます。 たとえば、クエリでビュー `HOLDLOCK` に `v1`ヒントが適用されるとします。 `v1` を展開すると、ビュー `v2` がその定義の一部であることがわかります。 `v2`の定義では、ベース テーブルの 1 つに `NOLOCK` ヒントが含まれています。 しかし、このテーブルはビュー `HOLDLOCK` のクエリから `v1`ヒントも継承します。 その結果、 `NOLOCK` ヒントと `HOLDLOCK` ヒントが競合するので、クエリが失敗します。

ビューが含まれるクエリで `FORCE ORDER` ヒントを使用すると、ビュー内のテーブルの結合順序は、順序付けられた構造内のビューの位置によって決まります。 たとえば、次のクエリは 3 つのテーブルとビューから選択を行います。

```sql
SELECT * FROM Table1, Table2, View1, Table3
WHERE Table1.Col1 = Table2.Col1 
    AND Table2.Col1 = View1.Col1
    AND View1.Col2 = Table3.Col2;
OPTION (FORCE ORDER);
```

さらに、次に示すように `View1` が定義されています。

```sql
CREATE VIEW View1 AS
SELECT Colx, Coly FROM TableA, TableB
WHERE TableA.ColZ = TableB.Colz;
```

クエリ プランでの結合順序は、 `Table1`、 `Table2`、 `TableA`、 `TableB`、 `Table3`の順になります。

### <a name="resolving-indexes-on-views"></a>ビューのインデックスの解決

インデックス付きビューは他のインデックスと同様、使用することにメリットがあるとクエリ オプティマイザーで判断された場合にのみ、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] でクエリ プランに使用されます。

インデックス付きビューは [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のどのエディションでも作成できます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のバージョンとエディションによっては、クエリ オプティマイザーにより自動的にインデックス付きビューが考慮されます。 その他のバージョンやエディションの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、インデックス付きビューを使用するには `NOEXPAND` テーブル ヒントを使用する必要があります。 詳細については、各バージョンのドキュメントを参照してください。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クエリ オプティマイザーは、次の条件が満たされている場合にインデックス付きビューを使用します。 

* 次のセッション オプションが `ON`である。 
  * `ANSI_NULLS`
  * `ANSI_PADDING`
  * `ANSI_WARNINGS`
  * `ARITHABORT`
  * `CONCAT_NULL_YIELDS_NULL`
  * `QUOTED_IDENTIFIER` 
  * `NUMERIC_ROUNDABORT` セッション オプションは OFF に設定します。
* クエリ オプティマイザーにより、ビューのインデックス列とクエリ要素との間で、次のような項目の一致が検出される。 
  * WHERE 句の検索条件の述語
  * 結合操作
  * 集計関数
  * `GROUP BY` 句
  * テーブル参照
* クエリ オプティマイザーが検討したアクセス方法の中で、インデックスを使用した場合の推定コストが最小である。 
* クエリ内で (直接、またはビューを展開して基になるテーブルにアクセスすることにより) 参照しているテーブルのうち、インデックス付きビュー内のテーブル参照に対応しているすべてのテーブルについて、クエリ内で適用されているヒントの組み合わせが同じである。

> [!NOTE] 
> 現在のトランザクション分離レベルにかかわらず、このコンテキストでは `READCOMMITTED` ヒントと `READCOMMITTEDLOCK` ヒントは常に異なるヒントと見なされます。
 
`SET` オプションおよびテーブル ヒントの要件を除くと、上記の条件は、テーブル インデックスがクエリをカバーするかどうかを判断するためにクエリ オプティマイザーにより使用されるルールと同じです。 クエリで他に何も指定しなくてもインデックス付きビューを使用できます。

クエリの `FROM` 句でインデックス付きビューを明示的に参照しなくても、インデックス付きビューが使用されます。 ベース テーブル内の列に対する参照がクエリに含まれており、その参照がインデックス付きビューにも存在する場合、クエリ オプティマイザーは、インデックス付きビューの使用によりアクセス コストを最小にできると推定できれば、インデックス付きビューを選択します。これはクエリ オプティマイザーが、ベース テーブルのインデックスを、クエリ内で直接参照されていない場合に選択するのと同じ手法です。 クエリ内で指定されている 1 つ以上の列をカバーするオプションとして最もコストが低ければ、クエリで参照されていない列がビューに含まれていても、クエリ オプティマイザーがそのビューを選択することがあります。

クエリ オプティマイザーは `FROM` 句で参照されているインデックス付きビューを標準のビューとして扱います。 最適化処理の開始時には、ビューの定義をクエリにまで拡張します。 そのうえで、インデックス付きビューの照合を実行します。 クエリ オプティマイザーが選択した最終的な実行プランでは、インデックス付きビューが使用されることも、ビューが参照するベース テーブルにアクセスすることにより、ビュー内の必要なデータが具体化されることもあります。 いずれにしても、最もコストが低いプランが選択されます。

#### <a name="using-hints-with-indexed-views"></a>インデックス付きビューでのヒントの使用

`EXPAND VIEWS` クエリ ヒントを指定すると、ビューのインデックスがクエリで使用されるのを禁止できます。 `NOEXPAND` テーブル ヒントを指定すると、クエリの `FROM` 句で指定したインデックス付きビューのインデックスを強制的に使用することができます。 ただし、各クエリを使用するための最適なアクセス方法はクエリ オプティマイザーによる動的な判断に任せることをお勧めします。 `EXPAND` および `NOEXPAND` を使用するのは、テストで結果パフォーマンスの大幅な向上が示された場合のみにしてください。

`EXPAND VIEWS` オプションは、クエリ オプティマイザーに対し、クエリ全体に関してビュー インデックスを使用しないことを指定します。 

`NOEXPAND` をビューに対して指定した場合、ビューに定義されたインデックスを使用することがクエリ オプティマイザーにより検討されます。 `NOEXPAND` をオプションの `INDEX()` 句で指定すると、クエリ オプティマイザーの判断で指定されたインデックスが強制的に使用されます。 `NOEXPAND` を指定できるのはインデックス付きビューに対してのみであり、インデックスのないビューには指定できません。

ビューを含んだクエリで `NOEXPAND` と `EXPAND VIEWS` のいずれも指定しない場合、基になるテーブルにアクセスするためにビューが拡張されます。 ビューを構成するクエリにテーブル ヒントが含まれている場合、基になるテーブルにヒントが反映されます (この処理の詳細については、「ビューの解決」を参照してください)。ビューの基になるテーブルに存在するヒントのセットがテーブル間で同一であれば、クエリはインデックス付きビューと一致する可能性があります。 ほとんどの場合、ヒントはビューから直接継承されるので双方のヒントは一致します。 ただし、クエリの参照先がビューではなくテーブルであり、参照先テーブルに直接適用されているヒントがテーブルによって異なる場合、そのようなクエリはインデックス付きビューと一致しません。 ビューの展開後、 `INDEX`、 `PAGLOCK`、 `ROWLOCK`、 `TABLOCKX`、 `UPDLOCK`、 `XLOCK` のいずれかのヒントがクエリの参照先テーブルに適用される場合、クエリはインデックス付きビューと一致しません。

`INDEX (index_val[ ,...n] )` という形式のテーブル ヒントでクエリ内のビューを参照しているときに、 `NOEXPAND` ヒントを指定しない場合、インデックス ヒントは無視されます。 特定のインデックスを使用するように指定するには `NOEXPAND` を使用します。 

通常、インデックス付きビューがクエリに一致すると、クエリ内のテーブルまたはビューに指定したヒントが直接インデックス付きビューに適用されます。 クエリ オプティマイザーがインデックス付きビューを使用しないと判断した場合、ヒントはすべて、ビュー内で参照しているテーブルに直接伝達されます。 詳細については、「ビューの解決」を参照してください。 この伝達は、結合ヒントには当てはまりません。 結合ヒントはクエリ内の元の場所でのみ適用されます。 クエリ オプティマイザーがクエリとインデックス付きビューを照合する際に、結合ヒントは無視されます。 結合ヒントを含むクエリの一部に一致したインデックス付きビューがクエリ プランで使用される場合、その結合ヒントはプランに使用されません。

インデックス付きビューの定義ではヒントが許可されていません。 互換性モードが 80 以上の場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] はインデックス付きビューの定義の保守時にも、インデックス付きビューを使用したクエリの実行時にも、定義に含まれているヒントを無視します。 互換性モード 80 では、インデックス付きビューの定義でヒントを使用しても構文エラーにはなりませんが、ヒントは無視されます。

### <a name="resolving-distributed-partitioned-views"></a>分散パーティション ビューの解決

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のクエリ プロセッサでは、分散パーティション ビューのパフォーマンスが最適化されます。 分散パーティション ビューのパフォーマンスで最も重要な点は、メンバー サーバー間で転送されるデータの量を最小限に抑えることです。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、リモート メンバー テーブルからのデータにアクセスするときに分散クエリを効率的に使用できる、高機能で動的なプランが構築されます。 

* クエリ プロセッサでは、最初に OLE DB を使用して、各メンバー テーブルから CHECK 制約の定義が取得されます。 これにより、クエリ プロセッサは、メンバー テーブル間でキー値の分布をマップできるようになります。
* クエリ プロセッサでは、[!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの `WHERE` 句で指定されたキーの範囲が、メンバー テーブルでの行の分布状況を示すマップと比較されます。 次に、クエリ プロセッサでは、分散クエリを使用して [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの完了に必要なリモート行だけを取得するクエリ実行プランが構築されます。 この実行プランでは、リモート メンバー テーブルのデータやメタデータへのアクセスが、情報が要求されるまで遅延されます。

たとえば、顧客テーブルが Server1 (`CustomerID` 1 ～ 3299999)、Server2 (`CustomerID` 3300000 ～ 6599999)、および Server3 (`CustomerID` 6600000 ～ 9999999) にパーティション分割されたシステムがあるとします。

Server1 で実行される次のクエリ用に構築される実行プランを考えてみます。

```sql
SELECT *
FROM CompanyData.dbo.Customers
WHERE CustomerID BETWEEN 3200000 AND 3400000;
```

このクエリの実行プランでは、ローカル メンバー テーブルから `CustomerID` のキー値が 3200000 ～ 3299999 の行が抽出され、分散クエリを実行して Server2 からキー値が 3300000 ～ 3400000 の行が取得されます。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のクエリ プロセッサでは、プランを構築する必要があるときにキー値がわからない [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメント用に、クエリの実行プランに動的なロジックを組み込むこともできます。 たとえば、次のようなストアド プロシージャがあるとします。

```sql
CREATE PROCEDURE GetCustomer @CustomerIDParameter INT
AS
SELECT *
FROM CompanyData.dbo.Customers
WHERE CustomerID = @CustomerIDParameter;
```

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、プロシージャが実行されるたびに `@CustomerIDParameter` パラメーターによって指定されるキー値を予測できません。 クエリ プロセッサはキー値を予測できないので、アクセスする必要のあるメンバー テーブルを予測することもできません。 この状況に対処するために、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、動的フィルターと呼ばれる条件ロジックを含む実行プランが構築され、アクセスされるメンバー テーブルが入力パラメーター値に基づいて制御されます。 `GetCustomer` ストアド プロシージャが Server1 で実行されたと仮定すると、実行プランのロジックは次のように表すことができます。

```sql
IF @CustomerIDParameter BETWEEN 1 and 3299999
   Retrieve row from local table CustomerData.dbo.Customer_33
ELSE IF @CustomerIDParameter BETWEEN 3300000 and 6599999
   Retrieve row from linked table Server2.CustomerData.dbo.Customer_66
ELSE IF @CustomerIDParameter BETWEEN 6600000 and 9999999
   Retrieve row from linked table Server3.CustomerData.dbo.Customer_99
```

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、パラメーター化されていないクエリに対してもこのような動的実行プランが構築されます。 クエリ オプティマイザーでは、クエリがパラメーター化され、実行プランを再利用できるようにします。 クエリ オプティマイザーがパーティション ビューを参照しているクエリをパラメーター化すると、必要な行が指定されたベース テーブルにあると仮定することができなくなります。 そのため、実行プランで動的フィルターを使用する必要があります。

## <a name="stored-procedure-and-trigger-execution"></a>ストアド プロシージャとトリガーの実行

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、ストアド プロシージャとトリガーのソースだけが格納されます。 ストアド プロシージャまたはトリガーを最初に実行するときに、ソースが実行プランにコンパイルされます。 時間が経過して実行プランがメモリから削除される前にストアド プロシージャまたはトリガーを再度実行すると、リレーショナル エンジンは既存の実行プランを検出してそれを再利用します。 時間が経過して実行プランがメモリから削除されると、新しい実行プランが構築されます。 これは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] がすべての [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントに行うのと同じ処理です。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] で、動的 [!INCLUDE[tsql](../includes/tsql-md.md)] のバッチと比較した場合の、ストアド プロシージャやトリガーのパフォーマンス上の主な利点は、[!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントが常に同じであることです。 したがって、リレーショナル エンジンを既存の実行プランに容易に適合させることができます。 その結果、ストアド プロシージャやトリガーのプランを簡単に再利用できます。

ストアド プロシージャとトリガーの実行プランは、ストアド プロシージャを呼び出すバッチやトリガーを起動するバッチの実行プランとは別に実行されます。 このため、ストアド プロシージャやトリガーの実行プランを何回でも再利用できます。

## <a name="execution-plan-caching-and-reuse"></a>実行プランのキャッシュと再利用

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] には、実行プランとデータ バッファーの両方を格納するためのメモリのプールが用意されています。 実行プランまたはデータ バッファーに割り当てられるプールの割合は、システムの状態によって動的に変動します。 実行プランの格納に使用されるメモリ プールの部分をプラン キャッシュといいます。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の実行プランは、主に次の要素から構成されます。 

- **クエリ実行プラン**     
  実行プランの大部分は、任意の数のユーザーが使用できる再入可能な読み取り専用のデータ構造体です。 これをクエリ プランといいます。 クエリ プランにはユーザー コンテキストは格納されません。 また、メモリに複数のクエリ プランのコピーが配置されることはありません。すべての直列実行に 1 つのコピーが使用され、すべての並列実行に 1 つのコピーが使用されます。 並列実行用コピーは、並列処理の次数に関係なくすべての並列実行に適用されます。 
- **実行コンテキスト**     
  クエリを現在実行しているユーザーごとに、パラメーター値など、実行に固有のデータを保持するデータ構造体が用意されています。 このデータ構造体を実行コンテキストといいます。 実行コンテキストのデータ構造体は再利用されます。 ユーザーがクエリを実行したときに使用されていない構造体が 1 つある場合、新しいユーザーのコンテキストでその構造体が再初期化されます。 

![execution_context](../relational-databases/media/execution-context.gif)

[!INCLUDE[tsql](../includes/tsql-md.md)] で任意の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ステートメントを実行すると、まずリレーショナル エンジンにより、プラン キャッシュが調査され、同じ [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの既存の実行プランが存在するかどうかが確認されます。 [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントは、キャッシュされたプランで前に実行された [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントと文字単位で一致する場合、既存と見なされます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、既存のプランが見つかった場合にはそれが再利用され、[!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを再びコンパイルするオーバーヘッドが削減されます。 既存の実行プランが存在しない場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] によってクエリの新しい実行プランが生成されます。

> [!NOTE]
> [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの中にはキャッシュされないものもあります。たとえば、行ストア上で実行される一括操作ステートメントや 8 KB より大きい文字列リテラルを含むステートメントなどです。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] には、特定の [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの既存の実行プランを検索する効率的なアルゴリズムが用意されています。 ほとんどのシステムでは、このスキャンで使用される最低限のリソースの量が、すべての [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントをコンパイルせずに既存の実行プランを再利用することで節約できるリソースの量を超えることはありません。

新しい [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントをキャッシュ内の使用されていない既存の実行プランと照合するアルゴリズムでは、すべてのオブジェクト参照が完全に修飾されている必要があります。 たとえば、`Person` は下の `SELECT` ステートメント実行するユーザーに対する既定のスキーマであるものとします。 この例では、実行するために `Person` テーブルが完全修飾されている必要はありませんが、これは、2 番目のステートメントは既存のプランと一致しないのに対し、3 番目は一致することを意味します。

```sql
SELECT * FROM Person;
GO
SELECT * FROM Person.Person;
GO
SELECT * FROM Person.Person;
GO
```

### <a name="removing-execution-plans-from-the-plan-cache"></a>プラン キャッシュからの実行プランの削除

実行プランは、格納しておくためのメモリがある間はプラン キャッシュに残ります。 メモリ負荷が存在する場合、[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]はコストベースの手法を使用して、どの実行プランをプラン キャッシュから削除するかを判断します。 コストベースの判断をするために、[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]は各実行プランの現在のコスト変数を以下のような要因に基づいて増減させます。

ユーザー プロセスは、キャッシュに実行プランを挿入するときに、現在のコストを元のクエリ コンパイル コストと同じ値に設定します。アドホック実行プランの場合、ユーザー プロセスは現在のコストをゼロに設定します。 これ以降、ユーザー プロセスは、実行プランを参照するたびに、現在のコストを元のコンパイル コストにリセットします。アドホック実行プランの場合、ユーザー プロセスは現在のコストを増加させます。 すべてのプランについて、現在のコストの最大値は元のコンパイル コストです。

メモリ負荷が存在する場合、[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]は実行プランをプラン キャッシュから削除することによって対応します。 どのプランを削除するかを決めるために、[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]は実行プランの状態を繰り返し検証して、現在のコストがゼロであるプランを削除します。 現在のコストがゼロである実行プランは、メモリ負荷がある場合でも、自動的には削除されません。削除されるのは、[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]がプランを検証し、現在のコストがゼロになっている場合だけです。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]が実行プランを検証するとき、クエリがそのプランを現在使用していない場合は、現在のコストが減少し、ゼロに近づきます。

[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]は、メモリ要件を満たすために必要な数の実行プランが削除されるまで、実行プランの検証を繰り返します。 メモリ負荷が存在する場合、実行プランのコストは数回にわたって増減することになります。 メモリ負荷が存在しなくなると、[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]は使用されていない実行プランの現在のコストを減らさなくなり、コストがゼロの実行プランもプラン キャッシュに残されます。

[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]はリソース モニターとユーザー ワーカー スレッドを使用して、メモリ負荷に応じてプラン キャッシュからメモリを解放します。 リソース モニターとユーザー ワーカー スレッドは、使用されていない各実行プランの現在のコストを減らすために、プランを同時に実行して検証することができます。 リソース モニターは、グローバルなメモリ負荷が存在する場合に、実行プランをプラン キャッシュから削除します。 リソース モニターはメモリを解放することによって、システム メモリ、プロセス メモリ、リソース プール メモリ、およびすべてのキャッシュの最大サイズのポリシーを強制的に適用します。 

すべてのキャッシュの最大サイズは、バッファー プール サイズの関数で、最大サーバー メモリを超えることはできません。 最大サーバー メモリの構成の詳細については、「 `max server memory` 」の `sp_configure`設定を参照してください。 

ユーザー ワーカー スレッドは、単一キャッシュ メモリ負荷が存在する場合に、実行プランをプラン キャッシュから削除します。 単一キャッシュの最大サイズおよび最大エントリのポリシーを強制的に適用します。 

次の例では、どの実行プランがプラン キャッシュから削除されるかを示しています。

* 実行プランは頻繁に参照されるため、そのコストがゼロになることはありません。 メモリ負荷が存在せず、現在のコストがゼロでない場合、実行プランはプラン キャッシュに残り、削除されません。
* アドホック実行プランは挿入され、メモリ負荷が生じるまでは再度参照されることはありません。 アドホック実行プランは、現在のコストがゼロで初期化されます。そのため、[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]は実行プランを検証するときに現在のコストがゼロであると認識し、プラン キャッシュから実行プランを削除します。 メモリ負荷が存在しない場合、アドホック実行プランは、現在のコストがゼロでプラン キャッシュに残ります。

キャッシュから 1 つまたはすべてのプランを手動で削除するには、 [DBCC FREEPROCCACHE](../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)を使用します。 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 以降は、`ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE` を使用してスコープ内のデータベースのプロシージャ (プラン) キャッシュをクリアします。

### <a name="recompiling-execution-plans"></a>実行プランの再コンパイル

データベースに変更を加えた場合、データベースの新しい状態によっては、実行プランの効率が低下したり、実行プランが無効になったりします。 実行プランが無効になるような変更は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] によって検出され、その実行プランは無効としてマークされます。 このため、クエリを実行する次回の接続用に新しい実行プランを再コンパイルする必要があります。 実行プランが無効になるのは、次の場合です。 

* クエリ (`ALTER TABLE` および `ALTER VIEW`) によって参照されるテーブルまたはビューに変更を加えた場合
* 単一のプロシージャに変更を加え、キャッシュからこのプロシージャの全プランを削除した場合 (`ALTER PROCEDURE`)
* 実行プランで使用されるインデックスに変更を加えた場合
* `UPDATE STATISTICS`などのステートメントを使用して明示的に生成した実行プラン、または自動的に生成された実行プランによって使用される統計を更新した場合
* 実行プランで使用されるインデックスを削除した場合
* `sp_recompile`を明示的に呼び出した場合
* クエリによって参照されるテーブルを変更する他のユーザーが、 `INSERT` ステートメントまたは `DELETE` ステートメントを使用して大量の変更をキーに加えた場合
* トリガーを含むテーブルで、inserted テーブルまたは deleted テーブルの行数が大幅に増加する場合
* `WITH RECOMPILE` オプションを使用してストアド プロシージャを実行する場合

主として再コンパイルが必要になるのは、ステートメントの正確性を維持したり、より処理速度が速いクエリ実行プランを取得したりする場合です。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]2005 より前のバージョンでは、バッチ内のステートメントが原因で再コンパイルが実行されるときに、そのバッチがストアド プロシージャ、トリガー、アドホック バッチ、または準備されたステートメントのいずれを使用して送信されたかどうかに関係なく、常にバッチ全体が再コンパイルされます。 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 以降では、再コンパイルをトリガーしたバッチ内のステートメントのみが再コンパイルされます。 また、[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 以降の再コンパイルには、拡張機能セットによって種類が追加されています。

ステートメントレベルの再コンパイルにより、パフォーマンスが向上します。これは、多くの場合、再コンパイルとそれに関連付けられた CPU 時間やロックへの悪影響を引き起こすステートメントの数が少ないからです。 したがって、再コンパイルする必要がないバッチの他のステートメントでは、これらの影響を回避できます。

`sql_statement_recompile` 拡張イベント (xEvent) によりステートメントレベルの再コンパイルが報告されます。 この xEvent は、ステートメントレベルの再コンパイルが何らかのバッチにより要求されるときに発生します。 ストアド プロシージャ、トリガー、アドホック バッチ、クエリなどが相当します。 バッチは、sp_executesql、動的 SQL、Prepare メソッド、Execute メソッドなど、いくつかのインターフェイスを使用して送信できます。
`sql_statement_recompile` xEvent の `recompile_cause` 列には、再コンパイルの理由を示す整数コードが含まれます。 考えられる理由をまとめたのが次の表です。

|||
|----|----|  
|スキーマの変更|統計の変更|  
|コンパイルの遅延|SET オプションの変更|  
|一時テーブルの変更|リモート行セットの変更|  
|`FOR BROWSE` アクセス許可の変更|クエリ通知環境の変更|  
|パーティション ビューの変更|カーソル オプションの変更|  
|`OPTION (RECOMPILE)` の要求|パラメーター化されたプランのフラッシュ|  
|プランに影響を与えるデータベース バージョンの変更|クエリ ストア プラン強制ポリシーの変更|  
|クエリ ストア プラン強制の失敗|クエリ ストアにプランがない|

> [!NOTE]
> xEvents が利用できない [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] バージョンの場合、ステートメントレベルの再コンパイルの報告という同じ目的に [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プロファイラー [SP:Recompile](../relational-databases/event-classes/sp-recompile-event-class.md) トレース イベントを利用できます。
> トレース イベント [SQL:StmtRecompile](../relational-databases/event-classes/sql-stmtrecompile-event-class.md) はまた、ステートメントレベルの再コンパイルを報告します。このトレース イベントを利用し、再コンパイルを追跡記録し、デバッグすることもできます。 SP:Recompile では、ストアド プロシージャとトリガーのみに対して値が生成されますが、`SQL:StmtRecompile` では、`sp_executesql`、準備されたクエリ、および動的 SQL を使用して実行されたストアド プロシージャ、トリガー、アドホック バッチ、およびバッチに対して値が生成されます。
> `SP:Recompile` と `SQL:StmtRecompile` の *EventSubClass* 列には、再コンパイルの理由を示す整数コードが含まれます。 コードの説明は[ここ](../relational-databases/event-classes/sql-stmtrecompile-event-class.md)にあります。

> [!NOTE]
> `AUTO_UPDATE_STATISTICS` データベース オプションが `ON` に設定されていると、対象にしているテーブルまたはインデックス付きビューの統計が更新された場合、または前回の実行から基数が大きく変更された場合、クエリが再コンパイルされます。 この動作は、標準のユーザー定義テーブル、一時テーブル、および DML トリガーによって作成された inserted テーブルと deleted テーブルに当てはまります。 過度の再コンパイルによってクエリのパフォーマンスが低下する場合は、この設定を `OFF`に変更することを検討してください。 `AUTO_UPDATE_STATISTICS` データベース オプションを `OFF` に設定すると、統計や基数の変更に基づく再コンパイルは行われません。ただし、DML `INSTEAD OF` トリガーで作成した inserted テーブルおよび deleted テーブルは例外です。 これらのテーブルは tempdb で作成されるため、それらにアクセスするクエリの再コンパイルは tempdb の `AUTO_UPDATE_STATISTICS` の設定によって異なります。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2005 より前のバージョンでは、この設定を `OFF` にした場合も、DML トリガーの inserted テーブルと deleted テーブルにタイする基数の変更に基づいて再コンパイルが引き続き行われます。

### <a name="PlanReuse"></a> パラメーターと実行プランの再利用

ADO、OLE DB、ODBC の各アプリケーションのパラメーター マーカーなどのパラメーターを使用すると、実行プランの再利用回数を増やすことができます。 

> [!WARNING] 
> エンド ユーザーが入力した値をパラメーターまたはパラメーター マーカーを使用して保持する方法は、文字列に値を連結し、その後この文字列をデータ アクセス API メソッド、 `EXECUTE` ステートメント、または `sp_executesql` ストアド プロシージャのいずれかを使用して実行する方法よりも安全です。
 
次の 2 つの `SELECT` ステートメントでは、 `WHERE` 句で比較する値のみが異なっています。

```sql
SELECT * 
FROM AdventureWorks2014.Production.Product 
WHERE ProductSubcategoryID = 1;
```

```sql
SELECT * 
FROM AdventureWorks2014.Production.Product 
WHERE ProductSubcategoryID = 4;
```

これらのクエリの実行プランでは、 `ProductSubcategoryID` 列に対して比較用に格納された値のみが異なります。 最終的な目標は、ステートメントが生成するプランは基本的に同じであると [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に常に認識させてプランを再利用することにありますが、[!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントが複雑になると [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] がこのことを検出できない場合があります。

パラメーターを使用して [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントと定数を切り離すと、同一のプランをリレーショナル エンジンが認識できるようになります。 パラメーターは、次の方法で使用できます。 

* [!INCLUDE[tsql](../includes/tsql-md.md)] では、`sp_executesql` を次のように使用します: 

   ```sql
   DECLARE @MyIntParm INT
   SET @MyIntParm = 1
   EXEC sp_executesql
     N'SELECT * 
     FROM AdventureWorks2014.Production.Product 
     WHERE ProductSubcategoryID = @Parm',
     N'@Parm INT',
     @MyIntParm
   ```

   この方法は、SQL ステートメントを動的に生成する [!INCLUDE[tsql](../includes/tsql-md.md)] スクリプト、ストアド プロシージャ、またはトリガーで使用することをお勧めします。 

* ADO、OLE DB、および ODBC ではパラメーター マーカーを使用します。 パラメーター マーカーは疑問符 (?) です。SQL ステートメント内の定数の代わりに置かれ、プログラム変数にバインドされます。 たとえば、ODBC アプリケーションでは次のような操作を実行できます。 

   * `SQLBindParameter` を使用して、整数変数を SQL ステートメントの最初のパラメーター マーカーにバインドします。
   * 変数に整数値を代入します。
   * 次のように、パラメーター マーカー (?) を指定してステートメントを実行します。 

   ```
   SQLExecDirect(hstmt, 
     "SELECT * 
     FROM AdventureWorks2014.Production.Product 
     WHERE ProductSubcategoryID = ?",
     SQL_NTS);
   ```

   アプリケーション内でパラメーター マーカーが使用されると、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に装備されている [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーと [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client ODBC ドライバーが `sp_executesql` を使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] にステートメントを送信します。 

* ストアド プロシージャをデザインする場合は、意図的にパラメーターを使用できます。

アプリケーションのデザインにパラメーターを明示的に組み込まない場合は、簡易パラメーター化の既定の動作を使用して、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クエリ オプティマイザーで自動的に特定のクエリをパラメーター化することもできます。 また、`ALTER DATABASE` ステートメントの `PARAMETERIZATION` オプションを `FORCED` に設定することで、クエリ オプティマイザーにデータベース内のすべてのクエリをパラメーター化するように強制できます。

強制パラメーター化が有効になっている場合でも、簡易パラメーター化が行われる可能性はあります。 たとえば、強制パラメーター化のルールに従えば、次のクエリはパラメーター化できません。

```sql
SELECT * FROM Person.Address
WHERE AddressID = 1 + 2;
```

ただし、簡易パラメーター化のルールに従ってパラメーター化することはできます。 強制パラメーター化の試行に失敗した場合でも、簡易パラメーター化が続けて試行されます。

### <a name="SimpleParam"></a> 簡易パラメーター化

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、Transact-SQL ステートメントでパラメーターまたはパラメーター マーカーを使用することで、新しい [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントと既存のコンパイル済みの実行プランとを照合するリレーショナル エンジンの機能が強化されています。

> [!WARNING] 
> パラメーターまたはパラメーター マーカーを使用してエンド ユーザーの入力値を保持する方法は、文字列に値を連結し、その後この文字列をデータ アクセス API メソッド、 `EXECUTE` ステートメント、または `sp_executesql` ストアド プロシージャのいずれかを使用して実行する方法よりも安全です。

パラメーターを指定せずに [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを実行した場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ではステートメントを内部でパラメーター化することにより、既存の実行プランとの照合機能が高められます。 この処理を簡易パラメーター化と呼びます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2005 より前のバージョンでは、この処理を自動パラメーター化と呼んでいました。

次のステートメントについて考えてみます。

```sql
SELECT * FROM AdventureWorks2014.Production.Product 
WHERE ProductSubcategoryID = 1;
```

ステートメントの最後の値 1 は、パラメーターとして指定できます。 リレーショナル エンジンにより、値 1 の位置にパラメーターが指定されたときと同様にこのバッチの実行プランが構築されます。 この簡易パラメーター化により、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] で次の 2 つのステートメントから基本的に同じ実行プランが生成されると認識され、2 番目のステートメントにも最初のプランが再利用されます。

```sql
SELECT * FROM AdventureWorks2014.Production.Product 
WHERE ProductSubcategoryID = 1;
```
```sql
SELECT * FROM AdventureWorks2014.Production.Product 
WHERE ProductSubcategoryID = 4;
```

複雑な [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを処理する場合、リレーショナル エンジンでは、どの式をパラメーター化できるのかを簡単に決定できないことがあります。 複雑な [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントと既存の使用されていない実行プランを照合するリレーショナル エンジンの機能を向上させるには、sp_executesql またはパラメーター マーカーを使用してパラメーターを明示的に指定します。 

> [!NOTE]
> +、-、\*、/、または % の算術演算子を使用して int、smallint、tinyint、または bigint の定数値を float、real、decimal、または numeric のデータ型に暗黙的にまたは明示的に変換した場合、その式の結果の型および有効桁数を計算するための特定の規則が [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] により適用されます。 ただし、これらの規則はクエリがパラメーター化されるかどうかによって異なります。 したがって、クエリ内の類似の式から異なる結果が生成される場合があります。

簡易パラメーター化の既定の動作では、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] により、比較的小さなクエリがパラメーター化されます。 ただし、いくつかの制約はありますが、 `PARAMETERIZATION` コマンドの `ALTER DATABASE` オプションを `FORCED`に設定することにより、データベース内のすべてのクエリをパラメーター化するように指定できます。 これにより、クエリをコンパイルする頻度が下がり、大量のクエリが同時に実行されるデータベースのパフォーマンスが向上します。

また、単一クエリと、単一クエリと構文的に等しくパラメーター値だけが異なるクエリをパラメーター化することを指定できます。 

### <a name="ForcedParam"></a> 強制パラメーター化

データベースのすべての `SELECT`、`INSERT`、`UPDATE`、`DELETE` ステートメントをパラメーター化するように指定することで、いくつかの制約はありますが [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の簡易パラメーター化の既定動作をオーバーライドできます。 強制パラメータ化を有効にするには、 `PARAMETERIZATION` ステートメントの `FORCED` オプションを `ALTER DATABASE` に設定します。 強制パラメーター化を行うと、クエリをコンパイルおよび再コンパイルする頻度を緩和できるので、データベースによってはパフォーマンスが向上します。 一般的に POS (point-of-sale) などのアプリケーションから大量のクエリが同時に実行されるデータベースは、強制パラメーター化によりパフォーマンスが向上します。

`PARAMETERIZATION` オプションを `FORCED`に設定すると、 `SELECT`、 `INSERT`、 `UPDATE`、 `DELETE` の各ステートメントに使用されているリテラル値は、その形式を問わずクエリのコンパイル時にパラメーターに変換されます。 ただし、次に示すクエリ構造に現れるリテラルは例外です。 

* `INSERT...EXECUTE` ステートメント。
* ストアド プロシージャ、トリガー、またはユーザー定義関数の本体内のステートメント。 これらのルーチンのクエリ プランは既に [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] により再利用されています。
* クライアント側のアプリケーションで既にパラメーター化されている、準備されたステートメント。
* XQuery メソッド呼び出しを含んでいるステートメントを、 `WHERE` 句など通常は引数がパラメーター化されるコンテキストで使用した場合。 引数がパラメーター化されないコンテキストでこのメソッドを使用した場合は、ステートメントの残りの部分がパラメーター化されます。
* [!INCLUDE[tsql](../includes/tsql-md.md)] カーソル内のステートメント (API カーソル内の`SELECT` ステートメントはパラメーター化されます)。
* 非推奨のクエリ構造。
* `ANSI_PADDING` または `ANSI_NULLS` が `OFF`に設定されている状態で実行されているステートメント。
* パラメーター化が可能なリテラルが 2,097 を超えるステートメント。
* `WHERE T.col2 >= @bb`など、変数を参照するステートメント。
* `RECOMPILE` クエリ ヒントを含んだステートメント。
* `COMPUTE` 句を含むステートメント。
* `WHERE CURRENT OF` 句を含むステートメント。

また、次のクエリ句はパラメーター化されません。 以下の場合については、パラメーター化されないのはこれらの句だけです。 同じクエリ内のその他の句では強制パラメーター化が可能な場合もあります。

* `SELECT` ステートメントの <select_list>。 これには、サブクエリの `SELECT` リストや `INSERT` ステートメント内の `SELECT` も含まれます。
* `SELECT` ステートメント内のサブクエリの `IF` ステートメント。
* クエリの `TOP`句、 `TABLESAMPLE`句、 `HAVING`句、 `GROUP BY`句、 `ORDER BY`句、 `OUTPUT...INTO`句、 `FOR XM`L 句。
* `OPENROWSET`、 `OPENQUERY`、 `OPENDATASOURCE`、 `OPENXML`、または任意の `FULLTEXT` 演算子に渡す引数。直接渡すか、サブ式として渡すかは問いません。
* `LIKE` 句の pattern 引数と escape_character 引数。
* `CONVERT` 句の style 引数。
* `IDENTITY` 句内の整数の定数。
* ODBC 拡張機能の構文で指定した定数。
* 演算子 +、-、\*、/、および % の引数であり、定数のたたみ込みが可能な式。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は、強制パラメーター化を行うことができるかどうかを決定する際に、次のいずれかの条件が満たされていれば式で定数のたたみ込みが可能であると見なします。  
  * 式に列、変数、およびサブクエリが使用されていない。  
  * 式に `CASE` 句が含まれている。  
* クエリ ヒントの句に渡す引数。 `number_of_rows` クエリ ヒントの `FAST` 引数、 `number_of_processors` クエリ ヒントの `MAXDOP` 引数、および `MAXRECURSION` クエリ ヒントの number 引数がこれに該当します。

パラメーター化は個々の [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメント レベルで行われます。 つまり、バッチ内では個々のステートメントがパラメーター化されます。 コンパイルの後、パラメーター化クエリは、最初に送信されたバッチのコンテキストで実行されます。 クエリの実行プランがキャッシュに残っている場合、sys.syscacheobjects 動的管理ビューの sql 列を参照することでクエリがパラメーター化されているかどうかを判断できます。 クエリがパラメーター化されている場合、この列には送信されたバッチのテキストの前に "\@1 tinyint" のように、パラメーターの名前とデータ型が付加されます。

> [!NOTE]
> パラメーター名の規則はありません。 特定の命名順序に依存することは避けてください。 また、次のものは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のバージョンおよび Service Pack の適用状況によって異なる場合があります:パラメーター名、パラメーター化されるリテラル、およびパラメーター化されたテキストに含まれるスペース。

#### <a name="data-types-of-parameters"></a>パラメーターのデータ型

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] がリテラルをパラメーター化する際に、パラメーターは次のデータ型に変換されます。

* int データ型の範囲に収まるサイズの整数リテラルは、int 型にパラメーター化されます。それよりも大きな整数リテラルのうち、比較演算子 (<、\<=、=、!=、>、>=、 、!\<、!>、<>、`ALL`、`ANY`、`SOME`、`BETWEEN`、`IN` など) を伴う述語で使用されているものは numeric(38,0) 型にパラメーター化されます。 比較演算子を伴う述語で使用されていないものは、リテラルのサイズに見合う十分な有効桁数があり、小数点以下桁数が 0 の numeric 型にパラメーター化されます。
* 比較演算子を伴う述語で使用されている固定小数点型のリテラルは、有効桁数が 38 桁で、リテラルのサイズに見合う十分な小数点以下桁数がある numeric 型にパラメーター化されます。 比較演算子を伴う述語で使用されていない固定小数点型のリテラルは、リテラルのサイズに見合う十分な有効桁数および小数点以下桁数がある numeric 型にパラメーター化されます。
* 浮動小数点型のリテラルは float(53) 型にパラメーター化されます。
* Unicode 以外の文字列リテラルは、8,000 文字以内の場合は varchar(8000) 型に、8,000 文字を超える場合は varchar(max) 型にパラメーター化されます。
* Unicode 文字列リテラルは、4,000 文字以内の場合は nvarchar(4000) 型に、4,000 文字を超える場合は nvarchar(max) 型にパラメーター化されます。
* バイナリ リテラルは、8,000 バイト以内の場合は varbinary(8000) 型にパラメーター化されます。 8,000 バイトを超える場合は、varbinary(max) 型に変換されます。
* money 型のリテラルは、money 型にパラメーター化されます。

#### <a name="ForcedParamGuide"></a> 強制パラメーター化使用のガイドライン

`PARAMETERIZATION` オプションを FORCED に設定するときは、次のことを考慮してください。

* 強制パラメーター化を行うと、クエリをコンパイルするときにクエリ内のリテラル定数がパラメーターに変更されます。 そのため、クエリ オプティマイザーで最適なクエリ プランが選択されない場合があります。 特に、インデックス付きビューや、計算列のインデックスに合わせてクエリが調整されることはあまりありません。 パーティション テーブルおよび分散パーティション ビューに発行するクエリについても、最適なプランが選択されない場合があります。 インデックス付きビューおよび計算列のインデックスに大きく依存する環境では、強制パラメーター化を使用しないでください。 `PARAMETERIZATION FORCED` オプションは、熟練したデータベース管理者が、パフォーマンスに悪影響が出ないことを確認した上でのみ使用してください。
* 複数のデータベースを参照する分散クエリでは、そのクエリを実行しているデータベースのコンテキストで `PARAMETERIZATION` オプションが `FORCED` に設定されていれば強制パラメーター化を行うことができます。
* `PARAMETERIZATION` オプションを `FORCED` に設定すると、コンパイル中、再コンパイル中、および実行中のクエリ プランを除くすべてのクエリ プランがデータベースのプラン キャッシュから消去されます。 設定の変更時にコンパイルまたは実行されているクエリのプランは、次回そのクエリを実行するときにパラメーター化されます。
* `PARAMETERIZATION` オプションはオンライン操作で設定します。このとき、データベースレベルの排他ロックは必要ありません。
* `PARAMETERIZATION` オプションの現在の設定は、データベースを再アタッチまたは復元するときも維持されます。

単一クエリ、および構文は同じでパラメーター値のみが異なる他の任意のクエリを簡易パラメーター化するように指定することで、強制パラメーター化の動作をオーバーライドできます。 逆に、データベースで強制パラメーター化の動作が無効になっている場合に、構文が同じクエリに対してのみ強制パラメーター化の動作を指定することもできます。 この方法については、「[プラン ガイド](../relational-databases/performance/plan-guides.md) 」を参照してください。

> [!NOTE]
> `PARAMETERIZATION` オプションを `FORCED` に設定すると、`PARAMETERIZATION` オプションを `SIMPLE` に設定する場合と比べて、報告されるエラー メッセージに違いが現れる場合があります。複数のエラー メッセージが強制パラメーター化で報告される場合があり、簡易パラメーター化よりも多くのエラー メッセージが報告されることがあります。また、エラーが発生した行番号が間違って報告されることがあります。

### <a name="preparing-sql-statements"></a>SQL ステートメントの準備

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のリレーショナル エンジンでは、[!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを実行前に準備する方式が完全にサポートされるようになりました。 アプリケーションでは、[!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを複数回実行する必要がある場合、データベース API を使用して次の処理を実行できます。 

* ステートメントを 1 回準備します。 これにより、[!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントがコンパイルされて実行プランが作成されます。
* ステートメントの実行が必要になるたびに、コンパイル済みの実行プランを実行します。 これにより、2 回目以降は実行ごとに [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを再コンパイルする必要がなくなります。   
  ステートメントの準備と実行は、API の関数およびメソッドによって制御されます。 これは [!INCLUDE[tsql](../includes/tsql-md.md)] 言語の一部ではありません。 [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを実行するための準備/実行のモデルは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーと [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client ODBC ドライバーによってサポートされています。 準備要求時に、プロバイダーまたはドライバーから [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に対し、準備要求と共にステートメントが送信されます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] で実行プランがコンパイルされ、このプランのハンドルがプロバイダーまたはドライバーに返されます。 実行要求時に、プロバイダーまたはドライバーのいずれかによって、ハンドルに関連付けられたプランの実行要求がサーバーに送信されます。 

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、準備されたステートメントを使用して一時オブジェクトを作成することはできません。 また、準備されたステートメントでは、一時テーブルなどの一時オブジェクトを作成するシステム ストアド プロシージャを参照できません。 このようなプロシージャは、直接実行する必要があります。

準備/実行のモデルを過度に使用すると、パフォーマンスが低下することがあります。 ステートメントを 1 回だけ実行する場合は、直接実行のためのネットワークからサーバーへのアクセスは 1 回だけで済みます。 1 回だけ実行される [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを準備してから実行する場合は、もう 1 回余分にネットワークからサーバーにアクセスする必要があります。つまり、1 回はステートメントを準備するため、もう 1 回はステートメントを実行するためです。

パラメーター マーカーを使用する場合、ステートメントを準備するとより効果的です。 たとえば、あるアプリケーションに対して、 `AdventureWorks` サンプル データベースから製品情報を取得するように頻繁に要求する場合を考えます。 アプリケーションでこの処理を実行できる方法は 2 つあります。 

最初の方法を使用すると、アプリケーションでは、次のように要求された製品ごとに個別のクエリを実行できます。

```sql
SELECT * FROM AdventureWorks2014.Production.Product
WHERE ProductID = 63;
```

2 番目の方法を使用すると、アプリケーションによって次の処理が行われます。 

1. 次のように、パラメーター マーカー (?) を含むステートメントを準備します。  
   ```sql
   SELECT * FROM AdventureWorks2014.Production.Product  
   WHERE ProductID = ?;
   ```
2. プログラム変数をパラメーター マーカーにバインドします。
3. 製品情報が必要になるたびに、バインドした変数にキー値を入力し、ステートメントを実行します。

ステートメントを 4 回以上実行する場合は、2 番目の方法がより効率的です。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、直接実行と比べて準備/実行モデルにパフォーマンス上のメリットはほとんどありません。これは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では実行プランが再利用されるためです。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] には、現在の [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを、同じ [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの前回の実行用に生成された実行プランと照合する効率的なアルゴリズムが備わっています。 アプリケーションにより、パラメーター マーカーを使用して [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントが複数回実行される場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では 2 回目以降の実行に最初の実行で使用した実行プランが再利用されます。ただし、プラン キャッシュのプランが古くなった場合は、実行プランは再利用されません。 準備/実行のモデルには次の利点もあります。 

* 識別のためのハンドルによって実行プランを検索する方が、[!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを既存の実行プランと照合するために使用するアルゴリズムよりも効率的です。
* 実行プランの作成および再利用のタイミングをアプリケーションで制御できます。
* 準備/実行のモデルは、以前のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] など、他のデータベースに移植できます。

### <a name="ParamSniffing"></a> パラメーター スニッフィング
"パラメーター スニッフィング" とは、コンパイルまたは再コンパイルの間に [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] が現在のパラメーター値を "スニッフィング (傍受)" し、クエリ オプティマイザーに渡すプロセスです。渡されたパラメーター値は、より効率的なクエリ実行プランを生成するために利用できます。

パラメーター値は、次のようなバッチのコンパイルまたは再コンパイル中にスニッフィングされます。

-  ストアド プロシージャ
-  sp_executesql 経由で送信されたクエリ 
-  準備されたクエリ

不適切なパラメーター スニッフィング問題のトラブルシューティングについては、「[Troubleshoot queries with parameter-sensitive query execution plan issues](https://docs.microsoft.com/azure/sql-database/sql-database-monitor-tune-overview#troubleshoot-performance-problems)」 (パラメーター依存のクエリ実行プランの問題を解決する) を参照してください。

> [!NOTE]
> `RECOMPILE` ヒントを利用するクエリの場合、パラメーター値とローカル変数の現在の値の両方がスニッフィングされます。 (パラメーターとローカル変数の) スニッフィングされた値は、バッチの中で、`RECOMPILE` ヒントのあるステートメントの手前に存在する値です。 特に、パラメーターの場合、バッチ呼び出しで共に与えられた値はスニッフィングされません。

## <a name="parallel-query-processing"></a>並列クエリ処理

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、複数の CPU (マイクロプロセッサ) を搭載したコンピューターのクエリ実行およびインデックス操作を最適化するための並列クエリを使用できます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] はオペレーティング システムのワーカー スレッドを複数使用してクエリやインデックス操作を並列的に実行できるため、操作を短時間で効率的に完了できます。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は、クエリを最適化する過程で、並列実行による効果が期待できるクエリやインデックス操作を検索します。 次に、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は、そのようなクエリの実行プランに交換操作を挿入して並列実行用クエリを作成します。 交換操作とは、プロセス管理、データの再配布、およびフロー制御を行うクエリ実行プラン内の操作です。 交換操作は `Distribute Streams`論理操作、 `Repartition Streams`論理操作、および `Gather Streams` 論理操作から構成されており、これらは並列クエリのプラン表示出力に含まれる可能性があります。 

> [!IMPORTANT]
> 一部の構造は、実行プランの全体または一部分で、並列処理を利用する [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の機能を妨げます。

並列処理を妨げる構造は次のとおりです。
>
> - **スカラー UDF**    
>   スカラー ユーザー定義関数について詳しくは、「[ユーザー定義関数の作成](../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar)」をご覧ください。 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 以降の [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]には、これらの関数をインライン化する機能があり、クエリ処理中の並列処理の使用をロック解除します。 スカラー UDF のインライン化について詳しくは、「[SQL データベースでのインテリジェントなクエリ処理](../relational-databases/performance/intelligent-query-processing.md#scalar-udf-inlining)」をご覧ください。
> - **リモート クエリ**    
>   リモート クエリについて詳しくは、「[プラン表示の論理操作と物理操作のリファレンス](../relational-databases/showplan-logical-and-physical-operators-reference.md)」をご覧ください。
> - **動的カーソル**    
>   カーソルについて詳しくは、「[DECLARE CURSOR](../t-sql/language-elements/declare-cursor-transact-sql.md)」をご覧ください。
> - **再帰クエリ**    
>   再帰について詳しくは、「[再帰共通テーブル式の定義および使用に関するガイドライン](../t-sql/queries/with-common-table-expression-transact-sql.md#guidelines-for-defining-and-using-recursive-common-table-expressions)」および「[Recursion in T-SQL](https://msdn.microsoft.com/library/aa175801(v=sql.80).aspx)」(T-SQL での再帰) をご覧ください。
> - **テーブル値関数 (TVF)**     
>   TVF について詳しくは、「[ユーザー定義関数の作成 (データベース エンジン)](../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)」をご覧ください。
> - **TOP キーワード**    
>   詳しくは、「[TOP (Transact-SQL)](../t-sql/queries/top-transact-sql.md)」をご覧ください。

交換操作を挿入すると、並列クエリの実行プランになります。 並列クエリの実行プランでは複数のワーカー スレッドを使用できます。 並列でないクエリで使用する直列の実行プランの場合、実行時に使用するワーカー スレッドは 1 つのみです。 並列クエリで実際に使用するワーカー スレッドの数は、クエリ プランを実行するための初期化の時点で、プランの複雑さと並列処理の次数に応じて決まります。 並列処理の次数は、使用している CPU の最大数によって決まります (これは使用しているワーカー スレッドの数という意味ではありません)。 並列処理の次数はサーバー レベルで設定され、sp_configure システム ストアド プロシージャで変更できます。 クエリ ステートメントで `MAXDOP` クエリ ヒントを、またはインデックス ステートメントで `MAXDOP` インデックス オプションを指定することにより、この値をオーバーライドできます。 

次のいずれかの条件が満たされている場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のクエリ オプティマイザーは、クエリに対して並列実行プランを使用しません。

* 代替策として並列実行プランの使用を考えるほど、クエリの直列実行コストが高くない。 
* 特定のクエリに対して可能な並列実行プランより、直列実行プランの方が速いと考えられる。
* クエリに、並列では実行できないスカラー演算子または関係演算子が含まれる。 演算子によっては、クエリ プランのセクションまたはプラン全体が直列モードで実行される場合があります。

### <a name="DOP"></a> 並列処理の次数

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は、並列クエリの実行またはインデックス DDL (データ定義言語) 操作のインスタンスごとに、並列処理の最適な次数を自動的に検出します。 この処理は次の基準に基づいて実行されます。 

1. SMP (対称型マルチプロセッシング) コンピューターなど、複数のマイクロプロセッサまたは CPU を搭載したコンピューターで [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] が実行されているかどうか。  
  並列クエリを使用できるのは、複数の CPU を搭載したコンピューターだけです。 

2. 十分な数のワーカー スレッドを使用できるかどうか。  
  各クエリまたはインデックス操作では、一定数のワーカー スレッドを実行する必要があります。 並列プランの実行には直列プランの場合よりも多くのワーカー スレッドが必要になり、必要なワーカー スレッド数は並列処理の次数が高くなるほど増加します。 並列処理の特定の次数に応じた並列プランのワーカー スレッド要件を満たすことができない場合、[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]が並列処理の次数を自動的に下げるか、指定されたワークロード コンテキストでの並列プランを完全に破棄します。 その後、直列プラン (1 つのワーカー スレッド) を実行します。 

3. 実行するクエリまたはインデックス操作の種類。  
  インデックスの作成や再構築またはクラスター化インデックスの削除を行うインデックス操作、および CPU サイクルを大量に使用するクエリは並列プランの候補として最適です。 たとえば、大きなテーブルの結合、大量の集計、および大きな結果セットの並べ替えは候補として適しています。 トランザクション処理アプリケーションに多い単純なクエリの場合、クエリを並列実行するにはさらに調整が必要なので、パフォーマンスの向上は困難です。 並列処理の利点を得られるクエリとそうでないクエリを区別するために、[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]は [cost threshold for parallelism](../database-engine/configure-windows/configure-the-cost-threshold-for-parallelism-server-configuration-option.md) 値を使用して、クエリまたはインデックス操作を実行するための推定コストを比較します。 適切なテストで実行中のワークロードには異なる値がより適していることが判明した場合、ユーザーは [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) を使用して既定値の 5 を変更することができます。 

4. 処理する十分な数の行があるかどうか。  
  クエリ オプティマイザーによって行数が少なすぎると判断されると、行を分散するための交換操作は導入されません。 したがって、操作は直列に実行されます。 直列プランで操作を実行すると、並列操作を実行したときに得られる効果より、起動、分散、および調整のコストの方が上回る事態を回避することができます。

5. 現在の分布統計が使用できるかどうか。  
  並列処理の最高次数が提供されない場合、並列プランが放棄される前に、それより低い次数が検討されます。  
  たとえば、ビューにクラスター化インデックスを作成する場合、クラスター化インデックスはまだ存在しないので、分布統計を評価できません。 この場合、[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]では、インデックス操作用に並列処理の最高次数を提供できません。 ただし、並べ替えやスキャンなどの一部の操作では、それまでどおり並列実行の利点を得ることができます。

> [!NOTE]
> 並列インデックス操作は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition、Developer Edition、および Evaluation Edition でのみ使用できます。
 
既に説明したような現在のシステムのワークロードと構成情報で並列実行が可能かどうかは、実行時に[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]によって判断されます。 並列実行の条件を満たしている場合、[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]により、最適なワーカー スレッド数が判断され、これらのワーカー スレッド全体に並列プランの実行が分散されます。 複数のワーカー スレッドでクエリまたはインデックス操作が並列実行で開始された後は、操作で使用されるワーカー スレッド数は操作の完了時まで変化しません。 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]は、プラン キャッシュから実行プランを取得するたびに、最適なワーカー スレッド数を再調査して決定します。 たとえば、1 回のクエリの実行では直列プランを使用し、同じクエリを再度実行するときは 3 つのワーカー スレッドを使用する並列プランを使用し、3 回目に実行するときは 4 つのワーカー スレッドを使用する並列プランを使用する場合があります。

並列クエリの実行プランでは、挿入操作、更新操作、および削除操作が直列に実行されます。 ただし、UPDATE ステートメントや DELETE ステートメントの WHERE 句、または INSERT ステートメントの SELECT 部分は並列に実行できます。 実際のデータ変更は、データベースに直列に適用されます。

静的カーソルとキーセット ドリブン カーソルは、並列実行プランによって作成できます。 ただし、動的カーソルの動作は、直列実行の場合だけ有効です。 クエリ オプティマイザーは、動的カーソルの一部であるクエリに対しては必ず直列実行プランを生成します。

#### <a name="overriding-degrees-of-parallelism"></a>並列処理の次数のオーバーライド

[max degree of parallelism](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) (MAXDOP) サーバー構成オプション ([!INCLUDE[ssSDS_md](../includes/sssds-md.md)]では [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)) を使用すると、並列プランの実行で使用されるプロセッサの数を制限できます。 max degree of parallelism オプションは、MAXDOP クエリ ヒントまたは MAXDOP インデックス オプションを指定することにより、個別のクエリやインデックス操作のステートメントでオーバーライドできます。 MAXDOP では、個別のクエリやインデックス操作をより制御できます。 たとえば、MAXDOP オプションを使用すると、オンライン インデックス操作専用のプロセッサの数を増減することによって制御できます。 このようにして、インデックス操作で使用されるリソースと同時実行ユーザーが使用するリソースのバランスをとることができます。 

max degree of parallelism オプションを 0 (既定) に設定すると、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] で並列プランの実行で使用するプロセッサの数を最大 64 に制限できます。 MAXDOP オプションを 0 に設定すると、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では 64 個の論理プロセッサという実行時ターゲットが設定されますが、必要であれば、別の値を手動で設定できます。 クエリおよびインデックスに対して MAXDOP を 0 に設定すると、並列プランの実行で指定されたクエリまたはインデックスに対して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] で利用可能なすべてのプロセッサ (最大 64) を使用できます。 MAXDOP はあらゆる並列クエリに強制される値ではなく、並列に望ましいあらゆるクエリにとっての仮のターゲットです。 つまり、実行時に十分なワーカー スレッドが利用できない場合、MAXDOP サーバー構成オプションより低い並列度でクエリが実行されることがあります。

MAXDOP 構成のベスト プラクティスについては、[この Microsoft サポート記事](https://support.microsoft.com/help/2806535/recommendations-and-guidelines-for-the-max-degree-of-parallelism-configuration-option-in-sql-server)を参照してください。

### <a name="parallel-query-example"></a>並列クエリの例

次のクエリでは、2000 年 4 月 1 日を開始日とする特定の四半期に受けた注文のうち、納品期日を過ぎた項目を 1 つ以上含む注文の件数を数えます。 さらに、該当する注文を受注優先度別にグループ分けし、受注優先度の昇順に並べ替えてその注文数を一覧表示します。 

この例には、架空のテーブル名と列名を使用しています。

```sql
SELECT o_orderpriority, COUNT(*) AS Order_Count
FROM orders
WHERE o_orderdate >= '2000/04/01'
   AND o_orderdate < DATEADD (mm, 3, '2000/04/01')
   AND EXISTS
         (
          SELECT *
            FROM    lineitem
            WHERE l_orderkey = o_orderkey
               AND l_commitdate < l_receiptdate
         )
   GROUP BY o_orderpriority
   ORDER BY o_orderpriority
```

`lineitem` テーブルと `orders` テーブルで次のインデックスが定義されていると想定します。

```sql
CREATE INDEX l_order_dates_idx 
   ON lineitem
      (l_orderkey, l_receiptdate, l_commitdate, l_shipdate)

CREATE UNIQUE INDEX o_datkeyopr_idx
   ON ORDERS
      (o_orderdate, o_orderkey, o_custkey, o_orderpriority)
```

上記のクエリに対して生成される並列プランの例を次に示します。

```
|--Stream Aggregate(GROUP BY:([ORDERS].[o_orderpriority])
                  DEFINE:([Expr1005]=COUNT(*)))
    |--Parallelism(Gather Streams, ORDER BY:
                  ([ORDERS].[o_orderpriority] ASC))
         |--Stream Aggregate(GROUP BY:
                  ([ORDERS].[o_orderpriority])
                  DEFINE:([Expr1005]=Count(*)))
              |--Sort(ORDER BY:([ORDERS].[o_orderpriority] ASC))
                   |--Merge Join(Left Semi Join, MERGE:
                  ([ORDERS].[o_orderkey])=
                        ([LINEITEM].[l_orderkey]),
                  RESIDUAL:([ORDERS].[o_orderkey]=
                        [LINEITEM].[l_orderkey]))
                        |--Sort(ORDER BY:([ORDERS].[o_orderkey] ASC))
                        |    |--Parallelism(Repartition Streams,
                           PARTITION COLUMNS:
                           ([ORDERS].[o_orderkey]))
                        |         |--Index Seek(OBJECT:
                     ([tpcd1G].[dbo].[ORDERS].[O_DATKEYOPR_IDX]),
                     SEEK:([ORDERS].[o_orderdate] >=
                           Apr  1 2000 12:00AM AND
                           [ORDERS].[o_orderdate] <
                           Jul  1 2000 12:00AM) ORDERED)
                        |--Parallelism(Repartition Streams,
                     PARTITION COLUMNS:
                     ([LINEITEM].[l_orderkey]),
                     ORDER BY:([LINEITEM].[l_orderkey] ASC))
                             |--Filter(WHERE:
                           ([LINEITEM].[l_commitdate]<
                           [LINEITEM].[l_receiptdate]))
                                  |--Index Scan(OBJECT:
         ([tpcd1G].[dbo].[LINEITEM].[L_ORDER_DATES_IDX]), ORDERED)
```

以下の図は、並列処理の次数が 4 で実行され、2 つのテーブルが結合されているクエリ プランを示しています。

![parallel_plan](../relational-databases/media/parallel-plan.gif)

並列プランには、3 つの並列処理操作が含まれています。 `o_datkey_ptr` インデックスの Index Seek 操作と `l_order_dates_idx` インデックスの Index Scan 操作が並列で実行されます。 これにより、複数の排他ストリームが生成されます。 この処理は、Index Scan 操作と Index Seek 操作の上位にあり最も近い Parallelism 操作からそれぞれ決定できます。 どちらの操作もストリームを再分割し、交換の種類を決定しています。 つまり、単にストリーム間でデータを再移動して、入力時と同じ数のストリームを出力時に生成しているということです。 このストリーム数は並列処理の次数と同じになります。

`l_order_dates_idx` Index Scan 操作の上位にある並列操作は、`L_ORDERKEY` の値を使用して入力ストリームを再分割します。 このようにして、同じ `L_ORDERKEY` の値が同じ出力ストリームで終了します。 同時に、出力ストリームは `L_ORDERKEY` 列の順序を維持し、Merge Join 操作の入力要件を満たします。

Index Seek 操作の上位にある並列操作は、`O_ORDERKEY` の値を使用して入力ストリームを再分割します。 この入力は `O_ORDERKEY` 列の値で並べ替えられておらず、`Merge Join` 操作の結合列であるので、並列操作と Merge Join 操作の間の Sort 操作により、`Merge Join` 操作のために入力を結合列で並べ替えています。 `Sort` 操作は、Merge Join 操作と同様に並列処理されます。

最上位にある並列操作は、複数のストリームから得た結果を 1 つのストリームに集めます。 この並列操作の下位にある Stream Aggregate 操作で実行された部分集計は、並列操作の上位にある Stream Aggregate 操作の `O_ORDERPRIORITY` の異なる値ごとに 1 つの `SUM` 値に累計されます。 このプランには並列処理の次数が 4 に設定された 2 つの交換セグメントが含まれているため、8 個のワーカー スレッドが使用されます。

この例で使用されている演算子の詳細については、「[Showplan Logical and Physical Operators Reference](../relational-databases/showplan-logical-and-physical-operators-reference.md)」 (プラン表示の論理および物理演算子のリファレンス) を参照してください。

### <a name="parallel-index-operations"></a>並列インデックス操作

インデックスの作成や再構築、クラスター化インデックスの削除などのインデックス操作用に構築されたクエリ プランでは、複数のマイクロプロセッサを備えたコンピューターでの並列マルチワーカー スレッド操作が可能になります。

> [!NOTE]
> 並列インデックス操作は、[!INCLUDE[ssKatmai](../includes/ssKatmai-md.md)] より、Enterprise Edition でのみ使用できます。
 
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、インデックス操作の並列処理の限度 (実行に使用する個別ワーカー スレッドの合計数) を決める際に、他のクエリに行うのと同じアルゴリズムが使用されます。 インデックス操作に必要な並列処理の最大限度は、 [max degree of parallelism](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) サーバー構成オプションによって決まります。 CREATE INDEX、ALTER INDEX、DROP INDEX、および ALTER TABLE の各ステートメントで MAXDOP インデックス オプションを設定することにより、個別のインデックス操作の max degree of parallelism 値をオーバーライドできます。

[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]によってインデックス実行プランが構築される際に、並列操作の数は、次のうち最も低い値に設定されます。 

* コンピューター内のマイクロプロセッサ (CPU) の数。
* max degree of parallelism サーバー構成オプションで指定されている数。
* [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のワーカー スレッド用に実行される作業のしきい値以下の CPU の数。

たとえば、CPU が 8 基ある場合でも、max degree of parallelism が 6 に設定されているコンピューターでは、インデックス操作用に生成される並列ワーカー スレッドの数は最大 6 つです。 インデックス実行プランを構築するとき、コンピューター内の 5 基の CPU が [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の作業のしきい値を超えている場合は、実行プランによって指定される並列ワーカー スレッドの数は 3 つだけになります。

並列インデックス操作の主なフェーズには、次のフェーズがあります。 

* 調整ワーカー スレッドがテーブルを迅速かつランダムにスキャンし、インデックス キーの分布を算出します。 調整ワーカー スレッドが、並列操作の限度と等しい数のキー範囲を作成するキーの境界を確立します。それぞれのキー範囲は、同じ数の行を処理対象として算出されます。 たとえば、テーブル内に 400 万行あって並列処理の限度が 4 の場合、調整ワーカー スレッドは 1 セット 100 万行で 4 セットの行に区切るキー値を決定します。 すべての CPU を使用するために十分なキー範囲を確立できない場合、並列処理の限度が適宜減少されます。  
* 調整ワーカー スレッドは、並列操作の限度と等しい数のワーカー スレッドを優先して、それらのワーカー スレッドの作業が完了するまで待ちます。 各ワーカー スレッドは、ワーカー スレッドに割り当てられた範囲内のキー値を持つ行だけを取得するフィルターを使用して、ベース テーブルをスキャンします。 各ワーカー スレッドは、そのキーの範囲内で行のインデックス構造を構築します。 パーティション インデックスの場合、各ワーカー スレッドで指定した数のパーティションが構築されます。 パーティションはワーカー スレッド間では共有されません。  
* すべての並列ワーカー スレッドが完了した後で、調整ワーカー スレッドはインデックスのサブユニットを単一のインデックスに接続します。 このフェーズは、オフライン インデックス操作にのみ適用されます。

個別の `CREATE TABLE` ステートメントまたは `ALTER TABLE` ステートメントには、インデックスの作成を必要とする複数の制約が課される場合があります。 これらの複数のインデックス作成操作は連続して実行されますが、個別のインデックス作成操作は複数の CPU を備えたコンピューターでは並列操作になることがあります。

## <a name="distributed-query-architecture"></a>分散クエリ アーキテクチャ

Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、[!INCLUDE[tsql](../includes/tsql-md.md)] ステートメント内で異種 OLE DB データ ソースを参照する方法として、次の 2 つがサポートされています。

* リンク サーバー名  
  `sp_addlinkedserver` と `sp_addlinkedsrvlogin` の各システム ストアド プロシージャを使用して、OLE DB データ ソースにサーバー名を渡します。 リンク サーバー内のオブジェクトは、4 部構成の名前を使用して [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメント内で参照できます。 たとえば、`DeptSQLSrvr` というリンク サーバー名が [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の別のインスタンスで定義されている場合、次のステートメントはこのサーバー上のテーブルを参照します。 
  
  ```sql
  SELECT JobTitle, HireDate 
  FROM DeptSQLSrvr.AdventureWorks2014.HumanResources.Employee;
  ```

   リンク サーバー名を `OPENQUERY` ステートメントで指定して、OLE DB データ ソースの行セットを開くこともできます。 この行セットは、[!INCLUDE[tsql](../includes/tsql-md.md)] ステートメント内でテーブルと同じように参照できます。 

* アドホック コネクタ名  
  データ ソースを頻繁に参照しない場合は、リンク サーバーに接続するために必要な情報を含めた `OPENROWSET` 関数または `OPENDATASOURCE` 関数を指定します。 これにより、行セットは [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメント内でテーブルと同じように参照できます。 
  
  ```sql
  SELECT *
  FROM OPENROWSET('Microsoft.Jet.OLEDB.4.0',
        'c:\MSOffice\Access\Samples\Northwind.mdb';'Admin';'';
        Employees);
  ```

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、OLE DB を使用してリレーショナル エンジンとストレージ エンジンの間の通信を行います。 リレーショナル エンジンは、各 [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを一連の操作に分割します。それぞれの操作は、ストレージ エンジンがベース テーブルから開いた単純な OLE DB 行セットに対する操作です。 これは、リレーショナル エンジンは、OLE DB データ ソースに対する単純な OLE DB 行セットも開くことができることを意味しています。  
![oledb_storage](../relational-databases/media/oledb-storage.gif)  
リレーショナル エンジンは OLE DB API (アプリケーション プログラミング インターフェイス) を使用して、リンク サーバー上の行セットを開き、行をフェッチし、トランザクションを管理します。

OLE DB データ ソースにリンク サーバーとしてアクセスするには、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] が動作するサーバー上に OLE DB プロバイダーが存在している必要があります。 OLE DB データ ソースに対して使用できる [!INCLUDE[tsql](../includes/tsql-md.md)] 操作の数は、OLE DB プロバイダーの機能によって決まります。

たとえば、`sysadmin` 固定サーバー ロールのメンバーは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスごとに [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の `DisallowAdhocAccess` プロパティを使用して、OLE DB プロバイダーのアドホック コネクタ名の使用を有効化または無効化できます。 アドホック アクセスが有効化されると、そのインスタンスにログオンしているユーザーは、アドホック コネクタ名を含んだ [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを実行し、OLE DB プロバイダーを使用してアクセスできるネットワークのすべてのデータ ソースを参照できます。 `sysadmin` ロールのメンバーは、データ ソースへのアクセスを制御するために、その OLE DB プロバイダーに対するアドホック アクセスを無効化できます。その結果、ユーザーは管理者が定義したリンク サーバー名で参照されるデータ ソースのみに制限されます。 既定では、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] OLE DB プロバイダーではアドホック アクセスが有効化されており、他のすべての OLE DB プロバイダーでは無効化されています。

分散クエリを使用すると、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] サービスを実行している Microsoft Windows アカウントのセキュリティ コンテキストを使用して、他のデータ ソース (たとえば、ファイルや Active Directory などのリレーショナルでないデータ ソース) にアクセスできます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は Windows ログインでは正常にログインを借用できますが、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ログインでは借用できません。 この場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] サービスを実行しているアカウントに権限があり、分散クエリ ユーザーには権限のない他のデータ ソースに、分散クエリ ユーザーからのアクセスを許してしまう可能性が生じます。 対応するリンク サーバーにアクセスする権限のある特定のログインを定義するには、 `sp_addlinkedsrvlogin` を使用します。 このような制御は、アドホック名では使用できないので、OLE DB プロバイダーでアドホック アクセスを有効にする場合は十分に注意してください。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は、可能であれば、OLE DB データ ソースに対して、結合、条件、射影、並べ替え、および GROUP BY (SQL 言語) 操作などのリレーショナル操作を試行します。 特に指定しない限り、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 自身がベース テーブルをスキャンして [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に読み込んだり、リレーショナル操作を実行することはありません。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は OLE DB プロバイダーに問い合わせて、そのプロバイダーがサポートする SQL 文法のレベルを判別し、その情報に基づいて、可能な限り多くのリレーショナル操作をプロバイダーに送ります。 

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、OLE DB プロバイダーのメカニズムを指定して、OLE DB データ ソース内でのキー値の分布状況を示す統計を返すようにします。 これにより、各 [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの必要条件に対して、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クエリ オプティマイザーがデータ ソース内のデータのパターンをより正確に分析できるようになり、最適な実行プランを作成するクエリ オプティマイザーの機能が向上します。 

## <a name="query-processing-enhancements-on-partitioned-tables-and-indexes"></a>パーティション テーブルとパーティション インデックスに対するクエリ処理の機能強化

[!INCLUDE[ssKatmai](../includes/ssKatmai-md.md)] では、多くの並列プランでのパーティション テーブルに対するクエリ処理のパフォーマンスが向上しています。また、並列プランと直列プランを表す方法が変更され、コンパイル時と実行時の両方の実行プランで示されるパーティション分割情報が強化されています。 このトピックでは、これらの機能強化について説明します。また、パーティション テーブルとパーティション インデックスのクエリ実行プランを解釈する方法、およびパーティション分割されたオブジェクトに対するクエリのパフォーマンス向上に関するベスト プラクティスについて説明します。 

> [!NOTE]
> パーティション テーブルとパーティション インデックスは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition、Developer Edition、および Evaluation Edition でのみサポートされます。

### <a name="new-partition-aware-seek-operation"></a>新しいパーティション対応のシーク操作

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ではパーティション テーブルの内部表現が変更され、テーブルはクエリ プロセッサに対して、先頭列に `PartitionID` を持つ複数列インデックスとして表されます。 `PartitionID` は、特定の行を含むパーティションの `ID` を表すために内部的に使用される非表示の計算列です。 たとえば、 `T(a, b, c)`として定義されているテーブル T が列 a でパーティション分割され、列 b にクラスター化インデックスがあるとします。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、このパーティション テーブルは内部的に、スキーマが `T(PartitionID, a, b, c)` で複合キー `(PartitionID, b)` にクラスター化インデックスがある非パーティション テーブルとして扱われます。 これにより、クエリ オプティマイザーは、パーティション テーブルまたはパーティション インデックスの `PartitionID` に基づいてシーク操作を実行できます。 

パーティションの解消は、このシーク操作で行われるようになりました。

In addition, the Query Optimizer is extended so that a seek or scan operation with one condition can be done on `PartitionID` (論理的な先頭列) およびその他のインデックス キー列に基づいて実行し、続いて 2 番目のレベルのシークを実行できます。このシークは最初のレベルのシーク操作の条件を満たす値ごとに、別の条件を指定した 1 つ以上の追加の列に基づいて実行できます。 つまり、スキップ スキャンと呼ばれるこの操作によって、クエリ オプティマイザーは、ある条件に基づいてシーク操作またはスキャン操作を実行してアクセス対象のパーティションを特定し、その操作内で 2 番目のレベルのインデックスのシーク操作を実行し、特定済みのパーティションのうち別の条件を満たすパーティションから行を返すことができます。 たとえば、次のクエリについて考えてみます。

```sql
SELECT * FROM T WHERE a < 10 and b = 2;
```

この例では、 `T(a, b, c)`として定義されているテーブル T が列 a でパーティション分割され、列 b にクラスター化インデックスがあるとします。 テーブル T のパーティション境界は、次のパーティション関数によって定義されます。

```sql
CREATE PARTITION FUNCTION myRangePF1 (int) AS RANGE LEFT FOR VALUES (3, 7, 10);
```

クエリを解決するために、クエリ プロセッサによって最初のレベルのシーク操作が実行され、条件 `T.a < 10`を満たす行を含むすべてのパーティションが検索されます。 これにより、アクセス対象のパーティションが特定されます。 特定された各パーティション内で、プロセッサによって列 b のクラスター化インデックスに対する 2 番目のレベルのシーク操作が実行され、条件 `T.b = 2` および `T.a < 10`を満たす行が検索されます。 

次の図は、スキップ スキャン操作を論理的に表したものです。 列 `T` および `a` にデータが格納されているテーブル `b` を示しています。 パーティションには 1 ～ 4 の番号が割り当てられており、パーティション境界は破線の縦線で表示されています。 パーティションに対する最初のレベルのシーク操作 (図には示されていません) で、パーティション 1、2、および 3 が、テーブルに対して定義されたパーティション分割および列 `a` の述語で暗黙的に指定された Seek 条件を満たすことが特定されています。 つまり、条件 `T.a < 10`を満たします。 スキップ スキャン操作の 2 番目のレベルの Seek 部分でスキャンされるパスは、曲線で表示されています。 基本的に、スキップ スキャン操作によって、前の各パーティションで条件 `b = 2`を満たす行がシークされます。 スキップ スキャン操作の総コストは、3 つの個別のインデックス シークの総コストと同じです。   

![skip_scan](../relational-databases/media/skip-scan.gif)

### <a name="displaying-partitioning-information-in-query-execution-plans"></a>クエリ実行プランのパーティション分割情報の表示

パーティション テーブルとパーティション インデックスに対するクエリの実行プランは、[!INCLUDE[tsql](../includes/tsql-md.md)] `SET` ステートメントの `SET SHOWPLAN_XML` または `SET STATISTICS XML` を使用するか、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Studio のグラフィカル実行プラン出力を使用して調べることができます。 たとえば、コンパイル時の実行プランを表示するにはクエリ エディターのツール バーの *[推定実行プランの表示]* をクリックし、実行時のプランを表示するには *[実際の実行プランを含める]* をクリックします。 

これらのツールを使用すると、次の情報を確認できます。

* パーティション テーブルまたはパーティション インデックスにアクセスする `scans`、 `seeks`、 `inserts`、 `updates`、 `merges`、 `deletes` などの操作。
* クエリによってアクセスされるパーティション。 たとえば、実行時の実行プランでは、アクセスされるパーティションの総数やアクセスされる連続したパーティションの範囲を確認できます。
* シーク操作またはスキャン操作でスキップ スキャン操作が使用され、1 つ以上のパーティションからデータが取得されるタイミング。

#### <a name="partition-information-enhancements"></a>パーティション情報に関する機能強化

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、コンパイル時と実行時の両方の実行プランのパーティション分割情報が強化されています。 実行プランで次の情報が示されるようになりました。

* `Partitioned` 、 `seek`、 `scan`、 `insert`、 `update`、 `merge`などの操作がパーティション テーブルに対して実行されることを示す `delete`属性 (オプション)。  
* 先頭のインデックス キー列として `SeekPredicateNew` を含み、 `SeekKeys` に対して範囲シークを指定するフィルター条件を含む `PartitionID` サブ要素を持つ新しい `PartitionID`要素。 2 つの `SeekKeys` サブ要素が存在する場合は、 `PartitionID` に対するスキップ スキャン操作が使用されることを示しています。   
* アクセスされるパーティションの総数を示す概要情報。 この情報は、実行時のプランでのみ確認できます。 

この情報をグラフィカル実行プラン出力と XML プラン表示出力の両方で表示する方法の説明のために、パーティション テーブル `fact_sales`に対する次のクエリについて考えます。 このクエリでは、2 つのパーティションのデータが更新されます。 

```sql
UPDATE fact_sales
SET quantity = quantity * 2
WHERE date_id BETWEEN 20080802 AND 20080902;
```

次の図は、このクエリのコンパイル時の実行プランにおける `Clustered Index Seek` 操作のプロパティを示しています。 `fact_sales` テーブルの定義およびパーティション定義を確認するには、このトピックの「例」を参照してください。  

![clustered_index_seek](../relational-databases/media/clustered-index-seek.gif)

#### <a name="partitioned-attribute"></a>Partitioned 属性

`Index Seek` などの操作がパーティション テーブルまたはパーティション インデックスに対して実行される場合、コンパイル時のプランと実行時のプランに `Partitioned` 属性が表示され、 `True` (1) に設定されます。 `False` (0) に設定された場合、この属性は表示されません。

`Partitioned` 属性は、次の物理操作と論理操作で表示されます。  
* `Table Scan`  
* `Index Scan`  
* `Index Seek`  
* `Insert`  
* `Update`  
* `Delete`  
* `Merge`  

前の図に示したように、この属性は、属性が定義されている操作のプロパティに表示されます。 XML プラン表示出力では、この属性は、属性が定義されている操作の `Partitioned="1"` ノードに `RelOp` として表示されます。

#### <a name="new-seek-predicate"></a>新しい Seek 述語

XML プラン表示出力では、 `SeekPredicateNew` 要素がその要素を定義している操作に表示されます。 この要素には、 `SeekKeys` サブ要素が最大 2 つ含まれることがあります。 最初の `SeekKeys` アイテムは、論理インデックスのパーティション ID レベルで最初のレベルのシーク操作を指定します。 つまり、この Seek によって、クエリの条件を満たすためにアクセスする必要があるパーティションが特定されます。 2 番目の `SeekKeys` アイテムは、最初のレベルの Seek で特定された各パーティション内で行われるスキップ スキャン操作の 2 番目のレベルの Seek 部分を指定します。 

#### <a name="partition-summary-information"></a>パーティションの概要情報

実行時の実行プランでは、パーティションの概要情報に、アクセスしたパーティションの数やアクセスした実際のパーティションの ID が示されます。 この情報を使用して、クエリで正しいパーティションにアクセスしているかどうか、および他のすべてのパーティションが考慮の対象から除外されているかどうかを確認できます。

示される情報は、 `Actual Partition Count`と `Partitions Accessed`です。 

`Actual Partition Count` は、クエリでアクセスされるパーティションの総数です。

`Partitions Accessed`(XML プラン表示出力内) は、新しい `RuntimePartitionSummary` 要素に表示されるパーティションの概要情報です。この要素は、要素が定義されている操作の `RelOp` ノードに表示されます。 次の例に、合計 2 つのパーティション (パーティション 2 および 3) にアクセスすることを示す `RuntimePartitionSummary` 要素の内容を示します。
```
<RunTimePartitionSummary>

    <PartitionsAccessed PartitionCount="2" >

        <PartitionRange Start="2" End="3" />

    </PartitionsAccessed>

</RunTimePartitionSummary>
```

#### <a name="displaying-partition-information-by-using-other-showplan-methods"></a>プラン表示のその他のメソッドを使用したパーティション情報の表示

`SHOWPLAN_ALL`、 `SHOWPLAN_TEXT`、 `STATISTICS PROFILE` の各プラン表示のメソッドでは、このトピックで説明したパーティション情報はレポートされません。 ただし、例外として、アクセスされるパーティションが、 `SEEK` 述語の一部としてパーティション ID を表す計算列の範囲述語によって特定されます。 次の例に、 `SEEK` 操作の `Clustered Index Seek` 述語を示します。 パーティション 2 および 3 にアクセスし、シーク オペレーターによって条件 `date_id BETWEEN 20080802 AND 20080902`を満たす行がフィルター選択されます。
```
|--Clustered Index Seek(OBJECT:([db_sales_test].[dbo].[fact_sales].[ci]), 

        SEEK:([PtnId1000] >= (2) AND [PtnId1000] \<= (3) 

                AND [db_sales_test].[dbo].[fact_sales].[date_id] >= (20080802) 

                AND [db_sales_test].[dbo].[fact_sales].[date_id] <= (20080902)) 

                ORDERED FORWARD)
```

#### <a name="interpreting-execution-plans-for-partitioned-heaps"></a>パーティション分割されたヒープの実行プランの解釈

パーティション分割されたヒープは、パーティション ID の論理インデックスとして扱われます。 パーティション分割されたヒープのパーティションの解消は、実行プランでは、 `Table Scan` 述語がパーティション ID に対して指定された `SEEK` 操作として表されます。 次の例は、プラン表示情報を示しています。
```
|-- Table Scan (OBJECT: ([db].[dbo].[T]), SEEK: ([PtnId1001]=[Expr1011]) ORDERED FORWARD)
```

#### <a name="interpreting-execution-plans-for-collocated-joins"></a>併置結合の実行プランの解釈

結合のコロケーションは、同じパーティション関数または同等のパーティション関数を使用して 2 つのテーブルをパーティション分割し、結合の両側のパーティション列をクエリの結合条件に指定すると発生します。 クエリ オプティマイザーでは、同じパーティション ID を持つ各テーブルのパーティションが個別に結合されるプランを生成できます。 併置結合では必要なメモリが少なくなり、処理時間が短縮されることがあるので、この結合は非併置結合よりも処理が高速になる場合があります。 クエリ オプティマイザーでは、コストの推定に基づいて、非併置プランまたは併置プランが選択されます。

併置プランでは、 `Nested Loops` 結合は内側の 1 つ以上の結合テーブルまたはインデックス パーティションを読み取ります。 `Constant Scan` 操作内の数値は、パーティション番号を表します。 

パーティション テーブルまたはパーティション インデックスに対して併置結合の並行プランが生成された場合、結合操作 `Constant Scan` と `Nested Loops` の間に Parallelism 操作が表れます。 その場合、結合外部にある複数のワーカー スレッドがそれぞれ異なるパーティションに対して読み取りや操作を行います。 

次の図は、併置結合の並列クエリ プランを示しています。   
![colocated_join](../relational-databases/media/colocated-join.gif)


#### <a name="parallel-query-execution-strategy-for-partitioned-objects"></a>パーティション分割されたオブジェクトの並列クエリの実行方法

クエリ プロセッサは、パーティション分割されたオブジェクトから選択するクエリに対して並列実行を使用します。 クエリ プロセッサでは、実行方法の一環として、クエリに必要なテーブル パーティションと、各パーティションに割り当てるワーカー スレッドの数を決定します。 ほとんどの場合、クエリ プロセッサは、各パーティションに同数またはほぼ同数のワーカー スレッドを割り当て、パーティション全体でクエリを並列実行します。 以降、ワーカー スレッドの割り当てについてさらに詳しく説明します。  

![ワーカー スレッド 1](../relational-databases/media/thread1.gif)

ワーカー スレッドの数がパーティションの数よりも少ない場合、クエリ プロセッサが各ワーカー スレッドを別々のパーティションに割り当てると、最初に、ワーカー スレッドが割り当てられていないパーティションが 1 つ以上残ります。 パーティションでワーカー スレッドの実行が完了すると、クエリ プロセッサは、各パーティションに 1 つのワーカー スレッドが割り当てられるまで、そのワーカー スレッドを次のパーティションに割り当てます。 これが当てはまるのは、クエリ プロセッサがワーカー スレッドを他のパーティションに再割り当てする場合に限ります。  
終了後に再割り当てされたワーカー スレッド。 ワーカー スレッドの数とパーティションの数が同じ場合、クエリ プロセッサは各パーティションに 1 つのワーカー スレッドを割り当てます。 ワーカー スレッドの終了時に、そのワーカー スレッドが別のパーティションに再割り当てされることはありません。  

![ワーカー スレッド 2](../relational-databases/media/thread2.gif)  

ワーカー スレッドの数がパーティションの数よりも多い場合、クエリ プロセッサは各パーティションに同じ数のワーカー スレッドを割り当てます。 ワーカー スレッドの数がパーティションの数で割り切れないと、クエリ プロセッサは、使用できるすべてのワーカー スレッドを使用するために、一部のパーティションにワーカー スレッドを 1 つ多く割り当てます。 パーティションが 1 つしかない場合は、すべてのワーカー スレッドがそのパーティションに割り当てられることに注意してください。 次の図では、4 個のパーティションと 14 個のワーカー スレッドがあります。 各パーティションには 3 つのワーカー スレッドが割り当てられ、さらに 2 つのパーティションには追加のワーカー スレッドが割り当てられて、合計で 14 ワーカー スレッドが割り当てられています。 ワーカー スレッドは、終了時に別のパーティションに再割り当てされることはありません。  

![ワーカー スレッド 3](../relational-databases/media/thread3.gif)  

上の例では簡単にワーカー スレッドを割り当てる方法を示していますが、実際の方法はより複雑で、クエリの実行中に発生する他の変数を使用します。 たとえば、テーブルがパーティション分割され、その列 A にクラスター化インデックスが設定されている場合、クエリで述語句 `WHERE A IN (13, 17, 25)`を使用すると、クエリ プロセッサは、1 つ以上のワーカー スレッドを、各テーブル パーティションではなくワーカー スレッドの 3 つの各シーク値 (A=13、A=17、A=25) に割り当てます。 これらの値を含むパーティションでクエリを実行すれば十分です。これらのシーク述語がすべて同じテーブル パーティションに含まれる場合は、すべてのワーカー スレッドが同じテーブル パーティションに割り当てられます。

別の例として、テーブルで列 A に境界点が (10、20、30) である 4 つのパーティションと、列 B にインデックスが設定されており、クエリに述語句 `WHERE B IN (50, 100, 150)`が含まれるとします。 テーブル パーティションは A の値に基づいているため、B の値はどのテーブル パーティションにも存在する可能性があります。 したがって、クエリ プロセッサは、4 つの各テーブル パーティションで、B の 3 つの値 (50、100、150) を検索します。 クエリ プロセッサは、これらの 12 個の各クエリ スキャンを並列実行できるように、ワーカー スレッドを均等に割り当てます。

|列 A に基づいたテーブル パーティション |各テーブル パーティションにおける列 B の検索 |
|----|----|
|テーブル パーティション 1:A < 10   |B=50、B=100、B=150 |
|テーブル パーティション 2:A >= 10 AND A < 20   |B=50、B=100、B=150 |
|テーブル パーティション 3:A >= 20 AND A < 30   |B=50、B=100、B=150 |
|テーブル パーティション 4:A >= 30  |B=50、B=100、B=150 |

### <a name="best-practices"></a>ベスト プラクティス

大きなパーティション テーブルおよびパーティション インデックスの大量のデータにアクセスするクエリのパフォーマンスを向上するために推奨するベスト プラクティスを次に示します。

* 各パーティションを多くのディスクにわたってストライピングします。 これは、回転ディスクを使用する場合に特に関連性が高くなります。
* 可能な場合は、アクセス頻度の高いパーティションまたはすべてのパーティションを保持できる十分なメイン メモリがあるサーバーを使用して、I/O コストを軽減します。
* クエリ対象のデータがメモリ内に収まらない場合は、テーブルおよびインデックスを圧縮します。 これにより、I/O コストを軽減します。
* 高速なプロセッサおよびできるだけ多くのプロセッサ コアを搭載したサーバーを使用して、並列クエリ処理機能を活用します。
* サーバーに十分な I/O コントローラーの帯域幅があることを確認します。 
* すべての大きなパーティション テーブルにクラスター化インデックスを作成して、B ツリーのスキャンの最適化を活用します。
* パーティション テーブルへのデータの一括読み込みを行う場合は、 [データ読み込みのパフォーマンス ガイド](https://msdn.microsoft.com/library/dd425070.aspx)に関するホワイト ペーパーで説明されている推奨事項に従ってください。

### <a name="example"></a>例

次の例では、7 つのパーティションを持つ 1 つのテーブルを含むテスト データベースを作成します。 この例でクエリを実行し、コンパイル時と実行時の両方のプランのパーティション分割情報を表示する場合は、前に説明したツールを使用します。 

> [!NOTE]
> この例では、100 万以上の行をテーブルに挿入します。 この例を実行すると、ハードウェアによっては数分かかる場合があります。 この例を実行する前に、1.5 GB を超えるディスク領域が確保されていることを確認してください。 
 
```sql
USE master;
GO
IF DB_ID (N'db_sales_test') IS NOT NULL
    DROP DATABASE db_sales_test;
GO
CREATE DATABASE db_sales_test;
GO
USE db_sales_test;
GO
CREATE PARTITION FUNCTION [pf_range_fact](int) AS RANGE RIGHT FOR VALUES 
(20080801, 20080901, 20081001, 20081101, 20081201, 20090101);
GO
CREATE PARTITION SCHEME [ps_fact_sales] AS PARTITION [pf_range_fact] 
ALL TO ([PRIMARY]);
GO
CREATE TABLE fact_sales(date_id int, product_id int, store_id int, 
    quantity int, unit_price numeric(7,2), other_data char(1000))
ON ps_fact_sales(date_id);
GO
CREATE CLUSTERED INDEX ci ON fact_sales(date_id);
GO
PRINT 'Loading...';
SET NOCOUNT ON;
DECLARE @i int;
SET @i = 1;
WHILE (@i<1000000)
BEGIN
    INSERT INTO fact_sales VALUES(20080800 + (@i%30) + 1, @i%10000, @i%200, RAND() * 25, (@i%3) + 1, '');
    SET @i += 1;
END;
GO
DECLARE @i int;
SET @i = 1;
WHILE (@i<10000)
BEGIN
    INSERT INTO fact_sales VALUES(20080900 + (@i%30) + 1, @i%10000, @i%200, RAND() * 25, (@i%3) + 1, '');
    SET @i += 1;
END;
PRINT 'Done.';
GO
-- Two-partition query.
SET STATISTICS XML ON;
GO
SELECT date_id, SUM(quantity*unit_price) AS total_price
FROM fact_sales
WHERE date_id BETWEEN 20080802 AND 20080902
GROUP BY date_id ;
GO
SET STATISTICS XML OFF;
GO
-- Single-partition query.
SET STATISTICS XML ON;
GO
SELECT date_id, SUM(quantity*unit_price) AS total_price
FROM fact_sales
WHERE date_id BETWEEN 20080801 AND 20080831
GROUP BY date_id;
GO
SET STATISTICS XML OFF;
GO
```

##  <a name="Additional_Reading"></a> その他の情報  
 [プラン表示の論理操作と物理操作のリファレンス](../relational-databases/showplan-logical-and-physical-operators-reference.md)  
 [拡張イベント](../relational-databases/extended-events/extended-events.md)  
 [クエリ ストアを使用する際の推奨事項](../relational-databases/performance/best-practice-with-the-query-store.md)  
 [カーディナリティ推定](../relational-databases/performance/cardinality-estimation-sql-server.md)  
 [インテリジェントなクエリ処理](../relational-databases/performance/intelligent-query-processing.md)   
 [演算子の優先順位](../t-sql/language-elements/operator-precedence-transact-sql.md)    
 [実行プラン](../relational-databases/performance/execution-plans.md)    
 [SQL Server データベース エンジンと Azure SQL Database のパフォーマンス センター](../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)
