---
title: Reporting Services のクライアント側印刷機能の有効化と無効化 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 0e709c96-7517-4547-8ef6-5632f8118524
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ea5016aa51a25bd296d2e77516b30b84a7a28cec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103928"
---
# <a name="enable-and-disable-client-side-printing-for-reporting-services"></a>Reporting Services のクライアント側印刷機能の有効化と無効化
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX コントロール、 **RSClientPrint**レポートのクライアント側印刷機能は、ブラウザーで表示を提供します。 このコントロールによって表示されるカスタム印刷ダイアログ ボックスでは、一般的な印刷ダイアログ ボックスの機能がサポートされています。 この機能には、印刷プレビュー、特定のページや範囲を指定するためのページ選択、ページ余白、ページの向きなどが含まれます。 クライアント側印刷機能は既定で有効になっていますが、無効にして使用できないようにすることもできます。  
  
> [!NOTE]  
>  ActiveX コントロールをダウンロードするには、管理者権限が必要です。  
  
## <a name="downloading-the-activex-control"></a>ActiveX コントロールのダウンロード  
 印刷機能を使用する各ユーザーは、クライアント側印刷機能を提供する ActiveX コントロールをダウンロードしてインストールする必要があります。 初めてクリックすると、ユーザー、**プリンター**アイコン レポート ツールバーで、Microsoft ActiveX コントロールは、コンピューターにダウンロードされます。 コントロールのダウンロード後、**印刷**ユーザーがクリックされるたびに、ダイアログ ボックスが表示されます、**プリンター**アイコン。  
  
 ブラウザーの設定によって、コントロールをインストールするかどうかを確認するメッセージが表示される場合と、コントロールをインストールできない場合と、ユーザーへの通知を行わずにコントロールがバックグラウンドでインストールされる場合があります。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX コントロールのダウンロードとインストールに影響する設定は、Internet Explorer を介して指定、 **ActiveX コントロールとプラグイン**内のノード、**セキュリティ設定**のページWeb コンテンツ ゾーン。 印刷コントロールをダウンロードして実行できるかどうかは、Web ゾーンの以下のセキュリティ設定によって決まります。  
  
-   署名済み ActiveX コントロールのダウンロード。  
  
-   スクリプトを実行しても安全とマークされている ActiveX コントロールのスクリプトの実行。  
  
-   ActiveX コントロールとプラグインの実行。  
  
 使用する必要のあるユーザー **RSClientPrint**クライアント側印刷機能を実行して以下を実現する必要があります。  
  
-   **署名済み ActiveX コントロールのダウンロード**と**ActiveX コントロールがスクリプトを実行しても安全とマーク**のインストールに必要です。  
  
-   **ActiveX コントロールとプラグイン**の継続的な印刷操作。  
  
 **RSClientPrint** ActiveX コントロールは署名済み、つまりから有効なデジタル証明書が含まれている[!INCLUDE[msCoName](../../includes/msconame-md.md)]します。  
  
## <a name="enabling-and-disabling-client-side-printing"></a>クライアント側印刷機能の有効化と無効化  
 レポート サーバーのシステム プロパティを設定して、印刷機能を無効にすることがレポート サーバー管理者**EnableClientPrinting**に`false`します。 これにより、サーバーが管理しているすべてのレポートでクライアント側印刷機能が無効になります。 既定では、 **EnableClientPrinting**に設定されている`true`します。 クライアント側印刷機能は、次の方法で無効にすることができます。  
  
-   **ネイティブ モードのレポート サーバー**の場合:  
  
    1.  管理者特権を使用して [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を開始します。  
  
    2.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でレポート サーバー インスタンスに接続します。  
  
    3.  レポート サーバー ノードを右クリックして、 **[プロパティ]** をクリックします。 **[プロパティ]** オプションが無効になっている場合は、管理者特権を使用して [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を開始したことを確認してください。  
  
    4.  選択**ActiveX クライアントの印刷コントロールのダウンロードを有効にする**します。  
  
    5.  [**OK**] をクリックします。  
  
-   **SharePoint モードのレポート サーバー**の場合:  
  
    1.  SharePoint サーバーの全体管理で、 **[アプリケーション構成の管理]** をクリックします。  
  
    2.  **[サービス アプリケーションの管理]** をクリックします。  
  
    3.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの名前をクリックし、SharePoint リボンで **[管理]** をクリックします。  
  
    4.  **[システム設定]** をクリックします。  
  
    5.  **[クライアントの印刷を有効にする]** を選択します。 **[クライアントの印刷を有効にする]** オプションは、ページの下部付近にあります。  
  
    6.  [**OK**] をクリックします。  
  
-   レポート サーバーのシステム プロパティを設定するスクリプトまたはコードを記述**EnableClientPrinting**に `false.`  
  
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
  
  
