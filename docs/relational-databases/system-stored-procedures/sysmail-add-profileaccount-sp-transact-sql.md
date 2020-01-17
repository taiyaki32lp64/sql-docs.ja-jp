---
title: sysmail_add_profileaccount_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_profileaccount_sp
- sysmail_add_profileaccount_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profileaccount_sp
ms.assetid: 7cbf430f-1997-45ea-9707-0086184de744
author: stevestein
ms.author: sstein
ms.openlocfilehash: 11ada827add27ae2186fdcc565b3dd2f99f76452
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017763"
---
# <a name="sysmailaddprofileaccountsp-transact-sql"></a>sysmail_add_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベース メール プロファイルには、データベース メール アカウントを追加します。 実行**sysmail_add_profileaccount_sp**データベース アカウントの作成後[sysmail_add_account_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-account-sp-transact-sql.md)、でデータベースプロファイルを作成および[sysmail_add_profile_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql.md)します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_add_profileaccount_sp { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    { [ @account_id = ] account_id | [ @account_name = ] 'account_name' }  
    [ , [ @sequence_number = ] sequence_number ]  
```  
  
## <a name="arguments"></a>引数  
`[ @profile_id = ] profile_id` アカウントを追加するプロファイルの id。 *profile_id*は**int**、既定値は NULL です。 いずれか、 *profile_id*または*profile_name*指定する必要があります。  
  
`[ @profile_name = ] 'profile_name'` アカウントを追加するプロファイルの名前。 *profile_name*は**sysname**、既定値は NULL です。 いずれか、 *profile_id*または*profile_name*指定する必要があります。  
  
`[ @account_id = ] account_id` プロファイルに追加するアカウント id。 *account_id*は**int**、既定値は NULL です。 いずれか、 *account_id*または*account_name*指定する必要があります。  
  
`[ @account_name = ] 'account_name'` プロファイルに追加するアカウントの名前。 *account_name*は**sysname**、既定値は NULL です。 いずれか、 *account_id*または*account_name*指定する必要があります。  
  
`[ @sequence_number = ] sequence_number` プロファイル内のアカウントのシーケンス番号。 *sequence_number*は**int**、既定値はありません。 シーケンス番号は、プロファイルのアカウントを使用する順序を決定します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 プロファイルとアカウントの両方が既に存在する必要があります。 両方またはいずれかが存在しないと、このストアド プロシージャはエラーを返します。  
  
 このストアド プロシージャが、指定されたプロファイルに関連付けられているアカウントのシーケンス番号を変更しないことに注意してください。 アカウントのシーケンス番号の更新の詳細については、次を参照してください。 [sysmail_update_profileaccount_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-update-profileaccount-sp-transact-sql.md)します。  
  
 シーケンス番号によって、データベース メールではプロファイル内のアカウントがどの順番で使用されるかが決まります。 新しい電子メール メッセージの場合、データベース メールでは、一番小さなシーケンス番号の付いたアカウントから処理が開始されます。 そのアカウントが失敗すると、データベース メールでは、このアカウントよりも大きいシーケンス番号を持つアカウントに処理が移ります。このように、データベース メールによってメッセージが正常に送信されるか、一番大きなシーケンス番号のアカウントが失敗するまで順に処理されます。 最も番号が大きいアカウントで失敗した場合、 *sysmail_configure_sp* の **AccountRetryDelay**パラメーターで構成した時間、メールの送信が一時停止されます。その後、最も番号が小さいアカウントからメールの送信プロセスが再開されます。 *sysmail_configure_sp* の **AccountRetryAttempts**パラメーターは、指定されたプロファイルの各アカウントを使用して外部メール プロセスが電子メール メッセージを送信する回数を構成します。  
  
 同じシーケンス番号を持つ複数のアカウントが存在する場合データベース メールはのみを使用して、それらのアカウントのいずれかの指定された電子メール メッセージの。 この場合、そのシーケンス番号に対してどのアカウントが使用されるか、またメッセージごとに同じアカウントが使用されるかついては、データベース メールでは保証されません。  
  
 ストアド プロシージャ**sysmail_add_profileaccount_sp**では、 **msdb**が所有するデータベースにあり、 **dbo**スキーマ。 現在のデータベースがない場合、3 つの部分の名前を持つプロシージャを実行する必要があります**msdb**します。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの既定のメンバーへのアクセス許可を実行、 **sysadmin**固定サーバー ロール。  
  
## <a name="examples"></a>使用例  
 次の例は、プロファイルを関連付ける`AdventureWorks Administrator`アカウントで`Audit Account`します。 監査アカウントには、1 のシーケンス番号があります。  
  
```  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator',  
    @account_name = 'Audit Account',  
    @sequence_number = 1 ;  
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベース メール アカウントを作成します。](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [データベース メール構成オブジェクト](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [データベース メール ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
