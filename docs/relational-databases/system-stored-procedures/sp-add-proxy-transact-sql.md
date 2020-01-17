---
title: sp_add_proxy (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_proxy
- sp_add_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE PROXY statement
- sp_add_proxy
ms.assetid: cb59df37-f103-439b-bec1-2871fb669a8b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4aa4120db7b45cb0b3a7d7a10bb53931b8300d9d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088472"
---
# <a name="spaddproxy-transact-sql"></a>sp_add_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定した追加[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント プロキシ。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_add_proxy  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @enabled = ] is_enabled ,  
    [ @description = ] 'description' ,  
    [ @credential_name = ] 'credential_name' ,  
    [ @credential_id = ] credential_id ,  
    [ @proxy_id = ] id OUTPUT   
```  
  
## <a name="arguments"></a>引数  
`[ @proxy_name = ] 'proxy_name'` 作成するプロキシの名前。 *Proxy_name*は**sysname**、既定値は NULL です。 ときに、 *proxy_name*が NULL または空の文字列、プロキシは既定の名前、 *user_name*指定します。  
  
`[ @enabled = ] is_enabled` プロキシが有効になっているかどうかを指定します。 *Is_enabled*フラグが**tinyint**、既定値は 1 です。 ときに*is_enabled*は**0**プロキシが有効でないと、ジョブ ステップでは使用できません。  
  
`[ @description = ] 'description'` プロキシの説明。 この説明は、 **nvarchar (512)** 、既定値は NULL です。 この説明はプロキシを記述する場合の参照情報として利用できますが、それ以外の目的では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによってこの説明が使用されることはありません。 そのため、この引数は省略可能です。  
  
`[ @credential_name = ] 'credential_name'` プロキシの資格情報の名前。 *Credential_name*は**sysname**、既定値は NULL です。 いずれか*credential_name*または*credential_id*指定する必要があります。  
  
`[ @credential_id = ] credential_id` プロキシの資格情報の識別番号。 *Credential_id*は**int**、既定値は NULL です。 いずれか*credential_name*または*credential_id*指定する必要があります。  
  
`[ @proxy_id = ] id OUTPUT` 正常に作成された場合は、プロキシに割り当てられているプロキシ識別番号。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 このストアド プロシージャを実行する必要があります、 **msdb**データベース。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシは、[!INCLUDE[tsql](../../includes/tsql-md.md)] サブシステム以外のサブシステムが含まれるジョブ ステップのセキュリティを管理します。 各プロキシには対応するセキュリティ資格情報が 1 つあります。 プロキシは、任意の数のサブシステムにアクセスする可能性があります。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定セキュリティ ロールは、このプロシージャを実行できます。  
  
 メンバー、 **sysadmin**固定セキュリティ ロールは、任意のプロキシを使用するジョブ ステップを作成できます。 ストアド プロシージャを使用して、 [sp_grant_login_to_proxy &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)プロキシに他のログイン アクセスを許可します。  
  
## <a name="examples"></a>使用例  
 この例は、資格情報のプロキシを作成します`CatalogApplicationCredential`します。 コードでは、資格情報が既に存在することを前提としています。 資格情報の詳細については、次を参照してください。 [CREATE CREDENTIAL &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_proxy  
    @proxy_name = 'Catalog application proxy',  
    @enabled = 1,  
    @description = 'Maintenance tasks on catalog application.',  
    @credential_name = 'CatalogApplicationCredential' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
