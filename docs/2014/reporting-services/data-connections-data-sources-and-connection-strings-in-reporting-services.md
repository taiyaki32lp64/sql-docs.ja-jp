---
title: Reporting Services のデータ接続、データソース、および接続文字列 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- connections [Reporting Services], data sources
- reports [Reporting Services], data
- expressions [Reporting Services], data sources
- data sources [Reporting Services], connections
- connection strings [Reporting Services]
- shared data sources [Reporting Services]
- Reporting Services, data sources
- logins [Reporting Services]
ms.assetid: 4d8f0ae1-102b-4b3d-9155-fa584c962c9e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fc918b390cedbca9016e4d14f72dea8c9ce8d148
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154594"
---
# <a name="data-connections-data-sources-and-connection-strings-in-reporting-services"></a>Reporting Services でのデータ接続、データ ソース、および接続文字列
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポートにデータを含めるには、最初に *データ ソース* および *データセット*を作成する必要があります。 このトピックでは、データ ソースの種類、データ ソースの作成方法、およびデータ ソースの資格情報に関連する重要な情報について説明します。 データ ソースには、データ ソースの種類、接続情報、および使用する資格情報の種類が含まれています。 データ ソースには、埋め込みと共有の 2 種類があります。 埋め込みデータ ソースは、レポート内で定義され、そのレポートでのみ使用されます。 共有データ ソースは、レポートとは別のアイテムとして定義され、複数のレポートで使用できます。 詳細については、「[埋め込みおよび共有のデータ接続またはデータ ソース (レポート ビルダーおよび SSRS)](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)」および「[埋め込みデータセットと共有データセット (レポート ビルダーおよび SSRS)](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)」を参照してください。  
  
||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ネイティブ モード &#124; [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint モード|  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  

  
##  <a name="bkmk_data_sources"></a> 埋め込みデータ ソースおよび共有データ ソース  
 埋め込みデータ ソースと共有データ ソースとでは、作成、格納、および管理の方法が異なります。  
  
-   レポート デザイナーで、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] プロジェクトの一部として、埋め込みデータ ソースまたは共有データ ソースを作成します。 プレビュー用にローカルで使用するか、プロジェクトの一部としてレポート サーバーまたは SharePoint サイトに配置するかを制御することができます。 自分のコンピューターおよびレポート サーバー、さらにレポートの配置先の SharePoint サイトにインストールされているカスタム データ拡張機能を使用できます。  
  
     システム管理者は、別のデータ処理拡張機能および .NET Framework データ プロバイダーをインストールおよび設定できます。 詳細については、「[データ処理拡張機能と .NET Framework データ プロバイダー (SSRS)](report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md)」を参照してください。  
  
     <xref:Microsoft.ReportingServices.DataProcessing> API を使ってデータ処理拡張機能を作成すると、その他の種類のデータ ソースもサポートできます。  
  
-   レポート ビルダーで、レポート サーバーまたは SharePoint サイト上の保存先を参照して共有データ ソースを選択するか、または、レポートに埋め込みデータ ソースを作成します。 共有データ ソースは、レポート ビルダーで作成することはできません。 レポート ビルダーでカスタム データ拡張機能を使用することはできません。  
  
##  <a name="bkmk_DataConnections"></a> 組み込みデータ拡張機能  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] の既定のデータ拡張機能には、次の種類のデータ接続が含まれます。  
  
-   Microsoft SQL Server  
  
-   Microsoft SQL Server Analysis Services  
  
-   Microsoft SharePoint リスト  
  
-   [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]  
  
-   Microsoft SQL Server 並列データ ウェアハウス  
  
-   OLE DB (OLE DB)  
  
-   [Oracle]  
  
-   SAP NetWeaver BI  
  
-   Hyperion Essbase  
  
-   Teradata  
  
-   XML  
  
-   ODBC  
  
