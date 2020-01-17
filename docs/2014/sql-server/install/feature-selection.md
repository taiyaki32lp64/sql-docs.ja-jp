---
title: 機能の選択 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- feature selection, Setup
helpviewer_keywords:
- SQL Server Installation Wizard, Components to Install page
- Components to Install page [SQL Server Installation Wizard]
ms.assetid: 73182088-153b-4634-a060-d14d1fd23b70
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0b516d76c1c814cb70215bfe37f3cddb60e614d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095223"
---
# <a name="feature-selection"></a>機能の選択
  **のインストールに含めるコンポーネントを選択するには、** インストール ウィザードの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [機能の選択] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ページのチェック ボックスを使用します。  
  
## <a name="installing-includessnoversionincludesssnoversion-mdmd-features"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能のインストール  
 **機能の選択** ページで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]機能は、2 つの主要なセクションに分かれています。**インスタンス機能**と**共有機能**します。  
  
 **インスタンス機能** は、各インスタンスにつき 1 回インストールされるコンポーネントを指します。つまり、特定のコンポーネントのコピーが複数 (インスタンスごとに 1 つ) 存在することになります。 インスタンスはそれぞれ独立して存在し、修正プログラムのレベルがインスタンスごとに異なる場合もあります。 サービス パックや累積的な更新プログラムも含め、何かの修正プログラムをインストールすると、特定のコンピューター上の 1 つのインスタンスについてのみファイルが更新されます。その際、共有機能が未更新であった場合には、共有機能も更新されます。  
  
 **共有機能** は、特定のコンピューター上のすべてのインスタンスに共通する機能をいいます。 共有機能はそれぞれ、サイド バイ サイドでインストール可能なサポート対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョン (サービス パック、累積的な更新プログラム、修正プログラム) との下位互換性を保つように設計されています。  
  
> [!NOTE]  
>  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター:** フェールオーバー クラスタリングをサポートする [!INCLUDE[ssDE](../../includes/ssde-md.md)] の機能は、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] コンポーネントと [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] コンポーネントだけです。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] や [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]など、その他のコンポーネントは、フェールオーバー クラスター ノードにインストールできますが、クラスターに対応していないため、フェールオーバー クラスター ノードがオフラインになると、そのサービスはフェールオーバーしません。 詳細については、「[Always On フェールオーバー クラスター インスタンス &#40;SQL Server&#41;](../failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)」を参照してください。  
  
### <a name="instance-features"></a>インスタンス機能  
 コンポーネントを選択すると、 **[説明]** ペインに、各コンポーネント グループの説明が表示されます。 チェック ボックスはいくつでもオンにできます。 続行するには、選択を行う必要があります。  
  
|機能のインストール|説明|  
|--------------|-----------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] サービス|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]には、データを格納、処理、およびセキュリティで保護するための主要サービスである[!INCLUDE[ssDE](../../includes/ssde-md.md)]、レプリケーション、フルテキスト検索、リレーショナル データと XML データの管理ツール、および [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) が含まれます。 データベース エンジンの機能を次に示します。<br /><br /> [!INCLUDE[ssDE](../../includes/ssde-md.md)] は、データの格納、処理、セキュリティ確保のための中心的なサービスです。<br /><br /> レプリケーション:省略可能:レプリケーションとは、あるデータベースから別のデータベースにデータやデータベース オブジェクトをコピーおよび配布し、それらのデータベースを同期させて一貫性を保つための一連のテクノロジです。<br /><br /> フルテキスト検索:省略可能:フルテキスト検索は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルのプレーン文字ベースのデータに対してフルテキスト クエリを実行するための機能を提供します。<br /><br /> [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]:省略可能:[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) は、データ ソース内で一貫性のない不適切なデータを発見できるデータ クレンジング ソリューションであり、データのクレンジングをコンピューター支援型のインタラクティブな方法で行うことができます。 DQS サーバーをインストールするには、このチェック ボックスをオンにします。 DQS サーバーのインストールを完了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]*するには、* のインストールを完了した後で、DQSInstaller.exe ファイルを実行する必要があります。 SQL server の既定のインスタンスをインストールした場合は、このファイルは C:\Program files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12. します。MSSQLSERVER\MSSQL\Binn します。<br /><br /> <br /><br /> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター:** レプリケーションとフルテキスト検索のコンポーネントは必須であり、セットアップによって自動的に選択[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]フェールオーバー クラスタ リングのインストール データベース エンジン サービスを選択するとします。|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] には、オンライン分析処理 (OLAP) アプリケーションおよびデータ マイニング アプリケーションを作成および管理するためのツールが含まれます。|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -ネイティブ|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モードには、表形式、マトリックス形式、グラフィカル形式、および自由形式のレポートを作成、管理、配置するためのサーバー コンポーネントとクライアント コンポーネントが含まれます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、レポート アプリケーション開発用の拡張可能プラットフォームとしても使用できます。|  
  
