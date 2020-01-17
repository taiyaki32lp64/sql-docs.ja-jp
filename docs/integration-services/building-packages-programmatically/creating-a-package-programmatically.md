---
title: プログラムを使用したパッケージ作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SSIS packages, creating
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
ms.assetid: e44bcc70-32d3-43e8-a84b-29aef819d5d3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6d81c961600eca7dddd1ecd5995dbb488094aafb
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294925"
---
# <a name="creating-a-package-programmatically"></a>プログラムを使用したパッケージ作成

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  <xref:Microsoft.SqlServer.Dts.Runtime.Package> オブジェクトは、[!INCLUDE[ssIS](../../includes/ssis-md.md)] プロジェクトによるソリューションで、他のすべてのオブジェクトの上位に位置するコンテナーです。 パッケージは、トップレベルのコンテナーとして、最初に作成されるオブジェクトです。それ以降のオブジェクトはパッケージに追加され、パッケージのコンテキスト内で実行されます。 パッケージ自体は、データの移動または変換を行いません。 パッケージは、格納しているタスクに依存して作業を実行します。 タスクは、パッケージが実行する作業のほとんどを実行し、パッケージの機能を定義します。 パッケージを作成して実行するには、わずか 3 行のコードを必要とするだけですが、さまざまなタスクおよび <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> オブジェクトをパッケージに追加して、機能を追加できます。 このセクションでは、プログラムによってパッケージを作成する方法について説明します。 タスクまたは <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> の作成方法についての説明は行いません。 これらについては、後のセクションで説明します。  
  
## <a name="example"></a>例  
 Visual Studio IDE を使用してコードを記述するには、Microsoft.SqlServer.Dts.Runtime に対して `using` ステートメント (Visual Basic .NET では `Imports`) を作成するために、Microsoft.SqlServer.ManagedDTS.DLL を参照する必要があります。 次のコード例では、空のパッケージを作成しています。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package package;  
      package = new Package();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Package  
    package = New Package  
  
  End Sub  
  
End Module  
```  
  
 サンプルをコンパイルして実行するには、Visual Studio で F5 キーを押します。 C# コンパイラ **csc.exe** を使用してコードを作成し、コマンド プロンプトからコンパイルするには、次のコマンドおよびファイル参照を使用します。 *\<filename>* は .cs または .vb ファイルの名前に置き換えて、任意の *\<outputfilename>* を付けます。  
  
 **csc /target:library /out: \<outputfilename>.dll \<filename>.cs /r:Microsoft.SqlServer.Managed DTS.dll" /r:System.dll**  
  
 Visual Basic .NET コンパイラ **vbc.exe** を使用してコードを作成し、コマンド プロンプトからコンパイルするには、次のコマンドおよびファイル参照を使用します。  
  
 **vbc /target:library /out: \<outputfilename>.dll \<filename>.vb /r:Microsoft.SqlServer.Managed DTS.dll" /r:System.dll**  
  
 また、ディスク上、ファイル システム、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に保存されている既存のパッケージを読み込むことにより、パッケージを作成することもできます。 その場合、<xref:Microsoft.SqlServer.Dts.Runtime.Application> オブジェクトが最初に作成され、そのパッケージ オブジェクトが、オーバーロードされた次のアプリケーションのメソッドのいずれかによって設定される点が異なります。そのメソッドとは、フラット ファイル用の **LoadPackage**、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に保存されているパッケージ用の **LoadFromSQLServer**、またはファイル システムに保存されているパッケージ用の <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A> です。 次の例では、ディスクから既存のパッケージを読み込み、パッケージの複数のプロパティを表示します。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class ApplicationTests  
  {  
    static void Main(string[] args)  
    {  
      // The variable pkg points to the location of the  
      // ExecuteProcess package sample that was installed with  
      // the SSIS samples.  
      string pkg = @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\ExecuteProcess Sample\ExecuteProcess\UsingExecuteProcess.dtsx";  
  
      Application app = new Application();  
      Package p = app.LoadPackage(pkg, null);  
  
      // Now that the package is loaded, we can query on  
      // its properties.  
      int n = p.Configurations.Count;  
      DtsProperty p2 = p.Properties["VersionGUID"];  
      DTSProtectionLevel pl = p.ProtectionLevel;  
  
      Console.WriteLine("Number of configurations = " + n.ToString());  
      Console.WriteLine("VersionGUID = " + (string)p2.GetValue(p));  
      Console.WriteLine("ProtectionLevel = " + pl.ToString());  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module ApplicationTests  
  
  Sub Main()  
  
    ' The variable pkg points to the location of the  
    ' ExecuteProcess package sample that was installed with  
    ' the SSIS samples.  
    Dim pkg As String = _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\ExecuteProcess Sample\ExecuteProcess\UsingExecuteProcess.dtsx"  
  
    Dim app As Application = New Application()  
    Dim p As Package = app.LoadPackage(pkg, Nothing)  
  
    ' Now that the package is loaded, we can query on  
    ' its properties.  
    Dim n As Integer = p.Configurations.Count  
    Dim p2 As DtsProperty = p.Properties("VersionGUID")  
    Dim pl As DTSProtectionLevel = p.ProtectionLevel  
  
    Console.WriteLine("Number of configurations = " & n.ToString())  
    Console.WriteLine("VersionGUID = " & CType(p2.GetValue(p), String))  
    Console.WriteLine("ProtectionLevel = " & pl.ToString())  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **サンプル出力:**  
  
 `Number of configurations = 2`  
  
 `VersionGUID = {09016682-89B8-4406-AAC9-AF1E527FF50F}`  
  
 `ProtectionLevel = DontSaveSensitive`  
  
## <a name="external-resources"></a>外部リソース  
  
-   blogs.msdn.com のブログ「[API Sample - OleDB source and OleDB destination](https://go.microsoft.com/fwlink/?LinkId=220824)」(API サンプル – OleDB ソースと OleDB 変換先)  
  
-   blogs.msdn.com のブログ「[EzAPI - Updated for SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=243223)」(EzAPI - SQL Server 2012 用の更新)  
  
## <a name="see-also"></a>参照  
 [プログラムによるタスクの追加](../../integration-services/building-packages-programmatically/adding-tasks-programmatically.md)  
  
  
