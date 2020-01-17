---
title: 構成ファイル内の URL (SSRS 構成マネージャー)
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL configuration [Reporting Services]
ms.assetid: 4f5e7fe0-b5b1-4665-93d4-80dce12d6b14
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 75da68330bcce06a4ffdaf152bb19811cffe1f99
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593937"
---
# <a name="urls-in-configuration-files--ssrs-configuration-manager"></a>構成ファイル内の URL (SSRS 構成マネージャー)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、RSReportServer.config ファイルにアプリケーション設定を格納します。 このファイルには、URL と URL 予約の両方の構成設定が含まれています。 これらの構成設定は、変更の目的とルールが大きく異なります。 構成ファイルの変更による配置のチューニングに慣れている場合、各 URL 設定の使用方法の理解にこのトピックが役立ちます。  
  
## <a name="url-settings-in-rsreportserverconfig-file"></a>RSReportServer.config ファイルの URL 設定  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、アプリケーションやレポートにアクセスするための URL、および Web フロントエンド コンポーネントをバックエンド レポート サーバーに接続するための URL が格納されます。  
  
#### <a name="urls-for-application-access"></a>アプリケーションにアクセスするための URL  
 レポート サーバー Web サービスと [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]へのアクセスに URL が使用されます。 URL を構成するには、Reporting Services 構成ツールを使用する必要があります。 このツールでは、HTTP.SYS に各アプリケーションの URL 予約が作成され、RSReportServer.config の **URLReservations** セクションに URL のエントリが追加されます。  
  
-   **URLReservations** セクションの各要素の説明を表示するには、「[RsReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)」を参照してください。  
  
-   **UrlString** 要素の構文の詳細については、「[URL 予約の構文 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)」を参照してください。  
  
-   アプリケーションにアクセスするための URL の構成方法については、「 [URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)へのアクセスに URL が使用されます。  
  
