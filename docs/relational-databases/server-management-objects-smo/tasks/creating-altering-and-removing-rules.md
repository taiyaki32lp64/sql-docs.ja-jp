---
title: ルールの作成、変更、および削除
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- rules [SMO]
ms.assetid: 16981459-524e-4b39-a899-4370eaf763cc
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b2f918e611a4bc88c1a77ad7d539a9101f3f8dac
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095526"
---
# <a name="creating-altering-and-removing-rules"></a>ルールの作成、変更、および削除
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  SMO では、<xref:Microsoft.SqlServer.Management.Smo.Rule> オブジェクトでルールが表現されます。 ルールは、<xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> プロパティによって定義されます。このプロパティは、IN、LIKE、または BETWEEN などの演算子や述語を使用した条件式を格納したテキスト文字列です。 ルールでは、列や別のデータベース オブジェクトを参照することはできません。 データベース オブジェクトを参照しない組み込み関数は含めることができます。  
  
 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> プロパティでの定義には、入力されたデータ値を参照する変数が含まれている必要があります。 ルールを作成するときに、任意の名前またはシンボルを使用して値を表すことができますが、最初の文字は \@ 記号である必要があります。  
  
## <a name="example"></a>例  
 提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual Studio&#35; .Net での Visual C SMO プロジェクトの作成](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-basic"></a>Visual Basic でのルールの作成、変更、および削除  
 このコード例では、ルールの作成、作成したルールの列へのアタッチ、<xref:Microsoft.SqlServer.Management.Smo.Rule> オブジェクトのプロパティの修正、列からのデタッチ、および削除を行う方法を示します。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Rule> オブジェクトの**Dim**ステートメントは、System. Data アセンブリ内の <xref:Microsoft.SqlServer.Management.Smo.Rule> オブジェクトがあいまいになるのを避けるために、完全なアセンブリパスで指定されます。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Declare a Table object variable and reference the Product table.
Dim tb As Table
tb = db.Tables("Product", "Production")
'Define a Rule object variable by supplying the parent database, name and schema in the constructor. 
'Note that the full namespace must be given for the Rule type to differentiate it from other Rule types.
Dim ru As Microsoft.SqlServer.Management.Smo.Rule
ru = New Rule(db, "TestRule", "Production")
'Set the TextHeader and TextBody properties to define the rule.
ru.TextHeader = "CREATE RULE [Production].[TestRule] AS"
ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())"
'Create the rule on the instance of SQL Server.
ru.Create()
'Bind the rule to a column in the Product table by supplying the table, schema, and 
'column as arguments in the BindToColumn method.
ru.BindToColumn("Product", "SellEndDate", "Production")
'Unbind from the column before removing the rule from the database.
ru.UnbindFromColumn("Product", "SellEndDate", "Production")
ru.Drop()
```
  
## <a name="creating-altering-and-removing-a-rule-in-visual-c"></a>Visual C# でのルールの作成、変更、および削除  
 このコード例では、ルールの作成、作成したルールの列へのアタッチ、<xref:Microsoft.SqlServer.Management.Smo.Rule> オブジェクトのプロパティの修正、列からのデタッチ、および削除を行う方法を示します。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Rule> オブジェクトの**Dim**ステートメントは、System. Data アセンブリ内の <xref:Microsoft.SqlServer.Management.Smo.Rule> オブジェクトがあいまいになるのを避けるために、完全なアセンブリパスで指定されます。  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Rule object variable by supplying the parent database, name and schema in the constructor.   
            //Note that the full namespace must be given for the Rule type to differentiate it from other Rule types.   
            Microsoft.SqlServer.Management.Smo.Rule ru;  
            ru = new Rule(db, "TestRule", "Production");  
            //Set the TextHeader and TextBody properties to define the rule.   
            ru.TextHeader = "CREATE RULE [Production].[TestRule] AS";  
            ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())";  
            //Create the rule on the instance of SQL Server.   
            ru.Create();  
            //Bind the rule to a column in the Product table by supplying the table, schema, and   
            //column as arguments in the BindToColumn method.   
            ru.BindToColumn("Product", "SellEndDate", "Production");  
            //Unbind from the column before removing the rule from the database.   
            ru.UnbindFromColumn("Product", "SellEndDate", "Production");  
            ru.Drop();  
  
        }  
```  
  
## <a name="creating-altering-and-removing-a-rule-in-powershell"></a>PowerShell でのルールの作成、変更、および削除  
 このコード例では、ルールの作成、作成したルールの列へのアタッチ、<xref:Microsoft.SqlServer.Management.Smo.Rule> オブジェクトのプロパティの修正、列からのデタッチ、および削除を行う方法を示します。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Rule> オブジェクトの**Dim**ステートメントは、System. Data アセンブリ内の <xref:Microsoft.SqlServer.Management.Smo.Rule> オブジェクトがあいまいになるのを避けるために、完全なアセンブリパスで指定されます。  
  
```powershell   
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a Rule object variable by supplying the parent database, name and schema in the constructor.   
$ru = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Rule `  
-argumentlist $db, "TestRule", "Production"  
  
#Set the TextHeader and TextBody properties to define the rule.   
$ru.TextHeader = "CREATE RULE [Production].[TestRule] AS"  
$ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())"  
  
#Create the rule on the instance of SQL Server.   
$ru.Create()  
  
# Bind the rule to a column in the Product table by supplying the table, schema, and   
# column as arguments in the BindToColumn method.   
$ru.BindToColumn("Product", "SellEndDate", "Production")  
  
#Unbind from the column before removing the rule from the database.   
$ru.UnbindFromColumn("Product", "SellEndDate", "Production")  
$ru.Drop()  
```  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.SqlServer.Management.Smo.Rule>  
  
  
