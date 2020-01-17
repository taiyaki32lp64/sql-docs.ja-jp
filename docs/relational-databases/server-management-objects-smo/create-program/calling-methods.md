---
title: メソッドの呼び出し |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- methods [SMO]
- calling methods
- SQL Server Management Objects, method calling
- SMO [SQL Server], method calling
ms.assetid: c88d5c5f-9ff0-4f84-b2b6-24c6b90fa15e
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 471549e5a42f8d08a62da37c4e98e66bc9b67413
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2019
ms.locfileid: "70148759"
---
# <a name="calling-methods"></a>メソッドの呼び出し
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  メソッドは、データベースでの**チェックポイント**の発行や、の[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンスに対するログオンの列挙リストの要求など、オブジェクトに関連する特定のタスクを実行します。  
  
 メソッドはオブジェクトに対する操作を実行します。 メソッドはパラメーターを受け取ることができ、多くの場合は戻り値があります。 戻り値には、単純なデータ型、複雑なオブジェクト、複数のメンバーを含んでいる構造のいずれを使用することもできます。  
  
 メソッドが正常に実行されたかどうかを検出するには、例外処理を使用します。 詳しくは、「 [Handling SMO Exceptions](../../../relational-databases/server-management-objects-smo/create-program/handling-smo-exceptions.md)」をご覧ください。  
  
## <a name="examples"></a>使用例  
提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual Studio&#35; .Net での Visual C SMO プロジェクトの作成](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
 
  
## <a name="using-a-simple-smo-method-in-visual-basic"></a>Visual Basic での簡単な SMO メソッドの使用  
 この例で、<xref:Microsoft.SqlServer.Management.Smo.Database.Create%2A> メソッドにはパラメーターがなく、戻り値もありません。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Define a Database object variable by supplying the parent server and the database name arguments in the constructor.
Dim db As Database
db = New Database(srv, "Test_SMO_Database")
'Call the Create method to create the database on the instance of SQL Server. 
db.Create()
```
  
## <a name="using-a-simple-smo-method-in-visual-c"></a>Visual C# での簡単な SMO メソッドの使用  
 この例で、<xref:Microsoft.SqlServer.Management.Smo.Database.Create%2A> メソッドにはパラメーターがなく、戻り値もありません。  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Define a Database object variable by supplying the parent server and the database name arguments in the constructor.   
Database db;   
db = new Database(srv, "Test_SMO_Database");   
//Call the Create method to create the database on the instance of SQL Server.   
db.Create();   
```  
  
 }  
  
## <a name="using-an-smo-method-with-a-parameter-in-visual-basic"></a>Visual Basic でのパラメーターを指定した SMO メソッドの使用  
 <xref:Microsoft.SqlServer.Management.Smo.Table> オブジェクトには、<xref:Microsoft.SqlServer.Management.Smo.Table.RebuildIndexes%2A> と呼ばれるメソッドがあります。 このメソッドには、 **FillFactor**を指定する数値パラメーターが必要です。  
  
```VBNET
Dim srv As Server  
srv = New Server  
Dim tb As Table  
tb = srv.Databases("AdventureWorks2012").Tables("Employee", "HumanResources")  
tb.RebuildIndexes(70)  
```  
  
## <a name="using-an-smo-method-with-a-parameter-in-visual-c"></a>Visual C# でのパラメーターを指定した SMO メソッドの使用  
 <xref:Microsoft.SqlServer.Management.Smo.Table> オブジェクトには、<xref:Microsoft.SqlServer.Management.Smo.Table.RebuildIndexes%2A> と呼ばれるメソッドがあります。 このメソッドには、 `FillFactor`を指定する数値パラメーターが必要です。  
  
```csharp  
{   
Server srv = default(Server);   
srv = new Server();   
Table tb = default(Table);   
tb = srv.Databases("AdventureWorks2012").Tables("Employee", "HumanResources");   
tb.RebuildIndexes(70);   
}   
```  
  
