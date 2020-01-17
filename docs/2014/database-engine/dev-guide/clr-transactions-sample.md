---
title: CLR トランザクションのサンプル |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: b09161af-6ac1-406c-9d62-e40be3b4cf8d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 00a5db60a0bccdd3deec1d1ac845e926b6af5fb9
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637754"
---
# <a name="clr-transactions-sample"></a>CLR Transactions サンプル
  このサンプルでは、`System.Transactions` 名前空間にあるマネージド API を使用してトランザクションを制御する例を示します。 このサンプルで `System.Transactions.TransactionScope` クラスは、要求に応じるのに十分な在庫が存在する場合を除き、ある場所から別の場所への移動をアトミック レベルで行える程度の在庫が存在する場合に、在庫数が調整されないように、トランザクション境界を確立するために使用されています。 分散トランザクションにおける自動登録の例を、別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに格納された監査データベースに在庫の変更を記録するという動作で示しています。  
  
## <a name="prerequisites"></a>前提条件  
 このプロジェクトを作成して実行するには、次のソフトウェアがインストールされている必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express ドキュメントとサンプルの [Web サイト](https://www.microsoft.com/sql-server/sql-server-editions-express)から無償で入手できます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] デベロッパー [Web サイト](https://go.microsoft.com/fwlink/?linkid=62796)から入手できる AdventureWorks データベース。  
  
-   .NET Framework SDK 2.0 以降または Microsoft Visual Studio 2005 以降。 .NET Framework SDK は無償で入手できます。  
  
-   また、次の条件を満たしている必要があります。  
  
-   使用している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで CLR 統合が有効になっている必要があります。  
  
-   CLR 統合を有効にするには、次の手順に従います。  
  
    #### <a name="enabling-clr-integration"></a>CLR 統合の有効化  
  
    -   以下の [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドを実行します。  
  
     `sp_configure 'clr enabled', 1`  
  
     `GO`  
  
     `RECONFIGURE`  
  
     `GO`  
  
    > [!NOTE]  
    >  CLR を有効にするには、`ALTER SETTINGS` サーバーレベルの権限を持っている必要があります。この権限は、固定サーバーロール `sysadmin` と `serveradmin` のメンバーによって暗黙的に保持されます。  
  
-   使用している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに AdventureWorks データベースがインストールされている必要があります。  
  
-   使用している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの管理者でない場合、インストールを完了するには、 **Createassembly**アクセス許可を管理者に付与する必要があります。  
  
## <a name="building-the-sample"></a>サンプルのビルド  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a>次の手順に従ってサンプルを作成し、実行します。  
  
1.  Visual Studio または .NET Framework のコマンド プロンプトを開きます。  
  
2.  必要な場合は、サンプル用のディレクトリを作成します。 この例では C:\MySample を使用します。  
  
3.  この例では署名付きアセンブリが必要であるため、次のコマンドを入力して非対称キーを作成します。  
  
     `sn -k SampleKey.snk`  
  
4.  選択した言語に応じて次のいずれかをコマンド プロンプトで実行し、サンプル コードをコンパイルします。  
  
    -   `Vbc /reference:"C:\Program Files (x86)\Reference Assemblies\Microsoft\Framework\v3.5\System.Core.dll","C:\Program Files (x86)\Reference Assemblies\Microsoft\Framework\v3.5\System.Data.DataSetExtensions.dll","C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll","C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll","C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Transactions.dll","C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll" /keyfile:Key.snk /target:Library /out:Transaction.dll InventoryMover.vb`  
  
    -   `Csc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Transactions.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll /keyfile:key.snk /out:Transaction.dll /target:library InventoryMover.cs`  
  
5.  [!INCLUDE[tsql](../../includes/tsql-md.md)] インストール コードをファイルにコピーし、`install.sql` としてサンプル ディレクトリに保存します。  
  
6.  次のコマンドを実行して、アセンブリとストアド プロシージャを配置します。  
  
    -   `sqlcmd -E -I -i install.sql -v root = "C:\MySample\"`  
  
7.  [!INCLUDE[tsql](../../includes/tsql-md.md)] データベースのインストールコードをファイルにコピーし、`installDB.sql` としてサンプルディレクトリに保存します。  
  
8.  次のコマンドを実行して、監査データベースをインストールします。  
  
    -   `Sqlcmd -S server_name [ \instance_name ] -E -I -i installDB.sql`  
  
     このコマンドを実行するときには、インスタンスとサーバーの適切な値を指定します。  
  
9. テストコマンドスクリプトをファイルにコピー [!INCLUDE[tsql](../../includes/tsql-md.md)]、`test.sql` としてサンプルディレクトリに保存します。  
  
10. 次のコマンドを使用してテスト スクリプトを実行します。  
  
    -   `sqlcmd -E -I -i test.sql`  
  
11. [!INCLUDE[tsql](../../includes/tsql-md.md)] データベース クリーンアップ スクリプトをファイルにコピーし、`cleanupDB.sql` としてサンプル ディレクトリに保存します。  
  
12. 次のコマンドを使用してこのスクリプトを実行します。  
  
    -   `Sqlcmd -S server_name [ \instance_name ] -E -I -i cleanup.sql`  
  
         このコマンドを実行するときには、インスタンスとサーバーの適切な値を指定します。  
  
13. [!INCLUDE[tsql](../../includes/tsql-md.md)] クリーンアップ スクリプトをファイルにコピーし、`cleanup.sql` としてサンプル ディレクトリに保存します。  
  
14. 次のコマンドを使用してこのスクリプトを実行します。  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a>サンプル コード  
 このサンプルのコード リストを次に示します。  
  
 C#  
  
```  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using System.Transactions;  
using Microsoft.SqlServer.Server;  
using System.Security.Principal;  
  
    public static class InventoryMover  
    {  
        const string contextConnectionString = "context connection=true";  
  
        // **********  
        // Important: Change this connection string to refer to a server other than the one  
        // you have installed the AdventureWorks database.  This sample demonstrates   
        // two-phase commit across multiple servers, and loopback to the same server is not  
        // permitted from CLR integrated based stored procedures.  
        // **********  
        const string auditConnectionString = "server=<YourServer>; database=InventoryAudit; user=<YourUser>; password=<YourPassword>";  
  
        [SqlMethod(DataAccess = DataAccessKind.Read, IsMutator = true)]  
        public static void ExecuteTransfer(int productID, short fromLocationID,  
            short toLocationID, short quantityToTransfer)  
        {  
                       // Establish bounds of the transaction  
            using (TransactionScope transScope = new TransactionScope())  
            {  
                using (SqlConnection adventureworksConnection = new  
                   SqlConnection(contextConnectionString))  
                {  
                    // Opening adventureworksConnection automatically enlists it in the   
                    // TransactionScope as part of the transaction.  
                    adventureworksConnection.Open();  
  
                    SqlCommand checkCommand = adventureworksConnection.CreateCommand();  
                    checkCommand.CommandText = "SELECT TOP 1 Quantity"  
                        + " FROM Production.ProductInventory WITH (REPEATABLEREAD)"  
                        + " WHERE ProductID = @ProductID AND LocationID = @LocationID;";  
                    checkCommand.Parameters.Add("@ProductID", SqlDbType.Int);  
                    checkCommand.Parameters[0].Value = productID;  
                    checkCommand.Parameters.Add("@LocationID", SqlDbType.Int);  
                    checkCommand.Parameters[1].Value = fromLocationID;  
  
                    object result = checkCommand.ExecuteScalar();  
                    short availableQuantity = (short)result;  
  
                    if (availableQuantity < quantityToTransfer)  
                        //It would be better to throw a custom error, and in some cases to actually  
                        //RAISERROR.  Also, it would be better to map product IDs and location IDs to   
                        //names for the error message.  
                        throw new ArgumentOutOfRangeException("quantityToTransfer",  
                            string.Format("Attempt to transfer {0} of product {1} from"  
                                + " location {2} but only {3} is available.",  
                                quantityToTransfer, productID, fromLocationID,  
                                availableQuantity));  
  
                    //Remove inventory count from source  
                    SqlCommand reduceCommand = adventureworksConnection.CreateCommand();  
                    reduceCommand.CommandText = "UPDATE Production.ProductInventory"  
                        + " SET Quantity = Quantity - @QuantityToTransfer"  
                        + " WHERE ProductID = @ProductID AND LocationID = @LocationID;";  
                    reduceCommand.Parameters.Add("@ProductID", SqlDbType.Int);  
                    reduceCommand.Parameters[0].Value = productID;  
                    reduceCommand.Parameters.Add("@LocationID", SqlDbType.SmallInt);  
                    reduceCommand.Parameters[1].Value = fromLocationID;  
                    reduceCommand.Parameters.Add("@QuantityToTransfer", SqlDbType.SmallInt);  
                    reduceCommand.Parameters[2].Value = quantityToTransfer;  
  
                    reduceCommand.ExecuteNonQuery();  
  
                    //Increate inventory count at destination  
                    SqlCommand increaseCommand = adventureworksConnection.CreateCommand();  
                    increaseCommand.CommandText = "UPDATE Production.ProductInventory"  
                        + " SET Quantity = Quantity + @QuantityToTransfer"  
                        + " WHERE ProductID = @ProductID AND LocationID = @LocationID;";  
                    increaseCommand.Parameters.Add("@ProductID", SqlDbType.Int);  
                    increaseCommand.Parameters[0].Value = productID;  
                    increaseCommand.Parameters.Add("@LocationID", SqlDbType.SmallInt);  
                    increaseCommand.Parameters[1].Value = toLocationID;  
                    increaseCommand.Parameters.Add("@QuantityToTransfer", SqlDbType.SmallInt);  
                    increaseCommand.Parameters[2].Value = quantityToTransfer;  
  
                    increaseCommand.ExecuteNonQuery();  
  
                    // Create an audit trail of the inventory transfer.  We must impersonate the  
                    // client credentials in order for this to work.  Otherwise we'd have to  
                    // set up security for the machine account.  
//                    SqlConnection auditConnection = adventureworksConnection;  
                    using (SqlConnection auditConnection = new SqlConnection(auditConnectionString))  
                    {  
                        SqlCommand auditCommand = auditConnection.CreateCommand();  
                        auditCommand.CommandText = "INSERT InventoryChange "  
                            + " (ProductID, FromLocationID, ToLocationID, Quantity) "  
                            + " VALUES (@ProductID, @FromLocationID, @ToLocationID, @Quantity);";  
                        auditCommand.Parameters.Add("@ProductID", SqlDbType.Int);  
                        auditCommand.Parameters[0].Value = productID;  
                        auditCommand.Parameters.Add("@FromLocationID", SqlDbType.SmallInt);  
                        auditCommand.Parameters[1].Value = fromLocationID;  
                        auditCommand.Parameters.Add("@ToLocationID", SqlDbType.SmallInt);  
                        auditCommand.Parameters[2].Value = toLocationID;  
                        auditCommand.Parameters.Add("@Quantity", SqlDbType.SmallInt);  
                        auditCommand.Parameters[3].Value = quantityToTransfer;  
  
                        // Opening auditConnection automatically enlists it in the   
                        // TransactionScope as part of the transaction.  
                        auditConnection.Open();  
                        auditCommand.ExecuteNonQuery();  
                    }  
  
                }  
                //  The Complete method commits the transaction.  
                transScope.Complete();  
            }  
        }  
    }  
  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Collections.Generic  
Imports System.Text  
Imports System.Data  
Imports System.Data.SqlTypes  
Imports System.Data.SqlClient  
Imports System.Transactions  
Imports Microsoft.SqlServer.Server  
Imports System.Security.Principal  
Imports System.Globalization  
  
Public NotInheritable Class InventoryMover  
    Private Const contextConnectionString As String = "context connection=true"  
  
    Private Sub New()  
  
    End Sub  
  
    ' **********  
    ' Important: Change this connection string to refer to a server other than the one  
    ' you have installed the AdventureWorks database.  This sample demonstrates   
    ' two-phase commit across multiple servers, and loopback to the same server is not  
    ' permitted from CLR integrated based stored procedures.  
    ' **********  
    Private Const auditConnectionString As String = "server=<YourServer>; database=InventoryAudit; user=<YourUser>; password=<YourPassword>"  
    <SqlMethod(DataAccess:=DataAccessKind.Read, IsMutator:=True)> _  
    Public Shared Sub ExecuteTransfer(ByVal productID As Integer, ByVal fromLocationID As Short, _  
        ByVal toLocationID As Short, ByVal quantityToTransfer As Short)  
        ' Establish bounds of the transaction  
        Using transScope As New TransactionScope()  
            Using adventureworksConnection As New SqlConnection(contextConnectionString)  
                ' Opening adventureworksConnection automatically enlists it in the   
                ' TransactionScope as part of the transaction.  
                adventureworksConnection.Open()  
  
                Dim checkCommand As SqlCommand = adventureworksConnection.CreateCommand()  
                checkCommand.CommandText = "SELECT TOP 1 Quantity" _  
                        & " FROM Production.ProductInventory WITH (REPEATABLEREAD)" _  
                        & " WHERE ProductID = @ProductID AND LocationID = @LocationID;"  
                checkCommand.Parameters.Add("@ProductID", SqlDbType.Int)  
                checkCommand.Parameters(0).Value = productID  
                checkCommand.Parameters.Add("@LocationID", SqlDbType.Int)  
                checkCommand.Parameters(1).Value = fromLocationID  
  
                Dim result As Object = checkCommand.ExecuteScalar()  
                Dim availableQuantity As Short = CType(result, Short)  
  
                If (availableQuantity < quantityToTransfer) Then  
                    'It would be better to throw a custom error, and in some cases to actually  
                    'RAISERROR.  Also, it would be better to map product IDs and location IDs to   
                    'names for the error message.  
                    Throw New ArgumentOutOfRangeException("quantityToTransfer", _  
                        String.Format(CultureInfo.InvariantCulture, "Attempt to transfer {0} of product {1} from" _  
                        & " location {2} but only {3} is available.", _  
                        quantityToTransfer, productID, fromLocationID, _  
                        availableQuantity))  
                End If  
  
                'Remove inventory count from source  
                Dim reduceCommand As SqlCommand = adventureworksConnection.CreateCommand()  
                reduceCommand.CommandText = "UPDATE Production.ProductInventory" _  
                    & " SET Quantity = Quantity - @QuantityToTransfer" _  
                    & " WHERE ProductID = @ProductID AND LocationID = @LocationID;"  
                reduceCommand.Parameters.Add("@ProductID", SqlDbType.Int)  
                reduceCommand.Parameters(0).Value = productID  
                reduceCommand.Parameters.Add("@LocationID", SqlDbType.SmallInt)  
                reduceCommand.Parameters(1).Value = fromLocationID  
                reduceCommand.Parameters.Add("@QuantityToTransfer", SqlDbType.SmallInt)  
                reduceCommand.Parameters(2).Value = quantityToTransfer  
  
                reduceCommand.ExecuteNonQuery()  
  
                'Increate inventory count at destination  
                Dim increaseCommand As SqlCommand = adventureworksConnection.CreateCommand()  
                increaseCommand.CommandText = "UPDATE Production.ProductInventory" _  
                    & " SET Quantity = Quantity + @QuantityToTransfer" _  
                    & " WHERE ProductID = @ProductID AND LocationID = @LocationID;"  
                increaseCommand.Parameters.Add("@ProductID", SqlDbType.Int)  
                increaseCommand.Parameters(0).Value = productID  
                increaseCommand.Parameters.Add("@LocationID", SqlDbType.SmallInt)  
                increaseCommand.Parameters(1).Value = toLocationID  
                increaseCommand.Parameters.Add("@QuantityToTransfer", SqlDbType.SmallInt)  
                increaseCommand.Parameters(2).Value = quantityToTransfer  
  
                increaseCommand.ExecuteNonQuery()  
  
                ' Create an audit trail of the inventory transfer.  We must impersonate the  
                ' client credentials in order for this to work.  Otherwise we'd have to  
                ' set up security for the machine account.  
                'SqlConnection auditConnection = adventureworksConnection  
                Using auditConnection As New SqlConnection(auditConnectionString)  
                    Dim auditCommand As SqlCommand = auditConnection.CreateCommand()  
                    auditCommand.CommandText = "INSERT InventoryChange " _  
                        & " (ProductID, FromLocationID, ToLocationID, Quantity) " _  
                        & " VALUES (@ProductID, @FromLocationID, @ToLocationID, @Quantity);"  
                    auditCommand.Parameters.Add("@ProductID", SqlDbType.Int)  
                    auditCommand.Parameters(0).Value = productID  
                    auditCommand.Parameters.Add("@FromLocationID", SqlDbType.SmallInt)  
                    auditCommand.Parameters(1).Value = fromLocationID  
                    auditCommand.Parameters.Add("@ToLocationID", SqlDbType.SmallInt)  
                    auditCommand.Parameters(2).Value = toLocationID  
                    auditCommand.Parameters.Add("@Quantity", SqlDbType.SmallInt)  
                    auditCommand.Parameters(3).Value = quantityToTransfer  
  
                    ' Opening auditConnection automatically enlists it in the   
                    ' TransactionScope as part of the transaction.  
                    auditConnection.Open()  
                    auditCommand.ExecuteNonQuery()  
  
                End Using  
            End Using  
  
            '  The Complete method commits the transaction.  
            transScope.Complete()  
        End Using  
    End Sub  
End Class  
  
```  
  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] インストール スクリプト (`Install.sql`) は、アセンブリを展開し、データベースにストアド プロシージャを作成します。  
  
```  
USE AdventureWorks  
GO  
  
-- Drop existing sproc and assembly if any.  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_ExecuteTransfer')  
DROP PROCEDURE usp_ExecuteTransfer;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'Transaction')  
DROP ASSEMBLY [Transaction];  
GO  
  
USE master  
GO  
  
IF EXISTS (SELECT * FROM sys.server_principals WHERE [name] = 'ExternalSample_Login')  
DROP LOGIN ExternalSample_Login;  
GO  
  
IF EXISTS (SELECT * FROM sys.asymmetric_keys WHERE [name] = 'ExternalSample_Key')  
DROP ASYMMETRIC KEY ExternalSample_Key;  
GO  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of the this variable if you have installed the sample someplace other than the default location.  
set @SamplesPath = 'C:\MySample\'  
  
EXEC('CREATE ASYMMETRIC KEY ExternalSample_Key FROM EXECUTABLE FILE = ''' + @SamplesPath + 'Transaction.dll'';');  
CREATE LOGIN ExternalSample_Login FROM ASYMMETRIC KEY ExternalSample_Key  
GRANT EXTERNAL ACCESS ASSEMBLY TO ExternalSample_Login  
GO  
  
USE AdventureWorks  
GO  
  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of this variable if you have installed the sample someplace other than the default location.  
set @SamplesPath = 'C:\MySample\'  
-- Add the assembly and CLR integration based stored procedure  
  
CREATE ASSEMBLY [Transaction]   
FROM @SamplesPath + 'Transaction.dll'  
WITH permission_set = External_Access;  
GO  
  
CREATE PROCEDURE usp_ExecuteTransfer  
(  
@ProductID int,  
@FromLocationID smallint,  
@ToLocationID smallint,  
@QuantityToTransfer smallint  
)  
AS EXTERNAL NAME [Transaction].[InventoryMover].ExecuteTransfer;  
GO  
```  
  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] インストール スクリプト (`InstallDB.sql`) は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 2 つ目のインスタンスに監査データベースを作成します。  
  
