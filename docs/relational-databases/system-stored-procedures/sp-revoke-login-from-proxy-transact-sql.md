---
title: sp_revoke_login_from_proxy (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revoke_login_from_proxy_TSQL
- sp_revoke_login_from_proxy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revoke_login_from_proxy
ms.assetid: e4546c13-9fba-4bab-8b42-d6f18b33ec25
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0aad616275d635ac32d6e81dbc5321db0db58b34
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019939"
---
# <a name="sprevokeloginfromproxy-transact-sql"></a>sp_revoke_login_from_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  セキュリティ プリンシパルが持つプロキシへのアクセスを取り消します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_revoke_login_from_proxy   
    [ @name = ] 'name' ,  
    [ @proxy_id = ] id ,  
    [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>引数  
`[ @name = ] 'name'` 名前、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログイン、サーバー ロール、または**msdb**へのアクセスを削除するデータベース ロール。 *名前*は**nvarchar (256)** 既定値はありません。  
  
`[ @proxy_id = ] id` アクセスを取り消すプロキシの id。 いずれか*id*または*proxy_name*指定する必要がありますが、両方を指定することはできません。 *Id*は**int**、既定値は NULL です。  
  
`[ @proxy_name = ] 'proxy_name'` アクセスを取り消すプロキシの名前。 いずれか*id*または*proxy_name*指定する必要がありますが、両方を指定することはできません。 *Proxy_name*は**sysname**、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 ログインによって所有されるジョブがこのプロキシを参照する場合、そのジョブは実行できなくなります。  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャを実行するには、 **sysadmin** 固定サーバー ロールのメンバーであることが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、ログイン `terrid` に対して、プロキシ `Catalog application proxy` へのアクセスを禁止します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_login_from_proxy  
    @name = N'terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [SQL Server エージェント ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_help_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)  
  
  
