---
title: プログラムによるタスクの追加 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- tasks [Integration Services], packages
- adding package tasks
ms.assetid: 5d4652d5-228c-4238-905c-346dd8503fdf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7357e1508172e5b4debbdea99967314c45d53bf4
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71299069"
---
# <a name="adding-tasks-programmatically"></a>プログラムによるタスクの追加

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  ランタイム エンジン内の次の種類のオブジェクトに、タスクを追加できます。  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Package>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Sequence>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.ForLoop>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>  
  
 これらのクラスはコンテナーと見なされ、すべて <xref:Microsoft.SqlServer.Dts.Runtime.IDTSSequence.Executables%2A> プロパティを継承します。 コンテナーにはタスクのコレクションを含めることができます。これらのタスクは、コンテナーの実行中にランタイムによって処理される実行可能オブジェクトです。 コレクション内のオブジェクトの実行順序は、コンテナー内の各タスクに設定された <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> によって決まります。 優先順位制約によって、コレクション内の <xref:Microsoft.SqlServer.Dts.Runtime.Executable> の成功、失敗、または完了に基づく、実行の分岐ができます。  
  
 各コンテナーには、個々の <xref:Microsoft.SqlServer.Dts.Runtime.Executables> オブジェクトを含んでいる <xref:Microsoft.SqlServer.Dts.Runtime.Executable> コレクションがあります。 各実行可能タスクは <xref:Microsoft.SqlServer.Dts.Runtime.Executable.Execute%2A> メソッドおよび <xref:Microsoft.SqlServer.Dts.Runtime.Executable.Validate%2A> メソッドを継承して実装します。 これらの 2 つのメソッドはランタイム エンジンによって呼び出され、各 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> を処理します。  
  
 パッケージにタスクを追加するには、<xref:Microsoft.SqlServer.Dts.Runtime.Executables> の既存のコレクションを持つコンテナーが必要です。 ほとんどの場合、コレクションに追加するタスクはパッケージです。 新しいタスクの実行可能ファイルをそのコンテナーのコレクションに追加するには、<xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A> メソッドを呼び出します。 このメソッドには単一の文字列パラメーターがあり、CLSID、PROGID、STOCK モニカー、または、追加するタスクの <xref:Microsoft.SqlServer.Dts.Runtime.TaskInfo.CreationName%2A> が格納されます。  
  
## <a name="task-names"></a>タスク名  
 名前または ID でタスクを指定できますが、<xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A> メソッドで最もよく使用されるパラメーターは **STOCK** モニカーです。 **STOCK** モニカーによって識別される実行可能ファイルにタスクを追加するには、次の構文を使用します。  
  
```csharp  
Executable exec = package.Executables.Add("STOCK:BulkInsertTask");  
  
```  
  
```vb  
Dim exec As Executable = package.Executables.Add("STOCK:BulkInsertTask")  
  
```  
  
 次の一覧は、**STOCK** モニカーの後に使用する各タスクの名前を示したものです。  
  
-   ActiveXScriptTask  
  
-   BulkInsertTask  
  
-   ExecuteProcessTask  
  
-   ExecutePackageTask  
  
-   Exec80PackageTask  
  
-   FileSystemTask  
  
-   FTPTask  
  
-   MSMQTask  
  
-   PipelineTask  
  
-   ScriptTask  
  
-   SendMailTask  
  
-   SQLTask  
  
-   TransferStoredProceduresTask  
  
-   TransferLoginsTask  
  
-   TransferErrorMessagesTask  
  
-   TransferJobsTask  
  
-   TransferObjectsTask  
  
-   TransferDatabaseTask  
  
-   WebServiceTask  
  
-   WmiDataReaderTask  
  
-   WmiEventWatcherTask  
  
-   XMLTask  
  
 明示的な構文を使用する場合、または追加しようとするタスクに STOCK モニカーがない場合は、長い名前を使用して実行可能ファイルにタスクを追加できます。 この構文では、タスクのバージョン番号も指定する必要があります。  
  