## <a name="using-an-enumeration-method-that-returns-a-datatable-object-in-visual-basic"></a>Visual Basic での DataTable オブジェクトを返す列挙メソッドの使用  
 このセクションでは、列挙メソッドを呼び出す方法、および返された <xref:System.Data.DataTable> オブジェクト内のデータを処理する方法について説明します。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Server.EnumCollations%2A> メソッドは <xref:System.Data.DataTable> オブジェクトを返します。このオブジェクトでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに関する利用可能な照合順序情報のすべてにアクセスするには、追加の操作を行う必要があります。  
  
```VBNET
'Connect to the local, default instance of SQL Server.  
Dim srv As Server  
srv = New Server  
'Call the EnumCollations method and return collation information to DataTable variable.  
Dim d As DataTable  
'Select the returned data into an array of DataRow.  
d = srv.EnumCollations  
'Iterate through the rows and display collation details for the instance of SQL Server.  
Dim r As DataRow  
Dim c As DataColumn  
For Each r In d.Rows  
    Console.WriteLine("==")  
    For Each c In r.Table.Columns  
        Console.WriteLine(c.ColumnName + " = " + r(c).ToString)  
    Next  
Next  
```  
  
## <a name="using-an-enumeration-method-that-returns-a-datatable-object-in-visual-c"></a>Visual C# での DataTable オブジェクトを返す列挙メソッドの使用  
 このセクションでは、列挙メソッドを呼び出す方法、および返された <xref:System.Data.DataTable> オブジェクト内のデータを処理する方法について説明します。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Server.EnumCollations%2A> メソッドは、システム <xref:System.Data.DataTable> オブジェクトを返します。 <xref:System.Data.DataTable> オブジェクトでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに関する利用可能な照合順序情報のすべてにアクセスするには、追加の操作を行う必要があります。  
  
```csharp  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
//Call the EnumCollations method and return collation information to DataTable variable.   
DataTable d = default(DataTable);   
//Select the returned data into an array of DataRow.   
d = srv.EnumCollations;   
//Iterate through the rows and display collation details for the instance of SQL Server.   
DataRow r = default(DataRow);   
DataColumn c = default(DataColumn);   
foreach ( r in d.Rows) {   
  Console.WriteLine("=========");   
  foreach ( c in r.Table.Columns) {   
    Console.WriteLine(c.ColumnName + " = " + r(c).ToString);   
  }   
}   
}   
```  
  
## <a name="constructing-an-object-in-visual-basic"></a>Visual Basic でのオブジェクトの構築  
 オブジェクトのコンストラクターは、 **New** 演算子を使用して呼び出すことができます。 <xref:Microsoft.SqlServer.Management.Smo.Database> オブジェクト コンストラクターはオーバーロードされます。コード例で使用するバージョンの <xref:Microsoft.SqlServer.Management.Smo.Database> オブジェクト コンストラクターでは、パラメーターとして、データベースの親である <xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクトおよび新しいデータベースの名前を表す文字列を受け取ります。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Declare and define a Database object by supplying the parent server and the database name arguments in the constructor.
