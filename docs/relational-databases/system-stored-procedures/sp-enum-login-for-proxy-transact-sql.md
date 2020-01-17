---
title: sp_enum_login_for_proxy (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_enum_login_for_proxy_TSQL
- sp_enum_login_for_proxy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_login_for_proxy
ms.assetid: 62a75019-248a-44c8-a5cc-c79f55ea3acf
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: ee6b6a701d4ff81863973c4c8e098bd9ed49c967
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124679"
---
# <a name="spenumloginforproxy-transact-sql"></a>sp_enum_login_for_proxy (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  セキュリティ プリンシパルとプロキシ間の関連付けを一覧表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_enum_login_for_proxy  
    [ @name = ] 'name'  
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>引数  
`[ @name = ] 'name'` 名前、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]プリンシパル、ログイン、サーバー ロール、または**msdb**プロキシを一覧表示するデータベース ロール。 名前は**nvarchar (256)** 、既定値は NULL です。  
  
`[ @proxy_id = ] id` に関する情報を表示するプロキシのプロキシ識別番号。 *Proxy_id*は**int**、既定値は NULL です。 いずれか、 *id*または*proxy_name*指定することがあります。  
  
`[ @proxy_name = ] 'proxy_name'` に関する情報を表示するプロキシの名前。 *Proxy_name*は**sysname**、既定値は NULL です。 いずれか、 *id*または*proxy_name*指定することがあります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|プロキシ識別番号。|  
|**proxy_name**|**sysname**|プロキシの名前。|  
|**name**|**sysname**|関連付けのセキュリティ プリンシパルの名前を指定します。|  
|**flags**|**int**|セキュリティ プリンシパルの種類<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログイン<br /><br /> **1** = 固定システム ロール<br /><br /> **2**データベース ロールを = **msdb**|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="remarks"></a>コメント  
 パラメーターが指定されていないときに**sp_enum_login_for_proxy**各プロキシのインスタンス内のすべてのログインに関する情報を一覧表示します。  
  
 プロキシ id またはプロキシ名を指定する、 **sp_enum_login_for_proxy**をプロキシへのアクセスを持つログインを一覧表示されます。 ログイン名を指定すると、 **sp_enum_login_for_proxy**へのアクセスをログインにはプロキシは、リスト。  
  
 プロキシ情報とログイン名の両方が指定されている場合、結果セットは、指定されたログインに指定したプロキシへのアクセスがある場合、行を返します。  
  
 このストアド プロシージャにある**msdb**します。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの既定のメンバーへのアクセス許可を実行、 **sysadmin**固定サーバー ロール。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-listing-all-associations"></a>A. すべての関連付けを一覧表示する  
 次の例では、現在のインスタンスで、ログインとプロキシの間で確立されているすべてのアクセス許可が一覧表示します。  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy ;  
GO  
```  
  
### <a name="b-listing-proxies-for-a-specific-login"></a>B. 指定したログインに対するプロキシを一覧表示する  
 次の例では、ログイン `terrid` がアクセスできるプロキシを一覧表示します。  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy  
    @name = 'terrid' ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_help_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
