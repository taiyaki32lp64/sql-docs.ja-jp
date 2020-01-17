---
title: レポート ビルダーをインストールする | Microsoft Docs
ms.date: 10/29/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d311062f362f7414a3a6d337ccc45b722e0a6c4c
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73536155"
---
# <a name="install-report-builder"></a>レポート ビルダーをインストールする
  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] はスタンドアロン アプリです。ユーザーまたは管理者によってコンピューターにインストールされます。 Microsoft ダウンロード センター、 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] レポート サーバー、または [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]と統合された SharePoint サイトからインストールできます。  

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。
  
 管理者は通常、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストールと構成、Web ポータルから [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] をダウンロードするための権限の許可、フォルダーの管理とレポート サーバーに保存されたレポート、レポート パーツ、および共有データセットに対する権限の管理を行います。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 管理の詳細については、「[Reporting Services Report Server &#40;Native Mode&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)」 (Reporting Services レポート サーバー &#40;ネイティブ モード&#41;) を参照してください。  
  
## <a name="install-includessrbnoversionincludesssrbnoversionmd-from--a--web-portal-or-sharepoint-library"></a>Web ポータルまたは SharePoint ライブラリから [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] をインストールする 
  
 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] Web ポータル、または [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] と統合された SharePoint サイトから [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]を起動できます。 詳細については、「 [レポート ビルダーの起動](../../reporting-services/report-builder/start-report-builder.md)」を参照してください。  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
### <a name="sharepoint-site-integrated-with-includessrsnoversionincludesssrsnoversion-mdmd"></a>統合された SharePoint サイト: [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]と統合された SharePoint サイトで、 **[新しいドキュメント]** メニューに **[レポート ビルダー レポート]** 、 **[レポート ビルダーのモデル]** 、および **[レポート データ ソース]** が表示されない場合は、それらのコンテンツの種類を SharePoint ライブラリに追加する必要があります。 詳細については、「 [SharePoint ライブラリへの Reporting Services のコンテンツの種類の追加](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)」を参照してください。  

::: moniker-end
 
## <a name="install-includessrbnoversionincludesssrbnoversionmd-with-system-center-configuration-manager"></a>System Center Configuration Manager を使用する [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] のインストール 
  
 管理者は System Center Configuration Manager などのソフトウェアを使用して、ユーザーのコンピューターにプログラムをプッシュすることもできます。 特定のソフトウェアを使用して [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]をインストールする方法については、そのソフトウェアのマニュアルを参照してください。 詳細については、 [System Center Configuration Manager のサイト](https://www.microsoft.com/cloud-platform/system-center-configuration-manager)を参照してください。  
  
> [!IMPORTANT]  
>  Windows Vista および Windows 7 でコマンド ライン操作を実行するには、セキュリティ機能に基づいて高度な権限が必要となり、コマンド ラインの実行権限が要求されます。 インストールはサイレント モードになりません。 インストールをサイレント モードにするには、管理者としてコマンド ラインを実行する必要があります。  
  
## <a name="system-requirements"></a>システム要件
  
 Microsoft ダウンロード センターの **レポート ビルダーのダウンロード ページ** で、「 [システム要件](https://go.microsoft.com/fwlink/?LinkID=734968) 」セクションを参照してください。
  
##  <a name="download"></a> ダウンロード サイトから [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] をインストールするには  
  
1.  [Microsoft ダウンロード センターのレポート ビルダー ページ](https://go.microsoft.com/fwlink/?LinkID=734968) で、 **[ダウンロード]** をクリックします。  
  
2.  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] のダウンロードが完了したら、  **[実行]** をクリックします。  
  
     SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] ウィザードが起動します。  
  
3.  使用許諾契約書に同意して、 **[次へ]** をクリックします。  
  
4.  **[既定のターゲット サーバー]** ページで、必要に応じて対象レポート サーバーの URL を指定します (既定の URL と異なる場合)。 **[次へ]** をクリックします。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] をレポート サーバーに接続して使用する場合は、ここでサーバーの URL を指定すると便利です。 また、[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] の **[オプション]** ダイアログ ボックスからも実行できます。  
  
