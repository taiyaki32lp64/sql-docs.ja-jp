---
title: sp_changedynamicsnapshot_job (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedynamicsnapshot_job
- sp_changedynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_changedynamicsnapshot_job
ms.assetid: ea0dacd2-a5fd-42f4-88dd-7d289b0ae017
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4db6a29d92fe093e9704f88fcc528c9fa687ccff
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768946"
---
# <a name="spchangedynamicsnapshotjob-transact-sql"></a>sp_changedynamicsnapshot_job (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  パラメーター化された行フィルターを使用して、パブリケーションに対するサブスクリプションのスナップショットを生成するエージェントジョブを変更します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changedynamicsnapshot_job [ @publication = ] 'publication'  
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
    [ , [ @frequency_type = ] frequency_type ]   
    [ , [ @frequency_interval = ] frequency_interval ]   
    [ , [ @frequency_subday = ] frequency_subday ]   
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]   
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]   
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]   
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'`変更するスナップショットジョブの名前を指定します。 *dynamic_snapshot_jobname*は**sysname**,、既定値は N '% ' です。 *Dynamic_snapshot_jobid*を指定する場合は、 *dynamic_snapshot_jobname*に既定値を使用する必要があります。  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'`変更するスナップショットジョブの ID を示します。 *dynamic_snapshot_jobid*は**uniqueidentifier**,、既定値は NULL です。 *Dynamic_snapshot_jobname*を指定する場合は、 *dynamic_snapshot_jobid*に既定値を使用する必要があります。  
  
`[ @frequency_type = ] frequency_type`エージェントをスケジュールする頻度を指定します。 *frequency_type*は**int**,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|指定日時|  
|**2**|[要求時]|  
|**4**|毎日。|  
|**8**|毎週。|  
|**16**|毎月。|  
|**32**|月単位の相対|  
|**64**|自動開始|  
|**128**|定期|  
|NULL (既定値)||  
  
`[ @frequency_interval = ] frequency_interval`エージェントを実行する曜日。 *frequency_interval*は**int**,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|日曜日|  
|**2**|月曜日|  
|**3**|火曜日|  
|**4**|水曜日|  
|**5**|木曜日|  
|**6**|金曜日|  
|**7**|土曜日|  
|**8**|Day|  
|**9**|平日|  
|"**10**"|週末|  
|NULL (既定値)||  
  
`[ @frequency_subday = ] frequency_subday`定義した期間中に再スケジュールする頻度を指定します。 *frequency_subday*は**int**,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|1 回。|  
|**2**|第 2 週|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (既定値)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*の間隔を指定します。 *frequency_subday_interval*は**int**,、既定値は NULL です。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`マージエージェントが実行される日付を指定します。 このパラメーターが使用されるときに *frequency_type* に設定されている **32** (月単位)。 *frequency_relative_interval*は**int**,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|First|  
|**2**|第 2 週|  
|**4**|サードパーティ|  
|**8**|4 番目|  
|**16**|Last|  
|NULL (既定値)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*によって使用される定期実行係数を示します。 *frequency_recurrence_factor*は**int**,、既定値は NULL です。  
  
`[ @active_start_date = ] active_start_date`マージエージェントを最初にスケジュール設定する日付を YYYYMMDD 形式で指定します。 *active_start_date*は**int**,、既定値は NULL です。  
  
`[ @active_end_date = ] active_end_date`マージエージェントのスケジュール設定を停止する日付を YYYYMMDD 形式で指定します。 *active_end_date*は**int**,、既定値は NULL です。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`マージエージェントを最初にスケジュール設定する時刻を HHMMSS 形式で指定します。 *active_start_time_of_day* は **int** 、既定値は NULL です。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`マージエージェントのスケジュール設定を停止する時刻を HHMMSS 形式で指定します。 *active_end_time_of_day*は**int**,、既定値は NULL です。  
  
`[ @job_login = ] 'job_login'`パラメーター化された行フィルターを使用してサブスクリプションのスナップショットを生成するときに、スナップショットエージェントを実行するWindowsアカウントを指定します。[!INCLUDE[msCoName](../../includes/msconame-md.md)] *job_login*は**nvarchar (257)** ,、既定の値は NULL です。  
  
`[ @job_password = ] 'job_password'`パラメーター化された行フィルターを使用してサブスクリプションのスナップショットを生成するときに、スナップショットエージェントを実行する Windows アカウントのパスワードを指定します。 *job_password*は**nvarchar (257)** ,、既定の値は NULL です。  
  
> [!IMPORTANT]  
>  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_changedynamicsnapshot_job**は、パラメーター化された行フィルターを使用したパブリケーションのマージレプリケーションで使用されます。  
  
 エージェントのログインまたはパスワードを変更した後、変更を有効にするには、エージェントを停止して再起動する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_changedynamicsnapshot_job**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [レプリケーションのセキュリティ設定の表示および変更](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [パラメーター化されたフィルターを使用したマージ パブリケーションのスナップショット](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
  
