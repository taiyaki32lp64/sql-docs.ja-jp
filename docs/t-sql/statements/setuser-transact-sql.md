---
title: SETUSER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SETUSER_TSQL
- SETUSER
dev_langs:
- TSQL
helpviewer_keywords:
- delegation [SQL Server]
- impersonation [SQL Server]
- SETUSER statement
- user impersonation [SQL Server]
ms.assetid: 7acfac5c-9ad6-4226-b874-7add36c4ea43
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 66830b3000d749ab17a5800c3450c5880c5d1aba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076443"
---
# <a name="setuser-transact-sql"></a>SETUSER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  固定サーバー ロール **sysadmin** のメンバーまたはデータベースの所有者が、別のユーザーの権限を借用できるようにします。  
  
> [!IMPORTANT]  
>  SETUSER は旧バージョンとの互換性のためだけに用意されています。 SETUSER は、将来の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リリースではサポートされない可能性があります。 代わりに [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md) を使用することをお勧めします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
SETUSER [ 'username' [ WITH NORESET ] ]   
```  
  
## <a name="arguments"></a>引数  
 **'** *username* **'**  
 権限の借用の対象となる、現在のデータベース内の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーまたは Windows ユーザーの名前です。 *username* を指定しない場合、ユーザーの権限を借用するシステム管理者またはデータベース所有者の元の ID 状態に戻ります。  
  
 WITH NORESET  
 後に *username* の指定されていない SETUSER ステートメントがあっても、システム管理者またはデータベース所有者の元の ID 状態にリセットされないことを指定します。  
  
## <a name="remarks"></a>Remarks  
 固定サーバー ロール **sysadmin** のメンバーまたはデータベースの所有者は、SETUSER を使用して別のユーザーの ID を借用し、そのユーザーの権限をテストできます。 db_owner 固定データベース ロールのメンバーシップが十分ではありません。  
  
 SETUSER は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーに対してだけ使用してください。 SETUSER は Windows ユーザーに対してはサポートされていません。 SETUSER を使用して別のユーザーの ID の権限を借用している場合、権限を借用しているユーザーが作成するすべてのオブジェクトは、権限を借用されているユーザーによって所有されます。 たとえば、データベース所有者が **Margaret** というユーザーの ID を借用し、**orders** というテーブルを作成する場合、**orders** テーブルは、システム管理者ではなく、**Margaret** によって所有されます。  
  
 SETUSER ステートメントは、別の SETUSER ステートメントを実行するか、現在のデータベースを USE ステートメントで変更するまで有効になります。  
  
> [!NOTE]  
>  SETUSER WITH NORESET を使用すると、データベース所有者またはシステム管理者が自分の権限を回復するには、いったんログ オフしてからもう一度ログ オンするしかありません。  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップを持っているか、またはデータベースの所有者である必要があります。 **db_owner** 固定データベース ロールのメンバーシップでは十分ではありません。  
  
## <a name="examples"></a>使用例  
 この例では、データベース所有者が別のユーザーの ID を借用する方法を示します。 ユーザー `mary` は、`computer_types` という名前のテーブルを作成しました。 SETUSER を使用して、データベース所有者は `mary` の権限を借用し、ユーザー `joe` に `computer_types` テーブルへのアクセス権を与え、その後自分自身の ID をリセットします。  
  
```  
SETUSER 'mary';  
GO  
GRANT SELECT ON computer_types TO joe;  
GO  
--To revert to the original user  
SETUSER;  
```  
  
## <a name="see-also"></a>参照  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  
  
  
