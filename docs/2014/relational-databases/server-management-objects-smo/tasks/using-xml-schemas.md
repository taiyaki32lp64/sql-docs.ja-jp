---
title: XML スキーマの使用 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- XML [SMO]
ms.assetid: 9d04de01-efeb-4b2d-8c28-3234bc7ff2f3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6aee91cdab8ff5404ebb333a81cad91297a99f17
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72781941"
---
# <a name="using-xml-schemas"></a>XML スキーマの使用方法
  SMO で使用できる XML プログラミングの機能は、XML データ型や XML 名前空間の提供、および XML データ型の列での簡易インデックス作成に限定されています。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、XML ドキュメントインスタンスのネイティブストレージが用意されています。 XML スキーマを使用すると、複雑な XML データ型を定義することができます。これを使用して、XML ドキュメントを検証し、データの整合性を確保することができます。 XML スキーマは、<xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> オブジェクトで定義します。  
  
## <a name="example"></a>例  
 提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual studio .net での VISUAL BASIC SMO プロジェクトの作成](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)」または「visual [studio .Net での Visual C&#35; SMO プロジェクトの作成](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="creating-an-xml-schema-in-visual-basic"></a>Visual Basic での XML スキーマの作成  
 このコード例では、<xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> オブジェクトを使用して XML スキーマを作成する方法を示します。 XML スキーマ コレクションを定義する <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A> プロパティは、複数の二重引用符記号を格納しています。 これらは `chr(34)` 文字列に置き換えられます。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBXMLSchema1](SMO How to#SMO_VBXMLSchema1)]  -->  
  
## <a name="creating-an-xml-schema-in-visual-c"></a>Visual C# での XML スキーマの作成  
 このコード例では、<xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> オブジェクトを使用して XML スキーマを作成する方法を示します。 XML スキーマ コレクションを定義する <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A> プロパティは、複数の二重引用符記号を格納しています。 これらは `chr(34)` 文字列に置き換えられます。  
  
```csharp
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = default(Server);  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define an XmlSchemaCollection object by supplying the parent  
            // database and name arguments in the constructor.   
            XmlSchemaCollection xsc = default(XmlSchemaCollection);  
            xsc = new XmlSchemaCollection(db, "MySampleCollection");  
            xsc.Text = "<schema xmlns=" + Strings.Chr(34) + "http://www.w3.org/2001/XMLSchema" + Strings.Chr(34) + " xmlns:ns=" + Strings.Chr(34) + "http://ns" + Strings.Chr(34) + "><element name=" + Strings.Chr(34) + "e" + Strings.Chr(34) + " type=" + Strings.Chr(34) + "dateTime" + Strings.Chr(34) + "/></schema>";  
            //Create the XML schema collection on the instance of SQL Server.   
            xsc.Create();  
        }  
```  
  
## <a name="creating-an-xml-schema-in-powershell"></a>PowerShell での XML スキーマの作成  
 このコード例では、<xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> オブジェクトを使用して XML スキーマを作成する方法を示します。 XML スキーマ コレクションを定義する <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A> プロパティは、複数の二重引用符記号を格納しています。 これらは `chr(34)` 文字列に置き換えられます。  
  
```powershell
#Get a server object which corresponds to the default instance replace LocalMachine with the physical server  
cd \sql\LocalHost  
$srv = Get-Item default  
  
#Reference the AdventureWorks database.  
$db = $srv.Databases["AdventureWorks2012"]  
  
#Create a new schema collection  
$xsc = New-Object -TypeName Microsoft.SqlServer.Management.SMO.XmlSchemaCollection `  
-argumentlist $db,"MySampleCollection"  
  
#Add the xml  
$dq = '"' # the double quote character  
$xsc.Text = "<schema xmlns=" + $dq + "http://www.w3.org/2001/XMLSchema" + $dq + `  
"  xmlns:ns=" + $dq + "http://ns" + $dq + "><element name=" + $dq + "e" + $dq +`  
 " type=" + $dq + "dateTime" + $dq + "/></schema>"  
  
#Create the XML schema collection on the instance of SQL Server.  
$xsc.Create()  
```  
