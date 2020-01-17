---
title: sp_helppublication_snapshot (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppublication_snapshot
- sp_helppublication_snapshot_TSQL
helpviewer_keywords:
- sp_helppublication_snapshot
ms.assetid: 97b4a7ae-40a5-4328-88f1-ff5d105bbb34
author: stevestein
ms.author: sstein
ms.openlocfilehash: d8909396e7a7da39ed2ae27c475a154c58bad090
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771502"
---
# <a name="sphelppublicationsnapshot-transact-sql"></a>sp_helppublication_snapshot (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  指定されたパブリケーションのスナップショットエージェントに関する情報を返します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helppublication_snapshot [ @publication = ] 'publication'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @publisher = ] 'publisher'`以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーを指定します。 *publisher*は**sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーにアーティクルを追加する場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーを使用しないでください。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|スナップショットエージェントの ID。|  
|**name**|**nvarchar(100)**|スナップショットエージェントの名前。|  
|**publisher_security_mode**|**smallint**|パブリッシャーに接続するときにエージェントによって使用されるセキュリティモード。次のいずれかになります。<br /><br /> **0**  = 認証[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> **1** = Windows 認証。|  
|**publisher_login**|**sysname**|パブリッシャーに接続するときに使用されるログインです。|  
|**publisher_password**|**nvarchar(524)**|セキュリティ上の理由から、の **\* \* \* \* \* 値は\*常に返されます。\* \* \* \***|  
|**job_id**|**uniqueidentifier**|エージェントジョブの一意の ID。|  
|**job_login**|**nvarchar(512)**|スナップショットエージェントを実行する Windows アカウントを指定します。このアカウントは、"*ドメイン*\\*ユーザー名*" の形式で返されます。|  
|**job_password**|**sysname**|セキュリティ上の理由から、の **\* \* \* \* \* 値は\*常に返されます。\* \* \* \***|  
|**schedule_name**|**sysname**|このエージェントジョブに使用するスケジュールの名前。|  
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
 **sp_help_publication_snapshot**は、すべての種類のレプリケーションで使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_help_publication_snapshot**を実行できるのは、パブリッシャー側の**sysadmin**固定サーバーロールのメンバー、またはパブリケーションデータベースの**db_owner**固定データベースロールのメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [パブリケーション プロパティの表示および変更](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addpublication_snapshot &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication_snapshot &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [sp_dropmergepublication &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_droppublication &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)  
  
  
