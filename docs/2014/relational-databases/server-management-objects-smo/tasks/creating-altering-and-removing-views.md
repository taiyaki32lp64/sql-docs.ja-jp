---
title: ビューの作成、変更、および削除 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- views [SMO]
ms.assetid: 7d445c0e-77ef-4734-993b-e022de31df23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e593ac7da77603bf0b14eb450446322ce7d975cd
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782302"
---
# <a name="creating-altering-and-removing-views"></a>ビューの作成、変更、および削除
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ビューは <xref:Microsoft.SqlServer.Management.Smo.View> オブジェクトで表現されます。  
  
 <xref:Microsoft.SqlServer.Management.Smo.View.TextBody%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.View> プロパティはビューを定義します。 これは、ビューを作成する [!INCLUDE[tsql](../../../includes/tsql-md.md)] SELECT ステートメントと等価です。  
  
## <a name="example"></a>例  
 提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual studio .net での VISUAL BASIC SMO プロジェクトの作成](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)」または「visual [studio .Net での Visual C&#35; SMO プロジェクトの作成](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="creating-altering-and-removing-a-view-in-visual-basic"></a>Visual Basic でのビューの作成、変更、および削除  
 このコード例では、内部結合を使用して 2 つのテーブルのビューを作成する方法を示します。 このビューはテキスト モードを使用して作成されるため、<xref:Microsoft.SqlServer.Management.Smo.View.TextHeader%2A> プロパティが設定されている必要があります。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBViews1](SMO How to#SMO_VBViews1)]  -->  
  
## <a name="creating-altering-and-removing-a-view-in-visual-c"></a>Visual C# でのビューの作成、変更、および削除  
 このコード例では、内部結合を使用して 2 つのテーブルのビューを作成する方法を示します。 このビューはテキスト モードを使用して作成されるため、<xref:Microsoft.SqlServer.Management.Smo.View.TextHeader%2A> プロパティが設定されている必要があります。  
  
```csharp
{  
        //Connect to the local, default instance of SQL Server.   
        Server srv;   
        srv = new Server();   
        //Reference the AdventureWorks2012 database.   
        Database db;   
        db = srv.Databases["AdventureWorks2012"];   
        //Define a View object variable by supplying the parent database, view name and schema in the constructor.   
        View myview;   
        myview = new View(db, "Test_View", "Sales");   
        //Set the TextHeader and TextBody property to define the view.   
        myview.TextHeader = "CREATE VIEW [Sales].[Test_View] AS";   
        myview.TextBody = "SELECT h.SalesOrderID, d.OrderQty FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID";   
        //Create the view on the instance of SQL Server.   
        myview.Create();   
        //Remove the view.   
        myview.Drop();   
        }  
```  
  
## <a name="creating-altering-and-removing-a-view-in-powershell"></a>PowerShell でのビューの作成、変更、および削除  
 このコード例では、内部結合を使用して 2 つのテーブルのビューを作成する方法を示します。 このビューはテキスト モードを使用して作成されるため、<xref:Microsoft.SqlServer.Management.Smo.View.TextHeader%2A> プロパティが設定されている必要があります。  
  
```powershell
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = Get-Item Adventureworks2012  
  
# Define a View object variable by supplying the parent database, view name and schema in the constructor.
$myview  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.View -argumentlist $db, "Test_View", "Sales"  
  
# Set the TextHeader and TextBody property to define the view.
$myview.TextHeader = "CREATE VIEW [Sales].[Test_View] AS"  
$myview.TextBody ="SELECT h.SalesOrderID, d.OrderQty FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID"  
  
# Create the view on the instance of SQL Server.
$myview.Create()  
  
# Remove the view
$myview.Drop();  
```  
  
## <a name="see-also"></a>「  
 <xref:Microsoft.SqlServer.Management.Smo.View>  
