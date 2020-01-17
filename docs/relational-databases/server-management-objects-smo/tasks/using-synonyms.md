---
title: シノニムの使用 |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- synonyms [SMO]
ms.assetid: db0a9022-9549-43e5-b6b3-deb236f05fb8
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4da1cefbb07186134a1c6f14c335a2aacc507f6d
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2019
ms.locfileid: "70148307"
---
# <a name="using-synonyms"></a>シノニムの使用
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  シノニムは、スキーマ スコープ オブジェクトの別名です。 SMO では、シノニムは <xref:Microsoft.SqlServer.Management.Smo.Synonym> オブジェクトで表現します。 <xref:Microsoft.SqlServer.Management.Smo.Synonym> オブジェクトは、<xref:Microsoft.SqlServer.Management.Smo.Database> オブジェクトの子です。 これは、シノニムは、そのシノニムが定義されているデータベースのスコープ内でのみ有効であることを意味しています。 ただし、シノニムは、別のデータベース上または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のリモート インスタンス上のオブジェクトを参照することができます。  
  
 別名を持つオブジェクトは、ベース オブジェクトと呼ばれます。 <xref:Microsoft.SqlServer.Management.Smo.Synonym> オブジェクトの名前プロパティは、ベース オブジェクトの別名です。  
  
## <a name="example"></a>例  
 次のコード例では、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual Studio&#35; .Net での Visual C SMO プロジェクトの作成](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="creating-a-synonym-in-visual-c"></a>Visual C# でのシノニムの作成  
 このコード例では、シノニム、またはスキーマ スコープ オブジェクトの別名を作成する方法を示します。 クライアント アプリケーションは、マルチパート名を使用してベース オブジェクトを参照するのではなく、シノニムを使用することによって、ベース オブジェクトの単一参照を使用することができます。  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
  
            //Reference the AdventureWorks2012 database.   
            Database db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Synonym object variable by supplying the   
            //parent database, name, and schema arguments in the constructor.   
            //The name is also a synonym of the name of the base object.   
            Synonym syn = new Synonym(db, "Shop", "Sales");  
  
            //Specify the base object, which is the object on which   
            //the synonym is based.   
            syn.BaseDatabase = "AdventureWorks2012";  
            syn.BaseSchema = "Sales";  
            syn.BaseObject = "Store";  
            syn.BaseServer = srv.Name;  
  
            //Create the synonym on the instance of SQL Server.   
            syn.Create();  
        }  
```  
  
## <a name="creating-a-synonym-in-powershell"></a>PowerShell でのシノニムの作成  
 このコード例では、シノニム、またはスキーマ スコープ オブジェクトの別名を作成する方法を示します。 クライアント アプリケーションは、マルチパート名を使用してベース オブジェクトを参照するのではなく、シノニムを使用することによって、ベース オブジェクトの単一参照を使用することができます。  
  
```powershell  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#And the database object corresponding to Adventureworks  
$db = $srv.Databases["AdventureWorks2012"]  
  
$syn = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Synonym `  
-argumentlist $db, "Shop", "Sales"  
  
#Specify the base object, which is the object on which the synonym is based.  
$syn.BaseDatabase = "AdventureWorks2012"  
$syn.BaseSchema = "Sales"  
$syn.BaseObject = "Store"  
$syn.BaseServer = $srv.Name  
  
#Create the synonym on the instance of SQL Server.  
$syn.Create()  
```  
  
## <a name="see-also"></a>参照  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](../../../t-sql/statements/create-synonym-transact-sql.md)  
  
  
