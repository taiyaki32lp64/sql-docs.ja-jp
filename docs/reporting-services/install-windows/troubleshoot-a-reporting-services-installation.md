---
title: Reporting Services インストール時の問題解決 | Microsoft Docs
ms.date: 01/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.assetid: e2536f7f-d90c-4571-9ffd-6bbfe69018d6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 281eeffa237a24e6da8794e99ff6d4fd3a716181
ms.sourcegitcommit: a1ddeabe94cd9555f3afdc210aec5728f0315b14
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "68889697"
---
# <a name="troubleshoot-a-reporting-services-installation"></a>Reporting Services インストール時の問題解決

  セットアップ中にエラーが発生して [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をインストールできない場合は、この記事の手順を使用して、インストール エラーの原因として最も可能性が高い状況に対処してください。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に関連するその他のエラーや問題については、[SSRS の問題とエラーのトラブルシューティング](https://social.technet.microsoft.com/wiki/contents/articles/ssrs-troubleshooting-issues-and-errors.aspx)に関するページを参照してください。  
  
 発生した問題がリリース ノートに記載されている場合があるので、[オンライン リリース ノート](https://go.microsoft.com/fwlink/?linkid=236893)を参照してください。  
  
##  <a name="bkmk_setuplogs"></a> セットアップ ログのチェック  
 セットアップ エラーは、 **[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Setup Bootstrap\Log** フォルダーにあるログ ファイルに記録されます。 セットアップを実行するたびにサブフォルダーが作成されます。 サブフォルダー名はセットアップを実行した日時です。 セットアップ ログ ファイルの表示方法については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」を参照してください。  
  
-   ログ ファイルには複数のファイルが含まれます。  
  
-   製品、コンポーネント、およびインスタンスの情報を表示するには、*_summary.txt ファイルを開きます。  
  
-   セットアップ中に生成されたエラー情報を表示するには、*_errorlog.txt ファイルを開きます。  
  
-   \_\*のセットアップ情報を表示するには、*_RS [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] _ComponentUpdateSetup.log を開きます。  
  
##  <a name="bkmk_prereq"></a> 前提条件のチェック  
 セットアップでは、前提条件が自動的にチェックされます。 ただし、セットアップ時の問題のトラブルシューティングを行う場合は、セットアップでチェックされる前提条件を把握しておくと役に立ちます。  
  
-   セットアップを実行するには、アカウントがローカルの Administrators グループのメンバーであることが必要です。 セットアップには、ファイルの追加、レジストリの設定、ローカル セキュリティ グループの作成、および権限の設定を行うための権限が必要です。 既定の構成をインストールする場合は、インストールする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスにレポート サーバー データベースを作成する権限がセットアップに必要です。  
  
-   オペレーティング システムが HTTP.SYS 1.1 をサポートしている必要があります。  
  
-   HTTP サービスが有効になっていて、実行されている必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスもインストールする場合は、分散トランザクション コーディネーター (DTC) が実行されている必要があります。  
  
-   System32 フォルダーに Authz.dll があることが必要です。  
  
 インターネット インフォメーション サービス (IIS) または [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]はセットアップでチェックされなくなりました。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には MDAC 2.0 および [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] バージョン 2.0 が必要です。これらがまだインストールされていない場合は、セットアップで自動的にインストールされます。  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
##  <a name="bkmk_tshoot_sharepoint"></a> SharePoint モードのインストールでのトラブルシューティング  
  
-   [Reporting Services 構成マネージャーが起動しない](#bkmk_configmanager_notstart)  
  
-   [SQL Server 2016 SSRS を SharePoint モードでインストールした後、SharePoint サーバーの全体管理に SQL Server Reporting Services サービスが表示されない](#bkmk_no_ssrs_service)  
  
-   [Reporting Services の PowerShell コマンドレットが使用できず、コマンドが認識されない](#bkmk_cmdlets_not_recognized)  
  
-   [URL が構成されていないことを示すエラー メッセージが表示される](#bkmk_URL_not_configured)  
  
-   [SharePoint がインストールされているコンピューターが構成されていない場合にセットアップに失敗する](#bkmk_sharepoint_not_confiugred)  
  
-   [SharePoint サーバーの全体管理ページが空白である](#bkmk_central_admin_blank)  
  
-   [新しいレポート ビルダー レポートを作成しようとすると、エラー メッセージが表示される](#bkmk_reportbuilder_newreport_error)  
  
-   [RS_SHP は PREPAREIMAGE でサポートされないことを示すエラー メッセージが表示される](#bkmk_RS_SHP_notsupported)  

### <a name="bkmk_configmanager_notstart"></a> Reporting Services Configuration Manager が起動しない

 **説明:** この問題は SQL Server 2012 以降の仕様です。 Reporting Services は、SharePoint サービス アーキテクチャ用に設計されています。 SharePoint モードで [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を構成および管理するために、構成マネージャーを使用する必要はなくなりました。  
  
 **解決方法:** SharePoint モードでレポート サーバーを構成するには、SharePoint サーバーの全体管理を使用します。 詳細については、「 [Reporting Services SharePoint サービス アプリケーションの管理](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)｣を参照してください  
  
 ![[トップに戻る] リンクで使用される矢印アイコン](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン") [SharePoint モードのインストールでのトラブルシューティング](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_no_ssrs_service"></a> SQL Server 2016 SSRS を SharePoint モードでインストールした後、SharePoint サーバーの全体管理に SQL Server Reporting Services サービスが表示されない  
 **説明:** SharePoint モードの SQL Server 2016 Reporting Services および SharePoint 2013/2016 用の SQL Server 2016 Reporting Services アドインが正常にインストールされた後、次の 2 つのメニューに "SQL Server Reporting Services" が表示されない場合、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスは登録されていません。  
  
-   [SharePoint 2013/2016 サーバーの全体管理] -> [アプリケーション構成の管理] -> [サーバーのサービスの管理] ページ  
  
-   [SharePoint 2013/2016 サーバーの全体管理] -> [アプリケーション構成の管理] -> [サービス アプリケーションの管理] -> [新規作成] メニュー  
  
 **解決方法:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint Services を登録して起動するには、次の手順を完了します。  
  
1.  SharePoint 2013/2016 サーバーの全体管理を実行するコンピューターで、次を実行します。  
  
    1.  管理者特権を使用して、SharePoint 2013/2016 管理シェルを開きます。 アイコンを右クリックし、 **[管理者として実行]** をクリックします。 シェルから次の 3 つのコマンドレットを実行します。  
  
    2.  ```  
        Install-SPRSService  
        ```  
  
    3.  ```  
        Install-SPRSServiceProxy  
        ```  
  
    4.  ```  
        Get-SPServiceInstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
        ```  
  
2.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスが、[SharePoint 2013/2016 サーバーの全体管理] -> **[アプリケーション構成の管理]** -> **[サーバーのサービスの管理]** ページで **[開始]** の状態を示していることを確認します。  
  
 ![[トップに戻る] リンクで使用される矢印アイコン](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン") [SharePoint モードのインストールでのトラブルシューティング](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_cmdlets_not_recognized"></a> Reporting Services の PowerShell コマンドレットが使用できず、コマンドが認識されない  
 **説明:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の PowerShell コマンドレットを実行しようとすると、次のようなエラー メッセージが表示されます。  
  
-   用語 'Install-SPRSServiceInstall-SPRSService' は、コマンドレット、関数、スクリプト ファイル、または操作可能なプログラムの名前として **認識されません** 。 名前が正しく記述されていることを確認し、パスが含まれている場合はそのパスが正しいことを確認してから、再試行してください。 発生場所 行:1 文字:39+ Install-SPRSServiceInstall-SPRSService <<<<    + CategoryInfo          : ObjectNotFound: (Install-SPRSServiceInstall-SPRSService:String) [], CommandNotFoundExcep  
  
 **解決方法:** 次のいずれかのアクションを行います。  
  
-   SharePoint 製品用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインを実行します。 **rssharepoint.msi**。  
  
-   SQL Server のインストール メディアから、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モードをインストールします。  
  
 解決方法のいずれかを完了したときに **SharePoint 2013/2016 管理シェル**が開いていた場合は、管理シェルをいったん閉じてから開き直します。  
  
 詳細については、次の各資料を参照してください。  
  
-   [SharePoint 製品用 Reporting Services アドインの検索場所](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
-   [SharePoint モードでの最初のレポート サーバーのインストール](install-the-first-report-server-in-sharepoint-mode.md)  
  
 ![[トップに戻る] リンクで使用される矢印アイコン](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン") [SharePoint モードのインストールでのトラブルシューティング](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_URL_not_configured"></a> URL が構成されていないことを示すエラー メッセージが表示される  
 **説明:** 次のようなエラー メッセージが表示されます。  
  
 この SQL Server Reporting Services (SSRS) の機能はサポートされていません。 サーバーの全体管理を使用して、次の問題の 1 つ以上を確認し、修正してください。
 
 - レポート サーバー URL が構成されていません。 SSRS 統合ページを使用して、レポート サーバー URL を設定してください。
 
 - SSRS サービス アプリケーション プロキシが構成されていません。 SSRS サービス アプリケーションのページを使用して、プロキシを構成してください。
 
 - SSRS サービス アプリケーションは、この Web アプリケーションにマップされていません。 SSRS サービス アプリケーションのページを使用して SSRS サービス アプリケーション プロキシをこの Web アプリケーションのアプリケーション プロキシ グループに関連付けてください。 
  
 **解決方法:** このエラー メッセージに、この問題を修正するための 3 つの推奨手順が含まれています。 メッセージ "レポート サーバーの URL が構成されていません" の最初の推奨事項は、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]よりも前のレポート サーバー バージョンとの統合に関連します。 以前のレポート サーバー バージョンの SharePoint 構成は、 **SQL Server Reporting Services (2008 および 2008 R2)** を使用して **[アプリケーションの全体設定]** ページで完了されます。  
  
 **その他の情報:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスへの接続が必要な [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 機能のいずれかを使用しようとすると、このエラー メッセージが表示されます。 この機能には、次が含まれます。  
  
-   SQL Server レポート ビルダーを SharePoint ドキュメント ライブラリから開いている。  
  
-   サブスクリプションを管理する。  
  
-   サービス アプリケーションを管理する。  
  
 ![[トップに戻る] リンクで使用される矢印アイコン](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン") [SharePoint モードのインストールでのトラブルシューティング](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_sharepoint_not_confiugred"></a> SharePoint がインストールされているコンピューターが構成されていない場合にセットアップに失敗する  
 **説明:** SharePoint がインストールされているものの構成されていないコンピューターに Reporting Services SharePoint モードをインストールするよう選択した場合、次のようなメッセージが表示され、セットアップが停止します。  
  
 SQL Server セットアップは動作を停止しました  
  
 **解決方法:** SharePoint を構成し、その後 SQL Server のインストールを実行します。  
  
 **追加情報:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を既存の SharePoint 環境にインストールするとき、セットアップで [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint サービスのインストールおよび開始が試行されます。 SharePoint が構成されていないと、このサービスのインストールは失敗し、セットアップがエラーを返します。  
  
 ![[トップに戻る] リンクで使用される矢印アイコン](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン") [SharePoint モードのインストールでのトラブルシューティング](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_central_admin_blank"></a> SharePoint サーバーの全体管理ページが空白である  
 **説明:** SharePoint 2013/2016 をインストール エラーなく正常にインストールできました。 [サーバーの全体管理] を表示すると空白のページしか表示されないことがあります。  
  
 **解決方法:** この問題は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に固有のものではなく、SharePoint 環境全体における権限の構成に関連するものです。 推奨事項をいくつか以下に示します。  
  
-   開発環境に関する SharePoint 記事を確認します。 [SharePoint の全般的な開発環境をセットアップする](https://msdn.microsoft.com/library/ee554869)  
  
-   フォーラムの投稿「 [Windows 7 へのインストール後、[サーバーの全体管理] が空白ページを返す](https://social.technet.microsoft.com/Forums/en/sharepoint2010setup/thread/a422a3c8-39f6-4b9e-988a-4c4d1e745694)」を参照します。  
  
-   SharePoint サービス (SharePoint 2013/2016 サーバーの全体管理サービスなど) に使用しているサービス アカウントに、ローカル オペレーティング システムの管理者特権を付与します。  
  
 ![[トップに戻る] リンクで使用される矢印アイコン](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン") [SharePoint モードのインストールでのトラブルシューティング](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_reportbuilder_newreport_error"></a> 新しいレポート ビルダー レポートを作成しようとすると、エラー メッセージが表示される  
 **説明:** ドキュメント ライブラリ内でレポート ビルダー レポートを作成しようとすると、次のようなエラー メッセージが表示されます。  
  
 SQL Server Reporting Services サービス アプリケーションが存在しないか、またはレポート サーバーの URL がサーバーの全体管理で構成されていないため、この機能はサポートされません。  
  
 **解決方法:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションが存在し、正しく構成されていることを確認します。 詳細については、「[SharePoint モードでの最初のレポート サーバーのインストール](install-the-first-report-server-in-sharepoint-mode.md)」をご覧ください。
  
 ![[トップに戻る] リンクで使用される矢印アイコン](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン") [SharePoint モードのインストールでのトラブルシューティング](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_RS_SHP_notsupported"></a> RS_SHP は PREPAREIMAGE でサポートされないことを示すエラー メッセージが表示される  
 **説明:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に対して PREPAREIMAGE を実行しようとすると、次のようなエラー メッセージが表示されます。  
  
 指定された機能 'RS_SHP' は、SysPrep をサポートしていないため、PREPAREIMAGE アクションの実行中にはサポートされません。 SysPrep と互換性のない機能を削除し、セットアップを再実行してください。  
  
 **解決方法:** 解決方法はありません。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SYSPREP (PREPAREIMAGE) をサポートしていません。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モードでは SYSPREP をサポートしています。  
  
 ![[トップに戻る] リンクで使用される矢印アイコン](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン") [SharePoint モードのインストールでのトラブルシューティング](#bkmk_tshoot_sharepoint)  

::: moniker-end
  
##  <a name="bkmk_tshoot_native"></a> ネイティブ モードのインストールでのトラブルシューティング  
  
###  <a name="PerfCounters"></a> Windows Vista または Windows Server 2008 にアップグレードするとパフォーマンス カウンターが表示されない  
 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] を実行するコンピューターでオペレーティング システムを [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] または [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]にアップグレードした場合、アップグレード後に [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のパフォーマンス カウンターが設定されなくなります。  
  
#### <a name="to-reinstate-reporting-services-performance-counters"></a>Reporting Services のパフォーマンス カウンターを再設定するには  
  
1.  次のレジストリ キーを削除します。  
  
    -   **HKLM\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service**  
  
    -   **HKLM\SYSTEM\CurrentControlSet\Services\MSRS 2016 Windows Service**  
  
2.  コマンド ウィンドウを開き、コマンド プロンプトで次のコマンドを入力します。  
  
    -   **run \<** *.NET 4.0 Framework のディレクトリ* **>\InstallUtil.exe \<** *レポート サーバーの Bin ディレクトリ* **>\ReportingServicesLibrary.dll**  
  
        > [!NOTE]  
        >  \< *.NET 4.0 Framework ディレクトリ*> は .NET Framework 4.0 ファイルの物理パス、\<*レポート サーバーの Bin ディレクトリ*> はレポート サーバーの bin ファイルの物理パスに置き換えます。  
  
3.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスを再開します。  
  
 手順が正しく行われたことを確認するには、Web ブラウザーを開き、Web ポータルの URL またはレポート サーバーの URL に移動します。 その後、パフォーマンス モニターを開き、カウンターが機能していることを確認します。  
  
#### <a name="to-add-the-performance-registry-keys-again-by-using-registry-editor"></a>レジストリ エディターを使用してパフォーマンス レジストリ キーをもう一度追加するには  
  
1.  レジストリ エディターを開きます。  
  
    1.  **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。  
  
    2.  **[ファイル名を指定して実行]** ダイアログ ボックスで、 **[名前]** ボックスに「 **regedit**」と入力します。  
  
2.  レジストリ エディターで、次のレジストリ キーを選択します。 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service\Performance`  
  
3.  **[Performance]** ノードを右クリックし、 **[新規]** をポイントして **[複数行文字列値]** をクリックします。  
  
4.  「 **Counter Names** 」と入力して Enter キーを押します。  
  
5.  同じ手順を繰り返して、このノードに **Counter Types** レジストリ キーを追加します。  
  
6.  次のレジストリ キーに移動します。 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service\Performance`  
  
7.  **[Performance]** ノードを右クリックし、 **[新規]** をポイントして **[複数行文字列値]** をクリックします。  
  
8.  「 **Counter Names** 」と入力して Enter キーを押します。  
  
9. 同じ手順を繰り返して、このノードに **Counter Types** レジストリ キーを追加します。  
  
 64 ビット インスタンスを修復するか、レジストリ キーをもう一度手動で追加したら、パフォーマンス モニターを使用して、監視する [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] パフォーマンス オブジェクトを構成できます。  
  
###  <a name="ConfigPropsMissing"></a> SQL Server 2005 からアップグレードすると構成プロパティの ReportServerExternalURL と PassThroughCookies が構成されない  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] から [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]にアップグレードする場合は、構成プロパティの **ReportServerExternalURL** と **PassThroughCookies** がアップグレード プロセスで構成されません。 **ReportServerExternalURL** はオプションのプロパティです。SharePoint 2.0 Web パーツを使用していて、ユーザーがレポートを取得して新しいブラウザー ウィンドウで開くことができるようにする場合にのみ設定する必要があります。 **ReportServerExternalURL** の詳細については、「[構成ファイル内の URL &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)」を参照してください。 **PassThroughCookies** はカスタム認証を使用する場合にのみ必要です。 **PassThroughCookies** については、「[カスタム認証クッキーを送信するようにレポート マネージャーを構成する](../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)」を参照してください。  
  
> [!NOTE]  
>  カスタム認証を使用する場合は、アップグレードを実行する代わりに現在のインストールを移行することをお勧めします。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を移行する方法については、「[Reporting Services のインストールの移行 &#40;ネイティブ モード&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)」を参照してください。  
  
 既定では、これらのプロパティは [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] の構成には存在しません。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] でこれらのプロパティを構成していて、その機能が引き続き必要な場合は、アップグレード プロセスの完了後にこれらを手動で **RSReportServer.config** ファイルに追加する必要があります。 詳細については、「[Reporting Services の構成ファイルの変更 &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)」を参照してください。  

### <a name="WindowsAuthBreaksAfterUpgrade"></a> SQL Server 2005 から SQL Server 2016 にアップグレードした後に Windows 認証を使用すると "401 - 権限がありません" エラーが表示される

 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] から [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] にアップグレードする場合に、レポート サーバー サービス アカウントにビルトイン アカウントを使って NTLM 認証を使っていると、アップグレード後にレポート サーバーや Web ポータルにアクセスするときに "401 - 権限がありません" エラーが表示される場合があります。  
  
 このメッセージが表示されるのは、Windows 認証用の既定の [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 構成が変更されているためです。 レポート サーバー サービス アカウントが NetworkService または LocalSystem である場合はネゴシエートが構成され、 レポート サーバー サービス アカウントがこれらのビルトイン アカウントではない場合は NTLM が構成されます。 アップグレード後にこの問題を修正するには、RSReportServer.config ファイルを編集して **AuthenticationType** を **RSWindowsNTLM**に設定します。 詳細については、「 [レポート サーバーで Windows 認証を構成する](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)」を参照してください。  

### <a name="Uninstall32BitBreaks64Bit"></a> SQL Server 2016 Reporting Services の 32 ビット インスタンスと 64 ビット インスタンスのサイド バイ サイド配置で 32 ビット インスタンスをアンインストールすると、64 ビット インスタンスが破損する

 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] の 32 ビット インスタンスと 64 ビット インスタンスをサイド バイ サイドでコンピューターにインストールしている場合に 32 ビット インスタンスをアンインストールすると、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の 4 つのレジストリ キーが削除されます。 キーを削除すると、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の 64 ビット インスタンスが破損します。 32 ビット インスタンスをアンインストールすると削除されるのは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の以下のレジストリ キーです。  
  
 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service\Performance:Counter Names` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Windows Service\Performance:Counter Names` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service\Performance:Counter Types` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Windows Service\Performance:Counter Types`  
  
 この問題を修正するには、64 ビット インスタンスを修復します。 修復を使用することをお勧めしますが、レジストリ エディターを使用してレジストリ キーをもう一度手動で追加することもできます。  
  
> [!CAUTION]  
>  レジストリを誤って編集すると、システムに重大な障害が発生する場合があります。 レジストリを変更する前に、コンピューター上のすべての重要なデータをバックアップしておくことをお勧めします。  
  
##  <a name="bkmk_additional"></a> その他のリソース  
 以下に示すのは、問題解決時に役立つ可能性のある追加資料です。  
  
-   TechNet Wiki: [SharePoint 2010 統合モードでの SQL Server Reporting Services (SSRS) のトラブルシューティング](https://social.technet.microsoft.com/wiki/contents/articles/troubleshoot-sql-server-reporting-services-ssrs-in-sharepoint-integrated-mode.aspx)  
  
-   [フォーラム: SQL Server Reporting Services](https://social.msdn.microsoft.com/Forums/sqlreportingservices/threads)  
  
-   フィードバックやその他のご不明な点がございましたら、 [Microsoft SQL Server UserVoice](https://feedback.azure.com/forums/908035-sql-server) にアクセスしてください。  
  
  
