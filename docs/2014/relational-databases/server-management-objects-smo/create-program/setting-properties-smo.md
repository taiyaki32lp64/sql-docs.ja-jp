---
title: プロパティの設定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SMO [SQL Server], properties
- SQL Server Management Objects, properties
- properties [SMO]
ms.assetid: 342569ba-d2f7-44d2-8f3f-ae9c701c7f0f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f07d9b2f613ca1face8be3bb23bac78202da6655
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63192151"
---
# <a name="setting-properties"></a>プロパティの設定
  プロパティとは、オブジェクトに関する説明情報を格納する値のことです。 たとえば、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]構成オプションがによって表される、<xref:Microsoft.SqlServer.Management.Smo.Server.Configuration%2A>オブジェクトのプロパティ。 プロパティは、直接、またはプロパティ コレクションを使用して間接的にアクセスすることができます。 プロパティへの直接アクセス時には、次の構文を使用します。  
  
 `objInstance.PropertyName`  
  
 プロパティ値は、そのプロパティが読み取り/書き込みアクセスまたは読み取り専用アクセスのどちらであるかに応じて、変更または取得を行うことができます。 また、オブジェクトを作成する前に、特定のプロパティを設定する必要もあります。 詳細については、SMO 参考資料で特定のオブジェクトを参照してください。  
  
> [!NOTE]  
>  子オブジェクトのコレクションは、オブジェクトのプロパティとして表現されます。 たとえば、`Tables` コレクションは、`Server` オブジェクトのプロパティとなります。 詳しくは、「 [Using Collections](using-collections.md)」をご覧ください。  
  
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
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="getting-and-setting-a-property-in-visual-basic"></a>Visual Basic でのプロパティの取得および設定  
 このコード例では、<xref:Microsoft.SqlServer.Management.Smo.Information.Edition%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Information> プロパティを取得する方法と、<xref:Microsoft.SqlServer.Management.Common.ServerConnection.SqlExecutionModes%2A> プロパティの <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> プロパティを <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes> 列挙型の `ExecuteSql` メンバーに設定する方法を示します。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBProperties1](SMO How to#SMO_VBProperties1)]  -->  
  
## <a name="getting-and-setting-a-property-in-visual-c"></a>Visual C# でのプロパティの取得および設定  
 このコード例では、<xref:Microsoft.SqlServer.Management.Smo.Information.Edition%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Information> プロパティを取得する方法と、<xref:Microsoft.SqlServer.Management.Common.ServerConnection.SqlExecutionModes%2A> プロパティの <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> プロパティを <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes> 列挙型の `ExecuteSql` メンバーに設定する方法を示します。  
  
```  
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
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBProperties2](SMO How to#SMO_VBProperties2)]  -->  
  
## <a name="setting-various-properties-before-an-object-is-created-in-visual-c"></a>Visual C# でのオブジェクト作成前のさまざまなプロパティの設定  
 このコード例では、<xref:Microsoft.SqlServer.Management.Smo.Table.AnsiNullsStatus%2A> オブジェクトを作成する前に、<xref:Microsoft.SqlServer.Management.Smo.Table> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Table> プロパティを直接設定する方法、および列の作成と追加を行う方法を示します。  
  
```  
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
 このコード例では、<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> オブジェクトの `Properties` コレクションが反復処理され、[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] の出力画面に表示されます。  
  
 この例では、<xref:Microsoft.SqlServer.Management.Smo.Property> オブジェクトは [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] のキーワードでもあるため、角かっこで囲まれています。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBProperties3](SMO How to#SMO_VBProperties3)]  -->  
  
## <a name="iterating-through-all-properties-of-an-object-in-visual-c"></a>Visual C# でのオブジェクトのすべてのプロパティの反復処理  
 このコード例では、<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> オブジェクトの `Properties` コレクションが反復処理され、[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] の出力画面に表示されます。  
  
```  
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
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDefaultInitFields1](SMO How to#SMO_VBDefaultInitFields1)]  -->  
  
## <a name="setting-default-initialization-fields-in-visual-c"></a>Visual C# での既定の初期化フィールドの設定  
 このコード例では、SMO プログラムで初期化されるオブジェクト プロパティの数を最小にする方法を示します。 <xref:System.Collections.Specialized.StringCollection> オブジェクトを使用するには、`using System.Collections.Specialized` ステートメントを含める必要があります。  
  
 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] を使用すれば、この最適化によって [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに送信されるステートメントの数を比較することができます。  
  
```  
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
  
  
