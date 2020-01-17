---
title: プログラムによる接続の追加 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- connection managers [Integration Services], packages
- Integration Services packages, connections
- connections [Integration Services], packages
- SSIS packages, connections
- packages [Integration Services], connections
- intrinsic properties [Integration Services]
- SQL Server Integration Services packages, connections
- ConnectionManager class
- SSIS connection managers
- adding package connections
ms.assetid: d90716d1-4c65-466c-b82c-4aabbee1e3e5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b1258797d76df49a2622335ee798120632706c78
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62772227"
---
# <a name="adding-connections-programmatically"></a>プログラムによる接続の追加
  <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> クラスは、外部データ ソースへの物理接続を表します。 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> クラスは、ランタイムから接続の実装詳細を分離します。 これにより、ランタイムは、一貫した予測可能な方法でそれぞれの接続マネージャーとやり取りを行うことができます。 接続マネージャーには、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Name%2A>、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ID%2A>、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Description%2A>、および <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ConnectionString%2A> など、すべての接続に共通のストック プロパティのセットが含まれています。 ただし、接続マネージャーを構成するために必要なプロパティは、通常 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ConnectionString%2A> および <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Name%2A> プロパティのみです。 接続クラスが `Open` や `Connect` などのメソッドを公開して物理的にデータ ソースへの接続を確立する他のプログラミング パラダイムと異なり、ランタイム エンジンは、パッケージの実行中に、そのパッケージのすべての接続を管理します。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> クラスは、パッケージに追加されて実行時に使用できる接続マネージャーのコレクションです。 コレクションの <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Add%2A> メソッドを使用し、接続マネージャーの種類を示す文字列を指定することによって、接続マネージャーをコレクションに追加できます。 <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Add%2A> メソッドは、パッケージに追加された <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> のインスタンスを返します。  
  
