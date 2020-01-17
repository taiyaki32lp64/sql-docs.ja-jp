---
title: プログラムによるイベントの処理 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Integration Services packages, events
- SQL Server Integration Services packages, events
- SSIS events, programmatically handling
- packages [Integration Services], events
- DtsEventHandler object
- SSIS packages, events
- SSIS events
- events [Integration Services], programmatically
- tasks [Integration Services], events
- IDTSEvents interface
ms.assetid: 0f00bd66-efd5-4f12-9e1c-36195f739332
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8e0417ddf5c4c09cfffa07b7b76918a89622aec6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771808"
---
# <a name="handling-events-programmatically"></a>プログラムによるイベントの処理
  [!INCLUDE[ssIS](../../includes/ssis-md.md)] のランタイムには、パッケージの検証や実行の処理前、処理中、処理後に発生する一連のイベントがあります。 これらのイベントをキャプチャするには、次の 2 つの方法があります。 1 つは、あるクラスに <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> インターフェイスを実装し、このクラスをパラメーターとして、パッケージの `Execute` メソッドおよび `Validate` メソッドに渡す方法です。 もう 1 つは <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> オブジェクトを作成する方法です。このオブジェクトには、タスクやループなど、<xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> に属するイベントが発生したときに実行される、他の [!INCLUDE[ssIS](../../includes/ssis-md.md)] オブジェクトを含めることができます。 ここでは、この 2 つの方法について説明し、その使用法をコード例で示します。  
  
