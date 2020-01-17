---
title: sp_addpublication_snapshot (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpublication_snapshot_TSQL
- sp_addpublication_snapshot
helpviewer_keywords:
- sp_addpublication_snapshot
ms.assetid: 192b6214-df6e-44a3-bdd4-9d933a981619
author: stevestein
ms.author: sstein
ms.openlocfilehash: c32ea67eef368a17b129989e3f05c29ab0533d72
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769110"
---
# <a name="spaddpublicationsnapshot-transact-sql"></a>sp_addpublication_snapshot (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  指定されたパブリケーションのスナップショット エージェントを作成します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
> [!IMPORTANT]  
>  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addpublication_snapshot [ @publication= ] 'publication'  
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
    [ , [ @snapshot_job_name = ] 'snapshot_agent_name' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @frequency_type = ] frequency_type`スナップショットエージェントを実行する頻度を指定します。 *frequency_type*は**int**,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|1 回のみ|  
|**4** (既定値)|毎日|  
|**8**|業務.|  
|**16**|支払い.|  
|**32**|月単位に frequency_interval で示される間隔|  
|**64**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントの起動時。|  
|**128**|コンピューターがアイドル状態のときに実行する|  
  
`[ @frequency_interval = ] frequency_interval`*Frequency_type*によって設定された頻度に適用する値を指定します。 *frequency_interval*は**int**,、値は次のいずれかを指定することができます。  
  
|Frequency_type の値|frequency_interval への影響|  
|------------------------------|-----------------------------------|  
|**1**|*frequency_interval*は使用されていません。|  
|**4** (既定値)|*Frequency_interval*日ごと。既定値は毎日です。|  
|**8**|*frequency_interval*は、次のうちの1つ以上 ( [ &#124;ビットごとの or)](../../t-sql/language-elements/bitwise-or-transact-sql.md)論理演算子と組み合わせたものです。<br /><br /> **1** = 日曜日&#124;<br /><br /> **2** = 月曜日&#124;<br /><br /> **4** = 火曜日&#124;<br /><br /> **8** = 水曜日&#124;<br /><br /> **16** = 木曜日&#124;<br /><br /> **32** = 金曜日&#124;<br /><br /> **64** = 土曜日|  
|**16**|月の*frequency_interval*日。|  
|**32**|*frequency_interval*は次のいずれかです。<br /><br /> **1** = 日曜日&#124;<br /><br /> **2** = 月曜日&#124;<br /><br /> **3** = 火曜日&#124;<br /><br /> **4** = 水曜日&#124;<br /><br /> **5** = 木曜日&#124;<br /><br /> **6** = 金曜日&#124;<br /><br /> **7** = 土曜日&#124;<br /><br /> **8** = 日&#124;<br /><br /> **9** = 平日&#124;<br /><br /> **10** = 週末|  
|**64**|*frequency_interval*は使用されていません。|  
|**128**|*frequency_interval*は使用されていません。|  
  
`[ @frequency_subday = ] frequency_subday`*Freq_subday_interval*の単位を示します。 *frequency_subday*は**int**,、これらの値のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|1 回。|  
|**2**|Second|  
|**4** (既定値)|Minute|  
|**8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*の間隔を指定します。 *frequency_subday_interval*は**int**,、既定値は5の場合は5分ごとです。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`スナップショットエージェントが実行される日付を指定します。 *frequency_relative_interval*は**int**,、既定値は1です。  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*によって使用される定期実行係数を示します。 *frequency_recurrence_factor*は**int**,、既定値は0です。  
  
`[ @active_start_date = ] active_start_date`スナップショットエージェントを最初にスケジュール設定する日付を YYYYMMDD 形式で指定します。 *active_start_date*は**int**,、既定値は0です。  
  
`[ @active_end_date = ] active_end_date`スナップショットエージェントのスケジュール設定を停止する日付を YYYYMMDD 形式で指定します。 *active_end_date*は**int**,、既定値は 99991231,、9999年12月31日を意味します。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`スナップショットエージェントを最初にスケジュール設定する時刻を HHMMSS 形式で指定します。 *active_start_time_of_day*は**int**,、既定値は0です。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`スナップショットエージェントのスケジュール設定を停止する時刻を HHMMSS 形式で指定します。 *active_end_time_of_day*は**int**,、既定値は 235959,、11:59:59 pm 24時間制として測定されます。  
  
`[ @snapshot_job_name = ] 'snapshot_agent_name'`既存のジョブが使用されている場合は、既存のスナップショットエージェントジョブ名の名前を指定します。 *snapshot_agent_name*は**nvarchar (100)** 、既定値は NULL です。 このパラメーターは内部で使用するため、新しいパブリケーションを作成するときには指定しないでください。 *Snapshot_agent_name*を指定する場合は、 *job_login*と*job_password*を NULL にする必要があります。  
  
`[ @publisher_security_mode = ] publisher_security_mode`パブリッシャーに接続するときにエージェントが使用するセキュリティモードを示します。 *publisher_security_mode*は**smallint**,、既定値は1です。 **0 は認証を**、1は Windows 認証を指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーには、値**0**を指定する必要があります。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'`パブリッシャーに接続するときに使用するログインを示します。 *publisher_login* は **sysname** 、既定値は NULL です。 *publisher_security_mode*が**0**の場合は、 *publisher_login*を指定する必要があります。 *Publisher_login*が NULL で、 *publisher_security_mode*が**1**の場合は、 *job_login*に指定されたアカウントがパブリッシャーに接続するときに使用されます。  
  
`[ @publisher_password = ] 'publisher_password'`パブリッシャーに接続するときに使用するパスワードを入力します。 *publisher_password* は **sysname** 、既定値は NULL です。  
  
> [!IMPORTANT]  
>  認証情報をスクリプトファイルに保存しないでください。 セキュリティを強化するために、実行時にログイン名とパスワードを指定することをお勧めします。  
  
`[ @job_login = ] 'job_login'`エージェントを実行するアカウントのログインを指定します。 Azure SQL Database Managed Instance で、SQL Server アカウントを使用します。 *job_login*は**nvarchar (257)** ,、既定値は NULL です。 このアカウントは、ディストリビューターへのエージェント接続に常に使用されます。 新しいスナップショットエージェントジョブを作成するときに、このパラメーターを指定する必要があります。  
  
> [!NOTE]
>  以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーの場合は、 [sp_adddistpublisher &#40;&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)で指定されたログインと同じである必要があります。  
  
`[ @job_password = ] 'job_password'`エージェントを実行する Windows アカウントのパスワードを指定します。 *job_password* は **sysname** 、既定値はありません。 新しいスナップショットエージェントジョブを作成するときに、このパラメーターを指定する必要があります。  
  
> [!IMPORTANT]  
>  認証情報をスクリプトファイルに保存しないでください。 セキュリティを強化するために、実行時にログイン名とパスワードを指定することをお勧めします。  
  
`[ @publisher = ] 'publisher'`以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーを指定します。 *publisher*は**sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーで[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スナップショットエージェントを作成する場合は、パブリッシャーを使用しないでください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_addpublication_snapshot**は、スナップショットレプリケーション、トランザクションレプリケーション、およびマージレプリケーションで使用します。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-snapsh_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addpublication_snapshot**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [スナップショットの作成および適用](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [sp_addpublication &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication_snapshot &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [sp_startpublication_snapshot &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
