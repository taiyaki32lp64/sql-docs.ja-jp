---
title: sp_helpuser (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpuser
- sp_helpuser_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpuser
ms.assetid: 9c70b41d-ef4c-43df-92da-bd534c287ca1
author: stevestein
ms.author: sstein
ms.openlocfilehash: a170c5e43329d90a4977db12a98bd9d2e556e91d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68048164"
---
# <a name="sphelpuser-transact-sql"></a>sp_helpuser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のデータベースに存在するデータベース レベルのプリンシパルに関する情報をレポートします。  
  
> [!IMPORTANT]  
>  **sp_helpuser**で導入されたセキュリティ保護可能な情報は返されません[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]します。 使用[sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpuser [ [ @name_in_db = ] 'security_account' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @name_in_db = ] 'security_account'` データベース ユーザーまたは現在のデータベース内のデータベース ロールの名前です。 *これ*現在のデータベースに存在する必要があります。 *これ*は**sysname**、既定値は NULL です。 場合*これ*が指定されていない**sp_helpuser**すべてのデータベース プリンシパルに関する情報を返します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 次の表は、結果セットのどちらの場合、ユーザー アカウントも[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]か、または Windows ユーザーが指定*これ*。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**UserName**|**sysname**|現在のデータベース内のユーザー。|  
|**RoleName**|**sysname**|ロール**UserName**が属しています。|  
|**LoginName**|**sysname**|ログイン**UserName**します。|  
|**DefDBName**|**sysname**|既定のデータベース**UserName**します。|  
|**DefSchemaName**|**sysname**|データベース ユーザーの既定のスキーマ。|  
|**UserID**|**smallint**|ID **UserName**現在のデータベースでします。|  
|**SID**|**smallint**|ユーザーのセキュリティ識別番号 (SID)。|  
  
 次の表では、ユーザー アカウントが指定されていないと、エイリアスは、現在のデータベースに存在する場合の結果セットを示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|現在のデータベースに存在するユーザーの別名であるログイン。|  
|**UserNameAliasedTo**|**sysname**|ログインがエイリアス化される現在のデータベース内のユーザー名。|  
  
 次の表は、ロールが指定されている場合の結果セット*これ*します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**Role_name**|**sysname**|現在のデータベース ロールの名前。|  
|**Role_id**|**smallint**|現在のデータベースで、ロールのロール ID。|  
|**Users_in_role**|**sysname**|現在のデータベース ロールのメンバー。|  
|**ユーザー Id**|**smallint**|ロールのメンバーのユーザー ID。|  
  
## <a name="remarks"></a>コメント  
 データベース ロールのメンバーシップに関する情報を表示する[sys.database_role_members](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)します。 サーバー ロールのメンバーに関する情報を表示する[sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)、サーバー レベル プリンシパルに関する情報を表示する[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)します。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
 返される情報は、メタデータへのアクセスの制限が適用されます。 これで、権限がプリンシパルにないエンティティは表示されません。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-listing-all-users"></a>A. すべてのユーザーを表示する  
 次の例では、現在のデータベースに存在するすべてのユーザーを表示します。  
  
```  
EXEC sp_helpuser;  
```  
  
### <a name="b-listing-information-for-a-single-user"></a>B. 特定のユーザーの情報を表示する  
 次の例は、ユーザー データベースの所有者に関する情報を一覧表示 (`dbo`)。  
  
```  
EXEC sp_helpuser 'dbo';  
```  
  
### <a name="c-listing-information-for-a-database-role"></a>C. データベース ロールに関する情報を表示  
 次の例では、`db_securityadmin` 固定データベース ロールに関する情報を表示します。  
  
```  
EXEC sp_helpuser 'db_securityadmin';  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
  
