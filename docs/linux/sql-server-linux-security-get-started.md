---
title: Linux での SQL Server のセキュリティの概要
description: この記事では、一般的なセキュリティ アクションについて説明します。
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.openlocfilehash: 1e64ce76ef2528c96ecc0206b7a56b31d4c95ef7
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68019501"
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>SQL Server on Linux のセキュリティ機能のチュートリアル

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server を初めて使用する Linux ユーザーの場合は、以下のタスクでは一部のセキュリティ タスクの手順がわかります。 これらは Linux 独自または固有のものではありませんが、さらに調べる領域について考えるヒントになります。 各例には、その領域の詳細なドキュメントのリンクが記載されています。

> [!NOTE]
>  次の例では、**AdventureWorks2014** サンプル データベースを使用します。 このサンプル データベースを入手してインストールする手順については、[Windows から Linux への SQL Server データベースの復元](sql-server-linux-migrate-restore-database.md)に関する記事を参照してください。


## <a name="create-a-login-and-a-database-user"></a>ログインとデータベース ユーザーを作成する 

[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) ステートメントを使って master データベースにログインを作成することにより、他のユーザーに SQL Server へのアクセスを許可します。 例:

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

> [!NOTE]
>  前のコマンドのアスタリスクの代わりに、常に強力なパスワードを使用します。

ログインは、SQL Server に接続し、master データベースに (制限付きで) アクセスできます。 ユーザー データベースに接続するには、データベース レベルで対応するデータベース ユーザーと呼ばれる ID がログインに必要です。 ユーザーは各データベースに固有であり、アクセス権を付与するには、データベースごとに個別に作成する必要があります。 次の例では、AdventureWorks2014 データベースに移動し、[CREATE USER](../t-sql/statements/create-user-transact-sql.md) ステートメントを使って、ログイン名 Larry に関連付けられている Larry という名前のユーザーを作成します。 ログインとユーザーは関連して (相互にマップされて) いますが、それらは異なるオブジェクトです。 ログインは、サーバー レベルの原則です。 ユーザーは、データベース レベルのプリンシパルです。

```
USE AdventureWorks2014;
GO
CREATE USER Larry;
GO
```

- SQL Server の管理者アカウントでは、任意のデータベースに接続し、データベースにさらに多くのログインとユーザーを作成できます。  
- データベースを作成したユーザーはデータベース所有者になり、そのデータベースに接続できます。 データベース所有者は、さらにユーザーを作成できます。

その後、他のログインに `ALTER ANY LOGIN` アクセス許可を付与することで、より多くのログインを作成することを承認できます。 データベース内では、他のユーザーに `ALTER ANY USER` アクセス許可を付与することで、より多くのユーザーを作成することを承認できます。 例:   

```
GRANT ALTER ANY LOGIN TO Larry;   
GO   
   
USE AdventureWorks2014;   
GO   
GRANT ALTER ANY USER TO Jerry;    
GO   
```

これで、ログイン Larry はさらに多くのログインを作成でき、ユーザー Jerry はより多くのユーザーを作成できるようになります。


## <a name="granting-access-with-least-privileges"></a>最小限の特権でアクセス権を付与する

ユーザー データベースに最初に接続するユーザーは、管理者アカウントとデータベース所有者アカウントになります。 ただし、これらのユーザーは、データベースに対するすべてのアクセス許可を使用できます。 これは、ほとんどのユーザーが持つべきものより多いアクセス許可です。 

作業を始めるだけのときは、組み込みの "*固定データベース ロール*" を使って、いくつかの一般的なアクセス許可のカテゴリを割り当てることができます。 たとえば、`db_datareader` 固定データベース ロールでは、データベース内のすべてのテーブルを読み取ることができますが、変更することはできません。 固定データベース ロールのメンバーシップを許可するには、[ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md) ステートメントを使います。 次の例では、ユーザー `Jerry` を `db_datareader` 固定データベース ロールに追加します。   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

固定データベース ロールの一覧については、「[データベース レベルのロール](../relational-databases/security/authentication-access/database-level-roles.md)」をご覧ください。

後で、データへのより正確なアクセス (強くお勧めします) を構成する準備ができたら、[CREATE ROLE](../t-sql/statements/create-role-transact-sql.md) ステートメントを使って、独自のユーザー定義のデータベース ロールを作成します。 次に、カスタム ロールに特定の詳細なアクセス許可を割り当てます。

たとえば、次のステートメントでは、`Sales` という名前のデータベース ロールが作成され、`Sales` グループに対して `Orders` テーブルの行を表示、更新、削除する権限が与えられてから、ユーザー `Jerry` が `Sales` ロールに追加されます。   
   
```   
CREATE ROLE Sales;   
GRANT SELECT ON Object::Sales TO Orders;   
GRANT UPDATE ON Object::Sales TO Orders;   
GRANT DELETE ON Object::Sales TO Orders;   
ALTER ROLE Sales ADD MEMBER Jerry;   
```   

For more information about the permission system, see [Getting Started with Database Engine Permissions](../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).


## Configure row-level security  

[Row-Level Security](../relational-databases/security/row-level-security.md) enables you to restrict access to rows in a database based on the user executing a query. This feature is useful for scenarios like ensuring that customers can only access their own data or that workers can only access data that is pertinent to their department.   

The following steps walk through setting up two Users with different row-level access to the `Sales.SalesOrderHeader` table. 

Create two user accounts to test the row level security:    
   
```   
USE AdventureWorks2014;   
GO   
   
CREATE USER Manager WITHOUT LOGIN;     
   
CREATE USER SalesPerson280 WITHOUT LOGIN;    
```   

Grant read access on the `Sales.SalesOrderHeader` table to both users:    
   
