---
title: Web ポータルの構成 | Microsoft Docs
ms.date: 05/10/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- the web portal [Reporting Services], configuring
ms.assetid: e918986c-af15-48f6-8178-256aed829c6a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 962ab17170c69b6225f852f0b625a6cd50fa20d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63308398"
---
# <a name="configure-the-web-portal"></a>Web ポータルの構成

Web ポータルは、Web フロント エンド アプリケーションであり、レポートの表示、レポート サーバー コンテンツの管理、およびネイティブ モードのレポート サーバーへのアクセス権の付与に使用されます。 Web ポータルは、レポート サーバー Web サービスと共に、同じレポート サーバー インスタンス内にインストールされます。また、セットアップ時に **[ネイティブ モードの既存の構成をインストールする]** を選択した場合は、必要に応じて構成できます。 Web ポータルはインストール後のタスクとしても構成できます。 このトピックでは、次の Web ポータルの構成シナリオについて説明します。

## <a name="prerequisites"></a>Prerequisites

Web ポータルを使用するには、次の条件を満たす必要があります。

- 最小限の構成が行われているレポート サーバーが必要です。 レポート サーバーの最小限の構成の詳細については、「[レポート サーバーの構成](../../reporting-services/report-server/configure-a-report-server-reporting-services-native-mode.md)」を参照してください。

- レポート サーバーはネイティブ モードで動作する必要があります。 Web ポータルは、SharePoint 統合モード用に構成されているレポート サーバーと併用できません。 SQL Server 2012 では、レポート サーバーを別のモードに切り替えることはできません。 環境で使用しているレポート サーバーの種類を変更するには、目的のモードのレポート サーバーをインストールした後、新しいレポート サーバーにレポート アイテムをコピーまたは移動する必要があります。 このプロセスは、一般的には "移行" と呼ばれます。 移行に必要な手順は、移行先のモードと移行元のバージョンによって異なります。 詳細については、「 [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)」を参照してください。

- また、Internet Explorer 11 以降 (スクリプト機能オン) も必要です。 詳細については、「 [Reporting Services と Power View のブラウザー サポート](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)」を参照してください。

## <a name="configure-the-web-portal-to-use-the-default-url"></a>既定の URL を使用する Web ポータルの構成

Web ポータルは、ユーザーが Web ブラウザーでアクセスする Web アプリケーションです。 少なくとも、ブラウザー ウィンドウでアプリケーションを開く際に使用する URL を定義する必要があります。 URL はホスト名、ポート、および仮想ディレクトリで構成されます。 この URL の既定値には、レポート サーバー Web サービスの URL 用に定義したホスト名とポートの値に加えて、 **レポート** の仮想ディレクトリ名が含まれます。 名前付きインスタンスを使用している場合、仮想ディレクトリは **reports_instance**になります ( **instance** の箇所には、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インスタンスの名前が入ります)。

既定では、Web ポータルの URL は一意の仮想ディレクトリ名に加えて、同じインスタンスで実行されているレポート サーバー Web サービス用に定義されているポートとホスト名で構成されます。 ほとんどの場合、ホスト名はレポート サーバー コンピューターのネットワーク名ですが、そのコンピューターを解決する IP アドレスまたはホスト ヘッダーである場合もあります。 既定の URL を使用するように Web ポータルを構成するには、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールの **[Web ポータル URL]** ページを使用します。

> [!TIP]
> リモート コンピューター上の Web ポータルにアクセスしようとして、ブラウザーに接続エラー メッセージが返される場合、一般的な原因はファイアウォールの設定です。 詳細については、「 [レポート サーバー アクセスに対するファイアウォールの構成](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)」をご覧ください。

#### <a name="to-configure-the-default-the-web-portal-url-and-virtual-directory"></a>既定の Web ポータル URL と仮想ディレクトリを構成するには

1. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを起動して、レポート サーバー インスタンスに接続します。

2. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールで、 **[Web ポータル URL]** を選択して、URL を構成するページを開きます。

3. Web ポータルの一意の仮想ディレクトリ名を入力します。

4. **[適用]** をクリックします。

5. [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] または Windows Server 2008 を使用している場合は、Web ポータルを使用する前に追加の手順が必要になることがあります。 詳細については、「 [ローカル管理用のネイティブ モードのレポート サーバー &#40;SSRS&#41; の構成](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)」を参照してください。

## <a name="configure-the-web-portal-to-use-a-specific-report-server-url"></a>特定の Web ポータルの URL を使用するレポート マネージャーの構成

既定では、Web ポータルは、同じレポート サーバー サービスで実行されているレポート サーバー Web サービスに接続します。 Web ポータルは、レポート サーバー Web サービスの URL を使用して接続を確立します。 レポート サーバー Web サービス用に複数の URL を定義している場合、Web ポータルは最後に定義した URL を使用します。 ただし、配置によっては、Web ポータルが Web サービスに接続する際に、常に静的 URL を使用しなければならない場合があります。 このような接続が必要になる状況として、特定のポートや IP アドレスに対してパケット フィルターを構成しており、レポート サーバーへ接続するときは必ず定義したフィルター ルールを適用する場合などが例として挙げられます。

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールで URL を構成すると、Web ポータルは、同じサーバー インスタンス内で実行されるレポート サーバー用の新しい URL や更新された URL を自動的に検出し、これを使用します。 すべてのレポート サーバー要求に 1 つの静的 URL を使用することが必要な配置では、RSReportServer.config ファイルでその URL を指定できます。

#### <a name="to-configure-a-static-report-server-url"></a>レポート サーバーの静的 URL を構成するには

1. テキスト エディターで **RSReportServer.config** ファイルを開きます。 既定では、\Program Files\Microsoft SQL Server\MSRS12.\<*instancename*>\Reporting Services\ReportServer にあります。  

2. **ReportServerURL**を探します。

3. レポート サーバー インスタンスの URL に置き換えます。

4. 変更を保存してファイルを閉じます。

構成ファイルの詳細については、「[Reporting Services の構成ファイル &#40;RSreportserver.config&#41; の変更」](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)および「[RsReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)」を参照してください。

## <a name="customize-styles-or-application-title"></a>スタイルのカスタマイズまたはアプリケーションのタイトルのカスタマイズ

カスタム ブランド パッケージを作成して、Web ポータルに使用する色を変更することができます。 詳細については、「[Web ポータルのブランド化](../branding-the-web-portal.md)」を参照してください。

#### <a name="to-modify-application-title"></a>アプリケーションのタイトルを変更するには

1. レポート サーバーに対する **システム管理者** 権限が割り当てられたアカウントを使用してログオンします。

2. Internet Explorer を開きます。

3. Web ポータルの URLを入力します。 既定では、 https://\<**your-server-name**>/reports ですが、Reporting Services を名前付きインスタンスとしてインストールした場合、既定の URL は https://\<**your-server-name**>/reports\< **_instancename**> になります。

4. **[サイトの設定]** を選択します。

5. **[全般]** タブの **[名前]** で、 **SQL Server Reporting Services** を別の名前に置き換えます。

6. **[適用]** を選択します。

## <a name="next-steps"></a>次の手順

[Web ポータル](../../reporting-services/web-portal-ssrs-native-mode.md)  
[Reporting Services のブラウザー サポート](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)
[URL の構成](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[Reporting Services のインストール状態の検証](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
[Reporting Services 機能の有効化と無効化](../../reporting-services/report-server/turn-reporting-services-features-on-or-off.md)   
[Reporting Services ネイティブ モードのレポート サーバーの管理](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
[RsReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[ローカル管理用のネイティブ モードのレポート サーバーの構成](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)

 その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
