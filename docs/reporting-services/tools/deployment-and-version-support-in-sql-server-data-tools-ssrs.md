---
title: SQL Server データ ツールの配置およびバージョン サポート (SSDT) | Microsoft Docs
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
ms.assetid: 36f5686d-7e40-4f31-be81-bd197ca33a02
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5f055219476507f52894fe7d5b246710e6054a20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571495"
---
# <a name="deployment-and-version-support-in-sql-server-data-tools-ssdt"></a>SQL Server データ ツールの配置およびバージョン サポート (SSDT)
  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] では、次のシナリオがサポートされます。  
  
-   レポート定義 (*.rdl) とレポート サーバー プロジェクト (\*.rptproj) を開く。  
  
-   レポート定義を作成する。  
  
-   レポート デザイナーでレポートをプレビューする。  
  
-   レポートをレポート サーバーに配置する。  
  
##  <a name="bkmk_ConfigurationandDeploymentProperties"></a> 構成プロパティと配置プロパティ  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] では、プロジェクト構成がサポートされています。 プロジェクトがレポートをプレビューまたは配置する手順の中でビルドされる場合、プロジェクト構成には、場所と動作を指定する一連のプロパティが含まれます。 プロジェクト構成の詳細については、Visual Studio のマニュアルを参照してください。  
  
 対象レポート サーバーと互換性のあるスキーマ バージョンへのレポート定義のアップグレードを制御するには、プロジェクト構成を使用します。 プロジェクト構成で制御されるプロパティには、対象レポート サーバー、ビルド プロセスでプレビューと配置のためにレポートを一時的に保存するフォルダー、およびエラー レベルが含まれます。  
  
 レポートは、レポート デザイナーでプレビューとしてレンダリングされるか、レポート サーバーに配置される前にビルドされます。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] **[プロジェクト プロパティ]** ダイアログ ボックスで、構成プロパティを設定します。  
  
 ビルド プロパティと配置プロパティには、以下の項目が含まれます。  
  
-   [OutputPath] は、ビルドの検証、配置、およびレポートのプレビューで使用されるレポート定義の保存先フォルダーのパスを識別するビルド プロパティです。  
  
-   [ErrorLevel] は、エラーとしてレポートされるビルドの問題の重大度を識別するビルド プロパティです。 [ErrorLevel] の値以下の重大度レベルを持つ問題は、エラーとしてレポートされます。それ以外の問題は、警告としてレポートされます。 詳細については、「[レポート デザイナーを使用してレポートをデザインする &#40;SSRS&#41;](../../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)」の「レポートの検証とエラー レベル」を参照してください。  
  
-   [TargetServerVersion] は、TargetServerURL プロパティで指定された対象レポート サーバーにインストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の想定されるバージョンを識別する配置プロパティです。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ダイアログ ボックスで以前のバージョンの **[プロジェクト プロパティ]** を指定しても、レポートが自動的に以前のバージョンに戻ることはありません。 このような場合、レポート サーバー プロジェクトには、2 つの異なる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]バージョンのレポートが含まれることになります。 レポート サーバー プロジェクトが配置されると、プロジェクト内のレポートはすべて、TargetServerVersion で指定されたバージョンに変換されます。  
  
 プロジェクトには複数のプロジェクト構成を追加できます。各プロジェクト構成は、異なるバージョンのレポート サーバーへの配置など、さまざまなシナリオで使用されます。 詳細については、「[配置プロパティを設定する (Reporting Services)](../../reporting-services/tools/set-deployment-properties-reporting-services.md)」および「[[プロパティ ページ] ダイアログ ボックス](../../reporting-services/tools/project-property-pages-dialog-box.md)」を参照してください。  
  
##  <a name="bkmk_SupportedVersions"></a> Supported Versions  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]レポート サーバー プロジェクトの 32 ビット開発環境であり、 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]ベースのコンピューターで実行できるようにデザインされていないため、 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]ベースのサーバーにはインストールされません。 ただし、x64 ベースのコンピューターでは [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] がサポートされています。  
  
 次の表では、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]でのレポートの作成およびパブリッシュをサポートするバージョンについて説明します。  
  
> [!NOTE]  
>  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]以降にスキーマが変更されました。  
  
|プロジェクトまたはファイルの種類|バージョン|レポートの作成|レポートのパブリッシュ|注|  
|--------------------------|-------------|--------------------|---------------------|-----------|  
|レポート サーバー プロジェクト<br /><br /> 内の複数の<br /><br /> レポート サーバー プロジェクト ウィザード|[!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]|2016 RDL スキーマ|[!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]||  
|レポート サーバー プロジェクト<br /><br /> 内の複数の<br /><br /> レポート サーバー プロジェクト ウィザード|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|2014 RDL スキーマ|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|レポート サーバー プロジェクト<br /><br /> 内の複数の<br /><br /> レポート サーバー プロジェクト ウィザード|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|2012 RDL スキーマ|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|レポート サーバー プロジェクト<br /><br /> 内の複数の<br /><br /> レポート サーバー プロジェクト ウィザード|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|2008 R2 RDL スキーマ|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|レポート サーバー プロジェクト<br /><br /> 内の複数の<br /><br /> レポート サーバー プロジェクト ウィザード|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|2008 RDL スキーマ|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーのみ|2003 RDL および 2005 RDL を 2008 RDL スキーマにローカルでアップグレードします。|  
  
 以前のバージョンのレポート定義スキーマでレポートを開く方法の詳細については、「 [レポートのアップグレード](../../reporting-services/install-windows/upgrade-reports.md)」を参照してください。 特定のレポート定義スキーマの詳細については、「 [レポート定義言語の仕様](https://go.microsoft.com/fwlink/?linkid=116865)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データ ソースとレポートのパブリッシュ](../../reporting-services/reports/publishing-data-sources-and-reports.md)  
  
  
