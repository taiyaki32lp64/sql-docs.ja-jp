---
title: プログラムによるローカル パッケージの読み込みと実行 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Integration Services packages, running
- events [Integration Services], capturing
- packages [Integration Services], running
- loading packages programmatically
- Visual Basic [Integration Services]
- running packages [Integration Services]
- programmatically load and run packages [SSIS]
ms.assetid: 2f9fc1a8-a001-4c54-8c64-63b443725422
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 00d213bf8ca554b60edc8dc3de3f1290cd00f538
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62766894"
---
# <a name="loading-and-running-a-local-package-programmatically"></a>プログラムによるローカル パッケージの読み込みと実行
  「[パッケージの実行](../packages/run-integration-services-ssis-packages.md)」で説明されている方法を使用して、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを必要に応じて実行したり、事前に定義した時刻に実行したりすることができます。 また、数行のコードを記述するだけで、Windows フォーム アプリケーション、コンソール アプリケーション、ASP.NET Web フォームや Web サービス、または Windows サービスなどのカスタム アプリケーションから、パッケージを実行することもできます。  
  
 このトピックの内容:  
  
-   プログラムによるパッケージの読み込み  
  
-   プログラムによるパッケージの実行  
  
 このトピックでパッケージを読み込み、実行するために使用するすべてのメソッドには、`Microsoft.SqlServer.ManagedDTS` アセンブリへの参照が必要です。 この参照を新しいプロジェクトに追加した後、`using` ステートメントまたは `Imports` ステートメントを使用して <xref:Microsoft.SqlServer.Dts.Runtime> 名前空間をインポートします。  
  
## <a name="loading-a-package-programmatically"></a>プログラムによるパッケージの読み込み  
 プログラムによってローカル コンピューターでパッケージを読み込むには、パッケージがローカルまたはリモートのどちらに保存されているかに関係なく、次のいずれかの方法を使用できます。  
  
|ストレージの場所|呼び出すメソッド|  
|----------------------|--------------------|  
|ファイル|<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadPackage%2A>|  
|[SSIS パッケージ ストア]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromSqlServer%2A>|  
  
> [!IMPORTANT]  
>  SSIS パッケージ ストアを操作するための <xref:Microsoft.SqlServer.Dts.Runtime.Application> クラスのメソッドは、"."、localhost、またはローカル サーバーのサーバー名のみをサポートします。 "(local)" は使用できません。  
  
## <a name="running-a-package-programmatically"></a>プログラムによるパッケージの実行  
 ローカル コンピューターでマネージド コードを使用して、パッケージを実行するカスタム アプリケーションを開発するには、次の方法が必要です。 ここにまとめた手順は、後のサンプル コンソール アプリケーションで示します。  
  
#### <a name="to-run-a-package-on-the-local-computer-programmatically"></a>プログラムによってローカル コンピューターでパッケージを実行するには  
  
1.  Visual Studio 開発環境を起動し、任意の開発言語で、新しいアプリケーションを作成します。 この例ではコンソール アプリケーションを使用しますが、Windows フォーム アプリケーション、ASP.NET Web フォームや Web サービス、または Windows サービスからパッケージを実行することもできます。  
  
2.  **[プロジェクト]** メニューの **[参照の追加]** をクリックし、**Microsoft.SqlServer.ManagedDTS.dll** への参照を追加します。 **[OK]** をクリックします。  
  
3.  Visual Basic を使用して、`Imports`ステートメント、または c#`using`をインポートするステートメント、 **Microsoft.SqlServer.Dts.Runtime**名前空間。  
  
