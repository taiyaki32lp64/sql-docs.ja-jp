---
title: SQL Server 用のジョブを作成して Linux 上で実行する
description: このチュートリアルでは、Linux 上で SQL Server エージェント ジョブを実行する方法について説明します。
author: VanMSFT
ms.author: vanto
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1d93d95e-9c89-4274-9b3f-fa2608ec2792
ms.openlocfilehash: 5abd2db590a89350f45497d7f94b81940a0ec5bc
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68065154"
---
# <a name="create-and-run-sql-server-agent-jobs-on-linux"></a>Microsoft SQL Server エージェント ジョブを作成して Linux 上で実行する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server ジョブを使用して、SQL Server データベースで同じ一連のコマンドを定期的に実行します。 このチュートリアルでは、Transact-SQL と SQL Server Management Studio (SSMS) の両方を使用して、Linux 上で実行される SQL Server エージェント ジョブを作成する方法の例を示します。

> [!div class="checklist"]
> * Linux 上に SQL Server エージェントをインストールする
> * データベースのバックアップを毎日実行する新しいジョブを作成する
> * ジョブのスケジュールを設定して実行する
> * SSMS で同じ手順を実行する (省略可能)

Linux 上の SQL Server エージェントに関する既知の問題については、[リリース ノート](sql-server-linux-release-notes.md)を参照してください。

## <a name="prerequisites"></a>Prerequisites

このチュートリアルを完了するには、次の前提条件を満たす必要があります。

* 次の前提条件を満たしている Linux コンピューター:
  * コマンドライン ツールを備えた SQL Server ([RHEL](quickstart-install-connect-red-hat.md)、[SLES](quickstart-install-connect-suse.md)、または [Ubuntu](quickstart-install-connect-ubuntu.md))。

次の前提条件には対応しなくてもかまいません。