Dim d As Database
d = New Database(srv, "Test_SMO_Database")
'Create the database on the instance of SQL Server.
d.Create()
Console.WriteLine(d.Name)
```
  
## <a name="constructing-an-object-in-visual-c"></a>Visual C# でのオブジェクトの構築  
 オブジェクトのコンストラクターは、 **New** 演算子を使用して呼び出すことができます。 <xref:Microsoft.SqlServer.Management.Smo.Database> オブジェクト コンストラクターはオーバーロードされます。コード例で使用するバージョンの <xref:Microsoft.SqlServer.Management.Smo.Database> オブジェクト コンストラクターでは、パラメーターとして、データベースの親である <xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクトおよび新しいデータベースの名前を表す文字列を受け取ります。  
  
```csharp  
{   
Server srv;   
srv = new Server();   
Table tb;   
tb = srv.Databases("AdventureWorks2012").Tables("Employee", "HumanResources");   
tb.RebuildIndexes(70);   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Declare and define a Database object by supplying the parent server and the database name arguments in the constructor.   
Database d;   
d = new Database(srv, "Test_SMO_Database");   
//Create the database on the instance of SQL Server.   
d.Create();   
Console.WriteLine(d.Name);   
}  
```  
  
## <a name="copying-an-smo-object-in-visual-basic"></a>Visual Basic での SMO オブジェクトのコピー  
 このコード例では、<xref:Microsoft.SqlServer.Management.Common.ServerConnection.Copy%2A> メソッドを使用して <xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクトのコピーを作成する方法を示します。 <xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクトは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスへの接続を表します。  
  
```VBNET  
'Connect to the local, default instance of SQL Server.
Dim srv1 As Server
srv1 = New Server()
'Modify the default database and the timeout period for the connection.
srv1.ConnectionContext.DatabaseName = "AdventureWorks2012"
srv1.ConnectionContext.ConnectTimeout = 30
'Make a second connection using a copy of the ConnectionContext property and verify settings.
Dim srv2 As Server
srv2 = New Server(srv1.ConnectionContext.Copy)
Console.WriteLine(srv2.ConnectionContext.ConnectTimeout.ToString)
```
  
## <a name="copying-an-smo-object-in-visual-c"></a>Visual C# での SMO オブジェクトのコピー  
 このコード例では、<xref:Microsoft.SqlServer.Management.Common.ServerConnection.Copy%2A> メソッドを使用して <xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクトのコピーを作成する方法を示します。 <xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクトは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスへの接続を表します。  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv1;   
srv1 = new Server();   
//Modify the default database and the timeout period for the connection.   
srv1.ConnectionContext.DatabaseName = "AdventureWorks2012";   
srv1.ConnectionContext.ConnectTimeout = 30;   
//Make a second connection using a copy of the ConnectionContext property and verify settings.   
Server srv2;   
srv2 = new Server(srv1.ConnectionContext.Copy);   
Console.WriteLine(srv2.ConnectionContext.ConnectTimeout.ToString);   
}  
```  
  
## <a name="monitoring-server-processes-in-visual-basic"></a>Visual Basic でのサーバー プロセスの監視  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに関する現在の状態の型情報は、列挙メソッドを使用して取得することができます。 コード例では、<xref:Microsoft.SqlServer.Management.Smo.Server.EnumProcesses%2A> メソッドを使用して、現在のプロセスに関する情報を検出します。 また、返された <xref:System.Data.DataTable> オブジェクトの列および行を操作する方法も示します。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Call the EnumCollations method and return collation information to DataTable variable.
Dim d As DataTable
'Select the returned data into an array of DataRow.
d = srv.EnumProcesses
'Iterate through the rows and display collation details for the instance of SQL Server.
Dim r As DataRow
Dim c As DataColumn
For Each r In d.Rows
    Console.WriteLine("============================================")
    For Each c In r.Table.Columns
        Console.WriteLine(c.ColumnName + " = " + r(c).ToString)
    Next
Next
```
  
## <a name="monitoring-server-processes-in-visual-c"></a>Visual C# でのサーバー プロセスの監視  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに関する現在の状態の型情報は、列挙メソッドを使用して取得することができます。 コード例では、<xref:Microsoft.SqlServer.Management.Smo.Server.EnumProcesses%2A> メソッドを使用して、現在のプロセスに関する情報を検出します。 また、返された <xref:System.Data.DataTable> オブジェクトの列および行を操作する方法も示します。  
  
```csharp  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
//Call the EnumCollations method and return collation information to DataTable variable.   
DataTable d = default(DataTable);   
//Select the returned data into an array of DataRow.   
d = srv.EnumProcesses;   
//Iterate through the rows and display collation details for the instance of SQL Server.   
DataRow r = default(DataRow);   
DataColumn c = default(DataColumn);   
foreach ( r in d.Rows) {   
  Console.WriteLine("=====");   
  foreach ( c in r.Table.Columns) {   
    Console.WriteLine(c.ColumnName + " = " + r(c).ToString);   
  }   
}   
}   
```  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  
