---
title: Reporting Services 機能の有効化と無効化 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, configuration
- security [Reporting Services], strategies
ms.assetid: b69db02a-43a7-4fdc-ad9b-438d817a7f83
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cf44b6af30d5db32c006c5a7d9b59d1810840d18
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103188"
---
# <a name="turn-reporting-services-features-on-or-off"></a>Reporting Services 機能の有効化と無効化
  運用レポート サーバーに対する外部からの攻撃の危険性を低減するためのロックダウン ストラテジには含まれないレポート サーバー機能を無効にできます。 ほとんどの場合は、複数の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 機能を同時に実行して、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]で提供される機能をすべて利用します。 ただし、配置モデルによっては、不要な機能を無効にすることができます。 たとえば、すべてのレポート処理をスケジュールに従って実行するように構成すると、バックグラウンド処理だけを有効にすることもできます。 同様に、対話型の要求時レポートだけが必要な場合は、レポート サーバー Web サービスだけを実行することもできます。  
  
 このトピックの手順では、ネイティブ モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 機能を無効にする方法を示します。 機能の構成は、 `RsReportServer.config` ファイルを直接編集する、 **のポリシー ベースの管理の** [Reporting Services のセキュリティ構成] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ファセットを使用するなど、さまざまな方法で行うことができます。 次のリンクを使用して、機能を有効または無効にする方法を説明した手順を探します。  
  