```  
SET NOCOUNT OFF;  
GO  
  
PRINT CONVERT(varchar(1000), @@VERSION);  
GO  
  
PRINT '';  
PRINT 'Started - ' + CONVERT(varchar, GETDATE(), 121);  
GO  
  
USE [master];  
GO  
  
-- ****************************************  
-- Drop Database  
-- ****************************************  
PRINT '';  
PRINT '*** Dropping Database';  
GO  
  
IF EXISTS (SELECT [name] FROM [master].[sys].[databases] WHERE [name] = N'InventoryAudit')  
    DROP DATABASE [InventoryAudit];  
  
-- If the database has any other open connections close the network connection.  
IF @@ERROR = 3702   
    RAISERROR('[InventoryAudit] database cannot be dropped because there are still other open connections', 127, 127) WITH NOWAIT, LOG;  
GO  
  
-- ****************************************  
-- Create Database  
-- ****************************************  
PRINT '';  
PRINT '*** Creating Database';  
GO  
  
DECLARE   
    @sql_path nvarchar(256),   
    @sql_cmd nvarchar(256);  
  
SELECT @sql_path = SUBSTRING([physical_name], 1, CHARINDEX(N'master.mdf', LOWER([physical_name])) - 1)  
FROM [master].[sys].[master_files]   
WHERE [database_id] = 1   
    AND [file_id] = 1;  
  
-- COLLATE Latin1_General_CS_AS  
EXECUTE (N'CREATE DATABASE [InventoryAudit]   
    ON (NAME = ''InventoryAudit_Data'', FILENAME = N''' + @sql_path + N'InventoryAudit_Data.mdf'', SIZE = 120, FILEGROWTH = 8)   
    LOG ON (NAME = ''InventoryAudit_Log'', FILENAME = N''' + @sql_path + N'InventoryAudit_Log.ldf'' , SIZE = 2, FILEGROWTH = 96);');  
GO  
  
ALTER DATABASE [InventoryAudit]   
SET RECOVERY SIMPLE,   
    ANSI_NULLS ON,   
    ANSI_PADDING ON,   
    ANSI_WARNINGS ON,   
    ARITHABORT ON,   
    CONCAT_NULL_YIELDS_NULL ON,   
    QUOTED_IDENTIFIER ON,   
    NUMERIC_ROUNDABORT OFF,   
    PAGE_VERIFY CHECKSUM,   
    ALLOW_SNAPSHOT_ISOLATION OFF;  
GO  
  
USE [InventoryAudit];  
GO  
  
PRINT '';  
PRINT '*** Creating Table';  
GO  
  
CREATE TABLE [InventoryChange] (  
[InventoryChangeID] int IDENTITY (1, 1) NOT NULL,  
[ProductID] int NOT NULL,  
[FromLocationID] smallint,  
[ToLocationID] smallint,  
[Quantity] smallint NOT NULL  
);  
GO  
  
```  
  
 次の `test.sql` は、関数を実行してサンプルをテストします。  
  
