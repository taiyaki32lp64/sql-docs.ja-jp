---
title: スクリプト コンポーネントのオブジェクト モデルについて | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], object model
ms.assetid: 2a0aae82-39cc-4423-b09a-72d2f61033bd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: aa6235337aab70ed826a5507e7bd8ff2a45c4636
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71286588"
---
# <a name="understanding-the-script-component-object-model"></a>スクリプト コンポーネントのオブジェクト モデルについて

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  「[スクリプト コンポーネントのコーディングおよびデバッグ](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)」で説明したように、スクリプト コンポーネント プロジェクトには、次の 3 つのプロジェクト アイテムがあります。  
  
1.  **ScriptMain** アイテム。**ScriptMain** クラスを含み、ここにカスタム コードを記述します。 **ScriptMain** クラスは **UserComponent** クラスから継承されます。  
  
2.  **ComponentWrapper** アイテム。**UserComponent** クラスを含みます。これは <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> のインスタンスで、データの処理やパッケージとのやり取りで使用するメソッドとプロパティが含まれています。 **ComponentWrapper** アイテムにも、**Connections** と **Variables** コレクション クラスが含まれています。  
  
3.  **BufferWrapper** アイテム。各入力および各出力に対して <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> から継承されるクラス、および各列に対する型指定されたプロパティが含まれています。  
  
 **ScriptMain** アイテムにコードを記述する際には、このトピックで説明するオブジェクト、メソッド、およびプロパティを使用します。 ここで一覧されているすべてのメソッドを各コンポーネントが使用するわけではありませんが、使用される場合は、ここで示した順序で使用されます。  
  
 基本クラス <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> には、ここで説明しているメソッドのコードは実装されていません。 したがって、メソッド独自の実装に基本クラスの実装の呼び出しを追加する必要はありませんが、追加した場合でも問題は生じません。  
  
 特定の種類のスクリプト コンポーネントで、これらのクラスのメソッドおよびプロパティを使用する方法については、セクション「[その他のスクリプト コンポーネントの例](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)」をご覧ください。 サンプルについてのトピックでは、完全なコード例も示します。  
  
## <a name="acquireconnections-method"></a>AcquireConnections メソッド  
 通常、変換元および変換先は外部データ ソースに接続する必要があります。 基本クラス <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A> の <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> メソッドをオーバーライドして、適切な接続マネージャーから、接続または接続情報を取得します。  
  
 次の例は、ADO.NET 接続マネージャーから **System.Data.SqlClient.SqlConnection** を返します。  
  
```vb  
Dim connMgr As IDTSConnectionManager100  
Dim sqlConn As SqlConnection  
  
Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
    connMgr = Me.Connections.MyADONETConnection  
    sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
End Sub  
```  
  
 次の例は、フラット ファイル接続マネージャーから完全パスおよびファイル名を返し、**System.IO.StreamReader** を使用してこのファイルを開きます。  
  
```vb  
Private textReader As StreamReader  
Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
    Dim connMgr As IDTSConnectionManager100 = _  
        Me.Connections.MyFlatFileSrcConnectionManager  
    Dim exportedAddressFile As String = _  
        CType(connMgr.AcquireConnection(Nothing), String)  
    textReader = New StreamReader(exportedAddressFile)  
  
End Sub  
```  
  
## <a name="preexecute-method"></a>PreExecute メソッド  
 データの行の処理を開始する前に 1 回だけ実行する必要のある処理がある場合は、基本クラス <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PreExecute%2A> の <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> メソッドをオーバーライドします。 たとえば、データの各行をデータ ソースに挿入するために変換先が使用するパラメーター化コマンドを、変換先に設定することができます。  
  
```vb  
    Dim sqlConn As SqlConnection  
    Dim sqlCmd As SqlCommand  
    Dim sqlParam As SqlParameter  
...  
    Public Overrides Sub PreExecute()  
  
        sqlCmd = New SqlCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
            "VALUES(@addressid, @city)", sqlConn)  
        sqlParam = New SqlParameter("@addressid", SqlDbType.Int)  
        sqlCmd.Parameters.Add(sqlParam)  
        sqlParam = New SqlParameter("@city", SqlDbType.NVarChar, 30)  
        sqlCmd.Parameters.Add(sqlParam)  
  
    End Sub  
```  
  
```csharp  
SqlConnection sqlConn;   
SqlCommand sqlCmd;   
SqlParameter sqlParam;   
  
public override void PreExecute()   
{   
  
    sqlCmd = new SqlCommand("INSERT INTO Person.Address2(AddressID, City) " + "VALUES(@addressid, @city)", sqlConn);   
    sqlParam = new SqlParameter("@addressid", SqlDbType.Int);   
    sqlCmd.Parameters.Add(sqlParam);   
    sqlParam = new SqlParameter("@city", SqlDbType.NVarChar, 30);   
    sqlCmd.Parameters.Add(sqlParam);   
  
}  
```  
  
