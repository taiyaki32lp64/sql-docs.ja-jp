---
title: 既定値の作成、変更、および削除
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- defaults [SMO]
ms.assetid: c30ac3b9-8150-4264-ba4c-c549f44261ab
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 17e7f0dd020004f0251fd470e42a591f926d7ce2
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74094642"
---
# <a name="creating-altering-and-removing-defaults"></a>既定値の作成、変更、および削除
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  SMO ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理オブジェクト) では、既定の制約は <xref:Microsoft.SqlServer.Management.Smo.Default> オブジェクトで表現します。  
  
 挿入する値を設定するには、<xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Default> プロパティを使用します。 挿入する値は、定数であっても、GETDATE() などの定数値を返す [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントであってもかまいません。 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> プロパティは、<xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> メソッドを使用して変更することはできません。 <xref:Microsoft.SqlServer.Management.Smo.Default> オブジェクトをいったん削除してから再作成する必要があります。  
  
## <a name="example"></a>例  
 提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual Studio&#35; .Net での Visual C SMO プロジェクトの作成](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="creating-altering-and-removing-a-default-in-visual-basic"></a>Visual Basic での既定値の作成、変更、および削除  
 このコード例では、シンプル テキストである既定値と [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントである別の既定値を作成する方法を示します。 既定値を列にアタッチするには <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> メソッドを使用し、列からのデタッチには <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A> メソッドを使用する必要があります。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a Default object variable by supplying the parent database and the default name 
'in the constructor.
Dim def As [Default]
def = New [Default](db, "Test_Default2")
'Set the TextHeader and TextBody properties that define the default.
def.TextHeader = "CREATE DEFAULT [Test_Default2] AS"
def.TextBody = "GetDate()"
'Create the default on the instance of SQL Server.
def.Create()
'Declare a Column object variable and reference a column in the AdventureWorks2012 database.
Dim col As Column
col = db.Tables("SpecialOffer", "Sales").Columns("StartDate")
'Bind the default to the column.
def.BindToColumn("SpecialOffer", "StartDate", "Sales")
'Unbind the default from the column and remove it from the database.
def.UnbindFromColumn("SpecialOffer", "StartDate", "Sales")
def.Drop()
```
  
## <a name="creating-altering-and-removing-a-default-in-visual-c"></a>Visual C# での既定値の作成、変更、および削除  
 このコード例では、シンプル テキストである既定値と [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントである別の既定値を作成する方法を示します。 既定値を列にアタッチするには <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> メソッドを使用し、列からのデタッチには <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A> メソッドを使用する必要があります。  
  
```csharp  
{  
  
          Server srv = new Server();  
  
            //Reference the AdventureWorks2012 database.   
            Database  db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Default object variable by supplying the parent database and the default name   
            //in the constructor.   
            Default def = new Default(db, "Test_Default2");  
  
            //Set the TextHeader and TextBody properties that define the default.   
            def.TextHeader = "CREATE DEFAULT [Test_Default2] AS";  
            def.TextBody = "GetDate()";  
  
            //Create the default on the instance of SQL Server.   
            def.Create();  
  
            //Bind the default to a column in a table in AdventureWorks2012  
            def.BindToColumn("SpecialOffer", "StartDate", "Sales");  
  
            //Unbind the default from the column and remove it from the database.   
            def.UnbindFromColumn("SpecialOffer", "StartDate", "Sales");  
            def.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-default-in-powershell"></a>PowerShell での既定値の作成、変更、および削除  
 このコード例では、シンプル テキストである既定値と [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントである別の既定値を作成する方法を示します。 既定値を列にアタッチするには <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> メソッドを使用し、列からのデタッチには <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A> メソッドを使用する必要があります。  
  
```powershell   
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
#Define a Default object variable by supplying the parent database and the default name in the constructor.  
$def = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Default `  
-argumentlist $db, "Test_Default2"  
  
#Set the TextHeader and TextBody properties that define the default.   
$def.TextHeader = "CREATE DEFAULT [Test_Default2] AS"  
$def.TextBody = "GetDate()"  
  
#Create the default on the instance of SQL Server.   
$def.Create()  
  
#Bind the default to the column.   
$def.BindToColumn("SpecialOffer", "StartDate", "Sales")  
  
#Unbind the default from the column and remove it from the database.   
$def.UnbindFromColumn("SpecialOffer", "StartDate", "Sales")  
$def.Drop()  
```  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.SqlServer.Management.Smo.Default>  
  
  
