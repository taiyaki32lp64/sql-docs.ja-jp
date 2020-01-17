---
title: SMO イベントの処理 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- events [SMO]
- SQL Server Management Objects, events
- SMO [SQL Server], events
- events [SMO], about events
ms.assetid: b4f120dd-ba78-46ff-99c5-e47effac8544
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d0d309103880a369a88952e19b252fc15693fdd4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63191927"
---
# <a name="handling-smo-events"></a>SMO イベントの処理
  サーバー イベントの型には、イベント ハンドラーおよび <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトを使用してサブスクライブできるものがあります。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) のインスタンス クラスの多くは、サーバー上で特定のアクションが発生した場合にイベントをトリガーすることができます。  
  
 これらのイベントは、イベント ハンドラーを設定し、関連するイベントをサブスクライブすることで、プログラムを使用して処理を行うことができます。 サブスクリプションは SMO クライアント プログラムの終了時にすべて削除されるため、この種類のイベント ハンドリングは一時的なものです。  
  
## <a name="connectioncontext-event-handling"></a>ConnectionContext イベント ハンドリング  
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトは複数のイベントの種類をサポートしています。 イベント プロパティは、適切なイベント ハンドラーのインスタンスに対して設定されている必要があります。また、イベント ハンドラー オブジェクトは、イベントを処理するプロテクト関数として定義されている必要があります。  
  
## <a name="event-subscription"></a>イベント サブスクリプション  
 イベントを処理するには、イベント ハンドラー クラスを作成し、イベント ハンドラー クラスのインスタンスの作成して、イベント ハンドラーを親オブジェクトに割り当てて、イベントをサブスクライブします。  
  
 イベントを処理するためには、イベント ハンドラー クラスが作成される必要があります。 イベント ハンドラー クラスは、2 つ以上のイベント ハンドラー関数を含めることができます。また、処理されるイベントに対してインストールされている必要があります。 イベント ハンドラー関数からのイベントに関する情報が表示される、 *ServerEventNotificatificationArgs*パラメーター イベントに関する情報をレポートするために使用できます。  
  
 処理可能なデータベースとサーバーのイベントの種類が記載されて、<xref:Microsoft.SqlServer.Management.Smo.DatabaseEventSet>クラスおよび<xref:Microsoft.SqlServer.Management.Smo.ServerEventSet>クラス。  
  
## <a name="example"></a>例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="registering-event-handlers-and-subscribing-to-event-handling-in-visual-basic"></a>Visual Basic でのイベント ハンドラーの登録およびイベント ハンドリングのサブスクライブ  
 このコード例では、イベント ハンドラーを設定する方法およびデータベース イベントをサブスクライブする方法を示します。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBEvents1](SMO How to#SMO_VBEvents1)]  -->  
  
## <a name="registering-event-handlers-and-subscribing-to-event-handling-in-visual-c"></a>Visual C# でのイベント ハンドラーの登録およびイベント ハンドリングのサブスクライブ  
 このコード例では、イベント ハンドラーを設定する方法およびデータベース イベントをサブスクライブする方法を示します。  
  
```  
//Create an event handler subroutine that runs when a table is created.   
private void MyCreateEventHandler(object sender, ServerEventArgs e)   
{   
Console.WriteLine("A table has just been added to the AdventureWorks2012 database.");   
}   
//Create an event handler subroutine that runs when a table is deleted.   
private void MyDropEventHandler(object sender, ServerEventArgs e)   
{   
Console.WriteLine("A table has just been dropped from the AdventureWorks2012 database.");   
}   
public void Main()   
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Create a database event set that contains the CreateTable event only.   
DatabaseEventSet databaseCreateEventSet = new DatabaseEventSet();   
databaseCreateEventSet.CreateTable = true;   
//Create a server event handler and set it to the first event handler subroutine.   
ServerEventHandler serverCreateEventHandler;   
serverCreateEventHandler = new ServerEventHandler(MyCreateEventHandler);   
//Subscribe to the first server event handler when a CreateTable event occurs.   
db.Events.SubscribeToEvents(databaseCreateEventSet, serverCreateEventHandler);   
    //Create a database event set that contains the DropTable event only.   
DatabaseEventSet databaseDropEventSet = new DatabaseEventSet();   
databaseDropEventSet.DropTable = true;   
//Create a server event handler and set it to the second event handler subroutine.   
ServerEventHandler serverDropEventHandler;   
serverDropEventHandler = new ServerEventHandler(MyDropEventHandler);   
//Subscribe to the second server event handler when a DropTable event occurs.   
db.Events.SubscribeToEvents(databaseDropEventSet, serverDropEventHandler);   
//Start event handling.   
db.Events.StartEvents();   
//Create a table on the database.   
Table tb;   
tb = new Table(db, "Test_Table");   
Column mycol1;   
mycol1 = new Column(tb, "Name", DataType.NChar(50));   
mycol1.Collation = "Latin1_General_CI_AS";   
mycol1.Nullable = true;   
tb.Columns.Add(mycol1);   
tb.Create();   
//Remove the table.   
tb.Drop();   
//Wait until the events have occured.   
int x;   
int y;   
for (x = 1; x <= 1000000000; x++) {   
    y = x * 2;   
}   
//Stop event handling.   
db.Events.StopEvents();   
}  
```  
  
  
