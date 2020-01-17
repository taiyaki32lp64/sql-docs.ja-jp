---
title: Reporting Services でサポートされるデータ ソース (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SQL Server data processing extension [Reporting Services]
- XML data processing extension [Reporting Services]
- reports [Reporting Services], data
- data processing extensions [Reporting Services], data sources
- Oracle [Reporting Services]
- OLE DB data processing extension
- data sources [Reporting Services], about data sources
- ODBC data processing extension
- Reporting Services, data sources
ms.assetid: 9d11d055-a3be-45aa-99a7-46447a94ed42
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6e569240f708d209fc965fa3c6e393859044f528
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155120"
---
# <a name="data-sources-supported-by-reporting-services-ssrs"></a>Reporting Services でサポートされるデータ ソース (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] でレポート データをデータ ソースから取得する処理は、データ処理拡張機能を使用するモジュール式の拡張可能なデータ レイヤーを通して行われます。 レポート データをデータ ソースから取得するには、対象となるデータ ソースの種類 (データ ソースで動作しているバージョンのソフトウェア) およびデータ ソース プラットフォーム (32 ビットまたは 64 ビット [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]) がサポートされているデータ処理拡張機能を選択する必要があります。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]を配置すると、レポート作成クライアントとレポート サーバーの両方にデータ処理拡張機能セットが自動的にインストールおよび登録され、さまざまな種類のデータ ソースにアクセスできるようになります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、次のデータ ソースの種類がインストールされます。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   MDX、DMX、[!INCLUDE[msCoName](../../includes/msconame-md.md)] PowerPivot、およびテーブルモデルの [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
-   並列データウェアハウスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   [Oracle]  
  
-   SAP NetWeaver BI  
  
-   [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint リスト  
  
-   Teradata  
  
-   OLE DB (OLE DB)  
  
-   ODBC  
  
-   XML  
  
 またシステム管理者は、カスタム データ処理拡張機能や標準の [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーをインストールおよび登録することができます。 レポートの処理や表示を行うには、データ処理拡張機能およびデータ プロバイダーをレポート サーバーにインストールし登録する必要があります。レポートをプレビューするには、データ処理拡張機能およびデータ プロバイダーをレポート作成クライアントにインストールし登録する必要があります。 データ処理拡張機能およびデータ プロバイダーは、インストールされているプラットフォームに対してネイティブでコンパイルされます。 SOAP Web サービスを使用してデータ ソースをプログラムで配置する場合は、データ ソース拡張機能を定義する必要があります。 **RSReportDesigner.config** ファイルのデータ拡張機能の値を使用します。 既定では、このファイルは次のフォルダーにあります。  
  
```  
<drive letter>\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies  
```  
  
 たとえば、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ拡張機能は OLEDB-MD です。  
  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Microsoft ダウンロード センター [およびサードパーティのサイトには、ダウンロードとしてサードパーティの標準](https://go.microsoft.com/fwlink/?linkid=51456) データ プロバイダーが多数用意されています。 また、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] パブリック フォーラムで、サードパーティ データ プロバイダーに関する情報を検索することもできます。  
  
> [!NOTE]  
>  標準 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理機能拡張により提供される機能をすべてサポートするわけではありません。 また、一部の OLE DB データ プロバイダーと ODBC ドライバーは、レポートを作成およびプレビューすることができますが、レポート サーバーでパブリッシュされたレポートをサポートするようには設計されていません。 たとえば、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet の場合、レポート サーバーでの使用はサポートされていません。 詳細については、「[データ処理拡張機能と .NET Framework データ プロバイダー (SSRS)](data-processing-extensions-and-net-framework-data-providers-ssrs.md)」を参照してください。  
  
 カスタムのデータ処理拡張機能の詳細については、「 [Implementing a Data Processing Extension](../extensions/data-processing/implementing-a-data-processing-extension.md)」を参照してください。 標準 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーの詳細については、 <xref:System.Data> 名前空間のセクションを参照してください。  
  
 レポート ビルダーがサポートしているデータ処理拡張機能の詳細については、msdn.microsoft.com の [レポート ビルダーに関するドキュメント](../data-connections-data-sources-and-connection-strings-in-report-builder.md) の「 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](https://go.microsoft.com/fwlink/?LinkId=154494) 」を参照してください。  
  
## <a name="platform-support-for-report-data-sources"></a>レポート データ ソースに対するプラットフォームのサポート  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の配置で使用できるデータ ソースは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエディション、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のバージョン、およびプラットフォームによって異なります。 機能の詳細については、「 [SQL Server 2014 の各エディションがサポートする機能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」を参照してください。 このトピックでは、サポートされるデータ ソースに関する情報をバージョンおよびプラットフォームごとに表に示します。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ ソースに関するプラットフォームの考慮事項は、レポート作成クライアントの場合とレポート サーバーの場合で異なります。  
  
### <a name="on-the-report-authoring-client"></a>レポート作成クライアント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] は 32 ビット アプリケーションです。 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] は、Itanium ベースのプラットフォームではサポートされていません。 x64 プラットフォームでは、レポート デザイナーでレポートを編集およびプレビューするために、32 ビットのデータ プロバイダーを (x86) プラットフォーム ディレクトリにインストールしておく必要があります。  
  
### <a name="on-the-report-server"></a>レポート サーバー  
 レポートを 64 ビットのレポート サーバー (x86) に配置する場合は、そのレポート サーバーに、ネイティブでコンパイル済みの 64 ビット データ プロバイダーがインストールされている必要があります。 64 ビット インターフェイスによる 32 ビット データ プロバイダーのラップはサポートされていません。 詳細については、データ プロバイダーのマニュアルを参照してください。  
  
## <a name="supported-data-sources"></a>サポートされるデータ ソース  
 次の表は、レポート データセットおよびレポート モデルのデータを取得するときに使用できる、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] データ処理拡張機能およびデータ プロバイダーを示しています。 拡張機能またはデータ プロバイダーの詳細を参照する場合は、2 番目の列のリンクをクリックしてください。 以下に、表の列の説明を示します。  
  
-   レポート データのソース: アクセス先のデータの種類 (リレーショナル データベース、多次元データベース、フラット ファイル、XML など)。 この列を参照すると、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] がレポートに使えるデータの種類がわかります。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ ソースの種類: [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]でデータ ソースを定義するときにドロップダウン リストに表示されるデータ ソースの種類のうちの 1 つ。 このリストには、インストールおよび登録された DPE とデータ プロバイダーから取得した値が設定されます。 この列を参照すると、レポート データ ソースを作成するときにドロップダウン リストから選択すべきデータ ソースの種類がわかります。  
  
-   データ処理拡張機能/データ プロバイダーの名前: 選択した [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ ソースの種類に対応する [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能または他のデータ プロバイダー。 この列では、データ ソースの種類を選択したときに、どのデータ処理拡張機能またはデータ プロバイダーが使用されるかを識別できます。  
  
-   基になるデータ プロバイダーのバージョン (オプション): データ ソースの種類によっては複数のデータ プロバイダーがサポートされます。 たとえば、同じプロバイダーに異なるバージョンが存在する場合や、特定の種類のデータ プロバイダーとして複数のサードパーティによる実装が存在する場合があります。 プロバイダー名は、データ ソースを構成した後の接続文字列に含まれることがよくあります。 この列では、データ ソースの種類を選択した後に、 **[接続プロパティ]** ダイアログ ボックスで選択すべきデータ プロバイダーを識別できます。  
  
-   データ ソース *\<platform>* : 対象データ ソースのデータ処理拡張機能またはデータ プロバイダーによりサポートされるデータ ソースのプラットフォーム。 この列では、プラットフォームの種類に応じて、データ ソースからデータを取得できるデータ処理拡張機能またはデータ プロバイダーを識別できます。  
  
-   データ ソースのバージョン: DPE またはデータ プロバイダーでサポートされている対象データ ソースのバージョン。 この列では、対象となるバージョンのデータ ソースからデータを取得できるデータ処理拡張機能またはプロバイダーを識別できます。  
  
-   RS *\<platform>* : カスタムの DPE またはデータ プロバイダーをインストールできる、レポート サーバーおよびレポート作成クライアントのプラットフォーム。 組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能は、インストールされた [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に含まれています。 カスタムのデータ処理拡張機能または [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーは、特定のプラットフォーム用にネイティブにコンパイルする必要があります。 この列では、対象となる種類のプラットフォームにインストールできるデータ処理拡張機能またはプロバイダーを識別できます。  
  
###  <a name="DataSourcesTable"></a> データ ソースの種類  
  
|レポート データの<br /><br /> ソース|Reporting Services データ ソースの種類|データ処理拡張機能/データ プロバイダーの名前|基になるデータ プロバイダーのバージョン<br /><br /> (オプション)|Data<br /><br /> ソース<br /><br /> プラットフォーム x86|Data<br /><br /> ソース<br /><br /> プラットフォーム x64|データ ソースのバージョン|RS<br /><br /> プラットフォーム x86|RS<br /><br /> プラットフォーム x64|  
|-------------------------------|-----------------------------------------|------------------------------------------------------|-------------------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|-------------------------|-------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リレーショナル データベース|[Microsoft SQL Server](#MicrosoftSQLServer)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|System.Data.SqlClient を拡張|Y|Y|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降。|Y|Y|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リレーショナル データベース|[OLEDB](#OLEDBSQL)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|System.Data.OledbClient を拡張|Y|Y|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降。|Y|Y|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リレーショナル データベース|[ODBC](#ODBC)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|System.Data.OdbcClient を拡張|Y|Y|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降。|Y|Y|  
|[!INCLUDE[ssSDS](../../includes/sssds-md.md)]|[Azure SQL データベース](#Azure)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|System.Data.SqlClient を拡張|なし|なし|[!INCLUDE[ssSDS](../../includes/sssds-md.md)]|Y|Y|  
|[!INCLUDE[ssDW](../../includes/ssdw-md.md)] アプライアンス|[Microsoft 並列データ ウェアハウス](#PWD)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|なし|なし|なし|[!INCLUDE[ssDWfull](../../includes/ssdwfull-md.md)]|Y|Y|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多次元データベース|[Microsoft SQL Server Analysis Services](#AnalysisServices)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|ADOMD.NET を使用|Y|Y|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 以降<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降|Y|Y|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多次元データベース|[OLEDB](#OLEDBAS9)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|System.Data.OledbClient を拡張<br /><br /> バージョン 10.0|Y|Y|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|Y|Y|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多次元データベース|[OLEDB](#OLEDBAS9)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|System.Data.OledbClient を拡張<br /><br /> バージョン 9.0|Y|Y|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|Y|Y|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多次元データベース|OLEDB|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|System.Data.OledbClient を拡張<br /><br /> Version 8.0|Y|×|なし|Y|×|  
|SharePoint リスト|[Microsoft SharePoint リスト](#SharePointList)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|Lists.asmx または SharePoint オブジェクト モデル API インターフェイスからデータを取得。<br /><br /> 詳細については、「 [注意](#SharePointList)」を参照してください。|×|Y|SharePoint 2013 製品<br /><br /> SharePoint 2010 製品|Y|Y|  
|SharePoint リスト|[Microsoft SharePoint リスト](#SharePointList)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|Lists.asmx または SharePoint オブジェクト モデル API インターフェイスからデータを取得。<br /><br /> 詳細については、「 [注意](#SharePointList)」を参照してください。|Y|Y|[!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 および [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007|Y|Y|  
|XML|[XML](#XML)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|XML データ ソースにはプラットフォーム依存関係がありません。|なし|なし|[!INCLUDE[vstecwebservices](../../includes/vstecwebservices-md.md)] またはドキュメント|Y|Y|  
|レポート サーバー モデル|レポート モデル|パブリッシュされた SMDL ファイル用の、組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|モデルのデータ ソースには組み込みのデータ処理拡張機能が使用されます。<br /><br /> Oracle ベースのモデルには、Oracle クライアント コンポーネントが必要です。<br /><br /> Teradata ベースのモデルには、Teradata からの .NET Data Provider for Teradata が必要です。<br /><br /> プラットフォームのサポートについては、Teradata のマニュアルを参照してください。|なし|なし|モデルの作成は次から可能です。[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降<br /><br /> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]<br /><br /> Oracle 9.2.0.3 以降<br /><br /> Teradata V14、v13、v12、および v6.2|Y|Y|  
|SAP 多次元データベース|[Sap BI NetWeaver](#SapBINetWeaver)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|プラットフォームのサポートについては、SAP のマニュアルを参照してください。|なし|なし|SAP BI NetWeaver 3.5|Y|なし|  
|[!INCLUDE[extEssbase](../../includes/extessbase-md.md)]|[Hyperion Essbase](#Hyperion)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|プラットフォームのサポートについては、Hyperion のマニュアルを参照してください。|Y|なし|[!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 9.3.1|Y|なし|  
|Oracle リレーショナル データベース|[Oracle](#OracleClient)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|System.Data.OracleClient を拡張<br /><br /> Oracle クライアント コンポーネントが必要です。|Y|なし|Oracle 10g、9、8.1.7|Y|Y|  
|Teradata リレーショナル データベース|[Teradata](#Teradata)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|Teradata からの .NET Data Provider for Teradata を拡張<br /><br /> Teradata からの .NET Data Provider for Teradata が必要です。<br /><br /> プラットフォームのサポートについては、Teradata のマニュアルを参照してください。|Y|なし|Teradata v14<br /><br /> Teradata v13<br /><br /> Teradata v12<br /><br /> Teradata v6.20|Y|×|  
|DB2 リレーショナル データベース|登録済みのカスタマイズされたデータ拡張機能名||2004 Host Integration (HI) Server<br /><br /> [HI Server のマニュアル](https://msdn.microsoft.com/library/gg241192\(v=bts.10\).aspx)を参照してください。|Y|なし|なし|Y|×|  
|汎用 OLE DB データ ソース|[OLEDB](#OLEDBStandard)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|OLE DB をサポートする任意のデータ ソース。<br /><br /> プラットフォームのサポートについては、データ ソースのマニュアルを参照してください。|Y|なし|OLE DB をサポートする任意のデータ ソース。 詳細については、「 [注意](#OLEDBStandard)」を参照してください。|Y|なし|  
|汎用 ODBC データ ソース|[ODBC](#ODBCGeneric)|組み込みの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能|ODBC をサポートする任意のデータ ソース。<br /><br /> プラットフォームのサポートについては、データ ソースのマニュアルを参照してください。|Y|なし|ODBC をサポートする任意のデータ ソース。 詳細については、「 [注意](#ODBCGeneric)」を参照してください。|Y|Y|  
  
 表形式のデータソースの使用の詳細については、「 [Reporting Services のデータ接続、データソース、および接続文字列](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)」を参照してください。  
  
 外部データ ソースの使用に関する詳細については、「[外部データ ソースのデータを追加する &#40;SSRS&#41;](add-data-from-external-data-sources-ssrs.md)」を参照してください。  
  
 サードパーティの標準 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーは多数あります。 詳細については、サードパーティの Web サイトまたはフォーラムを検索してください。  
  
 カスタム データ処理拡張機能または標準 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーをインストールおよび登録するには、データ プロバイダー リファレンス ドキュメントを参照する必要があります。 詳細については、「[標準 .NET Framework データ プロバイダーを登録する &#40;SSRS&#41;](register-a-standard-net-framework-data-provider-ssrs.md)」を参照してください。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
## <a name="reporting-services-data-processing-extensions"></a>Reporting Services データ処理拡張機能  
 次のデータ処理拡張機能は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] および [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]と一緒に自動的にインストールされます。 詳細およびインストールを確認する方法については、「 [Rsreportdesigner 構成ファイル](../report-server/rsreportdesigner-configuration-file.md)」と「 [rsreportserver 構成ファイル](../report-server/rsreportserver-config-configuration-file.md)」を参照してください。  
  
> [!NOTE]  
>  現在、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ処理拡張機能はサポートされていません。  
  
 レポート ビルダーがサポートしているデータ処理拡張機能の詳細については、msdn.microsoft.com の [レポート ビルダーに関するドキュメント](../data-connections-data-sources-and-connection-strings-in-report-builder.md) の「 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](https://go.microsoft.com/fwlink/?LinkId=154494) 」を参照してください。  
  
###  <a name="MicrosoftSQLServer"></a> Microsoft SQL Server データ処理拡張機能  
 データ ソースの種類 **Microsoft SQL Server** は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をラップし、拡張したものです。 このデータ処理拡張機能は、x86 および [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)] ベースのプラットフォーム用にネイティブでコンパイルされ、これらのプラットフォームで実行されます。  
  
 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]では、このデータ拡張機能に関連付けられているクエリ デザイナーは [Visual Database Tools デザイナー](../../ssms/visual-db-tools/visual-database-tool-designers.md)です。 クエリ デザイナーをグラフィカル モードで使用すると、クエリが分析され、再作成される場合があります。 クエリに使用する [!INCLUDE[tsql](../../includes/tsql-md.md)] 構文を制御するには、テキストベースのクエリ デザイナーを使用します。 詳細については、「[クエリおよびビュー デザイナー &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)」および「[グラフィカル クエリ デザイナーのユーザー インターフェイス](graphical-query-designer-user-interface.md)」を参照してください。  
  
 詳細については、「[SQL Server の接続の種類 &#40;SSRS&#41;](sql-server-connection-type-ssrs.md)」を参照してください。  
  
 レポート ビルダーでは、このデータ拡張機能に関連付けられているクエリ デザイナーはリレーショナル クエリ デザイナーです。 詳細については、「 [Relational Query Designer User Interface](../relational-query-designer-user-interface.md)」を参照してください。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
###  <a name="Azure"></a>Azure SQL Database 処理拡張機能  
 データ ソースの種類 **[[!INCLUDE[ssSDS](../../includes/sssds-md.md)]]** は、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をラップし、拡張したものです。  
  
 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]では、このデータ拡張機能に関連付けられているグラフィカル クエリ デザイナーは、 [リレーショナル クエリ デザイナーのユーザー インターフェイス](../relational-query-designer-user-interface.md)です。 [Microsoft SQL Server](../../ssms/visual-db-tools/visual-database-tool-designers.md) のデータ ソースの種類と共に使用する **Visual Database Tools デザイナー** ではありません。  
  
 では、 **[!INCLUDE[ssSDS](../../includes/sssds-md.md)]** と**Microsoft SQL Server**のデータソースの種類を自動的に区別し、データソースの種類に関連付けられているグラフィカルクエリデザイナーを開き [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] ます。  
  
 クエリ デザイナーをグラフィカル モードで使用すると、クエリが分析され、再作成される場合があります。 クエリの作成に、テキスト ベースのクエリ デザイナーを使用することもできます。 クエリに使用する [!INCLUDE[tsql](../../includes/tsql-md.md)] 構文を制御するには、テキストベースのクエリ デザイナーを使用します。 詳細については、「[テキストベースのクエリ デザイナーのユーザー インターフェイス](../text-based-query-designer-user-interface.md)」を参照してください。  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からのデータの取得は似ていますが、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]のみに適用される一部の要件が存在します。 詳細については、「[SQL Azure の接続の種類 (SSRS)](sql-azure-connection-type-ssrs.md)」を参照してください。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
###  <a name="PWD"></a> Microsoft SQL Server 並列データ ウェアハウス処理拡張機能  
 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]では、このデータ拡張機能に関連付けられているグラフィカル クエリ デザイナーは、 [リレーショナル クエリ デザイナーのユーザー インターフェイス](../relational-query-designer-user-interface.md)です。 [Microsoft SQL Server](../../ssms/visual-db-tools/visual-database-tool-designers.md) のデータ ソースの種類と共に使用する **Visual Database Tools デザイナー** ではありません。  
  
 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] は、 **SQL Server 並列データウェアハウス**と**Microsoft SQL Server**データソースの種類を自動的に区別し、データソースの種類に関連付けられているグラフィカルクエリデザイナーを開きます。  
  
 クエリ デザイナーをグラフィカル モードで使用すると、クエリが分析され、再作成される場合があります。 クエリの作成に、テキスト ベースのクエリ デザイナーを使用することもできます。 クエリに使用する [!INCLUDE[tsql](../../includes/tsql-md.md)] 構文を制御するには、テキストベースのクエリ デザイナーを使用します。 詳細については、「[テキストベースのクエリ デザイナーのユーザー インターフェイス](../text-based-query-designer-user-interface.md)」を参照してください。  
  
 [!INCLUDE[ssDWCurrentFull](../../includes/ssdwcurrentfull-md.md)] は、クエリ内でのストアド プロシージャおよびテーブル値関数の使用をサポートしていません。 詳細については、「[SQL Server 並列データ ウェアハウスの接続の種類 &#40;SSRS&#41;](sql-server-parallel-data-warehouse-connection-type-ssrs.md)」を参照してください。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
###  <a name="AnalysisServices"></a> Microsoft SQL Server Analysis Services データ処理拡張機能  
 データ ソースの種類に **[Microsoft SQL Server Analysis Services]** を選択した場合は、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Data Provider for [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] を拡張した [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ処理拡張機能が選択されます。 このデータ処理拡張機能は、x86 および x64 ベースのプラットフォーム用にネイティブでコンパイルされ、これらのプラットフォームで実行されます。  
  
 このデータ プロバイダーは、ADOMD.NET オブジェクト モデルを使用して、XML for Analysis (XMLA) Version 1.1 を使用したクエリを作成します。 結果はフラット化された行セットとして返されます。 詳細については、「[MDX のための Analysis Services の接続の種類 &#40;SSRS&#41;](analysis-services-connection-type-for-mdx-ssrs.md)」、「[DMX のための Analysis Services の接続の種類 &#40;SSRS&#41;](analysis-services-connection-type-for-dmx-ssrs.md)」、「[Analysis Services の MDX クエリ デザイナーのユーザー インターフェイス](analysis-services-mdx-query-designer-user-interface.md)」、および「[Analysis Services の DMX クエリ デザイナーのユーザー インターフェイス](analysis-services-dmx-query-designer-user-interface.md)」を参照してください。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ ソースに接続する場合、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ処理拡張機能では、複数値パラメーターがサポートされ、セルおよびメンバーのプロパティが [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]でサポートされる拡張プロパティにマップされます。 詳細については、「[Analysis Services データベースに対する拡張フィールド プロパティ &#40;SSRS&#41;](extended-field-properties-for-an-analysis-services-database-ssrs.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ ソースからモデルを作成することもできます。  
  
###  <a name="OLEDBAll"></a> OLE DB Data Processing Extension  
 OLE DB データ処理拡張機能では、レポートで使用するデータ ソースのバージョンに基づいて、追加のデータ プロバイダー レイヤーを選択する必要があります。 特定のデータ プロバイダーを選択しなかった場合は、既定値が使用されます。 **[データ ソース]** または **[共有データ ソース]** ダイアログ ボックスで、 [[編集]](../data-source-properties-dialog-box-general.md) ボタンをクリックし、 [[接続プロパティ]](../shared-data-source-properties-dialog-box-general.md) ダイアログ ボックスで特定のデータ プロバイダーを選択します。  
  
 OLE DB に関連付けられたクエリ デザイナーの詳細については、「[クエリおよびビュー デザイナー &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)」および「[グラフィカル クエリ デザイナーのユーザー インターフェイス](graphical-query-designer-user-interface.md)」を参照してください。 OLE DB プロバイダーに対するサポートの詳細については、 [サポート技術情報の「](https://support.microsoft.com/default.aspx/kb/811241) Visual Studio .NET デザイナーのツールでサポートされる OLE DB プロバイダー [!INCLUDE[msCoName](../../includes/msconame-md.md)] 」を参照してください。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
####  <a name="OLEDBSQL"></a> OLE DB for SQL Server  
 データ ソースの種類に **[OLE DB]** を選択した場合は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Data Provider for OLE DB を拡張した [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ処理拡張機能が選択されます。 このデータ処理拡張機能は、x86 および x64 プラットフォーム用にネイティブでコンパイルされ、これらのプラットフォームで実行されます。  
  
 詳細については、「[OLE DB の接続の種類 &#40;SSRS&#41;](ole-db-connection-type-ssrs.md)」を参照してください。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
####  <a name="OLEDBAS9"></a>Analysis Services 9.0 の OLE DB  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]に接続するには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [[OLE DB]] Provider for [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 9.0に接続するには、 the data source type **[OLE DB]** を選択してから、基になるデータ プロバイダーを名前で選択します。 このデータ処理拡張機能とデータ プロバイダーの組み合わせは、x86 および x64 プラットフォーム用にネイティブでコンパイルされ、これらのプラットフォームで動作します。  
  
> [!NOTE]  
>  このデータ処理拡張機能では、サーバー集計、拡張フィールド プロパティの自動マッピング、およびクエリ パラメーターはサポートされません。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ ソースのデータ プロバイダーとしては、 **Microsoft SQL Server Analysis Services**をお勧めします。  
  
 詳細については、「[OLE DB の接続の種類 &#40;SSRS&#41;](ole-db-connection-type-ssrs.md)」を参照してください。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
#### <a name="ole-db-for-olap-70"></a>OLE DB for OLAP 7.0  
 OLE DB Provider for OLAP Services 7.0 はサポートされません。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
####  <a name="OracleOLEDB"></a> OLE DB for Oracle  
 データ処理拡張機能の OLE DB for Oracle では、BLOB、CLOB、NCLOB、BFILE、UROWID といった Oracle データの種類はサポートされません。  
  
 位置に依存する無名パラメーターはサポートされます。 この拡張機能では、名前付きパラメーターはサポートされません。 名前付きパラメーターを使用するには、 [Oracle](#OracleClient) データ処理拡張機能を使用します。  
  
 Oracle をデータ ソースとして構成する方法の詳細については、「 [Reporting Services を使用して Oracle データ ソースの構成およびアクセスを行う方法](https://support.microsoft.com/kb/834305)」を参照してください。 追加の権限の構成の詳細については、 [サポート技術情報の「](https://support.microsoft.com/kb/870668) NETWORK SERVICE セキュリティ プリンシパルに権限を追加する方法 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 」を参照してください。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
####  <a name="OLEDBStandard"></a> 標準の OLE DB .NET Framework データ プロバイダー  
 OLE DB [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーをサポートするデータ ソースからデータを取得するには、データ ソースの種類に **OLE DB** を使用して、既定のデータ プロバイダーを選択するか、または **[接続文字列]** ダイアログ ボックスでインストール済みのデータ プロバイダーから選択します。  
  
> [!NOTE]  
>  レポート作成クライアントのレポートのプレビューに対応しているデータ プロバイダーもありますが、すべての OLE DB データ プロバイダーが、レポート サーバーでパブリッシュされたレポートをサポートするように設計されているわけではありません。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
###  <a name="ODBC"></a> ODBC Data Processing Extension  
 データ ソースの種類に **[ODBC]** を選択した場合は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Data Provider for ODBC を拡張した [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ処理拡張機能が選択されます。 このデータ処理拡張機能は、x86 および [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)] プラットフォーム用にネイティブでコンパイルされ、これらのプラットフォームで動作します。 この拡張機能を使用すると、ODBC プロバイダーを持つ任意のデータ ソースのデータに接続し、データを取得できます。  
  
> [!NOTE]  
>  レポート作成クライアントのレポートのプレビューに対応しているデータ プロバイダーもありますが、すべての ODBC データ プロバイダーが、レポート サーバーでパブリッシュされたレポートをサポートするように設計されているわけではありません。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
####  <a name="ODBCGeneric"></a> 標準の ODBC .NET Framework データ プロバイダー  
 標準の ODBC [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーをサポートするデータ ソースからデータを取得するには、データ ソースの種類に **[ODBC]** を使用して、既定のデータ プロバイダーを選択するか、または **[接続文字列]** ダイアログ ボックスでインストール済みのデータ プロバイダーから選択します。  
  
> [!NOTE]  
>  レポート作成クライアントのレポートのプレビューに対応しているデータ プロバイダーもありますが、すべての ODBC データ プロバイダーが、レポート サーバーでパブリッシュされたレポートをサポートするように設計されているわけではありません。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
###  <a name="OracleClient"></a> Oracle データ処理拡張機能  
 データ ソースの種類に **[Oracle]** を選択した場合は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Data Provider for Oracle を拡張した [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ処理拡張機能が選択されます。 **Oracle**データソースは、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]が必要とする <xref:System.Data.OracleClient> クラスをラップし、拡張します。 Oracle データベースからレポート データを取得するには、管理者が Oracle クライアント ツールをインストールする必要があります。 このデータ プロバイダーでは、Oracle Client ソフトウェアとして提供される Oracle 8i Release 3 の Oracle Call Interface (OCI) が使用されます。 クライアント アプリケーション バージョンは 8.1.7 以降である必要があります。 これらのツールをレポート作成クライアントにインストールすると、レポートをプレビューすることができ、レポート サーバーにインストールすると、パブリッシュされたレポートを表示できます。  
  
 この拡張機能では、名前付きパラメーターがサポートされます。 Oracle Version 9 以降の場合、複数値パラメーターがサポートされます。 位置に依存する無名パラメーターを使用するには、OLE DB データ処理拡張機能と [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Oracle データ プロバイダーを組み合わせて使用します。 Oracle をデータ ソースとして構成する方法の詳細については、「 [Reporting Services を使用して Oracle データ ソースの構成およびアクセスを行う方法](https://support.microsoft.com/kb/834305)」を参照してください。 追加の権限の構成の詳細については、 [サポート技術情報の「](https://support.microsoft.com/kb/870668) NETWORK SERVICE セキュリティ プリンシパルに権限を追加する方法 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 」を参照してください。  
  
 複数の入力パラメーターを使用してストアド プロシージャからデータを取得できますが、ストアド プロシージャから返せるのは 1 つの出力カーソルのみです。 詳細については、「 [DataReader を使用したデータの取得](https://go.microsoft.com/fwlink/?LinkId=81758)」の Oracle のセクションを参照してください。  
  
 詳細については、「[Oracle の接続の種類 &#40;SSRS&#41;](oracle-connection-type-ssrs.md)」を参照してください。 関連付けられたクエリ デザイナーの詳細については、「[クエリおよびビュー デザイナー &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)」および「[グラフィカル クエリ デザイナーのユーザー インターフェイス](graphical-query-designer-user-interface.md)」を参照してください。  
  
 Oracle データベースに基づくモデルを作成することもできます。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
###  <a name="Teradata"></a> Teradata データ処理拡張機能  
 データ ソースの種類に **[Teradata]** を選択した場合は、.NET Framework Data Provider for Teradata を拡張した [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] データ処理拡張機能が選択されます。 Teradata データベースからレポート データを取得するには、システム管理者はレポート作成クライアントに .NET Framework Data Provider for Teradata をインストールしてクライアント上でレポートを編集およびプレビューし、レポート サーバー上でパブリッシュされたレポートを表示する必要があります。  
  
 レポート サーバー プロジェクトには、この拡張で使用できるグラフィカル クエリ デザイナーはありません。 クエリを作成するにはテキストベースのクエリ デザイナーを使用する必要があります。  
  
 次の表に、 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]のレポート定義でデータ ソースを定義する場合にサポート対象となる .NET Data Provider for Teradata のバージョンを示します。  
  
|[!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] のバージョン|Teradata データベースのバージョン|.NET Framework Data Provider for Teradata のバージョン|  
|-----------------------------------|-------------------------------|-------------------------------------------------------|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|12.00|12.00|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|6.20|12.00|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|12.00|12.00.01|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|12.00|12.00.01|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|12.00|12.00.01|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|14.00|14.00.01|  
  
 この拡張機能では、複数値パラメーターがサポートされます。 クエリ モード TEXT の EXECUTE コマンドを使用すると、クエリでマクロを指定できます。  
  
 詳細については、「[Teradata の接続の種類 &#40;SSRS&#41;](teradata-connection-type-ssrs.md)」を参照してください。  
  
 Teradata データベースに基づくモデルを作成することもできます。 詳細については、Teradata サイトにあるホワイト ペーパー「 [Microsoft SQL Server 2012 Reporting Services and Teradata Corporation (Microsoft SQL Server 2012 Reporting Services と Teradata 社)](http://www.teradata.com/white-papers/Microsoft-SQL-Server-2012-Reporting-Services-and-Teradata-Corporation/?type=WP)」を参照してください。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
###  <a name="SharePointList"></a> SharePoint リスト データ拡張機能  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、レポートのデータ ソースに SharePoint リストを使用できるように、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint リスト データ拡張機能が含まれています。 リスト データは、以下から取得できます。  
  
-   [!INCLUDE[SPS2013](../../includes/sps2013-md.md)]  
  
-   [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 」、「 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]  
  
-   [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 および [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007  
  
 SharePoint リスト データ プロバイダーの実装には、3 つの方法があります。  
  
1.  [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]のレポート ビルダーまたはレポート デザイナーなどのレポート作成環境、あるいはネイティブ モードで構成されたレポート サーバーの場合、リスト データは SharePoint サイトの Lists.asmx Web サービスから取得されます。  
  
2.  SharePoint 統合モードで構成されたレポート サーバーの場合、リスト データは対応する Lists.asmx Web サービス、または SharePoint API に対するプログラム呼び出しのいずれかから取得されます。 このモードでは、SharePoint ファームからリスト データを取得できます。  
  
3.  [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] および [!INCLUDE[SPS2013](../../includes/sps2013-md.md)] では、[!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint テクノロジ用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] アドインを使用することで、リスト データは SharePoint サイトの Lists.asmx Web サービス、または SharePoint ファームを構成する SharePoint サイトから取得できます。 このシナリオは、レポート サーバーが不要なため、 *ローカル モード* とも呼ばれています。  
  
 指定できる資格情報は、クライアント アプリケーションが使用している実装によって異なります。 詳細については、「[SharePoint リストの接続の種類 &#40;SSRS&#41;](sharepoint-list-connection-type-ssrs.md)」を参照してください。  
  
###  <a name="XML"></a> XML データ処理拡張機能  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、レポート内で XML データを使用できるように、XML データ処理拡張機能が含まれています。 データは、XML ドキュメントや Web サービス、または URL を使用してアクセス可能な Web ベースのアプリケーションから取得できます。 詳細については、「[XML の接続の種類 &#40;SSRS&#41;](xml-connection-type-ssrs.md)」を参照してください。 関連付けられているクエリ デザイナーの詳細については、「 [グラフィカル クエリ デザイナーのユーザー インターフェイス](graphical-query-designer-user-interface.md)」の「テキスト ベースのクエリ デザイナー」セクションを参照してください。 例については、「 [Reporting Services: XML と Web サービス データ ソースの使用](https://go.microsoft.com/fwlink/?LinkId=81654)」を参照してください。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
###  <a name="SapBINetWeaver"></a>SAP NetWeaver のビジネスインテリジェンスデータ処理拡張機能  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、レポートの [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] データ ソースからのデータを使用できるデータ処理拡張機能が含まれます。  
  
 詳細については、「[SAP NetWeaver BI の接続の種類 &#40;SSRS&#41;](sap-netweaver-bi-connection-type-ssrs.md)」を参照してください。 関連付けられているクエリ デザイナーの詳細については、「 [SAP NetWeaver BI Query Designer User Interface](sap-netweaver-bi-query-designer-user-interface.md)」を参照してください。  
  
 [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)]の詳細については、「 [SAP NetWeaver Business Intelligence での SQL Server 2008 Reporting Services の使用](https://go.microsoft.com/fwlink/?LinkId=167352)」を参照してください。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
###  <a name="Hyperion"></a> Hyperion Essbase Business Intelligence のデータ拡張機能  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、レポートの [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] データ ソースからのデータを使用できるデータ処理拡張機能が含まれます。  
  
 詳細については、「[Hyperion Essbase の接続の種類 &#40;SSRS&#41;](hyperion-essbase-connection-type-ssrs.md)」を参照してください。 関連付けられているクエリ デザイナーの詳細については、「 [Hyperion Essbase Query Designer User Interface](hyperion-essbase-query-designer-user-interface.md)」を参照してください。  
  
 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]の詳細については、「 [Hyperion Essbase での SQL Server 2005 Reporting Services の使用](https://go.microsoft.com/fwlink/?LinkId=81970)」を参照してください。  
  
 [データ ソースの表に戻る](#DataSourcesTable)  
  
## <a name="see-also"></a>参照  
 [Reporting Services  のデータ接続、データソース、および接続文字列](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
 [レポートにデータを追加&#40;レポート ビルダーおよび SSRS&#41;](report-datasets-ssrs.md)  
  
  
