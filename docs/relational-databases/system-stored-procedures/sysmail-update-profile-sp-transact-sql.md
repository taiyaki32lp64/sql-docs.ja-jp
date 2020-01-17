---
title: sysmail_update_profile_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_profile_sp
- sysmail_update_profile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_profile_sp
ms.assetid: eaedf7ce-a8d5-4ab9-99e0-d77d5be19e90
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 36731206770b324bf4387143ef2c98b0532475ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902889"
---
# <a name="sysmailupdateprofilesp-transact-sql"></a>sysmail_update_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベース メール プロファイルの説明または名前を変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_update_profile_sp [ [ @profile_id = ] profile_id , ] [ [ @profile_name = ] 'profile_name' , ]  
    [ [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @profile_id = ] profile_id` 更新するプロファイルの id。 *profile_id*は**int**、既定値は NULL です。 少なくとも 1 つの*profile_id*または*profile_name*指定する必要があります。 両方が指定されている場合、手順は、プロファイルの名前を変更します。  
  
`[ @profile_name = ] 'profile_name'` 更新するプロファイルの名前またはプロファイルの新しい名前。 *profile_name*は**sysname**、既定値は NULL です。 少なくとも 1 つの*profile_id*または*profile_name*指定する必要があります。 両方が指定されている場合、手順は、プロファイルの名前を変更します。  
  
`[ @description = ] 'description'` プロファイルの新しい説明します。 *説明*は**nvarchar (256)** 、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 プロファイルの id とプロファイル名の両方を指定すると、プロシージャが指定された名前に、プロファイルの名前を変更し、プロファイルの説明を更新します。 これらの引数の 1 つだけを指定した場合、手順は、プロファイルの説明を更新します。  
  
 ストアド プロシージャ**sysmail_update_profile_sp**では、 **msdb**が所有するデータベースにあり、 **dbo**スキーマ。 現在のデータベースがない場合、3 つの部分の名前を持つプロシージャを実行する必要があります**msdb**します。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの既定のメンバーへのアクセス許可を実行、 **sysadmin**固定サーバー ロール。  
  
## <a name="examples"></a>使用例  
 **A.プロファイルの説明を変更します。**  
  
 次の例では、という名前のプロファイルの説明を変更する`AdventureWorks Administrator`で、 **msdb**データベース。  
  
```  
EXECUTE msdb.dbo.sysmail_update_profile_sp  
    @profile_name = 'AdventureWorks Administrator'  
    ,@description = 'Administrative mail profile.';  
```  
  
 **B.プロファイルの説明と名前を変更します。**  
  
 次の例では、プロファイル id を持つプロファイルの説明と名前の変更`750`します。  
  
```  
EXECUTE msdb.dbo.sysmail_update_profile_sp  
    @profile_id = 750  
    ,@profile_name = 'Operator'  
    ,@description = 'Profile to send alert e-mail to operators.';  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベース メール構成オブジェクト](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [データベース メール アカウントを作成します。](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [データベース メール ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
