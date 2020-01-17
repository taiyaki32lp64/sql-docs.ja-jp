---
title: sp_update_notification (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_notification_TSQL
- sp_update_notification
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatenotification
ms.assetid: 3e1c3d40-8c24-46ce-a68e-ce6c6a237fda
author: stevestein
ms.author: sstein
ms.openlocfilehash: 35cfa3aeda8e296cd1a85a0e8a098aaddac90954
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084865"
---
# <a name="spupdatenotification-transact-sql"></a>sp_update_notification (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  警告通知の通知方法を更新します。  

  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_update_notification  
          [@alert_name =] 'alert' ,  
     [@operator_name =] 'operator' ,  
     [@notification_method =] notification  
```  
  
## <a name="arguments"></a>引数  
`[ @alert_name = ] 'alert'` この通知に関連付けられているアラートの名前。 *アラート*は**sysname**、既定値はありません。  
  
`[ @operator_name = ] 'operator'` 警告が発生したときに通知するオペレーター。 *演算子*は**sysname**、既定値はありません。  
  
`[ @notification_method = ] notification` オペレーターに通知するメソッド。 *通知*は**tinyint**, で、既定値はありませんはこれらの値の 1 つ以上指定します。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|[電子メール]|  
|**2**|[ポケットベル]|  
|**4**|**net send**|  
|**7**|すべてのメソッド|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_update_notification**から実行する必要があります、 **msdb**データベース。  
  
 通知を更新するには、指定した必要なアドレス情報を持っていないユーザーの演算子の*notification_method*します。 電子メール メッセージやポケットベルによる通知を送信するときに、障害が発生した場合、Microsoft SQL Server エージェント エラー ログで、エラーが報告されます。  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャを実行するユーザーに付与する必要があります、 **sysadmin**固定サーバー ロール。  
  
## <a name="examples"></a>使用例  
 次の例に送信される通知の通知方法を変更する`François Ajenstat`アラートの`Test Alert`します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_notification  
   @alert_name = N'Test Alert',  
   @operator_name = N'François Ajenstat',  
   @notification_method = 7;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_add_notification &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_delete_notification &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_help_notification &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