> [!IMPORTANT]
>  1.  セットアップでは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] スケールアウト配置の複数ノードに対して負荷分散と単一 URL アドレス指定が構成されません。 スケールアウト配置を完了するには、Windows Server、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Application Center、またはサード パーティ製クラスター管理ソフトウェアを使用する必要があります。 Web ファーム配置のセットアップの詳細については、次を参照してください。 [Reporting Services のスケール アウト配置構成](https://go.microsoft.com/fwlink/?LinkId=199448)(https://go.microsoft.com/fwlink/?LinkId=199448) します。  
> 2.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンポーネントのブラウザーの要件については、「[Reporting Services と Power View のブラウザー サポートの計画 &#40;Reporting Services 2014&#41;](../../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)」を参照してください。  
> 3.  64 ビット プラットフォームと、64 ビット サーバーの 32 ビット サブシステム (WOW64) 上では、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を並列構成で同時に実行することはできません。  
  
### <a name="shared-features"></a>共有機能  
 1 つのコンピューター上のすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスによって共有される機能は、単一のディレクトリにインストールされます。 これらの機能を次に示します。  
  
|機能|説明|  
|-------------|-----------------|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モードは、電子メール、複数のファイル形式、および対話的な Web ベースの形式でレポートの作成、管理、および配信を行う、サーバー ベースのアプリケーションです。 SharePoint モードでは、レポートの表示と管理の機能を SharePoint 製品に統合します。 詳細については、「[Reporting Services レポート サーバー &#40;SharePoint モード&#41;](../../../2014/reporting-services/reporting-services-report-server-sharepoint-mode.md)」を参照してください。|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 製品用アドイン|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 製品用アドインには、SharePoint 製品を SharePoint モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーと統合するための管理コンポーネントとユーザー インターフェイス コンポーネントが含まれます。 詳細については、「 [SharePoint 製品用 Reporting Services アドインの検索場所](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)」を参照してください。|  
|Data Quality クライアント|Data Quality クライアントは、DQS サーバーに接続するスタンドアロン アプリケーションであり、直感的なグラフィカル ユーザー インターフェイスを使用して、データ クレンジング操作やデータ照合操作を実行したり、DQS の管理タスクを実行したりすることができます。|  
|クライアント ツール接続|クライアント ツールには、DB-Library、OLEDB for OLAP、ODBC、ADODB、ADOMD+ 用のネットワーク ライブラリなど、クライアントとサーバー間の通信を行うためのコンポーネントが含まれます。|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は、データを移動、コピー、変換するためのグラフィカル ツールおよびプログラミング可能なオブジェクトのセットです。|  
|クライアント ツールの旧バージョンとの互換性|クライアント ツールの旧バージョンとの互換性には、次のコンポーネントが含まれます。<br /><br /> SQL 分散管理オブジェクト (SQL-DMO)。 詳細については、「[SQL Server 2014 で提供が中止された機能](../../../2014/getting-started/discontinued-sql-server-features-in-sql-server-2014.md)」を参照してください。<br /><br /> Decision Support オブジェクト (DSO)。 詳細については、「[SQL Server 2014 の Analysis Services 機能における重大な変更](../../../2014/analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2014.md)」を参照してください。|  
|クライアント ツール SDK|プログラマのためのリソースを含むソフトウェア開発キットが含まれています。|  
|Documentation コンポーネント|Documentation コンポーネントには、ヘルプ コンテンツを表示および管理するためのコンポーネントが含まれます。|  
|管理ツール - 基本|**管理ツール - 基本:** これには、次の内容が含まれます。<br /><br /> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] サポート、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]、 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]、 **sqlcmd**ユーティリティ、および[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]PowerShell プロバイダー<br /><br /> **管理ツール - 完全:** これには、基本的なバージョンのコンポーネントに加え、次のコンポーネントも含まれます。<br /><br /> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] による [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、および [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のサポート<br /><br /> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]<br /><br /> Database Engine Tuning Advisor<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ管理|  
|分散再生コントローラー|分散再生コントローラーは、分散再生クライアントのアクションを統制します。 各分散再生環境には、コントローラーのインスタンスを 1 つだけ置くことができます。 詳細については、「 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)」を参照してください。|  
|分散再生クライアント|分散再生クライアントは、SQL Server のインスタンスに対するワークロードをシミュレートします。 各分散再生環境には、1 つまたは複数のクライアントを置くことができます。 詳細については、「 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)」を参照してください。|  
|SQL クライアント接続 SDK|データベース アプリケーション開発用の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (ODBC/OLE DB) SDK が含まれます。|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] は、情報の精度向上と監査を目的として、異種システムのデータを全社規模で単一のマスター データ ソースとして統合するプラットフォームです。 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] を選択すると、 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]、アセンブリ、Windows PowerShell スナップインのほか、Web アプリケーションおよび Web サービス用のフォルダーおよびファイルがインストールされます。|  
  
 既定では、共有コンポーネントは %Program Files%Microsoft SQL Server\\にインストールされます。 インストール パスを変更するには、 **[参照]** ボタンをクリックします。 1 つの共有コンポーネントのインストール パスを変更すると、他の共有コンポーネントのパスも変更されます。 以降のインストールでは、最初のインストールと同じ場所に共有コンポーネントがインストールされます。  
  
 **[インスタンス ルート ディレクトリ]** : 既定では、インスタンス ルート ディレクトリは、C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\ になります。 既定以外のルート ディレクトリを指定するには、 **[参照]** ボタンをクリックするか、パス名を入力します。  
  
 x64 ベースのオペレーティング システムでは、64 ビット コンポーネントのインストール先と、32 ビット コンポーネントの WOW64 サブシステム上のインストール先を指定できます。  
  
