---
title: 多次元およびデータマイニングモードでの Analysis Services のインストール |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Analysis Services, about installing Analysis Services
- installing Analysis Services
- SSAS, installing
- Analysis Services, installing
- SQL Server Analysis Services, installing
ms.assetid: 8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 2353d2f623a5aa0e0f1f5c25710724f836093998
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890375"
---
# <a name="install-analysis-services-in-multidimensional-and-data-mining-mode"></a>多次元モードおよびデータ マイニング モードでの Analysis Services のインストール
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] には、ビジネス インテリジェンス アプリケーション用のオンライン分析処理 (OLAP) 機能とデータ マイニング機能が用意されています。 このリリースでは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] *多次元モード*でをインストールするときに、OLAP データベースとデータマイニングモデルのサポートを利用できます。 多次元モードは、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] が実行される 3 つのサーバー モードのうちの 1 つです。 これは既定のモードです。 既定値を使用して [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] をインストールすると、多次元データベースとデータ マイニング モデルを実行するインスタンスがインストールされます。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は複数インスタンスに対応します。つまり、1 台のコンピューターに複数の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスをインストールすることも、新しいバージョンの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスを古いバージョンと共存して実行することもできます。 サーバー モードはインスタンスに固有です。 他のモードを使用するには、サーバーの追加インスタンスをインストールする必要があります。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、単体でインストールすることも、他のコンポーネントと共にインストールすることもできます。 だけ[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]をインストールする場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インストールウィザードの [機能の選択] ページで **[Analysis Services]** を選択すると、次の機能がインストールされます。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースとデータ マイニング モデルを実行するための [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバー  
  
-   ソース データベースへの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データのアクセスに使用されるデータ プロバイダー  
  
-   SQL Server 構成マネージャー  
  
## <a name="choosing-additional-features"></a>追加機能の選択  
 Analysis Services OLAP およびデータ ウェアハウス ソリューションでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの開発、配置、および管理を可能にするためにその他の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] コンポーネントもインストールする必要があります。 一般的なユーザー シナリオでは、データベース サービスに加えて次の機能もインストールします。  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]: Analysis Services データ構造およびデータ マイニング モデルの作成と表示に使用されます。  
  
-   クライアントツール接続コンポーネント。クライアントとサーバー間の通信に使用されます。これには、DB-LIBRARY、ODBC、および OLE DB 用のネットワークライブラリが含まれます。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]: データの移動、コピー、および変換に使用される、グラフィカル オブジェクトおよびプログラミング可能なオブジェクトのセットです。  
  
-   管理ツール: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャー、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]、レプリケーション モニターなどです。  
  
## <a name="installation-tasks"></a>インストール作業  
 インストール作業では、次の操作を行います。  
  
|リンク|処理手順|  
|-----------|-----------|  
|SQL Server 2014 をインストールし、 [Windows サービスアカウントとアクセス許可を構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)する[ためのハードウェアとソフトウェアの要件](hardware-and-software-requirements-for-installing-sql-server.md)。|セットアップを実行する前に、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインストールの前提条件を確認し、サーバーの準備に使用するアカウントを決定します。|  
|[インストール&#40;ウィザードのセットアップ&#41;から SQL Server 2014 をインストール](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)します。|SQL Server セットアップを実行して、ソフトウェアをインストールします。|  
|[Analysis Services のアクセスを許可するための Windows ファイアウォールの構成](https://docs.microsoft.com/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)|セットアップが完了したら、ファイアウォールの設定を構成して、サーバーに対するリモート接続を許可する必要があります。|  
|[オブジェクトと操作へのアクセスの承認 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services)|Analysis Services データベースにアクセスするユーザーには、サーバー上の少なくとも 1 つのデータベースに対する読み取り権限が必要です。|  
  
## <a name="related-content"></a>関連コンテンツ  
 その他のセットアップ コンテンツは次のトピックで確認できます。  
  
 [表形式モードでの Analysis Services のインストール](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services)  
  
 [PowerPivot for SharePoint 2010 のインストール](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
 [Analysis Services インスタンスのサーバー モードの決定](https://docs.microsoft.com/analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance)  
  
 [データマイニングアドインの SQL Server](https://go.microsoft.com/fwlink/?LinkId=197091)  
  
 既定では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ時にサンプル データベース、サンプル コード、およびクライアント アプリケーション アドインはインストールされません。 サンプル データベースとサンプル コードをインストールする場合は、 [CodePlex Web サイト](https://go.microsoft.com/fwlink/?LinkId=87843)を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server 2012 の各エディションがサポートする機能](https://go.microsoft.com/fwlink/?linkid=232473)   
 [言語および照合順序 (Analysis Services)](../../../2014/analysis-services/languages-and-collations-analysis-services.md)   
 [Analysis Services のアップグレード](../../database-engine/install-windows/upgrade-analysis-services.md)  
  
  
