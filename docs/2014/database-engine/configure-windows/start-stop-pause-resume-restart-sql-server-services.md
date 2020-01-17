---
title: データベースエンジン、SQL Server エージェント、または SQL Server Browser サービスを開始、停止、一時停止、再開、再起動する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, start and stop services
- stopping SQL Server Agent
- parameters [SQL Server], startup options
- SQL Server, startup options
- Database Engine [SQL Server], starting and stopping services
- pausing SQL Server
- PowerShell [SQL Server], starting and stopping services
- single-user mode [SQL Server], starting in
- SQL Server Management Studio [SQL Server], starting or stopping services
- stopping SQL Server Browser service
- starting SQL Server Agent
- default instances [SQL Server], starting and stopping
- SQL Server Agent, starting and stopping
- command prompt [SQL Server], starting and stopping SQL Server services
- continuing SQL Server
- starting SQL Server Database Engine
- net stop commands [SQL Server]
- command prompt [SQL Server], SQL Browser service
- Configuration Manager, start and stop services
- resuming SQL Server
- startup options [SQL Server]
- named instances [SQL Server], starting and stopping
- net start commands [SQL Server]
- SQL Server, starting and stopping
- stopping SQL Server
- starting SQL Server Browser service
- SQL Server Database Engine setting startup options
- administering SQL Server, starting and stopping services
- Management Studio [SQL Server], starting or stopping services
ms.assetid: 32660a02-e5a1-411a-9e57-7066ca459df6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 11d146144a05c9185a360b2791f9e162a94ff59a
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797948"
---
# <a name="start-stop-pause-resume-restart-the-database-engine-sql-server-agent-or-sql-server-browser-service"></a>データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動
  このトピックでは、コマンドプロンプト、Configuration Manager、または PowerShell から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../includes/tsql-md.md)]、 **net**コマンドを使用して、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスを開始、停止、一時停止、再開、または再起動する方法について説明します。  
  
