---
title: '[データ ソースの選択] (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs'
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.chooseadatasource.f1
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b707b2b31c15c565353f0ff581ca1f4d7308a25b
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71951938"
---
# <a name="choose-a-data-source-sql-server-import-and-export-wizard"></a>[データ ソースの選択] (SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [ようこそ] ページの後、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードに **[データ ソースを選ぶ]** が表示されます。 このページでは、データ ソースおよびデータに接続する方法についての情報を指定します。
  
使用できるデータ ソースの詳細については、「 [どのようなデータ ソースと変換先を使用できるでしょうか。](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)」を参照してください。

> [!NOTE]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードでは、SQL Server Integration Services (SSIS) が利用されます。 そのため、SSIS に適用されるものと同じ制限事項がウィザードにも適用されます。  たとえば、「[データの処理エラー](../../integration-services/data-flow/error-handling-in-data.md)」で説明されているように既定で追加される ErrorCode 列や ErrorColumn 列などです。

## <a name="screen-shot-of-the-choose-a-data-source-page"></a>[データ ソースの選択] ページのスクリーン ショット 
次のイメージは、ウィザードの **[データ ソースの選択]** ページの最初の部分を示しています。 ページの残りの部分には、ここで選択したデータ ソースに応じて変わるさまざまなオプションがあります。

![ソースの選択](../../integration-services/import-export-data/media/choose-source.png)

## <a name="choose-a-data-source"></a>[データ ソースを選ぶ]
 **データ ソース**  
データ ソースを指定するには、ソースに接続することができるデータ プロバイダーを選択します。

-   **必要なデータ プロバイダーは通常、その名前で判断できます**。プロバイダーの名前には通常、データ ソースの名前が含まれているからです。例: *フラット ファイル* ソース、Microsoft *Excel*、Microsoft *Access*、.NET Framework Data Provider for *SqlServer*、.NET Framework Data Provider for *Oracle* など。

-   **データ ソースで ODBC ドライバーを使用している場合は**、.NET Framework Data Provider for ODBC を選択します。 ドライバー固有の情報を入力します。 ODBC ドライバーは、データ ソースのドロップダウン リストに記載されていません。 .NET Framework Data Provider for ODBC は ODBC ドライバーのラッパーとして機能します。 詳細については、「[ODBC データ ソースに接続する](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)」をご覧ください。

-   **データ ソースに使用できるプロバイダーが複数存在する可能性があります。** 通常、ソースで使用できる任意のプロバイダーを選択できます。 たとえば、Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続するには、.NET Framework Data Provider for SQL Server、または SQL Server ODBC ドライバーを使用できます (その他のプロバイダーもリストに表示されますが、現在はサポートされていません)。 

## <a name="my-data-source-isnt-in-the-list"></a>データ ソースがリストにない
-   Microsoft またはサード パーティから**データ プロバイダーをダウンロードする必要があります**。 **[データ ソース]** のリストに表示される、使用できるデータ プロバイダーのリストに含まれているのは、コンピューターにインストールされているプロバイダーのみです。 使用できるデータ ソースの詳細については、「 [どのようなデータ ソースと変換先を使用できるでしょうか。](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)」を参照してください。

-   **データ ソースの ODBC ドライバーがありますか。** ODBC ドライバーは、データ ソースのドロップダウン リストに記載されていません。 データ ソースで ODBC ドライバーを使用している場合は、.NET Framework Data Provider for ODBC を選択します。 ドライバー固有の情報を入力します。 .NET Framework Data Provider for ODBC は ODBC ドライバーのラッパーとして機能します。 詳細については、「[ODBC データ ソースに接続する](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)」をご覧ください。

-   **64 ビットと 32 ビットのプロバイダー。** 64 ビットのウィザードを実行している場合、32 ビット プロバイダーしかインストールされていないデータ ソースは表示されません。その逆も同様です。

> [!NOTE]
> 64 ビット バージョンの SQL Server インポートおよびエクスポート ウィザードを使用するには、SQL Server をインストールする必要があります。 SQL Server Data Tools (SSDT) および SQL Server Management Studio (SSMS) は 32 ビット アプリケーションであり、32 ビット バージョンのウィザードを含む、32 ビット ファイルのみがインストールされます。

## <a name="after-you-choose-a-data-source"></a>データ ソースの選択後
データソースを選択した後、 **[データ ソースを選ぶ]** ページ プロパティの残りの部分で指定するオプションの数は、選択したデータ プロバイダーによって異なります。

よく使われるデータ ソースに接続するには、次のいずれかのページをご覧ください。
-   [SQL Server への接続](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Oracle への接続](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [フラット ファイル (テキスト ファイル) への接続](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Excel への接続](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Access への接続](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [ODBC への接続](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Azure Blob Storage への接続](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [PostgreSQL への接続](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [MySQL への接続](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

この一覧にないデータ ソースに接続する方法については、「[The Connection Strings Reference](https://www.connectionstrings.com/)」(接続文字列リファレンス) をご覧ください。 このサード パーティのサイトには、接続文字列のサンプルと、データ プロバイダーおよび必要な接続情報に関する詳細な情報が記載されています。

## <a name="whats-next"></a>次の操作
 データ ソースとデータへの接続方法を指定したら、 **[変換先の選択]** ページに進みます。 このページでは、データの変換先およびデータに接続する方法についての情報を指定します。 詳細については、「 [[変換先の選択] (SQL Server インポートおよびエクスポート ウィザード)](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)」をご覧ください。

## <a name="see-also"></a>参照
[簡単な例によるインポートおよびエクスポート ウィザードの概要](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../../includes/paragraph-content/contribute-to-content.md)]
