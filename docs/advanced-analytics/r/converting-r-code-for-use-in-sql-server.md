---
title: SQL 用の R コードを変換する
description: SQL Server 上でのソリューションの配置とリレーショナル データへのデータ アクセスのために、R コードを SQL Server ストアド プロシージャに移行します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 882ce47467a38ab4a891f632c9598070e13494e3
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727539"
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>SQL Server (データベース内) のインスタンスで実行するために R コードを変換する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、SQL Server で動作するように R コードを変更する方法の概要について説明します。 

R コードを R Studio または別の環境から SQL Server に移動するときに、コードはほとんどの場合 (たとえば、入力を受け取って値を返す関数など、コードが単純な場合)、追加の変更なしで動作します。 また、最小限の変更でさまざまな実行コンテキストでの実行をサポートする **RevoScaleR** や **MicrosoftMl** パッケージを使用するソリューションの移植も容易です。

ただし、次のいずれかに該当する場合は、コードに大幅な変更が必要になることがあります。

+ ネットワークにアクセスするか、SQL Server にインストールできない R ライブラリを使用する。
+ コードが、Excel ワークシート、共有のファイル、その他のデータベースなど、SQL Server 外部のデータソースに対して個別の呼び出しを行う。 
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) の *\@script* パラメーターでコードを実行し、ストアド プロシージャのパラメーター化も行う。
+ 元のソリューションに、データ準備や特徴エンジニアリング、またはモデル トレーニング、スコアリング、レポート作成など、単独で実行した方が運用環境で効率的な場合がある複数の手順が含まれている。
+ ライブラリを変更したり、並列実行を使用したり、一部の処理を SQL Server にオフロードしたりして、パフォーマンスを最適化したい。 

## <a name="step-1-plan-requirements-and-resources"></a>手順 1. 要件とリソースを計画する

**パッケージ**

+ 必要なパッケージを特定し、SQL Server で動作することを確認します。
 
+ Machine Learning Services によって使用される既定のパッケージ ライブラリに、事前にパッケージをインストールします。 ユーザー ライブラリはサポートされていません。

**[データ ソース]** 

+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) に R コードを埋め込む場合は、プライマリとセカンダリのデータ ソースを特定します。 

    + **プライマリ** データソースは、モデル トレーニング データや予測用の入力データなどの大規模なデータセットです。 最も大きなデータセットを、[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) の入力パラメーターにマップするよう計画します。

    + **セカンダリ** データソースは、通常、要因の一覧や追加のグループ化変数など、サイズの小さいデータセットです。 
    
    現在、sp_execute_external_script では、ストアド プロシージャへの入力として 1 つのデータセットのみがサポートされています。 ただし、複数のスカラーまたはバイナリの入力を追加できます。

    EXECUTE で始まるストアド プロシージャの呼び出しは、[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) への入力として使用することはできません。 クエリ、ビュー、またはその他の有効な SELECT ステートメントを使用できます。

+ 必要な出力を決定します。 sp_execute_external_script を使用して R コードを実行した場合、ストアド プロシージャは 1 つのデータ フレームだけを結果として出力できます。 ただし、バイナリ形式のプロットおよびモデルや、R コードまたは SQL パラメーターから派生したその他のスカラー値など、複数のスカラー出力を出力することもできます。

**データ型**

+ 起こり得るデータ型の問題のチェックリストを作成します。

    すべての R データ型は、SQL Server Machine Learning Services でサポートされています。 ただし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は R よりも多くの種類のデータ型をサポートします。そのため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータを R に送信するときに (逆の場合も)、暗黙的なデータ型変換が実行されます。 一部のデータは、明示的なキャストまたは変換が必要な場合もあります。 

    NULL 値がサポートされます。 ただし、R では、`na` データ コンストラクトを使用して、null 値に似た欠落値を表します。

