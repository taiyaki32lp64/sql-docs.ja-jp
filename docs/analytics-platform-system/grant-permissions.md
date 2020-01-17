---
title: Grant T-sql 権限
description: 並列データウェアハウスのデータベース操作に T-sql 権限を付与します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bbe78979c393490a52e1051fe158ae138f93dcc
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401150"
---
# <a name="grant-t-sql-permissions-for-parallel-data-warehouse"></a>Parallel Data Warehouse の T-sql 権限を許可する
並列データウェアハウスのデータベース操作に T-sql 権限を付与します。

## <a name="grant-permissions-to-submit-database-queries"></a>データベースクエリを送信するためのアクセス許可を付与する
このセクションでは、データベースロールとユーザーにアクセス許可を付与して SQL Server PDW アプライアンス上のデータを照会する方法について説明します。  
  
データのクエリを実行する権限を許可するために使用されるステートメントは、必要なアクセスの範囲によって異なります。 次の SQL ステートメントでは、アプライアンスにアクセスできる KimAbercrombie という名前のログインを作成し、 **AdventureWorksPDW2012**データベースに KimAbercrombie という名前のデータベースユーザーを作成し、PDWQueryData という名前のデータベースロールを作成して、そのアクセス許可をオブジェクトまたはデータベースレベルのどちらに付与するかに基づいて、クエリアクセス権を付与するオプションを表示します。  
  
```sql  
USE master;  
GO  
  
CREATE LOGIN KimAbercrombie WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
USE AdventureWorksPDW2012;  
GO  
  
CREATE USER KimAbercrombie;  
GO  
  
CREATE ROLE PDWQueryData;  
GO  
  
EXEC sp_addrolemember 'PDWQueryData', 'KimAbercrombie'  
GO  
  
-- If the permission is granted against a table or view only, use this syntax:  
GRANT SELECT ON OBJECT::AdventureWorksPDW2012..DimEmployee TO PDWQueryData;  
GO  
  
-- If the permission is granted for the database, use this syntax:  
GRANT SELECT ON DATABASE::AdventureWorksPDW2012 TO PDWQueryData;  
GO  
  
-- If KimAbercrombie is the only user that needs to access a table, use this syntax:  
GRANT SELECT ON OBJECT::AdventureWorksPDW2012..DimEmployee TO KimAbercrombie;  
GO  
```  
  
## <a name="grant-permissions-to-use-the-admin-console"></a>管理コンソールを使用するためのアクセス許可を付与する
このセクションでは、ログインに管理コンソールを使用するためのアクセス許可を付与する方法について説明します。  
  
**管理コンソールを使用する**  
  
管理コンソールを使用するには、ログインにサーバーレベルの**VIEW SERVER STATE**権限が必要です。 次の SQL ステートメントでは、Kim が管理コンソールを使用`KimAbercrombie`して SQL Server PDW アプライアンスを監視できるように、 **VIEW SERVER STATE**権限をログインに付与します。  
  
```sql  
USE master;  
GO  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
GO  
```  
  
**セッションの強制終了**  
  
セッションを強制終了する権限をログインに付与するには、 **ALTER ANY CONNECTION**権限を次のように与えます。  
  
```sql  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
## <a name="grant-permissions-to-load-data"></a>データを読み込むためのアクセス許可を付与する
このセクションでは、SQL Server PDWappliance にデータを読み込むための権限をデータベースロールとデータベースユーザーに付与する方法について説明します。  
  
次のスクリプトは、各読み込みオプションに必要なアクセス許可を示しています。 これは、特定のニーズに合わせて変更できます。  
  
```sql  
-- Create server login for the examples that follow.  
USE master;  
CREATE LOGIN BI_ETLUser WITH PASSWORD = '******';  
  
--Grant BULK Load permissions   
GRANT ADMINISTER BULK OPERATIONS TO BI_ETLUser;  
  
--Grant Staging database permissions  
USE stagedb;  
CREATE USER BI_ETLUser for login BI_ETLUser;  
EXEC sp_addrolemember 'db_datareader','BI_ETLUser';  
EXEC sp_addrolemember 'db_datawriter','BI_ETLUser';  
EXEC sp_addrolemember 'db_ddladmin','BI_ETLUser';  
  
-- The CREATE TABLE permission is required for the database hosting the temporary table.  
-- This may be the staging database (if specified) or destination database.   
-- The CREATE permission is not required if loading in fastappend mode.  
GRANT CREATE TABLE ON database::stagedb TO BI_ETLUser;  
  