## <a name="processing-inputs-and-outputs"></a>入力および出力の処理  
  
### <a name="processing-inputs"></a>入力の処理  
 変換または変換先として構成されたスクリプト コンポーネントには、1 つの入力があります。  
  
#### <a name="what-the-bufferwrapper-project-item-provides"></a>プロジェクト アイテム BufferWrapper が提供する機能  
 構成したコンポーネントの入力ごとに、プロジェクト アイテム **BufferWrapper** には、<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> から派生した、入力と同じ名前のクラスがあります。 各入力バッファー クラスには、次のプロパティ、関数、およびメソッドが含まれています。  
  
-   選択された各入力列の、型指定された名前付きのアクセサー プロパティ。 これらのプロパティが読み取り専用か読み取り/書き込み可能かどうかは、 **[スクリプト変換エディター]** の **[入力列]** ページで、列に対して指定され **[使用法の種類]** によって決まります。  
  
-   選択された各入力列の **\<column>_IsNull** プロパティ。 このプロパティが読み取り専用か読み取り/書き込み可能かどうかも、列に対して指定された **[使用法の種類]** によって決まります。  
  
-   設定された各出力の **DirectRowTo\<outputbuffer>** メソッド。 このメソッドは、行をフィルター選択して、同じ **ExclusionGroup** 内の複数の出力のいずれかに行を出力する場合に使用します。  
  
-   次の入力行を取得するための **NextRow** 関数、およびデータの最後のバッファーが処理されたかどうかを確認するための **EndOfRowset** 関数。 通常、基本クラス **UserComponent** に実装された入力処理メソッドを使用する場合、この関数は必要はありません。 次のセクションでは、基本クラス **UserComponent** について詳細に説明します。  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>プロジェクト アイテム ComponentWrapper が提供する機能  
 プロジェクト アイテム ComponentWrapper には、<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> から派生する **UserComponent** という名前のクラスがあります。 また、カスタム コードを記述する **ScriptMain** クラスは、**UserComponent** から派生します。 **UserComponent** クラスには、次のメソッドが含まれています。  
  
-   **ProcessInput** メソッドをオーバーライドして実装したメソッド。 これは、データ フロー エンジンが実行時に **PreExecute** メソッドの次に呼び出すメソッドで、繰り返し呼び出される場合があります。 **ProcessInput** は **\<inputbuffer>_ProcessInput** メソッドに処理を渡します。 次に **ProcessInput** メソッドは入力バッファーが末尾に達しているかどうかを確認し、達している場合は、オーバーライド可能な **FinishOutputs** メソッドとプライベート メソッド **MarkOutputsAsFinished** を呼び出します。 **MarkOutputsAsFinished** メソッドは、次に最後の出力バッファーの **SetEndOfRowset** を呼び出します。  
  
-   **\<inputbuffer>_ProcessInput** メソッドのオーバーライド可能な実装。 この既定の実装では、単に各入力行の間をループし、 **\<inputbuffer>_ProcessInputRow** を呼び出します。  
  
-   **\<inputbuffer>_ProcessInputRow** メソッドのオーバーライド可能な実装。 既定の実装では、空のままです。 このメソッドは、カスタム データ処理コードを記述するために、通常はオーバーライドして使用します。  
  
#### <a name="what-your-custom-code-should-do"></a>カスタム コードとして組み込むべき機能  
 **ScriptMain** クラスの入力を処理するには、次のメソッドを使用できます。  
  
-   入力行が渡されるたびにそのデータを処理するには、 **\<inputbuffer>_ProcessInputRow** をオーバーライドします。  
  
-   入力行をループするときに追加の処理を行う必要がある場合にのみ、 **\<inputbuffer>_ProcessInput** をオーバーライドします (たとえば、すべての行が処理された後に他のアクションを実行するために **EndOfRowset** をテストする必要がある場合)。行の処理を実行するには、 **\<inputbuffer>_ProcessInputRow** を呼び出します。  
  
-   出力を閉じる前に、出力に対して何らかの処理を行う場合は、**FinishOutputs** をオーバーライドします。  
  
 **ProcessInput** メソッドは、これらのメソッドが適切な時点で確実に呼び出されるようにするものです。  
  
### <a name="processing-outputs"></a>出力の処理  
 変換元または変換として構成されたスクリプト コンポーネントには、1 つ以上の出力があります。  
  
