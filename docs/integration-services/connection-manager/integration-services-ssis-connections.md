---
title: Integration Services (SSIS) の接続 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.asvs.connectionmanager.f1
- sql13.dts.designer.adddtsconnection.f1
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3ed4c8c8feacdd41d2e806a4d2d663f639633e07
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294427"
---
# <a name="integration-services-ssis-connections"></a>Integration Services (SSIS) の接続

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、接続の論理表現として接続マネージャーが使用されます。 デザイン時に接続マネージャーのプロパティを設定し、パッケージの実行時に [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] が作成する物理接続を指定します。 たとえば、接続マネージャーには、デザイン時に設定する **ConnectionString** プロパティが含まれており、実行時には、接続文字列のプロパティ内の値を使用して、物理接続が作成されます。  
  
 パッケージは、接続マネージャーの種類の複数のインスタンスを使用でき、各インスタンス上でプロパティを設定できます。 実行時に、接続マネージャーの種類の各インスタンスは、さまざまな属性を持つ接続を作成します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、さまざまな種類の接続マネージャーが用意されており、これにより、パッケージはさまざまなデータ ソースおよびサーバーに接続できます。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]のインストール時にセットアップ プログラムによってインストールされる組み込みの接続マネージャー。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] の Web サイトからダウンロード可能な接続マネージャー。  
  
-   カスタム接続マネージャー。既存の接続マネージャーではニーズを満たすことができない場合は独自に作成できます。  

### <a name="package-level-and-project-level-connection-managers"></a>パッケージ レベルとプロジェクト レベルの接続マネージャー
接続マネージャーは、パッケージ レベルまたはプロジェクト レベルで作成できます。 プロジェクト レベルで作成した接続マネージャーは、プロジェクト内のすべてのパッケージで使用できます。 一方、パッケージ レベルで作成した接続マネージャーは、特定のパッケージでのみ使用できます。  
  
 データ ソースの代わりにプロジェクト レベルで作成された接続マネージャーを使用して、ソースへの接続を共有します。 プロジェクト レベルで接続マネージャーを追加するには、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトでプロジェクト配置モデルを使用する必要があります。 このモデルを使用するようにプロジェクトが構成されている場合、 **[接続マネージャー]** フォルダーが **ソリューション エクスプローラー**に表示され、 **[データ ソース]** フォルダーが **ソリューション エクスプローラー**から削除されます。  
  
> [!NOTE]  
>  パッケージでデータ ソースを使用する場合は、プロジェクトをパッケージ配置モデルに変換する必要があります。  
>   
>  2 つのモデルの詳細とプロジェクト配置モデルへのプロジェクトの変換の詳細については、「[Deploy Integration Services (SSIS) Projects and Packages](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)」 (Integration Services (SSIS) プロジェクトおよびパッケージの展開) を参照してください。

### <a name="built-in-connection-managers"></a>組み込みの接続マネージャー  
 次の表は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に用意されている接続マネージャーの種類を一覧にしたものです。  
  