4.  メイン ルーチンに次のコードを追加します。 完成したコンソール アプリケーションは、たとえば次の例のようになります。  
  
    > [!NOTE]  
    >  このサンプル コードは、<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadPackage%2A> メソッドを使用してファイル システムからパッケージを読み込む方法を示していますが、 <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromSqlServer%2A> メソッドを呼び出して MSDB データベースからパッケージを読み込んだり、<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A> メソッドを呼び出して [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ ストアからパッケージを読み込むこともできます。  
  
5.  プロジェクトを実行します。 このサンプル コードでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のサンプルと共にインストールされている CalculatedColumns サンプル パッケージを実行します。 パッケージの実行結果がコンソール ウィンドウに表示されます。  
  
### <a name="sample-code"></a>サンプル コード  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim pkgLocation As String  
    Dim pkg As New Package  
    Dim app As New Application  
    Dim pkgResults As DTSExecResult  
  
    pkgLocation = _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx"  
    pkg = app.LoadPackage(pkgLocation, Nothing)  
    pkgResults = pkg.Execute()  
  
    Console.WriteLine(pkgResults.ToString())  
    Console.ReadKey()  
  
  End Sub  
  
End Module  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace RunFromClientAppCS  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string pkgLocation;  
      Package pkg;  
      Application app;  
      DTSExecResult pkgResults;  
  
      pkgLocation =  
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx";  
      app = new Application();  
      pkg = app.LoadPackage(pkgLocation, null);  
      pkgResults = pkg.Execute();  
  
      Console.WriteLine(pkgResults.ToString());  
      Console.ReadKey();  
    }  
  }  
}  
```  
  
## <a name="capturing-events-from-a-running-package"></a>実行中のパッケージからのイベントのキャプチャ  
 上記のサンプルのようにプログラムを使用してパッケージを実行するときは、パッケージの実行時に発生するエラーやその他のイベントをキャプチャすることが必要な場合もあります。 イベントのキャプチャは、<xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> クラスから継承するクラスを追加し、パッケージを読み込むときにそのクラスへの参照を渡すことによって行うことができます。 次の例では <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents.OnError%2A> イベントのみがキャプチャされますが、<xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> クラスによってキャプチャできるイベントは他にも多数あります。  
  
#### <a name="to-run-a-package-on-the-local-computer-programmatically-and-capture-package-events"></a>プログラムによってローカル コンピューターでパッケージを実行し、パッケージ イベントをキャプチャするには  
  
1.  上記の例の手順を実行し、この例のプロジェクトを作成します。  
  
2.  メイン ルーチンに次のコードを追加します。 完成したコンソール アプリケーションは、たとえば次の例のようになります。  
  
3.  プロジェクトを実行します。 このサンプル コードでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のサンプルと共にインストールされている CalculatedColumns サンプル パッケージを実行します。 パッケージ実行結果は、発生したエラーと共にコンソール ウィンドウに表示されます。  
  
### <a name="sample-code"></a>サンプル コード  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim pkgLocation As String  
    Dim pkg As New Package  
    Dim app As New Application  
    Dim pkgResults As DTSExecResult  
  
    Dim eventListener As New EventListener()  
  
    pkgLocation = _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx"  
    pkg = app.LoadPackage(pkgLocation, eventListener)  
    pkgResults = pkg.Execute(Nothing, Nothing, eventListener, Nothing, Nothing)  
  
    Console.WriteLine(pkgResults.ToString())  
    Console.ReadKey()  
  
  End Sub  
  
End Module  
  
Class EventListener  
  Inherits DefaultEvents  
  
  Public Overrides Function OnError(ByVal source As Microsoft.SqlServer.Dts.Runtime.DtsObject, _  
    ByVal errorCode As Integer, ByVal subComponent As String, ByVal description As String, _  
    ByVal helpFile As String, ByVal helpContext As Integer, _  
    ByVal idofInterfaceWithError As String) As Boolean  
  
    ' Add application-specific diagnostics here.  
    Console.WriteLine("Error in {0}/{1} : {2}", source, subComponent, description)  
    Return False  
  
  End Function  
  
End Class  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace RunFromClientAppWithEventsCS  
{  
  class MyEventListener : DefaultEvents  
  {  
    public override bool OnError(DtsObject source, int errorCode, string subComponent,   
      string description, string helpFile, int helpContext, string idofInterfaceWithError)  
    {  
      // Add application-specific diagnostics here.  
      Console.WriteLine("Error in {0}/{1} : {2}", source, subComponent, description);  
      return false;  
    }  
  }  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string pkgLocation;  
      Package pkg;  
      Application app;  
      DTSExecResult pkgResults;  
  
      MyEventListener eventListener = new MyEventListener();  
  
      pkgLocation =  
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx";  
      app = new Application();  
      pkg = app.LoadPackage(pkgLocation, eventListener);  
      pkgResults = pkg.Execute(null, null, eventListener, null, null);  
  
      Console.WriteLine(pkgResults.ToString());  
      Console.ReadKey();  
    }  
  }  
}  
```  
  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>関連項目  
 [ローカル実行とリモート実行の相違点について](../run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [プログラムによるリモート パッケージの読み込みと実行](../run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)   
 [ローカル パッケージの出力の読み込み](../run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
