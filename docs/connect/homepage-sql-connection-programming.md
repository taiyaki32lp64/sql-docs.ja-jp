---
title: SQL クライアントプログラミングのホームページ |Microsoft Docs
description: SQL Server または Azure SQL Database に接続するための、さまざまな言語およびオペレーティングシステムの組み合わせに関するダウンロードとドキュメントへのリンクが記載されたハブページ。
author: MightyPen
ms.date: 11/07/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-daveng
ms.author: genemi
ms.openlocfilehash: 6961f8c23b4acfd787958cc9a160faf88362b54c
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451854"
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Microsoft SQL Server に対するクライアント プログラミングのホーム ページ


Microsoft SQL Server と対話するためのクライアントプログラミングについてのホームページと、クラウドでの Azure SQL Database にようこそ。 この記事には以下の情報が含まれています。

- 使用できる言語とドライバーの組み合わせについて説明します。
    - Linux (Ubuntu など)、MacOS、Windows のオペレーティングシステムに関する情報が提供されます。
- 各組み合わせの詳細なドキュメントへのリンクを示します。
- 特定の言語の階層ドキュメントの領域とサブエリアを表示します (該当する場合)。


#### <a name="azure-sql-database"></a>Azure SQL データベース

特定の言語では、SQL Server に接続するコードは、Azure SQL Database に接続するためのコードとほぼ同じです。

Azure SQL Database に接続するための接続文字列の詳細については、以下を参照してください。

