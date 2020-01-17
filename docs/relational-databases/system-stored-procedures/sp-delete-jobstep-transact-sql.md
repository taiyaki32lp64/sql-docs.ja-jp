---
title: sp_delete_jobstep (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_jobstep
- sp_delete_jobstep_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobstep
ms.assetid: 421ede8e-ad57-474a-9fb9-92f70a3e77e3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8e55465dfe2424144d74bc40492fdb897d4aa72b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130623"
---
# <a name="spdeletejobstep-transact-sql"></a>sp_delete_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ジョブからジョブ ステップを削除します。  
  
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_delete_jobstep { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,   
     [ @step_id = ] step_id   
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` ステップの削除元となるジョブの識別番号。 *job_id*は**uniqueidentifier**、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` ステップの削除元となるジョブの名前。 *job_name*は**sysname**、既定値は NULL です。  
  
> **注:** いずれか*job_id*または*job_name*指定する必要があります。 両方を指定することはできません。  
  
`[ @step_id = ] step_id` 削除するステップの識別番号。 *step_id*は**int**、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 ジョブ ステップを削除すると、削除したステップを参照する他のジョブ ステップは自動的に更新されます。  
  
 特定のジョブに関連する手順の詳細については、実行**sp_help_jobstep**します。  
  
> **注:** 呼び出す**sp_delete_jobstep**で、 *step_id*ゼロの値はすべて、ジョブのジョブ ステップを削除します。  
  
 Microsoft SQL Server Management Studio は、ジョブを簡単に管理できるグラフィカルなツールです。ジョブのインフラストラクチャを作成し、管理するには、Microsoft SQL Server Management Studio を使用することをお勧めします。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、このストアド プロシージャを実行できるのは、 **sysadmin** 固定サーバー ロールのメンバーです。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 メンバーだけ**sysadmin**別のユーザーが所有するジョブ ステップを削除することができます。  
  
## <a name="examples"></a>使用例  
 次の例では、ジョブ ステップを削除する`1`ジョブから`Weekly Sales Data Backup`します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [表示またはジョブの変更](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_add_jobstep &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_update_jobstep &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
