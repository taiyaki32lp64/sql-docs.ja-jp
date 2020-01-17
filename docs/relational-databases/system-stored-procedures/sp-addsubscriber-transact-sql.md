---
title: sp_addsubscriber (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addsubscriber
- sp_addsubscriber_TSQL
helpviewer_keywords:
- sp_addsubscriber
ms.assetid: b8a584ea-2a26-4936-965b-b84f026e39c0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 278af2ca1bd6abdb84cdf2371628c6b95662e46e
ms.sourcegitcommit: eae9efe2a2d3758685e85039ffb8fa698aa47f9b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73962409"
---
# <a name="sp_addsubscriber-transact-sql"></a>sp_addsubscriber (Transact-sql)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  パブリッシャーに新しいサブスクライバーを追加し、サブスクライバーがパブリケーションを受け取れるようにします。 このストアドプロシージャは、パブリッシャー側のパブリケーションデータベースで、スナップショットパブリケーションおよびトランザクションパブリケーションに対して実行されます。また、リモートディストリビューターを使用するマージパブリケーションの場合、このストアドプロシージャはディストリビューター側で実行されます。  
  
> [!IMPORTANT]  
>  このストアドプロシージャは非推奨とされます。 パブリッシャーでサブスクライバーを明示的に登録する必要がなくなりました。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addsubscriber [ @subscriber = ] 'subscriber'  
    [ , [ @type = ] type ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @commit_batch_size = ] commit_batch_size ]  
    [ , [ @status_batch_size = ] status_batch_size ]  
    [ , [ @flush_frequency = ] flush_frequency ]  
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
    [ , [ @description = ] 'description' ]  
    [ , [ @security_mode = ] security_mode ]  
    [ , [ @encrypted_password = ] encrypted_password ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @subscriber = ] 'subscriber'`、このサーバー上のパブリケーションに有効なサブスクライバーとして追加するサーバーの名前を指定します。 *subscriber*は**sysname**、既定値はありません。  
  
`[ @type = ] type` はサブスクライバーの種類です。 *種類*は**tinyint**で、次のいずれかの値を指定できます。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**0** (既定値)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバーの [!INCLUDE[msCoName](../../includes/msconame-md.md)]|  
|**1**|ODBC データソースサーバー|  
|**2**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet データベース|  
|**3**|OLE DB プロバイダー|  
  
`[ @login = ] 'login'` は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証のログイン ID です。 *login* のデータ型は **sysname** で、既定値は NULL です。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @password = ] 'password'` は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証用のパスワードです。 *パスワード*は**nvarchar (524)** ,、既定値は NULL です。  
  
> [!IMPORTANT]  
>  空白のパスワードは使用しないでください。 強力なパスワードを使用してください。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @commit_batch_size = ] commit_batch_size` このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。  
  
> [!NOTE]  
>  この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @status_batch_size = ] status_batch_size` このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。  
  
> [!NOTE]  
>  この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @flush_frequency = ] flush_frequency` このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。  
  
> [!NOTE]  
>  この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @frequency_type = ] frequency_type` には、レプリケーションエージェントをスケジュールする頻度を指定します。 *frequency_type*は**int**,、これらの値のいずれかを指定できます。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**1**|指定日時|  
|**2**|[要求時]|  
|**4**|毎日。|  
|**8**|毎週。|  
|**16**|毎月。|  
|**32**|月単位の相対|  
|**64** (既定値)|自動開始|  
|**128**|定期|  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @frequency_interval = ] frequency_interval` は、 *frequency_type*によって設定された頻度に適用される値です。 *frequency_interval*は**int**,、既定値は1です。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` レプリケーションエージェントの日付を指定します。 このパラメーターが使用されるときに *frequency_type* に設定されている **32** (月単位)。 *frequency_relative_interval*は**int**,、これらの値のいずれかを指定できます。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**1** (既定値)|First|  
|**2**|第 2 週|  
|**4**|第 3 週|  
|**8**|Fourth|  
|**16**|Last|  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` は、 *frequency_type*によって使用される定期実行係数です。 *frequency_recurrence_factor*は**int**,、既定値は**0**です。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @frequency_subday = ] frequency_subday` は、定義された期間中に再スケジュールされる頻度です。 *frequency_subday*は**int**,、これらの値のいずれかを指定できます。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**1**|1 回。|  
|**2**|第 2 週|  
|**4** (既定値)|Minute|  
|**8**|Hour|  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` は*frequency_subday*の間隔です。 *frequency_subday_interval*は**int**,、既定値は**5**です。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` は、レプリケーションエージェントを最初にスケジュール設定する時刻を HHMMSS 形式で指定します。 *active_start_time_of_day*は**int**,、既定値は**0**です。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` は、レプリケーションエージェントのスケジュール設定を停止する時刻を HHMMSS 形式で指定します。 *active_end_time_of_day*は**int**,、既定値は 235959,、11:59:59 pm 24時間制として測定されます。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @active_start_date = ] active_start_date` は、レプリケーションエージェントを最初にスケジュール設定する日付を YYYYMMDD 形式で指定します。 *active_start_date*は**int**,、既定値は0です。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @active_end_date = ] active_end_date` は、レプリケーションエージェントのスケジュール設定を停止する日付を YYYYMMDD 形式で指定します。 *active_end_date*は**int**,、既定値は 99991231,、9999年12月31日を意味します。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @description = ] 'description'` は、サブスクライバーの説明テキストです。 *説明*は**nvarchar (255)** ,、既定値は NULL です。  
  
`[ @security_mode = ] security_mode` は、実装されているセキュリティモードです。 *security_mode*は**int**,、既定値は1です。 **0** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を指定します。 **1** Windows 認証を指定します。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
このパラメーターは非推奨とされており、旧バージョンとの互換性のみの設定のために提供されており、任意の値に*encrypted_password*ますが、 **0**を指定するとエラーが発生します。 `[ @encrypted_password = ] encrypted_password`  
  
`[ @publisher = ] 'publisher'` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリッシャーを指定します。 *publisher*は**sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パブリッシャーから発行する場合は、*パブリッシャー*を使用しないでください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>Remarks  
 **sp_addsubscriber**は、スナップショットレプリケーション、トランザクションレプリケーション、およびマージレプリケーションで使用します。  
  
 サブスクライバーがマージパブリケーションへの匿名サブスクリプションのみを持つ場合、 **sp_addsubscriber**は必要ありません。  
  
 **sp_addsubscriber**は、**ディストリビューション**データベースの[MSsubscriber_info](../../relational-databases/system-tables/mssubscriber-info-transact-sql.md)テーブルに書き込みます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addsubscriber**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [プル サブスクリプションの作成](../../relational-databases/replication/create-a-pull-subscription.md)   
 [sp_changesubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)  
  
  
