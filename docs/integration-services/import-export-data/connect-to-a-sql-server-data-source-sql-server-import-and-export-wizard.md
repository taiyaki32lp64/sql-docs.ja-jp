---
title: SQL Server データ ソースに接続する (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 386cedbb-fae5-45ce-9363-c4a417f80a2f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 938a6d8ba779d1cef37b5fab767e609d00b4f022
ms.sourcegitcommit: aaa42f26c68abc2de10eb58444fe6b490c174eab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74308003"
---
# <a name="connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard"></a>SQL Server データ ソースに接続する (SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


このトピックでは、SQL Server インポートおよびエクスポート ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページから **Microsoft SQL Server** データ ソースに接続する方法を説明します。 SQL Server への接続に使用できるいくつかのデータ プロバイダーがあります。

> [!TIP]
> 複数のサーバーがあるネットワーク上では、サーバーのドロップダウン リストを展開するよりも、サーバー名を入力する方が簡単な場合があります。 ドロップダウン リストをクリックすると、使用可能なすべてのサーバーがネットワークに照会されるため、時間がかかることがあります。また、結果に目的のサーバーが含まれない可能性もあります。

## <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>.NET Framework Data Provider for SQL Server を使用して SQL Server に接続する 
ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページで **[.NET Framework Data Provider for SQL Server]** を選択すると、そのページにプロバイダーのオプションのグループ化された一覧が表示されます。 これらの多くは、わかりにくい名前となじみのない設定です。 幸い、任意のエンタープライズ データベースに接続するには、通常、いくつかの情報を提供するだけで済みます。 他の設定の既定値は無視できます。

> [!NOTE]
> このデータ プロバイダーの接続オプションは、SQL Server が変換元または変換先の場合でも同じです。 つまり、表示されるオプションは、ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページともに同じです。

|必要な情報|.NET Framework Data Provider for SQL Server プロパティ|
|---|---|
|認証|"統合セキュリティ" として **NotSpecified** が既定で設定されます。または他の認証モードを選択します。 "Active Directory 対話型認証" はサポートされていません。 |
|サーバー名|**データ ソース**|
|認証 (ログイン) 情報|**統合セキュリティ**、または **ユーザー ID** と **パスワード**<br/>サーバー上のデータベースのドロップ ダウン リストを表示する場合は、まず、有効なログイン情報を提供する必要があります。|
|データベース名|**初期カタログ**|

![.NET プロバイダーで SQL に接続する](../../integration-services/import-export-data/media/connect-to-sql-with-net-provider.jpg)

### <a name="options-to-specify-net-framework-data-provider-for-sql-server"></a>指定するオプション (.NET Framework Data Provider for SQL Server)

> [!NOTE]
> このデータ プロバイダーの接続オプションは、SQL Server が変換元または変換先の場合でも同じです。 つまり、表示されるオプションは、ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページともに同じです。

**データ ソース**  
 ソース サーバーまたはターゲット サーバーの名前または IP アドレスを入力するか、ドロップダウン リストからサーバーを選択します。  
 
 非標準の TCP ポートを指定するには、サーバー名または IP アドレスの後にコンマを入力し、ポート番号を入力します。
 
 **初期カタログ**  
 ソース データベースまたはターゲット データベースの名前を入力するか、ドロップダウン リストからデータベースを選択します。  
  
 **統合セキュリティ**  
 **True** を指定して Windows 統合認証を使用して接続するか (推奨)、**False** を指定して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用して接続します。 **False** を指定した場合は、ユーザー ID とパスワードを入力する必要があります。 既定値は **False**です。  
  
 **[ユーザー ID]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合は、ユーザー名を入力します。  
  
 **パスワード**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合は、パスワードを入力します。  

## <a name="connect-to-sql-server-with-the-odbc-driver-for-sql-server"></a>SQL Server 用 ODBC ドライバーを使用して SQL Server に接続する 
ODBC ドライバーは、データ ソースのドロップダウン リストに記載されていません。 ODBC ドライバーを使用して接続するには、最初に **[.NET Framework Data Provider for ODBC]** をデータ ソースとして選択します。 このプロバイダーは、ODBC ドライバーのラッパーとして機能します。

> [!TIP]
> **最新のドライバーを入手します**。 [Microsoft ODBC Driver 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53339) をダウンロードします。

下の図は、.NET Framework Data Provider for ODBC を選んだ直後に表示される一般的な画面です。

![ODBC を使って SQL に接続する (前)](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-sql-server"></a>指定するオプション (SQL Server 用 ODBC ドライバー)

> [!NOTE]
> この ODBC ドライバーの接続オプションは、SQL Server が変換元または変換先の場合でも同じです。 つまり、表示されるオプションは、ウィザードの **[データ ソースの選択]** ページまたは **[変換先の選択]** ページともに同じです。

最新の ODBC ドライバーを使用して SQL Server に接続するには、次の設定とその値を含む接続文字列をアセンブルします。 完全な接続文字列の形式は、リストのすぐ後に示します。

> [!TIP]
> 適切な接続文字列をアセンブルするヘルプを参照してください。 または、接続文字列を提供する代わりに、既存の DSN (データ ソース名) を提供するか、新しく作成します。 これらのオプションの詳細については、「[Connect to an ODBC Data Source](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)」 (ODBC データ ソースに接続する) を参照してください。

**[ドライバー]**  
ODBC ドライバーの名前。 名前は、ドライバーのバージョンによって異なります。

**[サーバー]**  
SQL Server の名前。

**[データベース]**  
データベースの名前。  

**Trusted_Connection**、または **Uid** と **Pwd**  
Windows 統合認証を使用して接続するには **Trusted_Connection=Yes** を指定します。または SQL Server 認証を使用して接続するには **Uid** (ユーザー ID) と **Pwd** (パスワード) を指定します。

### <a name="connection-string-format"></a>接続文字列の形式
Windows 統合認証を使用する接続文字列の形式を次に示します。

    `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;trusted_connection=Yes;`

Windows 統合認証ではなく SQL Server 認証を使用する接続文字列の形式を次に示します。

     `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;uid=<user id>;pwd=<password>;`

### <a name="enter-the-connection-string"></a>接続文字列を入力する
**[データ ソースの選択]** ページまたは **[変換先の選択]** ページで、 **[ConnectionString]** フィールドに接続文字列を入力するか、 **[Dsn]** フィールドに DSN 名を入力します。 接続文字列を入力すると、ウィザードによって文字列が解析され、個々のプロパティとその値が一覧に表示されます。

次の例では、この接続文字列を使用しています。

    `Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;`

接続文字列を入力した後に表示される画面を次に示します。

![ODBC を使って SQL に接続する (後)](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="connect-to-sql-server-with-the-microsoft-ole-db-provider-for-sql-server-or-sql-server-native-client"></a>Microsoft OLE DB Provider for SQL Server または SQL Server Native Client を使用して SQL Server に接続する

> [!IMPORTANT]
> Microsoft OLE DB Provider for SQL Server と SQL Server Native Client は、SQL Server 2012 より後のバージョンではサポートされません。 代わりに、ODBC ドライバーを使用します。 ODBC ドライバーへの移行に関する詳細については、次のブログ記事を参照してください。
>   -   [ODBC のネイティブのリレーショナル データ アクセスへの対応](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)
>   -   [新しい Microsoft ODBC Drivers for SQL Server の概要](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/)

## <a name="other-data-providers-and-more-info"></a>その他のデータ プロバイダーと詳細情報
ここに記載されていないデータ プロバイダーを使用して SQL Server に接続する方法については、「[SQL Server connection strings](https://www.connectionstrings.com/sql-server/)」 (SQL Server 接続文字列) を参照してください。 このサード パーティのサイトには、このページで説明したデータ プロバイダーと接続パラメーターに関する詳細情報も含まれています。

## <a name="see-also"></a>参照
[データ ソースの選択](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[変換先の選択](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

