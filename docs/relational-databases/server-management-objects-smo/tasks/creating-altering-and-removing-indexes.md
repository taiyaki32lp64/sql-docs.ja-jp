---
title: インデックスの作成、変更、および削除
ms.custom: seo-dt-2019
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- indexes [SMO]
ms.assetid: ad1befa5-46e0-4895-b9d3-42852e07607b
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 42acad11884fa9edc779d6aa52a94ccf38ee5444
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095518"
---
# <a name="creating-altering-and-removing-indexes"></a>インデックスの作成、変更、および削除

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  SMO ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理オブジェクト) 階層では、インデックスは <xref:Microsoft.SqlServer.Management.Smo.Index> オブジェクトで表現します。 インデックス付き列は、<xref:Microsoft.SqlServer.Management.Smo.IndexedColumn> プロパティによって表される <xref:Microsoft.SqlServer.Management.Smo.Index.IndexedColumns%2A> オブジェクトのコレクションで表現します。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Index.IsXmlIndex%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Index> プロパティを指定すると、XML 列のインデックスを作成できます。  
  
## <a name="examples"></a>使用例  
 提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual Studio&#35; .Net での Visual C SMO プロジェクトの作成](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="creating-a-non-clustered-composite-index-in-visual-basic"></a>Visual Basic での非クラスター化複合インデックスの作成  
 このコード例では、複合の非クラスター化インデックスを作成する方法を示します。 複合インデックスの場合、2 つ以上の列をインデックスに追加します。 非クラスター化インデックスの場合は、<xref:Microsoft.SqlServer.Management.Smo.Index.IsClustered%2A> プロパティを**False**に設定します。  
  
```  
' /r:Microsoft.SqlServer.Smo.dll  
' /r:Microsoft.SqlServer.ConnectionInfo.dll  
' /r:Microsoft.SqlServer.SqlEnum.dll  
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
Imports Microsoft.SqlServer.Management.Smo  
Public Class A  
    Public Shared Sub Main()  
        ' Connect to the local, default instance of SQL Server.   
        Dim srv As Server  
        srv = New Server()  
  
        ' Reference the AdventureWorks2012 database.   
        Dim db As Database  
        db = srv.Databases("AdventureWorks2012")  
  
        ' Declare a Table object and reference the HumanResources table.   
        Dim tb As Table  
        tb = db.Tables("Employee", "HumanResources")  
  
        ' Define an Index object variable by providing the parent table and index name in the constructor.   
        Dim idx As Index  
        idx = New Index(tb, "TestIndex")  
  
        ' Add indexed columns to the index.   
        Dim icol1 As IndexedColumn  
        icol1 = New IndexedColumn(idx, "BusinessEntityID", True)  
        idx.IndexedColumns.Add(icol1)  
        Dim icol2 As IndexedColumn  
        icol2 = New IndexedColumn(idx, "HireDate", True)  
        idx.IndexedColumns.Add(icol2)  
  
        ' Set the index properties.   
        idx.IndexKeyType = IndexKeyType.DriUniqueKey  
        idx.IsClustered = False  
        idx.FillFactor = 50  
  
        ' Create the index on the instance of SQL Server.   
        idx.Create()  
  
        ' Modify the page locks property.   
        idx.DisallowPageLocks = True  
  
        ' Run the Alter method to make the change on the instance of SQL Server.   
        idx.Alter()  
  
        ' Remove the index from the table.   
        idx.Drop()  
    End Sub  
End Class  
  
```  
  
## <a name="creating-a-non-clustered-composite-index-in-visual-c"></a>Visual C# での非クラスター化複合インデックスの作成  
 このコード例では、複合の非クラスター化インデックスを作成する方法を示します。 複合インデックスの場合、2 つ以上の列をインデックスに追加します。 非クラスター化インデックスの場合は、<xref:Microsoft.SqlServer.Management.Smo.Index.IsClustered%2A> プロパティを**False**に設定します。  
  
