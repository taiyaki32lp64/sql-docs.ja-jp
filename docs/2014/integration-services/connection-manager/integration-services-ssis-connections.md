---
title: Integration Services (SSIS) の接続 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, connections
- SSIS packages, connections
- sources [Integration Services], connections
- packages [Integration Services], connections
- destinations [Integration Services], connections
- tasks [Integration Services], connections
- connections [Integration Services], about connections
- connections [Integration Services]
- SQL Server Integration Services packages, connections
ms.assetid: 72f5afa3-d636-410b-9e81-2ffa27772a8c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 78c3ba452d3ba681823e5c9f473d7a86f55809a1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833789"
---
# <a name="integration-services-ssis-connections"></a>Integration Services (SSIS) の接続
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージでは接続を使用して、各種のタスクの実行や [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 機能の実装を行います。  
  
-   テキスト、XML、Excel ブック、リレーショナル データベースなど、変換元および変換先のデータ ストアに接続し、データの抽出と読み込みを行います。  
  
-   参照データが含まれたリレーショナル データベースに接続し、完全参照またはあいまい参照を実行します。  
  
-   リレーショナル データベースに接続し、SELECT、DELETE、INSERT コマンドなどの SQL ステートメントやストアド プロシージャを実行します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、データベースのバックアップやログインの転送などのメンテナンス タスクおよび転送タスクを実行します。  
  
-   ログ エントリをテキスト ファイル、XML ファイル、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに書き込み、パッケージの構成を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに書き込みます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、一部の変換作業に使用する一時作業テーブルを作成します。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトおよびデータベースに接続して、データ マイニング モデルにアクセスし、キューブとディメンションを処理して、DDL コードを実行します。  
  
-   Foreach Loop 列挙子およびタスクで使用する既存のファイルとフォルダーを指定するか、新しく作成します。  
  
-   メッセージ キュー、Windows Management Instrumentation (WMI) サーバー、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) サーバー、Web サーバー、およびメール サーバーに接続します。  
  
 これらの接続を確立するために、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は接続マネージャーを使用します。次のセクションでは、この接続マネージャーについて説明します。  
  
## <a name="connection-managers"></a>接続マネージャー  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、接続の論理表現として接続マネージャーが使用されます。 デザイン時に接続マネージャーのプロパティを設定し、パッケージの実行時に [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] が作成する物理接続を指定します。 たとえば、接続マネージャーには、デザイン時に設定する `ConnectionString` プロパティが含まれており、実行時には、接続文字列のプロパティ内の値を使用して、物理接続が作成されます。  
  
 パッケージは、接続マネージャーの種類の複数のインスタンスを使用でき、各インスタンス上でプロパティを設定できます。 実行時に、接続マネージャーの種類の各インスタンスは、さまざまな属性を持つ接続を作成します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、さまざまな種類の接続マネージャーが用意されており、これにより、パッケージはさまざまなデータ ソースおよびサーバーに接続できます。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]のインストール時にセットアップ プログラムによってインストールされる組み込みの接続マネージャー。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] の Web サイトからダウンロード可能な接続マネージャー。  
  
-   カスタム接続マネージャー。既存の接続マネージャーではニーズを満たすことができない場合は独自に作成できます。  
  
### <a name="built-in-connection-managers"></a>組み込みの接続マネージャー  
 次の表は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に用意されている接続マネージャーの種類を一覧にしたものです。  
  
