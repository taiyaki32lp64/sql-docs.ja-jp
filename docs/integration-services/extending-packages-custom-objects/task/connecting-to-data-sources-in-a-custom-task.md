---
title: カスタム タスクでのデータ ソースへの接続 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ConnectionManager objects
- connection managers [Integration Services], external data sources
- data sources [Integration Services], external
- custom tasks [Integration Services], external data sources
- external data sources [Integration Services]
- connections [Integration Services], external data sources
- SSIS custom tasks, external data sources
ms.assetid: 9f0b3a43-3eaa-4b3c-bb08-29b630c11306
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3a93743753cf63514557e363af05c428f23899c4
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297101"
---
# <a name="connecting-to-data-sources-in-a-custom-task"></a>カスタム タスクでのデータ ソースへの接続

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  タスクは、接続マネージャーを使用して外部データ ソースに接続し、データを取得または保存します。 デザイン時には、接続マネージャーは論理接続を表し、サーバー名や認証プロパティなどの重要な情報を示します。 実行時に、タスクは接続マネージャーの <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> メソッドを呼び出して、データ ソースへの物理接続を確立します。  
  
 パッケージに多数のタスクが含まれていると、各タスクに異なるデータ ソースへの接続が含まれる場合があるため、パッケージは <xref:Microsoft.SqlServer.Dts.Runtime.Connections> コレクション内のすべての接続マネージャーを監視します。 タスクはパッケージ内にあるコレクションを使用し、検証および実行中に使用する接続マネージャーを検索します。 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> コレクションは、<xref:Microsoft.SqlServer.Dts.Runtime.Task.Validate%2A> および <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A> メソッドの最初のパラメーターです。  
  
 グラフィカル ユーザー インターフェイスのダイアログ ボックスまたはドロップダウン リストを使用して、コレクションの <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> オブジェクトをユーザーに表示すると、タスクで間違った接続マネージャーが使用されないようにすることができます。 これによりユーザーは、パッケージ内に含まれる適切な型の <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> オブジェクトのみから選択できるようになります。  
  
 タスクは、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> メソッドを呼び出し、データ ソースに対する物理接続を確立します。 メソッドは基になる接続オブジェクトを返し、タスクはその接続オブジェクトを使用できます。 接続マネージャーは、基になる接続オブジェクトの実装の詳細をタスクから分離します。そのため、接続を確立するには、タスクは <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> メソッドを呼び出すだけでよく、接続の他の側面を考慮する必要はありません。  
  
## <a name="example"></a>例  
 次の例では、Validate および Execute メソッドで <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 名を検証し、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> メソッドを使用して Execute メソッド内に物理接続を確立する方法を示します。  
  
```csharp  
private string connectionManagerName = "";  
  
public string ConnectionManagerName  
{  
  get { return this.connectionManagerName; }  
  set { this.connectionManagerName = value; }  
}  
  
public override DTSExecResult Validate(  
  Connections connections, VariableDispenser variableDispenser,  
  IDTSComponentEvents componentEvents, IDTSLogging log)  
{  
  // If the connection manager exists, validation is successful;  
  // otherwise, fail validation.  
  try  
  {  
    ConnectionManager cm = connections[this.connectionManagerName];  
    return DTSExecResult.Success;  
  }  
  catch (System.Exception e)  
  {  
    componentEvents.FireError(0, "SampleTask", "Invalid connection manager.", "", 0);  
    return DTSExecResult.Failure;  
  }  
}  
  
public override DTSExecResult Execute(Connections connections,   
  VariableDispenser variableDispenser, IDTSComponentEvents componentEvents,   
  IDTSLogging log, object transaction)  
{  
  try  
  {  
    ConnectionManager cm = connections[this.connectionManagerName];  
    object connection = cm.AcquireConnection(transaction);  
    return DTSExecResult.Success;  
  }  
  catch (System.Exception exception)  
  {  
    componentEvents.FireError(0, "SampleTask", exception.Message, "", 0);  
    return DTSExecResult.Failure;  
  }  
}  
```  
  
```vb  
Private _connectionManagerName As String = ""  
  
Public Property ConnectionManagerName() As String  
  Get  
    Return Me._connectionManagerName  
  End Get  
  Set(ByVal Value As String)  
    Me._connectionManagerName = value  
  End Set  
End Property  
  
Public Overrides Function Validate( _  
  ByVal connections As Microsoft.SqlServer.Dts.Runtime.Connections, _  
  ByVal variableDispenser As Microsoft.SqlServer.Dts.Runtime.VariableDispenser, _  
  ByVal componentEvents As Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents, _  
  ByVal log As Microsoft.SqlServer.Dts.Runtime.IDTSLogging) _  
  As Microsoft.SqlServer.Dts.Runtime.DTSExecResult  
  
  ' If the connection manager exists, validation is successful;  
  ' otherwise fail validation.  
  Try  
    Dim cm As ConnectionManager = connections(Me._connectionManagerName)  
    Return DTSExecResult.Success  
  Catch e As System.Exception  
    componentEvents.FireError(0, "SampleTask", "Invalid connection manager.", "", 0)  
    Return DTSExecResult.Failure  
  End Try  
  
End Function  
  
Public Overrides Function Execute( _  
  ByVal connections As Microsoft.SqlServer.Dts.Runtime.Connections, _  
  ByVal variableDispenser As Microsoft.SqlServer.Dts.Runtime.VariableDispenser, _  
  ByVal componentEvents As Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents, _  
  ByVal log As Microsoft.SqlServer.Dts.Runtime.IDTSLogging, ByVal transaction As Object) _  
  As Microsoft.SqlServer.Dts.Runtime.DTSExecResult  
  
  Try  
    Dim cm As ConnectionManager = connections(Me._connectionManagerName)  
    Dim connection As Object = cm.AcquireConnection(transaction)  
    Return DTSExecResult.Success  
  Catch exception As System.Exception  
    componentEvents.FireError(0, "SampleTask", exception.Message, "", 0)  
    Return DTSExecResult.Failure  
  End Try  
  
End Function  
```  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; の接続](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [接続マネージャーを作成する](https://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  
