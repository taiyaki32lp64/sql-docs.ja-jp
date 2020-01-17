---
title: sysmail_update_profileaccount_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_profileaccount_sp_TSQL
- sysmail_update_profileaccount_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_profileaccount_sp
ms.assetid: 92ca7488-29db-414e-8e36-08b0a8f542bb
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 246081eb5c362cb76a4c037693ee6c40b999fcdd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037327"
---
# <a name="sysmailupdateprofileaccountsp-transact-sql"></a>sysmail_update_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベース メール プロファイル内のアカウントのシーケンス番号を更新します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_update_profileaccount_sp  { [ @profile_id = ] profile_id   
| [ @profile_name = ] 'profile_name' } ,  
    { [ @account_id = ] account_id | [ @account_name = ] 'account_name' } ,  
    [ @sequence_number = ] sequence_number  
```  
  
## <a name="arguments"></a>引数  
`[ @profile_id = ] profile_id` 更新するプロファイルのプロファイル ID。 *profile_id*は**int**、既定値は NULL です。 いずれか、 *profile_id*または*profile_name*指定する必要があります。  
  
`[ @profile_name = ] 'profile_name'` 更新するプロファイルのプロファイルの名前。 *profile_name*は**sysname**、既定値は NULL です。 いずれか、 *profile_id*または*profile_name*指定する必要があります。  
  
`[ @account_id = ] account_id` 更新するアカウント ID。 *account_id*は**int**、既定値は NULL です。 いずれか、 *account_id*または*account_name*指定する必要があります。  
  
`[ @account_name = ] 'account_name'` 更新するアカウントの名前。 *account_name*は**sysname**、既定値は NULL です。 いずれか、 *account_id*または*account_name*指定する必要があります。  
  
`[ @sequence_number = ] sequence_number` アカウントの新しいシーケンス番号。 *sequence_number*は**int**、既定値はありません。 シーケンス番号は、プロファイルのアカウントを使用する順序を決定します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 指定されたプロファイルで指定されたアカウントが関連付けられていない場合は、エラーを返します。  
  
 シーケンス番号によって、データベース メールではプロファイル内のアカウントがどの順番で使用されるかが決まります。 新しい電子メール メッセージの場合、データベース メールでは、一番小さなシーケンス番号の付いたアカウントから処理が開始されます。 そのアカウントが失敗すると、データベース メールでは、このアカウントよりも大きいシーケンス番号を持つアカウントに処理が移ります。このように、データベース メールによってメッセージが正常に送信されるか、一番大きなシーケンス番号のアカウントが失敗するまで順に処理されます。 一番大きなシーケンス番号のアカウントが失敗した場合、電子メール メッセージは失敗します。  
  
 同じシーケンス番号を持つアカウントが複数存在する場合、データベース メールでは、指定された電子メール メッセージに対して、これらのアカウントのいずれか 1 つのみが使用されます。 この場合、そのシーケンス番号に対してどのアカウントが使用されるか、またメッセージごとに同じアカウントが使用されるかついては、データベース メールでは保証されません。  
  
 ストアド プロシージャ**sysmail_update_profileaccount_sp**では、 **msdb**が所有するデータベースにあり、 **dbo**スキーマ。 現在のデータベースがない場合、3 つの部分の名前を持つプロシージャを実行する必要があります**msdb**します。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの既定のメンバーへのアクセス許可を実行、 **sysadmin**固定サーバー ロール。  
  
## <a name="examples"></a>使用例  
 次の例では、アカウントのシーケンス番号を変更する`Admin-BackupServer`プロファイルにある`AdventureWorks Administrator`で、 **msdb**データベース。 このコードを実行すると、アカウントのシーケンス番号は `3` になります。これは、最初の 2 つのアカウントが失敗した場合に試行されることを示します。  
  
```  
EXECUTE msdb.dbo.sysmail_update_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator'  
    ,@account_name = 'Admin-BackupServer',  
    ,@sequence_number = 3;  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベース メール アカウントを作成します。](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [データベース メール構成オブジェクト](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [データベース メール ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
