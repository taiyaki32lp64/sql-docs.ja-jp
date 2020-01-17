---
title: カスタム ログ プロバイダーのコーディング | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom log providers [Integration Services], coding
ms.assetid: 979a29ca-956e-4fdd-ab47-f06e84cead7a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7c6c5cdc269c757b8578314d39fd07f9f947a5e7
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71287147"
---
# <a name="coding-a-custom-log-provider"></a>カスタム ログ プロバイダーのコーディング

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase> 基本クラスを継承するクラスを作成し、<xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> 属性をそのクラスに適用したら、基本クラスのプロパティとメソッドの実装をオーバーライドして、カスタム機能を提供する必要があります。  
  
 カスタム ログ プロバイダーの実際のサンプルが必要であれば、「[カスタム ログ プロバイダー用ユーザー インターフェイスの開発](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-user-interface-for-a-custom-log-provider.md)」をご覧ください。  
  
## <a name="configuring-the-log-provider"></a>ログ プロバイダーの構成  
  
### <a name="initializing-the-log-provider"></a>ログ プロバイダーの初期化  
 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.InitializeLogProvider%2A> メソッドをオーバーライドして、接続のコレクションおよびイベント インターフェイスへの参照をキャッシュします。 キャッシュした参照は、後でログ プロバイダーの他のメソッドで使用できます。  
  
### <a name="using-the-configstring-property"></a>ConfigString プロパティの使用  
 デザイン時に、ログ プロバイダーは **[構成]** 列から構成情報を受け取ります。 この構成情報は、ログ プロバイダーの <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> プロパティに対応しています。 既定では、この列には任意の文字列情報を取得可能なテキスト ボックスが含まれます。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] に含まれているほとんどのログ プロバイダーは、このプロパティを使用して、外部データ ソースに接続するためにプロバイダーが使用する接続マネージャーの名前を格納します。 ログ プロバイダーで <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> プロパティを使用する場合は、<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Validate%2A> メソッドを使用して、このプロパティが正しく設定されていることを検証します。  
  
### <a name="validating-the-log-provider"></a>ログ プロバイダーの検証  
 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Validate%2A> メソッドをオーバーライドして、プロバイダーが正しく構成され、実行の準備ができていることを確認します。 通常、少なくとも <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> が正しく設定されていることを検証します。 ログ プロバイダーが <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Success> メソッドから <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Validate%2A> を返すまでは、実行を続行できません。  
  
 次のコード例では、接続マネージャーの名前が指定され、パッケージに接続マネージャーが存在し、接続マネージャーが <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Validate%2A> プロパティにファイル名を返すことを確認する、<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> の実装を示します。  
  
```csharp  
public override DTSExecResult Validate(IDTSInfoEvents infoEvents)  
{  
    if (this.ConfigString.Length == 0 || connections.Contains(ConfigString) == false)  
    {  
        infoEvents.FireError(0, "MyTextLogProvider", "The ConnectionManager " + ConfigString + " specified in the ConfigString property cannot be found in the collection.", "", 0);  
        return DTSExecResult.Failure;  
    }  
    else  
    {  
        string fileName = connections[ConfigString].AcquireConnection(null) as string;  
  
        if (fileName == null || fileName.Length == 0)  
        {  
            infoEvents.FireError(0, "MyTextLogProvider", "The ConnectionManager " + ConfigString + " specified in the ConfigString property cannot be found in the collection.", "", 0);  
            return DTSExecResult.Failure;  
        }  
    }  
    return DTSExecResult.Success;  
}  
```  
  
```vb  
Public Overrides Function Validate(ByVal infoEvents As IDTSInfoEvents) As DTSExecResult  
    If Me.ConfigString.Length = 0 Or connections.Contains(ConfigString) = False Then  
        infoEvents.FireError(0, "MyTextLogProvider", "The ConnectionManager " + ConfigString + " specified in the ConfigString property cannot be found in the collection.", "", 0)  
        Return DTSExecResult.Failure  
    Else   
        Dim fileName As String =  connections(ConfigString).AcquireConnectionCType(as string, Nothing)  
  
        If fileName = Nothing Or fileName.Length = 0 Then  
            infoEvents.FireError(0, "MyTextLogProvider", "The ConnectionManager " + ConfigString + " specified in the ConfigString property cannot be found in the collection.", "", 0)  
            Return DTSExecResult.Failure  
        End If  
    End If  
    Return DTSExecResult.Success  
End Function  
```  
  
### <a name="persisting-the-log-provider"></a>ログ プロバイダーの保存  
 通常、接続マネージャーに対して、カスタムの永続性を実装する必要はありません。 カスタムの永続性は、オブジェクトのプロパティで複合データ型が使用されている場合にのみ必要です。 詳細については、「[Integration Services 用のカスタム オブジェクトの開発](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)」を参照してください。  
  
## <a name="logging-with-the-log-provider"></a>ログ プロバイダーによるログ記録  
 すべてのログ プロバイダーがオーバーライドする必要のある実行時のメソッドには、<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>、<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A>、および <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A> の 3 つがあります。  
  
> [!IMPORTANT]  
>  単一のパッケージを検証および実行している間に、<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A> メソッドと <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A> メソッドは複数回呼び出されます。 カスタム コードで次のログを開いたり閉じたりすることにより、以前のログ エントリが上書きされることがないようにする必要があります。 テスト パッケージで検証イベントをログに記録することを選択した場合、最初にログに記録されるイベントは OnPreValidate です。最初にログに記録されているイベントが PackageStart である場合、最初の検証イベントが上書きされています。  
  