```csharp  
Executable exec = package.Executables.Add(  
  "Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask, " +  
  "Microsoft.SqlServer.ScriptTask, Version=10.0.000.0, " +  
  "Culture=neutral, PublicKeyToken=89845dcd8080cc91");  
```  
  
```vb  
Dim exec As Executable = package.Executables.Add( _  
  "Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask, " & _  
  "Microsoft.SqlServer.ScriptTask, Version=10.0.000.0, " & _  
  "Culture=neutral, PublicKeyToken=89845dcd8080cc91")  
```  
  
 タスクのバージョンを指定しないで、次の例のようにクラスの **AssemblyQualifiedName** プロパティを使用して、プログラムによってタスクの長い名前を取得できます。 この例では、Microsoft.SqlServer.SQLTask アセンブリへの参照が必要です。  
  
```csharp  
using Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask;  
...  
      Executable exec = package.Executables.Add(  
        typeof(Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask.ExecuteSQLTask).AssemblyQualifiedName);  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask  
...  
    Dim exec As Executable = package.Executables.Add( _  
      GetType(Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask.ExecuteSQLTask).AssemblyQualifiedName)  
```  
  
 次のコード例は、新しいパッケージから <xref:Microsoft.SqlServer.Dts.Runtime.Executables> コレクションを作成し、**STOCK** モニカーを使用してファイル システム タスクと一括挿入タスクをコレクションに追加する方法を示しています。 この例では、Microsoft.SqlServer.FileSystemTask および Microsoft.SqlServer.BulkInsertTask アセンブリへの参照が必要です。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Tasks.FileSystemTask;  
using Microsoft.SqlServer.Dts.Tasks.BulkInsertTask;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
      // Add a File System task to the package.  
      Executable exec1 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileSystemTask = exec1 as TaskHost;  
      // Add a Bulk Insert task to the package.  
      Executable exec2 = p.Executables.Add("STOCK:BulkInsertTask");  
      TaskHost thBulkInsertTask = exec2 as TaskHost;  
  
      // Iterate through the package Executables collection.  
      Executables pExecs = p.Executables;  
      foreach (Executable pExec in pExecs)  
      {  
        TaskHost taskHost = (TaskHost)pExec;  
        Console.WriteLine("Type {0}", taskHost.InnerObject.ToString());  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Tasks.FileSystemTask  
Imports Microsoft.SqlServer.Dts.Tasks.BulkInsertTask  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    ' Add a File System task to the package.  
    Dim exec1 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileSystemTask As TaskHost = CType(exec1, TaskHost)  
    ' Add a Bulk Insert task to the package.  
    Dim exec2 As Executable = p.Executables.Add("STOCK:BulkInsertTask")  
    Dim thBulkInsertTask As TaskHost = CType(exec2, TaskHost)  
  
    ' Iterate through the package Executables collection.  
    Dim pExecs As Executables = p.Executables  
    Dim pExec As Executable  
    For Each pExec In pExecs  
      Dim taskHost As TaskHost = CType(pExec, TaskHost)  
      Console.WriteLine("Type {0}", taskHost.InnerObject.ToString())  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **サンプル出力:**  
  
 `Type Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask`  
  
 `Type Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask`  
  
## <a name="taskhost-container"></a>TaskHost コンテナー  
 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> クラスは、グラフィカル ユーザー インターフェイスには出現しないコンテナーですが、プログラムを作成する際には非常に重要です。 このクラスは、すべてのタスク用のラッパーです。 <xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A> メソッドを <xref:Microsoft.SqlServer.Dts.Runtime.Executable> オブジェクトとして使用してパッケージに追加されたタスクは、<xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> オブジェクトとしてキャストできます。 タスクが <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> としてキャストされる場合は、タスクの追加プロパティおよびメソッドを使用できます。 また、タスク自体には、<xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.InnerObject%2A> の <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> プロパティをとおしてアクセスできます。 必要に応じて、タスクを <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> オブジェクトとして保持し、<xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> コレクションをとおしてタスクのプロパティを使用することができます。 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> を使用する利点は、汎用性の高いコードを記述できることです。 タスク固有のコードが必要な場合は、タスクを適切なオブジェクトにキャストする必要があります。  
  
 次のコード例は、<xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> を含む <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask>、thBulkInsertTask を <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask> オブジェクトにキャストする方法を示しています。  
  
```csharp  
BulkInsertTask myTask = thBulkInsertTask.InnerObject as BulkInsertTask;  
```  
  
```vb  
Dim myTask As BulkInsertTask = CType(thBulkInsertTask.InnerObject, BulkInsertTask)  
```  
  
 次のコード例は、実行可能ファイルを <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> にキャストし、次に <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.InnerObject%2A> プロパティを使用して、ホストに含まれている実行可能ファイルの種類を特定する方法を示しています。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Tasks.FileSystemTask;  
using Microsoft.SqlServer.Dts.Tasks.BulkInsertTask;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
      // Add a File System task to the package.  
      Executable exec1 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileSystemTask1 = exec1 as TaskHost;  
      // Add a Bulk Insert task to the package.  
      Executable exec2 = p.Executables.Add("STOCK:BulkInsertTask");  
      TaskHost thFileSystemTask2 = exec2 as TaskHost;  
  
      // Iterate through the package Executables collection.  
      Executables pExecs = p.Executables;  
      foreach (Executable pExec in pExecs)  
      {  
        TaskHost taskHost = (TaskHost)pExec;  
        if (taskHost.InnerObject is Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask)  
        {  
          // Do work with FileSystemTask here.  
          Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString());  
        }  
        else if (taskHost.InnerObject is Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask)  
        {  
          // Do work with BulkInsertTask here.  
          Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString());  
        }  
        // Add additional statements to check InnerObject, if desired.  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Tasks.FileSystemTask  
