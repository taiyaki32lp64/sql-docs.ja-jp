---
title: sp_notify_operator (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_notify_operator_TSQL
- sp_notify_operator
dev_langs:
- TSQL
helpviewer_keywords:
- sp_notify_operator
ms.assetid: c440f5c9-9884-4196-b07c-55d87afb17c3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 74558320df59414a756e1655bb073e9bf0d7d73c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107979"
---
# <a name="spnotifyoperator-transact-sql"></a>sp_notify_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベース メールを使用してオペレーターに電子メール メッセージを送信します。  
  
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_notify_operator  
    [ @profile_name = ] 'profilename' ,  
    [ @id = ] id ,  
    [ @name = ] 'name' ,  
    [ @subject = ] 'subject' ,  
    [ @body = ] 'message' ,  
    [ @file_attachments = ] 'attachment'  
    [ @mail_database = ] 'mail_host_database'  
```  
  
## <a name="arguments"></a>引数  
`[ @profile_name = ] 'profilename'` メッセージの送信に使用するデータベース メール プロファイルの名前。 *profilename*は**nvarchar (128)** します。 場合*profilename*が指定されていない、既定のデータベース メール プロファイルを使用します。  
  
`[ @id = ] id` メッセージを送信するオペレーターの識別子。 *id*は**int**、既定値は NULL です。 いずれかの*id*または*名前*指定する必要があります。  
  
`[ @name = ] 'name'` メッセージを送信するオペレーターの名前。 *名前*は**nvarchar (128)** 、既定値は NULL です。 いずれかの*id*または*名前*指定する必要があります。  
  
> **注:** メッセージを受信する前に、オペレーターの電子メール アドレスを定義する必要があります。  
  
`[ @subject = ] 'subject'` 電子メール メッセージの件名。 *サブジェクト*は**nvarchar (256)** 既定値はありません。  
  
`[ @body = ] 'message'` 電子メール メッセージの本文。 *メッセージ*は**nvarchar (max)** 既定値はありません。  
  
`[ @file_attachments = ] 'attachment'` 電子メール メッセージに添付するファイルの名前。 *添付ファイル*は**nvarchar (512)** 、既定値はありません。  
  
`[ @mail_database = ] 'mail_host_database'` メール ホスト データベースの名前を指定します。 *mail_host_database* is **nvarchar(128)** . ない場合は*mail_host_database*が指定されている、 **msdb**データベースが既定で使用されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 ここでは、指定したメッセージが、指定したオペレーターの電子メール アドレスに送信されます。 オペレーターに電子メール アドレスが構成されていない場合、エラーが返されます。  
  
 オペレーターに通知を送信できる前に、データベース メールとメール ホスト データベースを構成する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、このストアド プロシージャを実行できるのは、 **sysadmin** 固定サーバー ロールのメンバーです。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次の例では、データベース メール プロファイル `François Ajenstat` を使用して、電子メールをオペレーター `AdventureWorks Administrator` に送信します。 電子メールの件名は`Test Notification`します。 電子メール メッセージには、"This is a test of notification via e-mail." という文が記載されています。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_notify_operator  
   @profile_name = N'AdventureWorks Administrator',  
   @name = N'François Ajenstat',  
   @subject = N'Test Notification',  
   @body = N'This is a test of notification via e-mail.' ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [SQL Server エージェント ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_help_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_delete_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)  
  
  