### <a name="opening-the-log"></a>ログを開く  
 ほとんどのログ プロバイダーは、ファイルやデータベースなどの外部データ ソースに接続し、パッケージの実行中に収集されるイベント情報を格納します。 ランタイム内の他のオブジェクトと同様に、外部データ ソースへの接続は、通常は接続マネージャー オブジェクトを使用して実行されます。  
  
 パッケージの実行の開始時に、<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A> メソッドが呼び出されます。このメソッドをオーバーライドし、外部データ ソースへの接続を確立します。  
  
 次のコード例では、<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A> メソッドが書き込むテキスト ファイルを開くログ プロバイダーを示します。 ここでは、<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> プロパティで指定されている接続マネージャーの <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> メソッドを呼び出すことによってファイルを開きます。  
  
```csharp  
public override void OpenLog()  
{  
    if(!this.connections.Contains(this.ConfigString))  
        throw new Exception("The ConnectionManager " + this.ConfigString + " does not exist in the Connections collection.");  
  
    this.connectionManager = connections[ConfigString];  
    string filePath = this.connectionManager.AcquireConnection(null) as string;  
  
    if(filePath == null || filePath.Length == 0)  
        throw new Exception("The ConnectionManager " + this.ConfigString + " is not a valid FILE ConnectionManager");  
  
    //  Create a StreamWriter to append to.  
    sw = new StreamWriter(filePath,true);  
  
    sw.WriteLine("Open log" + System.DateTime.Now.ToShortTimeString());  
}  
```  
  
```vb  
Public Overrides  Sub OpenLog()  
    If Not Me.connections.Contains(Me.ConfigString) Then  
        Throw New Exception("The ConnectionManager " + Me.ConfigString + " does not exist in the Connections collection.")  
    End If  
  
    Me.connectionManager = connections(ConfigString)  
    Dim filePath As String =  Me.connectionManager.AcquireConnectionCType(as string, Nothing)  
  
    If filePath = Nothing Or filePath.Length = 0 Then  
        Throw New Exception("The ConnectionManager " + Me.ConfigString + " is not a valid FILE ConnectionManager")  
    End If  
  
    '  Create a StreamWriter to append to.  
    sw = New StreamWriter(filePath,True)  
  
    sw.WriteLine("Open log" + System.DateTime.Now.ToShortTimeString())  
End Sub  
```  
  
### <a name="writing-log-entries"></a>ログ エントリの記述  
 パッケージ内のオブジェクトがいずれかのイベント インターフェイスで Fire\<event> メソッドを呼び出してイベントを発生させるたびに、<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> メソッドが呼び出されます。 各イベントを発生させるときは、イベントのコンテキスト情報に加えて、通常は説明のメッセージが使用されます。 ただし、<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> メソッドのすべての呼び出しに、すべてのメソッド パラメーターの情報が含まれているわけではありません。 たとえば、名前が説明になっている一部の標準イベントは MessageText を提供しません。また DataCode と DataBytes は、省略可能な補足情報のためのものです。  
  
 次のコード例では、<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> メソッドを実装し、前のセクションで開かれたストリームにイベントを書き込みます。  
  
```csharp  
public override void Log(string logEntryName, string computerName, string operatorName, string sourceName, string sourceID, string executionID, string messageText, DateTime startTime, DateTime endTime, int dataCode, byte[] dataBytes)  
{  
    sw.Write(logEntryName + ",");  
    sw.Write(computerName + ",");  
    sw.Write(operatorName + ",");  
    sw.Write(sourceName + ",");  
    sw.Write(sourceID + ",");  
    sw.Write(messageText + ",");  
    sw.Write(dataBytes + ",");  
    sw.WriteLine("");  
}  
```  
  
```vb  
Public Overrides  Sub Log(ByVal logEnTryName As String, ByVal computerName As String, ByVal operatorName As String, ByVal sourceName As String, ByVal sourceID As String, ByVal executionID As String, ByVal messageText As String, ByVal startTime As DateTime, ByVal endTime As DateTime, ByVal dataCode As Integer, ByVal dataBytes() As Byte)  
    sw.Write(logEnTryName + ",")  
    sw.Write(computerName + ",")  
    sw.Write(operatorName + ",")  
    sw.Write(sourceName + ",")  
    sw.Write(sourceID + ",")  
    sw.Write(messageText + ",")  
    sw.Write(dataBytes + ",")  
    sw.WriteLine("")  
End Sub  
```  
  
### <a name="closing-the-log"></a>ログを閉じる  
 パッケージ内のすべてのオブジェクトが実行を完了するか、またはパッケージがエラーのために停止したとき、パッケージ実行の最後に <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A> メソッドが呼び出されます。  
  
 次のコード例では、<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A> メソッドで開かれたファイル ストリームを閉じる <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A> メソッドの実装を示します。  
  
```csharp  
public override void CloseLog()  
{  
    if (sw != null)  
    {  
        sw.WriteLine("Close log" + System.DateTime.Now.ToShortTimeString());  
        sw.Close();  
    }  
}  
```  
  
```vb  
Public Overrides  Sub CloseLog()  
    If Not sw Is Nothing Then  
        sw.WriteLine("Close log" + System.DateTime.Now.ToShortTimeString())  
        sw.Close()  
    End If  
End Sub  
```  
 
## <a name="see-also"></a>参照  
 [カスタム ログ プロバイダーの作成](../../../integration-services/extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md)   
 [カスタム ログ プロバイダー用ユーザー インターフェイスの開発](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-user-interface-for-a-custom-log-provider.md)  
  
  
