---
title: SQL Server のインスタンスへの接続 |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, connections
- connections [SMO]
- instances of SQL Server, connections
- SMO [SQL Server], connections
ms.assetid: ad3cf354-b2e3-468b-b986-1232e375fd84
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 14eff405fd4eb1b96f4f5e5b50624d2c1251d546
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2019
ms.locfileid: "70148755"
---
# <a name="connecting-to-an-instance-of-sql-server"></a>SQL Server のインスタンスへの接続
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]管理オブジェクト (SMO) アプリケーションの最初のプログラミング手順では、 <xref:Microsoft.SqlServer.Management.Smo.Server>オブジェクトのインスタンスを作成し、のインスタンスへの[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]接続を確立します。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクトのインスタンスを作成し、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスへの接続を確立するには、3 つの方法があります。 1 つは、<xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクト変数を使用して接続情報を提供する方法です。 2 つ目は、<xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクト プロパティを明示的に設定することで接続情報を提供する方法です。 3 つ目は、<xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクト コンストラクターに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの名前を渡す方法です。 
  
 **ServerConnection オブジェクトの使用**  
  
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクト変数を使用することの利点は、接続情報を再利用できることです。 まず、<xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクト変数を宣言します。 次に、<xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトを宣言し、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスの名前などの接続情報を持つプロパティ、および認証モードを設定します。 そして、パラメーターとして <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクト変数を <xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクト コンストラクターに渡します。 異なるサーバー オブジェクト間で同時に接続を共有することはお勧めできません。 <xref:Microsoft.SqlServer.Management.Common.ServerConnection.Copy%2A> メソッドを使用して、既存の接続設定のコピーを取得してください。  
  
 **サーバーオブジェクトのプロパティを明示的に設定する**  
  
 別の方法として、<xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクト変数を宣言して、既定のコンストラクターを呼び出すこともできます。 <xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクトは、すべての既定の接続設定で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の既定インスタンスに接続しようとします。  
  
 **サーバーオブジェクトコンストラクターに SQL Server インスタンス名を指定する**  
  
 <xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクト変数を宣言し、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス名を文字列パラメーターとしてコンストラクターに渡します。 <xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクトは、既定の接続設定で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスとの接続を確立します。  
  
## <a name="connection-pooling"></a>接続のプール  
 通常、<xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Common.ServerConnection> メソッドを呼び出す必要はありません。 SMO は、必要な場合には自動的に接続を確立し、実行中の操作が完了した後で接続プールに接続を解放します。 <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> メソッドが呼び出された場合、接続はプールに解放されません。 接続をプールに解放するには、<xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> メソッドへの明示的な呼び出しが必要です。 また、<xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Common.ServerConnection> プロパティを設定することによって、プールされていない接続を要求することもできます。  
  
## <a name="multithreaded-applications"></a>マルチスレッド アプリケーション  
 マルチスレッド化されたアプリケーションの場合、各スレッドで別々の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトを使用します。  
  
## <a name="connecting-to-an-instance-of-sql-server-for-rmo"></a>RMO の SQL Server のインスタンスへの接続  
 レプリケーション管理オブジェクト (RMO) では、レプリケーション サーバーへの接続には、SMO とは少し異なる方法を使用します。  
  
 Rmo プログラミングオブジェクトを[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] <xref:Microsoft.SqlServer.Management.Common.ServerConnection>使用するには、のインスタンスへの接続が、 **Microsoft**の名前空間によって実装されたオブジェクトを使用して行われる必要があります。 サーバーへのこの接続は、RMO プログラミング オブジェクトからは独立して行われます。 そして、インスタンスの作成時、またはオブジェクトの <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティへの割り当てによって、RMO オブジェクトに渡されます。 この方法では、RMO プログラミング オブジェクトおよび接続オブジェクト インスタンスを別々に作成および管理することが可能となり、単一の接続オブジェクトを複数の RMO プログラミング オブジェクトと共に再利用することができます。 レプリケーション サーバーへの接続には、次の規則が適用されます。  
  
-   接続のプロパティはすべて、<xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトに対して定義します。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスへの各接続には、独自の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトが必要です。  
  
-   接続を作成し、サーバーに正常にログオンするための認証情報はすべて <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトで指定されます。  
  
