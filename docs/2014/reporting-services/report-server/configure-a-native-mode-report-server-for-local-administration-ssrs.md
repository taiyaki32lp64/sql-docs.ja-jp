---
title: ローカル管理用のネイティブ モードのレポート サーバー (SSRS) の構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- UAC
- installing Reporting Services
- Windows Vista
- Localhost
- windows server 2008
- Vista
ms.assetid: 312c6bb8-b3f7-4142-a55f-c69ee15bbf52
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d1725e49ce825d3d57a3b41857e26a3843fbfc7c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104188"
---
# <a name="configure-a-native-mode-report-server-for-local-administration-ssrs"></a>ローカル管理用のネイティブ モードのレポート サーバー (SSRS) の構成
  レポート サーバー インスタンスをローカルに管理しようとする場合、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーを次のオペレーティング システムのいずれかに配置するには、追加の構成手順が必要です。 このトピックでは、レポート サーバーをローカル管理用に構成する方法を説明します。 インストールまたは、レポート サーバーの構成がされていないを参照してください[インストール ウィザードからの SQL Server 2014 のインストール&#40;セットアップ&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)と[Reporting Services ネイティブ モード レポート サーバーの管理](manage-a-reporting-services-native-mode-report-server.md).  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード|  
  
-   [!INCLUDE[winblue_server_2](../../includes/winblue-server-2-md.md)]  
  
-   [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]  
  
-   [!INCLUDE[win8](../../includes/win8-md.md)]  
  
-   [!INCLUDE[win8srv](../../includes/win8srv-md.md)]  
  
-   [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]  
  
-   [!INCLUDE[win7](../../includes/win7-md.md)]  
  
-   [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]  
  
 記載されているオペレーティング システムによって権限が制限されるため、ほとんどのアプリケーションは、ローカルの Administrators グループのメンバーが実行しても、標準ユーザー アカウントを使用しているかのように実行されます。  
  
 これにより、システム全体のセキュリティが向上しますが、Reporting Services がローカル管理者のために作成するあらかじめ定義された組み込みのロールの割り当てを使用できなくなります。  
  
-   [構成変更の概要](#bkmk_configuraiton_overview)  
  
-   [ローカル レポート サーバーとレポート マネージャーの管理を構成するには](#bkmk_configure_local_server)  
  
-   [ローカル レポート サーバー管理を行う目的で SQL Server Management Studio (SSMS) を構成するには](#bkmk_configure_ssms)  
  
-   [SQL Server Data Tools BI (SSDT) をローカル レポート サーバーへの発行を構成するには](#bkmk_configure_ssdt)  
  
-   [追加情報](#bkmk_addiitonal_informaiton)  
  
##  <a name="bkmk_configuraiton_overview"></a> 構成変更の概要  
 以下に示す構成変更でサーバーを構成することにより、標準ユーザーの権限を使用してレポート サーバーのコンテンツや操作を管理できます。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の URL を信頼済みサイトに追加します。 既定では、記載されているオペレーティング システムで動作している Internet Explorer は **保護モード**で実行されます。保護モードとは、同じコンピューターで実行されている高レベルのプロセスにブラウザーの要求が到達するのを防ぐ機能です。 レポート サーバー アプリケーションを信頼済みサイトに追加することで、それらのアプリケーションに対して保護モードを無効にすることができます。  
  
-   Internet Explorer で **[管理者として実行]** 機能を使用しなくてもコンテンツや操作を管理できる権限をレポート サーバー管理者に与えるロールの割り当てを作成します。 Windows ユーザー アカウントに対してロールの割り当てを作成することにより、Reporting Services が作成するあらかじめ定義された組み込みのロールの割り当てを置き換える明示的なロールの割り当てを使用して、コンテンツ マネージャーおよびシステム管理者の権限でレポート サーバーにアクセスできるようになります。  
  
##  <a name="bkmk_configure_local_server"></a> ローカル レポート サーバーとレポート マネージャーの管理を構成するには  
 ローカル レポート サーバーを参照しているときに、次のようなエラーが表示された場合は、このセクションの構成手順を完了してください。  
  
-   ユーザー `'Domain\[user name]`' に必要なアクセス許可がありません。 適切なアクセス許可が付与されていることと、Windows ユーザー アカウント制御 (UAC) の制限に対処済みであることを確認してください。  
  
###  <a name="bkmk_site_settings"></a> ブラウザー内の信頼済みサイトの設定  
  
1.  [管理者として実行] の権限を使用してブラウザー ウィンドウを開きます。 **[スタート]** メニューの **[すべてのプログラム]** をクリックし、 **[Internet Explorer]** を右クリックして **[管理者として実行]** をクリックします。  
  
2.  **[許可]** をクリックして続行します。  
  
3.  URL アドレスにレポート マネージャーの URL を入力します。 手順については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「[レポート マネージャー (SSRS ネイティブ モード)](../report-manager-ssrs-native-mode.md)」を参照してください。  
  
4.  **[ツール]** をクリックします。  
  
5.  **[インターネット オプション]** をクリックします。  
  
6.  **[セキュリティ]** をクリックします。  
  
7.  **[信頼済みサイト]** をクリックします。  
  
8.  **[サイト]** をクリックします。  
  
9. `http://<your-server-name>`を追加します。  
  
10. 既定のサイトに HTTPS を使用していない場合は、 **[ゾーンのすべてのサイトにサーバー証明書 (https:) を必要とする]** チェック ボックスをオフにします。  
  
11. **[追加]** をクリックします。  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
###  <a name="bkmk_configure_folder_settings"></a> レポート マネージャーのフォルダーの設定  
  
1.  レポート マネージャーのホーム ページで、 **[フォルダー設定]** をクリックします。  
  
2.  [フォルダー設定] ページの **[セキュリティ]** をクリックします。  
  
3.  **[新しいロールの割り当て]** をクリックします。  
  
4.  **[グループ名またはユーザー名]** フィールドに、 `<domain>\<user>`という形式で自分 (レポート サーバー管理者) の Windows ユーザー アカウントを入力します。  
  
5.  **[コンテンツ マネージャー]** を選択します。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
###  <a name="bkmk_configure_site_settings"></a> レポート マネージャーのサイトの設定  
  
1.  管理者特権を使用してブラウザーを開き、レポート マネージャー ( `http://<server name>/reports`) を参照します。  
  
2.  ホーム ページの上隅にある **[サイトの設定]** をクリックします。  
  
    > [!TIP]  
    >  **注:** 表示されない場合、**サイト設定**オプション、閉じるとブラウザーを閉じて、管理者特権でのレポート マネージャーを参照します。  
  
3.  **[セキュリティ]** をクリックします。  
  
4.  **[新しいロールの割り当て]** をクリックします。  
  
5.  **[グループ名またはユーザー名]** フィールドに、 `<domain>\<user>`という形式で自分 (レポート サーバー管理者) の Windows ユーザー アカウントを入力します。  
  
6.  **[システム管理者]** を選択します。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  レポート マネージャーを閉じます。  
  
9. **[管理者として実行]** を使用せずに再び Internet Explorer でレポート マネージャーを開きます。  
  
##  <a name="bkmk_configure_ssms"></a> ローカル レポート サーバー管理を行う目的で SQL Server Management Studio (SSMS) を構成するには  
 既定では、管理者権限を使用して [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を開始した場合以外は、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] で使用できるレポート サーバー プロパティのいずれにもアクセスできません。  
  
 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]** ロール プロパティとロールの割り当てを構成して、高度な権限で [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を毎回起動する必要をなくすには、以下の手順を実行します。  
  
-   **[スタート]** メニューの **[すべてのプログラム]** をクリックし、 **[SQL Server 2014]** をクリックし、 **[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]** を右クリックして **[管理者として実行]** をクリックします。  
  
-   ローカル [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サーバーへの接続  
  
-   **[セキュリティ]** ノードで、 **[システム ロール]** をクリックします。  
  
-   **[システム管理者]** を右クリックし、 **[プロパティ]** をクリックします。  
  
-   **[システム ロールのプロパティ]** ページで、 **[レポート サーバーのプロパティを表示]** を選択します。 システム管理者ロールを持つメンバーに割り当てる他のすべてのプロパティを選択します。  
  
-   **[OK]** をクリックします。  
  
-   [閉じる] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
-   システム ロール "システム管理者" にユーザーを追加するには、このトピックで既に登場した「 [レポート マネージャーのサイトの設定](#bkmk_configure_site_settings) 」セクションを参照してください。  
  
 これで、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を開くときに **[管理者として実行]** を明示的に選択しなくても、レポート サーバーのプロパティにアクセスできるようになりました。  
  
##  <a name="bkmk_configure_ssdt"></a> SQL Server Data Tools BI (SSDT) をローカル レポート サーバーへの発行を構成するには  
 [!INCLUDE[SSDTDev11](../../includes/ssdtdev11-md.md)] を、このトピックの最初のセクションに記載したオペレーティング システムのいずれかにインストールした状況で、SSDT を使用してローカルのネイティブ モード レポート サーバーを操作する場合は、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] を高度な権限で開くか、レポート サービス ロールを構成しない限り、権限エラーが発生します。 たとえば、十分な権限がない場合には次のような問題が発生します。  
  
-   ローカル レポート サーバーにレポート アイテムを配置しようとすると、 **[エラー一覧]** ウィンドウに次のようなエラー メッセージが表示されます。  
  
    -   ユーザー 'Domain\\<user name\>' には、この操作を行うのに必要な権限が与えられていません。  
  
 **SSDT を開くときに高度な権限を毎回使用するには:**  
  
1.  スタート画面から「`sql server`し、右クリックし、 **for Visual Studio の SQL Server Data Tools**します。 **[管理者として実行]** をクリックします  
  
     **または**、それ以前のオペレーティング システムで次のように操作します。  
  
     **[スタート]** メニューの **[すべてのプログラム]** をクリックし、 **[SQL Server 2014]** をクリックし、 **[SQL Server Data Tools]** を右クリックして **[管理者として実行]** をクリックします。  
  
2.  **[続行]** をクリックします。  
  
3.  **[プログラムの実行]** をクリックします。  
  
 これで、レポートやその他のアイテムをローカル レポート サーバーに配置できるようになります。  
  
 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ロール プロパティとロールの割り当てを構成して、高度な権限で SSDT を毎回起動する必要をなくすには、以下の手順を実行します。**  
  
-   このトピックの「 [レポート マネージャーのフォルダーの設定](#bkmk_configure_folder_settings) 」および「 [レポート マネージャーのサイトの設定](#bkmk_configure_site_settings) 」を参照してください。  
  
##  <a name="bkmk_addiitonal_informaiton"></a> 追加情報  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の管理に関連する追加の一般的な手順は、Windows ファイアウォールでポート 80 を開いてレポート サーバー コンピューターへのアクセスを許可することです。 手順については、「 [Configure a Firewall for Report Server Access](configure-a-firewall-for-report-server-access.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [「Reporting Services ネイティブ モードのレポート サーバーの管理」](manage-a-reporting-services-native-mode-report-server.md)  
  
  