* SSMS を備えた Windows 仮想マシン:
  * SSMS 手順を実行するための [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (オプション)。

## <a name="enable-sql-server-agent"></a>SQL Server エージェントを有効にする

Linux 上で SQL Server エージェントを使用するには、まず SQL Server が既にインストールされているコンピューターで SQL Server エージェントを有効にする必要があります。

1. SQL Server エージェントを有効にするには、次の手順に従います。
  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
  ```

1. 次のコマンドを使用して SQL Server を再起動します。
  ```bash
  sudo systemctl restart mssql-server
  ```

> [!NOTE]
> SQL Server 2017 CU4 以降、SQL Server エージェントは **mssql-Server** パッケージに含まれており、既定で無効になっています。 CU4 より前のバージョンでエージェントを設定するには、[Linux 上に SQL Server エージェントをインストール](sql-server-linux-setup-sql-agent.md)します。

## <a name="create-a-sample-database"></a>サンプル データベースの作成

次の手順に従って、**SampleDB** という名前のサンプル データベースを作成します。 このデータベースは、毎日のバックアップ ジョブを実行するために使用されます。

1. Linux コンピューター上で、bash ターミナル セッションを開きます。

1. **sqlcmd** を使用して、Transact-SQL の **CREATE DATABASE** コマンドを実行します。

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'CREATE DATABASE SampleDB'
   ```

1. サーバー上のデータベースを一覧表示して、データベースが作成されていることを確認します。

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'SELECT Name FROM sys.Databases'
   ```

## <a name="create-a-job-with-transact-sql"></a>Transact-SQL を使用してジョブを作成する

次の手順では、Transact-SQL コマンドを使用して、Linux 上に SQL Server エージェント ジョブを作成します。 このジョブによって、サンプル データベース (**SampleDB**) のバックアップが毎日実行されます。

> [!TIP]
> 任意の T-SQL クライアントを使用して、これらのコマンドを実行できます。 たとえば、Linux 上で、[sqlcmd](sql-server-linux-setup-tools.md) または [Visual Studio Code](sql-server-linux-develop-use-vscode.md) を使用できます。 リモート Windows Server から SQL Server Management Studio (SSMS) でクエリを実行したり、次のセクションで説明されているジョブ管理用の UI インターフェイスを使用したりすることもできます。

1. [sp_add_job](../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md) を実行して、`Daily SampleDB Backup` という名前のジョブを作成します。

   ```sql
   -- Adds a new job executed by the SQLServerAgent service
   -- called 'Daily SampleDB Backup'
   USE msdb ;
   GO
   EXEC dbo.sp_add_job
      @job_name = N'Daily SampleDB Backup' ;
   GO
   ```

1. [sp_add_jobstep](../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md) を呼び出して、`SampleDB` データベースのバックアップを作成するジョブ ステップを作成します。

   ```sql
   -- Adds a step (operation) to the job
   EXEC sp_add_jobstep
      @job_name = N'Daily SampleDB Backup',
      @step_name = N'Backup database',
      @subsystem = N'TSQL',
      @command = N'BACKUP DATABASE SampleDB TO DISK = \
         N''/var/opt/mssql/data/SampleDB.bak'' WITH NOFORMAT, NOINIT, \
         NAME = ''SampleDB-full'', SKIP, NOREWIND, NOUNLOAD, STATS = 10',
      @retry_attempts = 5,
      @retry_interval = 5 ;
   GO
   ```

1. 次に、[sp_add_schedule](../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md) を使用して、ジョブの日次スケジュールを作成します。

   ```sql
   -- Creates a schedule called 'Daily'
   EXEC dbo.sp_add_schedule
      @schedule_name = N'Daily SampleDB',
      @freq_type = 4,
      @freq_interval = 1,
      @active_start_time = 233000 ;
   USE msdb ;
   GO
   ```

1. [sp_attach_schedule](../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md) を使用して、ジョブのスケジュールをジョブにアタッチします。

   ```sql
   -- Sets the 'Daily' schedule to the 'Daily SampleDB Backup' Job
   EXEC sp_attach_schedule
      @job_name = N'Daily SampleDB Backup',
      @schedule_name = N'Daily SampleDB';
   GO
   ```

1. [sp_add_jobserver](../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md) を使用して、対象サーバーにジョブを割り当てます。 この例では、ターゲットはローカル サーバーです。

   ```sql
   EXEC dbo.sp_add_jobserver
      @job_name = N'Daily SampleDB Backup',
      @server_name = N'(LOCAL)';
   GO
   ```
1. [sp_start_job](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md) を使用してジョブを開始します。

   ```sql
   EXEC dbo.sp_start_job N' Daily SampleDB Backup' ;
   GO
   ```

## <a name="create-a-job-with-ssms"></a>SSMS でジョブを作成する

Windows 上で SQL Server Management Studio (SSMS) を使用して、ジョブをリモートで作成して管理することもできます。

1. Windows 上で SSMS を起動し、Linux SQL Server インスタンスに接続します。 詳細については、[SSMS での SQL Server on Linux の管理](sql-server-linux-manage-ssms.md)に関する記事を参照してください。

1. **SampleDB** という名前のサンプル データベースが作成されていることを確認します。

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-0.png" alt="Create a SampleDB database" style="width: 550px;"/>

1. SQL エージェントが[インストールされ](sql-server-linux-setup-sql-agent.md)、正しく構成されていることを確認します。 オブジェクト エクスプローラーで [SQL Server エージェント] の横にあるプラス記号を見つけます。 SQL Server エージェントが有効になっていない場合は、Linux 上で **mssql-server** サービスを再起動してみてください。

   ![SQL Server エージェントがインストールされていることを確認する](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-1.png)

1. 新しいジョブを作成します。

   ![新しいジョブを作成する](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-2.png)

1. ジョブの名前を指定し、ジョブ ステップを作成します。

   ![ジョブ ステップを作成する](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-3.png)

1. 使用するサブシステムとジョブ ステップで実行する操作を指定します。

   ![ジョブのサブシステム](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-4.png)

   ![ジョブ ステップのアクション](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-5.png)

1. 新しいジョブ スケジュールを作成します。

   ![ジョブ スケジュール](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-6.png)

   ![ジョブ スケジュール](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-8.png)

1. ジョブを開始します。

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-9.png" alt="Start the SQL Server Agent job" style="width: 550px;"/>

## <a name="next-steps"></a>Next Steps

このチュートリアルでは、以下を実行する方法について説明しました。

> [!div class="checklist"]
> * Linux 上に SQL Server エージェントをインストールする
> * Transact-SQL とシステム ストアド プロシージャを使用してジョブを作成する
> * データベース バックアップを毎日実行するジョブを作成する
> * SSMS UI を使用してジョブの作成と管理を行う

次に、ジョブの作成と管理に関するその他の機能を確認してください。

> [!div class="nextstepaction"]
>[SQL Server エージェントのドキュメント](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)
