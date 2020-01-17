---
title: sp_add_notification (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_notification_TSQL
- sp_add_notification
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_notification
ms.assetid: 0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 60bb289f0fd6d7b7dd1034630929998d32cc59d0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115063"
---
# <a name="spaddnotification-transact-sql"></a>sp_add_notification (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  警告の通知を設定します。  
  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_add_notification [ @alert_name = ] 'alert' ,   
    [ @operator_name = ] 'operator' ,   
    [ @notification_method = ] notification_method  
```  
  
## <a name="arguments"></a>引数  
`[ @alert_name = ] 'alert'` この通知のアラート。 *アラート*は**sysname**、既定値はありません。  
  
`[ @operator_name = ] 'operator'` 警告が発生したときに通知する演算子です。 *演算子*は**sysname**、既定値はありません。  
  
`[ @notification_method = ] notification_method` オペレーターに通知するメソッド。 *notification_method*は**tinyint**、既定値はありません。 *notification_method*と組み合わせてこれらの値の 1 つ以上を指定することができます、 **OR**論理演算子です。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|[電子メール]|  
|**2**|[ポケットベル]|  
|**4**|**net send**|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 **sp_add_notification**から実行する必要があります、 **msdb**データベース。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、警告システム全体を簡単に管理できるグラフィカルなツールです。 警告システムを構成するときには、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用することをお勧めします。  
  
 警告に対応して通知を送るには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがメールを送れるようにあらかじめ構成しておく必要があります。  
  
 電子メールのメッセージやポケットベルによる通知に失敗した場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス エラー ログに失敗がレポートされます。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールが実行できる**sp_add_notification**します。  
  
## <a name="examples"></a>使用例  
 次の例では、指定された警告 (`Test Alert`) に対応する電子メールでの通知を追加します。  
  
> **注:** この例では、`Test Alert`既に存在することと`François Ajenstat`は有効な演算子の名前です。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_notification  
 @alert_name = N'Test Alert',  
 @operator_name = N'François Ajenstat',  
 @notification_method = 1 ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_delete_notification &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_help_notification &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [sp_update_notification &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [sp_add_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