```   
GRANT SELECT ON Sales.SalesOrderHeader TO Manager;      
GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;    
```   
   
Create a new schema and inline table-valued function. The function returns 1 when a row in the `SalesPersonID` column matches the ID of a `SalesPerson` login or if the user executing the query is the Manager user.   
   
```     
CREATE SCHEMA Security;   
GO   
   
CREATE FUNCTION Security.fn_securitypredicate(@SalesPersonID AS int)     
    RETURNS TABLE   
WITH SCHEMABINDING   
AS     
   RETURN SELECT 1 AS fn_securitypredicate_result    
WHERE ('SalesPerson' + CAST(@SalesPersonId as VARCHAR(16)) = USER_NAME())     
    OR (USER_NAME() = 'Manager');    
```   

Create a security policy adding the function as both a filter and a block predicate on the table:  

```
CREATE SECURITY POLICY SalesFilter   
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader,   
ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader   
WITH (STATE = ON);   
```

Execute the following to query the `SalesOrderHeader` table as each user. Verify that `SalesPerson280` only sees the 95 rows from their own sales and that the `Manager` can see all the rows in the table.  

```    
EXECUTE AS USER = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
REVERT; 
 
EXECUTE AS USER = 'Manager';   
SELECT * FROM Sales.SalesOrderHeader;   
REVERT;   
```
 
Alter the security policy to disable the policy.  Now both users can access all rows. 

```
ALTER SECURITY POLICY SalesFilter   
WITH (STATE = OFF);    
``` 


## Enable dynamic data masking

[Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md) enables you to limit the exposure of sensitive data to users of an application by fully or partially masking certain columns. 

Use an `ALTER TABLE` statement to add a masking function to the `EmailAddress` column in the `Person.EmailAddress` table: 
 
```
USE AdventureWorks2014; GO ALTER TABLE Person.EmailAddress     ALTER COLUMN EmailAddress    
ADD MASKED WITH (FUNCTION = 'email()');
``` 
 
Create a new user `TestUser` with `SELECT` permission on the table, then execute a query as `TestUser` to view the masked data:   

```  
CREATE USER TestUser WITHOUT LOGIN;   
GRANT SELECT ON Person.EmailAddress TO TestUser;    
 
EXECUTE AS USER = 'TestUser';   
SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;       
REVERT;    
```
 
Verify that the masking function changes the email address in the first record from:
  
|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |ken0@adventure-works.com |    
 
into 

|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |kXXX@XXXX.com |   


## Enable Transparent Data Encryption

One threat to your database is the risk that someone will steal the database files off of your hard-drive. This could happen with an intrusion that gets elevated access to your system, through the actions of a problem employee, or by theft of the computer containing the files (such as a laptop).

Transparent Data Encryption (TDE) encrypts the data files as they are stored on the hard drive. The master database of the SQL Server database engine has the encryption key, so that the database engine can manipulate the data. The database files cannot be read without access to the key. High-level administrators can manage, backup, and recreate the key, so the database can be moved, but only by selected people. When TDE is configured, the `tempdb` database is also automatically encrypted. 

Since the Database Engine can read the data, Transparent Data Encryption does not protect against unauthorized access by administrators of the computer who can directly read memory, or access SQL Server through an administrator account.

### Configure TDE

- Create a master key
- Create or obtain a certificate protected by the master key
- Create a database encryption key and protect it by the certificate
- Set the database to use encryption

Configuring TDE requires `CONTROL` permission on the master database and `CONTROL` permission on the user database. Typically an administrator configures TDE. 

The following example illustrates encrypting and decrypting the `AdventureWorks2014` database using a certificate installed on the server named `MyServerCert`.


```
USE master;  
GO  

CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**********';  
GO  

CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My Database Encryption Key Certificate';  
GO  

USE AdventureWorks2014;   GO
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO
  
ALTER DATABASE AdventureWorks2014  
SET ENCRYPTION ON;   
```

To remove TDE, execute `ALTER DATABASE AdventureWorks2014 SET ENCRYPTION OFF;`   

The encryption and decryption operations are scheduled on background threads by SQL Server. You can view the status of these operations using the catalog views and dynamic management views in the list that appears later in this topic.   

> [!WARNING]
>  Backup files of databases that have TDE enabled are also encrypted by using the database encryption key. As a result, when you restore these backups, the certificate protecting the database encryption key must be available. This means that in addition to backing up the database, you have to make sure that you maintain backups of the server certificates to prevent data loss. Data loss will result if the certificate is no longer available. For more information, see [SQL Server Certificates and Asymmetric Keys](../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  

For more information about TDE, see [Transparent Data Encryption (TDE)](../relational-databases/security/encryption/transparent-data-encryption-tde.md).   


## Configure backup encryption
SQL Server has the ability to encrypt the data while creating a backup. By specifying the encryption algorithm and the encryptor (a certificate or asymmetric key) when creating a backup, you can create an encrypted backup file.    
  
> [!WARNING]  
>  It is very important to back up the certificate or asymmetric key, and preferably to a different location than the backup file it was used to encrypt. Without the certificate or asymmetric key, you cannot restore the backup, rendering the backup file unusable. 
 
 
The following example creates a certificate, and then creates a backup protected by the certificate.
```
USE master;   GO   CREATE CERTIFICATE BackupEncryptCert   WITH SUBJECT = 'Database backups';   GO BACKUP DATABASE [AdventureWorks2014]   TO DISK = N'/var/opt/mssql/backups/AdventureWorks2014.bak'  
WITH  
  COMPRESSION,  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   SERVER CERTIFICATE = BackupEncryptCert  
   ),  
  STATS = 10  
GO  
```

For more information, see [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md).


## Next steps

For more information about the security features of SQL Server, see [Security Center for SQL Server Database Engine and Azure SQL Database](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).