-- If loading in append or fastappend mode, the INSERT permission is required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
  
-- If loading in reload mode, the INSERT and DELETE permissions are required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
GRANT DELETE ON database::stagedb TO BI_ETLUser;  
  
-- If loading in upsert mode, the INSERT and UPDATE permissions are required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
GRANT UPDATE ON database::stagedb TO BI_ETLUser;  
  
-- Destination DB  
USE tpch_1gb;  
CREATE USER BI_ETLUser FOR LOGIN BI_ETLUser;  
EXEC sp_addrolemember 'db_datareader','BI_ETLUser';  
EXEC sp_addrolemember 'db_datawriter','BI_ETLUser';  
```  
  
## <a name="grant-permissions-to-copy-data-off-the-appliance"></a>アプライアンスからデータコピーするためのアクセス許可を付与する
このセクションでは、SQL Server PDW アプライアンスからデータをコピーするためのアクセス許可をユーザーまたはデータベースロールに付与する方法について説明します。  
  
データを別の場所に移動するには、移動するデータが含まれているテーブルに対する**SELECT**権限が必要です。  
  
データの変換先が別の SQL Server PDW である場合、ユーザーは、そのテーブルを格納するスキーマに対する**CREATE TABLE**の権限と、そのテーブルを含むスキーマに対する**ALTER schema**権限を持っている必要があります。  
  
## <a name="grant-permissions-to-manage-databases"></a>データベースを管理する権限を付与する
このセクションでは、SQL Server PDW アプライアンス上のデータベースを管理する権限をデータベースユーザーに付与する方法について説明します。  
  
場合によっては、会社がデータベースのマネージャーを割り当てます。 マネージャーは、他のログインがデータベースに対して持つアクセス権、およびデータベース内のデータとオブジェクトを制御します。 データベース内のすべてのオブジェクト、ロール、およびユーザーを管理するには、データベースに対する**CONTROL**権限をユーザーに付与します。 次のステートメントは、 **AdventureWorksPDW2012**データベースに対する`KimAbercrombie` **CONTROL**権限をユーザーに許可します。  
  
```sql
USE AdventureWorksPDW2012;  
GO  
GRANT CONTROL ON DATABASE:: AdventureWorksPDW2012 TO KimAbercrombie;  
```  
  
アプライアンス上のすべてのデータベースを制御するアクセス許可を他のユーザーに付与するには、 **ALTER ANY database**権限を master データベースに付与します。  
  
## <a name="grant-permissions-to-manage-logins-users-and-database-roles"></a>ログイン、ユーザー、およびデータベースロールを管理するためのアクセス許可を付与する
ここでは、ログイン、データベースユーザー、およびデータベースロールを管理する権限を付与する方法について説明します。  
  
### <a name="PermsAdminConsole"></a>ログインを管理するためのアクセス許可を付与する  
**ログインの追加または管理**  
  
次の SQL ステートメントは、 [CREATE login](../t-sql/statements/create-login-transact-sql.md)ステートメントを使用して新しいログインを作成したり、 [alter login](../t-sql/statements/alter-login-transact-sql.md)ステートメントを使用して既存のログインを変更したりできる、KimAbercrombie という名前のログインを作成します。  
  
**ALTER ANY LOGIN**権限では、新しいログインを作成したり、既存のログインを削除したりすることができます。 ログインが存在する場合、 **ALTER ANY login**権限を持つログイン、またはそのログインに対する**alter**権限を持つログインで、ログインを管理できます。 ログインを使用すると、ログインのパスワードおよび既定のデータベースを変更できます。  
  
```sql 
CREATE LOGIN KimAbercrombie   
WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
GRANT ALTER ANY LOGIN TO KimAbercrombie;  
```  
  
### <a name="grant-permissions-to-manage-login-sessions"></a>ログインセッションを管理するためのアクセス許可を付与する  
サーバー上のすべてのセッションを表示できるようにするには、 **VIEW SERVER STATE**権限が必要です。 他のログインのセッションを終了する機能を利用するには、 **ALTER ANY CONNECTION**権限が必要です。 次の例では`KimAbercrombie` 、前に作成したログインを使用します。  
  
```sql  
-- Grant permissions to view sessions and queries  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
  
