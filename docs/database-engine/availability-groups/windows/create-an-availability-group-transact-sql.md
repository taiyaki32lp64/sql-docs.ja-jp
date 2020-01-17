---
title: Transact-SQL を使用した可用性グループの作成 (T-SQL)
description: 'Transact-SQL (T-SQL) を使用して Always On 可用性グループを作成する手順です。 '
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], creating
ms.assetid: 8b0a6301-8b79-4415-b608-b40876f30066
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1a9f888f651a7c5471014b151d60b0ad3844578b
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252975"
---
# <a name="create-an-always-on-availability-group-using-transact-sql-t-sql"></a>Transact-SQL (T-SQL) を使用した Always On 可用性グループの作成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 機能を有効にする [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] のインスタンス上で可用性グループを作成および構成するために [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] を使用する方法について説明します。 *可用性グループ* は、1 つのまとまりとしてフェールオーバーする一連のユーザー データベースと、フェールオーバーをサポートする一連のフェールオーバー パートナー ( *可用性レプリカ*) を定義します。  
  
> [!NOTE]  
>  可用性グループの概要については、「 [Always On 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)の Always On 可用性グループを PowerShell コマンドレットで作成および構成する方法について説明します。  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../../includes/tsql-md.md)]の代わりに、可用性グループの作成ウィザードまたは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell コマンドレットを使用する方法もあります。 詳細については、「 [可用性グループ ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)」、「 [[新しい可用性グループ] ダイアログ ボックスの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)」、または「 [可用性グループの作成 &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)」を参照してください。  

  
## <a name="PrerequisitesRestrictions"></a> 前提条件、制限事項、および推奨事項  
  
