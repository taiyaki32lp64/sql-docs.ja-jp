---
title: Reporting Services のクライアント側印刷機能の有効化と無効化 | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- pdf
- viewer
- reportviewer
- toolbar
ms.assetid: 0e709c96-7517-4547-8ef6-5632f8118524
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ae8d963b599191970497d841a6caa1f73fd920b3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580350"
---
# <a name="enable-and-disable-client-side-printing-for-reporting-services"></a>Reporting Services のクライアント側印刷機能の有効化と無効化

  レポート ビューアーのツールバーにある印刷ボタンをクリックすると、ブラウザーに表示される [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポートのクライアント側印刷機能で Portable Document Format (PDF) 形式が使用されます。 新しいリモート印刷の動作では、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]に含まれている PDF 表示拡張機能を使用して、レポートを PDF 形式で表示します。 PDF 形式のレポートはダウンロードできます。また、PDF ファイルを表示するためのアプリケーションがインストールされている場合は、印刷ボタンをクリックすると、PDF ファイルのページ サイズ、印刷の向き、プレビュー画像など、ページに共通の設定項目が印刷ダイアログ ボックスに表示されます。 クライアント側印刷機能は既定で有効になっていますが、無効にして使用できないようにすることもできます。  
  
 以前のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] で使用されていた ActiveX コントロールは、レポート サーバーからクライアント コンピューターにダウンロードする必要がありました。 レポート サーバーを SQL Server 2016 以降にアップグレードしても、この印刷コントロールはレポート サーバーまたはクライアント コンピューターから削除されません。  

##  <a name="bkmk_clientside_printexpereince"></a> 印刷時の動作  
 レポート ビューアーのツールバーで印刷 ![htmlviewer_print](../../reporting-services/report-server/media/htmlviewer-print.png "htmlviewer_print") ボタンをクリックしたときの動作は、クライアント コンピューターにインストールされている PDF 閲覧アプリケーションの種類と、使用しているブラウザーの種類によって異なります。   クライアント コンピューターの環境に応じて、PDF ファイルのダウンロード、ダイアログ ボックスでの印刷オプションの設定、またはその両方を行うことができます。  
  
 ![レポート ツールバー](../../reporting-services/media/ssrs-htmlviewer-toolbar.png "レポート ツールバー")  
  
|||  
|-|-|  
|最初のダイアログ ボックスは、すべてのブラウザーで同じです。印刷の向きなどの基本的なレイアウト プロパティを変更できます。 **[印刷]** をクリックしたときの動作は、使用しているブラウザーによって多少異なります。|![ssrs_pdfprint_chrome1](../../reporting-services/report-server/media/ssrs-pdfprint-chrome1.png "ssrs_pdfprint_chrome1")|  
|Chrome では、詳細なブラウザーの印刷ダイアログ ボックスが開きます。   印刷設定を変更したり、印刷を実行したり、オペレーティング システムの印刷ダイアログ ボックスを開いたりすることができます。|![ssrs_pdfprint_chrome2](../../reporting-services/report-server/media/ssrs-pdfprint-chrome2.png "ssrs_pdfprint_chrome2") ![ssrs_pdfprint_chrome3.png](../../reporting-services/report-server/media/ssrs-pdfprint-chrome3-png.png "ssrs_pdfprint_chrome3.png")|  
|PDF リーダー アプリケーションがインストール済みの場合、印刷ボタンをクリックすると PDF ファイルのプレビュー ウィンドウが表示され、PDF ファイルを保存または印刷することができます。||  
|PDF リーダー アプリケーションがインストールされていない場合は、次の 2 種類の動作になります。<br /><br /> レポートが自動的に表示され、使用しているブラウザーのダウンロード プロセスを使用して PDF ファイルがダウンロードされます。   **注:** 複雑なレポートになるほど、 **[印刷]** をクリックしてからブラウザーのダウンロード通知が表示されるまでの時間が長くなります。 **[レポートの PDF を表示するには、ここをクリックしてください。]** をクリックして、PDF ファイルを再度ダウンロードすることもできます。<br /><br /> **[レポートの PDF を表示するには、ここをクリックしてください。]** をクリックして、PDF ファイルをダウンロードします。|![ssrs_pdfprint_firefox2](../../reporting-services/report-server/media/ssrs-pdfprint-firefox2.png "ssrs_pdfprint_firefox2")|  
  
