---
title: sysmail_delete_account_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_account_sp
- sysmail_delete_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_account_sp
ms.assetid: 2adcac78-4a4a-407e-9666-1d9c43c73cc2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4b6adc5f6c02eae49a5f5e2598c6b02e5b00534e
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211265"
---
# <a name="sysmail_delete_account_sp-transact-sql"></a>sysmail_delete_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  データベースメール SMTP アカウントを削除します。 データベースメール構成ウィザードを使用してアカウントを削除することもできます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_delete_account_sp { [ @account_id = ] account_id | [ @account_name = ] 'account_name' }   
```  
  
## <a name="arguments"></a>引数  
削除するアカウントの ID 番号 `[ @account_id = ] account_id` ます。 *account_id*は**int**,、既定値はありません。 *Account_id*または*account_name*のいずれかを指定する必要があります。  
  
削除するアカウントの名前 `[ @account_name = ] 'account_name'` ます。 *account_name*は**sysname**であり、既定値はありません。 *Account_id*または*account_name*のいずれかを指定する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 [InclusionThresholdSetting]  
  
## <a name="remarks"></a>Remarks  
 この手順では、アカウントがプロファイルで使用されているかどうかに関係なく、指定されたアカウントを削除します。 アカウントが含まれていないプロファイルは、正常に電子メールを送信できません。  
  
 ストアドプロシージャ**sysmail_delete_account_sp**は**msdb**データベースにあり、 **dbo**スキーマが所有しています。 現在のデータベースが**msdb**でない場合は、3つの部分で構成される名前を使用してプロシージャを実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では**sysadmin**固定サーバーロールのメンバーに与えています。  
  
## <a name="examples"></a>使用例  
 次の例では、`AdventureWorks Administrator`という名前のデータベースメールアカウントを削除しています。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_account_sp  
    @account_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベースメールアカウントの作成](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [構成オブジェクトのデータベースメール](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [transact-sql &#40;  の&#41; sysmail_add_account_sp](../../relational-databases/system-stored-procedures/sysmail-add-account-sp-transact-sql.md)  
 [transact-sql &#40;  の&#41; sysmail_delete_profile_sp](../../relational-databases/system-stored-procedures/sysmail-delete-profile-sp-transact-sql.md)  
 [transact-sql &#40;  の&#41; sysmail_delete_profileaccount_sp](../../relational-databases/system-stored-procedures/sysmail-delete-profileaccount-sp-transact-sql.md)  
 [transact-sql &#40;  の&#41; sysmail_help_account_sp](../../relational-databases/system-stored-procedures/sysmail-help-account-sp-transact-sql.md)  
 [transact-sql &#40;  の&#41; sysmail_help_profile_sp](../../relational-databases/system-stored-procedures/sysmail-help-profile-sp-transact-sql.md)  
 [transact-sql &#40;  の&#41; sysmail_help_profileaccount_sp](../../relational-databases/system-stored-procedures/sysmail-help-profileaccount-sp-transact-sql.md)  
 [sysmail_update_profileaccount_sp &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sysmail-update-profileaccount-sp-transact-sql.md)  
  
  
