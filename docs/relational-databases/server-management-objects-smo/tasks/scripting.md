---
title: スクリプト |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- dependencies [SMO]
- scripts [SMO]
ms.assetid: 13a35511-3987-426b-a3b7-3b2e83900dc7
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 63f6e86f08ea93525704159483b939c79c6575d8
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909041"
---
# <a name="scripting"></a>スクリプトの作成
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  SMO でのスクリプト作成は、<xref:Microsoft.SqlServer.Management.Smo.Scripter> オブジェクトとその子オブジェクト、または個々のオブジェクトの**スクリプト**メソッドによって制御されます。 <xref:Microsoft.SqlServer.Management.Smo.Scripter> オブジェクトは、[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンス上のオブジェクトの依存関係からのマッピングを制御します。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Scripter> オブジェクト、およびその子オブジェクトを使用する高度なスクリプティング プロセスには、次の 3 つのフェーズがあります。  
  
1.  検出  
  
2.  リスト生成  
  
3.  スクリプト生成  

 検索フェーズでは、<xref:Microsoft.SqlServer.Management.Smo.DependencyWalker> オブジェクトが使用されます。 オブジェクトの URN リストが指定されている場合、<xref:Microsoft.SqlServer.Management.Smo.DependencyWalker.DiscoverDependencies%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker> メソッドは、URN リスト内のオブジェクトに対応する <xref:Microsoft.SqlServer.Management.Smo.DependencyTree> オブジェクトを返します。 ブール型の*Fparents*パラメーターを使用して、指定したオブジェクトの親または子を検出するかどうかを選択します。 依存関係ツリーはこの段階で変更することができます。  
  
 リスト生成フェーズでは、このツリーが渡され、結果リストが返されます。 このオブジェクト リストは記述順であり、変更することもできます。  
  
 リスト生成フェーズでは、<xref:Microsoft.SqlServer.Management.Smo.DependencyWalker.WalkDependencies%2A> メソッドを使用して <xref:Microsoft.SqlServer.Management.Smo.DependencyTree> を返します。 <xref:Microsoft.SqlServer.Management.Smo.DependencyTree> はこの段階で変更することができます。  
  
 3 番目の最後のフェーズでは、指定されたリストとスクリプティング オプションを使用してスクリプトが生成されます。 結果は <xref:System.Collections.Specialized.StringCollection> システム オブジェクトとして返されます。 このフェーズで、<xref:Microsoft.SqlServer.Management.Smo.DependencyTree> オブジェクトの Items コレクションおよび <xref:Microsoft.SqlServer.Management.Smo.DependencyTree.NumberOfSiblings%2A> や <xref:Microsoft.SqlServer.Management.Smo.DependencyTree.FirstChild%2A> などのプロパティから、依存オブジェクト名が抽出されます。  
  
## <a name="example"></a>例  
 提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual Studio&#35; .Net での Visual C SMO プロジェクトの作成](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
 このコード例では、system.string 名前空間の**Imports**ステートメントが必要です。 アプリケーションの宣言の前、かつ他の Imports ステートメントの後に、次のステートメントを挿入します。  
  
```  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Common  
Imports System.Collections.Specialized  
```  
  
## <a name="scripting-out-the-dependencies-for-a-database-in-visual-basic"></a>Visual Basic でデータベースの依存関係のスクリプトを作成する  
 このコード例では、依存関係を検出する方法と、リストを反復処理して結果を表示する方法を示します。  
  
```  
' compile with:   
' /r:Microsoft.SqlServer.Smo.dll   
' /r:Microsoft.SqlServer.ConnectionInfo.dll   
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Sdk.Sfc  
  
Public Class A  
   Public Shared Sub Main()  
      ' database name  
      Dim dbName As [String] = "AdventureWorksLT2012"   ' database name  
  
      ' Connect to the local, default instance of SQL Server.   
      Dim srv As New Server()  
  
      ' Reference the database.    
      Dim db As Database = srv.Databases(dbName)  
  
      ' Define a Scripter object and set the required scripting options.   
      Dim scrp As New Scripter(srv)  
      scrp.Options.ScriptDrops = False  
      scrp.Options.WithDependencies = True  
      scrp.Options.Indexes = True   ' To include indexes  
      scrp.Options.DriAllConstraints = True   ' to include referential constraints in the script  
  
      ' Iterate through the tables in database and script each one. Display the script.  
      For Each tb As Table In db.Tables  
         ' check if the table is not a system table  
         If tb.IsSystemObject = False Then  
            Console.WriteLine("-- Scripting for table " + tb.Name)  
  
            ' Generating script for table tb  
            Dim sc As System.Collections.Specialized.StringCollection = scrp.Script(New Urn() {tb.Urn})  
            For Each st As String In sc  
               Console.WriteLine(st)  
            Next  
            Console.WriteLine("--")  
         End If  
      Next  
   End Sub  
End Class  
```  
  
## <a name="scripting-out-the-dependencies-for-a-database-in-visual-c"></a>Visual C# でデータベースの依存関係のスクリプトを作成する  
 このコード例では、依存関係を検出する方法と、リストを反復処理して結果を表示する方法を示します。  
  
```  
// compile with:   
// /r:Microsoft.SqlServer.Smo.dll   
// /r:Microsoft.SqlServer.ConnectionInfo.dll   
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
using System;  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Sdk.Sfc;  
  
public class A {  
   public static void Main() {   
      String dbName = "AdventureWorksLT2012"; // database name  
  
      // Connect to the local, default instance of SQL Server.   
      Server srv = new Server();  
  
      // Reference the database.    
      Database db = srv.Databases[dbName];  
  
      // Define a Scripter object and set the required scripting options.   
      Scripter scrp = new Scripter(srv);  
      scrp.Options.ScriptDrops = false;  
      scrp.Options.WithDependencies = true;  
      scrp.Options.Indexes = true;   // To include indexes  
      scrp.Options.DriAllConstraints = true;   // to include referential constraints in the script  
  
      // Iterate through the tables in database and script each one. Display the script.     
      foreach (Table tb in db.Tables) {   
         // check if the table is not a system table  
         if (tb.IsSystemObject == false) {  
            Console.WriteLine("-- Scripting for table " + tb.Name);  
  
            // Generating script for table tb  
            System.Collections.Specialized.StringCollection sc = scrp.Script(new Urn[]{tb.Urn});  
            foreach (string st in sc) {  
               Console.WriteLine(st);  
            }  
            Console.WriteLine("--");  
         }  
      }   
   }  
}  
```  
  
## <a name="scripting-out-the-dependencies-for-a-database-in-powershell"></a>PowerShell でデータベースの依存関係のスクリプトを作成する  
 このコード例では、依存関係を検出する方法と、リストを反復処理して結果を表示する方法を示します。  
  
```  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default  
  
# Create a Scripter object and set the required scripting options.  
$scrp = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Scripter -ArgumentList (Get-Item .)  
$scrp.Options.ScriptDrops = $false  
$scrp.Options.WithDependencies = $true  
$scrp.Options.IncludeIfNotExists = $true  
  
# Set the path context to the tables in AdventureWorks2012.  
  
CD Databases\AdventureWorks2012\Tables  
  
foreach ($Item in Get-ChildItem)  
 {    
 $scrp.Script($Item)  
 }  
```  
  
  
