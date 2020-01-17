---
title: sp_migrate_user_to_contained (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/11/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_migrate_user_to_contained
- sp_migrate_user_to_contained_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_migrate_user_to_contained
ms.assetid: b3a49ff6-46ad-4ee7-b6fe-7e54213dc33e
author: stevestein
ms.author: sstein
ms.openlocfilehash: d5bcafb24313851f58fd18fc19ebabd0ee98f6dd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022332"
---
# <a name="spmigrateusertocontained-transact-sql"></a>sp_migrate_user_to_contained (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  変換にマップされているデータベース ユーザー、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パスワードを持つ包含データベース ユーザーへのログイン。 包含データベースでは、データベースがインストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの依存関係を削除するには、このプロシージャを使用します。 **sp_migrate_user_to_contained** 、元のユーザーを区切る[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログイン、パスワードや既定の言語などの設定、包含データベースに対して個別に管理できるようにします。 **sp_migrate_user_to_contained**の別のインスタンスに包含データベースを移動する前に使用することができます、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]現在への依存関係を排除する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンス ログインします。  
  
> [!NOTE]
> 使用する場合は注意**sp_migrate_user_to_contained**効果を反転することはできません。 この手順は、包含データベースでのみ使用されます。 詳細については、「 [包含データベース](../../relational-databases/databases/contained-databases.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_migrate_user_to_contained [ @username = ] N'user' ,   
    [ @rename = ] { N'copy_login_name' | N'keep_name' } ,   
    [ @disablelogin = ] { N'disable_login' | N'do_not_disable_login' }   
```  
  
## <a name="arguments"></a>引数  
 [ **@username =** ] **N'***ユーザー***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証ログインにマップされた、現在の包含データベースのユーザーの名前を指定します。 値が**sysname**、既定値は**NULL**します。  
  
 [ **@rename =** ] **N'***copy_login_name***'**  | **N'***keep_name***'**  
 ログインに基づくデータベース ユーザーのログイン名よりも、別のユーザー名のときに使用*keep_name*移行中にデータベース ユーザー名を保持します。 使用*copy_login_name* user の代わりに、ログインの名前を持つ新しい包含データベース ユーザーを作成します。 ログインに基づくデータベース ユーザーがログイン名と同じユーザー名を持つ場合は、どちらのオプションでも、名前を変更することなく包含データベース ユーザーが作成されます。  
  
 [ **@disablelogin =** ] **N'***disable_login***'**  | **N'***do_not_disable_login***'**  
 *disable_login* master データベースにログインを無効にします。 ログインが無効にするとを接続する接続が、包含データベースの名前を入力する必要があります、**初期カタログ**接続文字列の一部として。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_migrate_user_to_contained**プロパティやログインのアクセス許可に関係なく、パスワードを持つ包含データベース ユーザーを作成します。 たとえば、プロシージャが正常に完了、ログインが無効になっている場合、またはユーザーが拒否された場合、 **CONNECT**データベースに対する権限。  
  
 **sp_migrate_user_to_contained**は次の制限があります。  
  
-   データベース内に存在しないユーザー名を指定する必要がある。  
  
-   dbo や guest などの組み込みのユーザーは変換できない。  
  
-   ユーザーを指定することはできません、 **EXECUTE AS**署名されたストアド プロシージャの句。  
  
-   ユーザーが含まれるストアド プロシージャを所有できない、 **EXECUTE AS OWNER**句。  
  
-   **sp_migrate_user_to_contained**システム データベースでは使用できません。  
  
## <a name="security"></a>セキュリティ  
 ユーザーを移行する場合は、無効にするか、またはのインスタンスからすべての管理者ログインを削除しないように注意する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 すべてのログインが削除された場合は、次を参照してください。 [SQL Server システム管理者がロックアウトされた場合に接続する](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)します。  
  
 場合、 **builtin \administrators**ログインが存在する、管理者を使用して、アプリケーションを起動して接続できる、**管理者として実行**オプション。  
  
### <a name="permissions"></a>アクセス許可  
 **CONTROL SERVER** 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-migrating-a-single-user"></a>A. 単一のユーザーを移行する  
 次の例では、移行、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]という名前のログイン`Barry`パスワードを持つ包含データベース ユーザーにします。 この例では、ユーザー名を変更することはできませんし、ログインを有効になっている保持されます。  
  
```sql  
sp_migrate_user_to_contained   
@username = N'Barry',  
@rename = N'keep_name',  
@disablelogin = N'do_not_disable_login' ;  
  
```  
  
### <a name="b-migrating-all-database-users-with-logins-to-contained-database-users-without-logins"></a>B. ログインのあるすべてのデータベース ユーザーをログインなしの包含データベース ユーザーに移行する  
 次の例では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインに基づくすべてのユーザーを、パスワードを持つ包含データベース ユーザーに移行します。 有効になっていないログインは除外します。 この例は、包含データベースで実行する必要があります。  
  
```sql  
DECLARE @username sysname ;  
DECLARE user_cursor CURSOR  
    FOR   
        SELECT dp.name   
        FROM sys.database_principals AS dp  
        JOIN sys.server_principals AS sp   
        ON dp.sid = sp.sid  
        WHERE dp.authentication_type = 1 AND sp.is_disabled = 0;  
OPEN user_cursor  
FETCH NEXT FROM user_cursor INTO @username  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        EXECUTE sp_migrate_user_to_contained   
        @username = @username,  
        @rename = N'keep_name',  
        @disablelogin = N'disable_login';  
    FETCH NEXT FROM user_cursor INTO @username  
    END  
CLOSE user_cursor ;  
DEALLOCATE user_cursor ;  
```  
  
## <a name="see-also"></a>参照  
 [Migrate to a Partially Contained Database](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)   
 [包含データベース](../../relational-databases/databases/contained-databases.md)  
  
  
