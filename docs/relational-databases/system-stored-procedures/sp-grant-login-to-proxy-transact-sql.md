---
title: sp_grant_login_to_proxy (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grant_login_to_proxy
- sp_grant_login_to_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grant_login_to_proxy
ms.assetid: 90e1a6d5-a692-4462-a163-4b0709d83150
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: bdfeab5754a2397c01ace2bb9f822fa168eeef6b
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005858"
---
# <a name="sp_grant_login_to_proxy-transact-sql"></a>sp_grant_login_to_proxy (Transact-sql)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  プロキシへのセキュリティプリンシパルアクセスを許可します。  

  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_grant_login_to_proxy   
     { [ @login_name = ] 'login_name'   
     | [ @fixed_server_role = ] 'fixed_server_role'   
     | [ @msdb_role = ] 'msdb_role' } ,   
     { [ @proxy_id = ] id | [ @proxy_name = ] 'proxy_name' }  
```  
  
## <a name="arguments"></a>引数  
アクセス権を付与するログイン名 `[ @login_name = ] 'login_name'` ます。 *Login_name*は**nvarchar (256)** ,、既定値は NULL です。 **\@login_name**、 **\@fixed_server_role**、または **\@msdb_role**のいずれかを指定する必要があります。指定しないと、ストアドプロシージャは失敗します。  
  
へのアクセスを許可する固定サーバーロールを `[ @fixed_server_role = ] 'fixed_server_role'` します。 *Fixed_server_role*は**nvarchar (256)** 、既定値は NULL です。 **\@login_name**、 **\@fixed_server_role**、または **\@msdb_role**のいずれかを指定する必要があります。指定しないと、ストアドプロシージャは失敗します。  
  
アクセスを許可する**msdb**データベースのデータベースロールを `[ @msdb_role = ] 'msdb_role'` します。 *Msdb_role*は**nvarchar (256)** ,、既定値は NULL です。 **\@login_name**、 **\@fixed_server_role**、または **\@msdb_role**のいずれかを指定する必要があります。指定しないと、ストアドプロシージャは失敗します。  
  
アクセス権を付与するプロキシの識別子を `[ @proxy_id = ] id` します。 *Id*は**int**,、既定値は NULL です。 **\@proxy_id**または **\@proxy_name**のいずれかを指定する必要があります。指定しないと、ストアドプロシージャは失敗します。  
  
`[ @proxy_name = ] 'proxy_name'` アクセス権を付与するプロキシの名前を指定します。 *Proxy_name*は**nvarchar (256)** ,、既定値は NULL です。 **\@proxy_id**または **\@proxy_name**のいずれかを指定する必要があります。指定しないと、ストアドプロシージャは失敗します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>Remarks  
 **sp_grant_login_to_proxy**は、 **msdb**データベースから実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_grant_login_to_proxy**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>使用例  
 次の例では、ログイン `adventure-works\terrid` に対してプロキシ `Catalog application proxy` の使用を許可します。  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_login_to_proxy  
    @login_name = N'adventure-works\terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [transact-sql &#40;  の&#41; sp_add_proxy](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)  
 [sp_revoke_login_from_proxy &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