Imports Microsoft.SqlServer.Dts.Tasks.BulkInsertTask  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    ' Add a File System task to the package.  
    Dim exec1 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileSystemTask1 As TaskHost = CType(exec1, TaskHost)  
    ' Add a Bulk Insert task to the package.  
    Dim exec2 As Executable = p.Executables.Add("STOCK:BulkInsertTask")  
    Dim thFileSystemTask2 As TaskHost = CType(exec2, TaskHost)  
  
    ' Iterate through the package Executables collection.  
    Dim pExecs As Executables = p.Executables  
    Dim pExec As Executable  
    For Each pExec In pExecs  
      Dim taskHost As TaskHost = CType(pExec, TaskHost)  
      If TypeOf taskHost.InnerObject Is Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask Then  
        ' Do work with FileSystemTask here.  
        Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString())  
      ElseIf TypeOf taskHost.InnerObject Is Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask Then  
        ' Do work with BulkInsertTask here.  
        Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString())  
      End If  
      ' Add additional statements to check InnerObject, if desired.  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **サンプル出力:**  
  
 `Found task of type Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask`  
  
 `Found task of type Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask`  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A> ステートメントは、新しく作成された <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> オブジェクトから <xref:Microsoft.SqlServer.Dts.Runtime.Executable> オブジェクトにキャストされる実行可能ファイルを返します。  
  
 新しいオブジェクトのプロパティの設定またはメソッドの呼び出しを行う場合、2 つのオプションを使用できます。  
  
1.  <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> の <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> コレクションを使用します。 たとえば、オブジェクトからプロパティを取得するには、`th.Properties["propertyname"].GetValue(th))` を使用します。 プロパティを設定するには、`th.Properties["propertyname"].SetValue(th, <value>);` を使用します。  
  
2.  <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.InnerObject%2A> の <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> をタスク クラスにキャストします。 たとえば、一括挿入タスクが <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask> としてパッケージに追加され、その後 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> にキャストされた後で、このタスクを <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> にキャストするには、`BulkInsertTask myTask = th.InnerObject as BulkInsertTask;` を使用します。  
  
 タスク固有のクラスにキャストする代わりに <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> クラスをコードで使用する場合、次の利点があります。  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> プロバイダーは、コード内でアセンブリを参照する必要がありません。  
  
