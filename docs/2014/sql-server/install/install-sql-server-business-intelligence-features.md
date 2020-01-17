---
title: SQL Server 2014 の BI 機能のインストール
ms.custom: ''
ms.prod: sql-server-2014
ms.reviewer: ''
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.date: 10/24/2018
ms.technology: install
ms.openlocfilehash: 93f362adfbc85500854943a479dac01988eb3a01
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952561"
---
# <a name="install-sql-server-2014-bi-features"></a>SQL Server 2014 の BI 機能のインストール

  Microsoft Business Intelligence プラットフォームに含まれる SQL Server 機能には、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、および分析データの作成または操作に使用されるいくつかのクライアント アプリケーションがあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップのドキュメントのこのセクションでは、これらの機能のインストール方法について説明します。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] および [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、スタンドアロン サーバーとして、スケールアウト構成で、または SharePoint ファームの共有サービス アプリケーションとしてインストールできます。 サービスをファームにインストールすると、SharePoint のみで使用できる BI 機能が有効になります。これらの機能には、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint と、 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]または [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の表形式モデルのデータベースで実行される [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] を対話形式でアドホック実行したレポート デザイナーの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] が含まれます。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、または PowerPivot for SharePoint のインストール手順について詳しく理解している場合は、特定のシナリオを有効にする手順のチェック リストに進みます。 詳細については、「 [SharePoint を使用した BI 機能のインストールのチェックリスト](checklists-for-installing-bi-features-with-sharepoint.md)」を参照してください。  
  
## <a name="contents"></a>目次

このセクションの内容:
  
|リンク|タスク|  
|----------|----------|  
|[SharePoint を使用した BI 機能のインストール用チェック リスト](checklists-for-installing-bi-features-with-sharepoint.md)|インストール方法が既にわかっており、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、または [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint のインストール手順について詳しく理解している場合は、このセクションのチェック リストでインストールの順序、アカウントと権限の要件、マルチサーバーやマルチ機能の配置などの高度なトポロジを配置した手順を確認できます。|  
|[SharePoint &#40;PowerPivot と Reporting Services を使用した SQL Server BI 機能のインストール&#41;](install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)|このセクションでは、SQL Server 機能を SharePoint 環境でインストールする方法について説明します。 ここでは、指定されたバージョンとエディションの SharePoint が与えられている場合に使用できる SQL Server 機能を示します。 また、PowerPivot for SharePoint と Reporting Services を SharePoint モードでインストールする手順についても説明します。|  
|[多次元モードおよびデータ マイニング モードでの Analysis Services のインストール](install-analysis-services-in-multidimensional-and-data-mining-mode.md)<br /><br /> [表形式モードでの Analysis Services のインストール](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services)<br /><br /> [Data Quality Services のインストール](../../data-quality-services/install-windows/install-data-quality-services.md)<br /><br /> [Integration Services のインストール](../../integration-services/install-windows/install-integration-services.md)<br /><br /> [マスター データ サービスのインストール](../../master-data-services/install-windows/install-master-data-services.md)<br /><br /> [Reporting Services ネイティブ モードのレポート サーバーのインストール](../../reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)|このセクションでは、Analysis Services、Integration Services、マスター データ サービス、および Reporting Services のインストール手順について説明します。Analysis Services と Reporting Services は SharePoint がなくてもインストールできます。 これは、*ネイティブモード*と呼ばれることもあり、Reporting Services と Analysis Services における最も一般的なインストールシナリオです。 このセクションでは、サーバーの操作コンテキストを直接指定するインストール オプションについて学習します。 Reporting Services の場合、これは、事前構成済みのサーバーまたは使用する前に複数の構成が必要になるサーバーになります。 Analysis Services の場合は、選択するインストール オプションによって、サーバーに配置できるプロジェクトの種類が決定されます。|  
|[SQL Server BI 機能のインストールに関する問題を確認またはトラブルシューティングする](../../../2014/sql-server/install/verify-or-troubleshoot-sql-server-bi-feature-installation-problems.md)|このセクションには、インストールを確認するための手順が含まれています。 また、Web 上での問題の解決情報へのリンクも用意されています。|  
  
## <a name="related-content"></a>関連コンテンツ  
  
|リンク|タスク|  
|----------|----------|  
|[SQL Server 2014 へのアップグレード](../../database-engine/install-windows/upgrade-sql-server.md)<br /><br /> [Analysis Services のアップグレード](../../database-engine/install-windows/upgrade-analysis-services.md)<br /><br /> [PowerPivot for SharePoint のアップグレード](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)<br /><br /> [Reporting Services のアップグレードと移行](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)|このセクションの手順では、サーバーとコンテンツを以前のリリースから [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアップグレードします。|  
|[SQL Server 2014 のアンインストール](uninstall-sql-server.md)<br /><br /> [PowerPivot for SharePoint のアンインストール](../../../2014/sql-server/install/uninstall-power-pivot-for-sharepoint.md)<br /><br /> [Reporting Services のアンインストール](../../../2014/sql-server/install/uninstall-reporting-services.md)|このセクションの手順では、BI 機能をアンインストールします。|  
  
## <a name="see-also"></a>参照

* [新&#40;機能 Reporting Services&#41;](../../../2014/reporting-services/what-s-new-reporting-services.md)

* [Analysis Services とビジネスインテリジェンスの新機能](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)

* [SQL Server 2014 のインストール](../../database-engine/install-windows/install-sql-server.md)

* [SQL Server 2014 へのアップグレード](../../database-engine/install-windows/upgrade-sql-server.md)
