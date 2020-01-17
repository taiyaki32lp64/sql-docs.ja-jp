---
title: Oracle データ ソースに接続する (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b0bd1f5a-34dd-4be3-9ac8-f9f87727781b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: faa8517c24a3db78ee7e7b53ff0151be93a87ba2
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285433"
---
# <a name="connect-to-an-oracle-data-source-sql-server-import-and-export-wizard"></a>Oracle データ ソースに接続する (SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


このトピックでは、SQL Server インポートおよびエクスポート ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページから **Oracle** データ ソースに接続する方法を説明します。 Oracle への接続に使用できるいくつかのデータ プロバイダーがあります。

> [!IMPORTANT]
> Oracle データベースに接続するための詳細な要件と前提条件については、この Microsoft の記事では説明しません。 この記事では、Oracle クライアント ソフトウェアをインストール済みであることと、ターゲットの Oracle データベースに正常に接続できることを前提としています。 詳細については、Oracle データベース管理者に問い合わせるか、Oracle のドキュメントを参照してください。

## <a name="connect-to-oracle-with-the-net-framework-data-provider-for-oracle"></a>.NET Framework Data Provider for Oracle を使用して Oracle に接続する
ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページで **[.NET Framework Data Provider for Oracle]** を選択すると、そのページにプロバイダーのオプションのグループ化された一覧が表示されます。 これらの多くは、分かりにくい名前となじみのない設定です。 幸い、2、3 の情報を提供するだけで済みます。 他の設定の既定値は無視できます。

> [!NOTE]
> このデータ プロバイダーの接続オプションは、Oracle が変換元または変換先の場合でも同じです。 つまり、表示されるオプションは、ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページともに同じです。

|必要な情報|.NET Framework Data Provider for Oracle プロパティ|
|---|---|
|サーバー名|**[データ ソース]**|
|認証 (ログイン) 情報|**ユーザー ID** と**パスワード**、または**統合セキュリティ**|

リストの **[ConnectionString]** フィールドに接続文字列を入力する必要はありません。 Oracle サーバー名 (**データ ソース**) とログイン情報に個別の値を入力すると、ウィザードが個々のプロパティとその値から、接続文字列をアセンブルします。 

![.NET プロバイダーを使って Oracle に接続する](../../integration-services/import-export-data/media/connect-to-oracle-with-net-provider.jpg)

## <a name="connect-to-oracle-with-the-microsoft-odbc-driver-for-oracle"></a>Oracle 用 Microsoft ODBC ドライバーを使って Oracle に接続する
ODBC ドライバーは、データ ソースのドロップダウン リストに記載されていません。 ODBC ドライバーを使用して接続するには、最初に **[データ ソースの選択]** ページまたは **[変換先の選択]** ページで **[.NET Framework Data Provider for ODBC]** をデータ ソースとして選択します。 このプロバイダーは、ODBC ドライバーのラッパーとして機能します。

下の図は、.NET Framework Data Provider for ODBC を選んだ直後に表示される一般的な画面です。

![ODBC を使って Oracle に接続する (前)](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-oracle"></a>指定するオプション (Oracle 用 ODBC ドライバー)

> [!NOTE]
> このデータ プロバイダーと ODBC ドライバーの接続オプションは、Oracle が変換元または変換先の場合でも同じです。 つまり、表示されるオプションは、ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページともに同じです。

Oracle 用 ODBC ドライバーを使用して Oracle に接続するには、次の設定とその値を含む接続文字列をアセンブルします。 完全な接続文字列の形式は、リストのすぐ後に示します。

> [!TIP]
> 適切な接続文字列をアセンブルするヘルプを参照してください。 または、接続文字列を提供する代わりに、既存の DSN (データ ソース名) を提供するか、新しく作成します。 これらのオプションの詳細については、「[Connect to an ODBC Data Source](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)」 (ODBC データ ソースに接続する) を参照してください。

**[ドライバー]**  
ODBC ドライバーの名前、**Oracle 用 Microsoft ODBC**。

**[サーバー]**  
Oracle サーバーの名前。 

**[Uid]** と **[Pwd]**    
接続するユーザー ID とパスワード。

### <a name="connection-string-format"></a>接続文字列の形式
一般的な接続文字列の形式を次に示します。

    ```
    Driver={Microsoft ODBC for Oracle};Server=myServerAddress;Uid=myUsername;Pwd=myPassword;
    ```

### <a name="enter-the-connection-string"></a>接続文字列を入力する
**[データ ソースの選択]** ページまたは **[変換先の選択]** ページで、 **[ConnectionString]** フィールドに接続文字列を入力するか、 **[Dsn]** フィールドに DSN 名を入力します。 接続文字列を入力すると、ウィザードによって文字列が解析され、個々のプロパティとその値が一覧に表示されます。

接続文字列を入力した後に表示される画面を次に示します。

![ODBC を使って Oracle に接続する](../../integration-services/import-export-data/media/connect-to-oracle-with-odbc.jpg)

## <a name="whats-my-oracle-server-name"></a>Oracle サーバー名とは
次のいずれかのクエリを実行して、Oracle サーバーの名前を取得します。

`SELECT host_name FROM v$instance`

内の複数の

`SELECT sys_context('USERENV','SERVER_HOST') FROM dual`

## <a name="other-data-providers-and-more-info"></a>その他のデータ プロバイダーと詳細情報
ここに記載されていないデータ プロバイダーを使用して Oracle に接続する方法については、「[Oracle connection strings](https://www.connectionstrings.com/oracle/)」 (Oracle 接続文字列) を参照してください。 このサード パーティのサイトには、このページで説明したデータ プロバイダーと接続パラメーターに関する詳細情報も含まれています。

## <a name="see-also"></a>参照
[データ ソースの選択](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[変換先の選択](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

