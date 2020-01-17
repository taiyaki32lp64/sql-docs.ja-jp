---
title: サーバー レベルのロール | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.Security.BUILTIN.administrators
- sql12.Security.NT_AUTHORITY.SYSTEM
helpviewer_keywords:
- roles [SQL Server], server-level
- principals [SQL Server], server-level
- CONTROL SERVER permission
- fixed server roles [SQL Server]
- credentials [SQL Server], roles
- sysadmin fixed server role
- server-level roles [SQL Server]
- authentication [SQL Server], roles
ms.assetid: 7adf2ad7-015d-4cbe-9e29-abaefd779008
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 95ffdd52ff4c71039a87f177e67d51cb81830c68
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63011924"
---
# <a name="server-level-roles"></a>サーバー レベルのロール
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、サーバー上の権限を管理するためのサーバー レベルのロールを提供します。 これらのロールは、他のプリンシパルをグループ化するセキュリティ プリンシパルです。 サーバー レベルのロールは、その権限のスコープがサーバー全体に及びます (*ロール* は、Windows オペレーティング システムの *グループ* に似ています)。  
  
 固定サーバー ロールは、旧バージョンとの互換性を維持するために便宜的に提供されています。 可能な限り、より詳細な権限を割り当ててください。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、9 つの固定サーバー ロールを提供します。 固定サーバー ロールに許可される権限は変更できません。 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]以降では、ユーザー定義のサーバー ロールを作成し、そのユーザー定義のサーバー ロールにサーバー レベルの権限を追加できます。  
  
 サーバー レベルのロールには、サーバー レベルのプリンシパル ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログイン、Windows アカウント、および Windows グループ) を追加できます。 固定サーバー ロールの各メンバーは、そのロールに他のログインを追加することができます。 ユーザー定義のサーバー ロールのメンバーは、そのロールに他のサーバー プリンシパルを追加できません。  
  
## <a name="fixed-server-level-roles"></a>固定サーバー レベル ロール  
 次の表に、固定サーバー レベル ロールとその機能を示します。  
  
