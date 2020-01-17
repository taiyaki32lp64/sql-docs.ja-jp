---
title: データベースの作成、変更、および削除 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- databases [SMO]
- databases [SMO], creating
- databases [SMO], modifying
- databases [SMO], deleting
ms.assetid: fcfb3ec2-7556-4f72-971a-501295892cb0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 645ba8428dddb36de9a3edeb784d64f96b5c0603
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797040"
---
# <a name="creating-altering-and-removing-databases"></a>データベースの作成、変更、および削除
  SMO では、データベースは <xref:Microsoft.SqlServer.Management.Smo.Database> オブジェクトで表現されます。  
  
 修正または削除のために、<xref:Microsoft.SqlServer.Management.Smo.Database> オブジェクトを作成する必要はありません。 データベースは、コレクションを使用して参照することができます。  
  
## <a name="example"></a>例  
 提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual studio .net での VISUAL BASIC SMO プロジェクトの作成](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)」または「visual [studio .Net での Visual C&#35; SMO プロジェクトの作成](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="creating-altering-and-removing-a-database-in-visual-basic"></a>Visual Basic でのデータベースの作成、変更、および削除  
 このコード例では、新しいデータベースを作成します。 このデータベースに対し、ファイルおよびファイル グループが自動的に作成されます。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDatabase1](SMO How to#SMO_VBDatabase1)]  -->  
  
## <a name="creating-altering-and-removing-a-database-in-visual-c"></a>Visual C# でのデータベースの作成、変更、および削除  
 このコード例では、新しいデータベースを作成します。 このデータベースに対し、ファイルおよびファイル グループが自動的に作成されます。  
  
```csharp
{  
                //Connect to the local, default instance of SQL Server.   
                Server srv;  
                srv = new Server();  
                //Define a Database object variable by supplying the server and the database name arguments in the constructor.   
                Database db;  
                db = new Database(srv, "Test_SMO_Database");  
                //Create the database on the instance of SQL Server.   
                db.Create();  
                //Reference the database and display the date when it was created.   
                db = srv.Databases["Test_SMO_Database"];  
                Console.WriteLine(db.CreateDate);  
                //Remove the database.   
                db.Drop();  
            }  
```  
  
## <a name="creating-altering-and-removing-a-database-in-powershell"></a>PowerShell でのデータベースの作成、変更、および削除  
 このコード例では、新しいデータベースを作成します。 このデータベースに対し、ファイルおよびファイル グループが自動的に作成されます。  
  
```powershell
#Get a server object which corresponds to the default instance  
cd \sql\localhost\  
$srv = Get-Item default  
  
#Create a new database  
$db = New-Object -TypeName Microsoft.SqlServer.Management.Smo.Database -argumentlist $srv, "Test_SMO_Database"  
$db.Create()  
  
#Reference the database and display the date when it was created.
$db = $srv.Databases["Test_SMO_Database"]  
$db.CreateDate  
  
#Drop the database  
$db.Drop()  
```  
  
## <a name="see-also"></a>「  
 <xref:Microsoft.SqlServer.Management.Smo.Database>  
