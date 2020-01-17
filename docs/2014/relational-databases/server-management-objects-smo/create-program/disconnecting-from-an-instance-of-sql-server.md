---
title: SQL Server のインスタンスからの切断 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7783fa93912c305403cc34ad6e52668123d164ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63192071"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>SQL Server のインスタンスからの切断
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) オブジェクトを手動で閉じたり切断する処理は必要ありません。 接続を開いたり閉じたりする操作は、必要に応じて行われます。  
  
## <a name="connection-pooling"></a>接続のプール  
 <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> メソッドが呼び出された場合、接続は自動的には解放されません。 接続プールに接続を解放するには、<xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> メソッドを明示的に呼び出す必要があります。 また、プールされていない接続を要求することもできます。 これを行うには、<xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> オブジェクトを参照する <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> プロパティの <xref:Microsoft.SqlServer.Management.Common.ServerConnection> プロパティを設定します。  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>RMO の SQL Server のインスタンスからの切断  
 RMO を使ったプログラミングでサーバー接続を閉じる方法は、SMO とは若干異なります。  
  
 によって、RMO オブジェクトのサーバー接続が維持されるため、<xref:Microsoft.SqlServer.Management.Common.ServerConnection>オブジェクトのインスタンスから切断するときにも、このオブジェクトが使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] RMO を使用してプログラミングする場合。 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトを使用して接続を閉じるには、RMO オブジェクトの <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> メソッドを呼び出します。 接続が閉じられた後は、RMO オブジェクトを使用することはできません。  
  
## <a name="example"></a>例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>Visual Basic で SMO オブジェクトを閉じたり切断する処理を行う方法  
 このコード例では、<xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> オブジェクト プロパティの <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> プロパティを設定して、プールされていない接続を要求する方法を示します。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VB4](SMO How to#SMO_VB4)]  -->  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-c"></a>Visual C# で SMO オブジェクトを閉じたり切断する処理を行う方法  
 このコード例では、<xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> オブジェクト プロパティの <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> プロパティを設定して、プールされていない接続を要求する方法を示します。  
  
```  
{   
Server srv;   
srv = new Server();   
//Disable automatic disconnection.   
srv.ConnectionContext.AutoDisconnectMode = AutoDisconnectMode.NoAutoDisconnect;   
//Connect to the local, default instance of SQL Server.   
srv.ConnectionContext.Connect();   
//The actual connection is made when a property is retrieved.   
Console.WriteLine(srv.Information.Version);   
//Disconnect explicitly.   
srv.ConnectionContext.Disconnect();  
}  
```  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  
