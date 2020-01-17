---
title: sp_dropuser (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropuser
- sp_dropuser_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropuser
ms.assetid: e28f18f9-7ecf-4568-89f4-fe5c520df386
author: stevestein
ms.author: sstein
ms.openlocfilehash: 42628ab49e30a4c6dada2eafb505435b8b389de6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124720"
---
# <a name="spdropuser-transact-sql"></a>sp_dropuser (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のデータベースからデータベース ユーザーを削除します。 **sp_dropuser**の旧バージョンとの互換性を備えている[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[DROP USER](../../t-sql/statements/drop-user-transact-sql.md)代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dropuser [ @name_in_db = ] 'user'  
```  
  
## <a name="arguments"></a>引数  
`[ @name_in_db = ] 'user'` 削除するユーザーの名前です。 *ユーザー*は、 **sysname**、既定値はありません。 *ユーザー*現在のデータベースに存在する必要があります。 Windows ログインを指定する場合は、データベースでログインとして認識されている名前を使用してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_dropuser**実行**sp_revokedbaccess**現在のデータベースからユーザーを削除します。  
  
 使用**sp_helpuser**現在のデータベースから削除できるユーザー名の一覧を表示します。  
  
 データベース ユーザーを削除すると、そのユーザーの別名も削除されます。 ユーザーに、ユーザーと同じ名前の空のスキーマが所有している場合は、スキーマが削除されます。 ユーザーに、その他のセキュリティ保護可能なデータベースが所有している場合、ユーザーは削除されません。 オブジェクトの所有権を別のプリンシパルに転送される必要があります。 詳細については、次を参照してください。 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md). データベース ユーザーを自動的に削除すると、そのユーザーに関連付けられているアクセス許可を削除し、ユーザーがメンバー データベース ロールから削除します。  
  
 **sp_dropuser**データベース所有者を削除するのには使用できません (**dbo**) **INFORMATION_SCHEMA**ユーザー、または**ゲスト**からユーザー、**マスター**または**tempdb**データベース。 システム以外のデータベース、`EXEC sp_dropuser 'guest'`ユーザーの CONNECT 権限を取り消す**ゲスト**します。 ユーザー自体は削除されません。  
  
 **sp_dropuser**ユーザー定義のトランザクション内で実行することはできません。  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する ALTER ANY USER 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、ユーザーを削除する`Albert`現在のデータベースから。  
  
```  
EXEC sp_dropuser 'Albert';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [sp_revokedbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
