---
title: sp_droprolemember (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droprolemember_TSQL
- sp_droprolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droprolemember
ms.assetid: c2f19ab1-e742-4d56-ba8e-8ffd40cf4925
ms.author: vanto
author: VanMSFT
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7123c1bd3fee61a3d0671a0d8fbe27c2943ba7ea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124847"
---
# <a name="spdroprolemember-transact-sql"></a>sp_droprolemember (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  現在のデータベースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ロールからセキュリティ アカウントを削除します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md)代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  

### <a name="syntax-for-both-sql-server-and-azure-sql-database"></a>SQL Server と Azure SQL Database の両方の構文

```  
sp_droprolemember [ @rolename = ] 'role' ,   
     [ @membername = ] 'security_account'  
```  

### <a name="syntax-for-both-azure-sql-data-warehouse-and-parallel-data-warehouse"></a>Azure SQL Data Warehouse と Parallel Data Warehouse の両方の構文

```  
sp_droprolemember 'role' ,  
     'security_account'  
```  
  
## <a name="arguments"></a>引数  
`[ @rolename = ] 'role'` メンバーの削除元となるロールの名前です。 *ロール*は**sysname**、既定値はありません。 *ロール*現在のデータベースに存在する必要があります。  
  
`[ @membername = ] 'security_account'` ロールから削除されているセキュリティ アカウントの名前。 *これ*は**sysname**、既定値はありません。 *これ*データベース ユーザー、別のデータベース ロール、Windows ログイン、または Windows グループにすることができます。 *これ*現在のデータベースに存在する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 sp_droprolemember の各は、sysmembers テーブルから行を削除することによって、データベース ロールからメンバーを削除します。 メンバーがロールから削除されたときに、メンバーには、そのロールのメンバーシップがあるすべてのアクセス許可が失われます。  
  
 固定サーバー ロールからユーザーを削除するには、sp_dropsrvrolemember を使用します。 パブリックのロールからユーザーを削除して、dbo はどのロールから削除することはできません。  
  
 メンバーを表示する sp_helpuser を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ロール、および使用する ALTER ROLE をロールにメンバーを追加します。  
  
## <a name="permissions"></a>アクセス許可  
 ロールに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、ロール `JonB` からユーザー `Sales` を削除します。  
  
```sql
EXEC sp_droprolemember 'Sales', 'Jonb';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 次の例では、ロール `JonB` からユーザー `Sales` を削除します。  
  
```sql
EXEC sp_droprolemember 'Sales', 'JonB'  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)   
 [sp_dropsrvrolemember &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [sp_helpuser &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

