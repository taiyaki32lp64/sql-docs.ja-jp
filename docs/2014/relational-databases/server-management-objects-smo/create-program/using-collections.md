---
title: コレクションの使用 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQL Server Management Objects, collections
- SMO [SQL Server], collections
- collections [SMO]
ms.assetid: 209eb175-2514-4de1-bc32-b2e6a469d945
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0be31e67be0b80de13a9239b221ca73436a8d6e7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63192124"
---
# <a name="using-collections"></a>コレクションの使用
  コレクションとは、同じオブジェクト クラスから作成された、同じ親オブジェクトを持つオブジェクトのリストのことです。 コレクション オブジェクトには、Collection サフィックス付きのオブジェクトの種類の名前が必ず含まれています。 たとえば、指定されたテーブル内の列にアクセスするには、<xref:Microsoft.SqlServer.Management.Smo.ColumnCollection> というオブジェクトの種類を使用します。 これには、同じ <xref:Microsoft.SqlServer.Management.Smo.Column> オブジェクトに属するすべての <xref:Microsoft.SqlServer.Management.Smo.Table> オブジェクトが含まれます。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] `For...Each`ステートメントまたは[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] `foreach`コレクションの各メンバーを反復処理するステートメントを使用できます。  
  
## <a name="examples"></a>使用例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-basic"></a>Visual Basic でのコレクションを使用したオブジェクトの参照  
 このコード例では、<xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A> プロパティ、<xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> プロパティ、および <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A> プロパティを使用して、列プロパティを設定する方法を示します。 これらのプロパティはコレクションを表現しており、オブジェクトの名前を指定するパラメーターと共に使用すれば、特定のオブジェクトを識別するために使用できます。 <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> コレクション オブジェクト プロパティには、名前とスキーマが必要です。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCollections1](SMO How to#SMO_VBCollections1)]  -->  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-c"></a>Visual C# でのコレクションを使用したオブジェクトの参照  
 このコード例では、<xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A> プロパティ、<xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> プロパティ、および <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A> プロパティを使用して、列プロパティを設定する方法を示します。 これらのプロパティはコレクションを表現しており、オブジェクトの名前を指定するパラメーターと共に使用すれば、特定のオブジェクトを識別するために使用できます。 <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> コレクション オブジェクト プロパティには、名前とスキーマが必要です。  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Modify a property using the Databases, Tables, and Columns collections to reference a column.   
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("LastName").Nullable = true;   
//Call the Alter method to make the change on the instance of SQL Server.   
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("LastName").Alter();   
}  
```  
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-basic"></a>Visual Basic でのコレクションのメンバーの反復処理  
 このコード例では、<xref:Microsoft.AnalysisServices.Server.Databases%2A> コレクション プロパティを反復処理し、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスへのすべてのデータベース接続を表示します。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCollections2](SMO How to#SMO_VBCollections2)]  -->  
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-c"></a>Visual C# でのコレクションのメンバーの反復処理  
 このコード例では、<xref:Microsoft.AnalysisServices.Server.Databases%2A> コレクション プロパティを反復処理し、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスへのすべてのデータベース接続を表示します。  
  
```  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
int count = 0;   
int total = 0;   
//Iterate through the databases and call the GetActiveDBConnectionCount method.   
Database db = default(Database);   
foreach ( db in srv.Databases) {   
  count = srv.GetActiveDBConnectionCount(db.Name);   
  total = total + count;   
  //Display the number of connections for each database.   
  Console.WriteLine(count + " connections on " + db.Name);   
}   
//Display the total number of connections on the instance of SQL Server.   
Console.WriteLine("Total connections =" + total);   
}   
```  
  
  
