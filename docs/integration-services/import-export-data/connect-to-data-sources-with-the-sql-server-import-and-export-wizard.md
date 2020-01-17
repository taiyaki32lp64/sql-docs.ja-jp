---
title: SQL Server インポートおよびエクスポート ウィザードを使用してデータ ソースに接続する | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: fd726506-54b7-433b-bf70-3642235b7b31
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cd76d5aa66567dde3c5dc7b5ce4c2c6d787d2136
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296329"
---
# <a name="connect-to-data-sources-with-the-sql-server-import-and-export-wizard"></a>SQL Server インポートおよびエクスポート ウィザードを使用してデータ ソースに接続する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


このセクションのトピックでは、SQL Server インポートおよびエクスポート ウィザードを実行するときに、よく使用されるさまざまなデータ ソースに接続する方法を説明します。 ウィザードの **[データ ソースの選択]** ページと **[変換先の選択]** ページにデータ ソースの接続情報を入力する必要があります。

このセクションのトピックでは、ウィザードの **[データ ソースの選択]** ページと **[変換先の選択]** ページから**データ ソースへの接続**方法についてのみ説明します。 他のものをお探しの場合は、「[関連タスクとコンテンツ](#related)」を参照してください。

## <a name="connect-to-a-commonly-used-data-source"></a>一般的に使用されるデータ ソースへの接続
次のよく使用されるデータ ソースへの接続の詳細については、該当するリンクをクリックしてください。
-   [SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [フラット ファイル (テキスト ファイル)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [アクセス](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Azure Blob Storage](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

## <a name="connect-to-other-data-providers"></a>他のデータ プロバイダーへの接続
この一覧にないデータ ソースに接続する方法については、「[The Connection Strings Reference](https://www.connectionstrings.com/)」(接続文字列リファレンス) をご覧ください。 このサード パーティのサイトには、接続文字列のサンプルと、データ プロバイダーおよび必要な接続情報に関する詳細な情報が記載されています。

## <a name="related"></a> 関連タスクとコンテンツ  
その他の基本的なタスクは次のとおりです。
-   **ウィザードのしくみの簡単な例を参照してください。**

    -   **スクリーン ショットを参照する場合。** この単純なエンド ツー エンドの例を 1 つのページ示した「[簡単な例によるインポートおよびエクスポート ウィザードの概要](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)」をご覧ください。

    -   **ビデオを視聴する場合。** ウィザードを実行し、わかりやすく簡単な手順でデータを Excel にエクスポートする方法を説明した YouTube の 4 分間のビデオ「[SQL Server インポートおよびエクスポート ウィザードを使用して Excel にエクスポートする](https://go.microsoft.com/fwlink/?linkid=829049)」 をご覧ください。

-   **ウィザードのしくみについては、以下を参照してください。**

    -   **ウィザードのしくみについては、以下を参照してください。** ウィザードの概要をお探しの場合は、「 [SQL Server でサポートされるインポートとエクスポートのデータ ソース](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)」を参照してください。

    -   **ウィザードの手順について学習する。** ウィザードの手順についての情報を探している場合は、「[SQL Server インポートおよびエクスポート ウィザードの手順](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)」をご覧ください。 ウィザードのページごとに別のドキュメント ページもあります。

-   **ウィザードを起動します。** ウィザードを実行する準備が整い、開始方法について知りたい場合は、「[SQL Server インポートおよびエクスポート ウィザードを起動する](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)」を参照してください。

-   **ウィザードを取得します。** ウィザードを実行する必要はあるが、コンピューターに [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールしていない場合は、SQL Server Data Tools (SSDT) をインストールすることで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードをインストールできます。 詳細については、「 [SQL Server Data Tools (SSDT) のダウンロード](https://msdn.microsoft.com/library/mt204009.aspx)」を参照してください。

## <a name="see-also"></a>参照
[データ ソースの選択](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[変換先の選択](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