#### <a name="what-the-bufferwrapper-project-item-provides"></a>プロジェクト アイテム BufferWrapper が提供する機能  
 構成したコンポーネントの出力ごとに、プロジェクト アイテム BufferWrapper には、<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> から派生した、出力と同じ名前のクラスがあります。 各出力バッファー クラスには、次のプロパティおよびメソッドが含まれています。  
  
-   各出力列の、名前付きで型指定された、書き込み専用のアクセサー プロパティ。  
  
-   選択された各出力列の、書き込み専用の **\<column>_IsNull** プロパティ。列の値を **null** に設定するために使用できます。  
  
-   空の新しい行を出力バッファーに追加するための **AddRow** メソッド。  
  
-   データ フロー エンジンに対し、これ以上データのバッファーがないことを知らせるための **SetEndOfRowset** メソッド。 現在のバッファーが、データの最後のバッファーであるかどうかを確認するための **EndOfRowset** 関数もあります。 通常、基本クラス **UserComponent** に実装された出力処理メソッドを使用する場合、この関数は必要はありません。  
  
#### <a name="what-the-componentwrapper-project-item-provides"></a>プロジェクト アイテム ComponentWrapper が提供する機能  
 プロジェクト アイテム ComponentWrapper には、<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> から派生する **UserComponent** という名前のクラスがあります。 また、カスタム コードを記述する **ScriptMain** クラスは、**UserComponent** から派生します。 **UserComponent** クラスには、次のメソッドが含まれています。  
  
-   **PrimeOutput** メソッドをオーバーライドして実装したメソッド。 実行時、データ フロー エンジンは、このメソッドを **ProcessInput** の前に 1 回だけ呼び出します。 **PrimeOutput** は **CreateNewOutputRows** メソッドに処理を渡します。 コンポーネントが変換元の場合 (つまりコンポーネントに入力がない場合)、**PrimeOutput** はオーバーライド可能な **FinishOutputs** メソッドとプライベート メソッド **MarkOutputsAsFinished** を呼び出します。 **MarkOutputsAsFinished** メソッドは、最後の出力バッファーの **SetEndOfRowset** を呼び出します。  
  
-   **CreateNewOutputRows** メソッドのオーバーライド可能な実装。 既定の実装では、空のままです。 このメソッドは、カスタム データ処理コードを記述するために、通常はオーバーライドして使用します。  
  
#### <a name="what-your-custom-code-should-do"></a>カスタム コードとして組み込むべき機能  
 **ScriptMain** クラスの出力を処理するには、次のメソッドを使用できます。  
  
-   入力行を処理する前に出力行を追加して設定できる場合にのみ、**CreateNewOutputRows** をオーバーライドします。 たとえば、**CreateNewOutputRows** を変換元に使用することはできますが、非同期出力型の変換では、入力データの処理中または処理後に **AddRow** を呼び出す必要があります。  
  
-   出力を閉じる前に、出力に対して何らかの処理を行う場合は、**FinishOutputs** をオーバーライドします。  
  
 **PrimeOutput** メソッドは、これらのメソッドが適切な時点で確実に呼び出されるようにするものです。  
  
## <a name="postexecute-method"></a>PostExecute メソッド  
 データの行を処理した後に 1 回だけ実行する必要のある処理がある場合は、基本クラス <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PostExecute%2A> の <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> メソッドをオーバーライドします。 たとえば、変換元でデータをデータ フローに読み込むために使用した **System.Data.SqlClient.SqlDataReader** を閉じることができます。  
  
> [!IMPORTANT]  
>  **ReadWriteVariables** のコレクションは、**PostExecute** メソッド内でのみ使用できます。 したがって、データ行を処理するたびにパッケージ変数の値を直接増やすことはできません。 このような場合、ローカル変数の値を増やし、すべてのデータが処理された後で、**PostExecute** メソッド内でパッケージ変数の値をローカル変数の値に設定します。  
  
## <a name="releaseconnections-method"></a>ReleaseConnections メソッド  
 通常、変換元および変換先は外部データ ソースに接続する必要があります。 基本クラス <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReleaseConnections%2A> の <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> メソッドをオーバーライドして、以前に <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.AcquireConnections%2A> メソッドで開いた接続を閉じ、解放します。  
  
```vb  
    Dim connMgr As IDTSConnectionManager100  
...  
    Public Overrides Sub ReleaseConnections()  
  
        connMgr.ReleaseConnection(sqlConn)  
  
    End Sub  
```  
  
```csharp  
IDTSConnectionManager100 connMgr;  
  
public override void ReleaseConnections()  
{  
  
    connMgr.ReleaseConnection(sqlConn);  
  
}  
```  
  
## <a name="see-also"></a>参照  
 [スクリプト コンポーネント エディターでのスクリプト コンポーネントの構成](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)   
 [スクリプト コンポーネントのコーディングおよびデバッグ](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  
