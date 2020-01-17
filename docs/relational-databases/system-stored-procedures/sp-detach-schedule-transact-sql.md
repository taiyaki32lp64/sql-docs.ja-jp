---
title: sp_detach_schedule (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_detach_schedule
- sp_detach_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_detach_schedule
ms.assetid: 9a1fc335-1bef-4638-a33a-771c54a5dd19
author: stevestein
ms.author: sstein
ms.openlocfilehash: aed989cc09922b7b480a7dd7b3ca6820d6b77ab2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936743"
---
# <a name="spdetachschedule-transact-sql"></a>sp_detach_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  スケジュールとジョブ間の関連付けを削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_detach_schedule   
     { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,  
       { [ @schedule_id = ] schedule_id | [ @schedule_name = ] 'schedule_name' } ,  
     [ @delete_unused_schedule = ] delete_unused_schedule   
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` スケジュールを削除するジョブのジョブ識別番号。 *job_id*は**uniqueidentifier**、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` スケジュールを削除するジョブの名前。 *job_name*は**sysname**、既定値は NULL です。  
  
> [!NOTE]  
>  いずれか*job_id*または*job_name*指定する必要がありますが、両方を指定することはできません。  
  
`[ @schedule_id = ] schedule_id` ジョブから削除するスケジュールの識別番号を指定します。 *schedule_id*は**int**、既定値は NULL です。  
  
`[ @schedule_name = ] 'schedule_name'` ジョブから削除するスケジュールの名前。 *schedule_name*は**sysname**、既定値は NULL です。  
  
> [!NOTE]  
>  いずれか*schedule_id*または*schedule_name*指定する必要がありますが、両方を指定することはできません。  
  
`[ @delete_unused_schedule = ] delete_unused_schedule` 未使用のジョブ スケジュールを削除するかどうかを指定します。 *@delete_unused_schedule*は**ビット**、既定値は**0**、つまりすべてのスケジュールを保持することでもジョブ参照されていない場合にします。 場合設定**1**ジョブを参照しない場合、未使用のジョブ スケジュールは削除されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 既定では、このストアド プロシージャを実行できるのは、 **sysadmin** 固定サーバー ロールのメンバーです。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 ジョブの所有者が、ジョブをスケジュールにアタッチおよびにスケジュール所有者にならなくても、ジョブ、スケジュールをデタッチできますに注意してください。 ただし場合は、デタッチがのままにジョブがいずれも、呼び出し元が、スケジュール所有者でない限り、スケジュールを削除できません。  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ユーザーがスケジュールを所有しているかどうかが判断されます。 メンバーのみ、 **sysadmin**固定サーバー ロールは、別のユーザーが所有するジョブからスケジュールをデタッチできます。  
  
## <a name="examples"></a>使用例  
 次の例では、間のアソシエーションの削除、`'NightlyJobs'`スケジュールと`'BackupDatabase'`ジョブ。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_detach_schedule  
    @job_name = 'BackupDatabase',  
    @schedule_name = 'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)  
  
  
