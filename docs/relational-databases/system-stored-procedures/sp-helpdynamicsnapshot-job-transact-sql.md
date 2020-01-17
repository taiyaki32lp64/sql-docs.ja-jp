---
title: sp_helpdynamicsnapshot_job (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdynamicsnapshot_TSQL
- sp_helpdynamicsnapshot_job_TSQL
- job_TSQL
- helpdynamicsnapshot
- job
- sp_helpdynamicsnapshot
- sp_helpdynamicsnapshot_job
- helpdynamicsnapshot_TSQL
helpviewer_keywords:
- sp_helpdynamicsnapshot_job
ms.assetid: d6dfdf26-f874-495f-a8a6-8780699646d7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 55d7ad0dfd941102cfeb6661e65980f980fa8b2d
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770985"
---
# <a name="sphelpdynamicsnapshotjob-transact-sql"></a>sp_helpdynamicsnapshot_job (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  フィルター処理されたデータ スナップショットを生成するエージェント ジョブに関する情報を返します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpdynamicsnapshot_job [ [ @publication = ] 'publication' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *publication*のデータ型は**sysname**で、 **%** 既定値はで、指定した*dynamic_snapshot_jobid*と*dynamic_snapshot_jobname*に一致するすべてのフィルター選択されたデータスナップショットジョブに関する情報を返します。レプリケーション.  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'`フィルター選択されたデータスナップショットジョブの名前を指定します。 *dynamic_snapshot_jobname*は**sysname**で、既定値 **%** は ' です。これは、指定された*dynamic_snapshot_jobid*を持つパブリケーションのすべての動的ジョブを返します。 ジョブの作成時にジョブ名が明示的に指定されなかった場合、ジョブ名は次の形式になります。  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'`フィルター選択されたデータスナップショットジョブの識別子を選択します。 *dynamic_snapshot_jobid*は**uniqueidentifier**,、既定値は NULL の場合、指定された*dynamic_snapshot_jobname*に一致するすべてのスナップショットジョブを返します。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|フィルター選択されたデータスナップショットジョブを識別します。|  
|**job_name**|**sysname**|フィルター選択されたデータスナップショットジョブの名前。|  
|**job_id**|**uniqueidentifier**|ディストリビューター側[!INCLUDE[msCoName](../../includes/msconame-md.md)]のエージェントジョブを[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]識別します。|  
|**dynamic_filter_login**|**sysname**|パブリケーションに対して定義されたパラメーター化された行フィルターで[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)関数を評価するために使用される値です。|  
|**dynamic_filter_hostname**|**sysname**|パブリケーションに対して定義されたパラメーター化された行フィルターで[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)関数を評価するために使用される値です。|  
|**dynamic_snapshot_location**|**nvarchar (255)**|パラメーター化された行フィルターが使用されている場合に、スナップショットファイルの読み取り元フォルダーへのパス。|  
|**frequency_type**|**int**|エージェントの実行スケジュールを設定する頻度を指定します。次のいずれかの値を指定できます。<br /><br /> **1** = 1 回<br /><br /> **2** = 要求時<br /><br /> **4** = 日単位<br /><br /> **8** = 週単位<br /><br /> **16** = 月単位<br /><br /> **32** = 毎月の相対<br /><br /> **64** = 自動開始<br /><br /> **128** = 定期的|  
|**frequency_interval**|**int**|エージェントの実行日。次のいずれかの値になります。<br /><br /> **1** = 日曜日<br /><br /> **2** = 月曜日<br /><br /> **3** = 火曜日<br /><br /> **4** = 水曜日<br /><br /> **5** = 木曜日<br /><br /> **6** = 金曜日<br /><br /> **7** = 土曜日<br /><br /> **8** = 日<br /><br /> **9** = 平日<br /><br /> **10** = 週末|  
|**frequency_subday_type**|**int**|*Frequency_type*が**4** (毎日) の場合にエージェントを実行する頻度を定義する型です。これらの値のいずれかを指定できます。<br /><br /> **1** = 指定された時間<br /><br /> **2** = 秒<br /><br /> **4** = 分<br /><br /> **8** = 時間|  
|**frequency_subday_interval**|**int**|エージェントのスケジュールされた実行の間に発生する*frequency_subday_type*の間隔の数。|  
|**frequency_relative_interval**|**int**|*Frequency_type*が**32** (月単位) の場合に、特定の月にエージェントが実行される週を指定します。次のいずれかの値を指定できます。<br /><br /> **1** = 最初<br /><br /> **2** = 秒<br /><br /> **4** = 3 番目<br /><br /> **8** = 4 番目<br /><br /> **16** = 最後|  
|**frequency_recurrence_factor**|**int**|エージェントのスケジュールされた実行の間隔を週または月単位で指定します。|  
|**active_start_date**|**int**|エージェントの最初の実行予定日。日付の形式は YYYYMMDD です。|  
|**active_end_date**|**int**|エージェントの最後の実行予定日 (YYYYMMDD 形式)。|  
|**active_start_time**|**int**|エージェントの最初の実行予定時刻。時刻の形式は HHMMSS です。|  
|**active_end_time**|**int**|エージェントの実行が最後にスケジュールされた時刻 (HHMMSS 形式)。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helpdynamicsnapshot_job**は、マージレプリケーションで使用します。  
  
 すべての既定のパラメーター値が使用されている場合は、パブリケーションデータベース全体について、パーティション分割されたすべてのデータスナップショットジョブに関する情報が返されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helpdynamicsnapshot_job**を実行できるのは、 **sysadmin**固定サーバーロールのメンバー、 **db_owner**固定データベースロール、およびパブリケーションのパブリケーションアクセスリストのメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
