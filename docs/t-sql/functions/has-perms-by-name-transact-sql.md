---
title: HAS_PERMS_BY_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HAS_PERMS_BY_NAME
- HAS_PERMS_BY_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], verifying
- current permission status
- checking permission status
- verifying permission status
- testing permissions
- HAS_PERMS_BY_NAME function
ms.assetid: eaf8cc82-1047-4144-9e77-0e1095df6143
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1420c5f8a1a16dc7430af0b445a8464c16d1b763
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982949"
---
# <a name="has_perms_by_name-transact-sql"></a>HAS_PERMS_BY_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  セキュリティ保護可能なリソースに対して現在のユーザーが持つ有効な権限を評価します。 関連する関数は [fn_my_permissions](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md) です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
HAS_PERMS_BY_NAME ( securable , securable_class , permission    
    [ , sub-securable ] [ , sub-securable_class ] )  
```  
  
## <a name="arguments"></a>引数  
 *securable*  
 セキュリティ保護可能なリソースの名前を指定します。 セキュリティ保護可能なリソースがサーバー自体の場合、この値は NULL に設定する必要があります。 *securable* には **sysname** 型のスカラー式を指定します。 既定値はありません。  
  
 *securable_class*  
 権限のテスト対象とするセキュリティ保護可能なリソースのクラスの名前を指定します。 *securable_class* には **nvarchar(60)** 型のスカラー式を指定します。  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、securable_class 引数を次のいずれかに設定する必要があります。**DATABASE**、**OBJECT**、**ROLE**、**SCHEMA**、または **USER**。  
  
 *permission*  
 チェックする権限名を表す、NULL 以外の **sysname** 型のスカラー式を指定します。 既定値はありません。 権限名 ANY はワイルドカードです。  
  
 *sub-securable*  
 権限をチェックするセキュリティ保護可能なサブエンティティの名前を表す、**sysname** 型のスカラー式を指定します (省略可能)。 既定値は NULL です。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以降のバージョンでは、sub-securables に **'[** _sub name_ **]'** の形式で角かっこを使用することはできません。 代わりに **'** _sub name_ **'** を使用してください。  
  
 *sub-securable_class*  
 権限をチェックするセキュリティ保護可能なサブエンティティのクラスを表す、**nvarchar(60)** 型のスカラー式を指定します (省略可能)。 既定値は NULL です。  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、sub-securable_class 引数は、securable_class 引数が **OBJECT** に設定されている場合にのみ有効です。 securable_class 引数が **OBJECT** に設定されている場合、sub-securable_class 引数は **COLUMN** に設定する必要があります。  
  
## <a name="return-types"></a>戻り値の型  
 **int**  
  
 クエリが失敗した場合は NULL が返されます。  
  
## <a name="remarks"></a>Remarks  
 この組み込み関数では、現在のプリンシパルが、指定したセキュリティ保護可能なリソースに対して、特定の有効な権限を保持しているかどうかが評価されます。 HAS_PERMS_BY_NAME は、セキュリティ保護可能なリソースに対する有効な権限がユーザーにある場合は 1 を返し、有効な権限がない場合は 0 を返します。また、セキュリティ保護可能なクラスまたは権限が無効である場合は NULL を返します。 有効な権限とは、次のような権限です。  
  
-   プリンシパルに直接許可されており、拒否されていない権限。  
  
-   プリンシパルが保持する上位レベルの権限に暗黙的に含まれており、拒否されていない権限。  
  
-   プリンシパルがメンバーとなっているロールまたはグループに許可されており、拒否されていない権限。  
  
-   プリンシパルがメンバーとなっているロールまたはグループが保持しており、拒否されていない権限。  
  
 権限の評価は、常に呼び出し元のセキュリティ コンテキストで実行されます。 他のユーザーに有効な権限があるかどうかを評価する場合、呼び出し元には、そのユーザーに対する IMPERSONATE 権限が必要です。  
  
 スキーマ レベルのエンティティの場合、1 部、2 部、または 3 部構成の、NULL でない名前を使用できます。 データベース レベルのエンティティの場合、1 部構成の名前を使用できます。NULL 値は "現在のデータベース" を示します。 リソースがサーバー自体の場合は、"現在のサーバー" を表す NULL 値を使用する必要があります。 この関数では、リンク サーバーに対する権限や、サーバー レベルのプリンシパルが作成されていない Windows ユーザーの権限をチェックできません。  
  
 次のクエリでは、セキュリティ保護可能な組み込みクラスの一覧が返されます。  
  
```  
SELECT class_desc FROM sys.fn_builtin_permissions(default);  
```  
  
 次の照合順序が使用されます。  
  
-   現在のデータベースの照合順序: データベース レベルのセキュリティ保護可能なリソース (スキーマに含まれていないセキュリティ保護可能なリソースを含む)。スキーマ スコープの 1 部または 2 部構成のセキュリティ保護可能なリソース。3 部構成の名前を使用する場合のターゲット データベース。  
  
-   マスター データベース照合順序: サーバー レベルのセキュリティ保護可能なリソース。  
  
-   列レベルのチェックの場合、"ANY" はサポートされません。 適切な権限を指定する必要があります。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-do-i-have-the-server-level-view-server-state-permission"></a>A. サーバー レベルの VIEW SERVER STATE 権限を保持しているかどうかをチェックする  
  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降
  
```  
SELECT HAS_PERMS_BY_NAME(null, null, 'VIEW SERVER STATE');  
```  
  
### <a name="b-am-i-able-to-impersonate-server-principal-ps"></a>B. サーバー プリンシパル Ps に対する IMPERSONATE 権限を保持しているかどうかをチェックする  
  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降
  
```  
SELECT HAS_PERMS_BY_NAME('Ps', 'LOGIN', 'IMPERSONATE');  
```  
  
### <a name="c-do-i-have-any-permissions-in-the-current-database"></a>C. 現在のデータベースに対して権限を保持しているかどうかをチェックする  
  
```  
SELECT HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'ANY');  
```  
  
### <a name="d-does-database-principal-pd-have-any-permission-in-the-current-database"></a>D. 現在のデータベースに、データベース プリンシパル Pd の権限があるかどうかをチェックする  
 呼び出し元は、プリンシパル `Pd` に対する IMPERSONATE 権限を保持していることを前提としています。  
  
```  
EXECUTE AS user = 'Pd'  
GO  
SELECT HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'ANY');  
GO  
REVERT;  
GO  
```  
  
### <a name="e-can-i-create-procedures-and-tables-in-schema-s"></a>E. スキーマ S 内にプロシージャとテーブルを作成できるかどうかをチェックする  
 次の例では、`ALTER` に `S` 権限、データベースに `CREATE PROCEDURE` 権限、およびテーブルに同様の権限が必要です。  
  
```  
SELECT HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'CREATE PROCEDURE')  
    & HAS_PERMS_BY_NAME('S', 'SCHEMA', 'ALTER') AS _can_create_procs,  
    HAS_PERMS_BY_NAME(db_name(), 'DATABASE', 'CREATE TABLE') &  
    HAS_PERMS_BY_NAME('S', 'SCHEMA', 'ALTER') AS _can_create_tables;  
