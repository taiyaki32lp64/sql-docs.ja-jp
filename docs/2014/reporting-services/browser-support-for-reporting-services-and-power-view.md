---
title: Reporting Services と Power View ブラウザー サポートの計画 (Reporting Services 2014)
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: cd3a3e268e09e882b4e38eee6a620843fcc21a23
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241199"
---
# <a name="planning-for-reporting-services-and-power-view-browser-support-reporting-services-2014"></a>Reporting Services と Power View ブラウザー サポートの計画 (Reporting Services 2014)
  
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] では、Web ブラウザーを使用して、レポートを表示したりレポート マネージャーを実行したりします。 すべてのブラウザーですべてのレポート機能がサポートされているわけではありません。 このトピックでは、レポート マネージャーの管理機能、レポートの表示、Visual Studio のレポート ビューアー コントロールのサポートと要件について説明します。 また、サポートされるブラウザーで使用できる機能、認証要件、およびスクリプトの要件の概要も示します。  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]SharePoint モード |[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]ネイティブモード  
  
 **このトピックの内容:**  
  
- [Power View のブラウザーのシナリオ](#bkmk_powerview)  
  
- [レポート マネージャーのブラウザーの要件 (ネイティブ モード)](#bkmk_reportmanager)  
  
- [レポートを表示するためのブラウザーの要件](#bkmk_reportviewer)  
  
- [認証の要件](#bkmk_authentication)  
  
- [Visual Studio での ReportViewer Web サーバーコントロールのブラウザーサポート](#bkmk_controls)  
  
##  <a name="bkmk_powerview"></a>Power View ブラウザーのシナリオ

 
  [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] でサポートされているブラウザーとそのバージョンの一覧は、開くドキュメントの種類によって異なります。 Excel 2013 ブックと "**rdlx**" ファイルでは、さまざまなコンポーネントが使用されます。  
  
|ドキュメントの種類|環境|ブラウザーのサポート|  
|-------------------|-----------------|---------------------|  
|Power View レポート (.RDLX)|Sharepoint **Server:** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] sharepoint [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]統合モードの場合は、Power View web アプリケーションの場合は。|「 [Sharepoint Server の Power View」および「Sharepoint 統合モードの Reporting Services](#bkmk_powerview_on_SSRS)」を参照してください。|  
|Power View シートが含まれた Excel 2013 ブック|**SharePoint サーバー:** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] Excel Services で。<br /><br /> **SharePoint Online (Office 365):** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] Excel Web アプリの場合。|「 [Excel Services または SharePoint Online の Excel Web アプリでの Power View」を](#bkmk_powerview_on_ExcelServices)参照してください。|  
  
###  <a name="bkmk_powerview_on_SSRS"></a>SharePoint Server および Reporting Services SharePoint 統合モードでの Power View  
 次の表は、[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] サービス アプリケーションと SharePoint の [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] アドインがインストールされ、構成されている SharePoint ファームでユーザーが Power View レポート (.RDLX) を開く場合に、[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] でサポートされるブラウザーをまとめたものです。  
  
- この表は、SharePoint 2010 と SharePoint 2013 に適用されます。  
  
- SharePoint 2013 ブラウザーサポートの詳細については、「 [sharepoint 2013 でブラウザーサポート](https://technet.microsoft.com//library/cc263526\(office.15\).aspx)をhttps://technet.microsoft.com/library/cc263526(office.15).aspx)計画する」 (を参照してください。  
  
- SharePoint 2010 のブラウザーサポートの詳細については、「[ブラウザーサポートを計画する (Sharepoint Server 2010)](https://technet.microsoft.com/library/cc263526\(office.14\).aspx) 」 (https://technet.microsoft.com/library/cc263526(office.14).aspx)を参照してください。  
  
|**Browser**|**Windows 8 および8.1**|**Windows 7**|**Windows Server 2012 および 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10.6-10.9**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|  
|**Internet Explorer 11 (デスクトップ用)**|32 ビット、64 ビット|32 ビット、64 ビット|32 ビット、64 ビット|32 ビット、64 ビット|サポートされていません|サポートされていません|  
|**Internet Explorer 10 (デスクトップ用)**|32 ビット、64 ビット|32 ビット、64 ビット|32 ビット、64 ビット|32 ビット、64 ビット|サポートされていません|サポートされていません|  
|**Internet Explorer 9**|サポートされていません|32 ビット、64 ビット|サポートされていません|32 ビット、64 ビット|32 ビット、64 ビット|サポートされていません|  
|**Internet Explorer 8**|サポートされていません|32 ビット、64 ビット|サポートされていません|32 ビット、64 ビット|32 ビット、64 ビット|サポートされていません|  
|**Mozilla Firefox (一般公開されている最新バージョン)**|32 ビット|32 ビット|32 ビット|32 ビット|32 ビット|サポートされていません|  
|**Apple Safari (一般公開されている最新バージョン)**|サポートされていません|サポートされていません|サポートされていません|サポートされていません|サポートされていません|32 ビット、64 ビット|  
  
> [!NOTE]  
> "32 ビット" はブラウザーのことであり、オペレーティング システムではありません。 たとえば、32 ビット版の Internet Explorer 9 を 64 ビット版の Windows 7 で使用できます。  
  
#### <a name="inprivate-browsing-feature-in-internet-explorer"></a>Internet Explorer での InPrivate ブラウズ機能

 
  [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] では、[!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 8 および Internet Explorer 9 の InPrivate ブラウズ機能はサポートされていません。 InPrivate ブラウズの詳細については、「 [Inprivate ブラウズとは](https://windows.microsoft.com/Windows7/What-is-InPrivate-Browsing)」を参照してください。 (https://windows.microsoft.com/Windows7/What-is-InPrivate-Browsing).  
  
###  <a name="bkmk_powerview_on_ExcelServices"></a>Excel Services または SharePoint Online の Excel Web アプリでの Power View

 次の表は、Excel Services を実行している SharePoint Server で、Power View シートが含まれた Excel 2013 ブックをユーザーが開く場合に、 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] でサポートされるブラウザーのバージョンをまとめたものです。  
  
-   SharePoint 2013 ブラウザーサポートの詳細については、「 [sharepoint 2013 でブラウザーサポート](https://technet.microsoft.com/library/cc263526\(office.15\).aspx)をhttps://technet.microsoft.com/library/cc263526(office.15).aspx)計画する」 (を参照してください。  
  
|**Browser**|**Windows 8 および8.1**|**Windows 7**|**Windows Server 2012 および 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10.6-10.9**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|  
|**Internet Explorer 11 (デスクトップ用)**|32 ビット、64 ビット|32 ビット、64 ビット|32 ビット、64 ビット|32 ビット、64 ビット|サポートされていません|サポートされていません|  
|**Internet Explorer 10 (デスクトップ用)**|32 ビット、64 ビット|32 ビット、64 ビット|32 ビット、64 ビット|32 ビット、64 ビット|サポートされていません|サポートされていません|  
|**Internet Explorer 9**|サポートされていません|32 ビット、64 ビット|サポートされていません|32 ビット、64 ビット|32 ビット、64 ビット|サポートされていません|  
|**Internet Explorer 8**|サポートされていません|32 ビット、64 ビット|サポートされていません|32 ビット、64 ビット|32 ビット、64 ビット|サポートされていません|  
|**Mozilla Firefox (一般公開されている最新バージョン)**|32 ビット|32 ビット|32 ビット|32 ビット|32 ビット|32 ビット、64 ビット|  
|**Apple Safari (一般公開されている最新バージョン)**|サポートされていません|サポートされていません|サポートされていません|サポートされていません|サポートされていません|32 ビット、64 ビット|  
|**Google Chrome (一般公開されている最新バージョン)**|32-bit **(\*)** を期間限定|32-bit **(\*)** を期間限定|32-bit **(\*)** を期間限定|32-bit **(\*)** を期間限定|32-bit **(\*)** を期間限定|サポートされていません|  
  
 **(\*)** Chrome は、Silverlight によって使用される Netscape プラグイン API (npapi) のサポートを停止します。 Power View は、Silverlight に依存します。  詳細については、 [NPAPI の最終的なカウント ダウンに関するページ](http://blog.chromium.org/2014/11/the-final-countdown-for-npapi.html)を参照してください。  
  
##  <a name="bkmk_reportmanager"></a>レポートマネージャーブラウザーの要件 (ネイティブモード)

 次に示しているのは、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ネイティブ モードのレポート マネージャーを実行してレポートとレポート サーバーを管理するために使用できるブラウザーの最新の一覧です。  
  
|Browser|  
|-------------|  
|Internet Explorer 7 以降 (スクリプト機能オン)|  
|Mozilla FireFox (一般公開されている最新バージョン)|  
|Apple Safari (一般公開されている最新バージョン)|  
|Google Chrome (一般公開されている最新バージョン)|  
  
##  <a name="bkmk_reportviewer"></a>レポートを表示するためのブラウザーの要件

 レポート ビューアーでサポートされているブラウザーと機能の最新の一覧を次に示します。 レポート ビューアーでは、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート マネージャーおよび SharePoint ライブラリからのレポートの表示がサポートされています。  
  
|**Browser**|**Windows 8 および8.1**|**Windows 7**|**Windows Server 2012 および 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10.6-10.9**|**iPad の iOS 6 ～ 7**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|----------------------------|  
|**Internet Explorer 11 (デスクトップ用)**|32 ビット、64 ビット|32 ビット、64 ビット|32 ビット、64 ビット|サポートされていません|サポートされていません|サポートされていません|サポートされていません|  
|**Internet Explorer 10 (デスクトップ用)**|32 ビット、64 ビット|32 ビット、64 ビット|32 ビット、64 ビット|サポートされていません|サポートされていません|サポートされていません|サポートされていません|  
|**Internet Explorer 9**|サポートされていません|32 ビット、64 ビット|サポートされていません|32 ビット、64 ビット|32 ビット、64 ビット|サポートされていません|サポートされていません|  
|**Internet Explorer 8**|サポートされていません|32 ビット、64 ビット|サポートされていません|32 ビット、64 ビット|32 ビット、64 ビット|サポートされていません|サポートされていません|  
|**Internet Explorer 7**|サポートされていません|サポートされていません|サポートされていません|サポートされていません|32 ビット、64 ビット|サポートされていません|サポートされていません|  
|**Mozilla Firefox (一般公開されている最新バージョン)**|32 ビット|32 ビット|32 ビット|32 ビット|32 ビット|サポートされていません|サポートされていません|  
|**Apple Safari (一般公開されている最新バージョン)**|サポートされていません|サポートされていません|サポートされていません|サポートされていません|サポートされていません|32 ビット、64 ビット|機能制限付きでサポート<sup>(1)</sup>|  
|**Google Chrome (一般公開されている最新バージョン)**|32 ビット|32 ビット|32 ビット|32 ビット|32 ビット|サポートされていません|サポートされていません|  
  
 **<sup>(1)</sup>** 次の機能がサポートされています。  
  
- PDF 形式および TIFF 形式へのエクスポート  
  
- iOS デバイスの Apple Safari で対話的にレポートを表示します。 サポートされる機能には、展開/折りたたみ、パラメーター ペイン、対話的な並べ替えなどがあります。  
  
- 詳細については、「 [Microsoft Surface デバイスと Apple IOS デバイスで Reporting Services レポートを表示](../../2014/reporting-services/view-reporting-services-reports-surface-ios-devices.md)する」を参照してください。  
  
 **メモ**Macintosh コンピューターからレポートサーバーにアクセスする場合は、Safari を使用することをお勧めします。 と[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]統合された SharePoint 製品を使用している場合は、「[ブラウザーサポートを計画する (Windows SharePoint Services)](https://go.microsoft.com/fwlink/?LinkId=183583)」を参照してください。  
  
### <a name="url-access-for-viewing-reports"></a>URL アクセスを使用したレポートの表示

 レポート マネージャーを使用せずに直接レポートを表示するには、レポートおよびレポート ビューアーにリンクする URL アクセスを使用します。 URL アクセスでは、さまざまなブラウザーがサポートされます。  
  
 URL アクセスの詳細については、次のトピックを参照してください。  
  
- [URL アクセスパラメーターのリファレンス](url-access-parameter-reference.md)  
  
###  <a name="bkmk_authentication"></a>認証の要件

 クライアント要求が正常に終了するように、ブラウザーでは、レポート サーバーで処理する必要がある特定の認証方法をサポートしています。 次の表は、Windows オペレーティング システムで実行中の各ブラウザーでサポートされる既定の認証の種類を示しています。  
  
|**ブラウザーの種類**|**対応**|**ブラウザーの既定値**|**サーバーの既定値**|  
|----------------------|------------------|-------------------------|------------------------|  
|**Internet Explorer**|ネゴシエート、Kerberos、NTLM、基本|ネゴシエート|対応 Internet Explorer の既定の認証設定を使用します。|  
|**Browser**|NTLM、基本|NTLM|対応 Firefox の既定の認証設定を使用します。|  
|**Safari**|基本|基本|対応 Safari の既定の認証設定を使用します。|  
|**クロム**|ネゴシエート、NTLM、基本|ネゴシエート|対応 Chrome の既定の認証設定を使用します。|  
  
### <a name="script-requirements"></a>スクリプトの必要条件

 レポート ビューアーを使用するには、スクリプトを実行するようにブラウザーを構成する必要があります。  
  
 スクリプトが有効になっていない場合は、レポートを開くときに次のようなエラー メッセージが表示されます。  
  
- **ブラウザーでスクリプトがサポートされていないか、スクリプトを実行できないように構成されています。スクリプトを使用せずにこのレポートを表示するには、ここをクリックし**ます。  
  
 スクリプトを使用せずにレポートを表示することを選択した場合、レポート ツール バーやドキュメント マップなどのレポート ビューアー機能を使用しない HTML でレポートが表示されます。  
  
> [!NOTE]  
> レポート ツール バーは HTML ビューアー コンポーネントの一部です。 既定では、ツール バーはブラウザー ウィンドウに表示されるすべてのレポートの上部に表示されます。 レポート ビューアーには、レポート内の情報検索、特定のページへのスクロール、および表示目的でのページ サイズの調整機能があります。 レポート ツール バーまたは HTML ビューアーの詳細については、「 [HTML Viewer and the Report Toolbar](html-viewer-and-the-report-toolbar.md)」を参照してください。  
  
##  <a name="bkmk_controls"></a>Visual Studio での ReportViewer Web サーバーコントロールのブラウザーサポート

 ReportViewer Web サーバー コントロールは、ASP.NET Web アプリケーションにレポート機能を埋め込むために使用されます。 このコントロールは Visual Studio に含まれており、このトピックで説明している他のコンポーネントとはサポートしているブラウザーおよびブラウザー バージョンが異なります。 アプリケーションの表示に使用するブラウザーの種類によって、アプリケーションに埋め込むことができる ReportViewer の機能が決まります。 レポート機能が制限されるサポート対象のブラウザーとサポートされているプラットフォームについては、このトピックの表を参照してください。  
  
 サポートされているブラウザーの描画エンジンの違いにより、一部のレポートの拡張機能の表示がブラウザー間で異なる場合があります。  たとえば、文字の回転が異なります。  
  
### <a name="scripting-requirements"></a>スクリプトの必要条件

 スクリプトのサポートが有効になっているブラウザーを使用します。 ブラウザーがスクリプトを実行できない場合、レポートを表示することができません。  
  
### <a name="browser-requirements-for-viewing-reports-with-the-reportviewer-web-server-controls"></a>ReportViewer Web サーバー コントロールを使用してレポートを表示するためのブラウザーの要件

 対話型レポート機能のサポートは、ブラウザーの種類によって異なります。 次のサポート表には、各プラットフォームでサポートされているブラウザーの種類を示しています。備考欄には、適用される制限が記載されています。  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
|**Browser**|**Windows 8**および**Windows 8.1**|**Windows 7**|**Windows Server 2012**および**2012 R2**|**Windows Server 2008**および**2008 R2**|**Windows Server 2003**|**Mac OS X 10.6-10.9**|**注記**|  
|**Internet Explorer 11 (デスクトップ用**|はい|はい|はい|サポートされていません|サポートされていません|サポートされていません|Internet Explorer では、ReportViewer のすべての機能をサポートしています。|  
|**Internet Explorer 10 (デスクトップ用)**|はい|はい|はい|サポートされていません|サポートされていません|サポートされていません|Internet Explorer では、ReportViewer のすべての機能をサポートしています。|  
|**Internet Explorer 9**|サポートされていません|はい|サポートされていません|はい|はい|はい|Internet Explorer では、ReportViewer のすべての機能をサポートしています。|  
|**Internet Explorer 8.0**|サポートされていません|はい|サポートされていません|はい|はい <sup>1</sup>|サポートされていません|Internet Explorer では、ReportViewer のすべての機能をサポートしています。 <sup>1 で保護されたプロセスとして起動されました</sup>|  
|**Internet Explorer 7.0**|サポートされていません|はい|サポートされていません|はい|はい <sup>1</sup>|サポートされていません|Internet Explorer では、ReportViewer のすべての機能をサポートしています。 <sup>1 で保護されたプロセスとして起動されました</sup>|  
|**Firefox (一般公開されている最新バージョン)**|はい|はい|はい|はい|はい|サポートされていません|印刷とズームはサポートされていません。|  
|**Safari (一般公開されている最新バージョン)**|サポートされていません|サポートされていません|サポートされていません|サポートされていません|サポートされていません|はい|印刷とズームはサポートされていません。<br /><br /> パラメーター化されたレポートで日付を選択するために使用するカレンダー コントロールは、このブラウザーでは無効になっています。 ユーザーは、使用する日付をパラメーター プロンプト領域に手動で入力する必要があります。|  
|**Chrome (一般公開されている最新バージョン)**|はい|はい|はい|はい|はい|サポートされていません|印刷とズームはサポートされていません。|  
  
 <sup>1</sup>標準モードでは、Internet Explorer 7.0 および8.0 ではレポートに斜線が表示されません。 レポートで斜線を使用している場合は、ASP.NET ページを Internet Explorer の Quirks モードで実行するように設定します。 これを行うには、 \<を見つけます。ASP.NET ページの DOCTYPE> タグ。 また、マスター ページを使用している場合は、.master ファイルでこのタグを探します。 このタグは次のようになっています。  
  
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">  
```
  
 を\<置き換えます。次のタグを持つ DOCTYPE> タグ:  
  
```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">  
```
  
 Internet Explorer の互換モードの詳細については、「ドキュメントのhttps://go.microsoft.com/fwlink/?LinkId=180380)互換性の[定義](https://go.microsoft.com/fwlink/?LinkId=180380)」 (「」を参照してください。  
  
 ReportViewer コントロールの使用方法の詳細については、「[レポートと Reportviewer コントロールの配置](https://msdn.microsoft.com/library/ms251723.aspx)」 (https://msdn.microsoft.com/library/ms251723.aspx)を参照してください。  
  
## <a name="next-steps"></a>次の手順

 [Reporting Services ツール](tools/reporting-services-tools.md)[レポートマネージャー &#40;SSRS ネイティブモード&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md) [HTML ビューアーとレポートツールバー](html-viewer-and-the-report-toolbar.md)
