---
title: SQL Server インポートおよびエクスポート ウィザードを使用してデータをインポートおよびエクスポートする | Microsoft Docs
ms.custom: ''
ms.date: 10/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- exporting data
- mapping files [Integration Services]
- SQL Server Import and Export Wizard
- SSIS packages, creating
- packages [Integration Services], copying
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
- Import and Export Wizard
- copying data [Integration Services]
- importing data, SSIS packages
- sources [Integration Services], copying data
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2e8838c92e2af7ca79ad1aa69972e46be0a1f64c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296276"
---
# <a name="import-and-export-data-with-the-sql-server-import-and-export-wizard"></a>SQL Server インポートおよびエクスポート ウィザードを使用してデータをインポートおよびエクスポートする

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードは、変換元から変換先にデータをコピーするための単純な方法です。 この概要では、ウィザードで変換元および変換先として使うことができるデータ ソースと、ウィザードを実行するために必要なアクセス許可について説明します。

## <a name="get-the-wizard"></a>ウィザードを入手する
ウィザードを実行する必要はあるが、コンピューターに [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールしていない場合は、SQL Server Data Tools (SSDT) をインストールすることで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードをインストールできます。 詳細については、「 [SQL Server Data Tools (SSDT) のダウンロード](https://msdn.microsoft.com/library/mt204009.aspx)」を参照してください。

## <a name="what-happens-when-i-run-the-wizard"></a>ウィザードを実行したときの動作
-    **手順の一覧を見る。** ウィザードの手順の説明については、「[SQL Server インポートおよびエクスポート ウィザードの手順](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)」をご覧ください。 ウィザードのページごとに別のドキュメント ページもあります。  
    \- または \-
-   **例を見る。** 一般的なセッションで表示される複数の画面を簡単に確認するには、この簡単な例を 1 つのページで示した「[簡単な例によるインポートおよびエクスポート ウィザードの概要](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)」をご覧ください。  

##  <a name="wizardSources"></a> 使用できる変換元と変換先  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードは、次の表のデータ ソースをデータのコピー元およびコピー先として使うことができます。 一部のデータ ソースに接続するには、追加ファイルをダウンロードしてインストールする必要があります。
 
| データ ソース | 追加ファイルをダウンロードする必要があるかどうか |
|-------------|-----------------------------------------|
|**エンタープライズ データベース**<br/>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Oracle、DB2、その他。|SQL Server または SQL Server Data Tools (SSDT) は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続に必要なファイルをインストールします。 ただし、SSDT では、Oracle や IBM DB2 などの他のエンタープライズ データベースへの接続に必要なすべてのファイルはインストールされません。<br/><br/>エンタープライズ データベースに接続するには、通常、2 つのものが必要です。<br/><br/>1.**クライアント ソフトウェア**。 エンタープライズ データベース システム用のクライアント ソフトウェアを既にインストールしている場合、通常は接続するために必要なファイルは用意されています。 クライアント ソフトウェアをインストールしていない場合は、ライセンス コピーのインストール方法をデータベース管理者に問い合わせください。<br/><br/>2.**ドライバーまたはプロバイダー**。 Microsoft は、Oracle に接続するためのドライバーとプロバイダーをインストールします。 IBM DB2 に接続するには、MicrosoftÂ® OLEDB Provider for DB2 v5.0 for Microsoft SQL Server を [Microsoft SQL Server 2016 Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676) から入手する必要があります。<br/><br/>詳しくは、「[SQL Server データ ソースに接続する](connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)」または「[Oracle データ ソースに接続する](connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)」をご覧ください。|
|**テキスト ファイル** (フラット ファイル)|追加ファイルは必要ありません。<br/><br/>詳しくは、「[フラット ファイル データ ソースに接続する](connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)」をご覧ください。|
|**Microsoft Excel ファイルと Microsoft Access ファイル**|Microsoft Office は、Excel と Access のファイルにデータ ソースとして接続するために必要なすべてのファイルはインストールしません。 次のダウンロードを入手します - [Microsoft Access データベース エンジン 2016 再頒布可能パッケージ](https://www.microsoft.com/download/details.aspx?id=54920)。<br/><br/>詳しくは、「[Excel データ ソースに接続する](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)」または「[Access データ ソースに接続する](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)」をご覧ください。|
|**Azure データ ソース**<br/>現在 Azure BLOB ストレージのみ。|SQL Server Data Tools では、Azure BLOB Storage にデータ ソースとして接続するために必要なファイルはインストールされません。 次のダウンロードを取得してください - [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=49492)。<br/><br/>詳細については、「[Azure Blob Storage に接続する](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)」を参照してください。|
|**オープン ソース データベース**<br/>PostgreSQL、MySql、その他。|これらのデータ ソースに接続するには、追加ファイルをダウンロードする必要があります。<br/><br/>- **PostgreSQL** の場合は、「[PostgreSQL データ ソースに接続する](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)」をご覧ください。<br/>- **MySql** の場合は、「[MySQL データ ソースに接続する](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)」をご覧ください。|
|**ドライバーまたはプロバイダーを入手できるその他のデータ ソース**|通常、次の種類のデータ ソースに接続するために追加ファイルをダウンロードする必要があります。<br/><br/>- **ODBC ドライバー** を使用できるソース。 詳細については、「[ODBC データ ソースに接続する](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)」をご覧ください。<br/>- **.Net Framework Data Provider** を使用できるソース。<br/>- **OLE DB プロバイダー** を使用できるソース。<br/><br/>他のデータ ソースに変換元と変換先の機能を提供するサード パーティ製のコンポーネントが、SQL Server Integration Services (SSIS) 用のアドオン製品として販売されている場合があります。|

## <a name="how-do-i-connect-to-my-data"></a>データに接続する方法
よく使われるデータ ソースに接続する方法については、次のいずれかのページをご覧ください。
-   [SQL Server への接続](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Oracle への接続](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [フラット ファイル (テキスト ファイル) への接続](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Excel への接続](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Access への接続](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Azure Blob Storage への接続](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [ODBC への接続](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [PostgreSQL への接続](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [MySQL への接続](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)


この一覧にないデータ ソースに接続する方法については、「[The Connection Strings Reference](https://www.connectionstrings.com/)」(接続文字列リファレンス) をご覧ください。 このサード パーティのサイトには、接続文字列のサンプルと、データ プロバイダーおよび必要な接続情報に関する詳細な情報が記載されています。

## <a name="what-permissions-do-i-need"></a>必要なアクセス許可  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードを実行するには、少なくとも次の権限が必要です。 データ ソースと変換先で既に作業をしている場合は、必要な権限を既に持っている可能性があります。
  
|実行するには権限が必要な操作|SQL Server に接続している場合に必要な特定のアクセス許可 |  
|-------------------------|----------------------------------------------------|  
|変換元および変換先のデータベースまたはファイル共有に接続する。|サーバーおよびデータベースへのログイン権限。|  
|変換元のデータベースまたはファイルからデータをエクスポートする、または読み取る。|変換元のテーブルおよびビューに対する SELECT 権限。|  
|変換先のデータベースまたはファイルにデータをインポートする、または書き込む。|変換先のテーブルに対する INSERT 権限。|  
|変換先データベースまたはファイルを作成する (該当する場合)。|CREATE DATABASE 権限または CREATE TABLE 権限。|  
|ウィザードによって作成された SSIS パッケージを保存する (該当する場合)。|パッケージを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に保存する場合は、 **msdb** データベースにパッケージを保存するのに十分な権限。|  
  
## <a name="get-help-while-the-wizard-is-running"></a>ウィザードの実行中にヘルプを得る
> [!TIP]
> ウィザードのページまたはダイアログ ボックスで F1 キーをタップすると、現在のページの文書が表示されます。   
  
##  <a name="wizardSSIS"></a> ウィザードは SQL Server Integration Services (SSIS) を使用する  
 ウィザードは SQL Server Integration Services (SSIS) を使用してデータをコピーします。 SSIS は、データの抽出、変換、および読み込み (ETL) を行うツールです。 ウィザードの各ページでは、SSIS の言語の一部を使用します。
  
 SSIS での基本単位は **パッケージ**です。 ウィザードのページを進みながらオプションを指定すると、SSIS パッケージがメモリに作成されます。    
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition 以降をインストールしている場合は、ウィザードの最後に、必要に応じて SSIS パッケージを保存することもできます。 後でパッケージを再使用したり、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーを使用してタスク、変換、イベント ドリブン ロジックを追加することでパッケージを拡張したりできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードは、データを変換元から変換先にコピーする基本的な [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを作成するための最も簡単な方法です。

詳細については、「 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)」を参照してください。

## <a name="whats-next"></a>次の操作  
 ウィザードを開始します。 詳細については、「 [Start the SQL Server Import and Export Wizard](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)」(SQL Server インポートおよびエクスポート ウィザードを開始する) を参照してください。  

## <a name="see-also"></a>参照
[簡単な例によるインポートおよびエクスポート ウィザードの概要](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)  
[SQL Server インポートおよびエクスポート ウィザードのデータ型マッピング](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)