```  
  
### <a name="f-which-tables-do-i-have-select-permission-on"></a>F. どのテーブルに対して、SELECT 権限を保持しているかをチェックする  
  
```  
SELECT HAS_PERMS_BY_NAME  
(QUOTENAME(SCHEMA_NAME(schema_id)) + '.' + QUOTENAME(name),   
    'OBJECT', 'SELECT') AS have_select, * FROM sys.tables  
```  
  
### <a name="g-do-i-have-insert-permission-on-the-salesperson-table-in-adventureworks2012"></a>G. AdventureWorks2012 の SalesPerson テーブルに対して、INSERT 権限を保持しているかどうかをチェックする  
 次の例では、`AdventureWorks2012` が自分の現在のデータベース コンテキストであると想定し、2 部構成の名前を使用します。  
  
```  
SELECT HAS_PERMS_BY_NAME('Sales.SalesPerson', 'OBJECT', 'INSERT');  
```  
  
 次の例では、現在のデータベース コンテキストに関する想定はなく、3 部構成の名前を使用します。  
  
```  
SELECT HAS_PERMS_BY_NAME('AdventureWorks2012.Sales.SalesPerson',   
    'OBJECT', 'INSERT');  
```  
  
### <a name="h-which-columns-of-table-t-do-i-have-select-permission-on"></a>H. テーブル T のどの列に対して、SELECT 権限を保持しているかをチェックする  
  
```  
SELECT name AS column_name,   
    HAS_PERMS_BY_NAME('T', 'OBJECT', 'SELECT', name, 'COLUMN')   
    AS can_select   
    FROM sys.columns AS c   
    WHERE c.object_id=object_id('T');  
```  
  
## <a name="see-also"></a>参照  
 [アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [権限の階層 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
  
  