-   **作業を開始する準備:**  
  
    -   [これらのサービスの概要](#Services)  
  
    -   [追加情報](#MoreInformation)  
  
    -   [セキュリティ](#Security)  
  
-   **使用の手順:**  
  
    -   [SQL Server 構成マネージャー](#SSCMProcedure)  
  
    -   [SQL Server Management Studio](#SSMSProcedure)  
  
    -   [コマンド プロンプト ウィンドウからの net コマンド](#CommandPrompt)  
  
    -   [Transact-SQL](#TsqlProcedure)  
  
    -   [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Services"></a>[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] サービス、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスの概要  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントは、Windows サービスとして実行される実行可能プログラムです。 Windows サービスとして実行されるプログラムは、コンピューター画面にアクティビティを表示することなく動作を続行できます。  
  
 **[!INCLUDE[ssDE](../../includes/ssde-md.md)] サービス (service)**  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]である実行可能プロセスです。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] は、既定のインスタンス (1 台のコンピューターにつき 1 つのみ) にすることも、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の多数の名前付きインスタンスの 1 つにすることもできます。 コンピューターにインストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを判別するには、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 構成マネージャーを使用します。 既定のインスタンス (インストールした場合) は、 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)** として表示されます。 名前付きインスタンス (インストールした場合) は、 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (<instance_name>)** として表示されます。 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express は **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLEXPRESS)** としてインストールされます。  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス**  
 ジョブおよび警告と呼ばれる管理タスクをスケジュールに従って実行する Windows サービスです。 詳しくは、「 [SQL Server Agent](../../ssms/agent/sql-server-agent.md)」をご覧ください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされている機能の一覧については、「 [SQL Server 2014 の各エディションがサポートする機能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」を参照してください。  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービス**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各種リソースに関する着信要求を受信し、コンピューターにインストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに関するクライアント情報を提供する Windows サービスです。 コンピューターにインストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのインスタンスに対して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスのインスタンスが 1 つ使用されます。  
  
###  <a name="MoreInformation"></a> 追加情報  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] サービスを一時停止すると、新しいユーザーは [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続できなくなりますが、既に接続しているユーザーは接続が切断されるまで処理を続行できます。 ユーザーの処理の完了を待ってからサービスを停止する場合は、一時停止を使用してください。 これにより、ユーザーが実行中のトランザクションを完了できます。 再開すると、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] が再び新しい接続を受け入れられるようになります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを一時停止および再開することはできません。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーおよび [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、次のアイコンを使用してサービスの現在の状態が表示されます。  
  
     **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャー**  
  
    -   サービス名の隣にあるアイコン上の緑色の矢印は、サービスが開始されていることを示します。  
  
    -   サービス名の隣にあるアイコン上の赤い四角形は、サービスが停止していることを示します。  
  
    -   サービス名の隣にあるアイコン上の 2 本の青い縦線は、サービスが一時停止していることを示します。  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)]を再起動すると、サービスが停止したことが赤い四角形によって示された後、サービスが正常に開始されたことが緑色の矢印によって示されます。  
  
     **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
    -   サービス名の隣にある緑色の円形のアイコン上の白い矢印は、サービスが開始されていることを示します。  
  
    -   サービス名の隣にある赤い円形のアイコン上の白い四角形は、サービスが停止していることを示します。  
  
    -   サービス名の隣にある青い円形のアイコン上の 2 本の白い縦線は、サービスが一時停止していることを示します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーまたは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の使用時は、実行できるオプションのみが利用可能になります。 たとえば、サービスが既に開始されている場合、 **[開始]** は利用できません。  
  
-   クラスターで実行中の [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] サービスを管理するには、クラスター アドミニストレーターを使用するのが最適です。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> アクセス許可  
 サービスを開始、停止、一時停止、再開、または再起動できるのは、既定ではローカル管理者グループのメンバーだけです。 管理者以外のユーザーがサービスを管理できるようにする方法については、「 [[HOWTO] Windows Server 2003 でサービスを管理する権利をユーザーに付与する](https://support.microsoft.com/kb/325349)」をご覧ください (Windows の他のバージョンでも処理は同じです)。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドを使用して `SHUTDOWN` を停止するには、 **sysadmin** または **serveradmin** 固定サーバー ロールのメンバーシップが必要です。この権限は譲渡できません。  
  
##  <a name="SSCMProcedure"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーの使用  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-an-instance-of-the-includessdenoversionincludesssdenoversion-mdmd"></a>インスタンスを開始、停止、一時停止、再開、または再起動するには [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  
  
1.  **[スタート]** メニューで、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
2.  **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、 **[はい]** をクリックします。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーの左側のペインで、 **[SQL Server のサービス]** をクリックします。  
  
4.  結果ペインで **[SQL Server (MSSQLServer)]** または名前付きインスタンスを右クリックし、 **[開始]** 、 **[停止]** 、 **[一時停止]** 、 **[再開]** 、または **[再起動]** をクリックします。  
  
5.  **[OK]** をクリックし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを閉じます。  
  
> [!NOTE]  
>  スタートアップ オプションを指定して [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスを開始する方法については、「[サーバーのスタートアップ オプションの構成 &#40;SQL Server 構成マネージャー&#41;](scm-services-configure-server-startup-options.md)」をご覧ください。  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-includessnoversionincludesssnoversion-mdmd-browser-or-an-instance-of-the-includessnoversionincludesssnoversion-mdmd-agent"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのインスタンスを開始、停止、一時停止、再開、または再起動するには  
  
1.  **[スタート]** メニューで、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
2.  **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、 **[はい]** をクリックします。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーの左側のペインで、 **[SQL Server のサービス]** をクリックします。  
  
4.  結果ウィンドウで **[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser]** 、または **[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント (MSSQLServer)]** (名前付きインスタンスの場合には **[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント (<instance_name>)]** ) を右クリックし、 **[開始]** 、 **[停止]** 、 **[一時停止]** 、 **[再開]** 、または **[再起動]** をクリックします。  
  
5.  **[OK]** をクリックし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを閉じます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは一時停止できません。  
  
##  <a name="SSMSProcedure"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio の使用  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-an-instance-of-the-includessdenoversionincludesssdenoversion-mdmd"></a>インスタンスを開始、停止、一時停止、再開、または再起動するには [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続し、開始する [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスを右クリックし、 **[開始]** 、 **[停止]** 、 **[一時停止]** 、 **[再開]** 、または **[再起動]** をクリックします。  
  
     または、[登録済みサーバー] で、開始する [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスを右クリックし、 **[サービス コントロール]** をポイントし、 **[開始]** 、 **[停止]** 、 **[一時停止]** 、 **[再開]** 、または **[再起動]** をクリックします。  
  
2.  **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、 **[はい]** をクリックします。  
  
3.  アクションを実行するかどうかを確認するメッセージが表示されたら、 **[はい]** をクリックします。  
  
#### <a name="to-start-stop-or-restart-the-an-instance-of-the-includessnoversionincludesssnoversion-mdmd-agent"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのインスタンスを開始、停止、または再起動するには  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続し、 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント**を右クリックし、 **[開始]** 、 **[停止]** 、または **[再起動]** をクリックします。  
  
2.  **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、 **[はい]** をクリックします。  
  
3.  アクションを実行するかどうかを確認するメッセージが表示されたら、 **[はい]** をクリックします。  
  
##  <a name="CommandPrompt"></a> コマンド プロンプト ウィンドウからの net コマンドの使用  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]net[!INCLUDE[msCoName](../../includes/msconame-md.md)] コマンドを使用して、 のサービスを開始、停止、または一時停止できます。  
  
###  <a name="dbDefault"></a> 既定のインスタンスを開始するには [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   コマンド プロンプトで、次のいずれかのコマンドを入力します。  
  
     **net start "SQL Server (MSSQLSERVER)"**  
  
     \- または -  
  
     **net start MSSQLSERVER**  
  
###  <a name="dbNamed"></a> 名前付きインスタンスを開始するには [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   コマンド プロンプトで、次のいずれかのコマンドを入力します。 *\<instancename>* は、管理するインスタンスの名前に置き換えます。  
  
     **net start "SQL Server (** *instancename* **)"**  
  
     \- または -  
  
     **net start MSSQL$** *instancename*  
  
###  <a name="dbStartup"></a> スタートアップ オプションを指定して [!INCLUDE[ssDE](../../includes/ssde-md.md)] を開始するには  
  
-   **net start "SQL Server (MSSQLSERVER)"** ステートメントの末尾に、スタートアップ オプションをスペースで区切って追加します。 **net start**を使用して起動するときは、スタートアップ オプションでハイフン (-) の代わりにスラッシュ (/) を使用します。  
  
     **net start "SQL Server (MSSQLSERVER)" /f /m**  
  
     \- または -  
  
     **net start MSSQLSERVER /f /m**  
  
    > [!NOTE]  
    >  スタートアップ オプションの詳細については、「 [データベース エンジン サービスのスタートアップ オプション](database-engine-service-startup-options.md)」をご覧ください。  
  
###  <a name="agDefault"></a> スタートアップ オプションを指定して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   コマンド プロンプトで、次のいずれかのコマンドを入力します。  
  
     **net start "SQL Server Agent (MSSQLSERVER)"**  
  
     \- または -  
  
     **net start SQLSERVERAGENT**  
  
###  <a name="agNamed"></a> スタートアップ オプションを指定して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の名前付きインスタンスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   コマンド プロンプトで、次のいずれかのコマンドを入力します。 *instancename* は、管理するインスタンスの名前に置き換えます。  
  
     **net start "SQL Server Agent(** *instancename* **)"**  
  
     \- または -  
  
     **net start SQLAgent$** *instancename*  
  
 トラブルシューティングのために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを詳細モードで実行する方法については、「 [sqlagent90 アプリケーション](../../tools/sqlagent90-application.md)」をご覧ください。  
  
###  <a name="Browser"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser を開始するには  
  
-   コマンド プロンプトで、次のいずれかのコマンドを入力します。  
  
     **net start "SQL Server Browser"**  
  
     \- または -  
  
     **net start SQLBrowser**  
  
###  <a name="pauseStop"></a> コマンド プロンプト ウィンドウからサービスを一時停止または停止するには  
  
-   サービスを一時停止または停止するには、次のようにコマンドを変更します。  
  
    -   サービスを一時停止するには、 **net start** を **net pause**に置き換えます。  
  
    -   サービスを停止するには、 **net start** を **net stop**に置き換えます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ステートメントを使用して、`SHUTDOWN`を停止できます。  
  
#### <a name="to-stop-the-includessdeincludesssde-mdmd-using-includetsqlincludestsql-mdmd"></a>を使用して [!INCLUDE[ssDE](../../includes/ssde-md.md)] を停止するには [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
-   現在実行中の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントおよびストアド プロシージャが終了するまで待機してから [!INCLUDE[ssDE](../../includes/ssde-md.md)]を停止するには、次のステートメントを実行します。  
  
    ```sql  
    SHUTDOWN;   
    ```  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]を直ちに停止するには、次のステートメントを実行します。  
  
    ```sql  
    SHUTDOWN WITH NOWAIT;   
    ```  
  
 `SHUTDOWN` ステートメントの詳細については、 [「 &#40;transact-sql&#41;のシャットダウン](/sql/t-sql/language-elements/shutdown-transact-sql)」を参照してください。  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
  
#### <a name="to-start-and-stop-includessdeincludesssde-mdmd-services"></a>[!INCLUDE[ssDE](../../includes/ssde-md.md)] サービスを開始および停止するには  
  
1.  コマンド プロンプト ウィンドウで、次のコマンドを実行して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Power Shell を開始します。  
  
    ```ms-dos  
    sqlps  
    ```  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Power Shell コマンド プロンプトで、次のコマンドを実行します。 `computername` は自分のコンピューター名に置き換えます。  
  
    ```powershell  
    # Get a reference to the ManagedComputer class.  
    CD SQLSERVER:\SQL\computername  
    $Wmi = (Get-Item .).ManagedComputer
    ```  
  
3.  停止または開始するサービスを指定します。 以下のいずれかの行を選択してください。 `instancename` は名前付きインスタンスの名前に置き換えます。  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)]の既定のインスタンスへの参照を取得する場合  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['MSSQLSERVER']  
        ```  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)]の名前付きインスタンスへの参照を取得する場合  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['MSSQL$instancename']  
        ```  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンスの [!INCLUDE[ssDE](../../includes/ssde-md.md)]エージェント サービスへの参照を取得する場合  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLSERVERAGENT']  
        ```  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の名前付きインスタンスの [!INCLUDE[ssDE](../../includes/ssde-md.md)]エージェント サービスへの参照を取得する場合  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLAGENT$instancename']  
        ```  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスへの参照を取得する場合  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLBROWSER']  
        ```  
  
4.  例を実行して、選択したサービスを開始し、停止します。  
  
    ```powershell  
    # Display the state of the service.  
    $DfltInstance  
    # Start the service.  
    $DfltInstance.Start();  
    # Wait until the service has time to start.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    # Stop the service.  
    $DfltInstance.Stop();  
    # Wait until the service has time to stop.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    ```  
  
## <a name="see-also"></a>参照  
 [最小構成での SQL Server の起動](start-sql-server-with-minimal-configuration.md)   
 [SQL Server 2014 の各エディションがサポートする機能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
