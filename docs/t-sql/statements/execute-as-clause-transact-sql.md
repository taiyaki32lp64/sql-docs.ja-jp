---
title: EXECUTE AS 句 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AS
- AS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- permission sets [SQL Server]
- queues [SQL Server]
- stored procedures [SQL Server], executing
- user-defined functions [SQL Server], execution context
- EXECUTE AS
- triggers [SQL Server], execution context
- execution context [SQL Server]
- switching execution context
- functions [SQL Server], execution context
ms.assetid: bd517aa3-f06e-4356-87d8-70de5df4494a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2dfba9eef86ab77ec114bc74712d9573fb5e4c48
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155059"
---
# <a name="execute-as-clause-transact-sql"></a>EXECUTE AS 句 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、関数 (インライン テーブル値関数を除く)、プロシージャ、キュー、トリガーなどのユーザー定義モジュールの実行コンテキストを定義できます。  
  
 モジュールが実行されるコンテキストを指定することにより、[!INCLUDE[ssDE](../../includes/ssde-md.md)]がどのユーザー アカウントを使用して、モジュールによって参照されるオブジェクトの権限を検証するかを制御できます。 これにより、ユーザー定義モジュールとそれらのモジュールによって参照されるオブジェクト間に存在する、オブジェクトのチェーン全体に関する権限の管理を、さらに柔軟に制御できます。 ユーザーに付与する必要のある権限は、モジュール自体に対するもののみで、参照されるオブジェクトに対する明示的な権限の許可は必要ありません。 モジュールによってアクセスされるオブジェクトに対する権限が必要なのは、そのモジュールを実行しているユーザーのみです。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- SQL Server Syntax  
Functions (except inline table-valued functions), Stored Procedures, and DML Triggers  
{ EXEC | EXECUTE } AS { CALLER | SELF | OWNER | 'user_name' }   
  
DDL Triggers with Database Scope  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'user_name' }   
  
DDL Triggers with Server Scope and logon triggers  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'login_name' }   
  
Queues  
{ EXEC | EXECUTE } AS { SELF | OWNER | 'user_name' }   
```  
  
```  
  
-- Azure SQL Database Syntax  
Functions (except inline table-valued functions), Stored Procedures, and DML Triggers  
  
{ EXEC | EXECUTE } AS { CALLER | SELF | OWNER | 'user_name' }   
  
DDL Triggers with Database Scope  
  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'user_name' }  
  
