---
title: PostgreSQL データ ソースに接続する (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b7a75a72-b267-444f-9eb8-d23eb333fc35
author: chugugrace
ms.author: chugu
ms.openlocfilehash: da1688881523723206b03d7f7dec3abc2e518370
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296308"
---
# <a name="connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard"></a>PostgreSQL データ ソースに接続する (SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


このトピックでは、SQL Server インポートおよびエクスポート ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページから **PostgreSQL** データ ソースに接続する方法を説明します。 

> [!IMPORTANT]
> PostgreSQL データベースに接続するための詳細な要件と前提条件については、この Microsoft の記事では説明しません。 この記事では、PostgreSQL クライアント ソフトウェアをインストール済みであることと、ターゲットの PostgreSQL データベースに正常に接続できることを前提としています。 詳細については、PostgreSQL データベース管理者に問い合わせるか、PostgreSQL のドキュメントを参照してください。

## <a name="get-the-postgresql-odbc-driver"></a>PostgreSQL ODBC ドライバーを入手する

### <a name="install-the-odbc-driver-with-stack-builder"></a>Stack Builder で ODBC ドライバーをインストールする
Stack Builder を実行し、インストール済みの PostgreSQL に PostgreSQL ODBC ドライバー (psqlODBC) を追加します。

![Stack Builder で PostgreSQL ODBC をインストールする](../../integration-services/import-export-data/media/install-postgresql-odbc-with-stack-builder.png)

### <a name="or-download-the-latest-odbc-driver"></a>あるいは、最新の ODBC ドライバーをダウンロードする
あるいは、最新版の PostgreSQL ODBC ドライバー (psqlODBC) の Windows インストーラーを FTP サイト [https://www.postgresql.org/ftp/odbc/versions/msi/](https://www.postgresql.org/ftp/odbc/versions/msi/) から直接ダウンロードします。 .zip ファイルからファイルを解凍し、.msi ファイルを実行します。

## <a name="connect-to-postgresql-with-the-postgresql-odbc-driver-psqlodbc"></a>PostgreSQL ODBC ドライバー (psqlODBC) で PostgreSQL に接続する
ODBC ドライバーは、データ ソースのドロップダウン リストに記載されていません。 ODBC ドライバーを使用して接続するには、最初に **[データ ソースの選択]** ページまたは **[変換先の選択]** ページで **[.NET Framework Data Provider for ODBC]** をデータ ソースとして選択します。 このプロバイダーは、ODBC ドライバーのラッパーとして機能します。

下の図は、.NET Framework Data Provider for ODBC を選んだ直後に表示される一般的な画面です。

![ODBC を使って PostgreSQL に接続する](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-postgresql-odbc-driver"></a>指定するオプション (PostgreSQL ODBC ドライバー)

> [!NOTE]
> このデータ プロバイダーと ODBC ドライバーの接続オプションは、PostgreSQL が変換元または変換先の場合でも同じです。 つまり、表示されるオプションは、ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページともに同じです。

PostgreSQL ODBC ドライバーを使用して PostgreSQL に接続するには、次の設定とその値を含む接続文字列をアセンブルします。 完全な接続文字列の形式は、リストのすぐ後に示します。

> [!TIP]
> 適切な接続文字列をアセンブルするヘルプを参照してください。 または、接続文字列を提供する代わりに、既存の DSN (データ ソース名) を提供するか、新しく作成します。 これらのオプションの詳細については、「[Connect to an ODBC Data Source](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)」 (ODBC データ ソースに接続する) を参照してください。

**[ドライバー]**  
ODBC ドライバーの名前 - **[PostgreSQL ODBC Driver(UNICODE)]** または **[PostgreSQL ODBC Driver(ANSI)]** 。

**[サーバー]**  
PostgreSQL サーバーの名前。 

**[ポート]**  
PostgreSQL サーバーに接続するためのポート。

**[データベース]**  
PostgreSQL データベースの名前。

**[Uid]** と **[Pwd]**    
接続する **Uid** (ユーザー id) と **Pwd** (パスワード)。

### <a name="connection-string-format"></a>接続文字列の形式
一般的な接続文字列の形式を次に示します。 

    ```
    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=<server>;Port=<port>;Database=<database>;UID=<user id>;PWD=<password>
    ```

### <a name="enter-the-connection-string"></a>接続文字列を入力する
**[データ ソースの選択]** ページまたは **[変換先の選択]** ページで、 **[ConnectionString]** フィールドに接続文字列を入力するか、 **[Dsn]** フィールドに DSN 名を入力します。 接続文字列を入力すると、ウィザードによって文字列が解析され、個々のプロパティとその値が一覧に表示されます。

次の例では、この接続文字列を使用しています。

    ```
    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=127.0.0.1;Port=5432;Database=postgres;UID=postgres;PWD=********
    ```

接続文字列を入力した後に表示される画面を次に示します。

![ODBC を使って PostgreSQL に接続する](../../integration-services/import-export-data/media/connect-to-postgresql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>その他のデータ プロバイダーと詳細情報
ここに記載されていないデータ プロバイダーを使用して PostgreSQL に接続する方法については、「[PostgreSQL connection strings](https://www.connectionstrings.com/postgresql/)」 (PostgreSQL 接続文字列) を参照してください。 このサード パーティのサイトには、このページで説明したデータ プロバイダーと接続パラメーターに関する詳細情報も含まれています。

## <a name="see-also"></a>参照
[データ ソースの選択](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[変換先の選択](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

