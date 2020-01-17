---
title: ジョブの停止 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
ms.assetid: 4249328a-24d8-4284-9d1d-7d04ed90e3d7
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: baeca9415080f7b333e2edbe55f447d1017a9f2e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265221"
---
# <a name="stop-a-job"></a>Stop a Job
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブを停止する方法について説明します。 ジョブとは、SQL Server エージェントで実行される特定の一連の処理のことです。  
  
-   **作業を開始する準備:**  
  
    [制限事項と制約事項](#Restrictions)  
  
    [セキュリティ](#Security)  
  
-   **ジョブを停止する方法:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理オブジェクト](#SMO)  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Restrictions"></a>制限事項と制約事項  
  
-   ジョブで **CmdExec** または **PowerShell**型のステップが現在実行されている場合、実行中のプロセス (MyProgram.exe など) は途中で強制終了されます。 途中で強制終了した場合、そのプロセスによって使用されていたファイルが開いたままになるなど、予期しない結果が発生する可能性があります。  
  
-   マルチサーバー ジョブの場合、STOP 命令はそのジョブのすべてのターゲット サーバーに通知されます。  
  
### <a name="Security"></a>セキュリティ  
詳細については、「 [SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)」をご覧ください。  
  
## <a name="SSMS"></a>SQL Server Management Studio の使用  
  
#### <a name="to-stop-a-job"></a>ジョブを停止するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** 、 **[ジョブ]** の順に展開し、停止するジョブを右クリックして、 **[ジョブの停止]** をクリックします。  
  
3.  複数のジョブを停止するには、 **[ジョブの利用状況モニター]** を右クリックし、 **[ジョブの利用状況の表示]** をクリックします。 [ジョブの利用状況モニター] で、停止する複数のジョブを選択してから右クリックし、 **[ジョブの停止]** をクリックします。  
  
## <a name="TSQL"></a>Transact-SQL の使用  
  
#### <a name="to-stop-a-job"></a>ジョブを停止するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- stops a job named Weekly Sales Data Backup  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_stop_job  
        N'Weekly Sales Data Backup' ;  
    GO  
    ```  
  
詳しくは、「 [sp_stop_job (Transact-SQL)](https://msdn.microsoft.com/64b4cc75-99a0-421e-b418-94e37595bbb0)」をご覧ください。  
  
## <a name="SMO"></a>SQL Server 管理オブジェクトの使用  
**ジョブを停止するには**  
  
Visual Basic、Visual C#、PowerShell などのプログラミング言語で **Job** クラスの **Stop** メソッドを呼び出します。 詳細については、「 [SQL Server 管理オブジェクト (SMO) プログラミング ガイド](https://msdn.microsoft.com/library/ms162169.aspx)」を参照してください。  
  
