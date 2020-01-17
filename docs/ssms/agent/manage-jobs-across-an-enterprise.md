---
title: エンタープライズ全体におけるジョブの管理 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiserver job management [SQL Server]
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
- target servers [SQL Server], job changes
ms.assetid: 4fe7f6c6-f89b-4430-979c-4994a5dcf7a6
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6044edea68f00b27ed7be61b87d9438df7b72c18
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68257775"
---
# <a name="manage-jobs-across-an-enterprise"></a>エンタープライズ全体におけるジョブの管理
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用せずにマルチサーバー ジョブ定義を変更した場合は、ターゲット サーバーが更新済みジョブを再びダウンロードできるように、その変更をダウンロード一覧に通知する必要があります。 ターゲット サーバーが最新のジョブ定義を確実に持つように、マルチサーバー ジョブを更新した後で INSERT 命令を次のように通知します。  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
マルチサーバー ジョブが変更されたことをターゲット サーバーに通知するには、次のいずれかのプロシージャを使用した後で前述のコマンドを呼び出す必要があります。  
  
-   [sp_add_jobstep (Transact-SQL)](https://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755)  
  
-   [sp_update_jobstep (Transact-SQL)](https://msdn.microsoft.com/e158802c-c347-4a5d-bf75-c03e5ae56e6b)  
  
-   [sp_delete_jobstep (Transact-SQL)](https://msdn.microsoft.com/421ede8e-ad57-474a-9fb9-92f70a3e77e3)  
  
-   [イベントの管理](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
-   [sp_detach_schedule (Transact-SQL)](https://msdn.microsoft.com/9a1fc335-1bef-4638-a33a-771c54a5dd19)  
  
    > [!NOTE]  
    > **sp_update_job** または **sp_delete_job** を呼び出した後で **sp_post_msx_operation**を呼び出す必要はありません。この 2 つのストアド プロシージャは、必要な変更をダウンロード一覧に自動的に通知するためです。  
  
エンタープライズ全体でジョブを管理するための一般的なタスクは次のとおりです。  
  
**ターゲット サーバーの状態を確認するには**  
  
-   [Transact-SQL](https://msdn.microsoft.com/f841d3bd-901a-4980-ad0b-1c6eeba3f717)  
  
-   [SQL Server 管理オブジェクト (SMO)](https://msdn.microsoft.com/4cde2b85-2a31-4cac-8d16-7a4196066193)  
  
**ジョブのターゲット サーバーを変更するには**  
  
-   [SQL Server Management Studio](../../ssms/agent/modify-the-target-servers-for-a-job.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/485252cc-0081-490a-9bd1-cbbd68eea286)  
  
-   [SQL Server 管理オブジェクト (SMO)](https://msdn.microsoft.com/4cde2b85-2a31-4cac-8d16-7a4196066193)  
  
**ターゲット サーバーの場所を変更するには**  
  
-   [SQL Server Management Studio](../../ssms/agent/specify-a-target-server-s-location-sql-server-management-studio.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f)  
  
-   [SQL Server 管理オブジェクト (SMO)](https://msdn.microsoft.com/4cde2b85-2a31-4cac-8d16-7a4196066193)  
  
**ターゲット サーバーのクロックを同期するには**  
  
-   [SQL Server Management Studio](../../ssms/agent/synchronize-target-server-clocks-sql-server-management-studio.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/40e44df7-d3e3-44ee-b149-08aba629a21f)  
  
**ターゲット サーバーからマスター サーバーにポーリングさせるには**  
  
-   [SQL Server Management Studio](../../ssms/agent/force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/085deef8-2709-4da9-bb97-9ab32effdacf)  
  
## <a name="see-also"></a>参照  
[イベントの管理](../../ssms/agent/manage-events.md)  
  