```  
  
## <a name="arguments"></a>引数  
 **CALLER**  
 モジュール内のステートメントを、モジュールの呼び出し元のコンテキストで実行します。 モジュールを実行するユーザーは、モジュール自体に対してだけでなく、そのモジュールによって参照されるすべてのデータベース オブジェクトに対する、適切な権限を持っている必要があります。  
  
 CALLER はキュー以外のすべてのモジュールに対して、既定値となっています。またその動作は、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] の場合と同じです。  
  
 CALLER は、CREATE QUEUE または ALTER QUEUE ステートメントでは指定できません。  
  
 **SELF**  
 EXECUTE AS SELF は、EXECUTE AS *user_name* と同等で、異なるのは指定されるユーザーがモジュールを作成または変更したユーザーであるという点です。 モジュールを作成または変更するユーザーの実際のユーザー ID は、**sys.sql_modules** または **sys.service_queues** カタログ ビューの **execute_as_principal_id** 列に格納されます。  
  
 SELF は、キューの場合の既定値です。  
  
> [!NOTE]  
>  **sys.service_queues** カタログ ビューの **execute_as_principal_id** 列のユーザー ID を変更するには、ALTER QUEUE ステートメントで EXECUTE AS 設定を明示的に指定する必要があります。  
  
 OWNER  
 モジュール内のステートメントがモジュールの現在の所有者のコンテキストで実行されるように指定します。 モジュールの所有者が指定されていない場合、そのモジュールのスキーマの所有者が使用されます。 OWNER は、DDL トリガーまたはログオン トリガーに対しては指定できません。  
  
> [!IMPORTANT]  
>  OWNER は、単一アカウントにマップする必要があります。ロールまたはグループにはマップできません。  
  
 **'** *user_name* **'**  
 モジュール内のステートメントを、*user_name* で指定されたユーザーのコンテキスト内で実行します。 モジュール内のすべてのオブジェクトの権限は *user_name* に対して検証されます。 *user_name* は、サーバー スコープの DDL トリガーまたはログオン トリガーには指定できません。 代わりに *login_name* を使います。  
  
 *user_name* は、現在のデータベース内に存在し、単一アカウントである必要があります。 *user_name* には、グループ、ロール、証明書、キー、および、NT AUTHORITY\LocalService、NT AUTHORITY\NetworkService、NT AUTHORITY\LocalSystem などのビルトイン アカウントを指定できません。  
  
 実行コンテキストのユーザー ID はメタデータ内に格納され、**sys.sql_modules** または **sys.assembly_modules** カタログ ビューの **execute_as_principal_id** 列で参照できます。  
  
 **'** *login_name* **'**  
 モジュール内部のステートメントを、*login_name* で指定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインのコンテキストで実行します。 モジュール内のすべてのオブジェクトの権限は *login_name* に対して検証されます。 *login_name* は、サーバー スコープの DDL トリガーまたはログオン トリガーのみに指定できます。  
  
 *login_name* には、グループ、ロール、証明書、キー、および、NT AUTHORITY\LocalService、NT AUTHORITY\NetworkService、NT AUTHORITY\LocalSystem などのビルトイン アカウントを指定できません。  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]による、モジュール内で参照されるオブジェクトに対する権限の評価方法は、呼び出し元のオブジェクトと参照されるオブジェクト間に存在する所有権の継承によって異なります。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、呼び出し元のユーザーに対して、参照されるすべてのオブジェクトへのアクセスを許可するためには、所有権の継承を使用する方法しかありませんでした。  
  
 所有権の継承には、次のような制限があります。  
  
-   次の DML ステートメントにのみ適用されます:SELECT、INSERT、UPDATE、DELETE。  
  
-   呼び出し元のオブジェクトと呼び出されたオブジェクトの所有者は同一である必要があります。  
  
-   モジュール内部の動的クエリには適用されません。  
  
 モジュール内で指定される実行コンテキストに関係なく、次の操作が常に適用されます。  
  
-   モジュールが実行されると、[!INCLUDE[ssDE](../../includes/ssde-md.md)]は、モジュールを実行するユーザーにそのモジュールに対する EXECUTE 権限が与えられていることを最初に確認します。  
  
-   所有権の継承ルールは、引き続き適用されます。 つまり、呼び出し元のオブジェクトと呼び出されたオブジェクトの所有者が同一の場合、基になるオブジェクトに対する権限は確認されません。  
  
 ユーザーが、CALLER 以外のコンテキスト内で実行するように指定されたモジュールを実行すると、そのユーザーに対してモジュールの実行権限が確認されますが、さらに、そのモジュールによってアクセスされるオブジェクトの追加の権限確認が、EXECUTE AS 句で指定されたユーザー アカウントに対して行われます。 実質的に、モジュールを実行するユーザーは、指定されたユーザーの権限を借用します。  
  
 モジュールの EXECUTE AS 句で指定されたコンテキストは、モジュールの実行中のみ有効です。 モジュールの実行が完了すると、コンテキストは呼び出し元に戻されます。  
  
## <a name="specifying-a-user-or-login-name"></a>ユーザーまたはログイン名の指定  
 モジュールの EXECUTE AS 句で指定されたデータベース ユーザーまたはサーバー ログインは、モジュールが変更されて別のコンテキストで実行されるまでは削除できません。  
  
 EXECUTE AS 句で指定されたユーザーまたはログイン名は、それぞれ **sys.database_principals** または **sys.server_principals** 内にプリンシパルとして存在する必要があります。存在しない場合、モジュールの作成または変更処理は失敗します。 また、モジュールを作成または変更するユーザーには、そのプリンシパルに対する IMPERSONATE 権限が必要です。  
  
 ユーザーが、Windows グループのメンバーシップを使って [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータベースまたはインスタンスに暗黙的にアクセスした場合、モジュールが作成されるときに次のいずれかの要件を満たしていれば、EXECUTE AS 句で指定されたユーザーが暗黙的に作成されます。  
  
-   指定されたユーザーまたはログインが、固定サーバー ロール **sysadmin** のメンバーであること。  
  
-   モジュールを作成するユーザーに、プリンシパルを作成する権限が与えられていること。  
  
 これらの要件がどちらも満たされない場合、モジュールの作成操作は失敗します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) サービスがローカル アカウント (ローカル サービスまたはローカル ユーザー アカウント) で実行されている場合、このサービスには、EXECUTE AS 句で指定されている Windows ドメイン アカウントのグループのメンバーシップを取得する権限は与えられません。 このため、モジュールの実行は失敗します。  
  
 たとえば、次のような条件を想定します。  
  
-   **CompanyDomain\SQLUsers** グループに **Sales** データベースへのアクセス権がある。  
  
-   **CompanyDomain\SqlUser1** は **SQLUsers** のメンバーであり、したがって **Sales** データベースへのアクセスが許可されている。  
  
-   モジュールを作成または変更するユーザーに、プリンシパルを作成する権限が与えられている。  
  
 次の `CREATE PROCEDURE` ステートメントが実行されると、`CompanyDomain\SqlUser1` が、`Sales` データベースのデータベース プリンシパルとして暗黙的に作成されます。  
  
```  
USE Sales;  
GO  
CREATE PROCEDURE dbo.usp_Demo  
WITH EXECUTE AS 'CompanyDomain\SqlUser1'  
AS  
SELECT user_name();  
GO  
```  
  
## <a name="using-execute-as-caller-stand-alone-statement"></a>スタンドアロンの EXECUTE AS CALLER ステートメントの使用  
 スタンドアロンの EXECUTE AS CALLER ステートメントをモジュール内で使用すると、実行コンテキストがそのモジュールの呼び出し元に設定されます。  
  
 次のストアド プロシージャが `SqlUser2` によって呼び出されるとします。  
  
```  
CREATE PROCEDURE dbo.usp_Demo  
WITH EXECUTE AS 'SqlUser1'  
AS  
SELECT user_name(); -- Shows execution context is set to SqlUser1.  
EXECUTE AS CALLER;  
SELECT user_name(); -- Shows execution context is set to SqlUser2, the caller of the module.  
REVERT;  
SELECT user_name(); -- Shows execution context is set to SqlUser1.  
GO  
```  
  
## <a name="using-execute-as-to-define-custom-permission-sets"></a>EXECUTE AS を使用したカスタム権限セットの定義  
 モジュールの実行コンテキストを指定すると、カスタム権限セットを定義する場合に非常に便利です。 たとえば、TRUNCATE TABLE などの操作には、許可できる権限がありません。 モジュール内に TRUNCATE TABLE ステートメントを組み込み、テーブルの変更権限を持つユーザーがモジュールを実行するように指定すると、モジュールの EXECUTE 権限を許可するユーザーに、テーブルを切り捨てる権限を拡張して与えることができます。  
  
 実行コンテキストを指定したモジュールの定義を表示するには、[sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) カタログ ビューを使用します。  
  
## <a name="best-practice"></a>推奨事項  
 モジュール内で定義された操作を実行する場合に必要となる最低限の権限を持つログインまたはユーザーを指定します。 たとえば、データベース レベルの権限が必要とされない場合は、データベース所有者アカウントは指定しないでください。  
  
## <a name="permissions"></a>アクセス許可  
 EXECUTE AS で指定されたモジュールを実行するには、呼び出し元に、そのモジュールに対する EXECUTE 権限が必要です。  
  
 別のデータベースまたはサーバー内のリソースにアクセスする CLR モジュールを、EXECUTE AS で指定して実行する場合、対象のデータベースまたはサーバーは、モジュールが生成されたデータベース (基になるデータベース) の認証情報を信頼する必要があります。  
  
 モジュールを作成または変更するときに EXECUTE AS 句を指定するには、指定されたプリンシパルに対する IMPERSONATE 権限とそのモジュールを作成する権限が必要です。 ユーザー自身の権限は、常に借用できます。 実行コンテキストを指定しない場合、または EXECUTE AS CALLER を指定する場合、IMPERSONATE 権限は必要ありません。  
  
 Windows グループのメンバーシップを使ってデータベースに暗黙的にアクセスできる *login_name* または *user_name* を指定するには、そのデータベースに対する CONTROL 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例は、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースにストアド プロシージャを作成し、実行コンテキストを `OWNER` に割り当てます。  
  
```  
CREATE PROCEDURE HumanResources.uspEmployeesInDepartment   
@DeptValue int  
WITH EXECUTE AS OWNER  
AS  
    SET NOCOUNT ON;  
    SELECT e.BusinessEntityID, c.LastName, c.FirstName, e.JobTitle  
    FROM Person.Person AS c   
    INNER JOIN HumanResources.Employee AS e  
        ON c.BusinessEntityID = e.BusinessEntityID  
    INNER JOIN HumanResources.EmployeeDepartmentHistory AS edh  
        ON e.BusinessEntityID = edh.BusinessEntityID  
    WHERE edh.DepartmentID = @DeptValue  
    ORDER BY c.LastName, c.FirstName;  
GO  
  
-- Execute the stored procedure by specifying department 5.  
EXECUTE HumanResources.uspEmployeesInDepartment 5;  
GO  
  
```  
  
## <a name="see-also"></a>参照  
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.service_queues &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-service-queues-transact-sql.md)   
 [REVERT &#40;Transact-SQL&#41;](../../t-sql/statements/revert-transact-sql.md)   
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  
