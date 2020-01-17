---
title: Server Core インストールの構成
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- IsHadrEnabled server property
- Server Core Installation [SQL Server]
ms.assetid: ed6e5e94-4b8d-422a-a17e-61b05a4df903
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: ce38e546aa77e375d65a9f95f708718d283a53b0
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75251597"
---
# <a name="configure-sql-server-on-a-server-core-installation"></a>Server Core インストールでの SQL Server の構成

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

この記事では、Server Core インストールで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を構成する方法について詳しく説明します。  

##  <a name="BKMK_ConfigureWindows"></a> Windows Server の Server Core の構成と管理  
ここでは、Server Core インストールの構成および管理に役立つ記事へのリンクを示します。  
  
[!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] の一部の機能は、Server Core モードではサポートされていません。  このような一部の機能は、クライアント コンピューター、または Server Core を実行していない別のサーバーにインストールし、Server Core にインストールされているデータベース エンジン サービスに接続できます。  
  
Server Core インストールをリモートで構成および管理する方法について詳しくは、以下の記事をご覧ください。  
  
- [Server Core のインストール](https://technet.microsoft.com/windows-server-docs/get-started/getting-started-with-server-core)  
  
- [Sconfig.cmd を使用して Windows Server 2016 の Server Core インストールを構成する](https://docs.microsoft.com/windows-server/get-started/sconfig-on-ws2016)  
  
- [Server Core サーバーへのサーバーの役割と機能のインストール](https://technet.microsoft.com/library/jj574158(v=ws.11).aspx)
  
- [Server Core インストールの管理: 概要](https://go.microsoft.com/fwlink/?LinkId=245962)  
  
- [Server Core インストールの管理](https://go.microsoft.com/fwlink/?LinkId=245963)
  
##  <a name="BKMK_InstallSQLUpdates"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新プログラムのインストール  
ここでは、Windows Server Core コンピューターに [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] の更新プログラムをインストールする方法について説明します。 常に最新のセキュリティ更新プログラムがインストールされた状態になるように、適切なタイミングで最新の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新プログラムを評価してインストールすることをお勧めします。 Windows Server Core コンピューターへの [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] のインストールの詳細については、「[Server Core への SQL Server のインストール](../../database-engine/install-windows/install-sql-server-on-server-core.md)」を参照してください。  
  
製品の更新プログラムをインストールするための 2 つのシナリオを次に示します。  
  
- [新規インストール時に SQL Server の更新プログラムをインストールする](../../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md#bkmk_NewInstall)  
  
- [既にインストールされている SQL Server の更新プログラムをインストールする](../../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md#bkmk_alreadyInstall)  
  
###  <a name="bkmk_NewInstall"></a> 新規インストール時に [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] の更新プログラムをインストールする  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップでは、コマンド プロンプトによる Server Core オペレーティング システムへのインストールのみがサポートされています。 詳細については、「 [コマンド プロンプトからの SQL Server のインストール](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)」を参照してください。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップでは、メインの製品とそれに適用可能な更新プログラムが同時にインストールされるように、最新の製品の更新プログラムとメインの製品のインストールが統合されています。  
  
セットアップで最新バージョンの適用可能な更新プログラムが検出されると、ダウンロードが実行されて、現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ プロセスと統合されます。 製品の更新プログラムは、累積更新プログラム、サービス パック、またはサービス パックと累積更新プログラムに取り込むことができます。  
  
メインの製品のインストールに最新の製品の更新プログラムを含めるには、UpdateEnabled パラメーターと UpdateSource パラメーターを指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ時に製品の更新プログラムを有効にする場合は、次の例を参照してください。  
  
```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /UpdateEnabled=True /UpdateSource="<SourcePath>" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
###  <a name="bkmk_alreadyInstall"></a> 既にインストールされている [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] の更新プログラムをインストールする  
[!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]のインストール済みインスタンスでは、一般配布リリース (GDR) やサービス パック (SP) を含む最新のセキュリティ更新プログラムと重要な更新プログラムを適用することをお勧めします。 個々の累積更新プログラムとセキュリティ更新プログラムは、状況に応じて "必要なときに" に適用する必要があります。 更新プログラムを評価し、必要な場合は適用します。  
  
コマンド プロンプトで更新プログラムを適用する際に、<package_name> の部分は実際の更新プログラム パッケージの名前に置き換えてください。  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 1 つのインスタンスとすべての共有コンポーネントを更新します。 InstanceName パラメーターまたは InstanceID パラメーターを使用してインスタンスを指定できます。  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceName=MyInstance  
    ```  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共有コンポーネントのみを更新します。  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch  
    ```  
  
- コンピューター上のすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスと、すべての共有コンポーネントを更新します。  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances  
    ```  
  
## <a name="BKMK_StartStopServices"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの開始/停止  
コマンド プロンプトから [sqlservr アプリケーション](../../tools/sqlservr-application.md) を使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを起動、停止、一時停止、または続行します。  
  
また、Net サービスを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを起動および停止することもできます。  
  
## <a name="BKMK_EnableAlwaysON"></a> [AlwaysOn 可用性グループを有効にする]  
AlwaysOn 可用性グループが有効になっていることは、サーバー インスタンスが高可用性ディザスター リカバリー ソリューションとして可用性グループを使用するための前提条件です。 AlwaysOn 可用性グループの管理に関する詳細については、「 [AlwaysOn 可用性グループの有効化と無効化 (SQL Server)](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)」を参照してください。  
  
### <a name="using-includessnoversionincludesssnoversion-mdmd-configuration-manager-remotely"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーをリモートで使用する  
次の手順は、Windows のクライアント エディションを実行している PC、またはサーバー グラフィック シェルがインストールされている Windows Server で実行することを意図しています。  
  
1. **[コンピューターの管理]** を開きます。 **[コンピューターの管理]** を開くには、 **[スタート]** をクリックして、`compmgmt.msc` と入力し、 **[OK]** をクリックします。    
  
2. コンソール ツリーで、 **[コンピューターの管理]** を右クリックし、 **[別のコンピューターへ接続]** をクリックします。  
  
3. **[コンピューターの選択]** ダイアログ ボックスで、管理する Server Core コンピューターの名前を入力するか、 **[参照]** をクリックして目的のコンピューターを探し、 **[OK]** をクリックします。  
  
4. コンソール ツリーで、選択した Server Core コンピューターの **[コンピューターの管理]** の下にある **[サービスとアプリケーション]** をクリックします。  
  
5. **[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャー]** をダブルクリックします。  
  
6. **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャー**で、 **[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のサービス]** をクリックし、 **[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** (\<instance name>)] を右クリックして、[プロパティ] をクリックします。この場合、\<instance name> は、AlwaysOn 可用性グループを有効にするローカル サーバー インスタンスの名前です。  
  
7. **[AlwaysOn 高可用性]** タブを選択します。  
  
8. [Windows フェールオーバー クラスター名] フィールドに、ローカル フェールオーバー クラスター ノードの名前が表示されていることを確認します。 このフィールドが空白の場合、現在、このサーバー インスタンスでは AlwaysOn 可用性グループがサポートされていません。 ローカル コンピューターがクラスター ノードではないか、WSFC クラスターがシャットダウンされているか、このエディションの [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] では AlwaysOn 可用性グループがサポートされていません。  
  
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
  
次の PowerShell コマンドは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス (Machine\Instance) の AlwaysOn 可用性グループを有効にします。  
  
```  
Enable-SqlAlwaysOn -Path SQLSERVER:\SQL\Machine\Instance  
```  
  
##  <a name="BKMK_ConfigureRemoteAccess"></a> Server Core で実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のリモート アクセスの構成  
 Windows Server Core で実行している [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] インスタンスのリモート アクセスを構成するには、以下で説明する操作を実行します。  
  
### <a name="enable-remote-connections-on-the-instance-of-includessnoversionincludesssnoversion-mdmd"></a>のインスタンスでリモート接続を有効にする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 リモート接続を有効にするには、SQLCMD.exe をローカルで使用して、Server Core インスタンスに対して次のステートメントを実行します。  
  
-   `EXEC sys.sp_configure N'remote access', N'1'`  
  
     `GO`  
  
-   `RECONFIGURE WITH OVERRIDE`  
  
     `GO`  
  
### <a name="enable-and-start-the-includessnoversionincludesssnoversion-mdmd-browser-service"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスを有効にして開始する  
 Browser サービスは、既定では無効になっています。  Server Core で実行している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで無効になっている場合、このサービスを有効にするには、コマンド プロンプトから次のコマンドを実行します。  
  
 `sc config SQLBROWSER start= auto`  
  
 有効にした後は、コマンド プロンプトから次のコマンドを実行して、サービスを開始します。  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>Windows ファイアウォールで例外を作成する  
 Windows ファイアウォールで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アクセスの例外を作成するには、「 [SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」で指定されている手順に従います。  
  
### <a name="enable-tcpip-on-the-instance-of-includessnoversionincludesssnoversion-mdmd"></a>のインスタンスで TCP/IP を有効にする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Server Core 上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対して TCP/IP プロトコルを有効にするには、Windows PowerShell を使用します。 次の手順に従います。  
  
1.  Windows Server Core を実行しているコンピューターで、**タスク マネージャー**を起動します。  
  
2.  **[アプリケーション]** タブで、 **[新しいタスク]** をクリックします。  
  
3.  **[新しいタスクの作成]** ダイアログ ボックスで、 **[開く]** フィールドに **sqlps.exe** と入力して、 **[OK]** をクリックします。 **[Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell]** ウィンドウが開きます。  
  
4.  **[Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell]** ウィンドウで、次のスクリプトを実行して TCP/IP プロトコルを有効にします。  
  
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
  
##  <a name="BKMK_Profiler"></a> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロファイラー  
 リモート コンピューターで、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を起動し、[ファイル] メニューの [新しいトレース] をクリックすると、[サーバーへの接続] ダイアログ ボックスが表示されます。このダイアログ ボックスでは、Server Core コンピューター上にある接続先の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを指定できます。 詳細については、「 [SQL Server Profiler の起動](../../tools/sql-server-profiler/start-sql-server-profiler.md)」を参照してください。  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]の実行に必要な権限の詳細については、「 [SQL Server Profiler の実行に必要な権限](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)」を参照してください。  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]の詳細については、「 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)」を参照してください。  
  
##  <a name="BKMK_Auditing"></a> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 監査  
 監査は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] をリモートで使用して定義できます。 監査を作成して有効にすると、ターゲットがエントリを受け取るようになります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 監査の作成および管理の詳細については、「[SQL Server Audit &#40;データベース エンジン&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)」を参照してください。  
  
##  <a name="BKMK_CMD"></a> コマンド プロンプト ユーティリティ  
 次のコマンド プロンプト ユーティリティを使用すると、Server Core コンピューターでの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 操作のスクリプトを作成できます。 次の表は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に付属する、Server Core 用のコマンド プロンプト ユーティリティの一覧です。  
  
|**Utility**|**説明**|**インストール先**|  
|-----------------|---------------------|----------------------|  
|[bcp ユーティリティ](../../tools/bcp-utility.md)|ユーザー指定の形式で、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスとデータ ファイルとの間でデータをコピーします。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[dtexec ユーティリティ](../../integration-services/packages/dtexec-utility.md)|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを構成および実行します。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[dtutil ユーティリティ](../../integration-services/dtutil-utility.md)|SSIS パッケージを管理します。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[osql ユーティリティ](../../tools/osql-utility.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、システム プロシージャ、およびスクリプト ファイルをコマンド プロンプトで入力できるようになります。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlagent90 アプリケーション](../../tools/sqlagent90-application.md)|コマンド プロンプトから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを開始します。|\<drive>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<*instance_name*>\MSSQL\Binn|  
|[sqlcmd Utility](../../tools/sqlcmd-utility.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、システム プロシージャ、およびスクリプト ファイルをコマンド プロンプトで入力できるようになります。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[SQLdiag ユーティリティ](../../tools/sqldiag-utility.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] カスタマー サポート サービス用の診断情報を収集します。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlmaint ユーティリティ](../../tools/sqlmaint-utility.md)|以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で作成されたデータベース メンテナンス プランを実行します。|\<drive>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL14.MSSQLSERVER\MSSQL\Binn|  
|[sqlps ユーティリティ](../../tools/sqlps-utility.md)|PowerShell コマンドおよびスクリプトを実行します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell プロバイダーおよびコマンドレットの読み込みと登録を行います。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr アプリケーション](../../tools/sqlservr-application.md)|トラブルシューティングを行うために、コマンド プロンプトから [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスを開始および停止します。|\<drive>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL14.MSSQLSERVER\MSSQL\Binn|  
  
##  <a name="BKMK_troubleshoot"></a> トラブルシューティング ツールの使用  
 [SQLdiag ユーティリティ](../../tools/sqldiag-utility.md) を使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] やその他の種類のサーバーからログ ファイルやデータ ファイルを収集したり、サーバーを一定期間にわたって監視したり、サーバーに関する特定の問題をトラブルシューティングしたりすることができます。 SQLdiag は、マイクロソフト カスタマー サポート サービスによる診断情報収集の高速化と簡素化を目的としたユーティリティです。  
  
 このユーティリティは、「[SQLdiag ユーティリティ](../../tools/sqldiag-utility.md)」で指定されている構文を使って、Server Core の管理者のコマンド プロンプトで起動できます。  
  
## <a name="see-also"></a>参照  
 [Server Core への SQL Server のインストール](../../database-engine/install-windows/install-sql-server-on-server-core.md)   
 [インストール方法に関する記事](https://msdn.microsoft.com/library/59de41e7-557f-462a-8914-53ec35496baa)  
  
  
