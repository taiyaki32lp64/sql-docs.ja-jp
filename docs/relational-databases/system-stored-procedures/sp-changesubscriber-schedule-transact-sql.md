---
title: sp_changesubscriber_schedule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubscriber_schedule
- sp_changesubscriber_schedule_TSQL
helpviewer_keywords:
- sp_changesubscriber_schedule
ms.assetid: ff84e8e2-d496-482c-b23e-38a6626596e6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 22ecb1601108562607d1fdc550daaa945fe72910
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770733"
---
# <a name="spchangesubscriberschedule-transact-sql"></a>sp_changesubscriber_schedule (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  サブスクライバーのディストリビューション エージェントまたはマージ エージェントのスケジュールを変更します。 このストアドプロシージャは、パブリッシャー側で任意のデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changesubscriber_schedule [ @subscriber = ] 'subscriber', [ @agent_type = ] type  
    [ , [ @frequency_type = ] frequency_type ]  
    [ , [ @frequency_interval = ] frequency_interval ]  
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday = ] frequency_subday ]  
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]  
    [ , [ @active_start_date = ] active_start_date ]  
    [ , [ @active_end_date = ] active_end_date ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @subscriber = ] 'subscriber'`サブスクライバーの名前を指定します。 *サブスクライバー*は**sysname**です。 サブスクライバーの名前はデータベース内で一意である必要があり、存在しない場合は NULL にすることはできません。  
  
`[ @agent_type = ] type`エージェントの種類を示します。 *種類*は**smallint**,、既定値は**0**です。 **0**はディストリビューションエージェントを示します。 **1**はマージエージェントを示します。  
  
`[ @frequency_type = ] frequency_type`ディストリビューションタスクをスケジュールする頻度を指定します。 *frequency_type*は**int**,、既定値は**64**です。 スケジュール列は10個あります。  
  
`[ @frequency_interval = ] frequency_interval`*Frequency_type*によって設定された頻度に適用される値を指定します。 *frequency_interval*は**int**,、既定値は**1**です。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`ディストリビューションタスクの日付を指定します。 *frequency_relative_interval*は**int**,、既定値は**1**です。  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*によって使用される定期実行係数を示します。 *frequency_recurrence_factor*は**int**,、既定値は**0**です。  
  
`[ @frequency_subday = ] frequency_subday`定義した期間にスケジュールを再設定する頻度を分単位で指定します。 *frequency_subday*は**int**,、既定値は**4**です。  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*の間隔を指定します。 *frequency_subday_interval*は**int**,、既定値は**5**です。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`ディストリビューションタスクを最初にスケジュール設定する時刻を示します。 *active_start_time_of_day*は**int**,、既定値は**0**です。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`ディストリビューションタスクのスケジュール設定を停止する時刻を設定します。 *active_end_time_of_day*は**int**,、既定値は**235959**,、11:59:59 pm 午後 11 時 59 分 59 秒を意味します。  
  
`[ @active_start_date = ] active_start_date`ディストリビューションタスクを最初にスケジュール設定する日付を YYYYMMDD 形式で指定します。 *active_start_date*は**int**,、既定値は**0**です。  
  
`[ @active_end_date = ] active_end_date`ディストリビューションタスクのスケジュール設定を停止する日付を YYYYMMDD 形式で指定します。 *active_end_date*は**int**,、既定値は**99991231**,、9999年12月31日を意味します。  
  
`[ @publisher = ] 'publisher'`[!INCLUDE[msCoName](../../includes/msconame-md.md)] 以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーを指定します。 *publisher*は**sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーでアーティクルの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]プロパティを変更する場合は、パブリッシャーを使用しないでください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_changesubscriber_schedule**は、すべての種類のレプリケーションで使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_changesubscriber_schedule**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [sp_addsubscriber_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-schedule-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