#### <a name="urls-for-report-access"></a>レポートにアクセスするための URL  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、レポート リンクまたは添付ファイルの送信に使用できるレポート サーバーの電子メール配信拡張機能が用意されています。 レポート リンクは、レポートが配信されるときに構築されます。 レポート サーバーの電子メール配信拡張機能では、構成ファイルの **UrlRoot** 設定を使用してリンクが作成されます。 **UrlRoot** は、自動レポート処理によって生成される表示レポートでリンクを解決する場合にも使用されます。  
  
 **UrlRoot** は、アプリケーションにアクセスするための URL を構成するときに RSReportServer.config ファイルで自動的に指定されます。 構成ファイルでこの値を変更する場合は、配信するレポートが格納されているレポート サーバー データベースに接続しているレポート サーバー Web サービスの有効な URL アドレスを指定する必要があります。 **UrlRoot** は、各レポート サーバー インスタンスにつき 1 つしか指定できません。RSReportServer.config ファイルに存在できる **UrlRoot** エントリは、レポート サーバー インスタンスごとに 1 つだけです。 複数の URL をレポート サーバー Web サービス用に予約している場合は、 **UrlRoot**で使用可能な値のいずれかを選択する必要があります。  
  
 ほとんどの場合、 **UrlRoot**を変更する必要はありません。 ただし、完全修飾 URL を使用してレポート サーバーにアクセスする場合、ホスト ヘッダーを使用する URL を完全修飾サイト名に設定していないときは、RSReportServer.config を手動で編集して、 **UrlRoot** をレポートの表示に使用されるレポート サーバーの完全修飾 URL (たとえば https://www.adventure-works.com/mywebapp/reportserver) に設定する必要があります。  
  
#### <a name="urls-connecting-the-includessrswebportalincludesssrswebportalmd-and-web-parts-to-the-report-server-web-service"></a>[!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] および Web パーツをレポート サーバー Web サービスに接続するための URL  
 Reporting Services の [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] および SharePoint 2.0 Web パーツは、レポート サーバーに接続する Web フロントエンド コンポーネントです。 バックエンド レポート サーバーへの接続に使用される URL は次のとおりです。  
  
-   **ReportServerUrl** ( [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]で使用)  
  
-   **ReportServerExternalUrl** (Web パーツで使用)  
  
> [!NOTE]  
>  旧バージョンの Reporting Services には、 **ReportServerVirtualDirectory** 要素が含まれていました。 この値は [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンでは使用しません。 既存のインストールをアップグレードした場合にこの設定を含む構成ファイルを使用しても、レポート サーバーはこの値を読み取りません。  
  
 次の表は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ファイルで指定可能なすべての URL の概要を示しています。  
  
|設定|使用方法|[説明]|  
|-------------|-----------|-----------------|  
|**ReportServerUrl**|省略可。 この要素は、手動で追加しない限り RSReportServer.config ファイルには含まれません。<br /><br /> この要素は、次のいずれかのシナリオを構成する場合にのみ設定します。<br /><br /> 別のコンピューターまたは同じコンピューター上の別のインスタンスで実行されるレポート サーバー Web サービスへの Web フロントエンド アクセスを、 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] が提供する場合<br /><br /> [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] の URL が複数存在し、レポート マネージャーで特定の URL を使用する場合<br /><br /> [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] のすべての接続に特定のレポート サーバーの URL を使用する場合<br /><br /> たとえば、ネットワーク上のすべてのコンピューターに [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] へのアクセスを許可しても、ローカル接続を使用してレポート サーバーに接続するように [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] に求める場合があります。 この場合、**ReportServerUrl** を "`https://localhost/reportserver`" に設定します。|この値には、レポート サーバー Web サービスの URL を指定します。 この値は、起動時に [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] アプリケーションから読み取られます。 この値を設定すると、 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] は、URL で指定されたレポート サーバーに接続します。<br /><br /> 既定では、 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] は、 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]と同じレポート サーバー インスタンス内で実行されるレポート サーバー Web サービスへの Web フロントエンド アクセスを提供します。 ただし、別のインスタンスまたは別のコンピューター上のインスタンス内で実行されるレポート サーバー Web サービスで [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] を使用する場合は、外部のレポート サーバー Web サービスに接続するように [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] に指示するようにこの URL を設定することができます。<br /><br /> 接続先のレポート サーバーに SSL (Secure Sockets Layer) 証明書がインストールされている場合、 **ReportServerUrl** の値には、その証明書に登録されているサーバーの名前を指定する必要があります。 "基になる接続が閉じられました: SSL/TLS セキュリティ チャネルに対する信頼関係を確立できませんでした" というエラーが表示される場合は、 **ReportServerUrl** を、SSL 証明書が発行されたサーバーの完全修飾ドメイン名に設定してください。 たとえば、証明書が **https:\///adventure-works.com.onlinesales** に登録されている場合、レポート サーバー URL は **https:\///adventure-works.com.onlinesales/reportserver** になります。|  
|**ReportServerExternalUrl**|省略可。 この要素は、手動で追加しない限り RSReportServer.config ファイルには含まれません。<br /><br /> SharePoint 2.0 Web パーツを使用しており、ユーザーがレポートを取得して新しいブラウザー ウィンドウで開くことができるようにする場合にのみ、この要素を設定します。<br /><br /> \<**ReportServerUrl**> 要素の下に \<**ReportServerExternalUrl**> を追加し、別のブラウザー ウィンドウでアクセスされたときにレポート サーバー インスタンスに解決されるレポート サーバーの完全修飾名に設定します。 \<**ReportServerUrl**> は削除しないでください。<br /><br /> 構文例を次に示します。<br /><br /> `<ReportServerExternalUrl>https://myserver/reportserver</ReportServerExternalUrl>`|この値は SharePoint 2.0 Web パーツで使用されます。<br /><br /> 以前のリリースでは、この値を設定してインターネットに接続されたレポート サーバーにレポート ビルダーを配置することが推奨されていました。 この配置シナリオはテストされていません。 以前に、レポート ビルダーへのインターネット アクセスをサポートするためにこの設定を使用していた場合は、他の方法を検討してください。|  
  
## <a name="see-also"></a>参照  
 [レポート サーバー URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)