```  
// /r:Microsoft.SqlServer.Smo.dll  
// /r:Microsoft.SqlServer.ConnectionInfo.dll  
// /r:Microsoft.SqlServer.SqlEnum.dll  
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
using Microsoft.SqlServer.Management.Smo;  
  
public class A {  
   public static void Main() {  
      // Connect to the local, default instance of SQL Server.   
      Server srv;  
      srv = new Server();  
  
      // Reference the AdventureWorks2012 database.   
      Database db;  
      db = srv.Databases["AdventureWorks2012"];  
  
      // Declare a Table object and reference the HumanResources table.   
      Table tb;  
      tb = db.Tables["Employee", "HumanResources"];  
  
      // Define an Index object variable by providing the parent table and index name in the constructor.   
      Index idx;  
      idx = new Index(tb, "TestIndex");  
  
      // Add indexed columns to the index.   
      IndexedColumn icol1;  
      icol1 = new IndexedColumn(idx, "BusinessEntityID", true);  
      idx.IndexedColumns.Add(icol1);  
      IndexedColumn icol2;  
      icol2 = new IndexedColumn(idx, "HireDate", true);  
      idx.IndexedColumns.Add(icol2);  
  
      // Set the index properties.   
      idx.IndexKeyType = IndexKeyType.DriUniqueKey;  
      idx.IsClustered = false;  
      idx.FillFactor = 50;  
  
      // Create the index on the instance of SQL Server.   
      idx.Create();  
  
      // Modify the page locks property.   
      idx.DisallowPageLocks = true;  
  
      // Run the Alter method to make the change on the instance of SQL Server.   
      idx.Alter();  
  
      // Remove the index from the table.   
      idx.Drop();  
   }  
}  
  
```  
  
## <a name="creating-a-non-clustered-composite-index-in-powershell"></a>PowerShell での非クラスター化複合インデックスの作成  
 このコード例では、複合の非クラスター化インデックスを作成する方法を示します。 複合インデックスの場合、2 つ以上の列をインデックスに追加します。 非クラスター化インデックスの場合は、<xref:Microsoft.SqlServer.Management.Smo.Index.IsClustered%2A> プロパティを**False**に設定します。  
  
```  
# Set the path context to the local, default instance of SQL Server and to the  
#database tables in Adventureworks2012  
CD \sql\localhost\default\databases\AdventureWorks2012\Tables\  
  
#Get a reference to the table  
$tb = get-item HumanResources.Employee  
  
#Define an Index object variable by providing the parent table and index name in the constructor.   
$idx = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Index -argumentlist $tb, "TestIndex"  
  
#Add indexed columns to the index.   
$icol1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.IndexedColumn `  
-argumentlist $idx, "BusinessEntityId", $true  
$idx.IndexedColumns.Add($icol1)  
  
$icol2 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.IndexedColumn `  
-argumentlist $idx, "HireDate", $true  
$idx.IndexedColumns.Add($icol2)  
  
#Set the index properties.   
$idx.IndexKeyType = [Microsoft.SqlServer.Management.SMO.IndexKeyType]::DriUniqueKey   
$idx.IsClustered = $false  
$idx.FillFactor = 50  
  
#Create the index on the instance of SQL Server.   
$idx.Create()  
  
#Modify the page locks property.   
$idx.DisallowPageLocks = $true  
  
#Run the Alter method to make the change on the instance of SQL Server.   
$idx.Alter()  
  
#Remove the index from the table.   
$idx.Drop();  
```  
  
## <a name="creating-an-xml-index-in-visual-basic"></a>Visual Basic での XML インデックスの作成  
 このコード例では、XML データ型に対して XML インデックスを作成する方法を示します。 XML データ型は MySampleCollection という名前の XML スキーマコレクションで、XML スキーマ[を使用して](../../../relational-databases/server-management-objects-smo/tasks/using-xml-schemas.md)作成されます。 XML インデックスにはいくつかの制限事項がありますが、その 1 つは、XML インデックスはクラスター化主キーを既に持っているテーブルに作成する必要があるという点です。  
  
