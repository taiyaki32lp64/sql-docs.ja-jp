---
title: sysmail_help_profile_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_profile_sp_TSQL
- sysmail_help_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_profile_sp
ms.assetid: d7169a8e-92b1-49eb-9124-3b2f69755ddb
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2d8f2af3894377cc0922274ca26c231c003f3bd6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044503"
---
# <a name="sysmailhelpprofilesp-transact-sql"></a>sysmail_help_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  1 つ以上のメール プロファイルに関する情報を一覧表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_help_profile_sp  [   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @profile_id = ] profile_id` 情報を返すプロファイル id です。 *profile_id*は**int**、既定値は NULL です。  
  
`[ @profile_name = ] 'profile_name'` 情報を返すプロファイル名。 *profile_name*は**sysname**、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 次の列を含む結果セットが返されます。  
  
||||  
|-|-|-|  
|列名|データ型|説明|  
|**profile_id**|**int**|プロファイルのプロファイル id です。|  
|**name**|**sysname**|プロファイルのプロファイル名。|  
|**description**|**nvarchar (256)**|プロファイルの説明。|  
  
## <a name="remarks"></a>コメント  
 プロファイル名またはプロファイル id を指定すると、 **sysmail_help_profile_sp**そのプロファイルに関する情報を返します。 それ以外の場合、 **sysmail_help_profile_sp**のすべてのプロファイルに関する情報を返します、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンス。  
  
 ストアド プロシージャ**sysmail_help_profile_sp**では、 **msdb**が所有するデータベースにあり、 **dbo**スキーマ。 現在のデータベースがない場合、3 つの部分の名前を持つプロシージャを実行する必要があります**msdb**します。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの既定のメンバーへのアクセス許可を実行、 **sysadmin**固定サーバー ロール。  
  
## <a name="examples"></a>使用例  
 **A.すべてのプロファイルを一覧表示**  
  
 次の例では、インスタンス内のすべてのプロファイルを一覧表示を示します。  
  
```  
EXECUTE msdb.dbo.sysmail_help_profile_sp;  
```  
  
 行の長さを再フォーマット、サンプルの結果セットを次に示します。  
  
```  
profile_id  name                          description  
----------- ----------------------------- ------------------------------  
56          AdventureWorks Administrator  Administrative mail profile.    
57          AdventureWorks Operator       Operator mail profile.          
```  
  
 **B.特定のプロファイルを一覧表示します。**  
  
 次の例では、プロファイル `AdventureWorks Administrator` に関する情報を一覧表示します。  
  
```  
EXECUTE msdb.dbo.sysmail_help_profile_sp  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
 行の長さを再フォーマット、サンプルの結果セットを次に示します。  
  
```  
profile_id  name                          description  
----------- ----------------------------- ------------------------------  
56          AdventureWorks Administrator  Administrative mail profile.    
```  
  
## <a name="see-also"></a>関連項目  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [データベース メール ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
