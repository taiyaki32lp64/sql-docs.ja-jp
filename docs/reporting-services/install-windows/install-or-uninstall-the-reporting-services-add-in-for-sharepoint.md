---
title: SharePoint 用 Reporting Services アドインのインストールまたはアンインストール | Microsoft Docs
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
ms.assetid: c2804a9a-08ea-4f4a-805d-a2c19c68733d
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 41a93cfdac331830477171dfdfc4f306c073bda3
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893374"
---
# <a name="install-or-uninstall-the-reporting-services-add-in-for-sharepoint"></a>SharePoint 用 Reporting Services アドインのインストールまたはアンインストール

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  SharePoint サーバー上で [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Add-in for SharePoint products (rsSharePoint.msi) on SharePoint servers to enable [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] features within a SharePoint deployment. 提供される機能には、Power View、レポート ビューアー Web パーツ、URL プロキシ エンドポイント、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンテンツの種類、アプリケーション ページなどがあります。これにより、レポート、データ ソース、その他のレポート サーバー コンテンツを SharePoint サイト上で作成、表示、管理できます。 SharePoint 製品用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインは、SharePoint モードで実行されるレポート サーバーに必要なコンポーネントです。 アドインは、SQL Server 2016 セットアップ ウィザードからインストールするか、SQL Server 2016 機能パックから rsSharePoint.msi をダウンロードしてインストールすることができます。 アドインのバージョンの一覧およびダウンロード ページについては、「 [SharePoint 製品用 Reporting Services アドインの検索場所](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)」を参照してください。  
  
> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。
  
##  <a name="bkmk_prereq"></a> 前提条件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインのインストールは、レポート サーバーと SharePoint 製品のインスタンスを統合するために必要ないくつかの手順の 1 つです。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストールと構成について詳しくは、「[SharePoint モードでの最初のレポート サーバーのインストール](install-the-first-report-server-in-sharepoint-mode.md)」をご覧ください。  
  
-   複数の Web フロントエンド アプリケーションがある SharePoint ファームに [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を統合する場合は、Web サーバー フロントエンドがあるファームの各コンピューターにアドインをインストールします。 この作業は、レポート サーバー コンテンツのアクセスに使用する Web フロントエンドに対してのみ行ってください。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインをインストールするには、コンピューターの管理者である必要があります。 たとえば、コマンド プロンプトで rsSharePoint.msi を実行する場合は、 **[管理者として実行]** オプションを使用して、管理者特権でコマンド プロンプトを開く必要があります。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインをインストールするには、SharePoint ファーム管理者グループのメンバーである必要があります。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 統合機能をアクティブ化するには、サイト コレクションの管理者である必要があります。   
  
##  <a name="bkmk_whatinstalled"></a> アドインがインストールする内容  
 アドインのセットアップ プロセスは、2 つのフェーズで構成されます。標準インストールが完了すると、どちらのフェーズも自動的に完了します。  
  
-   最初のフェーズでは、正しいフォルダーにファイルをインストールします。 それらのフォルダーは、SharePoint 配置では標準です。 インストールされるファイルの 1 つに rsCustomAction.exe ファイルがあります。  
  
-   インストールの 2 つ目の部分では、一連のカスタム アクションを実行して、SharePoint に [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ファイルを登録します。 カスタム アクションは、rsCustomAction.exe から実行します。 2 つのフェーズで構成される完全なインストールが終了すると、exe ファイルは削除されます。 **[ファイルのみ]** のインストールを実行すると、インストールの終わりに rsCustomAction.exe は実行されず、ドライブに残ります。  
  
## <a name="the-reporting-services-installation-order"></a>Reporting Services のインストールの順序  
 アドインは、SharePoint をインストールする前でも後でもインストールできます。 アドインは、SharePoint の配置前の標準に準拠し、SharePoint のインストールで使用された場所にファイルをインストールします。  
  
> [!NOTE]  
>  SharePoint 製品より前にアドインをインストールする利点は、新しいサーバーをファームに追加すると、Reporting Services アドインが SharePoint ファームによって構成およびアクティブ化されることです。  
  
##  <a name="bkmk_3ways_to_install"></a> インストール方法の概要  
 SharePoint 製品用 SQL Server 2016 Reporting Services アドインは、次の 2 つの方法のいずれかを使ってインストールできます。  
  
-   **インストール ウィザード:** ![メモ](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/ssrs-fyi-note.png "メモ") SQL Server 2016 では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードでアドインをインストールできます。 ウィザードの **[機能の選択]** ページで、 **[SharePoint 製品用 Reporting Services アドイン]** を選択します。  
  
-   **rsSharepoint.msi:** インストール メディアまたはダウンロードからアドインを直接インストールする。 rsSharepoint.msi は、グラフィカル ユーザー インターフェイスもコマンド ライン インストールもサポートしています。 .msi を管理者特権を使用して実行する必要があるため、まず高度な権限でコマンド プロンプトを開いてから、コマンド ラインから rsSharepoint.msi を実行します。 アドインのダウンロードの詳細については、「 [SharePoint 製品用 Reporting Services アドインの検索場所](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)」を参照してください。  
  
    > [!NOTE]  
    >  サイレント コマンド ライン インストールで **/q** スイッチを使用する場合、使用許諾契約書は表示されません。 インストール方法にかかわらず、このソフトウェアの使用は、使用許諾契約に基づいています。ユーザーは使用許諾契約に準拠する責任があります。  
  
##  <a name="bkmk_install_rssharepoint"></a> rsSharePoint.msi インストール ファイルを使用したアドインのインストール  
 このセクションは、.msi インストール ウィザードの実行またはコマンド ライン インストールにより、rssharepoint.msi を直接インストールすることに関連しています。 SQL Server インストール ウィザードを使用してアドインをインストールする場合は、次の手順を実行する必要はありません。  
  
 次のコマンドを実行すると、コマンド ライン スイッチの全リストが表示されます。  
  
```  
Rssharepoint.msi /?  
```  
  
1.  **アドインのセットアップ プログラム (** rsSharepoint.msi [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ) をダウンロードします。 アドインのダウンロードの詳細については、「 [SharePoint 製品用 Reporting Services アドインの検索場所](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)」を参照してください。  
  
2.  管理者は、 **rsSharepoint.msi** を実行して、インストール ウィザードを実行します。 ウィザードに、"ようこそ" ページ、ソフトウェア ライセンス条項、および登録情報ページが表示されます。 セットアップ時に、次のパスにフォルダーが作成され、そのフォルダーにファイルがコピーされます。  
  
     `%program files%\common files\Microsoft Shared\Web Server Extensions\15\` (SharePoint 2013)
  
     内の複数の  
  
     `%program files%\common files\Microsoft Shared\Web Server Extensions\16\` (SharePoint 2016)  
  
3.  SharePoint サーバーの全体管理で、レポート サーバーの設定と機能のアクティブ化を構成します。 。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モードのインストールと構成の詳細については、「[SharePoint モードでの最初のレポート サーバーのインストール](install-the-first-report-server-in-sharepoint-mode.md)」を参照してください。  
  
###  <a name="bkmk_files_only_installation"></a> ファイルのみのインストール  
 インストールのカスタム アクション フェーズをスキップしてファイルをインストールするには、SKIPCA オプションを指定してコマンド ラインから rssharepoint.msi を実行します。  
  
1.  **管理者権限を使用して**コマンド プロンプトを開きます。  
  
2.  次のコマンドを実行します。  
  
    ```  
    Msiexec.exe /i rsSharePoint.msi SKIPCA=1  
    ```  
  
 インストールのユーザー インターフェイスが開き、正常に実行され、 **rsCustomAction.exe** ファイルがインストールされます。 ただし、.exe はインストールの終了時には実行されず、インストールの終了後、 **rsCustomAction.exe** はコンピューター上に残ります。  
  
### <a name="use-a-two-step-installation-to-troubleshoot-installation-issues"></a>2 ステップのインストールを使用したインストールの問題のトラブルシューティング  
 インストール中にエラーが発生した場合は、コマンド ラインから 2 つのステップでセットアップを実行できます。  
  
1.  **管理者権限で** コマンド プロンプトを開き、前のセクションの説明に従い、ファイルのみのインストールを実行します。  
  
2.  カスタム アクションの実行可能ファイルを実行します。  
  
    1.  ファイル **rsCustomAction.exe**を含むフォルダーに移動します。 このファイルは、アドインのファイルのみのインストールを実行することで、コンピューターにコピーされます。 **rsCustomAction.exe** は **%Temp%** ディレクトリにあります。 ファイルに移動するには、コマンド プロンプトから次のように入力します。  
  
         **CD %temp%** 。  
  
         ファイルを **\Users\\<ユーザー名\>\AppData\Local\Temp** に配置する必要があります。  
  
    2.  次のコマンドを入力します。 この構成手順は、完了まで数分かかります。 この処理中に W3SVC サービスが再起動されます。 プログラムでファイルがコピーされ、コンポーネントが登録され、SharePoint 製品構成ウィザードが実行されると共に、状態メッセージが表示されます。  
  
        ```  
        rsCustomAction.exe /i  
        ```  
  
    3.  変更が有効になるまでの時間はサーバー環境によって異なる場合があります。 **iisreset** 実行して、更新にかかる時間を短縮することもできます。  
  
### <a name="quiet-installation-for-scripting"></a>スクリプト作成のためのサイレント インストール  
 **/q** スイッチまたは **/quiet** スイッチを使用すると、ダイアログや警告が表示されない "サイレント" インストールを実行できます。 サイレント インストールは、アドインのインストールのスクリプトを作成する場合に役立ちます。  
  
> [!NOTE]  
>  サイレント コマンド ライン インストールで **/q** スイッチを使用する場合、使用許諾契約書は表示されません。 インストール方法にかかわらず、このソフトウェアの使用は、使用許諾契約に基づいています。ユーザーは使用許諾契約に準拠する責任があります。  
  
 サイレント インストールを行うには、次の手順を実行します。  
  
1.  **管理者権限を使用して**コマンド プロンプトを開きます。  
  
2.  次のコマンドを実行します。  
  
    ```  
    Msiexec.exe /i rsSharePoint.msi /q  
    ```  
  
##  <a name="bkmk_remove_addin"></a> Reporting Services アドインを削除する方法  
 SharePoint 製品用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows のコントロール パネルまたはコマンド ラインからアンインストールできます。  
  
1.  コントロール パネルを使用すると、現在のコンピューター上のファイルが完全にアンインストールされます。 **さらに** 、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のオブジェクトと機能が SharePoint ファームから削除されます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のオブジェクトと機能が削除されると、レポートの確認と更新ができなくなります。  
  
2.  コマンド ラインでアドインをアンインストールする場合は、LocalOnly パラメーターを使用して、ローカル コンピューターからアドイン ファイルのみを削除できます。ファーム内にある [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のオブジェクトと機能は変更されません。  
  
 アドインをアンインストールすると、レポート サーバーでレポートの処理に使用されているサーバー統合機能が削除されます。 SharePoint サーバーの全体管理ページおよびその他のカスタム [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ページから、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のページも削除されます。 また、影響を受ける SharePoint サイトで、今後使用しないレポートとその他のレポート サーバー アイテムをすべて削除することもできます。 これらは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインを削除すると実行できなくなります。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインをアンインストールするには、SharePoint がインストールされている必要があります。 SharePoint を先にアンインストールした場合は、それを再インストールしないと [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインをアンインストールできません。  
  
 アドインをアンインストールする手順は、スタンドアロンのサーバーの場合もサーバー ファームの場合も同じです。 セットアップにより、インストール時に追加されたプログラム ファイルと構成設定が削除されます。  
  
 アドインをアンインストールしても次のものは削除されません。  
  
-   SharePoint の構成データベースとコンテンツ データベースへのアクセスに使用される、レポート サーバー サービス アカウント用に作成されたログイン。 レポート サーバー サービス アカウント用のログインは、SharePoint データベースのホストに使用されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスからすべて削除する必要があります。  
  
-   レポート ユーザー用に作成した権限またはグループ。 レポート サーバーの機能へのアクセスを許可するためにカスタム権限レベルまたは SharePoint グループを作成した場合は、不要になった権限を取り消す必要があります。  
  
-   SharePoint ライブラリにアップロードしたデータ ファイル。レポート定義 (.rdl)、共有データ ソース (.rsds)、パブリッシュ済みレポート アイテム (.rsc) などのファイルは 削除されませんが、実行されなくなります。 これらのファイルは手動で削除する必要があります。  
  
-   セットアップによって、レポート サーバー データベースが削除されたり、統合操作に使用されていたレポート サーバー インスタンスが変更されることはありません。  
  
### <a name="to-uninstall-from-windows-control-panel"></a>Windows のコントロール パネルからアンインストールを行うには  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows のコントロール パネルからウィザードを起動してアドインを削除するには、次の手順を実行します。  
  
1.  コントロール パネルの **[プログラム]** で、 **[プログラムのアンインストール]** をクリックします。  
  
2.  **[SharePoint 用 Microsoft SQL Server RS アドイン]** を選択します。 コマンド プロンプトから、スイッチを指定せずに **rssharepoint.msi** を実行してアンインストール ウィザードを起動することもできます。  
  
3.  **[削除]** をクリックします。  
  
### <a name="uninstall-from-the-command-line"></a>コマンド ラインからのアンインストール  
 アドインをコマンド ラインからアンインストールするには、次の手順を実行します。  
  
1.  **管理者権限を使用して**コマンド プロンプトを開きます。  
  
2.  次のコマンドを実行します。  
  
    ```  
    msiexec.exe /uninstall rsSharePoint.msi  
    ```  
  
3.  確認メッセージ ボックスが表示されます。 **[はい]** をクリックします。  
  
### <a name="uninstall-the-add-in-from-the-local-server-only"></a>ローカル サーバーのみからのアドインのアンインストール  
 前に説明したアドインのアンインストール方法では、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の機能とオブジェクトがファームから削除されます。 マルチサーバー ファームにおいて、ローカル コンピューターからのみアドインをアンインストールして、SharePoint ファームは稼働させておく場合は、次の手順を実行します。  
  
1.  **管理者権限を使用して**コマンド プロンプトを開きます。  
  
2.  次のコマンドを実行します。  
  
    ```  
    Msiexec.exe /uninstall rsSharePoint.msi LocalOnly=1  
    ```  
  
 これにより、SharePoint から [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンポーネントの登録が解除され、ファイルが削除されます。ただし対象は、ローカル コンピューターのみです。  
  
 SharePoint から [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の機能の登録を解除するが、後で使用するためにファイルをディスクに残しておくには、次の手順を実行します。  
  
1.  **管理者権限を使用して**コマンド プロンプトを開きます。  
  
2.  次のコマンドを実行します。  
  
    ```  
    rsCustomAction.exe /p  
    ```  
  
 上記の手順は、SkipCA=1 で .msi がインストールされていること、および rscusstomaction.exe が使用可能であることを前提としています。 詳細については、ファイルのみのインストールを説明したセクションを参照してください。  
  
##  <a name="bkmk_repair"></a> コマンド ラインから rssharepoint.msi を修復する方法  
 コマンド ラインを使用して [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインを修復またはアンインストールするには、次の手順を実行します。  
  
1.  **管理者権限を使用して**コマンド プロンプトを開きます。  
  
2.  次のコマンドを実行します。  
  
    ```  
    msiexec.exe /f rssharepoint.msi  
    ```  
  
##  <a name="bkmk_logfiles"></a> セットアップ ログ ファイル  
 セットアップの実行中は、 **アドインをインストールしたユーザーの** %temp% [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] フォルダー内のログ ファイルに情報が記録されます。 このフォルダーのパスは、**C:\Users\\<ユーザー名\>\AppData\Local\Temp** などです。ファイル名の形式は **RS_SP_\<番号>.log** で、実際の名前は **RS_SP_0.log** のようになります。 ログ内では、エラーは "SSRSCustomActionError" という文字列から始まります。  
  
> [!NOTE]  
>  AppData は Windows オペレーティング システム内の隠れたフォルダーです。 隠れたファイルとフォルダーを表示するには、Windows エクスプローラーのフォルダー設定を変更する必要がある場合があります。  
  
#### <a name="view-a-log-file-with-windows-notepad"></a>Windows メモ帳でのログ ファイルの表示  
  
1.  次のコマンドは、コマンド プロンプトのパスを変更し、rs ログ ファイルを一覧表示し、Windows メモ帳でそれらのファイルの 1 つを表示します。  
  
    ```  
    cd %temp%  
    ```  
  
    ```  
    Dir rs_sp*.log  
    ```  
  
    ```  
    notepad rs_sp_3.log  
    ```  
  
#### <a name="view-a-log-file-with-powershell"></a>PowerShell でのログ ファイルの表示  
  
1.  SharePoint 管理シェルから次のコマンドを入力すると、フィルター選択された "ssrscustomactionerror" を含む行の一覧がファイルから返されます。  
  
    ```  
    Get-content -path C:\Users\<UserName\AppData\Local\Temp\rs_sp_0.log | select-string "ssrscustomactionerror"  
    ```  
  
2.  出力は次のようになります。  
  
     `2011-05-23 12:40:12: SSRSCustomActionError: SharePoint is installed, but not configured`」を参照してください。  
  
##  <a name="bkmk_upgrade"></a> アップグレード  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインの既存のバージョンがインストールされている場合は、最新のバージョンにアップグレードできます。 アドイン セットアップ時に既存のバージョンが検出され、更新するかどうかを確認するメッセージが表示されます。 エラー メッセージは、次のようになります。  
  
 **このシステムから、この製品の古いバージョンが検出されました。インストールされているバージョンをアップグレードしますか?**  
  
 確認すると、アドインの古いバージョンが削除され、新しいバージョンがインストールされます。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインはインスタンス対応ではありません。 このアドインのインスタンスは 1 台のコンピューターで 1 つだけ実行できます。 異なるバージョンと現在のバージョンとを同時に実行することはできません。  
  
##  <a name="bkmk_rscustomaction"></a> RsCustomAction.exe  
 次の表は、rscustomaction.exe スイッチについてまとめたものです。  
  
|スイッチ|[説明]|  
|------------|-----------------|  
|i|カスタム アクションをインストールします。 これにより、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンポーネントが SharePoint に登録されます。 W3SVCservice サービスが再起動されます。|  
|r|Repair|  
|u|アンインストール。 これにより、SharePoint ファーム全体から [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンポーネントの登録が解除されますが、ファイルはディスクに残ります。 W3SVCservice サービスが再起動されます。|  
|p|ローカル アンインストール。 これにより、ローカル コンピューターのみから [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンポーネントの登録が解除されます。 ファイルはディスクに残ります。 W3SVCservice サービスが再起動されます。|  
|t|SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 2005 のみ。 レポート サーバーにレポート サーバー データベースに対して機能する接続があるかどうかをテストします。|  
  
## <a name="configuring-reporting-services"></a>Reporting Services の構成  
 必要なコンピューターにアドインをインストールしたら、SharePoint サーバーの全体管理からレポート サーバーを構成する必要があります。 必要な手順は、さまざまなテクノロジがインストールされた順序によって異なります。 詳細については、「[SharePoint モードでの最初のレポート サーバーのインストール](install-the-first-report-server-in-sharepoint-mode.md)」および「[Reporting Services レポート サーバー &#40;SharePoint モード&#41;](../../reporting-services/report-server-sharepoint/reporting-services-report-server-sharepoint-mode.md)」をご覧ください。  
  
## <a name="see-also"></a>参照

[SharePoint モードでの最初のレポート サーバーのインストール](install-the-first-report-server-in-sharepoint-mode.md)   
[Reporting Services Report Server &#40;SharePoint Mode&#41; (Reporting Services レポート サーバー &#40;SharePoint モード&#41;)](../../reporting-services/report-server-sharepoint/reporting-services-report-server-sharepoint-mode.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
