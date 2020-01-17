---
title: シノニムの使用 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- synonyms [SMO]
ms.assetid: db0a9022-9549-43e5-b6b3-deb236f05fb8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a96f6ee89b920ec668af21ce625694fc31ce13bd
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72781866"
---
# <a name="using-synonyms"></a>シノニムの使用
  シノニムは、スキーマ スコープ オブジェクトの別名です。 SMO では、シノニムは <xref:Microsoft.SqlServer.Management.Smo.Synonym> オブジェクトで表現します。 <xref:Microsoft.SqlServer.Management.Smo.Synonym> オブジェクトは、<xref:Microsoft.SqlServer.Management.Smo.Database> オブジェクトの子です。 これは、シノニムは、そのシノニムが定義されているデータベースのスコープ内でのみ有効であることを意味しています。 ただし、シノニムは、別のデータベース上または [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のリモート インスタンス上のオブジェクトを参照することができます。  
  
 別名を持つオブジェクトは、ベース オブジェクトと呼ばれます。 <xref:Microsoft.SqlServer.Management.Smo.Synonym> オブジェクトの名前プロパティは、ベース オブジェクトの別名です。  
  
## <a name="example"></a>例  
 次のコード例では、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual studio .net での VISUAL BASIC SMO プロジェクトの作成](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)」および「visual [studio .Net での Visual C&#35; SMO プロジェクトの作成](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="creating-a-synonym-in-visual-basic"></a>Visual Basic でのシノニムの作成  
 このコード例では、シノニム、またはスキーマ スコープ オブジェクトの別名を作成する方法を示します。 クライアント アプリケーションは、マルチパート名を使用してベース オブジェクトを参照するのではなく、シノニムを使用することによって、ベース オブジェクトの単一参照を使用することができます。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBSynonyms1](SMO How to#SMO_VBSynonyms1)]  -->  
  
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
  
$syn = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Synonym -ArgumentList $db, "Shop", "Sales"  
  
#Specify the base object, which is the object on which the synonym is based.  
$syn.BaseDatabase = "AdventureWorks2012"  
$syn.BaseSchema = "Sales"  
$syn.BaseObject = "Store"  
$syn.BaseServer = $srv.Name  
  
#Create the synonym on the instance of SQL Server.  
$syn.Create()  
```  
  
## <a name="see-also"></a>「  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-synonym-transact-sql)  
