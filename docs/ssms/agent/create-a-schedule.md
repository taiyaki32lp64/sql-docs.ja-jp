---
title: スケジュールを作成する | Microsoft Docs
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
- schedules [SQL Server], jobs
ms.assetid: 8c7ef3b3-c06d-4a27-802d-ed329dc86ef3
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6d7c1b82b5e9580a7645258b38947cf84988d30f
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264801"
---
# <a name="create-a-schedule"></a>Create a Schedule
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、または SQL Server 管理オブジェクトを使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]エージェントのジョブのスケジュールを作成できます。  
  
-   **作業を開始する準備:**  
  
    [セキュリティ](#Security)  
  
-   **スケジュールを作成する方法:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理オブジェクト](#SMO)  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Security"></a>セキュリティ  
詳細については、「 [SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)」をご覧ください。  
  
## <a name="SSMS"></a>SQL Server Management Studio の使用  
  
#### <a name="to-create-a-schedule"></a>スケジュールを作成するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を展開し、 **[ジョブ]** を右クリックして、 **[スケジュールの管理]** をクリックします。  
  
3.  **[スケジュールの管理]** ダイアログ ボックスで **[新規作成]** をクリックします。  
  
4.  **[名前]** ボックスに新しいスケジュールの名前を入力します。  
  
5.  スケジュールを作成してもすぐに有効にしない場合は、 **[有効]** チェック ボックスをオフにします。  
  
6.  **[スケジュールの種類]** ボックスの一覧で、次のいずれかを選択します。  
  
    -   CPU がアイドル状態になったときにジョブを開始するには、 **[CPU がアイドル状態になったときに開始]** をクリックします。  
  
    -   スケジュールを繰り返し実行する場合は **[定期的]** をクリックします。 定期的なスケジュールを設定するには、ダイアログ ボックス上の **[頻度]** 、 **[一日のうちの頻度]** 、および **[実行時間]** のグループに値を指定します。  
  
    -   スケジュールを一度だけ実行するには、 **[指定日時]** をクリックします。 **指定日時** のスケジュールを設定するには、ダイアログ ボックス上の **[指定日時に発生]** グループに値を指定します。  
  
## <a name="TSQL"></a>Transact-SQL の使用  
  
#### <a name="to-create-a-schedule"></a>スケジュールを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- creates a schedule named RunOnce.   
    -- The schedule runs one time, at 23:30 on the day that the schedule is created.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',  
        @freq_type = 1,  
        @active_start_time = 233000 ;  
  
    GO  
    ```  
  
詳細については、「 [sp_add_schedule (Transact-SQL)](https://msdn.microsoft.com/9060aae3-3ddd-40a5-83bb-3ea7ab1ffbd7)」を参照してください。  
  
## <a name="SMO"></a>SQL Server 管理オブジェクトの使用  
**スケジュールを作成するには**  
  
Visual Basic、Visual C#、PowerShell などの選択したプログラミング言語で **JobSchedule** クラスを使用します。 詳細については、「 [SQL Server 管理オブジェクト (SMO) プログラミング ガイド](https://msdn.microsoft.com/library/ms162169.aspx)」を参照してください。  
  
