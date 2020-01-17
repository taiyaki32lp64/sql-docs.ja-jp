---
title: SharePoint ライブラリへの共有データ ソースのパブリッシュ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], publishing to a SharePoint library
- SharePoint integration [Reporting Services], publishing to a library
- publishing reports [Reporting Services], to a SharePoint library
ms.assetid: 966ed425-3ce2-4e76-8237-3c1c977954ae
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2866b0b8a72e48dbb6c93b37b2a1a83e20e12821
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102539"
---
# <a name="publish-a-shared-data-source-to-a-sharepoint-library"></a>SharePoint ライブラリへの共有データ ソースのパブリッシュ
  SharePoint 統合モードで実行されているレポート サーバーに共有データ ソースをパブリッシュするには、レポート デザイナーでレポート プロジェクトのプロパティを設定する必要があります。 プロジェクトのプロパティでは、サーバー、レポート、および共有データ ソースへの参照はすべて、完全修飾 URL で指定する必要があります。  
  
 また、SharePoint サイトの **メンバー** 権限または **所有者** 権限が必要です。 詳細については、「 [SharePoint モードのレポート サーバー上のパブリッシュされたレポート アイテムの URL の例 &#40;SSRS&#41;](../tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)」を参照してください。  
  
### <a name="to-publish-a-shared-data-source-to-a-sharepoint-site"></a>SharePoint サイトに共有データ ソースをパブリッシュするには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、既存または新規のレポート サーバー プロジェクトを開きます。  
  
2.  **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 _[\<プロジェクト>_ **プロパティ ページ]** ダイアログ ボックスが開きます。  
  
3.  SharePoint サイトへのパブリッシュに使用する **[構成]** を選択します。  
  
4.  プロジェクトの共有データ ソースをパブリッシュし、以前にパブリッシュされた共有データ ソースを上書きするには、 **[OverwriteDataSources]** を **[True]** に設定します。  
  
5.  (省略可) **[TargetDataSourceFolder]** には、SharePoint ライブラリまたはライブラリ フォルダーへの URL を入力します。 たとえば、  *http://TestServer/TestSite/Documents/DataSources* します。  
  
     値を指定しない場合は、 **[TargetReportFolder]** の値が使用されます。  
  
6.  **[TargetReportFolder]** に、ライブラリまたはライブラリ フォルダーの URL を入力します。 たとえば、「http: *//TestServer/TestSite/Documents/Reports*」と入力します。  
  
7.  **[TargetServerURL]** に、SharePoint トップレベル サイトまたはサブサイトの URL を入力します。 サイトを指定しなかった場合は、既定のトップレベル サイトが使用されます。 たとえば、「 http://*servername*」、「 http://*servername*/*site*」、または「 http://*servername*/*site*/*subsite*」のように指定します。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. ソリューション エクスプローラーで、パブリッシュする共有データ ソースを右クリックし、 **[配置]** をクリックします。 これで、 **[TargetDataSourceFolder]** で指定した場所にデータ ソースがパブリッシュされます。 配置エラーは出力ウィンドウに表示されます。  
  
    > [!NOTE]  
    >  共有データ ソースを SharePoint サイトにパブリッシュすると、ファイル名拡張子が .rsds に変更されます。 共有データ ソースの編集と管理は、SharePoint サイト上で直接行うことができます。 詳細については、「[共有データ ソースを作成および管理する &#40;Reporting Services の SharePoint 統合モード&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [SharePoint ライブラリへのレポートのパブリッシュ](publish-a-report-to-a-sharepoint-library.md)   
 [SharePoint モードのレポート サーバー上のパブリッシュされたレポート アイテムの URL の例 &#40;SSRS&#41;](../tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [[プロパティ ページ] ダイアログ ボックス](../tools/project-property-pages-dialog-box.md)   
 [配置プロパティを設定する &#40;Reporting Services&#41;](../tools/set-deployment-properties-reporting-services.md)   
 [レポート サーバーへのレポートのパブリッシュ](publishing-reports-to-a-report-server.md)   
 [レポートで Office Data Connection &#40;.odc&#41; を使用する &#40;Reporting Services の SharePoint 統合モード&#41;](../report-data/use-an-office-data-connection-odc-with-reports.md)  
  
  
