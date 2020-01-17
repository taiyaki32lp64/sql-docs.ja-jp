---
title: Azure で SSIS パッケージのスケジュールを設定する | Microsoft Docs
description: Azure SQL Database にデプロイされている SSIS パッケージの実行スケジュールの設定に利用できる方法の概要について示します。
ms.date: 05/29/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
ms.openlocfilehash: 4217acf163e8603c5993cfa8ade4207c9a79c6cf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054566"
---
# <a name="schedule-the-execution-of-sql-server-integration-services-ssis-packages-deployed-in-azure"></a>Azure でデプロイされている SQL Server Integration Services (SSIS) パッケージの実行スケジュールを設定する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



この記事で説明する方法の 1 つを選択することで、Azure SQL Database サーバーで SSISDB カタログにデプロイされている SSIS パッケージの実行をスケジュールできます。 パッケージは直接スケジュールするか、Azure Data Factory パイプラインの一部として間接的にスケジュールできます。 Azure の SSIS の概要については、「[SQL Server Integration Services ワークロードをクラウドにリフト アンド シフトする](ssis-azure-lift-shift-ssis-packages-overview.md)」を参照してください。

- パッケージのスケジュールを直接設定する

  - [SQL Server Management Studio (SSMS) のスケジュール オプションでスケジュールを設定する](#ssms)

  - [SQL Database エラスティック ジョブ](#elastic)

  - [SQL Server エージェント](#agent)

- [Azure Data Factory パイプラインの一部としてパッケージのスケジュールを間接的に設定する](#activity)


## <a name="ssms"></a> SSMS でパッケージをスケジュールする

SQL Server Management Studio (SSMS) では、SSIS カタログ データベース SSISDB に配置されたパッケージを右クリックして **[スケジュール]** を選択することで、 **[新しいスケジュール]** ダイアログ ボックスを開くことができます。 詳細については、「[SSMS を利用して Azure で SSIS パッケージのスケジュールを設定する](ssis-azure-schedule-packages-ssms.md)」を参照してください。

この機能には、SQL Server Management Studio バージョン 17.7 以降が必要です。 最新バージョンの SSMS を入手するには、「[SQL Server Management Studio (SSMS) のダウンロード](../../ssms/download-sql-server-management-studio-ssms.md)」を参照してください。

## <a name="elastic"></a> SQL Database エラスティック ジョブを使用してパッケージをスケジュールする

SQL Database のエラスティック ジョブに関する詳細については、「[スケールアウトされたクラウド データベースの管理](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)」を参照してください。

### <a name="prerequisites"></a>Prerequisites

エラスティック ジョブを使用して、Azure SQL Database サーバー上の SSISDB カタログ データベースに格納されている SSIS パッケージをスケジュール設定するには、事前に次の作業を行う必要があります。

1.  Elastic Database ジョブ コンポーネントをインストールして構成します。 詳細については、「[Elastic Database ジョブのインストールの概要](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-service-installation)」を参照してください。

2. ジョブで SSIS カタログ データベースにコマンドを送信するために使用できるデータベース スコープの資格情報を作成します。 詳細については、「[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)」 (データベース スコープの資格情報を作成する (Transact-SQL)) を参照してください。

### <a name="create-an-elastic-job"></a>エラスティック ジョブの作成

次の例に示されているスクリプトと同じような Transact-SQL スクリプトを使用して、ジョブを作成します。

```sql
-- Create Elastic Jobs target groupÂ 
EXECÂ jobs.sp_add_target_group 'TargetGroup'Â 

-- Add Elastic Jobs target group memberÂ 
EXECÂ jobs.sp_add_target_group_memberÂ @target_group_name='TargetGroup',Â 
    @target_type='SqlDatabase',Â @server_name='YourSQLDBServer.database.windows.net',
    @database_name='SSISDB'Â 

-- Add a job to schedule SSIS package execution
EXECÂ jobs.sp_add_jobÂ @job_name='ExecutePackageJob',Â @description='Description',Â 
    @schedule_interval_type='Minutes',Â @schedule_interval_count=60

-- Add a job step to create/start SSIS package execution using SSISDB catalog stored procedures
EXECÂ jobs.sp_add_jobstepÂ @job_name='ExecutePackageJob',Â 
    @command=N'DECLAREÂ @exe_idÂ bigintÂ 
        EXEC [SSISDB].[catalog].[create_execution]
            @folder_name=N''folderName'', @project_name=N''projectName'',
            @package_name=N''packageName'', @use32bitruntime=0,
            @runinscaleout=1, @useanyworker=1,Â 
            @execution_id=@exe_idÂ OUTPUT       Â 
        EXEC [SSISDB].[catalog].[start_execution] @exe_id, @retry_count=0',Â 
    @credential_name='YourDBScopedCredentials',Â 
    @target_group_name='TargetGroup'Â 

-- Enable the job scheduleÂ 
EXECÂ jobs.sp_update_jobÂ @job_name='ExecutePackageJob',Â @enabled=1,Â 
    @schedule_interval_type='Minutes',Â @schedule_interval_count=60Â 
```

## <a name="agent"></a> オンプレミス SQL Server エージェントを使用してパッケージのスケジュールを設定する

SQL Server エージェントの詳細については、「[パッケージに対する SQL Server エージェント ジョブ](../packages/sql-server-agent-jobs-for-packages.md)」を参照してください。

### <a name="prerequisite---create-a-linked-server"></a>前提条件 - リンク サーバーを作成する

オンプレミスの SQL Server エージェントを使用して、Azure SQL Database サーバーに格納されているパッケージの実行をスケジュール設定するには、事前に SQL Database サーバーをリンク サーバーとしてオンプレミス SQL Server に追加する必要があります。

1.  **リンク サーバーを設定する**

    ```sql
    -- Add the SSISDB database on your Azure SQL Database as a linked server to your SQL Server on premises
    EXEC sp_addlinkedserver
        @server='myLinkedServer', -- Name your linked server
        @srvproduct='',     
        @provider='sqlncli', -- Use SQL Server native client
        @datasrc='<server_name>.database.windows.net', -- Add your Azure SQL Database server endpoint
        @location='',
        @provstr='',
        @catalog='SSISDB'  -- Add SSISDB as the initial catalog
    ```

2.  **リンク サーバーの資格情報を設定する**

    ```sql
    -- Add your Azure SQL DB server admin credentials
    EXEC sp_addlinkedsrvlogin
        @rmtsrvname = 'myLinkedServer',
        @useself = 'false',
        @rmtuser = 'myUsername', -- Add your server admin username
        @rmtpassword = 'myPassword' -- Add your server admin password
    ```

3.  **リンク サーバーのオプションを設定する**

    ```sql
    EXEC sp_serveroption 'myLinkedServer', 'rpc out', true;
    ```

詳細については、「[リンク サーバーの作成](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)」と「[リンク サーバー](../../relational-databases/linked-servers/linked-servers-database-engine.md)」を参照してください。

### <a name="create-a-sql-server-agent-job"></a>SQL Server エージェント ジョブを作成する

オンプレミスの SQL Server エージェントを使用してパッケージのスケジュールを設定するには、SSIS カタログ ストアド プロシージャ `[catalog].[create_execution]` と `[catalog].[start_execution]` を順に呼び出すジョブ ステップでジョブを作成します。 詳細については、「[パッケージに対する SQL Server エージェント ジョブ](../packages/sql-server-agent-jobs-for-packages.md)」を参照してください。

1.  SQL Server Management Studio では、ジョブを作成するオンプレミスの SQL Server データベースに接続します。

2.  **SQL Server エージェント** ノードを右クリックし、 **[新規]** 、 **[ジョブ]** の順に選択し、 **[新しいジョブ]** ダイアログ ボックスを開きます。

3.  **[新しいジョブ]** ダイアログ ボックスで、 **[手順]** ページを選択し、 **[新規]** を選択して、 **[新しいジョブ ステップ]** ダイアログ ボックスを開きます。

4.  **[新しいジョブ ステップ]** ダイアログ ボックスで、`SSISDB` を**データベース**として選択します。

5.  **[コマンド]** フィールドで、次の例に示されたスクリプトのような Transact-SQL スクリプトを入力します。

    ```sql
    -- T-SQL script to create and start SSIS package execution using SSISDB stored procedures
    DECLARE @return_valueÂ int,Â @exe_idÂ bigintÂ 

    EXEC @return_valueÂ =Â [YourLinkedServer].[SSISDB].[catalog].[create_execution]Â 
        @folder_name=N'folderName',Â @project_name=N'projectName',Â 
        @package_name=N'packageName',Â @use32bitruntime=0,Â @runincluster=1,Â @useanyworker=1,
        @execution_id=@exe_idÂ OUTPUTÂ 

    EXEC [YourLinkedServer].[SSISDB].[catalog].[set_execution_parameter_value] @exe_id,
        @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1

    EXEC [YourLinkedServer].[SSISDB].[catalog].[start_execution]Â @execution_id=@exe_id
    ```

6.  ジョブの構成とスケジュール設定を完了します。

## <a name="activity"></a> Azure Data Factory パイプラインの一部としてパッケージのスケジュールを設定する

SSIS パッケージを実行する Azure Data Factory パイプラインの実行トリガーを使用し、パッケージのスケジュールを間接的に設定できます。

Data Factory パイプラインをスケジュールするには、次のトリガーの 1 つを使用します。

- [スケジュール トリガー](https://docs.microsoft.com/azure/data-factory/how-to-create-schedule-trigger)

- [タンブリング ウィンドウ トリガー](https://docs.microsoft.com/azure/data-factory/how-to-create-tumbling-window-trigger)

- [イベントベース トリガー](https://docs.microsoft.com/azure/data-factory/how-to-create-event-trigger)

Data Factory パイプラインの一部として SSIS パッケージを実行するには、次のアクティビティのいずれかを使用します。

- [SSIS パッケージの実行アクティビティ](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)

- [ストアド プロシージャ アクティビティ](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-stored-procedure-activity)

## <a name="next-steps"></a>次の手順

Azure にデプロイされている SSIS パッケージの実行オプションを確認してください。 詳細については、「[Azure で SSIS パッケージを実行する](ssis-azure-run-packages.md)」を参照してください。