5.  **[インストール]** をクリックして [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] のインストールを完了します。  
  
## <a name="to-install-includessrbnoversionincludesssrbnoversionmd-from-a-share"></a>共有から [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] をインストールするには  
  
1.  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] をローカル コンピューターにインストールするために実行する ReportBuilder3.msi の場所については、管理者にお問い合わせください。  
  
2.  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] の Windows インストーラー パッケージ (MSI) である ReportBuilder3.msi の場所を検索してクリックします。  
  
     これで SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] ウィザードが起動します。  
  
3.  「 [ダウンロード サイトからレポート ビルダーをインストールするには](#download)」の残りの手順を完了します。  
  
## <a name="to-install-includessrbnoversionincludesssrbnoversionmd-from-the-command-line"></a>コマンド ラインから [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] をインストールするには 

 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] のインストールをコマンド ラインから実行し、引数を指定してインストールをカスタマイズすることもできます。 標準の MSI 固有パラメーターに加えて、[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] に用意されているカスタム パラメーターの RBINSTALLDIR と REPORTSERVERURL も使用できます。 RBINSTALLDIR では、[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 用のルート インストール フォルダーを指定します。 REPORTSERVERURL では、 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] がサーバーにレポートを保存するときに使用する既定のレポート サーバーを指定します。  
  
 ユーザー インターフェイスをまったく操作しない完全なサイレント インストールを実行する場合は、 **/quiet** オプションを指定します。 quiet オプション フラグを使用するとインストール エラーが抑制されるように設計されています。 そのため、quiet オプションを使用する場合は、ログ記録を指定する **/l** オプションを含めることをお勧めします。   
  
1.  [Microsoft ダウンロード センターのレポート ビルダー ページ](https://go.microsoft.com/fwlink/?LinkID=734968)で、 **[ダウンロード]** をクリックします。  
  
2.  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] のダウンロードが完了したら、  **[保存]** をクリックします。  
  
3.  **[スタート]** メニューの **[ファイル名を指定して実行]** をクリックします。  
  
4.  **[開く]** ボックスに「 **cmd.** 」と入力します。  
  
5.  コマンド プロンプト ウィンドウで、ReportBuilder3.msi を保存したフォルダーに移動します。  
  
6.  次の形式のコマンドを入力します。  
  
     `msiexec/i ReportBuilder3.msi /option [value] [/option [value]]`  
  
     [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] のインストールに固有のオプションは、RBINSTALLDIR と REPORTSERVERURL の 2 つです。 コマンド ラインにこれらの引数を含める必要はありません。 標準的なコマンド ラインは次のとおりです。  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
7.  Enter キーを押してコマンドを実行します。  
  
## <a name="set-includessrbnoversionincludesssrbnoversionmd-defaults"></a>[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 既定値を設定する  
  
-   [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]のインストール後に、一部の既定のオプションを設定できます。 **[ファイル]**  >  **[オプション]** をクリックします。  
  
     既定の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web ポータルまたは SharePoint サイトを設定することをお勧めします。 詳細については、「 [Set default options for Report Builder](../../reporting-services/report-builder/set-default-options-for-report-builder.md)」を参照してください。  
  
-   **[レポート ビルダー]** をクリックします。  
  
     既存のサーバーのリストにレポート サーバーが表示されない場合は、 **[レポートを開く]** ダイアログ ボックスを閉じ、[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] の下部の **[接続]** をクリックしてサーバーに接続します。  
  
## <a name="see-also"></a>参照  
 [レポート ビルダーの起動](../../reporting-services/report-builder/start-report-builder.md)   
 [レポート ビルダーをアンインストールする](../../reporting-services/install-windows/uninstall-report-builder.md)  
  
  