|型|[説明]|トピック|  
|----------|-----------------|-----------|  
|ADO (ADO)|ActiveX Data Objects (ADO) オブジェクトに接続します。|[ADO 接続マネージャー](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|.NET プロバイダーを使用して、データ ソースに接続します。|[ADO.NET 接続マネージャー](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|CACHE|データ フローまたはキャッシュ ファイル (.caw) からデータを読み取り、そのデータをキャッシュ ファイルに保存できます。|[キャッシュ接続マネージャー](../../integration-services/connection-manager/cache-connection-manager.md)|  
|DQS|Data Quality Services サーバーとサーバー上の Data Quality Services データベースに接続します。|[DQS クレンジング接続マネージャー](../../integration-services/connection-manager/dqs-cleansing-connection-manager.md)|  
|EXCEL|Excel ブック ファイルに接続します。|[Excel 接続マネージャー](../../integration-services/connection-manager/excel-connection-manager.md)|  
|FILE|ファイルまたはフォルダーに接続します。|[ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)|  
|FLATFILE|単一のフラット ファイル内のデータに接続します。|[フラット ファイル接続マネージャー](../../integration-services/connection-manager/flat-file-connection-manager.md)|  
|FTP|FTP サーバーに接続します。|[FTP 接続マネージャー](../../integration-services/connection-manager/ftp-connection-manager.md)|  
|HTTP|Web サーバーに接続します。|[HTTP 接続マネージャー](../../integration-services/connection-manager/http-connection-manager.md)|  
|MSMQ (MSMQ)|メッセージ キューに接続します。|[MSMQ 接続マネージャー](../../integration-services/connection-manager/msmq-connection-manager.md)|  
|MSOLAP100|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスまたは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトに接続します。|[Analysis Services 接続マネージャー](../../integration-services/connection-manager/analysis-services-connection-manager.md)|  
|MULTIFILE|複数のファイルおよびフォルダーに接続します。|[複数ファイル接続マネージャー](../../integration-services/connection-manager/multiple-files-connection-manager.md)|  
|MULTIFLATFILE|複数のデータ ファイルおよびフォルダーに接続します。|[複数フラット ファイル接続マネージャー](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|  
|OLEDB|OLE DB プロバイダーを使用して、データ ソースに接続します。|[OLE DB 接続マネージャー](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|ODBC|ODBC を使用して、データ ソースに接続します。|[ODBC 接続マネージャー](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|SMOServer|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) サーバーに接続します。|[SMO 接続マネージャー](../../integration-services/connection-manager/smo-connection-manager.md)|  
|SMTP (SMTP)|SMTP メール サーバーに接続します。|[SMTP 接続マネージャー](../../integration-services/connection-manager/smtp-connection-manager.md)|  
|SQLMOBILE|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベースに接続します。|[SQL Server Compact Edition 接続マネージャー](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
|WMI (WMI)|サーバーに接続し、サーバー上の Windows Management Instrumentation (WMI) 管理のスコープを指定します。|[WMI 接続マネージャー](../../integration-services/connection-manager/wmi-connection-manager.md)|  
  
### <a name="connection-managers-available-for-download"></a>ダウンロード可能な接続マネージャー  
 次の表に、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] の Web サイトからダウンロードできるその他の種類の接続マネージャーをリストします。  
  
> [!IMPORTANT]  
>  次の表にリストされている接続マネージャーは、 [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] および [!INCLUDE[ssDeveloperEd11](../../includes/ssdevelopered11-md.md)]でのみ動作します。  
  
|型|[説明]|トピック|  
|----------|-----------------|-----------|  
|ORACLE|Oracle \<バージョン情報\> サーバーに接続します。|Oracle 接続マネージャーは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Oracle by Attunity の接続マネージャー コンポーネントです。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Oracle by Attunity には、変換元と変換先も含まれます。 詳細については、 [Microsoft Connectors for Oracle and Teradata by Attunity](https://go.microsoft.com/fwlink/?LinkId=251526)のダウンロード ページを参照してください。|  
|SAPBI|SAP NetWeaver BI Version 7 システムに接続します。|SAP BI 接続マネージャーは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for SAP BI の接続マネージャー コンポーネントです。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for SAP BI には、変換元と変換先も含まれます。 詳細については、[Microsoft SQL Server 2008 用 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=262016) のダウンロード ページを参照してください。|  
|TERADATA|Teradata \<バージョン情報\> サーバーに接続します。|Teradata 接続マネージャーは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Teradata by Attunity の接続マネージャー コンポーネントです。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Teradata by Attunity には、変換元と変換先も含まれます。 詳細については、[Microsoft Connectors for Oracle and Teradata by Attunity](https://go.microsoft.com/fwlink/?LinkId=251526) のダウンロード ページを参照してください。|  
  
### <a name="custom-connection-managers"></a>カスタム接続マネージャー  
 カスタム接続マネージャーを作成することもできます。 詳細については、「 [カスタム接続マネージャーの開発](../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)」を参照してください。  
  
## <a name="create-connection-managers"></a>接続マネージャーを作成する
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、さまざまな種類のサーバーやデータ ソースに接続するタスクのニーズに合わせるため、さまざまな接続マネージャーが用意されています。 接続マネージャーは、データを抽出してさまざまな種類のデータ ストアに読み込むデータ フロー コンポーネントや、ログをサーバー、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブル、またはファイルに書き込むログ プロバイダーによって使用されます。 たとえば、メール送信タスクが含まれるパッケージには、簡易メール転送プロトコル (SMTP) サーバーに接続するタイプの SMTP 接続マネージャーを使用します。 SQL 実行タスクが含まれるパッケージでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに接続する OLE DB 接続マネージャーを使用できます。 詳細については、「[Integration Services (SSIS) の接続](../../integration-services/connection-manager/integration-services-ssis-connections.md)」を参照してください。  
  
 新しいパッケージを作成する際に接続マネージャーを自動的に作成して構成する場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードを使用できます。 このウィザードは、接続マネージャーを使用する変換元および変換先の作成と構成を行う場合に役立ちます。 詳細については、「 [SQL Server データ ツールでのパッケージの作成](../../integration-services/create-packages-in-sql-server-data-tools.md)」を参照してください。  
  
 手動で新しい接続マネージャーを作成して既存のパッケージに追加するには、[!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの **[制御フロー]** タブ、 **[データ フロー]** タブ、および **[イベント ハンドラー]** タブに表示される **[接続マネージャー]** 領域を使用します。 **[接続マネージャー]** 領域で、作成する接続マネージャーの種類を選択し、[!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで用意されているダイアログ ボックスを使用して、接続マネージャーのプロパティを設定します。 詳細については、後の「[接続マネージャー] 領域の使用」を参照してください。  
  
 パッケージに接続マネージャーを追加すると、タスク、Foreach ループ コンテナー、変換元、変換、および変換先で使用できます。 詳細については、「[Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)」、「[Foreach ループ コンテナー](../../integration-services/control-flow/foreach-loop-container.md)」、および「[データ フロー](../../integration-services/data-flow/data-flow.md)」を参照してください。  
  
### <a name="using-the-connection-managers-area"></a>[接続マネージャー] 領域の使用  
 接続マネージャーは、[!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの **[制御フロー]** タブ、 **[データ フロー]** タブ、または **[イベント ハンドラー]** タブがアクティブなときに作成できます。  
  
 次の図は、[!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの **[制御フロー]** タブ上にある **[接続マネージャー]** 領域を示しています。  
  
 ![パッケージの制御フロー デザイナーのスクリーンショット](../../integration-services/connection-manager/media/samplecontrolflow.gif "パッケージの制御フロー デザイナーのスクリーンショット")    
  
### <a name="32-bit-and-64-bit-providers-for-connection-managers"></a>接続マネージャーの 32 ビット プロバイダーと 64 ビット プロバイダー  
 接続マネージャーが使用する多くのプロバイダーには、32 ビット バージョンと 64 ビット バージョンがあります。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のデザイン環境は 32 ビット環境であり、パッケージのデザイン時には 32 ビット プロバイダーのみが表示されます。 したがって、接続マネージャーで特定の 64 ビット プロバイダーが使用されるように構成できるのは、同じプロバイダーの 32 ビット バージョンがインストールされている場合のみです。  
  
 デザイン時に 32 ビット バージョンのプロバイダーを指定したかどうかにかかわらず、実行時には適切なバージョンが使用されます。 パッケージが [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] で実行されている場合でも、64 ビット バージョンのプロバイダーを実行できます。  
  
  どちらのバージョンのプロバイダーも ID は同じです。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ランタイムで使用可能な 64 ビット バージョンのプロバイダーを使用するかどうかを指定するには、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトの Run64BitRuntime プロパティを設定します。 Run64BitRuntime プロパティが **true** に設定されると、ランタイムは 64 ビット プロバイダーを探して使用します。Run64BitRuntime が **false** に設定されると、32 ビット プロバイダーを探して使用します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトで設定できるプロパティの詳細については、「[Integration Services (SSIS) と Studio の環境](https://msdn.microsoft.com/library/ms140028.aspx)」を参照してください。   

## <a name="add-a-connection-manager"></a>接続マネージャーを追加する
###  <a name="wizard"></a> パッケージ作成時に接続マネージャーを追加する  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードを使用します。  
  
     接続マネージャーの作成と構成に加えて、このウィザードでは、接続マネージャーを使用する変換元および変換先の作成と構成を行うこともできます。 詳細については、「 [SQL Server データ ツールでのパッケージの作成](../../integration-services/create-packages-in-sql-server-data-tools.md)」を参照してください。  
  
###  <a name="package"></a> 接続マネージャーを既存のパッケージに追加する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで、 **[制御フロー]** タブ、 **[データ フロー]** タブ、または **[イベント ハンドラー]** タブをクリックして、 **[接続マネージャー]** 領域を表示します。  
  
4.  **[接続マネージャー]** 領域で任意の場所を右クリックし、次のいずれかの操作を行います。  
  
    -   パッケージに追加する接続マネージャーの種類をクリックします。  
  
         \- または -  
  
    -   追加する種類が一覧にない場合は、 **[新しい接続]** をクリックして **[SSIS 接続マネージャーの追加]** ダイアログ ボックスを開き、接続マネージャーの種類を選択してから **[OK]** をクリックします。  
  
     選択した接続マネージャーの種類に応じたカスタム ダイアログ ボックスが開きます。 接続マネージャーの種類と設定可能なオプションの詳細については、次のオプションの表を参照してください。  
  
    |[ODBC 入力元エディター]|オプション|  
    |------------------------|-------------|  
    |[ADO 接続マネージャー](../../integration-services/connection-manager/ado-connection-manager.md)|[[OLE DB 接続マネージャーの構成]](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[ADO.NET 接続マネージャー](../../integration-services/connection-manager/ado-net-connection-manager.md)|[[ADO.NET の接続マネージャーの構成]](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)|  
    |[Analysis Services 接続マネージャー](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[[Analysis Services 接続マネージャーの追加] ダイアログ ボックスの UI リファレンス](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 接続マネージャー](../../integration-services/connection-manager/excel-connection-manager.md)|[Excel 接続マネージャー エディター](../../integration-services/connection-manager/excel-connection-manager-editor.md)|  
    |[ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)|[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
    |[複数ファイル接続マネージャー](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[[ファイル接続マネージャーの追加] ダイアログ ボックスの UI リファレンス](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[フラット ファイル接続マネージャー](../../integration-services/connection-manager/flat-file-connection-manager.md)|[[フラット ファイル接続マネージャー エディター] &#40;[全般] ページ&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)<br /><br /> [[フラット ファイル接続マネージャー エディター] &#40;[列] ページ&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [[フラット ファイル接続マネージャー エディター] &#40;[詳細設定] ページ&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [[フラット ファイル接続マネージャー エディター] ([プレビュー] ページ)](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)|  
    |[複数フラット ファイル接続マネージャー](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[[複数フラット ファイル接続マネージャー エディター] ([全般] ページ)](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [[複数フラット ファイル接続マネージャー エディター] ([列] ページ)](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [[複数フラット ファイル接続マネージャー エディター] ([詳細設定] ページ)](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [[複数フラット ファイル接続マネージャー エディター] &#40;[プレビュー] ページ&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP 接続マネージャー](../../integration-services/connection-manager/ftp-connection-manager.md)|[FTP 接続マネージャー エディター](../../integration-services/connection-manager/ftp-connection-manager-editor.md)|  
    |[HTTP 接続マネージャー](../../integration-services/connection-manager/http-connection-manager.md)|[[HTTP 接続マネージャー エディター] ([サーバー] ページ)](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)<br /><br /> [[HTTP 接続マネージャー エディター] ([プロキシ] ページ)](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ 接続マネージャー](../../integration-services/connection-manager/msmq-connection-manager.md)|[MSMQ 接続マネージャー エディター](../../integration-services/connection-manager/msmq-connection-manager-editor.md)|  
    |[ODBC 接続マネージャー](../../integration-services/connection-manager/odbc-connection-manager.md)|[ODBC 接続マネージャーの UI リファレンス](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB 接続マネージャー](../../integration-services/connection-manager/ole-db-connection-manager.md)|[[OLE DB 接続マネージャーの構成]](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[SMO 接続マネージャー](../../integration-services/connection-manager/smo-connection-manager.md)|[SMO 接続マネージャー エディター](../../integration-services/connection-manager/smo-connection-manager-editor.md)|  
    |[SMTP 接続マネージャー](../../integration-services/connection-manager/smtp-connection-manager.md)|[SMTP 接続マネージャー エディター](../../integration-services/connection-manager/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition 接続マネージャー](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[[SQL Server Compact Edition 接続マネージャー エディター] &#40;[接続] ページ&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [[SQL Server Compact Edition 接続マネージャー エディター] &#40;[すべて] ページ&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI 接続マネージャー](../../integration-services/connection-manager/wmi-connection-manager.md)|[WMI 接続マネージャー エディター](../../integration-services/connection-manager/wmi-connection-manager-editor.md)|  
  
     **[接続マネージャー]** 領域に、追加した接続マネージャーが一覧表示されます。  
  
5.  必要に応じて、接続マネージャーを右クリックし、 **[名前の変更]** をクリックして、接続マネージャーの既定の名前を変更します。  
  
6.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
###  <a name="project"></a> プロジェクト レベルで接続マネージャーを追加する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  **ソリューション エクスプローラー**で **[接続マネージャー]** を右クリックし、 **[新しい接続マネージャー]** をクリックします。  
  
3.  **[SSIS 接続マネージャーの追加]** ダイアログ ボックスで、接続マネージャーの種類を選択し、 **[追加]** をクリックします。  
  
     選択した接続マネージャーの種類に応じたカスタム ダイアログ ボックスが開きます。 接続マネージャーの種類と設定可能なオプションの詳細については、次のオプションの表を参照してください。  
  
    |[ODBC 入力元エディター]|オプション|  
    |------------------------|-------------|  
    |[ADO 接続マネージャー](../../integration-services/connection-manager/ado-connection-manager.md)|[[OLE DB 接続マネージャーの構成]](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[ADO.NET 接続マネージャー](../../integration-services/connection-manager/ado-net-connection-manager.md)|[[ADO.NET の接続マネージャーの構成]](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)|  
    |[Analysis Services 接続マネージャー](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[[Analysis Services 接続マネージャーの追加] ダイアログ ボックスの UI リファレンス](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 接続マネージャー](../../integration-services/connection-manager/excel-connection-manager.md)|[Excel 接続マネージャー エディター](../../integration-services/connection-manager/excel-connection-manager-editor.md)|  
    |[ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)|[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
    |[複数ファイル接続マネージャー](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[[ファイル接続マネージャーの追加] ダイアログ ボックスの UI リファレンス](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[フラット ファイル接続マネージャー](../../integration-services/connection-manager/flat-file-connection-manager.md)|[[フラット ファイル接続マネージャー エディター] &#40;[全般] ページ&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)<br /><br /> [[フラット ファイル接続マネージャー エディター] &#40;[列] ページ&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [[フラット ファイル接続マネージャー エディター] &#40;[詳細設定] ページ&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [[フラット ファイル接続マネージャー エディター] ([プレビュー] ページ)](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)|  
    |[複数フラット ファイル接続マネージャー](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[[複数フラット ファイル接続マネージャー エディター] ([全般] ページ)](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [[複数フラット ファイル接続マネージャー エディター] ([列] ページ)](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [[複数フラット ファイル接続マネージャー エディター] ([詳細設定] ページ)](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [[複数フラット ファイル接続マネージャー エディター] &#40;[プレビュー] ページ&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP 接続マネージャー](../../integration-services/connection-manager/ftp-connection-manager.md)|[FTP 接続マネージャー エディター](../../integration-services/connection-manager/ftp-connection-manager-editor.md)|  
    |[HTTP 接続マネージャー](../../integration-services/connection-manager/http-connection-manager.md)|[[HTTP 接続マネージャー エディター] ([サーバー] ページ)](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)<br /><br /> [[HTTP 接続マネージャー エディター] ([プロキシ] ページ)](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ 接続マネージャー](../../integration-services/connection-manager/msmq-connection-manager.md)|[MSMQ 接続マネージャー エディター](../../integration-services/connection-manager/msmq-connection-manager-editor.md)|  
    |[ODBC 接続マネージャー](../../integration-services/connection-manager/odbc-connection-manager.md)|[ODBC 接続マネージャーの UI リファレンス](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB 接続マネージャー](../../integration-services/connection-manager/ole-db-connection-manager.md)|[[OLE DB 接続マネージャーの構成]](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[SMO 接続マネージャー](../../integration-services/connection-manager/smo-connection-manager.md)|[SMO 接続マネージャー エディター](../../integration-services/connection-manager/smo-connection-manager-editor.md)|  
    |[SMTP 接続マネージャー](../../integration-services/connection-manager/smtp-connection-manager.md)|[SMTP 接続マネージャー エディター](../../integration-services/connection-manager/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition 接続マネージャー](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[[SQL Server Compact Edition 接続マネージャー エディター] &#40;[接続] ページ&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [[SQL Server Compact Edition 接続マネージャー エディター] &#40;[すべて] ページ&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI 接続マネージャー](../../integration-services/connection-manager/wmi-connection-manager.md)|[WMI 接続マネージャー エディター](../../integration-services/connection-manager/wmi-connection-manager-editor.md)|  
  
     追加した接続マネージャーが、 **ソリューション エクスプローラー** の **[接続マネージャー]** ノードの下に表示されます。 また、プロジェクト内のすべてのパッケージの **[SSIS デザイナー]** ウィンドウの **[接続マネージャー]** タブにも表示されます。 このタブに表示される接続マネージャーの名前の前には **(プロジェクト)** と表記され、パッケージ レベルの接続マネージャーと区別されます。  
  
4.  必要に応じて、 **[ソリューション マネージャー]** ウィンドウの **[接続マネージャー]** ノードまたは **[SSIS デザイナー]** ウィンドウの **[接続マネージャー]** タブで接続マネージャーを右クリックし、 **[名前の変更]** をクリックして、接続マネージャーの既定の名前を変更します。  
  
    > [!NOTE]  
    >  **[SSIS デザイナー]** ウィンドウの **[接続マネージャー]** タブでは、接続マネージャーの名前の前に表示されている **(プロジェクト)** を上書きすることはできません。 これは仕様です。  

### <a name="add-ssis-connection-manager-dialog-box"></a>[SSIS 接続マネージャーの追加] ダイアログ ボックス
**[SSIS 接続マネージャーの追加]** ダイアログ ボックスを使用すると、パッケージに追加する接続の種類を選択できます。  
  
 接続マネージャーの詳細については、「[Integration Services &#40;SSIS&#41; の接続](../../integration-services/connection-manager/integration-services-ssis-connections.md)」を参照してください。  
  
#### <a name="options"></a>オプション  
 **[接続マネージャーの種類]**  
 エディターを使用して接続の種類の接続プロパティを指定するには、接続の種類を選択して **[追加]** をクリックするか、接続の種類をダブルクリックします。  
  
 **[追加]**  
 エディターを使用して、接続の種類に対応する接続プロパティを指定します。  
   
##  <a name="parameter"></a> 接続マネージャーのプロパティのパラメーターを作成する  
  
1.  **[接続マネージャー]** 領域で、パラメーターを作成する接続マネージャーを右クリックし、 **[パラメーター化]** をクリックします。  
  
2.  **[パラメーター化]** ダイアログ ボックスでパラメーター設定を構成します。 詳細については、「 [[パラメーター化] ダイアログ ボックス](https://msdn.microsoft.com/library/fac02b6d-d247-447a-8940-e8700c7ac350)」を参照してください。  

## <a name="delete-a-connection-manager"></a>接続マネージャーを削除する 
###  <a name="DeletePackageLevel"></a> パッケージから接続マネージャーを削除する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで、 **[制御フロー]** タブ、 **[データ フロー]** タブ、または **[イベント ハンドラー]** タブをクリックして、 **[接続マネージャー]** 領域を表示します。  
  
4.  削除する接続マネージャーを右クリックして、 **[削除]** をクリックします。  
  
     SQL 実行タスクや OLE DB ソースなどのパッケージ要素が使用している接続マネージャーを削除すると、結果は次のようになります。  
  
    -   削除された接続マネージャーを使用していたパッケージ要素にエラー アイコンが表示されます。  
  
    -   パッケージの検証に失敗します。  
  
    -   パッケージを実行できません。  
  
5.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
###  <a name="DeleteProjectLevel"></a> 共有接続マネージャー (プロジェクト レベルの接続マネージャー) を削除する  
  
1.  プロジェクト レベルの接続マネージャーを削除するには、 **[ソリューション エクスプローラー]** ウィンドウの **[接続マネージャー]** ノードで接続マネージャーを右クリックし、 **[削除]** をクリックします。 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] で次のような警告メッセージが表示されます。  
  
    > [!WARNING]  
    >  プロジェクト接続マネージャーを削除すると、その接続マネージャーを使用するパッケージが動作しなくなる場合があります。 この操作を元に戻すことはできません。 接続マネージャーを削除しますか。  
  
2.  接続マネージャーを削除するには [OK] をクリックし、削除しない場合は [キャンセル] をクリックします。  
  
    > [!NOTE]  
    >  プロジェクトのパッケージに対して開いた **[SSIS デザイナー]** ウィンドウの **[接続マネージャー]** タブから、プロジェクト レベルの接続マネージャーを削除することもできます。 そのためには、タブで接続マネージャーを右クリックし、 **[削除]** をクリックします。 
    
## <a name="set-the-properties-of-a-connection-manager"></a>接続マネージャーのプロパティを設定する
すべての接続マネージャーは **[プロパティ]** ウィンドウを使用して構成できます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のさまざまな種類の接続マネージャーを変更するためのカスタム ダイアログ ボックスも用意されています。 ダイアログ ボックスに表示されるオプションは、接続マネージャーの種類によって異なります。  
  
### <a name="modify-a-connection-manager-using-the-properties-window"></a>[プロパティ] ウィンドウを使用して接続マネージャーを変更する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  SSIS デザイナーで、 **[制御フロー]** タブ、 **[データ フロー]** タブ、または **[イベント ハンドラー]** タブをクリックして、 **[接続マネージャー]** 領域を表示します。  
  
4.  接続マネージャーを右クリックして、 **[プロパティ]** をクリックします。  
  
5.  **[プロパティ]** ウィンドウで、プロパティの値を編集します。 **[プロパティ]** ウィンドウでは、接続マネージャーの標準エディターで構成できないプロパティにもアクセスできます。  
  
6.  **[OK]** をクリックします。  
  
7.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
### <a name="modify-a-connection-manager-using-a-connection-manager-dialog-box"></a>接続マネージャーのダイアログ ボックスを使用して接続マネージャーを変更する  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで、 **[制御フロー]** タブ、 **[データ フロー]** タブ、または **[イベント ハンドラー]** タブをクリックして、 **[接続マネージャー]** 領域を表示します。  
  
4.  **[接続マネージャー]** 領域で接続マネージャーをダブルクリックして、 **[接続マネージャー]** ダイアログ ボックスを開きます。 特定の種類の接続マネージャーおよび各種類で使用するオプションの詳細については、次の表を参照してください。  
  
    |[接続マネージャー]|オプション|  
    |------------------------|-------------|  
    |[ADO 接続マネージャー](../../integration-services/connection-manager/ado-connection-manager.md)|[[OLE DB 接続マネージャーの構成]](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[ADO.NET 接続マネージャー](../../integration-services/connection-manager/ado-net-connection-manager.md)|[[ADO.NET の接続マネージャーの構成]](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)|  
    |[Analysis Services 接続マネージャー](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[[Analysis Services 接続マネージャーの追加] ダイアログ ボックスの UI リファレンス](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 接続マネージャー](../../integration-services/connection-manager/excel-connection-manager.md)|[Excel 接続マネージャー エディター](../../integration-services/connection-manager/excel-connection-manager-editor.md)|  
    |[ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)|[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
    |[複数ファイル接続マネージャー](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[[ファイル接続マネージャーの追加] ダイアログ ボックスの UI リファレンス](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[フラット ファイル接続マネージャー](../../integration-services/connection-manager/flat-file-connection-manager.md)|[[フラット ファイル接続マネージャー エディター] &#40;[全般] ページ&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)<br /><br /> [[フラット ファイル接続マネージャー エディター] &#40;[列] ページ&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [[フラット ファイル接続マネージャー エディター] &#40;[詳細設定] ページ&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [[フラット ファイル接続マネージャー エディター] ([プレビュー] ページ)](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)|  
    |[複数フラット ファイル接続マネージャー](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[[複数フラット ファイル接続マネージャー エディター] ([全般] ページ)](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [[複数フラット ファイル接続マネージャー エディター] ([列] ページ)](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [[複数フラット ファイル接続マネージャー エディター] ([詳細設定] ページ)](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [[複数フラット ファイル接続マネージャー エディター] &#40;[プレビュー] ページ&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP 接続マネージャー](../../integration-services/connection-manager/ftp-connection-manager.md)|[FTP 接続マネージャー エディター](../../integration-services/connection-manager/ftp-connection-manager-editor.md)|  
    |[HTTP 接続マネージャー](../../integration-services/connection-manager/http-connection-manager.md)|[[HTTP 接続マネージャー エディター] ([サーバー] ページ)](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)<br /><br /> [[HTTP 接続マネージャー エディター] ([プロキシ] ページ)](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ 接続マネージャー](../../integration-services/connection-manager/msmq-connection-manager.md)|[MSMQ 接続マネージャー エディター](../../integration-services/connection-manager/msmq-connection-manager-editor.md)|  
    |[ODBC 接続マネージャー](../../integration-services/connection-manager/odbc-connection-manager.md)|[ODBC 接続マネージャーの UI リファレンス](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB 接続マネージャー](../../integration-services/connection-manager/ole-db-connection-manager.md)|[[OLE DB 接続マネージャーの構成]](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[SMO 接続マネージャー](../../integration-services/connection-manager/smo-connection-manager.md)|[SMO 接続マネージャー エディター](../../integration-services/connection-manager/smo-connection-manager-editor.md)|  
    |[SMTP 接続マネージャー](../../integration-services/connection-manager/smtp-connection-manager.md)|[SMTP 接続マネージャー エディター](../../integration-services/connection-manager/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition 接続マネージャー](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[[SQL Server Compact Edition 接続マネージャー エディター] &#40;[接続] ページ&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [[SQL Server Compact Edition 接続マネージャー エディター] &#40;[すべて] ページ&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI 接続マネージャー](../../integration-services/connection-manager/wmi-connection-manager.md)|[WMI 接続マネージャー エディター](../../integration-services/connection-manager/wmi-connection-manager-editor.md)|  
  
5.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  

## <a name="related-content"></a>関連コンテンツ  
  
-   technet.microsoft.com のビデオ「[パッケージのパフォーマンスを強化するための Microsoft Attunity Connector for Oracle の活用](https://technet.microsoft.com/sqlserver/gg598963.aspx)」  
  
-   social.technet.microsoft.com の Wiki の記事「[SSIS の接続性](https://social.technet.microsoft.com/wiki/contents/articles/sql-server-integration-services-ssis.aspx#Connectivity)」  
  
-   blogs.msdn.com のブログ「[SSIS から MySQL への接続](https://go.microsoft.com/fwlink/?LinkId=217669)」  
  
-   msdn.microsoft.com の技術記事「[SQL Server Integration Services での SharePoint データの抽出と読み込み](https://go.microsoft.com/fwlink/?LinkId=247826)」  
  
-   support.microsoft.com の技術記事「[SSIS で Oracle 接続マネージャーを使用すると、"DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" というエラー メッセージが表示される](https://go.microsoft.com/fwlink/?LinkId=233696)」  
  
  
