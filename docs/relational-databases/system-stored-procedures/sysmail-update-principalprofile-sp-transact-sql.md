---
title: sysmail_update_principalprofile_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_principalprofile_sp
- sysmail_update_principalprofile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_principalprofile_sp
ms.assetid: 9fe96e9a-4758-4e4a-baee-3e1217c4426c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: dd9644253302c6a577c6cc3923bb3a9e3a0d8c0e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037380"
---
# <a name="sysmailupdateprincipalprofilesp-transact-sql"></a>sysmail_update_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  アソシエーションのプリンシパルとプロファイルの間の情報を更新します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_update_principalprofile_sp { @principal_id = principal_id | @principal_name = 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    [ @is_default = ] 'is_default'  
```  
  
## <a name="arguments"></a>引数  
`[ @principal_id = ] principal_id` データベース ユーザーまたはロールの ID、 **msdb**の関連付けを変更するデータベース。 *principal_id*は**int**、既定値は NULL です。 いずれか*principal_id*または*principal_name*指定する必要があります。  
  
`[ @principal_name = ] 'principal_name'` データベース ユーザーまたはロールの名前、 **msdb**を更新するアソシエーションのデータベースです。 *principal_name*は**sysname**、既定値は NULL です。 いずれか*principal_id*または*principal_name*指定することがあります。  
  
`[ @profile_id = ] profile_id` 関連付けを変更するプロファイルの id。 *profile_id*は**int**、既定値は NULL です。 いずれか*profile_id*または*profile_name*指定する必要があります。  
  
`[ @profile_name = ] 'profile_name'` 関連付けを変更するプロファイルの名前。 *profile_name*は**sysname**、既定値は NULL です。 いずれか*profile_id*または*profile_name*指定する必要があります。  
  
`[ @is_default = ] 'is_default'` このプロファイルは、データベース ユーザーの既定のプロファイルかどうかです。 データベース ユーザーは、既定のプロファイルを 1 つのみあります。 *is_default*は**ビット**、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 このストアド プロシージャでは、指定したプロファイルを、データベース ユーザーの既定のプロファイルにするかどうかを変更します。 データベース ユーザーが持つことのできる既定のプライベート プロファイルは 1 つだけです。  
  
 アソシエーションのプリンシパル名の場合は**パブリック**、アソシエーションのプリンシパル id がまたは**0**、このストアド プロシージャは、パブリック プロファイルを変更します。 既定のパブリック プロファイルは 1 つしか存在できません。  
  
 ときに **\@is_default**は '**1**' と、プリンシパルが 1 つ以上のプロファイルに関連付けられた、指定されたプロファイルはプリンシパルの既定のプロファイルになります。 プロファイルされていた既定のプロファイルも、プリンシパルに関連付けられてが、既定のプロファイルではなくなりました。  
  
 ストアド プロシージャ**sysmail_update_principalprofile_sp**では、 **msdb**が所有するデータベースにあり、 **dbo**スキーマ。 現在のデータベースがない場合、3 つの部分の名前を持つプロシージャを実行する必要があります**msdb**します。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの既定のメンバーへのアクセス許可を実行、 **sysadmin**固定サーバー ロール。  
  
## <a name="examples"></a>使用例  
 **A.データベースの既定のパブリック プロファイルに、プロファイルの設定**  
  
 次の例では、設定、プロファイル`General Use Profile`内のユーザーの既定のパブリック プロファイルを**msdb**データベース。  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'General Use Profile',  
    @is_default = '1';  
```  
  
 **B.ユーザーの既定のプライベート プロファイルに、プロファイルの設定**  
  
 次の例では、設定、プロファイル`AdventureWorks Administrator`プリンシパルの既定のプロファイルに`ApplicationUser`で、 **msdb**データベース。 このプロファイルはプリンシパルに既に関連付けられている必要があります。 プロファイルされていた既定のプロファイルも、プリンシパルに関連付けられてが、既定のプロファイルではなくなりました。  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator',  
    @is_default = '1' ;  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベース メール構成オブジェクト](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [データベース メール ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
