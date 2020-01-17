---
title: ジョブのスケジュール設定 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- scheduling jobs [SQL Server]
- SQL Server Agent jobs, scheduling
- jobs [SQL Server Agent], scheduling
ms.assetid: f626390a-a3df-4970-b7a7-a0529e4a109c
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8e997912104b34fe15a0ab8a95073198484be163
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263079"
---
# <a name="schedule-a-job"></a>Schedule a Job
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブのスケジュールを設定する方法について説明します。  
  
-   **作業を開始する準備:**  
  
    [セキュリティ](#Security)  
  
-   **ジョブのスケジュールを設定する方法:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理オブジェクト](#SMO)  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Security"></a>セキュリティ  
詳細については、「 [SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)」をご覧ください。  
  
## <a name="SSMS"></a>SQL Server Management Studio の使用  
  
#### <a name="to-create-and-attach-a-schedule-to-a-job"></a>スケジュールを作成してジョブにアタッチするには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** 、 **[ジョブ]** の順に展開し、スケジュールを設定するジョブを右クリックします。次に、 **[プロパティ]** をクリックします。  
  
3.  **[スケジュール]** ページをクリックし、 **[新規作成]** をクリックします。  
  
4.  **[名前]** ボックスに新しいスケジュールの名前を入力します。  
  
5.  スケジュールを作成してもすぐに有効にしない場合は、 **[有効]** チェック ボックスをオフにします。  
  
6.  **[スケジュールの種類]** ボックスの一覧で、次のいずれかを選択します。  
  
    -   **[SQL Server エージェントの開始時に自動的に開始]** 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスが開始されたときにジョブを開始します。  
  
    -   **[CPU がアイドル状態になったときに開始]** 。CPU がアイドル状態になったときにジョブを開始します。  
  
    -   **[定期的]** 。スケジュールを繰り返し実行します。 定期的なスケジュールを設定するには、ダイアログ ボックス上の **[頻度]** 、 **[一日のうちの頻度]** 、および **[実行時間]** のグループに値を指定します。  
  
    -   **[指定日時]** 。スケジュールを 1 回のみ実行します。 **指定日時** のスケジュールを設定するには、ダイアログ ボックス上の **[指定日時に発生]** グループに値を指定します。  
  
#### <a name="to-attach-a-schedule-to-a-job"></a>ジョブにスケジュールをアタッチするには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** 、 **[ジョブ]** の順に展開し、スケジュールを設定するジョブを右クリックして、 **[プロパティ]** をクリックします。  
  
3.  **[スケジュール]** ページをクリックし、 **[選択]** をクリックします。  
  
4.  アタッチするスケジュールを選択して、 **[OK]** をクリックします。  
  
5.  **[ジョブのプロパティ]** ダイアログ ボックスで、アタッチされたスケジュールをダブルクリックします。  
  
6.  **[開始日]** が正しく設定されていることを確認します。 正しく設定されていない場合は、スケジュールの開始日を設定し、 **[OK]** をクリックします。  
  
7.  **[ジョブのプロパティ]** ダイアログ ボックスで、 **[OK]** をクリックします。  
  
## <a name="TSQL"></a>Transact-SQL の使用  
  
#### <a name="to-schedule-a-job"></a>ジョブのスケジュールを設定するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE msdb ;  
    GO  
    -- creates a schedule named NightlyJobs.   
    -- Jobs that use this schedule execute every day when the time on the server is 01:00.   
    EXEC sp_add_schedule  
        @schedule_name = N'NightlyJobs' ,  
        @freq_type = 4,  
        @freq_interval = 1,  
        @active_start_time = 010000 ;  
    GO  
    -- attaches the schedule to the job BackupDatabase  
    EXEC sp_attach_schedule  
       @job_name = N'BackupDatabase',  
       @schedule_name = N'NightlyJobs' ;  
    GO  
    ```  
  
詳しくは、「 [sp_add_schedule (Transact-SQL)](https://msdn.microsoft.com/9060aae3-3ddd-40a5-83bb-3ea7ab1ffbd7) 」および「 [sp_attach_schedule (Transact-SQL)](https://msdn.microsoft.com/80c80eaf-cf23-4ed8-b8dd-65fe59830dd1)」をご覧ください。  
  
## <a name="SMO"></a>SQL Server 管理オブジェクトの使用  
Visual Basic、Visual C#、PowerShell などの選択したプログラミング言語で **JobSchedule** クラスを使用します。 詳細については、「[SQL Server 管理オブジェクト (SMO) プログラミング ガイド](https://msdn.microsoft.com/library/ms162169.aspx)」を参照してください。  
  
