---
title: 変換先の選択 (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 86b2cf26c7af957579c5368ed70262e43db005f1
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285877"
---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>[変換先の選択] (SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 データ ソースとデータへの接続方法を指定すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードには、 **[変換先の選択]** が表示されます。 このページでは、データの変換先およびデータに接続する方法についての情報を指定します。
  
使用できるデータの変換先の詳細については、「 [使用できるデータ ソースと変換先](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)」を参照してください。 

## <a name="screen-shot-of-the-destination-page"></a>[変換先] ページのスクリーン ショット
次のスクリーンショットは、ウィザードの **[変換先の選択]** ページの最初の部分を示しています。 ページの残りの部分には、ここで選択した変換先に応じて変わるさまざまなオプションがあります。

![変換先の選択](../../integration-services/import-export-data/media/choose-destination.png)

## <a name="choose-a-destination"></a>[変換先の選択]
 **変換先**  
 変換先を指定するには、変換先にデータをインポートすることができるデータ プロバイダーを選択します。
 
-   **必要なデータ プロバイダーは通常、その名前で判断できます**。プロバイダーの名前には通常、変換先の名前が含まれているからです。例: *フラット ファイル*変換先、Microsoft *Excel*、Microsoft *Access*、.NET Framework Data Provider for *SqlServer*、.NET Framework Data Provider for *Oracle* など。

-   **変換先で ODBC ドライバーを使用している場合は**、.NET Framework Data Provider for ODBC を選択します。 ドライバー固有の情報を入力します。 ODBC ドライバーは、変換先のドロップダウン リストに記載されていません。 .NET Framework Data Provider for ODBC は ODBC ドライバーのラッパーとして機能します。 詳細については、「[ODBC データ ソースに接続する](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)」をご覧ください。

-   **変換先として使用できるプロバイダーが複数存在する可能性があります。** 通常、変換先で使用できる任意のプロバイダーを選択できます。 たとえば、Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続するには、.NET Framework Data Provider for SQL Server、または SQL Server ODBC ドライバーを使用できます (その他のプロバイダーもリストに表示されますが、現在はサポートされていません)。 

## <a name="my-destination-isnt-in-the-list"></a>変換先がリストに表示されない
-   Microsoft またはサード パーティから**データ プロバイダーをダウンロードする必要があります**。 **[変換先]** のリストに表示される、使用できるデータ プロバイダーのリストに含まれているのは、コンピューターにインストールされているプロバイダーのみです。 使用できる変換先の詳細については、「[使用できるデータ ソースと変換先](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)」を参照してください。

-   **変換先の ODBC ドライバーがありますか。** ODBC ドライバーは、変換先のドロップダウン リストに記載されていません。 変換先で ODBC ドライバーを使用している場合は、.NET Framework Data Provider for ODBC を選択します。 ドライバー固有の情報を入力します。 .NET Framework Data Provider for ODBC は ODBC ドライバーのラッパーとして機能します。 詳細については、「[ODBC データ ソースに接続する](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)」をご覧ください。

-   **64 ビットと 32 ビットのプロバイダー。** 64 ビットのウィザードを実行している場合、32 ビット プロバイダーしかインストールされていない変換先は表示されません。その逆も同様です。

> [!NOTE]
> 64 ビット バージョンの SQL Server インポートおよびエクスポート ウィザードを使用するには、SQL Server をインストールする必要があります。 SQL Server Data Tools (SSDT) および SQL Server Management Studio (SSMS) は 32 ビット アプリケーションであり、32 ビット バージョンのウィザードを含む、32 ビット ファイルのみがインストールされます。

## <a name="after-you-choose-a-destination"></a>変換先の選択後
変換先を選択した後、 **[変換先の選択]** ページ の残りの部分で指定するオプションの数は、選択したデータ プロバイダーによって異なります。

よく使われる変換先に接続するには、次のいずれかのページをご覧ください。
-   [SQL Server への接続](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Oracle への接続](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [フラット ファイル (テキスト ファイル) への接続](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Excel への接続](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Access への接続](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [ODBC への接続](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Azure Blob Storage への接続](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [PostgreSQL への接続](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [MySQL への接続](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

この一覧にない変換先に接続する方法については、「[The Connection Strings Reference](https://www.connectionstrings.com/)」(接続文字列リファレンス) をご覧ください。 このサード パーティのサイトには、接続文字列のサンプルと、データ プロバイダーおよび必要な接続情報に関する詳細な情報が記載されています。

## <a name="whats-next"></a>次の操作  
 データの変換先とデータへの接続方法を指定した後、次のページは、 **[テーブルのコピーまたはクエリの指定]** です。 このページでは、テーブル全体をコピーするか、特定の行のみをコピーするかを指定します。 詳細については、「 [テーブルのコピーまたはクエリの指定](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)」を参照してください。  

## <a name="see-also"></a>参照
[簡単な例によるインポートおよびエクスポート ウィザードの概要](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