##  <a name="bkmk_troubleshoot_clientsideprinting"></a> クライアント側印刷機能のトラブルシューティング  
 レポート ビューアーのツールバーで印刷ボタンが無効になっている場合は、次のことを確認します。  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]のレポート サーバーでクライアント側印刷機能が無効になっています。 このセクションの「  [クライアント側印刷機能を有効または無効にする](#bkmk_enable) 」セクションを参照してください。  
  
-   [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] の PDF 表示拡張機能が無効になっています。 `<Extension Name="PDF"` rsreportserver.config **ファイルの** セクションを確認してください。  
  
-   レポートを互換モードで表示しています。この場合、古い [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] HTML4 レンダリング エンジンが使用されます。 PDF の印刷には、HTML 5 レンダリング エンジンが必要です。  ツールバーの **[プレビューを試す]** ボタンをクリックしてください。  
  
     ![ssrs_html5_switch2html5](../../reporting-services/report-server/media/ssrs-html5-switch2html5.png "ssrs_html5_switch2html5")  
  
##  <a name="bkmk_enable"></a> クライアント側印刷機能を有効または無効にする  
 レポート サーバー管理者は、レポート サーバーのシステム プロパティ **EnableClientPrinting** を **false**に設定して、リモート印刷機能を無効にすることができます。 これにより、サーバーが管理しているすべてのレポートでクライアント側印刷機能が無効になります。 既定では、 **EnableClientPrinting** は **true**に設定されています。 クライアント側印刷機能は、次の方法で無効にすることができます。  
  
-   **ネイティブ モードのレポート サーバー**の場合:  
  
    1.  管理者特権を使用して [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を開始します。  
  
    2.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でレポート サーバー インスタンスに接続します。  
  
    3.  レポート サーバー ノードを右クリックして、 **[プロパティ]** をクリックします。 **[プロパティ]** オプションが無効になっている場合は、管理者特権を使用して [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を開始したことを確認してください。  
  
    4.  **[詳細設定]** をクリックします。  
  
    5.  **[EnableClientPrinting]** を選択します。  
  
    6.  True または False に設定して、 **[OK]** をクリックします。  
  
         ![ssrs_ssmsproperties_clientprinting](../../reporting-services/report-server/media/ssrs-ssmsproperties-clientprinting.png "ssrs_ssmsproperties_clientprinting")  
  
-   **SharePoint モードのレポート サーバー**の場合:  
  
    1.  SharePoint サーバーの全体管理で、 **[アプリケーション構成の管理]** をクリックします。  
  
    2.  **[サービス アプリケーションの管理]** をクリックします。  
  
    3.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの名前をクリックし、SharePoint リボンで **[管理]** をクリックします。  
  
    4.  **[システム設定]** をクリックします。  
  
    5.  **[クライアントの印刷を有効にする]** を選択します。 **[クライアントの印刷を有効にする]** オプションは、ページの下部付近にあります。  
  
    6.  **[OK]** をクリックします。  
  
-   レポート サーバー システム プロパティの **EnableClientPrinting** を **false.** に設定するスクリプトまたはコードを記述します。  
  
 次のサンプル スクリプトは、クライアント側印刷機能を無効にする方法の一例を示しています。 この [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] コードをコンパイルして実行すると、 **EnableClientPrinting** プロパティが **False**に設定されます。 コードの実行後、IIS を再起動してください。  
  
### <a name="sample-script"></a>サンプル スクリプト  
  
```  
Imports System  
Imports System.Web.Services.Protocols  
Class Sample  
   Public Shared Sub Main()  
Dim rs As New ReportingService()  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
        Dim props(0) As [Property]  
        Dim setProp As New [Property]  
        setProp.Name = "EnableClientPrinting"  
        setProp.Value = "False"   
        props(0) = setProp  
        Try  
            rs.SetSystemProperties(props)  
        Catch ex As System.Web.Services.Protocols.SoapException  
            Console.Write(ex.Detail.InnerXml)  
        Catch e as Exception  
            Console.Write(e.Message)  
        End Try  
    End Sub 'Main  
End Class 'Sample  
```

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
