---
title: SharePoint ライブラリへのレポートのパブリッシュ | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], reports in SharePoint integrated mode
- SharePoint integration [Reporting Services], publishing to a library
- publishing reports [Reporting Services], to a SharePoint library
ms.assetid: 3f6dfc28-50d8-4231-bd25-871b5f77cce6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1b10c9dbfa67a632ce007c1406f8b806a03475b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571046"
---
# <a name="publish-a-report-to-a-sharepoint-library"></a>SharePoint ライブラリへのレポートのパブリッシュ
  SharePoint 統合用に構成されている SharePoint サイトにレポートをパブリッシュするには、レポート デザイナーでレポート プロジェクトのプロパティを設定する必要があります。 プロジェクトのプロパティでは、サーバー、レポート、および共有データ ソースへの参照はすべて、完全修飾 URL で指定する必要があります。 レポート定義では、サブレポートや詳細レポートへの参照、および Web ベースの画像などのリソースへの参照はすべて完全修飾 URL で指定する必要があります。  
  
 プロジェクトにプロパティを設定するには、SharePoint サイトの **メンバー** 権限または **所有者** 権限が必要です。 詳細については、「 [SharePoint モードのレポート サーバー上のパブリッシュされたレポート アイテムの URL の例 (SSRS)](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)」を参照してください。  
  
### <a name="to-publish-a-report-to-a-sharepoint-site"></a>レポートを SharePoint サイトにパブリッシュするには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で既存または新規のレポート サーバー プロジェクトを開きます。  
  
2.  **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 _[\<プロジェクト>_ **プロパティ ページ]** ダイアログ ボックスが開きます。  
  
3.  **[構成]** ボックスで、レポートのビルドとパブリッシュに使用するソリューション ビルド構成の名前を選択します。 現在の構成は **[アクティブ]** ( *\<configuration>* ) として表示されます。  
  
4.  プロジェクトの共有データ ソースをパブリッシュし、以前にパブリッシュされた共有データ ソースを上書きするには、 **[OverwriteDataSources]** を **[True]** に設定します。  
  
5.  (省略可) **[TargetDataSourceFolder]** には、SharePoint ライブラリまたはライブラリ フォルダーの URL ( `https://TestServer/TestSite/Documents/DataSources`) として表示されます。  
  
     値を指定しない場合は、 **[TargetReportFolder]** の値が使用されます。  
  
6.  **[TargetReportFolder]** に、ライブラリまたはライブラリ フォルダーの URL (`https://TestServer/TestSite/Documents/Reports` など) を入力します。  
  
7.  **[TargetServerURL]** に、SharePoint トップレベル サイトまたはサブサイトの URL を入力します。 サイトを指定しなかった場合は、既定のトップレベル サイトが使用されます (たとえば、 `https://servername`、 `https://servername/site`、 `https://servername/site/subsite`) として表示されます。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. ソリューション エクスプローラーで、パブリッシュするレポートを右クリックし、 **[配置]** をクリックします。 これで、 **[TargetReportFolder]** で指定した場所にレポートがパブリッシュされます。 配置エラーは出力ウィンドウに表示されます。  
  
## <a name="see-also"></a>参照  
 [[プロパティ ページ] ダイアログ ボックス](../../reporting-services/tools/project-property-pages-dialog-box.md)   
 [配置プロパティを設定する &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
 [レポート サーバーへのレポートのパブリッシュ](../../reporting-services/reports/publishing-reports-to-a-report-server.md)   
 [SharePoint モードのレポート サーバー上のパブリッシュされたレポート アイテムの URL の例 (SSRS)](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [レポートで Office Data Connection (.odc) を使用する (Reporting Services の SharePoint 統合モード)](../../reporting-services/report-data/use-an-office-data-connection-odc-with-reports.md)  
  
  
