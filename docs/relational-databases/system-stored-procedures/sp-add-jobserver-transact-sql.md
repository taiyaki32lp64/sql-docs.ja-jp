---
title: sp_add_jobserver (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_jobserver
- sp_add_jobserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobserver
ms.assetid: 485252cc-0081-490a-9bd1-cbbd68eea286
author: stevestein
ms.author: sstein
ms.openlocfilehash: bc4d3bca563079c7e1dd7f3ee93e5947f65700b5
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305241"
---
# <a name="sp_add_jobserver-transact-sql"></a>sp_add_jobserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定されたジョブを、特定のサーバーにおける対象ジョブにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_add_jobserver [ @job_id = ] job_id | [ @job_name = ] 'job_name'  
     [ , [ @server_name = ] 'server' ]   
```  
  
## <a name="arguments"></a>引数  
ジョブの識別番号を `[ @job_id = ] job_id` します。 *job_id*は**uniqueidentifier**,、既定値は NULL です。  
  
ジョブの名前 `[ @job_name = ] 'job_name'` ます。 *job_name*は**sysname**,、既定値は NULL です。  
  
> [!NOTE]  
>  *Job_id*または*job_name*のいずれかを指定する必要がありますが、両方を指定することはできません。  
  
ジョブを対象とするサーバーの名前を `[ @server_name = ] 'server'` します。 *サーバー*は**nvarchar (30)** ,、既定値は N ' (LOCAL) ' です。 *サーバー*には、ローカルサーバーの場合は **(local)** 、または既存の対象サーバーの名前を指定できます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 [InclusionThresholdSetting]  
  
## <a name="remarks"></a>Remarks  
 **\@automatic_post**は**sp_add_jobserver**に存在しますが、[引数] の下には表示されません。 **\@automatic_post**は、内部使用のために予約されています。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、ジョブを簡単に管理できるグラフィカルなツールです。ジョブのインフラストラクチャを作成し、管理するには、このツールを使用することをお勧めします。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、このストアド プロシージャを実行できるのは、 **sysadmin** 固定サーバー ロールのメンバーです。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「[SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 複数のサーバーを含むジョブの**sp_add_jobserver**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-assigning-a-job-to-the-local-server"></a>A. ローカル サーバーにジョブを割り当てる  
 次の例では、ジョブ `NightlyBackups` をローカルサーバーで実行するように割り当てます。  
  
> [!NOTE]  
>  この例では、`NightlyBackups` ジョブが既に存在していることを前提としています。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_jobserver  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-assigning-a-job-to-run-on-a-different-server"></a>b. 異なるサーバーで実行するようジョブを割り当てる  
 次の例では、マルチサーバージョブ `Weekly Sales Backups` をサーバー `SEATTLE2`に割り当てます。  
  
> [!NOTE]  
>  この例では、`Weekly Sales Backups` ジョブが既に存在し、`SEATTLE2` が現在のインスタンスに対するターゲット サーバーとして登録されていることを前提としています。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_jobserver  
    @job_name = N'Weekly Sales Backups',  
    @server_name = N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [transact-sql &#40;  の&#41; sp_apply_job_to_targets](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_delete_jobserver](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