|型|説明|トピック|  
|----------|-----------------|-----------|  
|ADO (ADO)|ActiveX Data Objects (ADO) オブジェクトに接続します。|[ADO 接続マネージャー](ado-connection-manager.md)|  
|ADO.NET|.NET プロバイダーを使用して、データ ソースに接続します。|[ADO.NET 接続マネージャー](ado-net-connection-manager.md)|  
|CACHE|データ フローまたはキャッシュ ファイル (.caw) からデータを読み取り、そのデータをキャッシュ ファイルに保存できます。|[キャッシュ接続マネージャー](cache-connection-manager.md)|  
|DQS|Data Quality Services サーバーとサーバー上の Data Quality Services データベースに接続します。|[DQS クレンジング接続マネージャー](dqs-cleansing-connection-manager.md)|  
|EXCEL|Excel ブック ファイルに接続します。|[Excel 接続マネージャー](excel-connection-manager.md)|  
|FILE|ファイルまたはフォルダーに接続します。|[ファイル接続マネージャー](file-connection-manager.md)|  
|FLATFILE|単一のフラット ファイル内のデータに接続します。|[フラット ファイル接続マネージャー](flat-file-connection-manager.md)|  
|FTP|FTP サーバーに接続します。|[FTP 接続マネージャー](ftp-connection-manager.md)|  
|HTTP|Web サーバーに接続します。|[HTTP 接続マネージャー](http-connection-manager.md)|  
|MSMQ (MSMQ)|メッセージ キューに接続します。|[MSMQ 接続マネージャー](msmq-connection-manager.md)|  
|MSOLAP100|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスまたは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトに接続します。|[Analysis Services 接続マネージャー](analysis-services-connection-manager.md)|  
|MULTIFILE|複数のファイルおよびフォルダーに接続します。|[複数ファイル接続マネージャー](multiple-files-connection-manager.md)|  
|MULTIFLATFILE|複数のデータ ファイルおよびフォルダーに接続します。|[複数フラット ファイル接続マネージャー](multiple-flat-files-connection-manager.md)|  
|OLEDB|OLE DB プロバイダーを使用して、データ ソースに接続します。|[OLE DB 接続マネージャー](ole-db-connection-manager.md)|  
|ODBC|ODBC を使用して、データ ソースに接続します。|[ODBC 接続マネージャー](odbc-connection-manager.md)|  
|SMOServer|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) サーバーに接続します。|[SMO 接続マネージャー](smo-connection-manager.md)|  
|SMTP (SMTP)|SMTP メール サーバーに接続します。|[SMTP 接続マネージャー](smtp-connection-manager.md)|  
|SQLMOBILE|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベースに接続します。|[SQL Server Compact Edition 接続マネージャー](sql-server-compact-edition-connection-manager.md)|  
|WMI (WMI)|サーバーに接続し、サーバー上の Windows Management Instrumentation (WMI) 管理のスコープを指定します。|[WMI 接続マネージャー](wmi-connection-manager.md)|  
  
### <a name="connection-managers-available-for-download"></a>ダウンロード可能な接続マネージャー  
 次の表に、[!INCLUDE[msCoName](../../includes/msconame-md.md)] の Web サイトからダウンロードできるその他の種類の接続マネージャーをリストします。  
  
> [!IMPORTANT]  
>  次の表にリストされている接続マネージャーは、 [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] および [!INCLUDE[ssDeveloperEd11](../../includes/ssdevelopered11-md.md)]でのみ動作します。  
  
|型|説明|トピック|  
|----------|-----------------|-----------|  
|ORACLE|Oracle に接続する\<バージョン情報 > サーバー。|Oracle 接続マネージャーは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Oracle by Attunity の接続マネージャー コンポーネントです。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Oracle by Attunity には、変換元と変換先も含まれます。 詳細については、 [Microsoft Connectors for Oracle and Teradata by Attunity](https://go.microsoft.com/fwlink/?LinkId=251526)のダウンロード ページを参照してください。|  
|SAPBI|SAP NetWeaver BI Version 7 システムに接続します。|SAP BI 接続マネージャーは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for SAP BI の接続マネージャー コンポーネントです。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for SAP BI には、変換元と変換先も含まれます。 詳細については、[Microsoft SQL Server 2008 用 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=262016) のダウンロード ページを参照してください。|  
|TERADATA|Teradata に接続する\<バージョン情報 > サーバー。|Teradata 接続マネージャーは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Teradata by Attunity の接続マネージャー コンポーネントです。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Teradata by Attunity には、変換元と変換先も含まれます。 詳細については、[Microsoft Connectors for Oracle and Teradata by Attunity](https://go.microsoft.com/fwlink/?LinkId=251526) のダウンロード ページを参照してください。|  
  
### <a name="custom-connection-managers"></a>カスタム接続マネージャー  
 カスタム接続マネージャーを作成することもできます。 詳細については、「[カスタム接続マネージャーの開発](../extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 パッケージ内の接続マネージャーを追加または削除する方法の詳細については、「[パッケージの接続マネージャーを追加、削除、または共有する](../add-delete-or-share-a-connection-manager-in-a-package.md)」を参照してください。  
  
 パッケージ内の接続マネージャーのプロパティを設定する方法の詳細については、「[接続マネージャーのプロパティを設定する](../set-the-properties-of-a-connection-manager.md)」を参照してください。  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   technet.microsoft.com のビデオ「[パッケージのパフォーマンスを強化するための Microsoft Attunity Connector for Oracle の活用](https://technet.microsoft.com/sqlserver/gg598963.aspx)」  
  
-   social.technet.microsoft.com の Wiki の記事「[SSIS の接続性](https://social.technet.microsoft.com/wiki/contents/articles/sql-server-integration-services-ssis.aspx#Connectivity)」  
  
-   blogs.msdn.com のブログ「[SSIS から MySQL への接続](https://go.microsoft.com/fwlink/?LinkId=217669)」  
  
-   msdn.microsoft.com の技術記事「[SQL Server Integration Services での SharePoint データの抽出と読み込み](https://go.microsoft.com/fwlink/?LinkId=247826)」  
  
-   support.microsoft.com の技術記事「[SSIS で Oracle 接続マネージャーを使用すると、"DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" というエラー メッセージが表示される](https://go.microsoft.com/fwlink/?LinkId=233696)」  
  
  