-   可用性グループを作成する前に、可用性レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスが同じ Windows Server フェールオーバー クラスタリング (WSFC) フェールオーバー クラスター内の別の WSFC ノードに存在していることを確認します。 また、各サーバー インスタンスが [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の他のすべての前提条件を満たしていることも確認します。 詳細については、「[Always On 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」を参照することを強くお勧めします。  
  
  
##  <a name="Permissions"></a> Permissions  
 **sysadmin** 固定サーバー ロールのメンバーシップと、CREATE AVAILABILITY GROUP サーバー権限、ALTER ANY AVAILABILITY GROUP 権限、CONTROL SERVER 権限のいずれかが必要です。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL を使用した可用性グループの作成と構成 

###  <a name="SummaryTsqlStatements"></a> 作業の概要および対応する Transact-SQL ステートメント  
 次の表は、可用性グループの作成と構成に伴う基本的な作業と、これらの作業に使用する [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントの一覧です。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] に関連したこれらの作業は、この表に示されている順に実行する必要があります。  
  
|タスク|Transact-SQL ステートメント|作業の実行場所 **&#42;**|  
|----------|----------------------------------|---------------------------------|  
|データベース ミラーリング エンドポイントを作成する ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスごとに 1 回)|[CREATE ENDPOINT](../../../t-sql/statements/create-endpoint-transact-sql.md) *endpointName* ...FOR DATABASE_MIRRORING|データベース ミラーリング エンドポイントが欠落している各サーバー インスタンスで実行します。|  
|可用性グループを作成する|[CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md)|初期プライマリ レプリカをホストするサーバー インスタンスで実行します。|  
|セカンダリ レプリカを可用性グループに参加させる|[ALTER AVAILABILITY GROUP](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md) *group_name* JOIN|セカンダリ レプリカをホストする各サーバー インスタンスで実行します。|  
|セカンダリ データベースを準備する|[BACKUP](../../../t-sql/statements/backup-transact-sql.md) および [RESTORE](../../../t-sql/statements/restore-statements-transact-sql.md)|プライマリ レプリカをホストするサーバー インスタンスでバックアップを作成します。<br /><br /> セカンダリ レプリカをホストする各サーバー インスタンス上で、RESTORE WITH NORECOVERY を使用してバックアップを復元します。|  
|各セカンダリ データベースを可用性グループに参加させてデータ同期を開始する|[ALTER DATABASE](../../../t-sql/statements/alter-database-transact-sql-set-hadr.md) *database_name* SET HADR AVAILABILITY GROUP = *group_name*|セカンダリ レプリカをホストする各サーバー インスタンスで実行します。|  
  
 *ここに記載されたサーバー インスタンスに接続して作業を実行します。   
 
### <a name="using-transact-sql"></a>Transact-SQL の使用 
> [!NOTE]  
>  これらの各 [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントのコード例が使用された構成手順の例については、「[例:Windows 認証を使用した可用性グループの構成](#ExampleConfigAGWinAuth)」を参照してください。  
  
1.  プライマリ レプリカをホストするサーバー インスタンスに接続します。  
  
2.  可用性グループは、[CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md) という [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを使用して作成します。  
  
3.  新しいセカンダリ レプリカを可用性グループに参加させます。 詳細については、「 [可用性グループへのセカンダリ レプリカの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)、または PowerShell を使用して、既存の AlwaysOn 可用性グループにセカンダリ レプリカを追加する方法について説明します。  
  
4.  可用性グループ内の各データベースについて、セカンダリ データベースを作成します。これは、プライマリ データベースの最新のバックアップを、RESTORE WITH NORECOVERY で復元することによって行います。 詳細については、「[例:Windows 認証を使用した可用性グループの構成 (Transact-SQL)](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)」で、データベース バックアップの復元手順をまず参照してください。  
  
5.  新しいセカンダリ データベースをすべて可用性グループに参加させます。 詳細については、「 [可用性グループへのセカンダリ レプリカの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)、または PowerShell を使用して、既存の AlwaysOn 可用性グループにセカンダリ レプリカを追加する方法について説明します。  
  
##  <a name="ExampleConfigAGWinAuth"></a> 例: Windows 認証を使用した可用性グループの構成  
 この例では、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 構成プロシージャのサンプルを作成します。サンプルでは、Windows 認証を使用するデータベース ミラーリング エンドポイントのセットアップ、さらには、可用性グループとそのセカンダリ データベースの作成と構成を [!INCLUDE[tsql](../../../includes/tsql-md.md)] を使用して行います。  
  
 この例の内容は次のとおりです。  
  
-   [サンプル構成プロシージャを使用するうえでの前提条件](#PrerequisitesForExample)  
  
-   [サンプル構成プロシージャ](#SampleProcedure)  
  
-   [サンプル構成プロシージャの完全なコード例](#CompleteCodeExample)  
  
###  <a name="PrerequisitesForExample"></a> サンプル構成プロシージャを使用するうえでの前提条件  
 このサンプル プロシージャには、次の要件があります。  
  
-   サーバー インスタンスは [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]をサポートしている必要があります。 詳細については、「 [Always On 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)の構成に関する一般的な問題のトラブルシューティングに役立つ情報を提供します。  
  
-   2 つのサンプル データベース ( *MyDb1* および *MyDb2*) が、プライマリ レプリカをホストするサーバー インスタンス上に存在する必要があります。 次のコード例では、これらの 2 つのデータベースを作成、構成し、それぞれの完全バックアップを作成します。 これらのコード例は、サンプルの可用性グループの作成先となるサーバー インスタンス上で実行します。 サンプル可用性グループの初期プライマリ レプリカは、このサーバー インスタンスでホストされます。  
  
    1.  次の例の [!INCLUDE[tsql](../../../includes/tsql-md.md)] では、これらのデータベースを作成し、完全復旧モデルを使用するように変更を加えています。  
  
        ```  
        -- Create sample databases:  
        CREATE DATABASE MyDb1;  
        GO  
        ALTER DATABASE MyDb1 SET RECOVERY FULL;  
        GO  
  
        CREATE DATABASE MyDb2;  
        GO  
        ALTER DATABASE MyDb2 SET RECOVERY FULL;  
        GO  
        ```  
  
    2.  次のコード例では、 *MyDb1* および *MyDb2*データベースの完全バックアップを作成します。 このコード例では、架空のバックアップ共有 \\\\*FILESERVER*\\*SQLbackups*を使用します。  
  
        ```  
        -- Backup sample databases:  
        BACKUP DATABASE MyDb1   
        TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
            WITH FORMAT  
        GO  
  
        BACKUP DATABASE MyDb2   
        TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
            WITH FORMAT  
        GO  
  
        ```  
  
 [&#91;TopOfExample&#93;](#ExampleConfigAGWinAuth)  
  
###  <a name="SampleProcedure"></a> サンプル構成プロシージャ  
 このサンプル構成では、信頼関係のある異なるドメイン (`DOMAIN1` と `DOMAIN2`) の下でサービス アカウントが実行される 2 つのスタンドアロン サーバー インスタンスに可用性レプリカを作成します。  
  
 次の表は、このサンプル構成で使用する値をまとめたものです。  
  
|初期ロール|システム|ホスト [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス|  
|------------------|------------|---------------------------------------------|  
|プライマリ|`COMPUTER01`|`AgHostInstance`|  
|セカンダリ|`COMPUTER02`|既定のインスタンス|  
  
1.  可用性グループの作成先となるサーバー インスタンス ( *上の* という名前のインスタンス) 上に、 `AgHostInstance` dbm_endpoint `COMPUTER01`という名前のデータベース ミラーリング エンドポイントを作成します。 このエンドポイントはポート 7022 を使用します。 可用性グループの作成先となるサーバー インスタンスには、プライマリ レプリカがホストされることに注意してください。  
  
    ```  
    -- Create endpoint on server instance that hosts the primary replica:  
    CREATE ENDPOINT dbm_endpoint  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO  
  
    ```  
  
2.  セカンダリ レプリカをホストするサーバー インスタンス ( *上の既定のサーバー インスタンス) 上にエンドポイント* dbm_endpoint `COMPUTER02`を作成します。 このエンドポイントはポート 5022 を使用します。  
  
    ```  
    -- Create endpoint on server instance that hosts the secondary replica:   
    CREATE ENDPOINT dbm_endpoint  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=5022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO  
  
    ```  
  
3.  > [!NOTE]  
    >  可用性レプリカをホストするサーバー インスタンスのサービス アカウントが同じドメイン アカウントで実行されている場合、この手順は不要です。 省略して次の手順に進んでください。  
  
     2 つのサーバー インスタンスのサービス アカウントが、互いに異なるドメイン ユーザーで実行されている場合、それぞれのサーバー インスタンス上に、相手のサーバー インスタンス用のログインを作成し、このログイン権限に、ローカルのデータベース ミラーリング エンドポイントのアクセス権を付与します。  
  
     ログインを作成し、エンドポイントの権限を付与するための [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントのコード例を次に示します。 ここでは、リモート サーバー インスタンスのドメイン アカウントを *domain_name*\\*user_name*としています。  
  
    ```  
    -- If necessary, create a login for the service account, domain_name\user_name  
    -- of the server instance that will host the other replica:  
    USE master;  
    GO  
    CREATE LOGIN [domain_name\user_name] FROM WINDOWS;  
    GO  
    -- And Grant this login connect permissions on the endpoint:  
    GRANT CONNECT ON ENDPOINT::dbm_endpoint   
       TO [domain_name\user_name];  
    GO  
    ```  
  
4.  ユーザー データベースが存在するサーバー インスタンス上に、可用性グループを作成します。  
  
     次のコード例では、サンプル データベースの *MyDb1* と *MyDb2* を作成したサーバー インスタンス上に、 *MyAG*という名前の可用性グループを作成しています。 最初に、 `AgHostInstance`COMPUTER01 *上のローカル サーバー インスタンス (* ) が指定されています。 初期プライマリ レプリカは、このインスタンスによってホストされます。 リモート サーバー インスタンス ( *COMPUTER02*上の既定のサーバー インスタンス) は、セカンダリ レプリカをホストするように指定されています。 どちらの可用性レプリカも、非同期コミット モードと手動フェールオーバーを使用するように構成します (非同期コミットのレプリカでは、手動フェールオーバーは、データ損失の可能性を伴う強制フェールオーバーを意味します)。  
  
    ```  
  
              -- Create the availability group, MyAG:   
    CREATE AVAILABILITY GROUP MyAG   
       FOR   
          DATABASE MyDB1, MyDB2   
       REPLICA ON   
          'COMPUTER01\AgHostInstance' WITH   
             (  
             ENDPOINT_URL = 'TCP://COMPUTER01.Adventure-Works.com:7022',   
             AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
             FAILOVER_MODE = MANUAL  
             ),  
          'COMPUTER02' WITH   
             (  
             ENDPOINT_URL = 'TCP://COMPUTER02.Adventure-Works.com:5022',  
             AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
             FAILOVER_MODE = MANUAL  
             );   
    GO  
    ```  
  
     可用性グループを作成するための他の [!INCLUDE[tsql](../../../includes/tsql-md.md)] コード例については、「[CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)」を参照してください。  
  
5.  セカンダリ レプリカをホストするサーバー インスタンス上で、セカンダリ レプリカを可用性グループに参加させます。  
  
     次のコード例では、 `COMPUTER02` 上のセカンダリ レプリカを `MyAG` 可用性グループに参加させています。  
  
    ```  
    -- On the server instance that hosts the secondary replica,   
    -- join the secondary replica to the availability group:  
    ALTER AVAILABILITY GROUP MyAG JOIN;  
    GO  
    ```  
  
6.  セカンダリ レプリカをホストするサーバー インスタンス上でセカンダリ データベースを作成します。  
  
     次のコード例では、RESTORE WITH NORECOVERY でデータベース バックアップを復元することによって、 *MyDb1* と *MyDb2* のセカンダリ データベースを作成しています。  
  
    ```  
    -- On the server instance that hosts the secondary replica,   
    -- Restore database backups using the WITH NORECOVERY option:  
    RESTORE DATABASE MyDb1   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
        WITH NORECOVERY  
    GO  
  
    RESTORE DATABASE MyDb2   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
        WITH NORECOVERY  
    GO  
  
    ```  
  
7.  プライマリ レプリカをホストするサーバー インスタンス上で、各プライマリ データベースのトランザクション ログをバックアップします。  
  
    > [!IMPORTANT]  
    >  実際に可用性グループを構成する際は、このログのバックアップを作成する前に、まず対応するセカンダリ データベースを可用性グループに参加させ、それが済んでからプライマリ データベースのログ バックアップ作業を行うことをお勧めします。  
  
     次のコード例では、MyDb1 および MyDb2 のトランザクション ログのバックアップを作成します。  
  
    ```  
    -- On the server instance that hosts the primary replica,   
    -- Backup the transaction log on each primary database:  
    BACKUP LOG MyDb1   
    TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
        WITH NOFORMAT  
    GO  
  
    BACKUP LOG MyDb2   
    TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
        WITHNOFORMAT  
    GO  
  
    ```  
  
    > [!TIP]  
    >  通常、ログ バックアップは各プライマリ データベースで作成した後、対応するセカンダリ データベースで (WITH NORECOVERY を使用して) 復元する必要があります。 ただし、データベースを作成したばかりでこのログ バックアップがまだ作成されていない場合や、復旧モデルを SIMPLE から FULL に変更したばかりの場合など、ログ バックアップが不要な場合もあります。  
  
8.  セカンダリ レプリカをホストするサーバー インスタンス上で、セカンダリ データベースにログ バックアップを適用します。  
  
     次のコード例では、RESTORE WITH NORECOVERY でデータベース バックアップを復元することによって、 *MyDb1* と *MyDb2* のセカンダリ データベースにバックアップを適用しています。  
  
    > [!IMPORTANT]  
    >  実際のセカンダリ データベースを準備する際は、セカンダリ データベースの作成元となったデータベース バックアップの後に作成されたすべてのログ バックアップを適用する必要があります。その際には古いものから順に適用し、毎回 WITH NORECOVERY を使用します。 当然、完全と差分の両方のデータベース バックアップを復元する場合は、差分バックアップ以降に作成されたログ バックアップを適用するだけでかまいません。  
  
    ```  
    -- Restore the transaction log on each secondary database,  
    -- using the WITH NORECOVERY option:  
    RESTORE LOG MyDb1   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
        WITH FILE=1, NORECOVERY  
    GO  
    RESTORE LOG MyDb2   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
        WITH FILE=1, NORECOVERY  
    GO  
    ```  
  
9. セカンダリ レプリカをホストするサーバー インスタンス上で、新しいセカンダリ データベースを可用性グループに参加させます。  
  
     次のコード例では、 *MyDb1* のセカンダリ データベースと *MyDb2* のセカンダリ データベースを順に *MyAG* 可用性グループに参加させています。  
  
    ```  
    -- On the server instance that hosts the secondary replica,   
    -- join each secondary database to the availability group:  
    ALTER DATABASE MyDb1 SET HADR AVAILABILITY GROUP = MyAG;  
    GO  
  
    ALTER DATABASE MyDb2 SET HADR AVAILABILITY GROUP = MyAG;  
    GO  
  
    ```  
  
###  <a name="CompleteCodeExample"></a> サンプル構成プロシージャの完全なコード例  
 以下のコードは、すべての手順のコード例を総合したサンプル構成プロシージャの全体像です。 このコード例で使用されているプレースホルダーの値については次の表にまとめました。 このコード例の手順の詳細については、このトピックの「 [サンプル構成プロシージャを使用するうえでの前提条件](#PrerequisitesForExample) 」および「 [サンプル構成プロシージャ](#SampleProcedure)」を参照してください。  
  
|プレースホルダー|[説明]|  
|-----------------|-----------------|  
|\\\\*FILESERVER*\\*SQLbackups*|架空のバックアップ共有。|  
|\\\\*FILESERVER*\\*SQLbackups\MyDb1.bak*|MyDb1 のバックアップ ファイル。|  
|\\\\*FILESERVER*\\*SQLbackups\MyDb2.bak*|MyDb2 のバックアップ ファイル。|  
|*7022*|各データベース ミラーリング エンドポイントに割り当てられたポート番号。|  
|*COMPUTER01\AgHostInstance*|初期プライマリ レプリカをホストするサーバー インスタンス。|  
|*COMPUTER02*|初期セカンダリ レプリカをホストするサーバー インスタンス。 これは、 `COMPUTER02`上の既定のサーバー インスタンスです。|  
|*上の*|各データベース ミラーリング エンドポイントに指定した名前。|  
|*MyDb1*|サンプルの可用性グループの名前。|  
|*MyDb1*|1 つ目のサンプル データベースの名前。|  
|*MyDb2*|2 つ目のサンプル データベースの名前。|  
|*DOMAIN1\user1*|初期プライマリ レプリカをホストするサーバー インスタンスのサービス アカウント。|  
|*DOMAIN2\user2*|初期セカンダリ レプリカをホストするサーバー インスタンスのサービス アカウント。|  
|TCP://*COMPUTER01.Adventure-Works.com*:*7022*|COMPUTER01 上の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の AgHostInstance インスタンスのエンドポイント URL。|  
|TCP://*COMPUTER02.Adventure-Works.com*:*5022*|COMPUTER02 上の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の既定のインスタンスのエンドポイント URL。|  
  
> [!NOTE]  
>  可用性グループを作成するための他の [!INCLUDE[tsql](../../../includes/tsql-md.md)] コード例については、「[CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)」を参照してください。  
  
```  
-- on the server instance that will host the primary replica,   
-- create sample databases:  
CREATE DATABASE MyDb1;  
GO  
ALTER DATABASE MyDb1 SET RECOVERY FULL;  
GO  
  
CREATE DATABASE MyDb2;  
GO  
ALTER DATABASE MyDb2 SET RECOVERY FULL;  
GO  
  
-- Backup sample databases:  
BACKUP DATABASE MyDb1   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH FORMAT  
GO  
  
BACKUP DATABASE MyDb2   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITH FORMAT  
GO  
  
-- Create the endpoint on the server instance that will host the primary replica:  
CREATE ENDPOINT dbm_endpoint  
    STATE=STARTED   
    AS TCP (LISTENER_PORT=7022)   
    FOR DATABASE_MIRRORING (ROLE=ALL)  
GO  
  
-- Create the endpoint on the server instance that will host the secondary replica:   
CREATE ENDPOINT dbm_endpoint  
    STATE=STARTED   
    AS TCP (LISTENER_PORT=7022)   
    FOR DATABASE_MIRRORING (ROLE=ALL)  
GO  
  
-- If both service accounts run under the same domain account, skip this step. Otherwise,   
-- On the server instance that will host the primary replica,   
-- create a login for the service account   
-- of the server instance that will host the secondary replica, DOMAIN2\user2,   
-- and grant this login connect permissions on the endpoint:  
USE master;  
GO  
CREATE LOGIN [DOMAIN2\user2] FROM WINDOWS;  
GO  
GRANT CONNECT ON ENDPOINT::dbm_endpoint   
   TO [DOMAIN2\user2];  
GO  
  
-- If both service accounts run under the same domain account, skip this step. Otherwise,   
-- On the server instance that will host the secondary replica,  
-- create a login for the service account   
-- of the server instance that will host the primary replica, DOMAIN1\user1,   
-- and grant this login connect permissions on the endpoint:  
USE master;  
GO  
  
CREATE LOGIN [DOMAIN1\user1] FROM WINDOWS;  
GO  
GRANT CONNECT ON ENDPOINT::dbm_endpoint   
   TO [DOMAIN1\user1];  
GO  
  
-- On the server instance that will host the primary replica,   
-- create the availability group, MyAG:  
CREATE AVAILABILITY GROUP MyAG   
   FOR   
      DATABASE MyDB1, MyDB2   
   REPLICA ON   
      'COMPUTER01\AgHostInstance' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER01.Adventure-Works.com:7022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC  
         ),  
      'COMPUTER02' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER02.Adventure-Works.com:7022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC  
         );   
GO  
  
-- On the server instance that hosts the secondary replica,   
-- join the secondary replica to the availability group:  
ALTER AVAILABILITY GROUP MyAG JOIN;  
GO  
  
-- Restore database backups onto this server instance, using RESTORE WITH NORECOVERY:  
RESTORE DATABASE MyDb1   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH NORECOVERY  
GO  
  
RESTORE DATABASE MyDb2   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITH NORECOVERY  
GO  
  
-- Back up the transaction log on each primary database:  
BACKUP LOG MyDb1   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH NOFORMAT  
GO  
  
BACKUP LOG MyDb2   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITHNOFORMAT  
GO  
  
-- Restore the transaction log on each secondary database,  
-- using the WITH NORECOVERY option:  
RESTORE LOG MyDb1   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH FILE=1, NORECOVERY  
GO  
RESTORE LOG MyDb2   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITH FILE=1, NORECOVERY  
GO  
  
-- On the server instance that hosts the secondary replica,   
-- join each secondary database to the availability group:  
ALTER DATABASE MyDb1 SET HADR AVAILABILITY GROUP = MyAG;  
GO  
  
ALTER DATABASE MyDb2 SET HADR AVAILABILITY GROUP = MyAG;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **可用性グループおよびレプリカのプロパティを構成するには**  
  
-   [可用性レプリカの可用性モードの変更 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [可用性レプリカのフェールオーバー モードの変更 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [自動フェールオーバーの条件を制御する柔軟なフェールオーバー ポリシーの構成 &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/configure-flexible-automatic-failover-policy.md)  
  
-   [可用性レプリカを追加または変更する場合のエンドポイント URL の指定 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [可用性レプリカでのバックアップの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
-   [可用性レプリカでの読み取り専用アクセスの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [可用性グループの読み取り専用ルーティングの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [可用性レプリカのセッション タイムアウト期間の変更 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **可用性グループの構成を完了するには**  
  
-   [可用性グループへのセカンダリ レプリカの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **別の方法で可用性グループを作成する**  
  
-   [可用性グループ ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [[新しい可用性グループ] ダイアログ ボックスの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [可用性グループの作成 &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)  
  
 **Always On 可用性グループを有効にするには**  
  
-   [AlwaysOn 可用性グループの有効化と無効化 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **データベース ミラーリング エンドポイントを構成するには**  
  
-   [AlwaysOn 可用性グループのデータベース ミラーリング エンドポイントの作成 &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Windows 認証でのデータベース ミラーリング エンドポイントの作成 &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [データベース ミラーリング エンドポイントでの証明書の使用 &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   [可用性レプリカを追加または変更する場合のエンドポイント URL の指定 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **Always On 可用性グループの構成のトラブルシューティング方法**  
  
-   [AlwaysOn 可用性グループの構成のトラブルシューティング &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [失敗したファイルの追加操作のトラブルシューティング &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   **ブログ:**  
  
     [Always On - HADRON 学習シリーズ:HADRON 対応データベースでのワーカー プールの使用](https://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [SQL Server Always On チーム ブログ:SQL Server Always On チームのオフィシャル ブログ](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server エンジニアのブログ](https://blogs.msdn.com/b/psssql/)  
  
-   **ビデオ:**  
  
     [Microsoft SQL Server コードネーム "Denali" Always On シリーズ パート 1: 次世代高可用性ソリューションの概要](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server コードネーム "Denali" Always On シリーズ パート 2: Always On を使用したミッション クリティカルな高可用性ソリューションの構築](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **ホワイト ペーパー:**  
  
     [高可用性と災害復旧のための Microsoft SQL Server AlwaysOn ソリューション ガイド](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [SQL Server 2012 に関する Microsoft ホワイト ペーパー](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server ユーザー諮問チームのホワイト ペーパー](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
