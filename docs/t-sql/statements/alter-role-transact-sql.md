---
title: ALTER ROLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_ROLE_TSQL
- ALTER ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- modifying database roles
- ALTER ROLE statement
- renaming database roles
- database roles [SQL Server], modifying
- names [SQL Server], database roles
ms.assetid: e1e83caa-17cc-4871-b2db-2711339fb64f
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d2adf7404e80a0a04932c14b598011c1799b5611
ms.sourcegitcommit: 94f6a4b506dfda242fc3efb2403847e22a36d340
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/30/2019
ms.locfileid: "75546571"
---
# <a name="alter-role-transact-sql"></a>ALTER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  データベース ロールのメンバーを追加または削除するか、ユーザー定義のデータベース ロールの名前を変更します。  
  
> [!NOTE]  
>  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] のメンバーを追加または削除するロールを変更するには、[sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) と [sp_droprolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md) を使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for SQL Server (starting with 2012) and Azure SQL Database  
  
ALTER ROLE  role_name  
{  
       ADD MEMBER database_principal  
    |  DROP MEMBER database_principal  
    |  WITH NAME = new_name  
}  
[;]  
```  
  
 
```  
-- Syntax for SQL Server 2008, Azure SQL Data Warehouse and Parallel Data Warehouse
  
-- Change the name of a user-defined database role  
ALTER ROLE role_name   
    WITH NAME = new_name  
[;]  
```  
  
## <a name="arguments"></a>引数  
 *role_name*  
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (2008 以降)、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 変更するデータベース ロールを指定します。  
  
 ADD MEMBER *database_principal*  
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (2012 以降)、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 データベース ロールのメンバーシップにデータベース プリンシパルを追加することを指定します。  
  
-   *database_principal* はデータベース ユーザーまたはユーザー定義データベース ロールです。  
  
-   *database_principal* には固定データベース ロールまたはサーバー プリンシパルは指定できません。  
  
DROP MEMBER *database_principal*  
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (2012 以降)、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 データベース ロールのメンバーシップからデータベース プリンシパルを削除することを指定します。  
  
-   *database_principal* はデータベース ユーザーまたはユーザー定義データベース ロールです。  
  
-   *database_principal* には固定データベース ロールまたはサーバー プリンシパルは指定できません。  
  
WITH NAME = *new_name*  
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (2008 以降)、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 ユーザー定義データベース ロールの名前を変更することを指定します。 データベース内に存在しない新しい名前を指定してください。  
  
 データベース ロールの名前を変更しても、ロールの ID 番号、所有者、権限は変わりません。  
  
## <a name="permissions"></a>アクセス許可  
 このコマンドを実行するには、以下の権限またはメンバーシップの 1 つ以上が必要です。  
  
-   ロールに対する **ALTER** 権限  
-   データベースに対する **ALTER ANY ROLE** 権限  
-   **db_securityadmin** 固定データベース ロールのメンバーシップ  
  
また、固定データベース ロールのメンバーシップを変更するには以下が必要です。  
  
-   **db_owner** 固定データベース ロールのメンバーシップ  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
 固定データベース ロールの名前は変更できません。  
  
## <a name="metadata"></a>メタデータ  
 これらのシステム ビューには、データベース ロールとデータベース プリンシパルに関する情報が格納されます。  
  
-   [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)  
  
-   [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
## <a name="examples"></a>例  
  
### <a name="a-change-the-name-of-a-database-role"></a>A. データベース ロールの名前の変更  
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (2008 以降)、[!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 次の例では、ロール `buyers` の名前を `purchasing` に変更します。   この例では、[AdventureWorks](https://msftdbprodsamples.codeplex.com/) サンプル データベースで実行できます。
  
```sql  
ALTER ROLE buyers WITH NAME = purchasing;  
```  
  
### <a name="b-add-or-remove-role-members"></a>B. ロール メンバーの追加または削除  
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (2012 以降)、[!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 この例では、`Sales` という名前のデータベース ロールを作成します。 メンバーシップに Barry という名前のデータベース ユーザーを追加してから、メンバー Barry を削除する方法を示します。   この例では、[AdventureWorks](https://msftdbprodsamples.codeplex.com/) サンプル データベースで実行できます。
  
```sql  
CREATE ROLE Sales;  
ALTER ROLE Sales ADD MEMBER Barry;  
ALTER ROLE Sales DROP MEMBER Barry;  
```  
  
## <a name="see-also"></a>参照  
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