-   既定では、接続は Microsoft Windows 認証を使用して作成します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証を使用するには、<xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.LoginSecure%2A> を False に設定し、<xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Login%2A> および <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Password%2A> に、有効な [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログオンおよびパスワードを設定しておく必要があります。 セキュリティの資格情報は、常に安全に格納および処理し、いつでも可能であれば実行時に提供する必要があります。  
  
-   <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> メソッドは、RMO プログラミング オブジェクトに接続を渡す前に呼び出す必要があります。  
  
## <a name="examples"></a>使用例  
提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual Studio&#35; .Net での Visual C SMO プロジェクトの作成](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="connecting-to-the-local-instance-of-sql-server-by-using-windows-authentication-in-visual-basic"></a>Visual Basic で Windows 認証を使用して SQL Server のローカル インスタンスに接続する  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のローカル インスタンスへの接続に必要なコードは多くありません。 ただし、認証方法とサーバーの既定の設定によってコードが異なります。 接続は、データの取得を必要とする操作が初めて発生する際に作成します。  
 
この例は、Windows 認証を使用して SQL Server のローカルインスタンスに接続する .NET コード Visual Basic ます。 

```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'The connection is established when a property is requested.
Console.WriteLine(srv.Information.Version)
'The connection is automatically disconnected when the Server variable goes out of scope.
```
  
## <a name="connecting-to-the-local-instance-of-sql-server-by-using-windows-authentication-in-visual-c"></a>Visual C# で Windows 認証を使用して SQL Server のローカル インスタンスに接続する  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のローカル インスタンスへの接続に必要なコードは多くありません。 ただし、認証方法とサーバーの既定の設定によってコードが異なります。 接続は、データの取得を必要とする操作が初めて発生する際に作成します。  
  
 この例は、Windows 認証を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のローカル インスタンスに接続する Visual C# .NET コードです。  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//The connection is established when a property is requested.   
Console.WriteLine(srv.Information.Version);   
}   
//The connection is automatically disconnected when the Server variable goes out of scope.  
```  
  
## <a name="connecting-to-a-remote-instance-of-sql-server-by-using-windows-authentication-in-visual-basic"></a>Visual Basic で Windows 認証を使用して SQL Server のリモート インスタンスに接続する  
 Windows 認証を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに接続する場合、認証の種類を指定する必要はありません。 既定は Windows 認証です。  
  
 この例は[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 、Windows 認証を使用しての[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]リモートインスタンスに接続する .net コードです。 文字列変数*Strserver*には、リモートインスタンスの名前が含まれています。  
  
```VBNET   
'Connect to a remote instance of SQL Server.
Dim srv As Server
'The strServer string variable contains the name of a remote instance of SQL Server.
srv = New Server(strServer)
'The actual connection is made when a property is retrieved. 
Console.WriteLine(srv.Information.Version)
'The connection is automatically disconnected when the Server variable goes out of scope.
```
  
## <a name="connecting-to-a-remote-instance-of-sql-server-by-using-windows-authentication-in-visual-c"></a>Visual C# で Windows 認証を使用して SQL Server のリモート インスタンスに接続する  
 Windows 認証を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに接続する場合、認証の種類を指定する必要はありません。 既定は Windows 認証です。  
  
 この例は、Windows 認証を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のリモート インスタンスに接続する Visual C# .NET コードです。 文字列変数*Strserver*には、リモートインスタンスの名前が含まれています。  
  
```csharp  
{   
//Connect to a remote instance of SQL Server.   
Server srv;   
//The strServer string variable contains the name of a remote instance of SQL Server.   
srv = new Server(strServer);   
//The actual connection is made when a property is retrieved.   
Console.WriteLine(srv.Information.Version);   
}   
//The connection is automatically disconnected when the Server variable goes out of scope.  
```  
  
## <a name="connecting-to-an-instance-of-sql-server-by-using-sql-server-authentication-in-visual-basic"></a>Visual Basic で SQL Server 認証を使用して SQL Server のインスタンスに接続する  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに接続する場合、認証の種類を指定する必要があります。 この例では、もう 1 つの方法として、<xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクト変数を宣言する方法を示します。この方法では、接続情報の再利用が可能になります。  
  
 この例は[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 、リモートの接続方法と、ログオンとパスワードを格納する*vpassword*を示す .net コードです。  
  
```VBNET  
' compile with:   
' /r:Microsoft.SqlServer.Smo.dll  
' /r:Microsoft.SqlServer.ConnectionInfo.dll  
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Common  
  
