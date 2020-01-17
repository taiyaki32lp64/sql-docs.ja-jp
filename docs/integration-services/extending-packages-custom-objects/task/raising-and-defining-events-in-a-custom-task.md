---
title: カスタム タスクでのイベントの発生と定義 | Microsoft Docs
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
- SSIS events, custom
- status information [SQL Server], task events
- custom tasks [Integration Services], events
- SSIS custom tasks, events
- IDTSComponentEvents interface
- events [Integration Services], custom
- events [Integration Services], runtime
- custom events [Integration Services]
- SSIS events, runtime
- IDTSEvents interface
ms.assetid: e0898aa1-e90c-4c4e-99d4-708a76efddfd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 461750eee78c631adef9b012b971c9bab60bf29f
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71286893"
---
# <a name="raising-and-defining-events-in-a-custom-task"></a>カスタム タスクでのイベントの発生と定義

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] ランタイム エンジンには、タスクを検証および実行する際の進行状況の状態を示す、イベントのコレクションが用意されています。 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> インターフェイスはこれらのイベントを定義し、<xref:Microsoft.SqlServer.Dts.Runtime.Executable.Validate%2A> および <xref:Microsoft.SqlServer.Dts.Runtime.Executable.Execute%2A> メソッドに対するパラメーターとして、タスクに渡されます。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> インターフェイスでは、<xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> によってタスクの代わりに発生するイベントのセットが別に定義されています。 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> は、検証および実行の前後にイベントを発生させます。これに対してタスクは、実行および検証中にイベントを発生させます。  
  
## <a name="creating-custom-events"></a>カスタム イベントの作成  
 カスタム タスクの開発者は、オーバーライドした <xref:Microsoft.SqlServer.Dts.Runtime.EventInfo> メソッドの実装に新しい <xref:Microsoft.SqlServer.Dts.Runtime.Task.InitializeTask%2A> を作成することにより、新しいカスタム イベントを定義できます。 <xref:Microsoft.SqlServer.Dts.Runtime.EventInfo> が作成されると、<xref:Microsoft.SqlServer.Dts.Runtime.EventInfos.Add%2A> メソッドを使用して **EventInfos** コレクションに追加されます。 次に、<xref:Microsoft.SqlServer.Dts.Runtime.EventInfos.Add%2A> メソッドのメソッド シグネチャを示します。  
  
 `public void Add(string eventName, string description, bool allowEventHandlers, string[] parameterNames, TypeCode[] parameterTypes, string[] parameterDescriptions);`  
  
 次のコード例では、カスタム タスクの **InitializeTask** メソッドを示します。ここでは、2 つのカスタム イベントが作成され、そのプロパティが設定されます。 次に、新しいイベントが <xref:Microsoft.SqlServer.Dts.Runtime.EventInfos> コレクションに追加されます。  
  
 最初のカスタム イベントの *eventName* は "**OnBeforeIncrement**" で、*description* は "**Fires after the initial value is updated**" です。 次のパラメーターの値は **true** であり、イベントを処理するために、イベント ハンドラーのコンテナーの作成を許可する必要があることを示します。 このイベント ハンドラーは、Package、Sequence、ForLoop、ForEachLoop などの他のコンテナーと同様、パッケージの構造およびサービスをタスクに提供するコンテナーです。 *allowEventHandlers* パラメーターが **true** の場合、そのイベント用に <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> オブジェクトが作成されます。 これで、イベント用に定義された任意のパラメーターが、<xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> の変数コレクション内の <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> で使用できます。  
  
```csharp  
public override void InitializeTask(Connections connections,  
   VariableDispenser variables, IDTSInfoEvents events,  
   IDTSLogging log, EventInfos eventInfos,  
   LogEntryInfos logEntryInfos, ObjectReferenceTracker refTracker)  
{  
    this.eventInfos = eventInfos;  
    string[] paramNames = new string[1];  
    TypeCode[] paramTypes = new TypeCode[1]{TypeCode.Int32};  
    string[] paramDescriptions = new string[1];  
  
    paramNames[0] = "InitialValue";  
    paramDescriptions[0] = "The value before it is incremented.";  
  
    this.eventInfos.Add("OnBeforeIncrement",   
      "Fires before the task increments the value.",  
      true,paramNames,paramTypes,paramDescriptions);  
    this.onBeforeIncrement = this.eventInfos["OnBeforeIncrement"];  
  
    paramDescriptions[0] = "The value after it has been incremented.";  
    this.eventInfos.Add("OnAfterIncrement",  
      "Fires after the initial value is updated.",  
      true,paramNames, paramTypes,paramDescriptions);  
    this.onAfterIncrement = this.eventInfos["OnAfterIncrement"];  
}  
```  
  