-   [レポート サーバー Web サービス](#RSWebSvc)  
  
-   [スケジュールされたイベントおよび処理](#Sched)  
  
-   [レポート マネージャー](#ReportManager)  
  
-   [レポート ビルダー](#ReportBuilder)  
  
-   [レポート データ ソース用 Windows 統合セキュリティ](#WinIntSec)  
  
##  <a name="RSWebSvc"></a> Report Server Web Service  
  
#### <a name="to-turn-on-or-off-the-report-server-web-service-by-editing-configuration"></a>構成を編集してレポート サーバー Web サービスを有効または無効にするには  
  
1.  テキスト エディターで `RsReportServer.config` ファイルを開きます。 詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「[Reporting Services の構成ファイル &#40;RSreportserver.config&#41; の変更](modify-a-reporting-services-configuration-file-rsreportserver-config.md)」を参照してください。  
  
2.  レポート サーバー Web サービスを有効にするには、`IsWebServiceEnabled` を `true` に設定します。  
  
    ```  
    <IsWebServiceEnabled>true</IsWebServiceEnabled>  
    ```  
  
3.  レポート サーバー Web サービスを無効にするには、`IsWebServiceEnabled` を `false` に設定します。  
  
    ```  
    <IsWebServiceEnabled>false</IsWebServiceEnabled>  
    ```  
  
4.  変更を保存し、ファイルを閉じます。  
  
#### <a name="to-turn-on-or-off-the-report-server-web-service-by-using-sql-server-management-studio"></a>SQL Server Management Studio を使用してレポート サーバー Web サービスを有効または無効にするには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を開き、構成する [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インスタンスに接続します。  
  
2.  オブジェクト エクスプローラーで [ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ] ノードを右クリックし、 **[ポリシー]** をポイントして、 **[ファセット]** をクリックします。  
  
3.  **[ファセット]** ボックスの一覧で、 **[Reporting Services のセキュリティ構成]** を選択します。  
  
4.  **[ファセットのプロパティ]** で次の操作を行います。  
  
    -   レポート サーバー Web サービスを有効にするには設定**WebServiceAndHTTPAccessEnabled**に`True`します。  
  
    -   レポート サーバー Web サービスを無効にするには、次のように設定します。 **WebServiceAndHTTPAccessEnabled**に`False`します。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="Sched"></a> 定期的なイベントおよび配信  
  
#### <a name="to-turn-on-or-off-scheduled-events-and-delivery-by-editing-configuration"></a>構成を編集して定期的なイベントおよび配信を有効または無効にするには  
  
1.  テキスト エディターで RsReportServer.config ファイルを開きます。 詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「[Reporting Services の構成ファイル &#40;RSreportserver.config&#41; の変更](modify-a-reporting-services-configuration-file-rsreportserver-config.md)」を参照してください。  
  
2.  スケジュールされたレポート処理および配信を有効にするには、`IsSchedulingService`、`IsNotificationService`、および `IsEventService` を `true` に設定します。  
  
    ```  
    <IsSchedulingService>true</IsSchedulingService>  
    <IsNotificationService>true</IsNotificationService>  
    <IsEventService>true</IsEventService>  
    ```  
  
3.  スケジュールされたレポート処理および配信を無効にするには、`IsSchedulingService`、`IsNotificationService`、および `IsEventService` を `false` に設定します。  
  
    ```  
    <IsSchedulingService>false</IsSchedulingService>  
    <IsNotificationService>false</IsNotificationService>  
    <IsEventService>false</IsEventService>  
    ```  
  
4.  変更を保存し、ファイルを閉じます。  
  
> [!NOTE]  
>  バックグラウンド処理によって、サーバー処理に必要なデータベース メンテナンス機能が提供されているため、バックグラウンド処理を完全に無効にすることはできません。  
  
#### <a name="to-turn-on-or-off-scheduled-events-and-delivery-by-using-sql-server-management-studio"></a>SQL Server Management Studio を使用して定期的なイベントおよび配信を有効または無効にするには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を開き、構成する [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インスタンスに接続します。  
  
2.  オブジェクト エクスプローラーで [ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ] ノードを右クリックし、 **[ポリシー]** をポイントして、 **[ファセット]** をクリックします。  
  
3.  **[ファセット]** ボックスの一覧で、 **[Reporting Services のセキュリティ構成]** を選択します。  
  
4.  **[ファセットのプロパティ]** で次の操作を行います。  
  
    -   スケジュールされたイベントおよび配信を有効にするのには、設定**ScheduleEventsAndReportDeliveryEnabled**に`True`します。  
  
    -   スケジュールされたイベントおよび配信を無効にするには、次のように設定します。 **ScheduleEventsAndReportDeliveryEnabled**に`False`します。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  バックグラウンド処理によって、サーバー処理に必要なデータベース メンテナンス機能が提供されているため、バックグラウンド処理を完全に無効にすることはできません。  
  
##  <a name="ReportManager"></a> レポート マネージャー  
  
#### <a name="to-turn-on-or-off-report-manager-by-editing-configuration"></a>構成を編集してレポート マネージャーを有効または無効にするには  
  
1.  テキスト エディターで RsReportServer.config ファイルを開きます。 手順については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「[Reporting Services の構成ファイル &#40;RSreportserver.config&#41; の変更](modify-a-reporting-services-configuration-file-rsreportserver-config.md)」をご覧ください。  
  
2.  レポート マネージャーを有効にするには、`IsReportManagerEnabled` を `true` に設定します。  
  
    ```  
    <IsReportManagerEnabled>true</IsReportManagerEnabled>  
    ```  
  
3.  レポート マネージャーを無効にするには、`IsReportManagerEnabled` を `false` に設定します。  
  
    ```  
    <IsReportManagerEnabled>false</IsReportManagerEnabled>  
    ```  
  
4.  変更を保存し、ファイルを閉じます。  
  
#### <a name="to-turn-on-or-off-report-manager-by-using-sql-server-management-studio"></a>SQL Server Management Studio を使用してレポート マネージャーを有効または無効にするには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を開き、構成する [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インスタンスに接続します。  
  
2.  **オブジェクト エクスプローラー**で [ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ] ノードを右クリックし、 **[ポリシー]** をポイントして、 **[ファセット]** をクリックします。  
  
3.  **[ファセット]** ボックスの一覧で、 **[Reporting Services のセキュリティ構成]** を選択します。  
  
4.  **[ファセットのプロパティ]** で次の操作を行います。  
  
    -   レポート マネージャーを有効にするには設定**ReportManagerEnabled**に`True`します。  
  
    -   レポート マネージャーをオフにして、次のように設定します。 **ReportManagerEnabled**に`False`します。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="ReportBuilder"></a> レポート ビルダー  
  
#### <a name="to-turn-on-or-off-report-builder-by-using-sql-server-management-studio"></a>SQL Server Management Studio を使用してレポート ビルダーを有効または無効にするには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を開き、構成する [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インスタンスに接続します。  
  
2.  オブジェクト エクスプローラーで [ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ] ノードを右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[サーバーのプロパティ]** ダイアログ ボックスの **[ページの選択]** で **[セキュリティ]** をクリックします。  
  
    -   レポート ビルダーを有効にするには、 **[アドホック レポート実行を有効にする]** オプションを選択します。  
  
    -   レポート ビルダーを無効にするには、 **[アドホック レポート実行を有効にする]** オプションを選択解除します。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="WinIntSec"></a> Windows 統合セキュリティ  
  
#### <a name="to-turn-on-or-off-windows-integrated-security-by-using-sql-server-management-studio"></a>SQL Server Management Studio を使用して Windows 統合セキュリティを有効または無効にするには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を開き、構成する [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インスタンスに接続します。  
  
2.  オブジェクト エクスプローラーで [ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ] ノードを右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[サーバーのプロパティ]** ダイアログ ボックスの **[ページの選択]** で **[セキュリティ]** をクリックします。  
  
    -   Windows 統合セキュリティを有効にするには、 **[レポート データ ソースで Windows 統合セキュリティを有効にする]** オプションを選択します。  
  
    -   Windows 統合セキュリティを無効にするには、 **[レポート データ ソースで Windows 統合セキュリティを有効にする]** オプションを選択解除します。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
