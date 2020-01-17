---
title: スケジュールを作成する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- scheduling jobs [SQL Server]
- SQL Server Agent jobs, scheduling
- jobs [SQL Server Agent], scheduling
- schedules [SQL Server], jobs
ms.assetid: 8c7ef3b3-c06d-4a27-802d-ed329dc86ef3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a00b07bb54d30d4e1db49cf2db70dec8286b27e0
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798286"
---
# <a name="create-a-schedule"></a>Create a Schedule
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、または SQL Server 管理オブジェクトを使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]エージェントのジョブのスケジュールを作成できます。  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **スケジュールを作成する方法:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理オブジェクト](#SMO)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> Security  
 詳細については、「 [SQL Server エージェントのセキュリティの実装](implement-sql-server-agent-security.md)」をご覧ください。  
  
##  <a name="SSMS"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-a-schedule"></a>スケジュールを作成するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を展開し、 **[ジョブ]** を右クリックして、 **[スケジュールの管理]** をクリックします。  
  
3.  **[スケジュールの管理]** ダイアログ ボックスで **[新規作成]** をクリックします。  
  
4.  **[名前]** ボックスに新しいスケジュールの名前を入力します。  
  
5.  スケジュールを作成してもすぐに有効にしない場合は、 **[有効]** チェック ボックスをオフにします。  
  
6.  **[スケジュールの種類]** ボックスの一覧で、次のいずれかを選択します。  
  
    -   CPU がアイドル状態になったときにジョブを開始するには、 **[CPU がアイドル状態になったときに開始]** をクリックします。  
  
    -   スケジュールを繰り返し実行する場合は **[定期的]** をクリックします。 定期的なスケジュールを設定するには、ダイアログ ボックス上の **[頻度]** 、 **[一日のうちの頻度]** 、および **[実行時間]** のグループに値を指定します。  
  
    -   スケジュールを一度だけ実行するには、 **[指定日時]** をクリックします。 **指定日時** のスケジュールを設定するには、ダイアログ ボックス上の **[指定日時に発生]** グループに値を指定します。  
  
##  <a name="TSQL"></a> Transact-SQL の使用  
  
#### <a name="to-create-a-schedule"></a>スケジュールを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```sql
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
  
 詳細については、「 [sp_add_schedule &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql)」を参照してください。  
  
##  <a name="SMO"></a>SQL Server 管理オブジェクトの使用  
 **スケジュールを作成するには**  
  
 Visual Basic、ビジュアルC#、PowerShell などのプログラミング言語で `JobSchedule` クラスを使用します。 詳細については、「 [SQL Server 管理オブジェクト (SMO) プログラミング ガイド](https://msdn.microsoft.com/library/ms162169.aspx)」を参照してください。  
