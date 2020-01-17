---
title: 設定のプロパティ-SMO |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SMO [SQL Server], properties
- SQL Server Management Objects, properties
- properties [SMO]
ms.assetid: 342569ba-d2f7-44d2-8f3f-ae9c701c7f0f
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6ffcdda8e1c6a3c85703ad7f3d6ed94ca0ca91fe
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2019
ms.locfileid: "70148714"
---
# <a name="setting-properties---smo"></a>プロパティの設定 - SMO
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  プロパティとは、オブジェクトに関する説明情報を格納する値のことです。 たとえば、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]構成オプションは、オブジェクトのプロパティによって表されます。<xref:Microsoft.SqlServer.Management.Smo.Server.Configuration%2A> プロパティは、直接、またはプロパティ コレクションを使用して間接的にアクセスすることができます。 プロパティへの直接アクセス時には、次の構文を使用します。  
  
 `objInstance.PropertyName`  
  
 プロパティ値は、そのプロパティが読み取り/書き込みアクセスまたは読み取り専用アクセスのどちらであるかに応じて、変更または取得を行うことができます。 また、オブジェクトを作成する前に、特定のプロパティを設定する必要もあります。 詳細については、SMO 参考資料で特定のオブジェクトを参照してください。  
  
> [!NOTE]  
>  子オブジェクトのコレクションは、オブジェクトのプロパティとして表現されます。 たとえば、 **Tables** コレクションは、 **Server** オブジェクトのプロパティとなります。 詳しくは、「 [Using Collections](../../../relational-databases/server-management-objects-smo/create-program/using-collections.md)」をご覧ください。  
  
 オブジェクトのプロパティは、Properties コレクションのメンバーです。 Properties コレクションを使用して、オブジェクトの各プロパティを反復処理することができます。  
  
 次の理由によって、プロパティを使用できない場合があります。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の以前のバージョンで、新しい [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 機能を表すプロパティにアクセスしようとするなど、サーバーのバージョンがプロパティをサポートしていない場合。  
  
-   インストールされていない [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コンポーネントを表すプロパティにアクセスしようとするなど、サーバーがプロパティのデータを提供しない場合。  
  
 <xref:Microsoft.SqlServer.Management.Smo.UnknownPropertyException> および <xref:Microsoft.SqlServer.Management.Smo.PropertyCannotBeRetrievedException> の SMO 例外をキャッチすることによって、これらの状況に対処することができます。  
  
## <a name="setting-default-initialization-fields"></a>既定の初期化フィールドの設定  
 SMO は、オブジェクトの取得時に最適化を行います。 最適化によって、次の状態の間で自動的にスケーリングを行うことによって読み込まれるプロパティ数を最小限に抑えることができます。  
  
1.  部分的読み込み。 オブジェクトへの最初の参照時には、最少限のプロパティ (Name や Schema など) のみが使用可能になります。  
  
2.  完全読み込み。 いずれかのプロパティが参照されたとき、すぐに読み込まれた残りのプロパティが初期化されて使用可能になります。  
  
3.  大量のメモリを使用するプロパティ。 これ以外の、多くのメモリを使用し、<xref:Microsoft.SqlServer.Management.Smo.Property.Expensive%2A> プロパティ値 (<xref:Microsoft.SqlServer.Management.Smo.Database.DataSpaceUsage%2A> など) の値が true であるプロパティは読み込まれません。 これらのプロパティは、明示的に参照された場合にのみ読み込まれます。  
  
 部分的に読み込まれた状態で提供されたプロパティだけでなく、それ以外のプロパティもアプリケーションによってフェッチされる場合、これらの追加のプロパティを取得するクエリが送信され、完全に読み込まれた状態にスケール アップされます。 これにより、クライアントとサーバーの間に不要なトラフィックが発生する場合があります。 <xref:Microsoft.SqlServer.Management.Smo.Server.SetDefaultInitFields%2A> メソッドを呼び出すことにより、さらに最適化を行うことができます。 <xref:Microsoft.SqlServer.Management.Smo.Server.SetDefaultInitFields%2A> メソッドを使用すると、オブジェクトの初期化時に読み込まれるプロパティを指定することができます。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Server.SetDefaultInitFields%2A> メソッドでは、アプリケーションの残り部分に対して、またはリセットされるまでの、プロパティの読み込み動作を設定することができます。 <xref:Microsoft.SqlServer.Management.Smo.Server.GetDefaultInitFields%2A> メソッドを使用して、元の動作を保存し、必要に応じて復元することができます。  
  
## <a name="examples"></a>使用例  
提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual Studio&#35; .Net での Visual C SMO プロジェクトの作成](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  

  
## <a name="getting-and-setting-a-property-in-visual-basic"></a>Visual Basic でのプロパティの取得および設定  
 <xref:Microsoft.SqlServer.Management.Smo.Information.Edition%2A>このコード例<xref:Microsoft.SqlServer.Management.Smo.Information> <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> では<xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes> 、オブジェクトのプロパティを取得する方法と、プロパティのプロパティを列挙型のExecuteSqlメンバーに設定する方法を示し<xref:Microsoft.SqlServer.Management.Common.ServerConnection.SqlExecutionModes%2A>ます。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Get a property.
Console.WriteLine(srv.Information.Version)
'Set a property.
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.ExecuteSql
```
  
## <a name="getting-and-setting-a-property-in-visual-c"></a>Visual C# でのプロパティの取得および設定  
 <xref:Microsoft.SqlServer.Management.Smo.Information.Edition%2A>このコード例<xref:Microsoft.SqlServer.Management.Smo.Information> <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> では<xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes> 、オブジェクトのプロパティを取得する方法と、プロパティのプロパティを列挙型のExecuteSqlメンバーに設定する方法を示し<xref:Microsoft.SqlServer.Management.Common.ServerConnection.SqlExecutionModes%2A>ます。  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Get a property.   
Console.WriteLine(srv.Information.Version);   
//Set a property.   
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.ExecuteSql;   
}  
```  
  
## <a name="setting-various-properties-before-an-object-is-created-in-visual-basic"></a>Visual Basic でのオブジェクト作成前のさまざまなプロパティの設定  
 このコード例では、<xref:Microsoft.SqlServer.Management.Smo.Table.AnsiNullsStatus%2A> オブジェクトを作成する前に、<xref:Microsoft.SqlServer.Management.Smo.Table> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Table> プロパティを直接設定する方法、および列の作成と追加を行う方法を示します。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Create a new table in the AdventureWorks2012 database. 
Dim db As Database
db = srv.Databases("AdventureWorks2012")
Dim tb As Table
'Specify the parent database, table schema and the table name in the constructor.
tb = New Table(db, "Test_Table", "HumanResources")
'Add columns because the table requires columns before it can be created. 
Dim c1 As Column
'Specify the parent table, the column name and data type in the constructor.
c1 = New Column(tb, "ID", DataType.Int)
tb.Columns.Add(c1)
c1.Nullable = False
c1.Identity = True
c1.IdentityIncrement = 1
c1.IdentitySeed = 0
Dim c2 As Column
c2 = New Column(tb, "Name", DataType.NVarChar(100))
c2.Nullable = False
tb.Columns.Add(c2)
tb.AnsiNullsStatus = True
'Create the table on the instance of SQL Server.
tb.Create()
```
  
## <a name="setting-various-properties-before-an-object-is-created-in-visual-c"></a>Visual C# でのオブジェクト作成前のさまざまなプロパティの設定  
 このコード例では、<xref:Microsoft.SqlServer.Management.Smo.Table.AnsiNullsStatus%2A> オブジェクトを作成する前に、<xref:Microsoft.SqlServer.Management.Smo.Table> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Table> プロパティを直接設定する方法、および列の作成と追加を行う方法を示します。  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Create a new table in the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
Table tb;   
//Specify the parent database, table schema, and the table name in the constructor.   
tb = new Table(db, "Test_Table", "HumanResources");   
//Add columns because the table requires columns before it can be created.   
Column c1;   
//Specify the parent table, the column name, and data type in the constructor.   
c1 = new Column(tb, "ID", DataType.Int);   
tb.Columns.Add(c1);   
c1.Nullable = false;   
c1.Identity = true;   
c1.IdentityIncrement = 1;   
c1.IdentitySeed = 0;   
Column c2;   
c2 = new Column(tb, "Name", DataType.NVarChar(100));   
c2.Nullable = false;   
tb.Columns.Add(c2);   
tb.AnsiNullsStatus = true;   
//Create the table on the instance of SQL Server.   
tb.Create();   
}  
```  
  
## <a name="iterating-through-all-properties-of-an-object-in-visual-basic"></a>Visual Basic でのオブジェクトのすべてのプロパティの反復処理  
 このコード例では<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> 、オブジェクトの**Properties**コレクションを反復処理し、 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]出力画面に表示します。  
  
 この例では、<xref:Microsoft.SqlServer.Management.Smo.Property> オブジェクトは [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] のキーワードでもあるため、角かっこで囲まれています。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Set properties on the uspGetEmployeeManagers stored procedure on the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
Dim sp As StoredProcedure
sp = db.StoredProcedures("uspGetEmployeeManagers")
sp.AnsiNullsStatus = False
sp.QuotedIdentifierStatus = False
'Iterate through the properties of the stored procedure and display.
'Note the Property object requires [] parentheses to distinguish it from the Visual Basic key word.
Dim p As [Property]
For Each p In sp.Properties
    Console.WriteLine(p.Name & p.Value)
Next
```
  
## <a name="iterating-through-all-properties-of-an-object-in-visual-c"></a>Visual C# でのオブジェクトのすべてのプロパティの反復処理  
 このコード例では<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> 、オブジェクトの**Properties**コレクションを反復処理し、 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]出力画面に表示します。  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Set properties on the uspGetEmployeedManagers stored procedure on the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
StoredProcedure sp;   
sp = db.StoredProcedures("uspGetEmployeeManagers");   
sp.AnsiNullsStatus = false;   
sp.QuotedIdentifierStatus = false;   
//Iterate through the properties of the stored procedure and display.   
  Property p;   
  foreach ( p in sp.Properties) {   
    Console.WriteLine(p.Name + p.Value);   
  }   
}  
```  
  
## <a name="setting-default-initialization-fields-in-visual-basic"></a>Visual Basic での既定の初期化フィールドの設定  
 このコード例では、SMO プログラムで初期化されるオブジェクト プロパティの数を最小にする方法を示します。 <xref:System.Collections.Specialized.StringCollection> オブジェクトを使用するには、`using System.Collections.Specialized` ステートメントを含める必要があります。  
  
 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] を使用すれば、この最適化によって [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに送信されるステートメントの数を比較することができます。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Assign the Table object type to a System.Type object variable.
Dim tb As Table
Dim typ As Type
tb = New Table
typ = tb.GetType
'Assign the current default initialization fields for the Table object type to a 
'StringCollection object variable.
Dim sc As StringCollection
sc = srv.GetDefaultInitFields(typ)
'Set the default initialization fields for the Table object type to the CreateDate property.
srv.SetDefaultInitFields(typ, "CreateDate")
'Retrieve the Schema, Name, and CreateDate properties for every table in AdventureWorks2012.
'Note that the improvement in performance can be viewed in SQL Profiler.
For Each tb In db.Tables
    Console.WriteLine(tb.Schema + "." + tb.Name + " " + tb.CreateDate)
Next
'Set the default initialization fields for the Table object type back to the original settings.
srv.SetDefaultInitFields(typ, sc)
```
  
## <a name="setting-default-initialization-fields-in-visual-c"></a>Visual C# での既定の初期化フィールドの設定  
 このコード例では、SMO プログラムで初期化されるオブジェクト プロパティの数を最小にする方法を示します。 <xref:System.Collections.Specialized.StringCollection> オブジェクトを使用するには、`using System.Collections.Specialized` ステートメントを含める必要があります。  
  
 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] を使用すれば、この最適化によって [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに送信されるステートメントの数を比較することができます。  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Assign the Table object type to a System.Type object variable.   
Table tb;   
Type typ;   
tb = new Table();   
typ = tb.GetType;   
//Assign the current default initialization fields for the Table object type to a   
//StringCollection object variable.   
StringCollection sc;   
sc = srv.GetDefaultInitFields(typ);   
//Set the default initialization fields for the Table object type to the CreateDate property.   
srv.SetDefaultInitFields(typ, "CreateDate");   
//Retrieve the Schema, Name, and CreateDate properties for every table in AdventureWorks2012.   
   //Note that the improvement in performance can be viewed in SQL Server Profiler.   
foreach ( tb in db.Tables) {   
   Console.WriteLine(tb.Schema + "." + tb.Name + " " + tb.CreateDate);   
}   
//Set the default initialization fields for the Table object type back to the original settings.   
srv.SetDefaultInitFields(typ, sc);   
}  
```  
  
  
