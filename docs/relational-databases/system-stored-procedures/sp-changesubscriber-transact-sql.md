---
title: sp_changesubscriber (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubscriber
- sp_changesubscriber_TSQL
helpviewer_keywords:
- sp_changesubscriber
ms.assetid: d453c451-e957-490f-b968-5e03aeddaf10
author: stevestein
ms.author: sstein
ms.openlocfilehash: 42b56712e8b441184d55bf12ce16dbcb55930374
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68762782"
---
# <a name="spchangesubscriber-transact-sql"></a>sp_changesubscriber (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  サブスクライバーのオプションを変更します。 このパブリッシャーのサブスクライバーに対するディストリビューション タスクはすべて更新されます。 このストアドプロシージャは、ディストリビューションデータベースの**MSsubscriber_info**テーブルに書き込みます。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changesubscriber [ @subscriber= ] 'subscriber'  
    [ , [ @type= ] type ]  
    [ , [ @login= ] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @commit_batch_size= ] commit_batch_size ]  
    [ , [ @status_batch_size= ] status_batch_size ]  
    [ , [ @flush_frequency= ] flush_frequency ]  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @security_mode= ] security_mode ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @subscriber = ] 'subscriber'`オプションを変更するサブスクライバーの名前を指定します。 *サブスクライバー*は**sysname**,、既定値はありません。  
  
`[ @type = ] type`サブスクライバーの種類を示します。 *種類*は**tinyint**,、既定値は NULL です。 **0**はサブスクライバー [!INCLUDE[msCoName](../../includes/msconame-md.md)]を[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]示します。 **1** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は、以外の ODBC データソースサーバーサブスクライバーを指定します。  
  
`[ @login = ] 'login'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証ログイン ID を示します。 *login* のデータ型は **sysname** で、既定値は NULL です。  
  
`[ @password = ] 'password'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証パスワードを入力します。 *パスワード*は**sysname**,、既定値 **%** はです。 **%** password プロパティが変更されていないことを示します。  
  
`[ @commit_batch_size = ] commit_batch_size`旧バージョンとの互換性のためにのみサポートされています。  
  
`[ @status_batch_size = ] status_batch_size`旧バージョンとの互換性のためにのみサポートされています。  
  
`[ @flush_frequency = ] flush_frequency`旧バージョンとの互換性のためにのみサポートされています。  
  
`[ @frequency_type = ] frequency_type`ディストリビューションタスクをスケジュールする頻度を指定します。 *frequency_type*は**int**,、これらの値のいずれかを指定することができます。  
  
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
  
`[ @frequency_interval = ] frequency_interval`*Frequency_type*の間隔を指定します。 *frequency_interval*は**int**,、既定値は NULL です。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`ディストリビューションタスクの日付を指定します。 このパラメーターが使用されるときに *frequency_type* に設定されている **32** (月単位)。 *frequency_relative_interval*は**int**,、これらの値のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|First|  
|**2**|第 2 週|  
|**4**|サードパーティ|  
|**8**|4 番目|  
|**16**|Last|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`定義された*frequency_type*中にディストリビューションタスクを繰り返す頻度を指定します。 *frequency_recurrence_factor*は**int**,、既定値は NULL です。  
  
`[ @frequency_subday = ] frequency_subday`定義した期間中に再スケジュールする頻度を指定します。 *frequency_subday*は**int**,、これらの値のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|1 回。|  
|**2**|第 2 週|  
|**4**|Minute|  
|**8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequence_subday*の間隔を指定します。 *frequency_subday_interval*は**int**,、既定値は NULL です。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`ディストリビューションタスクを最初にスケジュール設定する時刻を HHMMSS 形式で指定します。 *active_start_time_of_day* は **int** 、既定値は NULL です。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`ディストリビューションタスクのスケジュール設定を停止する時刻を HHMMSS 形式で指定します。 *active_end_time_of_day*は**int**,、既定値は NULL です。  
  
`[ @active_start_date = ] active_start_date`ディストリビューションタスクを最初にスケジュール設定する日付を YYYYMMDD 形式で指定します。 *active_start_date*は**int**,、既定値は NULL です。  
  
`[ @active_end_date = ] active_end_date`ディストリビューションタスクのスケジュール設定を停止する日付を YYYYMMDD 形式で指定します。 *active_end_date*は**int**,、既定値は NULL です。  
  
`[ @description = ] 'description'`省略可能なテキストの説明を指定します。 *説明*は**nvarchar (255)** ,、既定値は NULL です。  
  
`[ @security_mode = ] security_mode`実装されているセキュリティモードです。 *security_mode*は**int**,、これらの値のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [認証]|  
|**1**|[Windows 認証]|  
  
`[ @publisher = ] 'publisher'`以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーを指定します。 *publisher*は**sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーでアーティクルの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]プロパティを変更する場合は、パブリッシャーを使用しないでください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_changesubscriber**は、すべての種類のレプリケーションで使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_changesubscriber**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [sp_addsubscriber &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
