---
title: SharePoint 2013 用の SharePoint モードのインストール Reporting Services |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: b29d0f45-0068-4c84-bd7e-5b8a9cd1b538
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 8874d4c57e2fb7b94e4efac44c90e93865d2b40f
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798340"
---
# <a name="install-reporting-services-sharepoint-mode-for-sharepoint-2013"></a>SharePoint 2013 用 Reporting Services の SharePoint モードのインストール
  このトピックでは、SharePoint モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のシングル サーバー インストールの手順について説明します。 手順には、SQL Server インストール ウィザードの実行と、SharePoint サーバーの全体管理を使用する構成タスクが含まれます。 また、既存のインストールの更新について個々の手順 ( [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの作成など) をこのトピックで確認することもできます。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Sharepoint 2013 &#124; **注:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sharepoint モードでは、sharepoint Server マルチテナントはサポート**されていません**。|  
  
 既存のファームへの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サーバーの追加については、以下を参照してください。  
  
-   [ファームへのレポート サーバーの追加 &#40;SSRS スケールアウト&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
-   [ファームへの Reporting Services Web フロントエンドの追加](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 シングル サーバー インストールは、開発およびテストのシナリオには便利ですが、運用環境にはお勧めしません。  
  
 **このトピックの内容:**  
  
-   [シングルサーバー配置の例](#bkmk_singleserver)  
  
-   [セットアップアカウント](#bkmk_setupaccounts)  
  
-   [手順 1: Reporting Services レポートサーバーを SharePoint モードでインストールする](#bkmk_install_SSRS)  
  
-   [手順 2: Reporting Services SharePoint サービスを登録して開始する](#bkmk_install_SSRS_sharedservice)  
  
-   [手順 3: Reporting Services サービスアプリケーションを作成する](#bkmk_create_serrviceapplication)  
  
-   [手順 4: Power View サイトコレクション機能をアクティブにします。](#bkmk_powerview)  
  
-   [手順1-4 の Windows PowerShell スクリプト](#bkmk_full_script)  
  
-   [Additional Configuration](#bkmk_additional_config) (サブスクリプションと警告の準備、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンテンツの種類、Analysis Services サーバーを使用するための Excel Services の構成など)  
  
-   [インストールを確認する](#bkmk_verify_installation)  
  
##  <a name="bkmk_singleserver"></a> シングル サーバー配置の例  
 シングル サーバー インストールは、開発およびテストのシナリオには便利ですが、シングル サーバーは運用環境にはお勧めしません。 シングル サーバー環境とは、同じコンピューターに SharePoint と [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] コンポーネントがインストールされた 1 台のコンピューターのことです。 このトピックでは、複数の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サーバーへのスケールアウトについては説明しません。  
  
 次の図は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のシングル サーバー配置に含まれるコンポーネントを示しています。  
  
|||  
|-|-|  
|**(1)**|SharePoint サービス: SQL Server をインストールすると、インストールされます。 1 つ以上の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションを作成することができます。|  
|**(2)**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 製品用アドイン: SharePoint サーバーにユーザー インターフェイス コンポーネントが追加されます。|  
|**(3)**|Power View と PowerPivot で使用される Excel サービス アプリケーション。|  
|**(4)**|PowerPivot サービス アプリケーション。|  
  
 ![SSRS SharePoint モードのシングルサーバー配置](../../../2014/sql-server/install/media/rs-sharepoint-1server-deployment.gif "SSRS SharePoint モードのシングルサーバー配置")  
  
> [!TIP]  
>  より複雑な配置例については、「 [Deployment Topologies for SQL Server BI Features in SharePoint (SharePoint での SQL Server BI 機能の配置トポロジ)](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)」を参照してください。  
  
##  <a name="bkmk_setupaccounts"></a> セットアップ アカウント  
 このセクションでは、SharePoint モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の主な配置手順に使用するアカウントと権限について説明します。  
  
 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスのインストールと登録:**  
  
-   SharePoint モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストール中の現在のアカウント (' セットアップ ' アカウントと呼ばれます) は、ローカルコンピューターの管理者権限を持っている必要があります。 SharePoint のインストール後に [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をインストールし、' セットアップ ' アカウントが SharePoint ファーム管理者グループのメンバーでもある場合は、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストールによって [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスが登録されます。 SharePoint をインストールする前に [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をインストールする場合、または ' セットアップ ' アカウントがファーム管理者グループのメンバーでない場合は、サービスを手動で登録します。 「 [手順 2。 Reporting Services SharePoint サービスの登録と開始](#bkmk_install_SSRS_sharedservice)。  
  
 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの作成:**  
  
-   インストールと [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスの登録の後、1 つ以上の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションを作成します。 Reporting Services サービス アプリケーションを作成できるように、"SharePoint ファーム サービス アカウント" を一時的にローカルの Administrators グループのメンバーにする必要があります。 SharePoint 2013 アカウントのアクセス許可の詳細については、「 [sharepoint 2013 のアカウントのアクセス許可とセキュリティ設定](https://technet.microsoft.com/library/cc678863.aspx)」 (https://technet.microsoft.com/library/cc678863.aspx)を参照してください。  
  
     セキュリティ上、SharePoint ファーム管理者アカウントがローカル オペレーティング システムの管理者アカウントを兼ねないことをお勧めします。 インストール プロセスの一環としてファーム管理者アカウントをローカルの Administrators グループに追加する場合は、インストールの完了後にローカルの Administrators グループからそのアカウントを削除することをお勧めします。  
  
##  <a name="bkmk_install_SSRS"></a> 手順 1. SharePoint モードの Reporting Services レポート サーバーのインストール  
 この手順では、SharePoint モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーと SharePoint 製品用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインをインストールします。 コンピューターに既にインストールされている内容によっては、次の手順で説明するインストール ページの一部は表示されない場合があります。  
  
1.  SQL Server インストール ウィザード (Setup.exe) を実行します。  
  
2.  ウィザードの左側の **[インストール]** をクリックし、 **[SQL Server の新規スタンドアロン インストールを実行するか、既存のインストールに機能を追加します]** をクリックします。  
  
3.  **[セットアップ サポート ルール]** ページで、すべてのルールに合格したら、 **[OK]** をクリックします。  
  
4.  **[セットアップ サポート ファイル]** ページで、 **[インストール]** をクリックします。 コンピューターに既にインストールされている内容によっては、次のメッセージが表示される場合があります。  
  
    -   "影響を受けた 1 つ以上のファイルで操作が保留されています。 セットアップ プロセスが完了した後で、コンピューターを再起動する必要があります。"  
  
    -   **[OK]** をクリックします。  
  
5.  サポート ファイルのインストールが完了し、 **[セットアップ サポート ルール]** ページに **[合格]** というステータスが表示されたら、 **[次へ]** をクリックします。 警告やインストールの障害となる問題を確認します。  
  
6.  **[インストールの種類]** ページで、 **[既存の SQL Server 2014 インスタンスに機能を追加する]** をクリックします。 ドロップダウン リストで適切なインスタンスを選択し、 **[次へ]** をクリックします。  
  
7.  **[プロダクト キー]** ページが表示されたら、キーを入力するか、既定の "Enterprise Evaluation" を受け入れます。  
  
     **[次へ]** をクリックします。  
  
8.  [ライセンス条項] ページが表示されたら、ライセンス条項を確認して同意します。 マイクロソフトでは、機能使用状況に関するデータを送信することに同意して、製品の機能やサポートの改善にご協力いただき感謝しております。  
  
     **[次へ]** をクリックします。  
  
9. **[セットアップ ロール]** ページが表示されたら、 **[SQL Server 機能のインストール]** を選択します。  
  
     **[次へ]** をクリックします。  
  
     ![セットアップロールの SQL Server 機能のインストール](../../../2014/sql-server/install/media/rs-setuprole.gif "セットアップロールの SQL Server 機能のインストール")  
  
10. **[機能の選択]** ページで、次のオプションを選択します。  
  
    -   **Reporting Services - SharePoint**  
  
    -   **SharePoint 製品用 Reporting Services アドイン**。  
  
         ![メモ](../../../2014/reporting-services/media/rs-fyinote.png "note")アドインをインストールするためのインストールウィザードオプションは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] リリースで新しく追加されました。  
  
    -   SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスがまだインストールされていない場合は、 **[データベース エンジン サービス]** および **[管理ツール - 完全]** をクリックして完全な環境をインストールすることもできます。  
  
     **[次へ]** をクリックします。  
  
     ![SharePoint モードの SSRS 機能の選択](../../../2014/sql-server/install/media/rs-setupfeatureselection-sharepoint-with-circles.gif "SharePoint モードの SSRS 機能の選択")  
  
11. **[インストール ルール]** ページが表示されたら、 警告やインストールの障害となる問題を確認します。 続けて、 **[次へ]** をクリックします。  
  
12. データベース エンジン サービスを選択した場合は、 **[インスタンスの構成]** ページで **MSSQLSERVER** の既定のインスタンスを受け入れて、 **[次へ]** をクリックします。  
  
     ![メモ](../../../2014/reporting-services/media/rs-fyinote.png "note")Reporting Services SharePoint サービスアーキテクチャは、以前の Reporting Services アーキテクチャとは異なり、SQL Server の "インスタンス" に基づいていません。  
  
13. **[必要なディスク領域]** ページを確認し、 **[次へ]** をクリックします。  
  
14. **[サーバーの構成]** ページが表示されたら、適切な資格情報を入力します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のデータ警告機能またはサブスクリプション機能を使用する場合は、SQL Server エージェントの **[スタートアップの種類]** を **[自動]** に変更する必要があります。 コンピューターに既にインストールされている内容によっては、 **[サーバーの構成]** ページは表示されない場合があります。  
  
     **[次へ]** をクリックします。  
  
15. データベース エンジン サービスを選択した場合は、 **[データベース エンジンの構成]** ページが表示されるので、SQL 管理者の一覧に適切なアカウントを追加して、 **[次へ]** をクリックします。  
  
16. **[Reporting Services の構成]** ページで、 **[インストールのみ]** オプションをクリックします。 このオプションはレポート サーバー ファイルをインストールするもので、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]用の SharePoint 環境は構成されません。  
  
    > [!NOTE]  
    >  SQL Server のインストールが完了したら、このトピックの他のセクションに従って SharePoint 環境を構成します。 これには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共有サービスのインストールと、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの作成が含まれます。  
  
     ![SQL Server セットアップウィザード-SSRS 構成ページ](../../../2014/sql-server/install/media/rs-2012sp1-setup-ssrs-configpage-with-circles.gif "SQL Server セットアップウィザード-SSRS 構成ページ")  
  
17. **[エラー レポート]** ページでエラー レポートを送信するためのチェック ボックスをオンにすると、マイクロソフトが SQL Server の機能とサービスを改善するのに役立ちます。  
  
     **[次へ]** をクリックします。  
  
18. **[インストール構成ルール]** ページで警告を確認して、 **[次へ]** をクリックします。  
  
19. **[インストールの準備完了]** ページで、インストールの概要を確認して **[次へ]** をクリックします。 概要には、 **SharePointFilesOnlyMode** の値を示す **[Reporting Services SharePoint モード]** 子ノードが含まれます。 **[インストール]** をクリックします。  
  
20. インストールには数分かかります。 機能の一覧と各機能の状態が表示された **[完了]** ページが表示されます。 コンピューターの再起動が必要であることを示す情報ダイアログが表示される場合もあります。  
  
##  <a name="bkmk_install_SSRS_sharedservice"></a> 手順 2。 Reporting Services SharePoint サービスの登録と開始  
 ![PowerShell 関連コンテンツ](../../../2014/reporting-services/media/rs-powershellicon.jpg "PowerShell 関連コンテンツ")  
  
> [!NOTE]  
>  既存の SharePoint ファームにインストールしている場合は、このセクションの手順を実行する必要はありません。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint サービスはインストールされており、このドキュメントの前のセクションの一部として SQL Server インストール ウィザードを実行したときに開始しています。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスを手動で登録する必要がある一般的な理由を次に示します。  
  
-   SharePoint のインストール前に [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モードをインストールした。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モードのインストールに使用したアカウントが SharePoint ファーム管理者グループのメンバーではない。 詳細については、「 [Setup accounts](#bkmk_setupaccounts)」を参照してください。  
  
 必要なファイルは SQL Server インストール ウィザードの中でインストールされていますが、サービスを SharePoint ファームに登録する必要があります。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] リリースでは、SharePoint モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に対する PowerShell が新たにサポートされました。  
  
 以下では、SharePoint 管理シェルを開いてコマンドレットを実行する手順を説明します。  
  
1.  **[スタート]** ボタンをクリックします。  
  
2.  **[Microsoft SharePoint 2013 製品]** グループをクリックします。  
  
3.  **[SharePoint 2013 管理シェル]** を右クリックし、 **[管理者として実行]** をクリックします。 注: SharePoint コマンドは、標準的な Windows PowerShell ウィンドウでは認識されません。 **SharePoint 2013 管理シェル**を使用してください。  
  
4.  次の PowerShell コマンドを実行して、SharePoint サービスをインストールします。 コマンドが正常に完了すると、管理シェルの表示が改行されます。 コマンドが正常に完了しても、管理シェルに**メッセージは表示されません** 。  
  
    ```powershell
    Install-SPRSService  
    ```  
  
    > [!IMPORTANT]  
    >  次のようなエラー メッセージが表示される場合があります。  
    >   
    >  Install-sprsserviceinstall-sprsservice: 用語 ' Install-sprsserviceinstall-sprsservice ' は、次のように**認識されません**。  
    > コマンドレット、関数、スクリプト ファイル、または操作可能なプログラムの名前として認識されません。 名前が正しく記述されていることを確認し、  
    > パスが含まれている場合はそのパスが正しいことを確認してから、  
    > 再試行してください。  
  
5.  次の PowerShell コマンドを実行して、サービス プロキシをインストールします。 コマンドが正常に完了すると、管理シェルの表示が改行されます。 コマンドが正常に完了しても、管理シェルに**メッセージは表示されません** 。  
  
    ```powershell
    Install-SPRSServiceProxy  
    ```  
  
6.  次の PowerShell コマンドを実行してサービスを開始するか、または SharePoint サーバーの全体管理からサービスを開始する方法に関する後の注意事項を参照してください。  
  
    ```powershell
    Get-SPServiceInstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
    ```  
  
 SharePoint 管理シェルではなく Windows Powershell が表示されているか、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モードがインストールされていません。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] と PowerShell の詳細については、「 [Reporting Services SharePoint モード用の PowerShell コマンドレット](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)」をご覧ください。  
  
 3 番目の PowerShell コマンドを実行する代わりに、SharePoint サーバーの全体管理からサービスを開始することもできます。 次の手順を使用すると、サービスが実行していることを確認することもできます。  
  
1.  SharePoint サーバーの全体管理で、 **[システム設定]** の **[サーバーのサービスの管理]** をクリックします。  
  
2.  **[SQL Server Reporting Services サービス]** を探して、[アクション] 列の **[開始]** をクリックします。  
  
3.  Reporting Services サービスのステータスが **[停止]** から **[開始]** に変わります。 Reporting Services サービスが一覧にない場合は、PowerShell を使用してサービスをインストールします。  
  
    > [!NOTE]  
    >  Reporting Services サービスが **[開始中]** ステータスのままで、 **[開始]** に変わらない場合は、Windows サーバー マネージャーで "SharePoint 2013 Administration" サービスが開始されていることを確認します。  
  
##  <a name="bkmk_create_serrviceapplication"></a> 手順 3. Reporting Services サービス アプリケーションの作成  
 ここでは、既存のサービス アプリケーションを確認している場合に、サービス アプリケーションおよびプロパティの説明を作成する手順について説明します。  
  
1.  SharePoint サーバーの全体管理で、 **[アプリケーション構成の管理]** の **[サービス アプリケーションの管理]** をクリックします。  
  
2.  SharePoint リボンで、 **[新規作成]** ボタンをクリックします。  
  
3.  [新規作成] メニューで、 **[SQL Server Reporting Services サービス アプリケーション]** をクリックします。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] オプションが一覧に表示されない場合は、 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共有サービスがインストールされていない**ことを示しています。 前のセクションの、PowerShell コマンドレットを使用して [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスをインストールする方法を確認してください。  
  
4.  **[SQL Server Reporting Services サービス アプリケーションの作成]** ページで、アプリケーションの名前を入力します。 複数の Reporting Services サービス アプリケーションを作成する場合は、わかりやすい名前または名前付け規則を使用すると、管理および運用操作を体系化できます。  
  
5.  **[アプリケーション プール]** セクションで、このアプリケーションのための新しいアプリケーション プールを作成します (推奨)。 新しいアプリケーション プールの名前をサービス アプリケーションと同じにすると、日常の管理が簡単になります。 また、これは、作成するサービス アプリケーションの数や、シングル アプリケーション プールで複数使用する必要があるかどうかによっても影響を受ける場合があります。 アプリケーション プール管理の推奨事項とベスト プラクティスに関する SharePoint Server のドキュメントを参照してください。  
  
     そのアプリケーション プールのセキュリティ アカウントを選択または作成します。 必ずドメイン ユーザー アカウントを指定してください。 ドメイン ユーザー アカウントにより、パスワードやアカウント情報をまとめて更新できる SharePoint の管理アカウント機能を使用できるようになります。 ドメイン アカウントは、配置をスケールアウトして、同じ ID で実行されるサービス インスタンスを追加する場合にも必要です。  
  
6.  **[データベース サーバー]** で、現在のサーバーを使用するか、または別の SQL Server を選択することができます。  
  
7.  **[データベース名]** の既定値は " `ReportingService_<guid>`" で、これは一意のデータベース名です。 新しい値を入力する場合は、一意の値を入力します。 これは、サービス アプリケーションを明確な対象として作成される新しいデータベースです。  
  
8.  **[データベース認証]** の既定値は、"Windows 認証" です。 **[SQL 認証]** を選択する場合は、SharePoint のドキュメントを参照して、SharePoint 配置でその認証の種類を使用するためのベスト プラクティスを確認してください。  
  
9. **[Web アプリケーションの関連付け]** セクションで、現在の Reporting Services サービス アプリケーションによるアクセス用に準備する Web アプリケーションを選択します。 1 つの Reporting Services サービス アプリケーションを 1 つの Web アプリケーションに関連付けることができます。 現在のすべての Web アプリケーションが既に Reporting Services サービス アプリケーションと関連付けられている場合は、警告メッセージが表示されます。  
  
10. クリックして **OK**です。  
  
11. サービス アプリケーションの作成処理には数分かかることがあります。 完了すると、確認メッセージと、 **[サブスクリプションと警告の準備]** ページへのリンクが表示されます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のサブスクリプション機能とデータ警告機能を使用する場合は、準備手順を行います。 詳細については、「[SSRS サービス アプリケーションを使用するためのサブスクリプションと警告の準備](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)」を参照してください。  
  
 ![PowerShell 関連コンテンツ](../../../2014/reporting-services/media/rs-powershellicon.jpg "PowerShell 関連コンテンツ")PowerShell を使用して [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスアプリケーションを作成する方法の詳細については、以下を参照してください。  
  
-   後の「[手順 1 ～ 4 に対応する Windows PowerShell スクリプト](#bkmk_full_script)」セクションをご覧ください。  
  
-   トピック「 [PowerShell を使用して Reporting Services サービス アプリケーションを作成するには](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md#bkmk_powershell_create_ssrs_serviceapp)」。  
  
##  <a name="bkmk_powerview"></a> 手順 4. Power View のサイト コレクション機能のアクティブ化  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint 製品用の [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインの機能であり、サイトコレクション機能です。 この機能は、ルート サイト コレクションと、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインのインストール後に作成されたサイト コレクションで自動的にアクティブ化されます。 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]を使用する場合は、この機能がアクティブ化されていることを確認してください。  
  
 SharePoint Server のインストール後に SharePoint 製品用の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アドインをインストールした場合、レポート サーバーの統合機能と Power View の統合機能はルート サイト コレクションでのみアクティブ化されます。 他のサイト コレクションについては、この機能を手動でアクティブ化します。  
  
#### <a name="to-activate-or-verify-the-power-view-site-collection-feature"></a>Power View のサイト コレクション機能をアクティブ化または確認するには  
  
1.  次の手順は、SharePoint サイトが 2013 の **体験版**用に構成されていることを前提としています。  
  
     ブラウザーで目的の SharePoint サイトを開きます。 たとえば、 http://\<サーバー名>/sites/bi などです。  
  
2.  **[設定]** [![SharePoint の設定](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint の設定")] をクリックします。  
  
3.  **[サイトの設定]** をクリックします。  
  
4.  **[サイト コレクションの管理]** グループで **[サイト コレクションの機能]** をクリックします。  
  
5.  一覧で **[Power View 統合機能]** を探します。  
  
6.  **[アクティブ化]** をクリックします。 機能の状態が **[アクティブ]** に変化します。  
  
 この手順は、サイト コレクションごとに実行します。 詳しくは、「 [SharePoint でのレポート サーバーと Power View の統合機能のアクティブ化](../../../2014/reporting-services/activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)」をご覧ください。  
  
##  <a name="bkmk_full_script"></a>手順1-4 の Windows PowerShell スクリプト  
 このセクション内の PowerShells スクリプトは、前のセクションで手順 1 ～ 4 を実行するときに使用したものと同じです。 このスクリプトは、次の作業を実行します。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスおよびサービス プロキシをインストールし、そのサービスを開始します。  
  
-   "Reporting Services" という名前のサービス プロキシを作成します。  
  
-   "Reporting Services アプリケーション" という名前の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスアプリケーションを作成します。  
  
-   サイト コレクションに対応する [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 機能を有効にします。  
  
 パラメーター  
  
-   サービス プロキシに合わせて **-Account** を更新します。 このアカウントは、SharePoint ファーム内で管理されるサービス アカウントであることが必要です。 詳細については、SharePoint のトピック「 [SharePoint 2013 の管理アカウントとサービス アカウントを計画する](https://technet.microsoft.com/library/cc263445.aspx)」を参照してください。  
  
-   サービス アプリケーションに合わせて **-DatabaseServer** パラメーターを更新します。 このパラメーターは、データベース エンジンのインスタンスを意味します  
  
-   **の機能を有効にするサイトの**-url[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] パラメーターを更新します。  
  
 **スクリプトを使用するには**  
  
1.  管理者特権で Windows PowerShell を開きます。  
  
2.  次のコードをスクリプト ウィンドウにコピーします。  
  
3.  前のセクションで説明した 3 つのパラメーターを更新し、スクリプトを実行します。  
  
```powershell
#This script Configures SQL Server Reporting Services SharePoint mode  
  
$starttime = Get-Date  
Write-Host -foregroundcolor DarkGray StartTime>> $starttime   
  
Write-Host -ForegroundColor Green "Import the SharePoint PowerShell snappin"  
Add-PSSnapin Microsoft.Sharepoint.Powershell -EA 0  
  
Write-Host -ForegroundColor Green "Install SSRS Service and Service Proxy, and start the service"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
  
    Write-Host -ForegroundColor Green "Install the Reporting Services Shared Service"  
    Install-SPRSService  
  
    Write-Host -ForegroundColor Green " Install the Reporting Services Service Proxy"  
    Install-SPRSServiceProxy  
  
    # Get the ID of the RS Service Instance and start the service   
    Write-Host -ForegroundColor Green "Start the Reporting Services Service"  
    $RS = Get-SPServiceInstance | Where {$_.TypeName -eq "SQL Server Reporting Services Service"}  
    Start-SPServiceInstance -Identity $RS.Id.ToString()  
  
    # Wait for the Reporting Services Service to start...  
    $Status = Get-SPServiceInstance $RS.Id.ToString()  
    While ($Status.Status -ne "Online")  
    {  
        Write-Host -ForegroundColor Green "SSRS Service Not Online...Current Status = " $Status.Status  
        Start-Sleep -Seconds 2  
        $Status = Get-SPServiceInstance $RS.Id.ToString()  
    }  
  
$time = Get-Date  
Write-Host -foregroundcolor DarkGray StartTime>> $starttime   
Write-Host -foregroundcolor DarkGray $time  
  
Write-Host -ForegroundColor Green "Create a new application pool and Reporting Services service application"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Write-Host -ForegroundColor Green "Create a new application pool"  
#!!!! update "-Account" with an existing Managed Service Account  
New-SPServiceApplicationPool -Name "Reporting Services" -Account "<domain>\User name>"  
$appPool = Get-SPServiceApplicationPool "Reporting Services"  
  
Write-Host -ForegroundColor Green " Create the Reporting Services Service Application"  
#!!!! Update "-DatabaseServer", an instance of the SQL Server database engine   
$rsService = New-SPRSServiceApplication -Name "Reporting Services Application" -ApplicationPool $appPool -DatabaseName "Reporting_Services_Application" -DatabaseServer "<server name>"  
  
Write-Host -ForegroundColor Green "Create the Reporting Services Service Application Proxy"  
$rsServiceProxy = New-SPRSServiceApplicationProxy -Name "Reporting Services Application Proxy" -ServiceApplication $rsService  
  
Write-Host -ForegroundColor Green "Associate service application proxy to default web site and grant web applications rights to SSRS application pool"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"     
# Associate the Reporting Services Service Applicatoin Proxy to the default web site...  
Get-SPServiceApplicationProxyGroup -default | Add-SPServiceApplicationProxyGroupMember -Member $rsServiceProxy  
  
$time=Get-Date  
Write-Host -foregroundcolor DarkGray StartTime>> $starttime   
Write-Host -foregroundcolor DarkGray $time  
  
Write-Host -ForegroundColor Green "Enable the PowerView and reportserver site features"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
#!!!! update "-url"  of the site where you want the features enabled  
Enable-SPfeature -identity "powerview" -Url http://server/sites/bi  
Enable-SPfeature -identity "reportserver" -Url http://server/sites/bi  
  
####To Verify, you can run the following:  
#Get-SPRSServiceApplication  
#Get-SPServiceApplicationPool | where {$_.name -like "reporting*"}  
#Get-SPRSServiceApplicationProxy
```  
  
##  <a name="bkmk_additional_config"></a> その他の構成  
 このセクションでは、SharePoint のほとんどの配置で重要になる追加の構成手順について説明します。  
  
###  <a name="bkmk_configure_ECS"></a>Excel Services と PowerPivot の構成  
 SharePoint で Excel 2013 ブックの [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] Power View レポートを表示する場合は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーを SharePoint モードで使用するように、ファームの Excel Services アプリケーションを構成する必要があります。 また、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションによって使用されるアプリケーション プールのセキュリティ アカウントは、Analysis Services サーバーの管理者である必要があります。 詳細については、以下をご覧ください。  
  
-   [PowerPivot for SharePoint 2013 インストール](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)の「Analysis Services 統合用に Excel Services を構成する」セクションを参照してください。  
  
-   [Excel Services のデータ モデルの設定を管理する (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780.aspx)。  
  
###  <a name="bkmk_provision_agent"></a> サブスクリプションと警告の準備  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のサブスクリプションとデータ警告の機能を利用するには、SQL Server エージェントの権限の構成が必要になる場合があります。 SQL Server エージェントが実行中であるにもかかわらず、SQL Server エージェントが必要であることを示すエラー メッセージが表示された場合は、権限を更新します。 サービス アプリケーション作成成功ページの **[サブスクリプションと警告の準備]** リンクをクリックして、SQL Server エージェントを準備するための別のページに移動します。 配置がコンピューターの境界をまたいでいる場合は (たとえば、SQL Server データベース インスタンスが異なるコンピューターにある場合)、準備手順を行う必要があります。 詳細については、「 [SSRS サービス アプリケーションを使用するためのサブスクリプションと警告の準備](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)」をご覧ください  
  
### <a name="configure-e-mail-for-ssrs-service-applications"></a>SSRS サービス アプリケーション用電子メールを構成する  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のデータ警告機能は、電子メール メッセージで警告を送信します。 電子メールを送信するには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションを構成して、このサービス アプリケーションの電子メール配信拡張機能を変更しなければならない場合があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サブスクリプション機能の電子メール配信拡張機能を使用する場合は、電子メールの設定が必要です。 詳細については、「[Reporting Services サービス アプリケーションの電子メールの構成 &#40;SharePoint 2010 および SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)」を参照してください。  
  
### <a name="add-reporting-services-content-types-to-content-libraries"></a>コンテンツ ライブラリに Reporting Services のコンテンツの種類を追加する  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、共有データ ソース (.rsds) ファイル、レポート モデル (.smdl)、レポート ビルダーのレポート定義 (.rdl) ファイルを管理する際に使用されるコンテンツの種類が、あらかじめ定義されています。 コンテンツの種類として、 **[レポート ビルダー レポート]** 、 **[レポート モデル]** 、および **[レポート データ ソース]** をライブラリに追加すると、 **[新規作成]** コマンドが有効になり、その種類のドキュメントを新規作成できるようになります。 詳細については、「 [SharePoint 統合モード&#40;&#41;のライブラリ Reporting Services にレポートサーバーコンテンツの種類を追加する](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)」を参照してください。  
  
### <a name="activate-the-report-server-file-sync-feature"></a>レポート サーバー ファイル同期機能をアクティブにする  
 ユーザーがパブリッシュされたレポート アイテムを SharePoint ドキュメント ライブラリに頻繁に直接アップロードする場合は、サイト レベルの **レポート サーバー ファイル同期** 機能が役立ちます。 ファイル同期機能では、レポート サーバー カタログとドキュメント ライブラリのアイテムの同期が、より頻繁に行われます。 詳しくは、「 [SharePoint サーバーの全体管理でレポート サーバーのファイル同期機能をアクティブにする](../../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)」をご覧ください。  
  
##  <a name="bkmk_verify_installation"></a> インストールの確認  
 次に、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の SharePoint モードの配置を確認するための推奨手順と手続きについて説明します。  
  
-   検証トピック「 [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)」の「SharePoint」を参照してください。  
  
-   SharePoint ドキュメント ライブラリ内で、タイトルなどに使用するテキスト ボックスのみを含む基本的な [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポートを作成します。 このレポートには、データ ソースやデータセットは何も含めません。 目標は、レポート ビルダーを開き、基本的なレポートを作成し、そのレポートをプレビューできることの確認です。  
  
     レポートをドキュメント ライブラリに保存し、ライブラリからレポートを実行します。 レポート ビルダーでレポートを作成する方法の詳細については、「[レポート ビルダーの起動 (レポート ビルダー)](https://technet.microsoft.com/library/ms159221.aspx)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services SharePoint モード用の PowerShell コマンドレット](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)   
 [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
 [コンテンツロードマップ: SharePoint Server と SQL SERVER BI  のセットアップと構成](https://technet.microsoft.com/library/dn205112.aspx)  
 [SQL Server 2012  の各エディションがサポートする機能](https://go.microsoft.com/fwlink/?linkid=232473)  
 [Reporting Services の SharePoint サービスとサービス アプリケーション](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md)
