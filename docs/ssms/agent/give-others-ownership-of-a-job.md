---
title: ジョブの所有権を他のユーザーに割り当てる | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], owners
- owners [SQL Server], jobs
- SQL Server Agent jobs, owners
ms.assetid: 2ded5e9c-4251-4fb1-a047-99f13d150b61
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1516bb84fbfe733ba9d37838d945ef2f88019d76
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262407"
---
# <a name="give-others-ownership-of-a-job"></a>Give Others Ownership of a Job
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブの所有権を他のユーザーに割り当てる方法を説明します。  
  
-   **作業を開始する準備:** [制限事項と制約事項](#Restrictions)、[セキュリティ](#Security)  
  
-   **ジョブの所有権を他のユーザーに割り当てる方法:**  
  
    [SQL Server Management Studio](#SSMSProc2)  
  
    [Transact-SQL](#TsqlProc2)  
  
    [SQL Server 管理オブジェクト](#SMOProc2)  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Restrictions"></a>制限事項と制約事項  
ジョブを作成するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定データベース ロールか **sysadmin** 固定サーバー ロールのメンバーである必要があります。 ジョブの編集は、ジョブの所有者または **sysadmin** ロールのメンバーのみが行うことができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定データベース ロールの詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
ジョブの所有者を変更するには、システム管理者でなければなりません。  
  
別のログインにジョブを割り当てた場合に、新しい所有者がそのジョブを正常に実行できる十分な権限を持っていないこともあります。  
  
### <a name="Security"></a>セキュリティ  
セキュリティを確保するため、ジョブの所有者または **sysadmin** ロールのメンバーだけがジョブの定義を変更できます。 **sysadmin** 固定サーバー ロールのメンバーのみが別のユーザーにジョブの所有権を割り当てることができ、ジョブの所有者とは無関係にジョブを実行できます。  
  
> [!NOTE]  
> ジョブの所有権を **sysadmin** 固定サーバー ロールのメンバーでないユーザーに変更し、そのジョブがプロキシ アカウントを必要とするジョブ ステップを実行する ( [!INCLUDE[ssIS](../../includes/ssis_md.md)] パッケージの実行など) 場合は、ユーザーがそのプロキシ アカウントにアクセスできることを確認してください。アクセスできない場合、ジョブは失敗します。  
  
#### <a name="Permissions"></a>アクセス許可  
詳細については、「 [SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)」をご覧ください。  
  
## <a name="SSMSProc2"></a>SQL Server Management Studio の使用  
**ジョブの所有権を他のユーザーに割り当てるには**  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** 、 **[ジョブ]** の順に展開し、ジョブを右クリックして **[プロパティ]** をクリックします。  
  
3.  **[所有者]** ボックスの一覧で、ログインを選択します。 ジョブの所有者を変更するには、システム管理者でなければなりません。  
  
    別のログインにジョブを割り当てた場合に、新しい所有者がそのジョブを正常に実行できる十分な権限を持っていないこともあります。  
  
## <a name="TsqlProc2"></a>Transact-SQL の使用  
**ジョブの所有権を他のユーザーに割り当てるには**  
  
1.  オブジェクト エクスプローラーで、データベース エンジンのインスタンスに接続し、そのインスタンスを展開します。  
  
2.  ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  クエリ ウィンドウで、 [sp_manage_jobs_by_login (Transact-SQL)](https://msdn.microsoft.com/832ec15a-6e92-4eb5-8c4a-af4dba79fbaa) システム ストアド プロシージャを使用する次のステートメントを入力します。 次の例では、 `danw` からのすべてのジョブを `françoisa`に再割り当てします。  
  
    ```  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_manage_jobs_by_login  
        @action = N'REASSIGN',  
        @current_owner_login_name = N'danw',  
        @new_owner_login_name = N'françoisa' ;  
    GO  
    ```  
  
## <a name="SMOProc2"></a>SQL Server 管理オブジェクトの使用  
**ジョブの所有権を他のユーザーに割り当てるには**  
  
1.  Visual Basic、Visual C#、PowerShell などのプログラミング言語で **Job** クラスを呼び出します。 コード例については、「 [SQL Server エージェントでの自動管理タスクのスケジュール設定](../../relational-databases/server-management-objects-smo/tasks/scheduling-automatic-administrative-tasks-in-sql-server-agent.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[ジョブの実装](../../ssms/agent/implement-jobs.md)  
[ジョブの作成](../../ssms/agent/create-jobs.md)  
  