-- Grant permission to end sessions  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
### <a name="grant-permission-to-manage-database-users"></a>データベースユーザーを管理する権限を付与する  
データベースユーザーを作成および削除するには、 **ALTER ANY USER**権限が必要です。 既存のユーザーを管理するには、 **ALTER ANY user**権限、またはそのユーザーに対する**alter**権限が必要です。 次の例では`KimAbercrombie` 、前に作成したログインを使用します。  
  
```sql  
-- Create a user  
USE AdventureWorksPDW2012;  
GO  
CREATE USER KimAbercrombie;  
  
-- Grant permissions to create and drop users   
GRANT ALTER ANY USER TO KimAbercrombie;  
```  
  
### <a name="grant-permisson-to-manage-database-roles"></a>アクセスを許可してデータベースロールを管理する  
ユーザー定義のデータベースロールを作成および削除するには、 **ALTER ANY ROLE**権限が必要です。 次の例では`KimAbercrombie` 、前に作成したログインと使用を使用します。  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
-- Grant permissions to create and drop roles  
GRANT ALTER ANY ROLE TO KimAbercrombie;  
```  
  
### <a name="login-user-and-role-permission-charts"></a>ログイン、ユーザー、およびロール権限のグラフ  
次のグラフでは混乱が生じる可能性がありますが、より高度なレベルのアクセス許可 (コントロールなど) に、個別に付与できるより詳細なアクセス許可 (ALTER など) が含まれていることがわかります。 ベストプラクティスとしては、必要なタスクを完了するための最小限のアクセス許可を常に付与することをお勧めします。 これを行うには、最上位レベルのアクセス許可ではなく、より具体的なアクセス許可を付与します。  
  
**ログイン権限:**  
  
![APS セキュリティのログイン権限](./media/grant-permissions/APS_security_login_perms.png "APS_security_login_perms")  
  
**ユーザーのアクセス許可:**  
  
![APS セキュリティのユーザー権限](./media/grant-permissions/APS_security_user_perms.png "APS_security_user_perms")  
  
**ロールのアクセス許可:**  
  
![APS セキュリティのロール権限](./media/grant-permissions/APS_security_role_perms.png "APS_security_role_perms")  
  
<!-- MISSING LINKS
For a list of all permissions, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  
  
-->

## <a name="grant-permissions-to-monitor-the-appliance"></a>アプライアンスを監視するアクセス許可を付与する
SQL Server PDW アプライアンスは、管理コンソールまたは SQL Server PDW システムビューのいずれかを使用して監視できます。 ログインには、アプライアンスを監視するためのサーバーレベルの**VIEW SERVER STATE**権限が必要です。 ログインでは、管理コンソールまたは**KILL**コマンドを使用して接続を終了するために、 **ALTER ANY CONNECTION**アクセス許可が必要です。 管理コンソールの使用に必要なアクセス許可の詳細については、「[管理コンソールを使用するためのアクセス許可を付与する &#40;SQL Server PDW&#41;](#grant-permissions-to-use-the-admin-console)」を参照してください。  
  
### <a name="PermsAdminConsole"></a>システムビューを使用してアプライアンスを監視するアクセス許可を付与する  
次の SQL ステートメントでは、と`monitor_login`いう名前のログインを作成し、その`monitor_login`ログインに**VIEW SERVER STATE**権限を与えます。  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_login WITH PASSWORD='Password4321';  
GRANT VIEW SERVER STATE TO monitor_login;  
GO  
```  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views-and-to-terminate-connections"></a>システムビューを使用してアプライアンスを監視し、接続を終了するアクセス許可を付与します。  
次の SQL ステートメントは、という`monitor_and_terminate_login`名前のログインを作成し、 **VIEW SERVER STATE**と**ALTER ANY CONNECTION**権限を`monitor_and_terminate_login`ログインに付与します。  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_and_terminate_login WITH PASSWORD='Password1234';   
GRANT VIEW SERVER STATE TO monitor_and_terminate_login;   
GRANT ALTER ANY CONNECTION TO monitor_and_terminate_login;  
GO  
```  
  
管理者ログインを作成するには、「[固定サーバーロール](pdw-permissions.md#fixed-server-roles)」を参照してください。  
  
## <a name="see-also"></a>参照
[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)  
[ユーザーの作成](../t-sql/statements/create-user-transact-sql.md)  
[ロールの作成](../t-sql/statements/create-role-transact-sql.md)  
[給紙](load-overview.md)  