```vb  
Public Overrides Sub InitializeTask(ByVal connections As Connections, _  
ByVal variables As VariableDispenser, ByVal events As IDTSInfoEvents, _  
ByVal log As IDTSLogging, ByVal eventInfos As EventInfos, _  
ByVal logEntryInfos As LogEntryInfos, ByVal refTracker As ObjectReferenceTracker)   
  
    Dim paramNames(0) As String  
    Dim paramTypes(0) As TypeCode = {TypeCode.Int32}  
    Dim paramDescriptions(0) As String  
  
    Me.eventInfos = eventInfos  
  
    paramNames(0) = "InitialValue"  
    paramDescriptions(0) = "The value before it is incremented."  
  
    Me.eventInfos.Add("OnBeforeIncrement", _  
      "Fires before the task increments the value.", _  
      True, paramNames, paramTypes, paramDescriptions)  
    Me.onBeforeIncrement = Me.eventInfos("OnBeforeIncrement")  
  
    paramDescriptions(0) = "The value after it has been incremented."  
    Me.eventInfos.Add("OnAfterIncrement", _  
      "Fires after the initial value is updated.", True, _  
      paramNames, paramTypes, paramDescriptions)  
    Me.onAfterIncrement = Me.eventInfos("OnAfterIncrement")  
  
End Sub  
```  
  
## <a name="raising-custom-events"></a>カスタム イベントの発生  
 カスタム イベントは、<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireCustomEvent%2A> メソッドを呼び出すことにより発生します。 次のコード行では、カスタム イベントが発生します。  
  
```csharp  
componentEvents.FireCustomEvent(this.onBeforeIncrement.Name,  
   this.onBeforeIncrement.Description, ref arguments,  
   null, ref bFireOnBeforeIncrement);  
```  
  
```vb  
componentEvents.FireCustomEvent(Me.onBeforeIncrement.Name, _  
Me.onBeforeIncrement.Description, arguments, _  
Nothing,  bFireOnBeforeIncrement)  
```  
  
## <a name="sample"></a>サンプル  
 次の例では、**InitializeTask** メソッドでカスタム イベントを定義し、<xref:Microsoft.SqlServer.Dts.Runtime.EventInfos> コレクションに追加するタスクを示します。このタスクは、次に **Execute** メソッドを呼び出して、<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireCustomEvent%2A> メソッドでカスタム イベントを発生させます。  
  
```csharp  
[DtsTask(DisplayName = "CustomEventTask")]  
    public class CustomEventTask : Task  
    {  
        public override DTSExecResult Execute(Connections connections,   
          VariableDispenser variableDispenser, IDTSComponentEvents componentEvents,  
           IDTSLogging log, object transaction)  
        {  
            bool fireAgain;  
            object[] args = new object[1] { "The value of the parameter." };  
            componentEvents.FireCustomEvent( "MyCustomEvent",   
              "Firing the custom event.", ref args,  
              "CustomEventTask" , ref fireAgain );  
            return DTSExecResult.Success;  
        }  
  
        public override void InitializeTask(Connections connections,  
          VariableDispenser variableDispenser, IDTSInfoEvents events,  
          IDTSLogging log, EventInfos eventInfos,  
          LogEntryInfos logEntryInfos, ObjectReferenceTracker refTracker)  
        {  
            string[] names = new string[1] {"Parameter1"};  
            TypeCode[] types = new TypeCode[1] {TypeCode.String};  
            string[] descriptions = new string[1] {"Parameter description." };  
  
            eventInfos.Add("MyCustomEvent",  
             "Fires when my interesting event happens.",  
             true, names, types, descriptions);  
  
        }  
   }  
```  
  
```vb  
<DtsTask(DisplayName = "CustomEventTask")> _   
    Public Class CustomEventTask  
     Inherits Task  
        Public Overrides Function Execute(ByVal connections As Connections, _  
          ByVal variableDispenser As VariableDispenser, _  
          ByVal componentEvents As IDTSComponentEvents, _  
          ByVal log As IDTSLogging, ByVal transaction As Object) _  
          As DTSExecResult  
  
            Dim fireAgain As Boolean  
            Dim args() As Object =  New Object(1) {"The value of the parameter."}  
  
            componentEvents.FireCustomEvent("MyCustomEvent", _  
              "Firing the custom event.", args, _  
              "CustomEventTask" ,  fireAgain)  
            Return DTSExecResult.Success  
        End Function  
  
        Public Overrides  Sub InitializeTask(ByVal connections As Connections, _  
          ByVal variableDispenser As VariableDispenser,  
          ByVal events As IDTSInfoEvents,  
          ByVal log As IDTSLogging, ByVal eventInfos As EventInfos, ByVal logEnTryInfos As LogEnTryInfos, ByVal refTracker As ObjectReferenceTracker)  
  
            Dim names() As String =  New String(1) {"Parameter1"}  
            Dim types() As TypeCode =  New TypeCode(1) {TypeCode.String}  
            Dim descriptions() As String =  New String(1) {"Parameter description."}  
  
            eventInfos.Add("MyCustomEvent", _  
              "Fires when my interesting event happens.", _  
              True, names, types, descriptions)  
  
        End Sub  
  
    End Class  
```  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; のイベント ハンドラー](../../../integration-services/integration-services-ssis-event-handlers.md)   
 [パッケージにイベント ハンドラーを追加する](https://msdn.microsoft.com/library/5e56885d-8658-480a-bed9-3f2f8003fd78)  
  
  
