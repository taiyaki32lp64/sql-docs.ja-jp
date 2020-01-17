---
title: sysmail_delete_principalprofile_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_principalprofile_sp_TSQL
- sysmail_delete_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_principalprofile_sp
ms.assetid: 8fc14700-e17a-4073-9a96-7fc23e775c69
author: stevestein
ms.author: sstein
ms.openlocfilehash: 86f9566ce86423939aff22fc37331c5c9db89904
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909210"
---
# <a name="sysmaildeleteprincipalprofilesp-transact-sql"></a>sysmail_delete_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベースのユーザーやロールから、パブリックまたはプライベートなデータベース メール プロファイルを使用する権限を削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_delete_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
```  
  
## <a name="arguments"></a>引数  
`[ @principal_id = ] principal_id` データベース ユーザーまたはロールの id、 **msdb**の関連付けを削除するデータベース。 *principal_id*は**int**、既定値は NULL です。 パブリック プロファイルをプライベート プロファイルにするために、プリンシパル ID を提供**0**またはプリンシパル名の **'public'** します。 いずれか*principal_id*または*principal_name*指定する必要があります。  
  
`[ @principal_name = ] 'principal_name'` データベース ユーザーまたはロールの名前を指定します、 **msdb**の関連付けを削除するデータベース。 *principal_name*は**sysname**、既定値は NULL です。 パブリック プロファイルをプライベート プロファイルにするために、プリンシパル ID を提供**0**またはプリンシパル名の **'public'** します。 いずれか*principal_id*または*principal_name*指定する必要があります。  
  
`[ @profile_id = ] profile_id` 関連付けを削除するプロファイルの ID です。 *profile_id*は**int**、既定値は NULL です。 いずれか*profile_id*または*profile_name*指定する必要があります。  
  
`[ @profile_name = ] 'profile_name'` 関連付けを削除するプロファイルの名前です。 *profile_name*は**sysname**、既定値は NULL です。 いずれか*profile_id*または*profile_name*指定する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 パブリック プロファイルをプライベート プロファイルにするために、提供 **'public'** プリンシパル名または**0**プリンシパルの id。  
  
 ユーザーの既定のプライベート プロファイルや、既定のパブリック プロファイルを削除する場合は慎重に行ってください。 既定のプロファイルが使用できないときに**sp_send_dbmail**を引数としてプロファイルの名前が必要です。 そのため、既定のプロファイルを削除する可能性への呼び出し**sp_send_dbmail**が失敗します。 詳細については、次を参照してください。 [sp_send_dbmail &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)します。  
  
 ストアド プロシージャ**sysmail_delete_principalprofile_sp**では、 **msdb**が所有するデータベースにあり、 **dbo**スキーマ。 現在のデータベースがない場合、3 つの部分の名前を持つプロシージャを実行する必要があります**msdb**します。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの既定のメンバーへのアクセス許可を実行、 **sysadmin**固定サーバー ロール。  
  
## <a name="examples"></a>使用例  
 次の例は、プロファイルの間の関連付けを削除する**AdventureWorks Administrator**とログインの**ApplicationUser**で、 **msdb**データベース。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベース メール構成オブジェクト](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [データベース メール ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