```  
' /r:Microsoft.SqlServer.Smo.dll  
' /r:Microsoft.SqlServer.ConnectionInfo.dll  
' /r:Microsoft.SqlServer.SqlEnum.dll  
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
Imports Microsoft.SqlServer.Management.Smo  
  
Public Class A  
    Public Shared Sub Main()  
        ' Connect to the local, default instance of SQL Server.   
        Dim srv As Server  
        srv = New Server()  
        Dim db1 As Database = srv.Databases("TESTDB")  
        ' Define a Table object variable and add an XML type column.   
        Dim tb As New Table(db1, "XmlTable3")  
  
        Dim mySample As New XmlSchemaCollection(db1, "Sample4", "dbo")  
        mySample.Text = "<xsd:schema xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" targetNamespace=""NS2""> <xsd:element name=""elem1"" type=""xsd:integer""/></xsd:schema>"  
        mySample.Create()  
  
        Dim col11 As Column  
  
        ' This sample requires that an XML schema type called MySampleCollection exists on the database.   
        col11 = New Column(tb, "XMLValue", DataType.Xml("Sample4"))  
  
        ' Add another integer column that can be made into a unique, primary key.   
        tb.Columns.Add(col11)  
        Dim col21 As Column  
        col21 = New Column(tb, "Number", DataType.Int)  
        col21.Nullable = False  
        tb.Columns.Add(col21)  
  
        ' Create the table of the instance of SQL Server.   
        tb.Create()  
  
        ' Create a unique, clustered, primary key index on the integer column. This is required for an XML index.   
        Dim cp As Index  
        cp = New Index(tb, "clusprimindex3")  
        cp.IsClustered = True  
        cp.IndexKeyType = IndexKeyType.DriPrimaryKey  
        Dim cpcol As IndexedColumn  
        cpcol = New IndexedColumn(cp, "Number", True)  
        cp.IndexedColumns.Add(cpcol)  
        cp.Create()  
  
        ' Define and XML Index object variable by supplying the parent table and the XML index name arguments in the constructor.   
        Dim i As Index  
        i = New Index(tb, "xmlindex")  
        Dim ic As IndexedColumn  
        ic = New IndexedColumn(i, "XMLValue", True)  
        i.IndexedColumns.Add(ic)  
  
        ' Create the XML index on the instance of SQL Server.   
        i.Create()  
    End Sub  
End Class  
  
```  
  
## <a name="creating-an-xml-index-in-visual-c"></a>Visual C# での XML インデックスの作成  
 このコード例では、XML データ型に対して XML インデックスを作成する方法を示します。 XML データ型は MySampleCollection という名前の XML スキーマコレクションで、XML スキーマ[を使用して](../../../relational-databases/server-management-objects-smo/tasks/using-xml-schemas.md)作成されます。 XML インデックスにはいくつかの制限事項がありますが、その 1 つは、XML インデックスはクラスター化主キーを既に持っているテーブルに作成する必要があるという点です。  
  