```  
USE AdventureWorks  
GO  
SELECT 'Before first transfer quantity of adjustable races at Tool Crib = ', Quantity FROM Production.ProductInventory  
WHERE ProductID = 1 AND LocationID = 1  
  
SELECT 'Before first transfer quantity of adjustable races at Miscellaneous Storage = ', Quantity FROM Production.ProductInventory  
WHERE ProductID = 1 AND LocationID = 6  
  
--Move 12 adjustable race parts (product id 1) from the Tool Crib (location id 1)   
--to Miscellaneous Storage (location id 6).  
EXEC usp_ExecuteTransfer 1, 1, 6, 12  
  
SELECT 'After first transfer quantity of adjustable races at Tool Crib = ', Quantity FROM Production.ProductInventory  
WHERE ProductID = 1 AND LocationID = 1  
  
SELECT 'After first transfer quantity of adjustable races at Miscellaneous Storage = ', Quantity FROM Production.ProductInventory  
WHERE ProductID = 1 AND LocationID = 6  
  
--Move them back  
EXEC usp_ExecuteTransfer 1, 6, 1, 12  
  
SELECT 'After second transfer quantity of adjustable races at Tool Crib = ', Quantity FROM Production.ProductInventory  
WHERE ProductID = 1 AND LocationID = 1  
  
SELECT 'After second transfer quantity of adjustable races at Miscellaneous Storage = ', Quantity FROM Production.ProductInventory  
WHERE ProductID = 1 AND LocationID = 6  
  
The following tsql removes the assembly and stored procedure from the database (Cleanup.sql).  
USE AdventureWorks  
GO  
  
-- Drop existing sproc and assembly if any.  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_ExecuteTransfer')  
DROP PROCEDURE usp_ExecuteTransfer;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'Transaction')  
DROP ASSEMBLY [Transaction];  
GO  
  
USE master  
GO  
  
IF EXISTS (SELECT * FROM sys.server_principals WHERE [name] = 'ExternalSample_Login')  
DROP LOGIN ExternalSample_Login;  
GO  
  
IF EXISTS (SELECT * FROM sys.asymmetric_keys WHERE [name] = 'ExternalSample_Key')  
DROP ASYMMETRIC KEY ExternalSample_Key;  
GO  
  
USE AdventureWorks  
GO  
```  
  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] は、2 つ目のインスタンスから監査データベースを削除します。  
  
