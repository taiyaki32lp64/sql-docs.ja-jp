---
title: sp_droprole (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droprole
- sp_droprole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droprole
ms.assetid: 889ee074-00f8-40a9-bddb-d7d3ef0cbc19
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2573019948a326c9171fc83d62428e7e2f888eb5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933817"
---
# <a name="spdroprole-transact-sql"></a>sp_droprole (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のデータベースからデータベース ロールを削除します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、 **Sp_droprole** DROP ROLE ステートメントに置き換えられています。 **sp_droprole**が以前のバージョンの互換性のためだけに含まれる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将来のリリースではサポートされない可能性があります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_droprole [ @rolename= ] 'role'  
```  
  
## <a name="arguments"></a>引数  
`[ @rolename = ] 'role'` 現在のデータベースから削除するデータベース ロールの名前です。 *ロール*は、 **sysname**、既定値はありません。 *ロール*現在のデータベースに既に存在する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 使用してデータベースの役割のみを削除できる**sp_droprole**します。  
  
 メンバーが既に存在するデータベース ロールは削除できません。 データベース ロールを削除するには、あらかじめそのデータベース ロールのすべてのメンバーを削除しておく必要があります。 ロールからユーザーを削除するには使用**sp_droprolemember**します。 すべてのユーザーは、ロールのメンバーではまだ場合**sp_droprole**それらのメンバーが表示されます。  
  
 固定ロールと**パブリック**ロールは削除できません。  
  
 保護可能なアイテムが所有している場合、ロールを削除できません。 セキュリティ保護可能なリソースを所有しているアプリケーション ロールを削除するには、先にセキュリティ保護可能なリソースの所有権を譲渡するか削除する必要があります。 削除する必要がないオブジェクトの所有者を変更するのにには、ALTER AUTHORIZATION を使用します。  
  
 **sp_droprole**ユーザー定義のトランザクション内で実行することはできません。  
  
## <a name="permissions"></a>アクセス許可  
 ロールに対する CONTROL 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、アプリケーション ロール `Sales` を削除します。  
  
```  
EXEC sp_droprole 'Sales';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sp_dropapprole &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropapprole-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
