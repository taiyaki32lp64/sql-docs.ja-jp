---
title: SQL Server のインスタンスに接続する |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, connections
- connections [SMO]
- instances of SQL Server, connections
- SMO [SQL Server], connections
ms.assetid: ad3cf354-b2e3-468b-b986-1232e375fd84
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1d22ec44b7be6562c7186272b403a76cd562be62
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63192081"
---
# <a name="connecting-to-an-instance-of-sql-server"></a>SQL Server のインスタンスへの接続
  最初のプログラミングのステップを[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]管理オブジェクト (SMO) アプリケーションがのインスタンスを作成するには、<xref:Microsoft.SqlServer.Management.Smo.Server>オブジェクトのインスタンスへの接続を確立するために、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクトのインスタンスを作成し、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスへの接続を確立するには、3 つの方法があります。 1 つは、<xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクト変数を使用して接続情報を提供する方法です。 2 つ目は、<xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクト プロパティを明示的に設定することで接続情報を提供する方法です。 3 つ目は、<xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクト コンストラクターに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの名前を渡す方法です。  
  
 **ServerConnection オブジェクトを使用します。**  
  
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクト変数を使用することの利点は、接続情報を再利用できることです。 まず、<xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクト変数を宣言します。 次に、<xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトを宣言し、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスの名前などの接続情報を持つプロパティ、および認証モードを設定します。 そして、パラメーターとして <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクト変数を <xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクト コンストラクターに渡します。 異なるサーバー オブジェクト間で同時に接続を共有することはお勧めできません。 <xref:Microsoft.SqlServer.Management.Common.ServerConnection.Copy%2A> メソッドを使用して、既存の接続設定のコピーを取得してください。  
  
 **サーバー オブジェクトのプロパティを明示的に設定**  
  
 別の方法として、<xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクト変数を宣言して、既定のコンストラクターを呼び出すこともできます。 <xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクトは、すべての既定の接続設定で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の既定インスタンスに接続しようとします。  
  
 **サーバー オブジェクトのコンス トラクターで SQL Server インスタンス名を指定します。**  
  
 <xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクト変数を宣言し、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス名を文字列パラメーターとしてコンストラクターに渡します。 <xref:Microsoft.SqlServer.Management.Smo.Server> オブジェクトは、既定の接続設定で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスとの接続を確立します。  
  
## <a name="connection-pooling"></a>接続のプール  
 通常、<xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Common.ServerConnection> メソッドを呼び出す必要はありません。 SMO は、必要な場合には自動的に接続を確立し、実行中の操作が完了した後で接続プールに接続を解放します。 <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> メソッドが呼び出された場合、接続はプールに解放されません。 接続をプールに解放するには、<xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> メソッドへの明示的な呼び出しが必要です。 また、<xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Common.ServerConnection> プロパティを設定することによって、プールされていない接続を要求することもできます。  
  
## <a name="multithreaded-applications"></a>マルチスレッド アプリケーション  
 マルチスレッド化されたアプリケーションの場合、各スレッドで別々の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトを使用します。  
  
## <a name="connecting-to-an-instance-of-sql-server-for-rmo"></a>RMO の SQL Server のインスタンスへの接続  
 レプリケーション管理オブジェクト (RMO) では、レプリケーション サーバーへの接続には、SMO とは少し異なる方法を使用します。  
  
 RMO プログラミング オブジェクトでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスへの接続は、`Microsoft.SqlServer.Management.Common` 名前空間によって実装された <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトを使用して行われる必要があります。 サーバーへのこの接続は、RMO プログラミング オブジェクトからは独立して行われます。 そして、インスタンスの作成時、またはオブジェクトの <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティへの割り当てによって、RMO オブジェクトに渡されます。 この方法では、RMO プログラミング オブジェクトおよび接続オブジェクト インスタンスを別々に作成および管理することが可能となり、単一の接続オブジェクトを複数の RMO プログラミング オブジェクトと共に再利用することができます。 レプリケーション サーバーへの接続には、次の規則が適用されます。  
  
-   接続のプロパティはすべて、<xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトに対して定義します。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスへの各接続には、独自の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトが必要です。  
  
-   接続を作成し、サーバーに正常にログオンするための認証情報はすべて <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトで指定されます。  
  
-   既定では、接続は Microsoft Windows 認証を使用して作成します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証を使用するには、<xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.LoginSecure%2A> を False に設定し、<xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Login%2A> および <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Password%2A> に、有効な [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログオンおよびパスワードを設定しておく必要があります。 セキュリティの資格情報は、常に安全に格納および処理し、いつでも可能であれば実行時に提供する必要があります。  
  
-   <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> メソッドは、RMO プログラミング オブジェクトに接続を渡す前に呼び出す必要があります。  
  
## <a name="examples"></a>使用例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="connecting-to-the-local-instance-of-sql-server-by-using-windows-authentication-in-visual-basic"></a>Visual Basic で Windows 認証を使用して SQL Server のローカル インスタンスに接続する  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のローカル インスタンスへの接続に必要なコードは多くありません。 ただし、認証方法とサーバーの既定の設定によってコードが異なります。 接続は、データの取得を必要とする操作が初めて発生する際に作成します。  
  
 この例は[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]のローカル インスタンスに接続する .NET コード[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Windows 認証を使用しています。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VB1](SMO How to#SMO_VB1)]  -->  
  
## <a name="connecting-to-the-local-instance-of-sql-server-by-using-windows-authentication-in-visual-c"></a>Visual C# で Windows 認証を使用して SQL Server のローカル インスタンスに接続する  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のローカル インスタンスへの接続に必要なコードは多くありません。 ただし、認証方法とサーバーの既定の設定によってコードが異なります。 接続は、データの取得を必要とする操作が初めて発生する際に作成します。  
  
 この例は、Windows 認証を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のローカル インスタンスに接続する Visual C# .NET コードです。  
  
```  
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
  
 この例は[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]のリモート インスタンスに接続する .NET コード[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Windows 認証を使用しています。 文字列変数*strServer*リモート インスタンスの名前が含まれています。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VB2](SMO How to#SMO_VB2)]  -->  
  
## <a name="connecting-to-a-remote-instance-of-sql-server-by-using-windows-authentication-in-visual-c"></a>Visual C# で Windows 認証を使用して SQL Server のリモート インスタンスに接続する  
 Windows 認証を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに接続する場合、認証の種類を指定する必要はありません。 既定は Windows 認証です。  
  
 この例は、Windows 認証を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のリモート インスタンスに接続する Visual C# .NET コードです。 文字列変数*strServer*リモート インスタンスの名前が含まれています。  
  
```  
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
  
 例は、 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 、リモート インスタンスに接続する方法については、.NET コードと*vPassword*はログインとパスワードを含めることができます。  
  
```  
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
  
 例は、リモート インスタンスに接続する方法については、Visual c# .NET コードと*vPassword*はログインとパスワードを含めることができます。  
  
```  
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
  
  