-   コンパイル時にタスクの名前を知る必要がないため、すべてのタスクで動作する汎用ルーチンをコーディングできます。 このような汎用ルーチンには、タスク名を引数として受け取るメソッドが含まれます。このメソッド コードはすべてのタスクで動作します。 これは、テスト コードを記述するのに適したメソッドです。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> からタスク固有のクラスにキャストする場合、次の利点があります。  
  
-   Visual Studio プロジェクトからステートメントの完了が提供されます (IntelliSense)。  
  
-   コードの実行が高速化する場合があります。  
  
-   タスク固有のオブジェクトを使用すると、事前バインドおよび結果の最適化が有効になります。 事前バインドおよび遅延バインドの詳細については、「Visual Basic 言語の概念」の「事前バインドと遅延バインド」を参照してください。  
  
 次のコード例は、タスク コードの再利用の概念について、詳細を示しています。 このコード例では、タスクを同等のクラスにキャストせず、代わりに実行可能ファイルを <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> にキャストしてから、<xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> を使用してすべてのタスクに対する汎用コードを記述する方法を示しています。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package package = new Package();  
  
      string[] tasks = { "STOCK:SQLTask", "STOCK:ScriptTask",   
        "STOCK:ExecuteProcessTask", "STOCK:PipelineTask",   
        "STOCK:FTPTask", "STOCK:SendMailTask", "STOCK:MSMQTask" };  
  
      foreach (string s in tasks)  
      {  
        TaskHost taskhost = package.Executables.Add(s) as TaskHost;  
        DtsProperties props = taskhost.Properties;  
        Console.WriteLine("Enumerating properties on " + taskhost.Name);  
        Console.WriteLine(" TaskHost.InnerObject is " + taskhost.InnerObject.ToString());  
        Console.WriteLine();  
  
        foreach (DtsProperty prop in props)  
        {  
          Console.WriteLine("Properties for " + prop.Name);  
          Console.WriteLine("Name : " + prop.Name);  
          Console.WriteLine("Type : " + prop.Type.ToString());  
          Console.WriteLine("Readable : " + prop.Get.ToString());  
          Console.WriteLine("Writable : " + prop.Set.ToString());  
          Console.WriteLine();  
        }  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Package = New Package()  
  
    Dim tasks() As String = New String() {"STOCK:SQLTask", "STOCK:ScriptTask", _  
              "STOCK:ExecuteProcessTask", "STOCK:PipelineTask", _  
              "STOCK:FTPTask", "STOCK:SendMailTask", "STOCK:MSMQTask"}  
  
    For Each s As String In tasks  
  
      Dim taskhost As TaskHost = CType(package.Executables.Add(s), TaskHost)  
      Dim props As DtsProperties = taskhost.Properties  
      Console.WriteLine("Enumerating properties on " & taskhost.Name)  
      Console.WriteLine(" TaskHost.InnerObject is " & taskhost.InnerObject.ToString())  
      Console.WriteLine()  
  
      For Each prop As DtsProperty In props  
        Console.WriteLine("Properties for " + prop.Name)  
        Console.WriteLine(" Name : " + prop.Name)  
        Console.WriteLine(" Type : " + prop.Type.ToString())  
        Console.WriteLine(" Readable : " + prop.Get.ToString())  
        Console.WriteLine(" Writable : " + prop.Set.ToString())  
        Console.WriteLine()  
      Next  
  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
## <a name="external-resources"></a>外部リソース  
 blogs.msdn.com のブログ「[EzAPI - Updated for SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=243223)」(EzAPI - SQL Server 2012 用の更新)  

## <a name="see-also"></a>参照  
 [プログラムによるタスクの接続](../../integration-services/building-packages-programmatically/connecting-tasks-programmatically.md)  
  
  
