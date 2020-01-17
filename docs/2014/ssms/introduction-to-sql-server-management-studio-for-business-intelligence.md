---
title: ビジネスインテリジェンスの SQL Server Management Studio の概要 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio for Integration Services
- SQL Server Management Studio for Reporting Services
- SQL Server Management Studio for Analysis Services
ms.assetid: ffaa77b7-03d0-4d7a-aa42-c5091a4f2ceb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3a914aeeae889189453b4f4e6f47ebfbcd0fc44c
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892272"
---
# <a name="introduction-to-sql-server-management-studio-for-business-intelligence"></a>ビジネス インテリジェンスに使用される SQL Server Management Studio の概要
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]、および [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] のアクセス、構成、管理を行うには、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を使用します。 この 3 つのビジネス インテリジェンス テクノロジは [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]を使用しますが、各テクノロジに関連付けられている管理タスクは少しずつ異なります。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]、および [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の各ソリューションを作成および変更するには、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]ではなく [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]を使用します。 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] は、 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[vsprvs](../includes/vsprvs-md.md)]をベースとする開発環境です。  
  
## <a name="managing-analysis-services-solutions-using-sql-server-management-studio"></a>SQL Server Management Studio を使用した Analysis Services ソリューションの管理  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] では、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] オブジェクトの管理を行うことができます (バックアップの実行やオブジェクトの処理など)。  
  
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] では、多次元式 (MDX)、データ マイニング拡張機能 (DMX)、および XML for Analysis (XMLA) で作成されるスクリプトの開発と保存を行う [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] スクリプト プロジェクトが提供されます。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] スクリプト プロジェクトは、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスで管理タスクを実行したり、データベースやキューブなどのオブジェクトを再作成したりする場合に使用します。 たとえば、既存の [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスで直接新しいオブジェクトを作成する XMLA スクリプトを [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] スクリプト プロジェクトで開発することができます。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] スクリプト プロジェクトは、ソリューションの一部として保存し、ソース コード コントロールに統合できます。  
  
 の使用[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]方法の詳細については、「 [SQL Server Management Studio の Analysis Services Scripts プロジェクト](https://docs.microsoft.com/analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio)」を参照してください。  
  
## <a name="managing-integration-services-solutions-using-sql-server-management-studio"></a>SQL Server Management Studio を使用した Integration Services ソリューションの管理  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] では、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスを使用して、パッケージの管理および実行中のパッケージの監視を行うことができます。 また [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] では、パッケージをフォルダーに編成できるほか、パッケージの実行、インポート、エクスポート、データ変換サービス (DTS) パッケージの移行、および [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージのアップグレードを行うことができます。  
  
## <a name="managing-reporting-services-projects-using-sql-server-management-studio"></a>SQL Server Management Studio を使用した Reporting Services プロジェクトの管理  
 SQL Server Management Studio では、Reporting Services の機能の有効化、サーバーとデータベースの管理、およびロールとジョブの管理を行うことができます。  
  
 [共有スケジュール] フォルダーを使用して共有スケジュールを管理し、レポート サーバー データベース (ReportServer、ReportServerTempdb) を管理します。 また、レポート サーバー データベースを新規または別の SQL Server データベース エンジン ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]) に移動する場合は、master システム データベースで RSExecRole を作成します。 これらの作業の詳細については、次のトピックを参照してください。  
  
-   [SQL Server Management Studio の Reporting Services &#40;SSRS&#41;](../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)  
  
-   [レポートサーバーデータベース&#40;の SSRS ネイティブモードの管理&#41;](../reporting-services/report-server/report-server-database-ssrs-native-mode.md)  
  
-   [RSExecRole を作成する](../reporting-services/security/create-the-rsexecrole.md)  
  
 また、各種機能の有効化と構成、サーバーの既定値の設定、およびロールとジョブの管理を行うことで、サーバーを管理します。 これらの作業の詳細については、次のトピックを参照してください。  
  
-   [レポート サーバーのプロパティを設定する (Management Studio)](../reporting-services/tools/set-report-server-properties-management-studio.md)  
  
-   [ロールを作成、削除、または変更する (Management Studio)](../reporting-services/security/role-definitions-create-delete-or-modify.md)  
  
-   [Reporting Services のクライアント側印刷機能の有効化と無効化](../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)  
  
## <a name="see-also"></a>関連項目  
 [SQL Server データ ツール (SSDT) を使用した多次元モデルの作成](https://docs.microsoft.com/analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt)   
 [SQL Server Data Tools &#40;SSDT の Reporting Services&#41;](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)  
  
  
