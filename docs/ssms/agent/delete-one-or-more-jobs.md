---
title: 1 つまたは複数のジョブの削除 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, deleting
- dropping jobs
- jobs [SQL Server Agent], deleting
- deleting jobs
- removing jobs
ms.assetid: 67dcdad0-57b2-431c-b77f-4ffc926af93d
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f2dd5a2f8ba4c1edb05df681769115485675403d
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69552984"
---
# <a name="delete-one-or-more-jobs"></a>1 つまたは複数のジョブの削除
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、または SQL Server 管理オブジェクトを使用して、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、 or SQL Server Management Objects.  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Security"></a>セキュリティ  
**sysadmin** 固定サーバー ロールのメンバー以外は、所有しているジョブしか削除できません。  
  
## <a name="SSMS"></a>SQL Server Management Studio の使用  
  
#### <a name="to-delete-a-job"></a>ジョブを削除するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を展開し、 **[ジョブ]** を展開します。次に、削除するジョブを右クリックして、 **[削除]** をクリックします。  
  
3.  **[オブジェクトの削除]** ダイアログ ボックスで、削除するジョブが選択されていることを確認します。  
  
4.  **[OK]** をクリックします。  
  
#### <a name="to-delete-multiple-jobs"></a>複数のジョブを削除するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を展開します。  
  
3.  **[ジョブの利用状況モニター]** を右クリックし、 **[ジョブの利用状況の表示]** をクリックします。  
  
4.  ジョブの利用状況モニターで、削除する複数のジョブを選択します。次に、選択したジョブを右クリックして、 **[ジョブの削除]** をクリックします。  
  
## <a name="TSQL"></a>Transact-SQL の使用  
  
#### <a name="to-delete-a-job"></a>ジョブを削除するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE msdb ;  
    GO  
  
    EXEC sp_delete_job  
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
詳細については、「 [sp_delete_job (Transact-SQL)](https://msdn.microsoft.com/b85db6e4-623c-41f1-9643-07e5ea38db09)」を参照してください。  
  
## <a name="SMO"></a>SQL Server 管理オブジェクトの使用  
**複数のジョブを削除するには**  
  
Visual Basic、Visual C#、PowerShell などのプログラミング言語で **JobCollection** クラスを使用します。 詳細については、「 [SQL Server 管理オブジェクト (SMO) プログラミング ガイド](https://msdn.microsoft.com/library/ms162169.aspx)」を参照してください。  
  