- [.Net Core (C#) を使用して Azure SQL database に対してクエリを](/azure/sql-database/sql-database-connect-query-dotnet-core)実行します。
- 目次の前の記事の近くにあるその他の Azure SQL Database、他の言語については、「」をご覧ください。 たとえば、「 [PHP を使用して AZURE SQL database にクエリを実行する](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php)」を参照してください。


#### <a name="build-an-app-webpages"></a>アプリ web ページのビルド

*アプリのビルド*web ページには、コード例と構成情報が別の形式で表示されています。 詳細については、この記事の後半の「 [*ビルド-アプリ web サイト*」](#an-204-aka-ms-sqldev)を参照してください。



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>クライアントプログラムの言語とドライバー


次の表では、各言語イメージが、SQL Server での言語の使用に関する詳細へのリンクを示しています。 各リンクは、この記事の後のセクションにジャンプします。

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| &nbsp; [![C#ロゴ][image-ref-320-csharp]](#an-110-ado-net-docu) | &nbsp; [![ORM Entity Framework、.NET Framework][image-ref-333-ef]](#an-116-csharp-ef-orm) | &nbsp; [![Java のロゴ][image-ref-330-java]](#an-130-jdbc-docu) |
| &nbsp; [![Node のロゴ][image-ref-340-node]](#an-140-node-js-docu) | &nbsp; [ **`ODBC for C++`** ](#an-160-odbc-cpp-docu)<br/>[![cpp-big-plus][image-ref-322-cpp]](#an-160-odbc-cpp-docu) | &nbsp; [![PHP ロゴ][image-ref-360-php]](#an-170-php-docu) |
| &nbsp; [![Python ロゴ][image-ref-370-python]](#an-180-python-docu) | &nbsp; [![Ruby ロゴ][image-ref-380-ruby]](#an-190-ruby-docu) | &nbsp; ... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>ダウンロードとインストール

次の記事では、プログラミング言語で使用するさまざまな SQL 接続ドライバーのダウンロードとインストールについて説明します。

- [SQL Server ドライバー](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![C#msn][image-ref-320-csharp] C#ADO.NET の使用

C#や Visual Basic などの .net マネージ言語は、ADO.NET の最も一般的なユーザーです。 *ADO.NET*は .NET Framework クラスのサブセットの名前です。

#### <a name="code-examples"></a>コード例

|||
| :-- | :-- |
| [ADO.NET を使用した SQL への接続を概念実証する](./ado-net/step-3-connect-sql-ado-net.md) | SQL Server の接続とクエリに重点を置いた小さなコード例。 |
| [ADO.NET で SQL に弾性的に接続する](./ado-net/step-4-connect-resiliently-sql-ado-net.md) | 接続の損失が発生する可能性があるため、コード例でロジックを再試行します。<br /><br />再試行ロジックは、インターネットを介して管理される接続に、Azure SQL Database などの任意のクラウドデータベースに適切に適用されます。 |
| [Azure SQL Database: Windows/Linux/macOS で .NET Core を使用してC#プログラムを作成し、接続してクエリを実行する方法のデモ](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Azure SQL Database 例。 |
| [アプリのビルド: C#、ADO.NET、Windows](https://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | 構成情報とコード例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>ドキュメント

|||
| :-- | :-- |
| [C#ADO.NET の使用](./ado-net/index.md)| ドキュメントのルート。 |
| [名前空間: system.string](https://docs.microsoft.com/dotnet/api/system.data) | ADO.NET に使用されるクラスのセット。 |
| [名前空間: System.Data.SqlClient](https://docs.microsoft.com/dotnet/api/system.data.SqlClient) | ADO.NET の中心に最も直接的なクラスのセット。 |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Entity Framework のロゴ][image-ref-333-ef] C# では、Entity Framework(EF)

Entity Framework (EF) は、オブジェクトリレーショナルマッピング (ORM) を提供します。 ORM を使用すると、リレーショナル SQL データベースから取得したデータをオブジェクト指向プログラミング (OOP) のソースコードで操作しやすくなります。

EF には、次のテクノロジとの直接的または間接的な関係があります。

- .NET Framework
- [LINQ to SQL](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/)、または[LINQ to Entities](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- 言語構文の機能強化 ( C#の **=>** 演算子など)。
- SQL database 内のテーブルにマップされるクラスのソースコードを生成する便利なプログラム。 たとえば、 [edmgen.exe](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe)のようになります。


#### <a name="original-ef-and-new-ef"></a>元の EF と新しい EF

[Entity Framework の開始ページ](https://docs.microsoft.com/ef/)には、次のような EF が導入されています。

- Entity Framework は、.net 開発者が .NET オブジェクトを使用してデータベースを操作できるようにする、オブジェクトリレーショナルマッパー (O/RM) です。 これにより、開発者が通常記述する必要があるほとんどのデータアクセスソースコードは不要になります。

*Entity Framework*は、2つの異なるソースコード分岐によって共有される名前です。 1つの EF 分岐が古いため、そのソースコードをパブリックで管理できるようになりました。 もう1つは新しい EF です。 次に、2つの EFs について説明します。

|     |     |
| :-- | :-- |
| [EF 6.x](https://docs.microsoft.com/ef/ef6/) | Microsoft は、2008年8月にリリースされた EF の最初のリリースです。 2015年3月に、Microsoft が開発する最新バージョンの EF 6.x が発表されました。 Microsoft は、ソースコードをパブリックドメインにリリースしました。<br /><br />最初の EF は .NET Framework に含まれていました。 ただし、EF 6.x は .NET Framework から削除されました。<br /><br />[リポジトリ*aspnet/EntityFramework6*の EF 6.x ソースコード (Github)](https://github.com/aspnet/EntityFramework6) |
| [EF Core](https://docs.microsoft.com/ef/core/) | Microsoft は、2016年6月に新たに開発された EF Core をリリースしました。 EF Core は、柔軟性と移植性が向上するように設計されています。 EF Core は、Microsoft Windows 以外のオペレーティングシステムでも実行できます。 と EF Core は、Microsoft SQL Server やその他のリレーショナルデータベースだけでなく、データベースと対話できます。<br /><br />**C&#x23;コード例:**<br />[Entity Framework Core でのはじめに](https://docs.microsoft.com/ef/core/get-started/index)<br />[既存のデータベースを使用した .NET Framework での EF Core の概要](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF と関連テクノロジは強力であり、領域全体をマスターする開発者を対象としています。

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Java のロゴ][image-ref-330-java] Java と JDBC

Microsoft では、SQL Server (またはもちろん Azure SQL Database で使用するための Java Database Connectivity (JDBC) ドライバーを提供しています。 これは Type 4 JDBC ドライバーであり、標準の JDBC アプリケーション プログラム インターフェイス (API) によってデータベース接続を提供します。

#### <a name="code-examples"></a>コード例

|||
| :-- | :-- |
| [コード例](./jdbc/code-samples/index.md) | データ型、結果セット、および大規模なデータについて学習するコード例。 |
| [接続 URL のサンプル](./jdbc/connection-url-sample.md) | 接続 URL を使用して SQL Server に接続する方法について説明します。 次に、SQL ステートメントを使用してデータを取得します。 |
| [データ ソースのサンプル](./jdbc/data-source-sample.md) | データソースを使用して SQL Server に接続する方法について説明します。 次に、ストアドプロシージャを使用してデータを取得します。 |
| [Java を使用して Azure SQL database に対してクエリを実行する](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Azure SQL Database 例。 |
| [Ubuntu で SQL Server を使用して Java アプリを作成する](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | 構成情報とコード例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>ドキュメント

JDBC のドキュメントには、次の主な領域が含まれています。

|||
| :-- | :-- |
| [Java Database Connectivity (JDBC)](./jdbc/index.md) | JDBC ドキュメントのルート。 |
| [リファレンス](./jdbc/reference/index.md) | インターフェイス、クラス、およびメンバー。 |
| [JDBC SQL ドライバーのプログラミング ガイド](./jdbc/programming-guide-for-jdbc-sql-driver.md) | 構成情報とコード例。 |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Node.js ロゴ][image-ref-340-node] Node.js

Node.js を使用すると、Windows、Linux、または Mac から SQL Server に接続できます。 Node.js のドキュメントのルートは[こちら](./node-js/index.md)です。

SQL Server 用の node.js 接続ドライバーは、JavaScript で実装されます。 このドライバーは、すべての最新バージョンの SQL Server でサポートされている TDS プロトコルを使用します。 このドライバーは、 [Github で入手できる](https://tediousjs.github.io/tedious/)オープンソースプロジェクトです。

#### <a name="code-examples"></a>コード例

|||
| :-- | :-- |
| [Node.js を使用した SQL への接続を概念実証する](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | SQL Server に接続し、クエリを実行するためのベアボーンソースコード。 |
| [Azure SQL database: node.js を使用してクエリを実行する](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | クラウド内の Azure SQL Database の例。 |
| [MacOS で SQL Server を使用する node.js アプリを作成する](https://www.microsoft.com/sql-server/developer-get-started/node/mac/) | 構成情報とコード例。 |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>ODBCC++ 

![ODBC ロゴ][image-ref-350-odbc] ![cpp-big-plus][image-ref-322-cpp]

Open database connectivity (ODBC) は、1990年に開発され、.NET Framework 登場しました。 ODBC は、特定のデータベースシステムに依存せず、オペレーティングシステムに依存しないように設計されています。

長年にわたり、Microsoft の内外のグループによって多数の ODBC ドライバーが作成およびリリースされています。 ドライバーの範囲には、いくつかのクライアントプログラミング言語が含まれます。 データターゲットの一覧は、SQL Server の範囲を超えています。

その他の接続ドライバーでは、ODBC を内部的に使用します。

#### <a name="code-example"></a>コードの例

- [ODBC を使用する C++ コードの例](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>ドキュメントアウトライン

このセクションの ODBC コンテンツは、からC++SQL Server または Azure SQL Database にアクセスすることに重点を置いています。 次の表に、ODBC の主要なドキュメントのおおよその概要を示します。


| 領域 | 領域 | [説明] |
| :--- | :------ | :---------- |
| [ODBCC++](./odbc/index.md) | ドキュメントのルート。 |
| [Linux、Mac](./odbc/linux-mac/index.md) | &nbsp; | Linux または MacOS オペレーティングシステムで ODBC を使用する方法について説明します。 |
| [Windows](./odbc/windows/index.md)     | &nbsp; | Windows オペレーティングシステムで ODBC を使用する方法について説明します。 |
| [管理](../odbc/admin/index.md) | &nbsp; | ODBC データソースを管理するための管理ツールです。 |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | Microsoft によって作成および提供されるさまざまな ODBC ドライバー。 |
| [概念とリファレンス](../odbc/reference/index.md) | &nbsp; | 従来のリファレンスに加え、ODBC インターフェイスに関する概念情報。 |
| &nbsp; " | [付録](../odbc/reference/appendixes/index.md)    | 状態遷移テーブル、ODBC カーソルライブラリなど。 |
| &nbsp; " | [アプリの開発](../odbc/reference/develop-app/index.md)  | 関数、ハンドルなどがあります。 |
| &nbsp; " | [ドライバーの開発](../odbc/reference/develop-driver/index.md) | 特化されたデータソースがある場合は、独自の ODBC ドライバーを開発する方法。 |
| &nbsp; " | [インストール](../odbc/reference/install/index.md) | ODBC のインストール、サブキーなど。 |
| &nbsp; " | [構文](../odbc/reference/syntax/index.md)   | セットアップ、インストーラー、変換、およびデータアクセスのための Api。 |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![PHP ロゴ][image-ref-360-php] PHP (PHP)

PHP を使用して、SQL Server と対話できます。 PHP ドキュメントのルートは[こちら](./php/index.md)です。

#### <a name="code-examples"></a>コード例

|||
| :-- | :-- |
| [PHP を使用した SQL への接続を概念実証する](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | SQL Server の接続とクエリに重点を置いた小さなコード例。 |
| [PHP で SQL に弾性的に接続する](./php/step-4-connect-resiliently-to-sql-with-php.md) | コード例でロジックを再試行します。インターネットとクラウド経由の接続によって接続が失われる可能性があるためです。 |
| [Azure SQL database: PHP を使用してクエリを実行する](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Azure SQL Database 例。 |
| [RHEL で SQL Server を使用する PHP アプリを作成する](https://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | 構成情報とコード例。 |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Python ロゴ][image-ref-370-python] Python


Python を使用して、SQL Server と対話できます。

#### <a name="code-examples"></a>コード例

|||
| :-- | :-- |
| [Pyodbc を使用した Python を使用した SQL 接続の概念実証](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | SQL Server の接続とクエリに重点を置いた小さなコード例。 |
| [Azure SQL database: Python を使用したクエリ](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Azure SQL Database 例。 |
| [SLES で SQL Server を使用する PHP アプリを作成する](https://www.microsoft.com/sql-server/developer-get-started/python/sles/) | 構成情報とコード例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>ドキュメント

| 領域 | [説明] |
| :--- | :---------- |
| [Python を SQL Server](./python/index.md) | ドキュメントのルート。 |
| [pymssql ドライバー](./python/pymssql/index.md) | Microsoft では、pymssql ドライバーを保守またはテストしません。<br /><br />Pymssql 接続ドライバーは、Python プログラムで使用するための、SQL データベースへの単純なインターフェイスです。 Pymssql は、FreeTDS の上にビルドして、Python DB API (PEP-249) インターフェイスを Microsoft SQL Server に提供します。 |
| [pyodbc ドライバー](./python/pyodbc/index.md)   | Pyodbc 接続ドライバーは、ODBC データベースに簡単にアクセスできるオープンソースの Python モジュールです。 ここでは、DB API 2.0 仕様を実装していますが、さらに Python らしいな利便性でパックされています。 |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Ruby ロゴ][image-ref-380-ruby] Ruby

Ruby を使用して、SQL Server と対話できます。 Ruby ドキュメントのルートは[こちら](./ruby/index.md)です。

#### <a name="code-examples"></a>コード例

|||
| :-- | :-- |
| [Ruby を使用した SQL への接続を概念実証する](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | SQL Server の接続とクエリに重点を置いた小さなコード例。 |
| [Azure SQL database: Ruby を使用してクエリを実行する](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Azure SQL Database 例。 |
| [MacOS で SQL Server を使用する Ruby アプリを作成する](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | 構成情報とコード例。 |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-developmenthttpswwwmicrosoftcomsql-serverdeveloper-get-started"></a>[ビルド-アプリ web サイト (SQL クライアント開発用)](https://www.microsoft.com/sql-server/developer-get-started/)


アプリの[*ビルド*](https://www.microsoft.com/sql-server/developer-get-started/)web ページでは、SQL Server に接続するためのプログラミング言語の長い一覧から選択できます。 また、クライアントプログラムでは、さまざまなオペレーティングシステムを実行できます。

*アプリに*よって、作業を開始する開発者のための単純さと完全性が強調されています。 この手順では、次のタスクについて説明します。

1. Microsoft SQL Server のインストール方法
2. ツールとドライバーをダウンロードしてインストールする方法。
3. 選択したオペレーティングシステムに合わせて必要な構成を行う方法について説明します。
4. 提供されたソースコードをコンパイルする方法。
5. プログラムの実行方法。

次に、web サイトで提供されている詳細のおおよその概略を示します。

#### <a name="java-on-ubuntu"></a>Ubuntu 上の Java:

1. 環境の設定方法
    - 手順 1.1 SQL Server をインストールする
    - 手順 1.2 Java をインストールする
    - 手順 1.3 Java Development Kit (JDK) をインストールする
    - 手順 1.4 Maven をインストールする
2. SQL Server を使用した Java アプリケーションの作成
    - 手順 2.1 SQL Server に接続してクエリを実行する Java アプリを作成する
    - 手順2.2 人気のフレームワーク休止状態を使用して SQL Server に接続する Java アプリを作成する
3. Java アプリを最大100倍まで高速化
    - 手順3.1 列ストアインデックスを示す Java アプリを作成する

#### <a name="python-on-windows"></a>Windows 上の Python:

1. 環境の設定方法
    - 手順 1.1 SQL Server をインストールする
    - 手順 1.2 Python をインストールする
    - 手順 1.3 SQL Server 用の ODBC ドライバーと SQL コマンドラインユーティリティをインストールする
2. SQL Server を使用した Python アプリケーションの作成
    - 手順 2.1 SQL Server 用の Python ドライバーをインストールする
    - 手順2.2 アプリケーションのデータベースを作成する
    - 手順 2.3 SQL Server に接続してクエリを実行する Python アプリを作成する
3. Python アプリを最大100倍まで高速化
    - 手順 3.1 sqlcmd を使用して500万を含む新しいテーブルを作成する
    - 手順3.2 このテーブルに対してクエリを実行し、かかった時間を測定する Python アプリを作成する
    - 手順3.3 クエリの実行にかかる時間を測定する
    - 手順 3.4. 列ストアインデックスをテーブルに追加する
    - 手順3.5 列ストアインデックスを使用してクエリを実行するのにかかる時間を測定する

次のスクリーンショットは、SQL 開発ドキュメント web サイトの外観を示しています。

#### <a name="choose-a-language"></a>言語の選択:

![SQL Dev web サイト, はじめに][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>オペレーティングシステムの選択:

![SQL Dev web サイト, Java Ubuntu][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>その他の開発


このセクションでは、その他の開発オプションに関するリンクを示します。 これには、一般的に Azure の開発にも同じ言語を使用することが含まれます。 この情報は、Azure SQL Database と Microsoft SQL Server だけを対象としています。

#### <a name="developer-hub-for-azure"></a>Azure の開発者ハブ

- [Azure の開発者ハブ](https://docs.microsoft.com/azure/)
- [Azure for .NET 開発者](https://docs.microsoft.com/dotnet/azure/)
- [Java 開発者向けの Azure](https://docs.microsoft.com/java/azure/)
- [Node.js 開発者向けの Azure](https://docs.microsoft.com/nodejs/azure/)
- [Python 開発者向けの Azure](https://docs.microsoft.com/python/azure/)
- [Azure での PHP web アプリの作成](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>その他の言語

- [Windows で SQL Server を使用したゴーアプリの作成](https://www.microsoft.com/sql-server/developer-get-started/go/windows/)



<!-- Image references. -->

[image-ref-322-cpp]: ./media/homepage-sql-connection-drivers/gm-cpp-4point-p61f.png
[image-ref-320-csharp]: ./media/homepage-sql-connection-drivers/gm-csharp-c10c.png
[image-ref-333-ef]: ./media/homepage-sql-connection-drivers/gm-entity-framework-ef20d.png
[image-ref-330-java]: ./media/homepage-sql-connection-drivers/gm-java-j18c.png
[image-ref-340-node]: ./media/homepage-sql-connection-drivers/gm-node-n30.png
[image-ref-350-odbc]: ./media/homepage-sql-connection-drivers/gm-odbc-ic55826-o35.png
[image-ref-360-php]: ./media/homepage-sql-connection-drivers/gm-php-php60.png
[image-ref-370-python]: ./media/homepage-sql-connection-drivers/gm-python-py72.png
[image-ref-380-ruby]: ./media/homepage-sql-connection-drivers/gm-ruby-un-r82.png
[image-ref-390-aka-ms-sqldev-choose-language]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-400-aka-ms-sqldev-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png