Public Class A  
   Public Shared Sub Main()  
      Dim sqlServerLogin As [String] = "user_id"  
      Dim password As [String] = "pwd"  
      Dim instanceName As [String] = "instance_name"  
      Dim remoteSvrName As [String] = "remote_server_name"  
  
      ' Connecting to an instance of SQL Server using SQL Server Authentication  
      Dim srv1 As New Server()   ' connects to default instance  
      srv1.ConnectionContext.LoginSecure = False   ' set to true for Windows Authentication  
      srv1.ConnectionContext.Login = sqlServerLogin  
      srv1.ConnectionContext.Password = password  
      Console.WriteLine(srv1.Information.Version)   ' connection is established  
  
      ' Connecting to a named instance of SQL Server with SQL Server Authentication using ServerConnection  
      Dim srvConn As New ServerConnection()  
      srvConn.ServerInstance = ".\" & instanceName   ' connects to named instance  
      srvConn.LoginSecure = False   ' set to true for Windows Authentication  
      srvConn.Login = sqlServerLogin  
      srvConn.Password = password  
      Dim srv2 As New Server(srvConn)  
      Console.WriteLine(srv2.Information.Version)   ' connection is established  
  
      ' For remote connection, remote server name / ServerInstance needs to be specified  
      Dim srvConn2 As New ServerConnection(remoteSvrName)  
      srvConn2.LoginSecure = False  
      srvConn2.Login = sqlServerLogin  
      srvConn2.Password = password  
      Dim srv3 As New Server(srvConn2)  
      Console.WriteLine(srv3.Information.Version)   ' connection is established  
   End Sub  
End Class  
```  
  
## <a name="connecting-to-an-instance-of-sql-server-by-using-sql-server-authentication-in-visual-c"></a>Visual C# で SQL Server 認証を使用して SQL Server のインスタンスに接続する  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに接続する場合、認証の種類を指定する必要があります。 この例では、もう 1 つの方法として、<xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクト変数を宣言する方法を示します。この方法では、接続情報の再利用が可能になります。  
  
 この例は、 C#リモートに接続する方法と、ログオンとパスワードを格納する*Vpassword*を示す Visual .net コードです。  
  
```csharp  
// compile with:   
// /r:Microsoft.SqlServer.Smo.dll  
// /r:Microsoft.SqlServer.ConnectionInfo.dll  
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
using System;  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Common;  
  
public class A {  
   public static void Main() {   
      String sqlServerLogin = "user_id";  
      String password = "pwd";  
      String instanceName = "instance_name";  
      String remoteSvrName = "remote_server_name";  
  
      // Connecting to an instance of SQL Server using SQL Server Authentication  
      Server srv1 = new Server();   // connects to default instance  
      srv1.ConnectionContext.LoginSecure = false;   // set to true for Windows Authentication  
      srv1.ConnectionContext.Login = sqlServerLogin;  
      srv1.ConnectionContext.Password = password;  
      Console.WriteLine(srv1.Information.Version);   // connection is established  
  
      // Connecting to a named instance of SQL Server with SQL Server Authentication using ServerConnection  
      ServerConnection srvConn = new ServerConnection();  
      srvConn.ServerInstance = @".\" + instanceName;   // connects to named instance  
      srvConn.LoginSecure = false;   // set to true for Windows Authentication  
      srvConn.Login = sqlServerLogin;  
      srvConn.Password = password;  
      Server srv2 = new Server(srvConn);  
      Console.WriteLine(srv2.Information.Version);   // connection is established  
  
      // For remote connection, remote server name / ServerInstance needs to be specified  
      ServerConnection srvConn2 = new ServerConnection(remoteSvrName);  
      srvConn2.LoginSecure = false;  
      srvConn2.Login = sqlServerLogin;  
      srvConn2.Password = password;  
      Server srv3 = new Server(srvConn2);  
      Console.WriteLine(srv3.Information.Version);   // connection is established  
   }  
}  
```  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  