+ R で使用できないデータへの依存関係を排除することを検討してください。たとえば、SQL Server の rowid および GUID データ型を R で使用してエラーを生成することはできません。

    詳しくは、[R のライブラリとデータ型](../r/r-libraries-and-data-types.md)に関する記事をご覧ください。

## <a name="step-2-convert-or-repackage-code"></a>手順 2. コードを変換または再パッケージ化する

コードをどの程度変更するかは、リモート クライアントから R コードを送信して SQL Server の計算コンテキストで実行するか、パフォーマンスとデータ セキュリティに優れた、ストアド プロシージャの一部としてのコードの配置を行うかによって異なります。 ストアド プロシージャでコードをラップするには、いくつかの追加要件があります。 

+ データ移動を回避するために、可能な限り、プライマリ入力データを SQL クエリとして定義します。

+ ストアド プロシージャで R を実行する場合は、複数の**スカラー**入力をパススルーできます。 出力で使用するパラメーターについては、**OUTPUT** キーワードを追加します。 

    たとえば、次のスカラー入力 `@model_name` には、モデル名が含まれています。これは、結果の独自の列にも出力されます。

    ```sql
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ ストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) のパラメーターとして渡す変数は、R コードの変数にマップする必要があります。 既定では、変数は、名前によってマップされます。

    入力データセット内のすべての列も、R スクリプトの変数にマップする必要があります。  たとえば、R スクリプトに次のような数式が含まれているとします。

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    ArrDelay、CRSDepTime、DayOfWeek、CRSDepHour、および DayOfWeek と一致する名前の列が入力データセットに含まれていない場合は、エラーが発生します。

+ 場合によっては、結果に対して事前に出力スキーマを定義する必要があります。

    たとえば、データをテーブルに挿入するには、**WITH RESULT SET** 句を使用してスキーマを指定する必要があります。

    R スクリプトで引数 `@parallel=1` を使用する場合は、出力スキーマも必要です。 理由は、クエリを並列で実行するために SQL Server が複数のプロセスを作成し、最後に結果を収集する可能性があるためです。 したがって、並列処理を作成する前に、出力スキーマを準備する必要があります。
    
    それ以外の場合は、オプション **WITH RESULT SETS UNDEFINED** を使用して結果スキーマを省略できます。 このステートメントは、列に名前を付けたり SQL データ型を指定したりせずに、R スクリプトからデータセットを返します。

+ R ではなく T-SQL を使用して、タイミング データまたは追跡データを生成することを検討してください。

    たとえば、R スクリプトで類似のデータを生成するのではなく、結果に渡される T-SQL 呼び出しを追加することによって、監査とストレージに使用されるシステム時刻やその他の情報を渡すことができます。 

**パフォーマンスとセキュリティを向上させる**

+ 予測または中間結果をファイルに書き込むことは避けてください。 データ移動を避けるために、予測はテーブルに書き込みます。

+ すべてのクエリを事前に実行し、SQL Server クエリ プランを確認して、並列で実行できるタスクを識別します。

    入力クエリを並列化できる場合は、[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) に渡す引数の一部として `@parallel=1` を設定します。 

    このフラグによる並列処理は、SQL Server がパーティション分割されたテーブルを操作できるか、クエリを複数のプロセスに分散して最後に結果を集計できるときは、通常はいつでも実行できます。 このフラグによる並列処理は、すべてのデータを読み取る必要があるアルゴリズムを使用するモデルをトレーニングする場合、または集計を作成する必要がある場合は、通常は実行できません。

+ R コードを見直して、別のストアド プロシージャの呼び出しを使用して単独で実行できる手順またはより効率的に実行できる手順があるかどうかを判断します。 たとえば、特徴エンジニアリングや特徴抽出を別々に実行し、値をテーブルに保存することによってパフォーマンスを高めることができる場合があります。

+ セットベースの計算では、R コードではなく T-SQL を使用する方法を探します。

    たとえば、次の R ソリューションは、ユーザー定義の T-SQL 関数と R が同じ特徴エンジニアリング タスクをどのように実行できるかを示しています。[データ サイエンスのエンドツーエンド チュートリアル](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)。

+ 可能であれば、従来の R 関数を、分散実行をサポートする **ScaleR** 関数に置き換えます。 詳細については、[ベース R とスケール R 関数の比較](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r)に関するページを参照してください。

+ データベース開発者と相談して、[メモリ最適化テーブル](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)などの SQL Server 機能 (または、Enterprise Edition を使用している場合は [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor)) を使用してパフォーマンスを向上させる方法を決定します。

    詳細については、「[Analytics Services のための SQL Server 最適化のヒントとテクニック](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)」を参照してください

### <a name="step-3-prepare-for-deployment"></a>手順 3. 展開を準備する

+ 管理者に通知して、コードを展開する前にパッケージをインストールして事前にテストできるようにしてください。 

    開発環境では、パッケージをコードの一部としてインストールしても問題はないかもしれませんが、これは運用環境では不適切な行為です。 

    ストアド プロシージャを使用しているか、SQL Server の計算コンテキストで R コードを実行しているかに関係なく、ユーザー ライブラリはサポートされません。

**ストアド プロシージャで R コードをパッケージ化する**

+ コードが比較的単純な場合は、これらのサンプルで説明されているように、コードを変更せずに T-SQL ユーザー定義関数に埋め込むことができます。

    + [rxExec で実行する R 関数を作成する](../tutorials/deepdive-create-a-simple-simulation.md)
    + [T-SQL と R を使用した特徴エンジニアリング](../tutorials/sqldev-create-data-features-using-t-sql.md)

+ コードがより複雑な場合は、R パッケージ **sqlrutils** を使用してコードを変換します。 このパッケージは、経験豊富な R ユーザーが適切なストアド プロシージャ コードを記述できるように設計されています。 

    最初の手順では、明示的に定義された入力と出力を使用して、R コードを 1 つの関数として書き直します。

    次に、**sqlrutils** パッケージを使用して、正しい形式で入力と出力を生成します。 **sqlrutils** パッケージは、ストアド プロシージャの完全なコードを自動的に生成します。また、データベースにストアド プロシージャを登録することもできます。 

    詳細と例については、[sqlrutils (SQL)](ref-r-sqlrutils.md) に関する記事を参照してください。

**他のワークフローと統合する**

+ T-SQL ツールと ETL プロセスを活用します。 データ ワークフローの一部として、特徴エンジニアリング、特徴抽出、およびデータ クレンジングを事前に実行します。

    [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] や RStudio などの専用の R 開発環境で作業する場合は、データをコンピューターにプルして繰り返し分析した後、結果を書き出すか表示することができます。 
    
    ただし、スタンドアロン R コードが SQL Server に移行された場合、このプロセスの大半は、簡素化するか他の SQL Server ツールに委任できます。 

+ セキュリティで保護された非同期の視覚化方法を使用します。

    多くの場合、SQL Server のユーザーはサーバー上のファイルにアクセスすることはできず、SQL クライアント ツールは、通常、R グラフィックス デバイスをサポートしていません。 ソリューションの一部としてプロットまたはその他のグラフィックスを生成する場合は、プロットをバイナリ データとしてエクスポートし、テーブルに保存するか、書き込みを行うことを検討してください。

+ アプリケーションによる直接アクセスのために、予測およびスコアリング関数をストアド プロシージャにラップします。

### <a name="other-resources"></a>その他のリソース

SQL Server への R ソリューションの展開方法の例については、これらのサンプルを参照してください。

+ [R と SQL Server を使用してスキー レンタル事業用の予測モデルを作成する](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [SQL 開発者向けのデータベース内分析](../tutorials/sqldev-in-database-r-for-sql-developers.md): R コードをストアド プロシージャにラップすることでモジュール性を高める方法が示されています

+ [エンドツーエンドのデータ サイエンス ソリューション](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md): R と T-SQL での特徴エンジニアリングの比較が含まれています
