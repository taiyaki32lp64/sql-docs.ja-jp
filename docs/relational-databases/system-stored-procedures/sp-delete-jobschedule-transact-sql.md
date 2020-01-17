---
title: sp_delete_jobschedule (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_jobschedule
- sp_delete_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobschedule
ms.assetid: 82fbb48b-603a-4016-a7fb-1ce17fb76919
author: stevestein
ms.author: sstein
ms.openlocfilehash: a1641685bfe017ab7bc3adfda5c667684a70b786
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130648"
---
# <a name="spdeletejobschedule-transact-sql"></a>sp_delete_jobschedule (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ジョブのスケジュールを削除します。  
  
 **sp_delete_jobschedule**旧バージョンとの互換性を保つのために提供されます。  
  
  
## <a name="remarks"></a>コメント  
 ジョブのスケジュールは、ジョブとは無関係に管理できるようにします。 ジョブからスケジュールを削除するには使用**sp_detach_schedule**します。 スケジュールを削除するには使用**sp_delete_schedule**します。  
  
> **注: sp_delete_jobschedule**は複数のジョブにアタッチされているスケジュールをサポートしていません。 既存のスクリプトを呼び出す場合**sp_delete_jobschedule**を 1 つ以上のジョブに関連付けられているスケジュールを削除する手順には、エラーが返されます。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、このストアド プロシージャを実行できるのは、 **sysadmin** 固定サーバー ロールのメンバーです。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 メンバー、 **sysadmin**ロールは、任意のジョブ スケジュールを削除できます。 以外のユーザーがメンバーの**sysadmin**ロールは、自分が所有するジョブ スケジュールのみを削除できます。  
  
## <a name="see-also"></a>関連項目  
 [sp_delete_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)   
 [表示またはジョブの変更](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_help_jobschedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobschedule-transact-sql.md)   
 [sp_update_jobschedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-jobschedule-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