|固定サーバー レベル ロール|説明|  
|------------------------------|-----------------|  
|sysadmin|sysadmin 固定サーバー ロールのメンバーは、サーバーに対するすべての操作を実行できます。|  
|serveradmin|serveradmin 固定サーバー ロールのメンバーは、サーバー全体の構成オプションを変更したり、サーバーをシャットダウンしたりできます。|  
|securityadmin|securityadmin 固定サーバー ロールのメンバーは、ログインとログインのプロパティを管理します。 このメンバーは、サーバー レベルの権限を許可、拒否、および禁止できます。 また、データベースにアクセスできる場合は、データベース レベルの権限も許可、拒否、および禁止できます。 また、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインのパスワードをリセットできます。<br /><br /> **\*\* セキュリティに関する注意 \*\*** セキュリティ管理者は、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] へのアクセスを許可する権限およびユーザー権限を構成する権限を使用して、ほとんどのサーバー権限を割り当てることができます。 `securityadmin`ロールを扱う必要がありますに相当する、`sysadmin`ロール。|  
|processadmin|processadmin 固定サーバー ロールのメンバーは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンス内で実行中のプロセスを終了できます。|  
|setupadmin|setupadmin 固定サーバー ロールのメンバーは、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを使用して、リンク サーバーを追加および削除できます。 (sysadmin メンバーシップは、 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]を使用するときに必要になります)。|  
|bulkadmin|bulkadmin 固定サーバー ロールのメンバーは、BULK INSERT ステートメントを実行できます。|  
|diskadmin|diskadmin 固定サーバー ロールは、ディスク ファイルを管理するために使用します。|  
|dbcreator|dbcreator 固定サーバー ロールのメンバーは、任意のデータベースを作成、変更、削除、および復元できます。|  
|public|すべての [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインは、public サーバー ロールに属しています。 サーバー プリンシパルにセキュリティ保護可能なオブジェクトに対する特定の権限が与えられていないか権限が拒否されている場合、そのユーザーは、そのオブジェクトに対して public に付与されている権限を継承します。 すべてのユーザーがオブジェクトを使用できるようにする場合は、対象のオブジェクトに public 権限のみを割り当てます。 public のメンバーシップを変更することはできません。<br /><br /> 注: public は、他のロールとは実装方法が異なります。 しかし、public から権限の許可、拒否、および取り消しを行うことができます。|  
  
## <a name="permissions-of-fixed-server-roles"></a>固定サーバー ロールの権限  
 各固定サーバー ロールには、特定の権限が割り当てられます。 サーバー ロールに割り当てられる権限のチャートについては、「 [データベース エンジンの固定サーバー ロールおよび固定データベース ロール](https://social.technet.microsoft.com/wiki/contents/articles/2024.database-engine-fixed-server-and-fixed-database-roles.aspx)」を参照してください。  
  
> [!IMPORTANT]  
>  `CONTROL SERVER` 権限は `sysadmin` 固定サーバー ロールと似ていますが、同じではありません。 権限があることはロールのメンバーシップを意味せず、ロールのメンバーシップによって権限は付与されません。 (例: `CONTROL SERVER` メンバーシップを意味しません、`sysadmin`固定サーバー ロール)。ただし、ロールと同等の権限の間で借用が可能な場合があります。 ほとんどの `DBCC` コマンドと多くのシステム プロシージャには、`sysadmin` 固定サーバー ロールのメンバーシップが必要です。 ストアド プロシージャを必要とする 171 のシステムの一覧について`sysadmin`メンバーシップ、ブログの投稿では、Andreas Wolter を参照してください[CONTROL SERVER と sysadmin/sa: 権限、システム プロシージャ、DBCC、自動スキーマ作成および権限。エスカレーション - 注意事項](http://www.insidesql.org/blogs/andreaswolter/2013/08/control-server-vs-sysadmin-sa-permissions-privilege-escalation-caveats)します。  
  
## <a name="server-level-permissions"></a>サーバーレベルの権限  
 ユーザー定義のサーバー ロールに追加できるのは、サーバー レベルの権限のみです。 サーバー レベルの権限の一覧を表示するには、次のステートメントを実行します。 サーバー レベルの権限は、次のとおりです。  
  
```sql  
SELECT * FROM sys.fn_builtin_permissions('SERVER') ORDER BY permission_name;  
```  
  
 権限の詳細については、「[アクセス許可 (データベース エンジン)](../permissions-database-engine.md)」および「[sys.fn_builtin_permissions &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql)」を参照してください。  
  
## <a name="working-with-server-level-roles"></a>サーバー レベルのロールの操作  
 次の表では、サーバー レベルのロールを操作するためのコマンド、ビュー、および関数について説明します。  
  
|機能|型|説明|  
|-------------|----------|-----------------|  
|[sp_helpsrvrole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql)|メタデータ|サーバー レベルのロールの一覧を返します。|  
|[sp_helpsrvrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql)|メタデータ|サーバー レベルのロールのメンバーに関する情報を返します。|  
|[sp_srvrolepermission &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql)|メタデータ|サーバー レベルのロールの権限を表示します。|  
|[IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](/sql/t-sql/functions/is-srvrolemember-transact-sql)|メタデータ|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインが、指定されたサーバー レベルのロールのメンバーであるかどうかを示します。|  
|[sys.server_role_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-role-members-transact-sql)|メタデータ|各サーバー レベルのロールのメンバーごとに 1 行のデータを返します。|  
|[sp_addsrvrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql)|コマンド|ログインをサーバー レベルのロールのメンバーとして追加します。 使用しないでください。 代わりに [ALTER SERVER ROLE](/sql/t-sql/statements/alter-server-role-transact-sql) を使用してください。|  
|[sp_dropsrvrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql)|コマンド|サーバー レベルのロールから、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインや、Windows ユーザーまたはグループを削除します。 使用しないでください。 代わりに [ALTER SERVER ROLE](/sql/t-sql/statements/alter-server-role-transact-sql) を使用してください。|  
|[CREATE SERVER ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-role-transact-sql)|コマンド|ユーザー定義サーバー ロールを作成します。|  
|[ALTER SERVER ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-role-transact-sql)|コマンド|サーバー ロールのメンバーシップを変更、またはユーザー定義のサーバー ロールの名前を変更します。|  
|[DROP SERVER ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-server-role-transact-sql)|コマンド|ユーザー定義サーバー ロールを削除します。|  
|[IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](/sql/t-sql/functions/is-srvrolemember-transact-sql)|関数|サーバー ロールのメンバーシップを決定します。|  
  
## <a name="see-also"></a>参照  
 [データベース レベルのロール](../authentication-access/database-level-roles.md)   
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/security-catalog-views-transact-sql)   
 [セキュリティ関数 &#40;Transact-SQL&#41;](/sql/t-sql/functions/security-functions-transact-sql)   
 [SQL Server の保護](../securing-sql-server.md)   
 [GRANT (サーバー プリンシパルの権限の許可) &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-server-principal-permissions-transact-sql)   
 [REVOKE (サーバー プリンシパルの権限の取り消し) &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-server-principal-permissions-transact-sql)   
 [DENY (サーバー プリンシパルの権限の拒否) &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-server-principal-permissions-transact-sql)   
 [サーバー ロールの作成](../authentication-access/create-a-server-role.md)  
  
  
