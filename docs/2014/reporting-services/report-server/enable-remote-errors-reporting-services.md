---
title: リモート エラーの有効化 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- remote data source [Reporting Services]
- EnableRemoteError server property
ms.assetid: 5f05022b-d557-43e0-b50a-f5e2a1846b83
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e2d239dfc3d094f72d40ce6d020610fe1c0eabbc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103806"
---
# <a name="enable-remote-errors-reporting-services"></a>リモート エラーの有効化 (Reporting Services)
  リモート サーバーで発生するエラー状態に関する追加情報が返されるように、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーのサーバー プロパティを設定できます。 エラー メッセージに "このエラーの詳細を表示するには、ローカルのサーバー コンピューターでレポート サーバーを開くか、リモート エラーを有効にしてください。" と表示されている場合は、`EnableRemoteErrors` プロパティを設定すると、問題のトラブルシューティングに役立つ追加情報にアクセスできます。 詳細については、 [オンライン ブックの「](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md) レポート サーバーのシステム プロパティ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 」を参照してください。  
  
 **このトピックの内容:**  
  
-   [SharePoint モードのリモート エラーの有効化](#bkmk_sharepoint)  
  
-   [SQL Server Management Studio を使用したリモート エラーの有効化 (ネイティブ モード)](#bkmk_mgtStudio)  
  
-   [スクリプトを使用したリモート エラーの有効化 (ネイティブ モード)](#bkmk_script)  
  
-   [ConfigurationInfo テーブルの変更 (ネイティブ モード)](#bkmk_ConfigurationInfo)  
  
##  <a name="bkmk_sharepoint"></a> SharePoint モードのリモート エラーの有効化  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モードのリモート エラーを有効化する手順は 2 種類あります。 この手順は、レポート サーバーのアーキテクチャによって異なります。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] リリースで導入されたアーキテクチャに基づく新しい SharePoint サービスでは、各 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーション用に構成できる設定が使用されます。 旧式のアーキテクチャでは、単一のサイト レベル設定が使用されます。  
  
#### <a name="enable-remote-errors-for-a-reporting-services-service-application"></a>Reporting Services サービス アプリケーションのリモート エラーの有効化  
  
1.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] か、またはそれ以降バージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]を使用してインストールされた SharePoint モード レポート サーバーの場合は、サービス アプリケーション設定 **[リモート エラーを有効にする]** を有効にします。 この設定は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションごとに構成できます。  
  
2.  SharePoint サーバーの全体管理で、 **[アプリケーション構成の管理]** の **[サービス アプリケーションの管理]** をクリックします。  
  
3.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションを探し、サービス アプリケーションの名前をクリックします。  
  
4.  **[システム設定]** をクリックします。  
  
5.  **[セキュリティ]** セクションで **[リモート エラーを有効にする]** をクリックします。  
  
6.  **[OK]** をクリックします。  
  
#### <a name="enable-remote-errors-for-a-sharepoint-site"></a>SharePoint サイトのリモート エラーの有効化  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] より前のバージョンの [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]を使用してインストールされた SharePoint モード レポート サーバーの場合は、サイト設定 **[ローカル モードでのリモート エラーを有効にします]** を有効にします。  
  
2.  **[サイトの操作]** で、変更するサイトの **[サイトの設定]** をクリックします。  
  
3.  **[Reporting Services]** グループで **[Reporting Services のサイト設定]** をクリックします。  
  
4.  **[ローカル モードでのリモート エラーを有効にします]** をクリックします。  
  
5.  **[OK]** をクリックします。  
  
##  <a name="bkmk_mgtStudio"></a> SQL Server Management Studio を使用したリモート エラーの有効化 (ネイティブ モード)  
  
1.  Management Studio を起動し、レポート サーバー インスタンスに接続します。 詳細については、 [オンライン ブックの「](../tools/connect-to-a-report-server-in-management-studio.md) Management Studio でレポート サーバーに接続する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 」を参照してください。  
  
2.  レポート サーバー ノードを右クリックして、 **[プロパティ]** をクリックします。  
  
3.  **[詳細設定]** をクリックすると、プロパティ ページが表示されます。 詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「[サーバーのプロパティ &#40;[詳細設定] ページ&#41; - Reporting Services」](../tools/server-properties-advanced-page-reporting-services.md)を参照してください。  
  
4.  `EnableRemoteErrors`、`True`します。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="bkmk_script"></a> スクリプトを使用したリモート エラーの有効化 (ネイティブ モード)  
  
1.  テキスト ファイルを作成し、そのファイルに次のスクリプトをコピーします。  
  
    ```  
    Public Sub Main()  
      Dim P As New [Property]()  
      P.Name = "EnableRemoteErrors"  
      P.Value = True  
      Dim Properties(0) As [Property]  
      Properties(0) = P  
      Try  
        rs.SetSystemProperties(Properties)  
        Console.WriteLine("Remote errors enabled.")  
      Catch SE As SoapException  
        Console.WriteLine(SE.Detail.OuterXml)  
      End Try  
    End Sub  
    ```  
  
2.  ファイルを EnableRemoteErrors.rss として保存します。  
  
3.  **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。「 **cmd**」と入力して **[OK]** をクリックすると、コマンド プロンプト ウィンドウが開きます。  
  
4.  作成した .rss ファイルが保存されているディレクトリに移動します。  
  
5.  次のコマンド ラインを入力します。 *servername* は実際のサーバー名に置き換えます。  
  
    ```  
    rs -i EnableRemoteErrors.rss -s http://servername/ReportServer  
    ```  
  
6.  詳細については、「[RS.exe ユーティリティ (SSRS)](../tools/rs-exe-utility-ssrs.md)」を参照してください。  
  
##  <a name="bkmk_ConfigurationInfo"></a> ConfigurationInfo テーブルの変更 (ネイティブ モード)  
  
1.  > [!NOTE]  
    >  編集することができます、 **ConfigurationInfo**を設定するレポート サーバー データベース内のテーブル`EnableRemoteErrors`に`True`が、設定を変更する SQL Server Management Studio またはスクリプトのいずれを使用する場合は、レポート サーバーはアクティブに使用すると、します。 データベース内で設定を変更した場合、変更は [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスの再起動後に反映されます。  
  
  