## <a name="receiving-idtsevents-callbacks"></a>IDTSEvents コールバックの受信  
 プログラムによってパッケージを構築し、実行する開発者は、<xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> インターフェイスを使用して、検証中や実行中に発生したイベント通知を受信することができます。 これを行うには、<xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> インターフェイスを実装したクラスを作成し、このクラスをパラメーターとして、パッケージの `Validate` メソッドおよび `Execute` メソッドに渡します。 イベントが発生すると、ランタイム エンジンによってこのクラスのメソッドが呼び出されます。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> クラスにはあらかじめ <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> インターフェイスが実装されています。したがって、<xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> インターフェイスを直接実装する代わりに、<xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> から派生するクラスを作成し、応答を受ける特定のイベントをオーバーライドする方法を取ることもできます。 その後、このクラスをパラメーターとして、<xref:Microsoft.SqlServer.Dts.Runtime.Package> の `Validate` メソッドおよび `Execute` メソッドに渡し、イベントのコールバックを受け取ります。  
  
 次のコード サンプルは、<xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> から派生するクラスを示し、<xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnPreExecute%2A> メソッドをオーバーライドします。 クラスをパラメーターとして指定、`Validate`と`Execute`パッケージのメソッド。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
      MyEventsClass eventsClass = new MyEventsClass();  
  
      p.Validate(null, null, eventsClass, null);  
      p.Execute(null, null, eventsClass, null, null);  
  
      Console.Read();  
    }  
  }  
  class MyEventsClass : DefaultEvents  
  {  
    public override void OnPreExecute(Executable exec, ref bool fireAgain)  
    {  
      // TODO: Add custom code to handle the event.  
      Console.WriteLine("The PreExecute event of the " +  
        exec.ToString() + " has been raised.");  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    Dim eventsClass As MyEventsClass = New MyEventsClass()  
  
    p.Validate(Nothing, Nothing, eventsClass, Nothing)  
    p.Execute(Nothing, Nothing, eventsClass, Nothing, Nothing)  
  
    Console.Read()  
  
  End Sub  
  
End Module  
  
Class MyEventsClass  
  Inherits DefaultEvents  
  
  Public Overrides Sub OnPreExecute(ByVal exec As Executable, ByRef fireAgain As Boolean)  
  
    ' TODO: Add custom code to handle the event.  
    Console.WriteLine("The PreExecute event of the " & _  
      exec.ToString() & " has been raised.")  
  
  End Sub  
  
End Class  
```  
  
## <a name="creating-dtseventhandler-objects"></a>DtsEventHandler オブジェクトの作成  
 ランタイム エンジンには、<xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> オブジェクトを介した、堅牢で柔軟性の高いイベント処理/通知システムが含まれています。 このオブジェクトを使用すると、イベント ハンドラー内のワークフロー全体をデザインして、そのイベント ハンドラーが属するイベントが発生したときにのみ、ワークフローを実行させることができます。 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> はコンテナー オブジェクトで、親オブジェクト内の対応するイベントが発生すると実行されます。 したがって、コンテナー上で発生したイベントに応答して実行されるワークフローを、他のワークフローとは独立して作成できます。 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> オブジェクトは同期型であるため、イベントにアタッチされたイベント ハンドラーが返されるまで、実行は再開されません。  
  
 次のコードは、<xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> オブジェクトの作成方法を示しています。 コードは、<xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask> をパッケージの <xref:Microsoft.SqlServer.Dts.Runtime.Package.Executables%2A> コレクションに追加し、次にタスクの <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> イベント用の <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnError%2A> オブジェクトを作成します。 <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask> がイベント ハンドラーに追加されます。これは、最初の <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnError%2A> に対する <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask> イベントが発生したときに行われます。 この例では、C:\Windows\Temp\DemoFile.txt という名前のファイルをテストに使用することを前提にしています。 サンプルを初めて実行するとき、ファイルが正常にコピーされていれば、イベント ハンドラーは呼び出されません。 2 回目にサンプルを実行すると、最初の <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask> はファイルのコピーに失敗し (<xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask.OverwriteDestinationFile%2A> の値が `false` であるため)、イベント ハンドラーが呼び出され、2 番目の <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask> によって変換元ファイルが削除され、エラーの発生が原因でパッケージによって失敗が報告されます。  
  
## <a name="example"></a>例  
  
```csharp  
using System;  
using System.IO;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Tasks.FileSystemTask;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string f = "DemoFile.txt";  
      Executable e;  
      TaskHost th;  
      FileSystemTask fst;  
  
      Package p = new Package();  
  
      p.Variables.Add("sourceFile", true, String.Empty,  
        @"C:\Windows\Temp\" + f);  
      p.Variables.Add("destinationFile", true, String.Empty,  
        Path.Combine(Directory.GetCurrentDirectory(), f));  
  
      // Create a first File System task and add it to the package.  
      // This task tries to copy a file from one folder to another.  
      e = p.Executables.Add("STOCK:FileSystemTask");  
      th = e as TaskHost;  
      th.Name = "FileSystemTask1";  
      fst = th.InnerObject as FileSystemTask;  
  
      fst.Operation = DTSFileSystemOperation.CopyFile;  
      fst.OverwriteDestinationFile = false;  
      fst.Source = "sourceFile";  
      fst.IsSourcePathVariable = true;  
      fst.Destination = "destinationFile";  
      fst.IsDestinationPathVariable = true;  
  
      // Add an event handler for the FileSystemTask's OnError event.  
      DtsEventHandler ehOnError = (DtsEventHandler)th.EventHandlers.Add("OnError");  
  
      // Create a second File System task and add it to the event handler.  
      // This task deletes the source file if the event handler is called.  
      e = ehOnError.Executables.Add("STOCK:FileSystemTask");  
      th = e as TaskHost;  
      th.Name = "FileSystemTask2";  
      fst = th.InnerObject as FileSystemTask;  
  
      fst.Operation = DTSFileSystemOperation.DeleteFile;  
      fst.Source = "sourceFile";  
      fst.IsSourcePathVariable = true;  
  
      DTSExecResult vr = p.Validate(null, null, null, null);  
      Console.WriteLine("ValidationResult = " + vr.ToString());  
      if (vr == DTSExecResult.Success)  
      {  
        DTSExecResult er = p.Execute(null, null, null, null, null);  
        Console.WriteLine("ExecutionResult = " + er.ToString());  
        if (er == DTSExecResult.Failure)  
          if (!File.Exists(@"C:\Windows\Temp\" + f))  
            Console.WriteLine("Source file has been deleted by the event handler.");  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports System.IO  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Tasks.FileSystemTask  
  
Module Module1  
  
  Sub Main()  
  
    Dim f As String = "DemoFile.txt"  
    Dim e As Executable  
    Dim th As TaskHost  
    Dim fst As FileSystemTask  
  
    Dim p As Package = New Package()  
  
    p.Variables.Add("sourceFile", True, String.Empty, _  
      "C:\Windows\Temp\" & f)  
    p.Variables.Add("destinationFile", True, String.Empty, _  
      Path.Combine(Directory.GetCurrentDirectory(), f))  
  
    ' Create a first File System task and add it to the package.  
    ' This task tries to copy a file from one folder to another.  
    e = p.Executables.Add("STOCK:FileSystemTask")  
    th = CType(e, TaskHost)  
    th.Name = "FileSystemTask1"  
    fst = CType(th.InnerObject, FileSystemTask)  
  
    fst.Operation = DTSFileSystemOperation.CopyFile  
    fst.OverwriteDestinationFile = False  
    fst.Source = "sourceFile"  
    fst.IsSourcePathVariable = True  
    fst.Destination = "destinationFile"  
    fst.IsDestinationPathVariable = True  
  
    ' Add an event handler for the FileSystemTask's OnError event.  
    Dim ehOnError As DtsEventHandler = CType(th.EventHandlers.Add("OnError"), DtsEventHandler)  
  
    ' Create a second File System task and add it to the event handler.  
    ' This task deletes the source file if the event handler is called.  
    e = ehOnError.Executables.Add("STOCK:FileSystemTask")  
    th = CType(e, TaskHost)  
    th.Name = "FileSystemTask1"  
    fst = CType(th.InnerObject, FileSystemTask)  
  
    fst.Operation = DTSFileSystemOperation.DeleteFile  
    fst.Source = "sourceFile"  
    fst.IsSourcePathVariable = True  
  
    Dim vr As DTSExecResult = p.Validate(Nothing, Nothing, Nothing, Nothing)  
    Console.WriteLine("ValidationResult = " + vr.ToString())  
    If vr = DTSExecResult.Success Then  
      Dim er As DTSExecResult = p.Execute(Nothing, Nothing, Nothing, Nothing, Nothing)  
      Console.WriteLine("ExecutionResult = " + er.ToString())  
      If er = DTSExecResult.Failure Then  
        If Not File.Exists("C:\Windows\Temp\" + f) Then  
          Console.WriteLine("Source file has been deleted by the event handler.")  
        End If  
      End If  
    End If  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>関連項目  
 [Integration Services &#40;SSIS&#41; のイベント ハンドラー](../integration-services-ssis-event-handlers.md)   
 [パッケージにイベント ハンドラーを追加する](../add-an-event-handler-to-a-package.md)  
  
  