## <a name="disk-space-requirements"></a>必要なディスク領域  
 [ディスク コストの概要] ページを使用して、インストール対象として選択した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能に必要なディスク領域を調べます。  
  
### <a name="options"></a>および  
 必要なディスク領域が大きすぎる場合は、次の方法を検討してください。  
  
-   インストール ディレクトリを、ディスク領域の大きいディスクに変更します。  
  
-   インストールする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能を変更します。  
  
-   他のファイルやアプリケーションを移動して、指定したドライブ上の空き領域を増やします。  
  
## <a name="installing-adventureworks-sample-databases"></a>AdventureWorks サンプル データベースのインストール  
 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ時にサンプル データベースとサンプル コードはインストールされません。 サンプル データベースとサンプル コードのインストールの詳細については、次を参照してください。、 [Microsoft SQL Server コミュニティのプロジェクトとサンプル](https://go.microsoft.com/fwlink/?LinkId=87843)(https://go.microsoft.com/fwlink/?LinkId=87843) します。  
  
 サンプルの詳細については、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] をインストールした後で確認できます。 **開始** メニューのをクリックして**すべてのプログラム**、をクリックして **[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** 、をクリックして**マニュアルとチュートリアル**をクリックして **[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サンプルの概要**します。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2014 のエディションとコンポーネント](../editions-and-components-of-sql-server-2016.md)  
  
  
