---
title: sp_unsetapprole (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_unsetapprole_TSQL
- sp_unsetapprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unsetapprole
ms.assetid: 4c4033d3-1a34-4dfb-835d-e3293d1a442d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9cf190198859bb3202dc2bcc62b066e5995d8fed
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305163"
---
# <a name="sp_unsetapprole-transact-sql"></a>sp_unsetapprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  アプリケーション ロールを非アクティブ化し、以前のセキュリティ コンテキストに戻します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_unsetapprole @cookie   
```  
  
## <a name="arguments"></a>引数  
 **\@cookie**  
 アプリケーション ロールがアクティブ化されたときに作成されたクッキーを指定します。 クッキーは[sp_setapprole &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)によって作成されます。 **varbinary (8000)** 。  
  
> [!NOTE]  
>  **sp_setapprole** のクッキーの **OUTPUT** パラメーターは現在、適切な最大長である **varbinary(8000)** としてドキュメントに記載されています。 ただし、現在の実装では **varbinary(50)** を返します。 アプリケーションは、今後のリリースでクッキーの戻り値のサイズが増加した場合にアプリケーションが引き続き正常に動作するように、 **varbinary (8000)** を引き続き予約する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) と 1 (失敗)  
  
## <a name="remarks"></a>Remarks  
 **Sp_setapprole**を使用してアプリケーションロールをアクティブ化した後は、ユーザーがサーバーとの接続を切断するか**sp_unsetapprole**を実行するまで、ロールはアクティブのままになります。  
  
 アプリケーションロールの概要については、「[アプリケーションロール](../../relational-databases/security/authentication-access/application-roles.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 アプリケーションロールがアクティブ化されたときに保存された cookie の**メンバーシップとナレッジ**のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="activating-an-application-role-with-a-cookie-then-reverting-to-the-previous-context"></a>クッキーの作成を指定してアプリケーション ロールをアクティブ化し、その後以前のコンテキストに戻す  
 次の例では、パスワード `Sales11` が設定されているアプリケーション ロール `fdsd896#gfdbfdkjgh700mM` をアクティブ化し、クッキーを作成します。 この例では、現在のユーザーの名前を返し、 **sp_unsetapprole**を実行して元のコンテキストに戻します。  
  
```  
DECLARE @cookie varbinary(8000);  
EXEC sp_setapprole 'Sales11', 'fdsd896#gfdbfdkjgh700mM'  
    , @fCreateCookie = true, @cookie = @cookie OUTPUT;  
-- The application role is now active.  
SELECT USER_NAME();  
-- This will return the name of the application role, Sales11.  
EXEC sp_unsetapprole @cookie;  
-- The application role is no longer active.  
-- The original context has now been restored.  
GO  
SELECT USER_NAME();  
-- This will return the name of the original user.   
GO   
```  
  
## <a name="see-also"></a>参照  
 [sp_setapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md)  
  
  
