---
title: sysmail_help_profileaccount_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_profileaccount_sp_TSQL
- sysmail_help_profileaccount_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_profileaccount_sp
ms.assetid: 3ea68271-0a6b-4d77-991c-4757f48f747a
author: stevestein
ms.author: sstein
ms.openlocfilehash: c4f0ceb580ddc7538dd1ea98b9e08a82cd8d35b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044487"
---
# <a name="sysmailhelpprofileaccountsp-transact-sql"></a>sysmail_help_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  1 つ以上のデータベース メール プロファイルに関連付けられているアカウントを一覧表示します。  
    
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_help_profileaccount_sp  
   {   [ @profile_id = ] profile_id   
      | [ @profile_name = ] 'profile_name' }  
   [ , {   [ @account_id = ] account_id  
         | [ @account_name = ] 'account_name' } ]  
```  
  
## <a name="arguments"></a>引数  
`[ @profile_id = ] profile_id` 表示するプロファイルのプロファイル ID です。 *profile_id*は**int**、既定値は NULL です。 いずれか*profile_id*または*profile_name*指定する必要があります。  
  
`[ @profile_name = ] 'profile_name'` 表示するプロファイルのプロファイル名です。 *profile_name*は**sysname**、既定値は NULL です。 いずれか*profile_id*または*profile_name*指定する必要があります。  
  
`[ @account_id = ] account_id` 一覧にアカウント ID です。 *account_id*は**int**、既定値は NULL です。 ときに*account_id*と*account_name*が両方の NULL の場合、プロファイル内のすべてのアカウントを一覧表示されます。  
  
`[ @account_name = ] 'account_name'` 一覧にアカウントの名前です。 *account_name*は**sysname**、既定値は NULL です。 ときに*account_id*と*account_name*が両方の NULL の場合、プロファイル内のすべてのアカウントを一覧表示されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 次の列を含む結果セットが返されます。  
  
||||  
|-|-|-|  
|列名|データ型|説明|  
|**profile_id**|**int**|プロファイルのプロファイル ID です。|  
|**profile_name**|**sysname**|プロファイルの名前。|  
|**account_id**|**int**|アカウントのアカウント ID。|  
|**account_name**|**sysname**|アカウントの名前。|  
|**sequence_number**|**int**|プロファイル内のアカウントのシーケンス番号。|  
  
## <a name="remarks"></a>コメント  
 ない場合*profile_id*または*profile_name*を指定すると、このストアド プロシージャがインスタンス内のすべてのプロファイル情報を返します。  
  
 ストアド プロシージャ**sysmail_help_profileaccount_sp**では、 **msdb**が所有するデータベースにあり、 **dbo**スキーマ。 現在のデータベースがない場合、3 つの部分の名前を持つプロシージャを実行する必要があります**msdb**します。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの既定のメンバーへのアクセス許可を実行、 **sysadmin**固定サーバー ロール。  
  
## <a name="examples"></a>使用例  
 **A.名前で、特定のプロファイルのアカウントを一覧表示**  
  
 次の例ではの情報を一覧表示、`AdventureWorks Administrator`プロファイル名を指定してプロファイルできます。  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp  
   @profile_name = 'AdventureWorks Administrator';  
```  
  
 次に結果セットを示します。行の長さは編集されています。  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
```  
  
 **B.特定のプロファイルのプロファイル ID のアカウントを一覧表示**  
  
 次の例では、`AdventureWorks Administrator` プロファイルの情報を、プロファイル ID を指定して一覧表示します。  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp  
    @profile_id = 131 ;  
```  
  
 次に結果セットを示します。行の長さは編集されています。  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
```  
  
 **C.すべてのプロファイルのアカウントを一覧表示**  
  
 インスタンス内のすべてのプロファイルのアカウントを一覧表示する次の例を示しています。  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp;  
```  
  
 次に結果セットを示します。行の長さは編集されています。  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
106         AdventureWorks Operator      210         Operator-MainServer  1  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベース メール アカウントを作成します。](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [データベース メール構成オブジェクト](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [データベース メール ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
