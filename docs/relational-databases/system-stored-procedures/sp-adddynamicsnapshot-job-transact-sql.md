---
title: sp_adddynamicsnapshot_job (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adddynamicsnapshot_job
- sp_adddynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_adddynamicsnapshot_job
ms.assetid: ef50ccf6-e360-4e4b-91b9-6706b8fabefa
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 48f94f7fcf823a9ed9acc519e393369e44b45302
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771341"
---
# <a name="spadddynamicsnapshotjob-transact-sql"></a>sp_adddynamicsnapshot_job (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  パラメーター化された行フィルターを使用して、パブリケーションのフィルター選択されたデータスナップショットを生成するエージェントジョブを作成します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。 このストアドプロシージャは、サブスクライバー用にフィルター選択されたデータスナップショットジョブを手動で作成するために管理者によって使用されます。  
  
> [!NOTE]  
>  フィルター選択されたデータスナップショットジョブを作成するには、パブリケーションの標準スナップショットジョブが既に存在している必要があります。  
  
 詳しくは、「 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」をご覧ください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_adddynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @suser_sname = ] 'suser_sname' ]   
    [ , [ @host_name = ] 'host_name' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' OUTPUT ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' OUTPUT ]   
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`フィルター選択されたデータスナップショットジョブを追加するパブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @suser_sname = ] 'suser_sname'`サブスクライバー側で[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)関数の値によってフィルター選択されるサブスクリプションのフィルター選択されたデータスナップショットを作成するときに使用する値を指定します。 *suser_sname*の**sysname**,、既定値はありません。 パブリケーションを動的にフィルター選択するためにこの関数を使用しない場合、 *suser_sname*は NULL にする必要があります。  
  
`[ @host_name = ] 'host_name'`サブスクリプションのフィルター選択されたデータスナップショットを作成するときに使用する値を指定します。この値は、サブスクライバー側で[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)関数の値によってフィルター処理されます。 *host_name*は**sysname**,、既定値はありません。 この関数を使用せずにパブリケーションを動的にフィルター選択する場合は、 *host_name*を NULL にする必要があります。  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'`作成するフィルター選択されたデータスナップショットジョブの名前を指定します。 *dynamic_snapshot_jobname*は**sysname**で、既定値は NULL です。これは省略可能な出力パラメーターです。 指定した場合、 *dynamic_snapshot_jobname*はディストリビューターで一意のジョブに解決される必要があります。 指定しない場合、ジョブ名が自動的に生成され、結果セットに返されます。この名前は次のように作成されます。  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
> [!NOTE]  
>  動的スナップショットジョブの名前を生成するときに、標準スナップショットジョブの名前を切り捨てることができます。  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'`作成するフィルター選択されたデータスナップショットジョブの識別子を選択します。 *dynamic_snapshot_jobid*は**uniqueidentifier**,、既定値は NULL の場合、は省略可能な出力パラメーターです。  
  
`[ @frequency_type = ] frequency_type`フィルター選択されたデータスナップショットジョブをスケジュールする頻度を指定します。 *frequency_type*は**int**,、これらの値のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|指定日時|  
|**2**|[要求時]|  
|**4** (既定値)|毎日。|  
|**8**|毎週。|  
|**16**|毎月。|  
|**32**|月単位の相対|  
|**64**|自動開始|  
|**128**|定期|  
  
`[ @frequency_interval = ] frequency_interval`フィルター選択されたデータスナップショットジョブを実行する期間 (日数単位) です。 *frequency_interval*は**int**,、既定値は 1,、 *frequency_type*の値に依存します。  
  
|*Frequency_type*の値|*Frequency_interval*への影響|  
|--------------------------------|-------------------------------------|  
|**1**|*frequency_interval*は使用されていません。|  
|**4** (既定値)|*Frequency_interval*日ごと。既定値は毎日です。|  
|**8**|*frequency_interval*は、次のうちの1つ以上 ( [ &#124; &#40;ビットごとの&#41; &#40;&#41; or transact-sql](../../t-sql/language-elements/bitwise-or-transact-sql.md)論理演算子と組み合わせたもの) です。<br /><br /> **1** = 日曜日&#124; **2** = 月曜日&#124; **4** = 火曜日&#124; **8** = 水曜日&#124; **16** = 木曜日&#124; **32** = 金曜&#124; **64** = 土曜日|  
|**16**|月の*frequency_interval*日。|  
|**32**|*frequency_interval*は次のいずれかです。<br /><br /> **1** = 日曜日&#124; **2** = 月曜日&#124; **3** = 火曜日&#124; **4** = 水曜日&#124; **5** = 木曜日&#124; **6** = 金曜日&#124; **7** = 土曜日&#124; **8** = 日&#124;**9** = 平日&#124; **10** = 週末|  
|**64**|*frequency_interval*は使用されていません。|  
|**128**|*frequency_interval*は使用されていません。|  
  
`[ @frequency_subday = ] frequency_subday`*Frequency_subday_interval*の単位を指定します。 *frequency_subday*は**int**,、これらの値のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|1 回。|  
|**2**|Second|  
|**4** (既定値)|Minute|  
|**8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`ジョブの各実行間に発生する*frequency_subday*期間の数を指定します。 *frequency_subday_interval*は**int**,、既定値は5です。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`毎月のフィルター選択されたデータスナップショットジョブの発生を示します。 このパラメーターが使用されるときに *frequency_type* に設定されている **32** (月単位)。 *frequency_relative_interval*は**int**,、これらの値のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1** (既定値)|First|  
|**2**|第 2 週|  
|**4**|サードパーティ|  
|**8**|4 番目|  
|**16**|Last|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*によって使用される定期実行係数を示します。 *frequency_recurrence_factor*は**int**,、既定値は0です。  
  
`[ @active_start_date = ] active_start_date`フィルター選択されたデータスナップショットジョブを最初にスケジュール設定する日付を YYYYMMDD 形式で指定します。 *active_start_date*は**int**,、既定値は NULL です。  
  
`[ @active_end_date = ] active_end_date`フィルター選択されたデータスナップショットジョブのスケジュール設定を停止する日付を YYYYMMDD 形式で指定します。 *active_end_date*は**int**,、既定値は NULL です。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`フィルター選択されたデータスナップショットジョブを最初にスケジュール設定する時刻を HHMMSS 形式で指定します。 *active_start_time_of_day* は **int** 、既定値は NULL です。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`フィルター選択されたデータスナップショットジョブのスケジュール設定を停止する時刻を HHMMSS 形式で指定します。 *active_end_time_of_day*は**int**,、既定値は NULL です。  
  
## <a name="result-set"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|[Msdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md)システムテーブル内のフィルター選択されたデータスナップショットジョブを識別します。|  
|**dynamic_snapshot_jobname**|**sysname**|フィルター選択されたデータスナップショットジョブの名前。|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|ディストリビューター側の[!INCLUDE[msCoName](../../includes/msconame-md.md)]エージェントジョブを[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]一意に識別します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_adddynamicsnapshot_job**は、パラメーター化されたフィルターを使用するパブリケーションのマージレプリケーションで使用します。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-adddynamicsnapshot-jo_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_adddynamicsnapshot_job**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [パラメーター化されたフィルターを使用してマージパブリケーションのスナップショットを作成する](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [sp_dropdynamicsnapshot_job &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md)   
 [sp_helpdynamicsnapshot_job &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md)  
  
  
