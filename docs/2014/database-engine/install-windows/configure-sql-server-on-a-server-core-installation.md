---
title: Server Core インストールでの SQL Server の構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- IsHadrEnabled server property
- Server Core Installation [SQL Server]
ms.assetid: ed6e5e94-4b8d-422a-a17e-61b05a4df903
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0c2a82aac84777c0601d234162135f9404184c39
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797909"
---
# <a name="configure-sql-server-on-a-server-core-installation"></a>Server Core インストールでの SQL Server の構成
  このトピックでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SP1 の Server Core インストールで [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] を構成する方法について詳しく説明します。 
  
##  <a name="configure-and-manage-server-core-on-windows-server"></a>Windows Server の Server Core の構成と管理  
 ここでは、Server Core インストールの構成および管理に役立つトピックへのリンクを示します。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の一部の機能は、Server Core モードではサポートされていません。  このような一部の機能は、クライアント コンピューター、または Server Core を実行していない別のサーバーにインストールし、Server Core にインストールされているデータベース エンジン サービスに接続できます。  
  
 Server Core インストールをリモートで構成および管理する方法の詳細については、次のトピックを参照してください。  
  
-   [Windows server 2008 R2: Server Core 展開のベストプラクティス](https://go.microsoft.com/fwlink/?LinkID=245957)(https://go.microsoft.com/fwlink/?LinkID=245957)  
  
-   [Server Core インストールの構成: 概要](https://go.microsoft.com/fwlink/?LinkId=245958)(https://go.microsoft.com/fwlink/?LinkId=245958)  
  
-   [Sconfig.cmd を使用した Windows server 2008 R2 の Server Core インストールの構成](https://go.microsoft.com/fwlink/?LinkId=245959)(https://go.microsoft.com/fwlink/?LinkId=245959)  
  
-   [Windows server 2008 R2 の Server Core インストールを実行しているサーバーへのサーバーロールのインストール: 概要](https://go.microsoft.com/fwlink/?LinkId=245960)(https://go.microsoft.com/fwlink/?LinkId=245960)  
  
-   Windows [server 2008 R2 の Server Core インストールを実行しているサーバーへの Windows 機能のインストール: 概要](https://go.microsoft.com/fwlink/?LinkId=245961)(https://go.microsoft.com/fwlink/?LinkId=245961)  
  
-   [Server Core インストールの管理: 概要](https://go.microsoft.com/fwlink/?LinkId=245962)(https://go.microsoft.com/fwlink/?LinkId=245962)  
  
-   [Server Core インストールの管理](https://go.microsoft.com/fwlink/?LinkId=245963)(https://go.microsoft.com/fwlink/?LinkId=245963)  
  
##  <a name="install-updates"></a>の更新プログラムをインストールする  
 ここでは、Windows Server Core コンピューターに [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の更新プログラムをインストールする方法について説明します。 常に最新のセキュリティ更新プログラムがインストールされた状態になるように、適切なタイミングで最新の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新プログラムを評価してインストールすることをお勧めします。 Windows Server Core コンピューターへの [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインストールの詳細については、「 [Server core への SQL Server 2014 のインストール](install-sql-server-on-server-core.md)」を参照してください。  
  
 製品の更新プログラムをインストールするための 2 つのシナリオを次に示します。  
  
-   [新規インストール時に SQL Server 2014 の更新プログラムをインストールする](#installing-updates-during-a-new-installation) 
  
-   [インストール後に SQL Server 2014 の更新プログラムをインストールする](#installing-updates-after-installation) 
  
### <a name="installing-updates-during-a-new-installation"></a>新規インストール中の更新プログラムのインストール  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップでは、コマンド プロンプトによる Server Core オペレーティング システムへのインストールのみがサポートされています。 詳細については、「[コマンド プロンプトからの SQL Server 2014 のインストール](install-sql-server-from-the-command-prompt.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップでは、メインの製品とそれに適用可能な更新プログラムが同時にインストールされるように、最新の製品の更新プログラムとメインの製品のインストールが統合されています。  
  
 セットアップで最新バージョンの適用可能な更新プログラムが検出されると、ダウンロードが実行されて、現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ プロセスと統合されます。 製品の更新プログラムは、累積更新プログラム、サービス パック、またはサービス パックと累積更新プログラムに取り込むことができます。  
  
 メインの製品のインストールに最新の製品の更新プログラムを含めるには、UpdateEnabled パラメーターと UpdateSource パラメーターを指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ時に製品の更新プログラムを有効にする場合は、次の例を参照してください。  
  
```cmd 
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,Replication /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /UpdateEnabled=True /UpdateSource="<SourcePath>" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
### <a name="installing-updates-after-installation"></a>インストール後の更新プログラムのインストール 
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のインストール済みインスタンスでは、一般配布リリース (GDR) やサービス パック (SP) を含む最新のセキュリティ更新プログラムと重要な更新プログラムを適用することをお勧めします。 個々の累積更新プログラムとセキュリティ更新プログラムは、状況に応じて "必要なときに" に適用する必要があります。 更新プログラムを評価し、必要な場合は適用します。  
  
 コマンド プロンプトで更新プログラムを適用する際に、<package_name> の部分は実際の更新プログラム パッケージの名前に置き換えてください。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 1 つのインスタンスとすべての共有コンポーネントを更新します。 InstanceName パラメーターまたは InstanceID パラメーターを使用してインスタンスを指定できます。  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceName=MyInstance  
    ```  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共有コンポーネントのみを更新します。  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch  
    ```  
  
-   コンピューター上のすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスと、すべての共有コンポーネントを更新します。  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances  
    ```  
  
##  <a name="startstop-sql-server-service"></a>サービスの開始/停止 SQL Server  
 コマンド プロンプトから [sqlservr アプリケーション](../../tools/sqlservr-application.md)を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを起動、停止、一時停止、または続行します。  
  
 また、Net サービスを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを起動および停止することもできます。  
  
## <a name="enable-alwayson-availability-groups"></a>[AlwaysOn 可用性グループを有効にする]  
 AlwaysOn 可用性グループが有効になっていることは、サーバー インスタンスが高可用性ディザスター リカバリー ソリューションとして可用性グループを使用するための前提条件です。 AlwaysOn 可用性グループの管理に関する詳細については、「[AlwaysOn 可用性グループの有効化と無効化 &#40;SQL Server&#41;](../availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)」参照してください。  
  
### <a name="using-sql-server-configuration-manager-remotely"></a>リモートでの SQL Server 構成マネージャーの使用  
 次の手順は、[!INCLUDE[win7](../../includes/win7-md.md)] 以降のクライアント エディションを実行している PC、またはサーバー グラフィック シェルがインストールされている別のサーバー ([!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] の完全インストールやサーバー グラフィック シェル機能を有効にした Windows Server 8 インストールなど) に対して実行してください。  
  
1.  [コンピューターの管理] を開きます。 [コンピューターの管理] を開くには、次のいずれかの操作を行います。  
  
    1.  [!INCLUDE[win7](../../includes/win7-md.md)]、Windows Server 2008、または [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] の場合:  
  
        1.  [スタート] ボタンをクリックし、[すべてのプログラム]、[管理ツール] の順にクリックして、[コンピューターの管理] をクリックします。  
  
        2.  [スタート] ボタンをクリックし、[ファイル名を指定して実行] をクリックして「COMPMGMT.MSC」と入力し、[OK] をクリックします。  
  
    2.  サーバー グラフィック シェルを有効にした Windows 8 の場合:  
  
        1.  マウス ポインターを画面の左下隅に移動し、[スタート] のオーバーレイが表示されたら右クリックします。  
  
        2.  コンテキスト メニューの [コンピューターの管理] をクリックします。  
  
2.  コンソール ツリーで、[コンピューターの管理] を右クリックし、[別のコンピューターへ接続] をクリックします。  
  
3.  [コンピューターの選択] ダイアログ ボックスで、管理する Server Core コンピューターの名前を入力するか、[参照] をクリックして目的のコンピューターを探し、[OK] をクリックします。  
  
4.  コンソール ツリーで、選択した Server Core コンピューターの [コンピューターの管理] の下にある [サービスとアプリケーション] をクリックします。  
  
5.  [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャー] をダブルクリックします。  
  
6.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration manager、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サービスを右クリックして[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](\<インスタンス名 >) ここで、\<インスタンス名 > AlwaysOn を有効にするローカル サーバー インスタンスの名前を指定します可用性グループのプロパティ をクリックします。  
  
7.  [AlwaysOn 高可用性] タブを選択します。  
  
8.  [Windows フェールオーバー クラスター名] フィールドに、ローカル フェールオーバー クラスター ノードの名前が表示されていることを確認します。 このフィールドが空白の場合、現在、このサーバー インスタンスでは AlwaysOn 可用性グループがサポートされていません。 ローカル コンピューターがクラスター ノードではないか、WSFC クラスターがシャットダウンされているか、このエディションの [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では AlwaysOn 可用性グループがサポートされていません。  
  
9. [AlwaysOn 可用性グループを有効にする] チェック ボックスをオンにし、[OK] をクリックします。  
  
10. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーによって変更内容が保存されます。 その後、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを手動で再起動する必要があります。 業務上の要件に合った時間帯を選んで再起動することができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが再起動されると、AlwaysOn が有効になり、IsHadrEnabled サーバー プロパティが 1 に設定されます。  
  
> [!NOTE]
>  -   ターゲット コンピューターに接続するには、適切なユーザー権限を持っているか、そのコンピューターに対する適切な権限が委任されている必要があります。  
> -   管理しているコンピューターの名前は、コンソール ツリーの [コンピューターの管理] の横に、かっこで囲まれて表示されます。  
  
### <a name="using-powershell-cmdlets-to-enable-alwayson-availability-groups"></a>PowerShell コマンドレットを使用して AlwaysOn 可用性グループを有効にする

 PowerShell コマンドレット Enable-SqlAlwaysOn を使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスの AlwaysOn 可用性グループを有効にします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの実行中に AlwaysOn 可用性グループを有効にした場合は、変更を完了するために、データベース エンジン サービスを再起動する必要があります。 -Force パラメーターを指定しない限り、サービスを再起動するかどうかを確認するメッセージが表示されます。キャンセルすると、操作は実行されません。  
  
 このコマンドレットを実行するには、管理者権限が必要です。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスで AlwaysOn 可用性グループを有効にするには、次のいずれかの構文を使用できます。  
  
```  
Enable-SqlAlwaysOn [-Path <string>] [-Credential <PSCredential>] [-Force] [-NoServiceRestart] [-Confirm] [-WhatIf] [<Commom Parameters>]  
```  
  
```  
Enable-SqlAlwaysOn -InputObject <Server> [-Credential <PSCredential>] [-Force] [-NoServiceRestart] [-Confirm] [-WhatIf] [<Commom Parameters>]  
```  
  
```  
Enable-SqlAlwaysOn [-ServerInstance <string>] [-Credential <PSCredential>] [-Force] [-NoServiceRestart] [-Confirm] [-WhatIf] [<Commom Parameters>]  
```  
  
 次の PowerShell コマンドは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス (Machine\Instance) の AlwaysOn 可用性グループを有効にします。  
  
```powershell
Enable-SqlAlwaysOn -Path SQLSERVER:\SQL\Machine\Instance  
```  
  
## <a name="configuring-remote-access-of-sql-server-running-on-server-core"></a>Server Core で実行されている SQL Server のリモートアクセスの構成  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Server Core SP1 で実行している [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] インスタンスのリモート アクセスを構成するには、以下で説明する操作を実行します。  
  
### <a name="enable-remote-connections-on-an-instance-of-sql-server"></a>SQL Server のインスタンスでリモート接続を有効にする 
 リモート接続を有効にするには、SQLCMD.exe をローカルで使用して、Server Core インスタンスに対して次のステートメントを実行します。  
  
-   `EXEC sys.sp_configure N'remote access', N'1'`  
  
     `GO`  
  
-   `RECONFIGURE WITH OVERRIDE`  
  
     `GO`  
  
### <a name="enable-and-start-the-sql-server-browser-service"></a>SQL Server Browser サービスを有効にして開始する  
 Browser サービスは、既定では無効になっています。  Server Core で実行している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで無効になっている場合、このサービスを有効にするには、コマンド プロンプトから次のコマンドを実行します。  
  
 `sc config SQLBROWSER start= auto`  
  
 有効にした後は、コマンド プロンプトから次のコマンドを実行して、サービスを開始します。  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>Windows ファイアウォールで例外を作成する  
 Windows ファイアウォールで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アクセスの例外を作成するには、「[SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」で指定されている手順に従います。  
  
### <a name="enable-tcpip-on-an-instance-of-sql-server"></a>SQL Server のインスタンスで TCP/IP を有効にする
 Server Core 上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対して TCP/IP プロトコルを有効にするには、Windows PowerShell を使用します。 次の手順に従います。  
  
1.  Windows Server 2008 R2 Server Core SP1 を搭載しているコンピューターで、タスク マネージャーを起動します。  
  
2.  **[アプリケーション]** タブで、 **[新しいタスク]** をクリックします。  
  
3.  **[新しいタスクの作成]** ダイアログ ボックスで、 **[開く]** フィールドに **sqlps.exe** と入力して、 **[OK]** をクリックします。 **[Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell]** ウィンドウが開きます。  
  
4.  **[Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell]** ウィンドウで、次のスクリプトを実行して TCP/IP プロトコルを有効にします。  
  
```powershell
$smo = 'Microsoft.SqlServer.Management.Smo.'  
$wmi = new-object ($smo + 'Wmi.ManagedComputer')  
# Enable the TCP protocol on the default instance.  If the instance is named, replace MSSQLSERVER with the instance name in the following line.  
$uri = "ManagedComputer[@Name='" + (get-item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
$Tcp = $wmi.GetSmoObject($uri)  
$Tcp.IsEnabled = $true  
$Tcp.Alter()  
$Tcp  
```  
  
##  <a name="sql-server-profiler"></a>[SQL Server Profiler]  
 リモート コンピューターで、[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を起動し、[ファイル] メニューの [新しいトレース] をクリックすると、[サーバーへの接続] ダイアログ ボックスが表示されます。このダイアログ ボックスでは、Server Core コンピューター上にある接続先の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを指定できます。 詳細については、「 [SQL Server Profiler の起動](../../tools/sql-server-profiler/start-sql-server-profiler.md)」を参照してください。  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]の実行に必要な権限の詳細については、「 [SQL Server Profiler の実行に必要な権限](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)」を参照してください。  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] の詳細については、「[SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)」を参照してください。  
  
##  <a name="sql-server-auditing"></a>SQL Server 監査  
 監査は、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] をリモートで使用して定義できます。 監査を作成して有効にすると、ターゲットがエントリを受け取るようになります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 監査の作成および管理の詳細については、「[SQL Server Audit &#40;データベース エンジン&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)」を参照してください。  
  
##  <a name="sql-servevr-command-prompt-utilities"></a>SQL server のコマンドプロンプトユーティリティ  
 次のコマンド プロンプト ユーティリティを使用すると、Server Core コンピューターでの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 操作のスクリプトを作成できます。 次の表は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に付属する、Server Core 用のコマンド プロンプト ユーティリティの一覧です。  
  
|**Utility**|**説明**|**インストール先**|  
|-----------------|---------------------|----------------------|  
|[bcp ユーティリティ](../../tools/bcp-utility.md)|ユーザー指定の形式で、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスとデータ ファイルとの間でデータをコピーします。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[dtexec ユーティリティ](../../integration-services/packages/dtexec-utility.md)|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを構成および実行します。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[Encrypt](../../integration-services/dtutil-utility.md)|SSIS パッケージを管理します。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[osql ユーティリティ](../../tools/osql-utility.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、システム プロシージャ、およびスクリプト ファイルをコマンド プロンプトで入力できるようになります。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlagent90 アプリケーション](../../tools/sqlagent90-application.md)|コマンド プロンプトから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを開始します。|\<drive>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<*instance_name*>\MSSQL\Binn|  
|[sqlcmd ユーティリティ](../../tools/sqlcmd-utility.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、システム プロシージャ、およびスクリプト ファイルをコマンド プロンプトで入力できるようになります。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[SQLdiag ユーティリティ](../../tools/sqldiag-utility.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] カスタマー サポート サービス用の診断情報を収集します。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlmaint ユーティリティ](../../tools/sqlmaint-utility.md)|以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で作成されたデータベース メンテナンス プランを実行します。|\<drive >: \MSSQL12.\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]MSSQLSERVER\MSSQL\Binn|  
|[sqlps ユーティリティ](../../tools/sqlps-utility.md)|PowerShell コマンドおよびスクリプトを実行します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell プロバイダーおよびコマンドレットの読み込みと登録を行います。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr アプリケーション](../../tools/sqlservr-application.md)|トラブルシューティングを行うために、コマンド プロンプトから [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスを開始および停止します。|\<drive >: \MSSQL12.\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]MSSQLSERVER\MSSQL\Binn|  
  
##  <a name="use-troubleshooting-tools"></a>トラブルシューティング ツールの使用  
 [SQLdiag ユーティリティ](../../tools/sqldiag-utility.md)を使用すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] やその他の種類のサーバーからログ ファイルやデータ ファイルを収集したり、サーバーを一定期間にわたって監視したり、サーバーに関する特定の問題をトラブルシューティングしたりすることができます。 SQLdiag は、マイクロソフト カスタマー サポート サービスによる診断情報収集の高速化と簡素化を目的としたユーティリティです。  
  
 このユーティリティは、「 [SQLdiag ユーティリティ](../../tools/sqldiag-utility.md)」で指定されている構文を使用して、Server Core の管理者のコマンド プロンプトで起動できます。  
  
## <a name="see-also"></a>参照  
 [Server Core  に SQL Server 2014 をインストール](install-sql-server-on-server-core.md)する  
 [インストール方法に関するトピック](../../sql-server/install/installation-how-to-topics.md)  