-   Power View 用 Microsoft BI セマンティック モデル: PowerPivot ギャラリーおよび [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]用に構成されている SharePoint サイトでは、このデータ ソースの種類を使用できます。 このデータ ソースの種類は、 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] プレゼンテーションにのみ使用されます。 詳細については、「 [Power View に適した BI セマンティック表形式モデルの作成 (ビデオ)](https://technet.microsoft.com/video/building-the-perfect-bi-semantic-tabular-models-for-power-view.aspx)」を参照してください。  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] でサポートされるデータ ソースおよびバージョンの一覧については、「[Reporting Services でサポートされるデータ ソース (SSRS)](create-deploy-and-manage-mobile-and-paginated-reports.md)」を参照してください。  
  
##  <a name="bkmk_create_data_source"></a>データソースの作成  
 データ ソースを作成するには、次の情報が必要です。  
  
-   **データソースの種類**接続の種類 (たとえば、[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)])。 この値は、接続の種類のドロップダウン リストから選択します。  
  
-   **接続情報** 接続情報には、データ ソースの名前と場所、および各データ プロバイダーに固有の接続プロパティが含まれます。 *接続文字列* は、接続情報のテキスト表現です。 たとえば、データ ソースが SQL Server データベースの場合は、データベースの名前を指定することができます。 埋め込みデータ ソースの場合は、実行時に評価される式に基づく接続文字列を記述することもできます。 詳細については、このトピックで後述する「 [式に基づく接続文字列](#bkmk_Expressions_in_connection_strings) 」を参照してください。  
  
-   **資格情報** データにアクセスするために必要な資格情報を指定します。 データ ソースおよびデータ ソースの特定のデータにアクセスするには、データ ソースの所有者から適切な権限を許可されていることが必要です。 たとえば、ネットワーク サーバーにインストールされた [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] サンプル データベースに接続するには、サーバーに接続する権限およびデータベースにアクセスする読み取り専用権限が必要です。  
  
    > [!NOTE]  
    >  資格情報は、あえてデータ ソースとは別に管理されます。 ローカル システムでレポートのプレビューに使用する資格情報は、パブリッシュされたレポートの表示に必要な資格情報とは異なります。 レポート サーバーまたは SharePoint サイトにデータ ソースを保存した後は、その場所にあるデータを操作する関係上、資格情報の変更が必要となる場合があります。 詳細については、「 [データ ソースの資格情報](#bkmk_credentials)」を参照してください。  
  
> [!NOTE]  
>  レポートの埋め込みデータ ソースを [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で作成する場合、データ ソースの作成は、レポート デザイナーのソリューション エクスプローラーまたはレポート データ ペインで行う必要があります。サーバー エクスプローラーでデータ ソースを作成することは避けてください。 サーバー エクスプローラーで作成された [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データ ソースは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] レポート デザイナーではサポートされません。  
  
 レポート データ ペインには、レポートに追加された共有データ ソースへの参照と埋め込みデータ ソースが表示されます。 レポート ビルダーにおける共有データ ソースの参照先は、レポート サーバー上または SharePoint サイト上の共有データ ソースです。 レポート デザイナーにおける共有データ ソースの参照先は、ソリューション エクスプローラーの [共有データ ソース] フォルダーに表示される共有データ ソースです。  
  
##  <a name="bkmk_credentials"></a>データソースの資格情報  
 資格情報は、接続情報とは別に保存および管理できる設計になっています。 資格情報は、データ ソースの作成、データセット クエリの実行、レポートのプレビューなどで使用されます。  
  
> [!NOTE]  
>  ログイン名やパスワードなどのログイン情報は、データ ソースの接続プロパティに含めないようにすることをお勧めします。 可能な限り、資格情報が保存された共有データ ソースを使用してください。 データ接続を作成する場合やデータセット クエリを実行する場合は、作成環境で **[データ ソース]** ダイアログ ボックスの [資格情報] ページを使用して資格情報を入力します。  
  
 自分のコンピューターからデータにアクセスする際に入力する資格情報は、ローカルのプロジェクト構成ファイルに安全に保管され、そのコンピューターに固有の情報となります。 プロジェクト ファイルを別のコンピューターにコピーするときは、データ ソースの資格情報を再定義する必要があります。  
  
 レポート サーバーまたは SharePoint サイトにレポートを配置した場合、埋め込みデータ ソースと共有データ ソースは別々に管理されます。 ローカル コンピューターからデータにアクセスするために必要なデータ ソース資格情報は、レポート サーバーからデータにアクセスするために必要な資格情報とは異なる場合があります。  
  
 ![注]レポートをパブリッシュした後も、データソース接続が正常に接続されていることを確認することをお(media/rs-fyinote.png "勧めします")。 資格情報を変更する必要がある場合は、レポート サーバー上で直接変更できます。  
  
 レポートで使用されるデータソースを変更するには、ネイティブモードレポートマネージャーまたは SharePoint モードのドキュメントライブラリからレポートのプロパティを変更します。 詳細については、以下をご覧ください。  
  
-   [Reporting Services データソース](report-data/store-credentials-in-a-reporting-services-data-source.md)[ストアの資格情報を Reporting Services データソースに](report-data/store-credentials-in-a-reporting-services-data-source.md)格納する  
  
-   [レポート データ ソースに関する資格情報と接続情報を指定する](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
-   [カスタム データ処理拡張機能の接続を指定する](report-data/specify-connections-for-custom-data-processing-extensions.md)  
  
-   [レポート ビルダーでの資格情報の指定](../../2014/reporting-services/specify-credentials-in-report-builder.md)  
  
-   [データ接続またはデータソース&#40;レポートビルダーと SSRS の追加と検証&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
##  <a name="bkmk_connection_examples"></a> 一般的な接続文字列の例  
 接続文字列は、データ プロバイダーの接続プロパティのテキスト表現です。 次の表に、さまざまなデータ接続に使用される接続文字列の例を示します。  
  
|**データ ソース**|**例**|**説明**|  
|---------------------|-----------------|---------------------|  
|ローカル サーバーの SQL Server データベース|`data source="(local)";initial catalog=AdventureWorks`|データソースの種類を `Microsoft SQL Server`に設定します。 詳細については、「[SQL Server の接続の種類 &#40;SSRS&#41;](report-data/sql-server-connection-type-ssrs.md)」を参照してください。|  
|ローカル サーバーの SQL Server データベース|`data source="(local)";initial catalog=AdventureWorks`|データソースの種類を `Microsoft SQL Server`に設定します。|  
|SQL Server インスタンス<br /><br /> データベース (database)|`Data Source=localhost\MSSQL10_50.InstanceName; Initial Catalog=AdventureWorks`|データソースの種類を `Microsoft SQL Server`に設定します。|  
|SQL Server Express データベース|`Data Source=localhost\MSSQL10_50.SQLEXPRESS; Initial Catalog=AdventureWorks`|データソースの種類を `Microsoft SQL Server`に設定します。|  
|クラウド内の [!INCLUDE[ssSDS](../includes/sssds-md.md)]|`Data Source=<host>;Initial Catalog=AdventureWorks; Encrypt=True`|データソースの種類を `Azure SQL Database`に設定します。 詳細については、「[SQL Azure の接続の種類 (SSRS)](report-data/sql-azure-connection-type-ssrs.md)」を参照してください。|  
|SQL Server 並列データ ウェアハウス|`HOST=<IP address>;database= AdventureWorks; port=<port>`|データソースの種類を `Microsoft SQL Server Parallel Data Warehouse`に設定します。 詳細については、「[SQL Server 並列データ ウェアハウスの接続の種類 &#40;SSRS&#41;](report-data/sql-server-parallel-data-warehouse-connection-type-ssrs.md)」を参照してください。|  
|ローカル サーバーの Analysis Services データベース|`data source=localhost;initial catalog=Adventure Works DW`|データソースの種類を `Microsoft SQL Server Analysis Services`に設定します。 詳細については、「[MDX のための Analysis Services の接続の種類 &#40;SSRS&#41;](report-data/analysis-services-connection-type-for-mdx-ssrs.md)」または「[DMX のための Analysis Services の接続の種類 &#40;SSRS&#41;](report-data/analysis-services-connection-type-for-dmx-ssrs.md)」を参照してください。|  
|Sales パースペクティブを持つ Analysis Services テーブル モデル データベース|`Data source=<servername>;initial catalog= Adventure Works DW;cube='Sales'`|データソースの種類を `Microsoft SQL Server Analysis Services`に設定します。 cube= 設定にパースペクティブの名前を指定します。 詳しくは、「[パースペクティブ &#40;SSAS Tabular&#41;](https://docs.microsoft.com/analysis-services/tabular-models/perspectives-ssas-tabular)」をご覧ください。|  
|ネイティブ モードで構成されているレポート サーバーのレポート モデル データ ソース|`Server=http://myreportservername/reportserver; datasource=/models/Adventure Works`|レポート サーバーまたはドキュメント ライブラリの URL と、レポート サーバー フォルダーまたはドキュメント ライブラリ フォルダーの名前空間内のパブリッシュされたモデルへのパスを指定します。
|SharePoint 統合モードで構成されているレポート サーバーのレポート モデル データ ソース|`Server=http://server; datasource=http://server/site/documents/models/Adventure Works.smdl`|レポート サーバーまたはドキュメント ライブラリの URL と、レポート サーバー フォルダーまたはドキュメント ライブラリ フォルダーの名前空間内のパブリッシュされたモデルへのパスを指定します。|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] サーバー|`provider=MSOLAP.2;data source=<remote server name>;initial catalog=FoodMart 2000`|データ ソースの種類を `OLE DB Provider for OLAP Services 8.0` に設定します。<br /><br /> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プロパティを [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] に設定すると、`ConnectTo` 2000 `8.0` のデータ ソースにより高速に接続できるようになります。 このプロパティを設定するには、 **[接続プロパティ]** ダイアログ ボックスの **[詳細プロパティ]** タブを使用します。|  
|Oracle サーバー|`data source=myserver`|データ ソースの種類を `Oracle` に設定します。 レポート デザイナーがインストールされているコンピューターとレポート サーバーに、Oracle クライアント ツールがインストールされている必要があります。 詳細については、「[Oracle の接続の種類 &#40;SSRS&#41;](report-data/oracle-connection-type-ssrs.md)」を参照してください。|  
|SAP NetWeaver BI データ ソース|`DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla`|データ ソースの種類を `SAP NetWeaver BI` に設定します。 詳細については、「[SAP NetWeaver BI の接続の種類 &#40;SSRS&#41;](report-data/sap-netweaver-bi-connection-type-ssrs.md)」を参照してください。|  
|Hyperion Essbase データ ソース|`Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample`|データ ソースの種類を `Hyperion Essbase` に設定します。 詳細については、「[Hyperion Essbase の接続の種類 &#40;SSRS&#41;](report-data/hyperion-essbase-connection-type-ssrs.md)」を参照してください。|  
|Teradata データ ソース|`data source=`\<NNN>.\<NNN>.\<NNN>.\<NNN>`;`|データ ソースの種類を `Teradata` に設定します。 接続文字列は、各フィールドが 1 ～ 3 桁の 4 つのフィールドで構成されるインターネット プロトコル (IP) アドレスです。 詳細については、「[Teradata の接続の種類 &#40;SSRS&#41;](report-data/teradata-connection-type-ssrs.md)」を参照してください。|  
|XML データ ソース、Web サービス|`data source=http://adventure-works.com/results.aspx`|データ ソースの種類を `XML` に設定します。 接続文字列は、Web サービス記述言語 (WSDL) をサポートする Web サービスの URL です。 詳細については、「[XML の接続の種類 &#40;SSRS&#41;](report-data/xml-connection-type-ssrs.md)」を参照してください。|  
|XML データ ソース、XML ドキュメント|`http://localhost/XML/Customers.xml`|データ ソースの種類を `XML` に設定します。 接続文字列は XML ドキュメントへの URL です。|  
|XML データ ソース、埋め込み XML ドキュメント|*空*|データ ソースの種類を `XML` に設定します。 XML データはレポート定義に埋め込まれています。|  
  
`localhost` を使用してレポート サーバーに接続できない場合は、TCP/IP プロトコルのネットワーク プロトコルが有効になっていることを確認します。 詳細については、「 [Configure Client Protocols](../database-engine/configure-windows/configure-client-protocols.md)」を参照してください。  
  
##  <a name="bkmk_special_password_characters"></a> パスワードの特殊文字  
 パスワードを要求したり、接続文字列にパスワードを含めるように ODBC データ ソースや SQL データ ソースを構成し、ユーザーが句読点のような特殊文字を使用してパスワードを入力した場合、基になるデータ ソースのドライバーによってはその特殊文字を検証することができません。 レポートを処理する際に、この問題によって、"パスワードが無効です" というメッセージが表示される場合があります。 パスワードを変更できない場合は、データベース管理者と連携して、適切な資格情報をシステム ODBC データ ソース名 (DSN) の一部としてサーバーに格納することができます。 詳細については、 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK ドキュメントの「OdbcConnection.ConnectionString」を参照してください。  
  
##  <a name="bkmk_Expressions_in_connection_strings"></a> 式に基づく接続文字列  
 式に基づく接続文字列は実行時に評価されます。 たとえば、データ ソースをパラメーターとして指定し、接続文字列にパラメーター参照を含めて、ユーザーがレポートのデータ ソースを選択できるようにすることができます。 たとえば、多国籍企業がいくつもの国にデータ サーバーを持っていると仮定します。 式ベースの接続文字列を使用すると、販売レポートを実行するユーザーは、レポートの実行前に特定の国のデータ ソースを選択することができます。  
  
 次の例では、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の接続文字列でデータ ソースの式を使用する方法を示します。 この例では、 `ServerName`というレポート パラメーターが作成されているものとします。  
  
```  
="data source=" & Parameters!ServerName.Value & ";initial catalog=AdventureWorks"  
```  
  
 データ ソースの式は、実行時またはレポートのプレビュー時に処理されます。 式は、 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]で記述する必要があります。 データ ソースの式を定義する際には、次のガイドラインに従います。  
  
-   静的な接続文字列を使用してレポートをデザインする。 静的な接続文字列とは、式を使わずに設定した接続文字列です (たとえば、レポート固有のデータ ソースまたは共有データ ソースの作成手順に従うと、静的な接続文字列を定義することになります)。 静的な接続文字列を使用することで、レポート デザイナーでデータ ソースに接続し、レポートの作成に必要なクエリ結果を取得することができます。  
  
-   データ ソースの接続を定義する際には、共有データ ソースを使用しない。 共有データ ソース内では、データ ソースの式を使用できません。 レポートの埋め込みデータ ソースを定義する必要があります。  
  
-   資格情報は接続文字列とは別に指定する。 保存された資格情報、要求された資格情報、または統合セキュリティを使用することができます。  
  
-   レポート パラメーターを追加してデータ ソースを指定する。 パラメーター値には、使用可能な値の静的な一覧を指定するか (この場合、使用可能な値には、レポートで使用できるデータ ソースを指定する必要があります)、実行時にデータ ソースの一覧を取得するクエリを定義します。  
  
-   データ ソースの一覧が同じデータベース スキーマを共有するようにする。 すべてのレポートのデザインは、スキーマ情報から始まります。 レポートの定義で使用されているスキーマと、実行時にレポートが使用する実際のスキーマが一致しないと、レポートが実行されない場合があります。  
  
-   レポートをパブリッシュする前に、静的な接続文字列を式で置き換える。 レポートのデザインが完了するまでは、静的な接続文字列を式で置き換えません。 式を使用すると、レポート デザイナー内でクエリを実行できなくなります。 さらに、レポート データ ペイン内のフィールド一覧と、[パラメーター] の一覧が、自動的に更新されなくなります。  
  
## <a name="see-also"></a>参照  
 [埋め込みおよび共有のデータ接続またはデータ ソース (レポート ビルダーおよび SSRS)](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [レポート データ ソースを管理する](report-data/manage-report-data-sources.md)   
 [[資格情報の ] ([データソースのプロパティ] ダイアログボックス)](../../2014/reporting-services/data-source-properties-dialog-box-credentials.md)  
 [[資格情報] ([共有データソースのプロパティ] ダイアログボックス)](../../2014/reporting-services/shared-data-source-properties-dialog-box-credentials.md)   
 [共有データ ソースを作成、変更、および削除する (SSRS)](report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [配置プロパティを設定する (Reporting Services)](tools/set-deployment-properties-reporting-services.md)   
 [レポート データ ソースに関する資格情報と接続情報を指定する](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [データ接続またはデータソース&#40;レポートビルダーと SSRS の追加と検証&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
