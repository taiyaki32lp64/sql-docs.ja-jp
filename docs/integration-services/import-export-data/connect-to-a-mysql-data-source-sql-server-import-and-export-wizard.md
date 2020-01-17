---
title: MySQL データ ソースに接続する (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3d7c5a38-18d3-4cc9-a241-04422cb250d3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9fc1128ff50a6b5f6fbb459dca23f518cbcd4f26
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285685"
---
# <a name="connect-to-a-mysql-data-source-sql-server-import-and-export-wizard"></a>MySQL データ ソースに接続する (SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


このトピックでは、SQL Server インポートおよびエクスポート ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページから **MySQL** データ ソースに接続する方法を説明します。 MySQL への接続に使用できるいくつかのデータ プロバイダーがあります。

> [!IMPORTANT]
> MySQL データベースに接続するための詳細な要件と前提条件については、この Microsoft の記事では説明しません。 この記事では、MySQL クライアント ソフトウェアをインストール済みであることと、ターゲットの MySQL データベースに正常に接続できることを前提としています。 詳細については、MySQL データベース管理者に問い合わせるか、MySQL のドキュメントを参照してください。

## <a name="get-the-mysql-connectors"></a>MySQL Connector を取得する
このトピックで説明されているプロバイダーおよびドライバーを「[MySQL Connectors](https://dev.mysql.com/downloads/connector/)」ページからダウンロードします。

## <a name="connect-to-mysql-with-the-net-framework-data-provider-for-mysql"></a>.Net Framework Data Provider for MySQL を使用して MySQL に接続する
ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページで **[.NET Framework Data Provider for MySQL]** を選択すると、そのページにプロバイダーのオプションのグループ化された一覧が表示されます。 これらの多くは、わかりにくい名前となじみのない設定です。 幸い、いくつかの情報を提供するだけで済みます。 他の設定の既定値は無視できます。

> [!NOTE]
> このデータ プロバイダーの接続オプションは、MySQL が変換元または変換先の場合でも同じです。 つまり、表示されるオプションは、ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページともに同じです。

|必要な情報|.NET Framework Data Provider for MySQL プロパティ|
|---|---|
|サーバー名|**[サーバー]**|
|データベース名|**[データベース]**|
|認証 (ログイン) 情報|**ユーザー ID**と**パスワード**|

リストの **[ConnectionString]** フィールドに接続文字列を入力する必要はありません。 MySQL サーバー名 (**サーバー**) とログイン情報に個別の値を入力すると、ウィザードが個々のプロパティとその値から、接続文字列をアセンブルします。 

![.NET プロバイダーを使用して MySQL に接続する、1/2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-1-of-2.png)

![.NET プロバイダーを使用して MySQL に接続する、2/2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-2-of-2.png)

## <a name="connect-to-mysql-with-the-mysql-odbc-driver"></a>MySQL ODBC ドライバーを使用して MySQL に接続する
ODBC ドライバーは、データ ソースのドロップダウン リストに記載されていません。 ODBC ドライバーを使用して接続するには、最初に **[データ ソースの選択]** ページまたは **[変換先の選択]** ページで **[.NET Framework Data Provider for ODBC]** をデータ ソースとして選択します。 このプロバイダーは、ODBC ドライバーのラッパーとして機能します。

下の図は、.NET Framework Data Provider for ODBC を選んだ直後に表示される一般的な画面です。

![ODBC を使用して SQL に接続する](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-mysql-odbc-driver"></a>指定するオプション (MySQL ODBC ドライバー)

> [!NOTE]
> このデータ プロバイダーと ODBC ドライバーの接続オプションは、MySQL が変換元または変換先の場合でも同じです。 つまり、表示されるオプションは、ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページともに同じです。

MySQL ODBC ドライバーを使用して MySQL に接続するには、次の設定とその値を含む接続文字列をアセンブルします。 完全な接続文字列の形式は、リストのすぐ後に示します。

> [!TIP]
> 適切な接続文字列をアセンブルするヘルプを参照してください。 または、接続文字列を提供する代わりに、既存の DSN (データ ソース名) を提供するか、新しく作成します。 これらのオプションの詳細については、「[Connect to an ODBC Data Source](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)」 (ODBC データ ソースに接続する) を参照してください。

**ドライバー**  
ODBC ドライバーの名前。

**[サーバー]**  
MySQL サーバーの名前。 

**[データベース]**  
MySQL データベースの名前。

**UID** と **PWD**   
接続するユーザー ID とパスワード。

### <a name="connection-string-format"></a>接続文字列の形式
一般的な接続文字列の形式を次に示します。

    ```
    Driver={MySQL ODBC 5.3 Unicode Driver};Server=<server>;Database=<database>;UID=<user id>;PWD=<password>
    ```

### <a name="enter-the-connection-string"></a>接続文字列を入力する
**[データ ソースの選択]** ページまたは **[変換先の選択]** ページで、 **[ConnectionString]** フィールドに接続文字列を入力するか、 **[Dsn]** フィールドに DSN 名を入力します。 接続文字列を入力すると、ウィザードによって文字列が解析され、個々のプロパティとその値が一覧に表示されます。

次の例では、この接続文字列を使用しています。

    ```
    Driver={MySQL ODBC 5.3 Unicode Driver};Server=127.0.0.1;Database=world;UID=root;PWD=********
    ```

接続文字列を入力した後に表示される画面を次に示します。

![ODBC を使用して MySQL に接続する](../../integration-services/import-export-data/media/connect-to-mysql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>その他のデータ プロバイダーと詳細情報
ここに記載されていないデータ プロバイダーを使用して MySQL に接続する方法については、「[MySQL connection strings](https://www.connectionstrings.com/mysql/)」 (MySQL 接続文字列) を参照してください。 このサード パーティのサイトには、このページで説明したデータ プロバイダーと接続パラメーターに関する詳細情報も含まれています。

## <a name="see-also"></a>参照
[データ ソースの選択](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[変換先の選択](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