```  
SET NOCOUNT OFF;  
GO  
  
PRINT CONVERT(varchar(1000), @@VERSION);  
GO  
  
PRINT '';  
PRINT 'Started - ' + CONVERT(varchar, GETDATE(), 121);  
GO  
  
USE [master];  
GO  
  
-- ****************************************  
-- Drop Database  
-- ****************************************  
PRINT '';  
PRINT '*** Dropping Database';  
GO  
  
IF EXISTS (SELECT [name] FROM [master].[sys].[databases] WHERE [name] = N'InventoryAudit')  
    DROP DATABASE [InventoryAudit];  
  
-- If the database has any other open connections close the network connection.  
IF @@ERROR = 3702   
    RAISERROR('[InventoryAudit] database cannot be dropped because there are still other open connections', 127, 127) WITH NOWAIT, LOG;  
GO  
```  
  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] は、アセンブリと関数をデータベースから削除します。  
  
```  
SE AdventureWorks  
GO  
  
-- Drop existing sproc and assembly if any.  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_ExecuteTransfer')  
DROP PROCEDURE usp_ExecuteTransfer;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'Transaction')  
DROP ASSEMBLY [Transaction];  
GO  
  
USE master  
GO  
  
IF EXISTS (SELECT * FROM sys.server_principals WHERE [name] = 'ExternalSample_Login')  
DROP LOGIN ExternalSample_Login;  
GO  
  
IF EXISTS (SELECT * FROM sys.asymmetric_keys WHERE [name] = 'ExternalSample_Key')  
DROP ASYMMETRIC KEY ExternalSample_Key;  
GO  
  
USE AdventureWorks  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CLR &#40;共通言語ランタイム&#41; 統合の使用シナリオと例](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
