---
title: Microsoft SQL データベースの接続ライブラリ |Microsoft Docs
description: さまざまなクライアントプログラミング言語から Microsoft SQL Server および Azure SQL Database への接続を可能にするモジュールのダウンロードリンクを提供します。
author: MightyPen
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: article
ms.date: 06/18/2018
ms.author: genemi
ms.openlocfilehash: 71254b937c4c0173af9e1549efb98a0b42f65e02
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632815"
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Microsoft SQL データベースの接続モジュール

この記事では、クライアントプログラムが[Microsoft SQL Server](../relational-databases/database-features.md)との対話に使用できる接続モジュールまたは*ドライバー*のダウンロードリンクと、クラウド[Azure SQL Database](https://docs.microsoft.com/azure/sql-database/)でのツインについて説明します。 ドライバーは、次のオペレーティングシステムで実行されるさまざまなプログラミング言語で使用できます。

- Linux
- MacOS
- Windows

#### <a name="oop-to-relational-mismatch"></a>OOP とリレーショナルの不一致

*リレーショナル*: オブジェクト指向プログラミング (OOP) 言語で記述されたクライアントプログラムは、多くの場合、オブジェクト指向よりもリレーショナルな形式でクエリを実行するデータを返す SQL ドライバーを使用します。 C#ADO.NET の使用は1つの例です。 OOP リレーショナル形式の不一致により、OOP コードの記述と理解が困難になることがあります。

*ORM*: 他のドライバーまたはフレームワークは、クエリを実行するデータを OOP 形式で返し、不一致を回避します。 これらのドライバーは、特定の SQL テーブルのデータ列と一致するようにクラスが定義されていることを前提として機能します。 次に、ドライバーは*オブジェクトリレーショナルマッピング*(ORM) を実行して、クエリされたデータをクラスのインスタンスとして返します。 Microsoft の Entity Framework (EF) for C#、および Java 用の休止状態は2つの例です。

この記事では、この2種類の接続ドライバーに個別のセクションを提供しています。

<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>リレーショナルアクセス用のドライバー


<!--
Each given Microsoft Download Center page should be enhanced
with a link to the next NEWER version page, on the day that the
original page is no longer the latest because the newer page is being added.
But this policy is not agreed on or observed,
putting the links in the following table at risk for being outdated.

PHP driver in Github.com also uses this FWLink:  https://go.microsoft.com/fwlink/?LinkID=518036 ,
although the FWLink is less precise than is https://github.com/Microsoft/msphpsql/tree/dev#install-unix .
-->

| [言語] | SQL ドライバーのダウンロード |
| :------- | :---------------------- |
| C# | [ADO.NET](https://www.microsoft.com/net/download/)<br />[Microsoft.Data.SqlClient](https://www.nuget.org/packages/Microsoft.Data.SqlClient/)<br /><br />[Linux-Ubuntu 用の .NET Core](https://www.microsoft.com/net/core#Ubuntu)<br />[MacOS 用 .NET Core](https://www.microsoft.com/net/core#macos)<br />[Windows 用 .NET Core](https://www.microsoft.com/net/core) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/download-oledb-driver-for-sql-server.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Node.js ドライバー、インストール手順](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP (PHP) | [PHP](./php/download-drivers-php-sql-server.md) |
| Python | [pyodbc、インストール手順](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[ODBC のダウンロード](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Ruby ドライバー、インストール手順](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Ruby ダウンロードページ](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br /> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>ORM アクセス用のドライバー


次の表は、クライアントアプリケーションが Microsoft SQL データベースに接続するために使用するオブジェクトリレーショナルマッピング (ORM) フレームワークの例を示しています。


| [言語] | ORM ドライバーのダウンロード |
| :------- | :------------------ |
| C# | [Entity Framework Core](https://docs.microsoft.com/ef/core/)<br />[Entity Framework (6.x 以降)](https://docs.microsoft.com/ef/) |
| Java | [Hibernate ORM](https://hibernate.org/orm)|
| PHP (PHP) | [Eloquent ORM (Laravel install に含まれています)](https://laravel.com/docs/) |
| Node.js | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | [Django](https://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) |


<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>アプリ web ページのビルド
[https://aka.ms/sqldev](https://aka.ms/sqldev)には、*アプリ*の一連の web ページが表示されます。 Web ページには、プログラミング言語、オペレーティングシステム、および SQL 接続ドライバーのさまざまな組み合わせに関する情報が記載されています。 アプリ web ページによって提供される情報の中には、次の項目があります。

- 言語 + オペレーティングシステム + ドライバーの組み合わせごとに、最初から開始する方法について詳しく説明します。
    - 最新の SQL 接続ドライバーをインストールするための手順です。
- 次の各項目のコード例を次に示します。
    - オブジェクトリレーショナルコードの例。
    - RDS のコード例です。
    - 列ストアインデックスのデモにより、パフォーマンスが大幅に向上します。

#### <a name="first-page-of-build-an-app-webpages"></a>アプリ web ページの最初のページ
![アプリ web ページ、最初のページのスクリーンショット][image-ref-163-buildanapp-webpages-first-page]

#### <a name="menu-for-java---ubuntu-of-build-an-app-webpages"></a>Java 用のメニュー-Ubuntu、アプリの web ページ
![アプリのビルド-web ページ、メニュー Java Ubuntu][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

&nbsp;

## <a name="related-links"></a>関連リンク
- [Java とその他の言語を使用して、クラウド内の Azure SQL Database に接続するためのコード例を示し](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java)ます。

<!-- Image references -->

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
