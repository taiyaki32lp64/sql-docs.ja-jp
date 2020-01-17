---
title: sp_help_notification (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_notification
- sp_help_notification_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_notification
ms.assetid: 0273457f-9d2a-4a6f-9a16-6a6bf281cba0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 630c2f90085cedfbb5c59ba395c7d0d9ae9d9643
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906106"
---
# <a name="sphelpnotification-transact-sql"></a>sp_help_notification (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  特定の演算子または演算子は指定された警告の一覧には、アラートの一覧を報告します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_notification  
     [ @object_type = ] 'object_type' ,  
     [ @name = ] 'name' ,  
     [ @enum_type = ] 'enum_type' ,   
     [ @notification_method = ] notification_method   
     [ , [ @target_name = ] 'target_name' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @object_type = ] 'object_type'` 返される情報の種類。 *object_type*は**char (9)** 、既定値はありません。 *object_type*指定されたオペレーター名に割り当てられているアラートを一覧表示する、アラートは、 *、* または演算子では、指定された警告名を担当する演算子の一覧を表示する*します。*  
  
`[ @name = ] 'name'` オペレーター名 (場合*object_type* is 演算子) または警告の名前 (場合*object_type* alerts)。 *名前*は**sysname**、既定値はありません。  
  
`[ @enum_type = ] 'enum_type'` *Object_type*返される情報。 *enum_type*は「ACTUAL」は、ほとんどの場合。 *enum_type*は**char (10)** , で、既定値はありませんはこれらの値のいずれかを指定します。  
  
|値|説明|  
|-----------|-----------------|  
|ACTUAL|だけを表示、 *object_types*に関連付けられている*名前*します。|  
|ALL|すべてを一覧表示、*object_types*に関連付けられていないものも含め*名前*します。|  
|TARGET|だけを表示、 *object_types* 、指定された照合*target_name*との関連付けに関係なく、*名前*します。|  
  
`[ @notification_method = ] notification_method` 返される通知方法の列を決定する数値。 *notification_method*は**tinyint**値は次のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|電子メール: だけを返す、 **use_email**列。|  
|**2**|ポケットベル: だけを返す、 **use_pager**列。|  
|**4**|NetSend: だけを返す、 **use_netsend**列。|  
|**7**|All: すべての列を返します。|  
  
`[ @target_name = ] 'target_name'` 検索するアラートの名前 (場合*object_type*アラートは、) を検索するオペレーター名 (場合*object_type* is 演算子)。 *target_name*場合にのみ必要*enum_type*はターゲットです。 *target_name*は**sysname**、既定値は NULL です。  
  
## <a name="return-code-valves"></a>戻り値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 場合*object_type*は**アラート**、結果セットには、特定の演算子のすべてのアラートが表示されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|警告識別番号。|  
|**alert_name**|**sysname**|アラートの名前。|  
|**use_email**|**int**|オペレーターに通知する電子メールを使用するとします。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
|**use_pager**|**int**|ポケットベルを使用して、オペレーターに通知します。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
|**use_netsend**|**int**|オペレーターへの通知にネットワーク ポップアップを使用するかどうか。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
|**has_email**|**int**|この警告で送信する電子メール通知の数。|  
|**has_pager**|**int**|この警告で送信するポケットベルによる通知の数。|  
|**has_netsend**|**int**|数**net send**通知がこの警告で送信します。|  
  
 場合**object_type**は**演算子**、結果セットは指定された警告のすべての演算子の一覧です。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**operator_id**|**int**|オペレーター識別番号。|  
|**operator_name**|**sysname**|演算子の名前。|  
|**use_email**|**int**|オペレーターの通知を送信する電子メールを使用するとします。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
|**use_pager**|**int**|オペレーターへの通知にポケットベルを使用するかどうか。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
|**use_netsend**|**int**|オペレーターに通知するために使用するネットワーク ポップアップ。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
|**has_email**|**int**|オペレーターが電子メール アドレスを持っているかどうか。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
|**has_pager**|**int**|オペレーターがポケットベル アドレスを持っているかどうか。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
|**has_netsend**|**int**|演算子は、net send による通知を構成します。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
  
## <a name="remarks"></a>コメント  
 このストアド プロシージャを実行する必要があります、 **msdb**データベース。  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャを実行するには、 **sysadmin** 固定サーバー ロールのメンバーであることが必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-listing-alerts-for-a-specific-operator"></a>A. 特定のオペレーターに対する警告を表示します。  
 次の例では、オペレーター `François Ajenstat` が通知を受け取るすべての警告を返します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_notification   
    @object_type = N'ALERTS',  
    @name = N'François Ajenstat',  
    @enum_type = N'ACTUAL',  
    @notification_method = 7 ;  
GO  
```  
  
### <a name="b-listing-operators-for-a-specific-alert"></a>B. 特定の警告の送信先となるオペレーターを表示する  
 次の例は、任意の種類の通知を受信するすべてのオペレーターを返して、`Test Alert`アラート。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_notification  
    @object_type = N'OPERATORS',  
    @name = N'Test Alert',  
    @enum_type = N'ACTUAL',  
    @notification_method = 7 ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_add_notification &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_delete_notification &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_update_notification &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
