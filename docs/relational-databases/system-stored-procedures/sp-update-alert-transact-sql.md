---
title: sp_update_alert (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_alert_TSQL
- sp_update_alert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_alert
ms.assetid: 4bbaeaab-8aca-4c9e-abc1-82ce73090bd3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2856f89264994b9f1812653450d94e2cb2e2b0c2
ms.sourcegitcommit: cbbb210c0315f9e2be2b9cd68db888ac53429814
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69890843"
---
# <a name="sp_update_alert-transact-sql"></a>sp_update_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  既存のアラートの設定を更新します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_update_alert   
     [ @name =] 'name'   
     [ , [ @new_name =] 'new_name']   
     [ , [ @enabled =] enabled]   
     [ , [ @message_id =] message_id]   
     [ , [ @severity =] severity]   
     [ , [ @delay_between_responses =] delay_between_responses]   
     [ , [ @notification_message =] 'notification_message']   
     [ , [ @include_event_description_in =] include_event_description_in]   
     [ , [ @database_name =] 'database']   
     [ , [ @event_description_keyword =] 'event_description_keyword']   
     [ , [ @job_id =] job_id | [@job_name =] 'job_name']   
     [ , [ @occurrence_count = ] occurrence_count]   
     [ , [ @count_reset_date =] count_reset_date]   
     [ , [ @count_reset_time =] count_reset_time]   
     [ , [ @last_occurrence_date =] last_occurrence_date]   
     [ , [ @last_occurrence_time =] last_occurrence_time]   
     [ , [ @last_response_date =] last_response_date]   
     [ , [ @last_response_time =] last_response _time]  
     [ , [ @raise_snmp_trap =] raise_snmp_trap]  
     [ , [ @performance_condition =] 'performance_condition' ]   
     [ , [ @category_name =] 'category']  
     [ , [ @wmi_namespace = ] 'wmi_namespace' ]  
     [ , [ @wmi_query = ] 'wmi_query' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @name = ] 'name'`更新する警告の名前を指定します。 *名前*は**sysname**,、既定値はありません。  
  
`[ @new_name = ] 'new_name'`警告の新しい名前。 名前は一意である必要があります。 *新しい名前*は**sysname**,、既定値は NULL です。  
  
`[ @enabled = ] enabled`アラートが有効 (**1**) か無効 (**0**) かを指定します。 *有効*になっているは**tinyint**,、既定値は NULL です。 起動するには、アラートを有効にする必要があります。  
  
`[ @message_id = ] message_id`警告定義の新しいメッセージまたはエラー番号。 通常、 *message_id*は**sysmessages**テーブルのエラー番号に対応します。 *message_id*は**int**,、既定値は NULL です。 メッセージ ID は、警告の重大度レベルの設定が**0**の場合にのみ使用できます。  
  
`[ @severity = ] severity`警告定義の新しい重大度レベル ( **1** ~ **25**)。 Windows アプリケーションログに指定した重要度のメッセージが送信されると、アラートがアクティブ化されます。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] *重大度*は**int**,、既定値は NULL です。 重大度レベルは、警告のメッセージ ID 設定が**0**の場合にのみ使用できます。  
  
`[ @delay_between_responses = ] delay_between_responses`警告への応答の間の新しい待機時間 (秒単位)。 *delay_between_responses*は**int**,、既定値は NULL です。  
  
`[ @notification_message = ] 'notification_message'`電子メール、 **net send**、またはポケットベルによる通知の一部としてオペレーターに送信される追加メッセージの変更されたテキスト。 *このパラメーター*は**nvarchar (512)** ,、既定値は NULL です。  
  
`[ @include_event_description_in = ] include_event_description_in`Windows アプリケーションログからの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エラーの説明を通知メッセージに含めるかどうかを指定します。 *include_event_description_in*は**tinyint**,、既定値は NULL の場合、これらの値の1つ以上を指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**0**|なし|  
|**1**|[電子メール]|  
|**2**|[ポケットベル]|  
|**4**|**net send**|  
|**7**|All|  
  
`[ @database_name = ] 'database'`警告を起動するためにエラーが発生する必要があるデータベースの名前。 *データベース*は**sysname です。** 角かっこ ([]) で囲まれた名前は使用できません。 既定値は NULL です。  
  
`[ @event_description_keyword = ] 'event_description_keyword'`エラーメッセージログのエラーの説明に含まれている文字のシーケンス。 [!INCLUDE[tsql](../../includes/tsql-md.md)]LIKE 式パターン一致文字を使用できます。 *event_description_keyword*は**nvarchar (100)** ,、既定値は NULL です。 このパラメーターは、オブジェクト名 ( **% customer_table%** など) をフィルター処理する場合に便利です。  
  
`[ @job_id = ] job_id`ジョブの識別番号を指定します。 *job_id*は**uniqueidentifier**,、既定値は NULL です。 *Job_id*を指定する場合は、 *job_name*を省略する必要があります。  
  
`[ @job_name = ] 'job_name'`この警告に応答して実行されるジョブの名前。 *job_name*は**sysname**,、既定値は NULL です。 *Job_name*を指定する場合は、 *job_id*を省略する必要があります。  
  
`[ @occurrence_count = ] occurrence_count`アラートが発生した回数をリセットします。 *occurrence_count*は**int**,、既定値は NULL の場合にのみ設定できます**0**です。  
  
`[ @count_reset_date = ] count_reset_date`発生回数が最後にリセットされた日付をリセットします。 *count_reset_date*は**int**,、既定値は NULL です。  
  
`[ @count_reset_time = ] count_reset_time`発生回数が最後にリセットされた時刻をリセットします。 *count_reset_time*は**int**,、既定値は NULL です。  
  
`[ @last_occurrence_date = ] last_occurrence_date`警告が最後に発生した日付をリセットします。 *last_occurrence_date*は**int**,、既定値は NULL の場合にのみ設定できます**0**です。  
  
`[ @last_occurrence_time = ] last_occurrence_time`アラートが最後に発生した時刻をリセットします。 *last_occurrence_time*は**int**,、既定値は NULL の場合にのみ設定できます**0**です。  
  
`[ @last_response_date = ] last_response_date`SQLServerAgent サービスが最後に警告に応答した日付をリセットします。 *last_response_date*は**int**,、既定値は NULL の場合にのみ設定できます**0**です。  
  
`[ @last_response_time = ] last_response_time`SQLServerAgent サービスが最後に警告に応答した時刻をリセットします。 *last_response_time*は**int**,、既定値は NULL の場合にのみ設定できます**0**です。  
  
`[ @raise_snmp_trap = ] raise_snmp_trap`確保.  
  
`[ @performance_condition = ] 'performance_condition'` **'** _Itemcomparatorvalue_ **'** という形式で表された値。 *performance_condition*は**nvarchar (512)** ,、既定値は NULL の場合、これらの要素で構成されます。  
  
|要素の書式設定|説明|  
|--------------------|-----------------|  
|*アイテム*|パフォーマンス オブジェクト、パフォーマンス カウンター、またはカウンターの名前付きインスタンス。|  
|*演算子*|次のいずれかの **>** 演算子 **<** :、、 **=**|  
|*[値]*|カウンターの数値|  
  
`[ @category_name = ] 'category'`警告カテゴリの名前。 *category*は**sysname**で、既定値は NULL です。  
  
`[ @wmi_namespace = ] 'wmi_namespace'`イベントを照会する WMI 名前空間。 *wmi_namespace*は**sysname**,、既定値は NULL です。  
  
`[ @wmi_query = ] 'wmi_query'`警告の WMI イベントを指定するクエリ。 *wmi_query*は**nvarchar (512)** ,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アプリケーションログに書き込まれた**sysmessages**のみが、アラートを発生させることができます。  
  
 **sp_update_alert**では、パラメーター値が指定されているアラート設定のみが変更されます。 パラメーターを省略した場合は、現在の設定が保持されます。  
  
## <a name="permissions"></a>アクセス許可  
 このストアドプロシージャを実行するには、 **sysadmin**固定サーバーロールのメンバーである必要があります。  
  
## <a name="examples"></a>使用例  
 次の例では、警告が有効になっている `Test Alert` の設定を `0` (無効) に変更します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_alert  
    @name = N'Test Alert',  
    @enabled = 0 ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sp_help_alert &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
