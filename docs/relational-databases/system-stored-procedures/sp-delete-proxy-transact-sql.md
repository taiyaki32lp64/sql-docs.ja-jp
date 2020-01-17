---
title: sp_delete_proxy (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_proxy
- sp_delete_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_proxy
- DROP PROXY statement
ms.assetid: 44a1db13-b7f2-4dab-a1b5-b8dafb41737c
author: stevestein
ms.author: sstein
ms.openlocfilehash: fd717f645b9e53d08f6dabbfc1ea5779c373056e
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305110"
---
# <a name="sp_delete_proxy-transact-sql"></a>sp_delete_proxy (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定したプロキシを削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_delete_proxy [ @proxy_id = ] id , [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>引数  
`[ @proxy_id = ] id` 削除するプロキシのプロキシ識別番号を指定します。 *Proxy_id*は**int**,、既定値は NULL です。  
  
`[ @proxy_name = ] 'proxy_name'` 削除するプロキシの名前。 *Proxy_name*の部分は**sysname**で、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 **@No__t-1proxy_name**または **\@proxy_id**を指定する必要があります。 両方の引数を指定する場合は、両方とも同じプロキシを参照する必要があります。異なるプロキシを参照する場合、ストアド プロシージャは失敗します。  
  
 指定されたプロキシをジョブステップが参照している場合、プロキシを削除することはできず、ストアドプロシージャは失敗します。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sp_delete_proxy**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>使用例  
 次の例では、プロキシを削除 `Catalog application proxy` です。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_proxy  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_add_proxy &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)  
  
  