```  
// /r:Microsoft.SqlServer.Smo.dll  
// /r:Microsoft.SqlServer.ConnectionInfo.dll  
// /r:Microsoft.SqlServer.SqlEnum.dll  
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
using Microsoft.SqlServer.Management.Smo;  
  
public class A {  
   public static void Main() {  
      // Connect to the local, default instance of SQL Server.   
      Server srv;  
      srv = new Server();  
      Database db1 = srv.Databases["TESTDB"];  
      // Define a Table object variable and add an XML type column.   
      Table tb = new Table(db1, "XmlTable3");  
  
      XmlSchemaCollection mySample = new XmlSchemaCollection(db1, "Sample4", "dbo");  
      mySample.Text = "<xsd:schema xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\" targetNamespace=\"NS2\"> <xsd:element name=\"elem1\" type=\"xsd:integer\"/></xsd:schema>";  
      mySample.Create();  
  
      Column col11;  
  
      // This sample requires that an XML schema type called MySampleCollection exists on the database.   
      col11 = new Column(tb, "XMLValue", DataType.Xml("Sample4"));  
  
      // Add another integer column that can be made into a unique, primary key.   
      tb.Columns.Add(col11);  
      Column col21;  
      col21 = new Column(tb, "Number", DataType.Int);  
      col21.Nullable = false;  
      tb.Columns.Add(col21);  
  
      // Create the table of the instance of SQL Server.   
      tb.Create();  
  
      // Create a unique, clustered, primary key index on the integer column. This is required for an XML index.   
      Index cp;  
      cp = new Index(tb, "clusprimindex3");  
      cp.IsClustered = true;  
      cp.IndexKeyType = IndexKeyType.DriPrimaryKey;  
      IndexedColumn cpcol;  
      cpcol = new IndexedColumn(cp, "Number", true);  
      cp.IndexedColumns.Add(cpcol);  
      cp.Create();  
  
      // Define and XML Index object variable by supplying the parent table and the XML index name arguments in the constructor.   
      Index i;  
      i = new Index(tb, "xmlindex");  
      IndexedColumn ic;  
      ic = new IndexedColumn(i, "XMLValue", true);  
      i.IndexedColumns.Add(ic);  
  
      // Create the XML index on the instance of SQL Server.   
      i.Create();  
   }  
}  
  
```  
  
## <a name="creating-an-xml-index-in-powershell"></a>PowerShell での XML インデックスの作成  
 このコード例では、XML データ型に対して XML インデックスを作成する方法を示します。 XML データ型は MySampleCollection という名前の XML スキーマコレクションで、XML スキーマ[を使用して](../../../relational-databases/server-management-objects-smo/tasks/using-xml-schemas.md)作成されます。 XML インデックスにはいくつかの制限事項がありますが、その 1 つは、XML インデックスはクラスター化主キーを既に持っているテーブルに作成する必要があるという点です。  
  
```  
# Set the path context to the local, default instance of SQL Server and get a reference to adventureworks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
#Define a Table object variable and add an XML type column.   
#This sample requires that an XML schema type called MySampleCollection exists on the database.   
#See sample on Creating an XML schema to do this  
$tb = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Table -argumentlist $db, "XmlTable"  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::Xml("MySampleCollection")  
$col1 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"XMLValue", $Type  
$tb.Columns.Add($col1)  
  
#Add another integer column that can be made into a unique, primary key.   
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::Int  
$col2 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"Number", $Type  
$col2.Nullable = $false  
$tb.Columns.Add($col2)  
  
#Create the table of the instance of SQL Server.   
$tb.Create()  
  
#Create a unique, clustered, primary key index on the integer column. This is required for an XML index.   
#Define an Index object variable by providing the parent table and index name in the constructor.   
$cp = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Index -argumentlist $tb, "clusprimindex"          
$cp.IsClustered = $true;  
$cp.IndexKeyType = [Microsoft.SqlServer.Management.SMO.IndexKeyType]::DriPrimaryKey;  
  
#Create and add an indexed column to the index.   
$cpcol = New-Object -TypeName Microsoft.SqlServer.Management.SMO.IndexedColumn `  
-argumentlist $cp, "Number", $true  
$cp.IndexedColumns.Add($cpcol)  
$cp.Create()  
  
#Define and XML Index object variable by supplying the parent table and  
# the XML index name arguments in the constructor.   
$i = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Index -argumentlist $tb, "xmlindex"   
  
#Create and add an indexed column to the index.   
$ic = New-Object -TypeName Microsoft.SqlServer.Management.SMO.IndexedColumn `  
-argumentlist $i, "XMLValue", $true    
$i.IndexedColumns.Add($ic)  
  
#Create the XML index on the instance of SQL Server  
$i.Create()  
```  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.SqlServer.Management.Smo.Index>  
  
  