## <a name="intrinsic-properties"></a>固有プロパティ  
 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> クラスは、すべての接続に共通のプロパティのセットを公開します。 ただし、特定の接続の種類に固有のプロパティにアクセスする必要が生じる場合もあります。 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Properties%2A> クラスの <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> コレクションは、これらのプロパティへのアクセスを提供します。 プロパティをコレクションから取得するには、インデクサーまたはプロパティ名、および **GetValue** メソッドを使用し、その値を設定するには **SetValue** メソッドを使用します。 基になる接続オブジェクトのプロパティには、オブジェクトの実際のインスタンスを取得し、そのプロパティを直接設定することもできます。 基になる接続を取得するには、接続マネージャーの <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.InnerObject%2A> プロパティを使用します。 次のコード行は、基になるクラス <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.ConnectionManagerAdoNetClass> を持つ ADO.NET 接続マネージャーを作成する C# の行を示しています。  
  
 `ConnectionManagerAdoNetClass cmado = cm.InnerObject as ConnectionManagerAdoNet;`  
  
 これは、マネージド接続マネージャー オブジェクトを、その基になる接続オブジェクトにキャストします。 C++ を使用している場合、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> オブジェクトの `QueryInterface` メソッドが呼び出され、基になる接続オブジェクトのインターフェイスが要求されます。  
  
 次の表は、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] が備えている接続マネージャーと `package.Connections.Add("xxx")` ステートメントで使用される文字列を示しています。 すべての接続マネージャーのリストについては、「[Integration Services &#40;SSIS&#41; の接続](../connection-manager/integration-services-ssis-connections.md)」を参照してください。  
  
|String|[ODBC 入力元エディター]|  
|------------|------------------------|  
|"OLEDB"|OLE DB 接続用の接続マネージャー|  
|"ODBC"|ODBC 接続用の接続マネージャー|  
|"ADO"|ADO 接続用の接続マネージャー|  
|"ADO.NET:SQL"|ADO.NET (SQL データ プロバイダー) 接続用の接続マネージャー|  
|"ADO.NET:OLEDB"|ADO.NET (OLE DB データ プロバイダー) 接続用の接続マネージャー|  
|"FLATFILE"|フラット ファイル接続用の接続マネージャー|  
|"FILE"|ファイル接続用の接続マネージャー|  
|"MULTIFLATFILE"|複数のフラット ファイル接続用の接続マネージャー|  
|"MULTIFILE"|複数のファイル接続用の接続マネージャー|  
|"SQLMOBILE"|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 接続用の接続マネージャー|  
|"MSOLAP100"|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続用の接続マネージャー|  
|"FTP"|FTP 接続用の接続マネージャー|  
|"HTTP"|HTTP 接続用の接続マネージャー|  
|"MSMQ"|メッセージ キュー (MSMQ) 接続用の接続マネージャー|  
|"SMTP"|SMTP 接続用の接続マネージャー|  
|"WMI"|WMI (Windows Management Instrumentation) 接続用の接続マネージャー|  
  
 次のコード例では、OLE DB 接続およびファイル接続を <xref:Microsoft.SqlServer.Dts.Runtime.Package.Connections%2A> の <xref:Microsoft.SqlServer.Dts.Runtime.Package> コレクションに追加する方法を示します。 この例では、次に、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ConnectionString%2A>、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Name%2A>、および <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Description%2A> プロパティを設定します。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      // Create a package, and retrieve its connections.  
      Package pkg = new Package();  
      Connections pkgConns = pkg.Connections;  
  
      // Add an OLE DB connection to the package, using the   
      // method defined in the AddConnection class.  
      CreateConnection myOLEDBConn = new CreateConnection();  
      myOLEDBConn.CreateOLEDBConnection(pkg);  
  
      // View the new connection in the package.  
      Console.WriteLine("Connection description: {0}",  
         pkg.Connections["SSIS Connection Manager for OLE DB"].Description);  
  
      // Add a second connection to the package.  
      CreateConnection myFileConn = new CreateConnection();  
      myFileConn.CreateFileConnection(pkg);  
  
      // View the second connection in the package.  
      Console.WriteLine("Connection description: {0}",  
        pkg.Connections["SSIS Connection Manager for Files"].Description);  
  
      Console.WriteLine();  
      Console.WriteLine("Number of connections in package: {0}", pkg.Connections.Count);  
  
      Console.Read();  
    }  
  }  
  // <summary>  
  // This class contains the definitions for multiple  
  // connection managers.  
  // </summary>  
  public class CreateConnection  
  {  
    // Private data.  
    private ConnectionManager ConMgr;  
  
    // Class definition for OLE DB Provider.  
    public void CreateOLEDBConnection(Package p)  
    {  
      ConMgr = p.Connections.Add("OLEDB");  
      ConMgr.ConnectionString = "Provider=SQLOLEDB.1;" +  
        "Integrated Security=SSPI;Initial Catalog=AdventureWorks;" +  
        "Data Source=(local);";  
      ConMgr.Name = "SSIS Connection Manager for OLE DB";  
      ConMgr.Description = "OLE DB connection to the AdventureWorks database.";  
    }  
    public void CreateFileConnection(Package p)  
    {  
      ConMgr = p.Connections.Add("File");  
      ConMgr.ConnectionString = @"\\<yourserver>\<yourfolder>\books.xml";  
      ConMgr.Name = "SSIS Connection Manager for Files";  
      ConMgr.Description = "Flat File connection";  
    }  
  }  
  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    ' Create a package, and retrieve its connections.  
    Dim pkg As New Package()  
    Dim pkgConns As Connections = pkg.Connections  
  
    ' Add an OLE DB connection to the package, using the   
    ' method defined in the AddConnection class.  
    Dim myOLEDBConn As New CreateConnection()  
    myOLEDBConn.CreateOLEDBConnection(pkg)  
  
    ' View the new connection in the package.  
    Console.WriteLine("Connection description: {0}", _  
      pkg.Connections("SSIS Connection Manager for OLE DB").Description)  
  
    ' Add a second connection to the package.  
    Dim myFileConn As New CreateConnection()  
    myFileConn.CreateFileConnection(pkg)  
  
    ' View the second connection in the package.  
    Console.WriteLine("Connection description: {0}", _  
      pkg.Connections("SSIS Connection Manager for Files").Description)  
  
    Console.WriteLine()  
    Console.WriteLine("Number of connections in package: {0}", pkg.Connections.Count)  
  
    Console.Read()  
  
  End Sub  
  
End Module  
  
' This class contains the definitions for multiple  
' connection managers.  
  
Public Class CreateConnection  
  ' Private data.  
  Private ConMgr As ConnectionManager  
  
  ' Class definition for OLE DB provider.  
  Public Sub CreateOLEDBConnection(ByVal p As Package)  
    ConMgr = p.Connections.Add("OLEDB")  
    ConMgr.ConnectionString = "Provider=SQLOLEDB.1;" & _  
      "Integrated Security=SSPI;Initial Catalog=AdventureWorks;" & _  
      "Data Source=(local);"  
    ConMgr.Name = "SSIS Connection Manager for OLE DB"  
    ConMgr.Description = "OLE DB connection to the AdventureWorks database."  
  End Sub  
  
  Public Sub CreateFileConnection(ByVal p As Package)  
    ConMgr = p.Connections.Add("File")  
    ConMgr.ConnectionString = "\\<yourserver>\<yourfolder>\books.xml"  
    ConMgr.Name = "SSIS Connection Manager for Files"  
    ConMgr.Description = "Flat File connection"  
  End Sub  
  
End Class  
```  
  
 **サンプル出力:**  
  
 `Connection description: OLE DB connection to the AdventureWorks database.`  
  
 `Connection description: OLE DB connection to the AdventureWorks database.`  
  
 `Number of connections in package: 2`  
  
## <a name="external-resources"></a>外部リソース  
 carlprothman.net の [接続文字列](https://go.microsoft.com/fwlink/?LinkId=220743)に関する技術記事  
  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>関連項目  
 [Integration Services &#40;SSIS&#41; の接続](../connection-manager/integration-services-ssis-connections.md)   
 [接続マネージャーを作成する](../create-connection-managers.md)  
  
  
