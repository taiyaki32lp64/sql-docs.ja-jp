---
title: Reporting Services と Power View のブラウザー サポート | Microsoft Docs
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- displaying reports
- scripts [Reporting Services], requirements
- viewing reports
- browsers [Reporting Services]
- Web browsers [Reporting Services], about browser support
- browsing reports [Reporting Services]
- components [Reporting Services], browsers
- Web browsers [Reporting Services]
ms.assetid: 48a75bbb-0029-4c43-891d-dc8f4fc0ebe1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 46176d786314284f4056b58ba351dacee37a06e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65574816"
---
# <a name="browser-support-for-reporting-services-and-power-view"></a>Reporting Services と Power View のブラウザー サポート

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

SQL Server Reporting Services、ReportViewer コントロール、Power View. の管理と表示にサポートされているブラウザーのバージョンについて説明します。

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。

## <a name="browser-requirements-for-the-web-portal"></a>Web ポータルのブラウザーの要件

次は、Web ポータルでサポートされているブラウザーの現行リストです。

**Microsoft Windows**  
*Windows 7、8.1、10、Windows Server 2008 R2、2012、2012 R2*
- Microsoft Edge (+)
- Microsoft Internet Explorer 10 または 11
- Google Chrome (+)
- Mozilla Firefox (+)

**Apple OS X**  
*OS X 10.9-10.11*

- Apple Safari (+)
- Google Chrome (+)
- Mozilla Firefox (+)

**Apple iOS**  
*iOS 9 を内蔵した iPhone または iPad*

- Apple Safari (+)

**Google Android**  
*Android 4.4 (KitKat) 以降を内蔵したスマートフォンまたはタブレット*

- Google Chrome (+)

 **(+)** 最新公開リリース バージョン

## <a name="browser-requirements-for-the-reportviewer-web-control-2015"></a>ブラウザー要件: ReportViewer Web コントロール (2015)

 次は、ReportViewer Web コントロール (2015) でサポートされているブラウザーの現行リストです。 レポート ビューアーでは、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Web ポータルや SharePoint ライブラリのレポートを表示できます。  

**Microsoft Windows**  
*Windows 7、8.1、10、Windows Server 2008 R2、2012、2012 R2*

- Microsoft Edge (+)
- Microsoft Internet Explorer 10 または 11
- Google Chrome (+)
- Mozilla Firefox (+)

**Apple OS X**  
*OS X 10.9-10.11*

- Apple Safari (+)

 **(+)** 最新公開リリース バージョン

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]に統合されている SharePoint 製品を使用している場合は、「  [SharePoint 2016 でブラウザー サポートを計画する](https://technet.microsoft.com//library/cc263526\(v=office.16\).aspx)」を参照してください。

::: moniker-end

### <a name="authentication-requirements"></a>認証の要件

 クライアント要求が正常に終了するように、ブラウザーでは、レポート サーバーで処理する必要がある特定の認証方法をサポートしています。 次の表は、Windows オペレーティング システムで実行中の各ブラウザーでサポートされる既定の認証の種類を示しています。

|**ブラウザーの種類**|**サポート**|**ブラウザーの既定値**|**サーバーの既定値**|
|----------------------|------------------|-------------------------|------------------------|
|**Microsoft Edge** (+)|ネゴシエート、Kerberos、NTLM、基本|ネゴシエート|可能。 Edge の既定の認証設定を使用します。|
|**[Microsoft Internet Explorer]**|ネゴシエート、Kerberos、NTLM、基本|ネゴシエート|可能。 Internet Explorer の既定の認証設定を使用します。|
|**Google Chrome**(+)|ネゴシエート、NTLM、基本|ネゴシエート|可能。 Chrome の既定の認証設定を使用します。|
|**Mozilla Firefox**(+)|NTLM、基本|NTLM|可能。 Firefox の既定の認証設定を使用します。|
|**Apple Safari**(+)|NTLM、基本|Basic|可能。 Safari の既定の認証設定を使用します。|

 **(+)** 最新公開リリース バージョン

### <a name="script-requirements-for-viewing-reports"></a>レポートを表示するためのスクリプトの要件

 レポート ビューアーを使用するには、スクリプトを実行するようにブラウザーを構成する必要があります。

 スクリプトが有効になっていない場合は、レポートを開くときに次のようなエラー メッセージが表示されます。

- **ブラウザーでスクリプトがサポートされていないか、スクリプトの実行を許可するように構成されていません。ここをクリックして、スクリプトを使用せずにこのレポートを表示します**。

 スクリプトを使用せずにレポートを表示することを選択した場合、レポート ツール バーやドキュメント マップなどのレポート ビューアー機能を使用しない HTML でレポートが表示されます。

> [!NOTE]
> レポート ツール バーは HTML ビューアー コンポーネントの一部です。 既定では、ツール バーはブラウザー ウィンドウに表示されるすべてのレポートの上部に表示されます。 レポート ビューアーには、レポート内の情報検索、特定のページへのスクロール、および表示目的でのページ サイズの調整機能があります。 レポート ツール バーまたは HTML ビューアーの詳細については、「 [HTML Viewer and the Report Toolbar](../reporting-services/html-viewer-and-the-report-toolbar.md)」を参照してください。

## <a name="browser-support-for-reportviewer-web-server-controls-in-visual-studio"></a>Visual Studio での ReportViewer Web サーバー コントロールのブラウザー サポート

 ReportViewer Web サーバー コントロールは、ASP.NET Web アプリケーションにレポート機能を埋め込むために使用されます。 このコントロールは Visual Studio に含まれており、このトピックで説明している他のコンポーネントとはサポートしているブラウザーおよびブラウザー バージョンが異なります。 アプリケーションの表示に使用するブラウザーの種類によって、アプリケーションに埋め込むことができる ReportViewer の機能が決まります。 レポート機能が制限されるサポート対象のブラウザーとサポートされているプラットフォームについては、このトピックの表を参照してください。  

 スクリプトのサポートが有効になっているブラウザーを使用します。 ブラウザーがスクリプトを実行できない場合、レポートを表示することができません。

**Microsoft Windows**  
*Windows 7、8.1、10、Windows Server 2008 R2、2012、2012 R2*

- Microsoft Edge (+)
- Microsoft Internet Explorer 10 または 11
- Google Chrome (+)
- Mozilla Firefox (+)

 **(+)** 最新公開リリース バージョン

## <a name="power-view-browser-support"></a>Power View のブラウザー サポート

**Microsoft Windows**  
*Windows 7、8.1、10、Windows Server 2008 R2、2012、2012 R2*

- Microsoft Internet Explorer 10 または 11
- Mozilla Firefox (+)

**Apple OS X**  
*OS X 10.9-10.11*

- Apple Safari (+)

 **(+)** 最新公開リリース バージョン

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

 SharePoint 2016 のブラウザー サポートの詳細については、「 [SharePoint 2013 でブラウザー サポートを計画する](https://technet.microsoft.com//library/cc263526\(v=office.16\).aspx)」を参照してください。

::: moniker-end

## <a name="next-steps"></a>次の手順

[Web ポータルを使用したレポートの検索と表示](report-builder/finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md)  
[Reporting Services ツール](../reporting-services/tools/reporting-services-tools.md)  
[Web ポータル (SSRS ネイティブ モード)](https://msdn.microsoft.com/7349e626-6ed5-4d21-b05f-cf042ad9ad70)  
[HTML Viewer and the Report Toolbar](../reporting-services/html-viewer-and-the-report-toolbar.md)  
[URL アクセス パラメーター リファレンス](../reporting-services/url-access-parameter-reference.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)

