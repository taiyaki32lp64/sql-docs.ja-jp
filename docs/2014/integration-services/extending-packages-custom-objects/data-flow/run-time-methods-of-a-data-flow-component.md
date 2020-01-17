---
title: データ フロー コンポーネントの実行時のメソッド | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- run-time [Integration Services]
- data flow components [Integration Services], run-time methods
ms.assetid: fd9e4317-18dd-43af-bbdc-79db32183ac4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e107660073716019f48def8578a424ead92abf32
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768638"
---
# <a name="run-time-methods-of-a-data-flow-component"></a>データ フロー コンポーネントの実行時のメソッド
  実行時に、データ フロー タスクは、コンポーネントの順序の確認、実行プランの準備、および作業プランを実行するワーカー スレッドのプールの管理を行います。 タスクは、データの行を変換元から読み込み、変換を使用して処理し、変換先に保存します。  
  
## <a name="sequence-of-method-execution"></a>メソッドの実行順序  
 データ フロー コンポーネントの実行中に、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 基本クラス内のメソッドのサブセットが呼び出されます。 呼び出されるメソッドとその順序は常に同じです。ただし、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> および <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> メソッドは例外です。 これら 2 つのメソッドは、コンポーネントの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100> および <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> オブジェクトの存在と構成に基づいて呼び出されます。  
  
 次の一覧では、コンポーネントの実行中に呼び出される順にメソッドを示します。 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> は、常に <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> の前に呼び出されます。  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrepareForExecute%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PostExecute%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Cleanup%2A>  
  
### <a name="primeoutput-method"></a>PrimeOutput メソッド  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100.PrimeOutput%2A> メソッドは、コンポーネントに少なくとも 1 つの出力があり、その出力が <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> オブジェクトを介して下流コンポーネントにアタッチされ、出力の <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A> プロパティが 0 の場合に呼び出されます。 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100.PrimeOutput%2A> メソッドは、非同期出力型の変換元コンポーネントと変換の場合に呼び出されます。 後述の <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> メソッドとは異なり、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> メソッドは必要とされる各コンポーネントに対して 1 回だけ呼び出されます。  
  
### <a name="processinput-method"></a>ProcessInput メソッド  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100.ProcessInput%2A> メソッドは、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> オブジェクトによって上流コンポーネントにアタッチされる入力が少なくとも 1 つあるコンポーネントに対して呼び出されます。 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100.ProcessInput%2A> メソッドは、同期出力型の変換先コンポーネントと変換に対して呼び出されます。 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> は、処理する行が上流コンポーネントから渡されなくなるまで繰り返し呼び出されます。  
  
## <a name="working-with-inputs-and-outputs"></a>入力と出力の処理  
 データ フロー コンポーネントは、実行時に次のタスクを実行します。  
  
-   変換コンポーネントは行を追加します。  
  
-   同期出力型の変換コンポーネントは、変換元コンポーネントから渡される行を受け取ります。  
  
-   非同期出力型の変換コンポーネントは、行を受け取って行を追加します。  
  
-   変換先コンポーネントは、行を受け取って変換先に読み込みます。  
  
 実行中、データ フロー タスクは、コンポーネントのシーケンスの出力列コレクションで定義されたすべての列を含む <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> オブジェクトを割り当てます。 たとえば、データ フロー シーケンス内の 4 つの各コンポーネントが 1 つの出力列をその出力列コレクションに追加した場合、各コンポーネントに提供されているバッファーには 4 つの列、つまりコンポーネントごとに 1 つの出力列が格納されます。 この動作のため、使用しない列を含むバッファーをコンポーネントが受け取る場合があります。  
  
 コンポーネントが受け取るバッファーにはコンポーネントが使用しない列が含まれる場合もあるので、データ フロー タスクがコンポーネントに提供するバッファー内のコンポーネントの入力および出力列のコレクションから、使用する列を検索する必要があります。 これを行うには、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> プロパティの <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> メソッドを使用します。 パフォーマンスの理由により、このタスクは通常、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> や <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> ではなく、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> メソッドで実行します。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> は <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> および <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> メソッドの前に呼び出され、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> がコンポーネントで使用できるようになった後に初めてコンポーネントで作業を実行できます。 このメソッドの実行中、コンポーネントはバッファー内の列を検索してこの情報を内部的に格納し、列が <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> または <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> メソッドのどちらかで使用できるようにします。  
  
 次のコード例では、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> で、同期出力型の変換コンポーネントがバッファー内の入力列を検索する方法を示します。  
  
```csharp  
private int []bufferColumnIndex;  
public override void PreExecute()  
{  
    IDTSInput100 input = ComponentMetaData.InputCollection[0];  
    bufferColumnIndex = new int[input.InputColumnCollection.Count];  
  
    for( int x=0; x < input.InputColumnCollection.Count; x++)  
    {  
        IDTSInputColumn100 column = input.InputColumnCollection[x];  
        bufferColumnIndex[x] = BufferManager.FindColumnByLineageID( input.Buffer, column.LineageID);  
    }  
}  
```  
  
```vb  
Dim bufferColumnIndex As Integer()  
  
    Public Overrides Sub PreExecute()  
  
        Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)  
  
        ReDim bufferColumnIndex(input.InputColumnCollection.Count)  
  
        For x As Integer = 0 To input.InputColumnCollection.Count  
  
            Dim column As IDTSInputColumn100 = input.InputColumnCollection(x)  
            bufferColumnIndex(x) = BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID)  
  
        Next  
  
    End Sub  
```  
  
### <a name="adding-rows"></a>行の追加  
 コンポーネントは、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> オブジェクトに行を追加することで、下流コンポーネントに行を提供します。 データ フロー タスクは、下流コンポーネントに接続される <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> オブジェクトごとに 1 つずつ、出力バッファーの配列を <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> メソッドに渡すパラメーターとして提供します。 非同期出力型の変換元コンポーネントと変換コンポーネントは、行をバッファーに追加し、行の追加が完了したら <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetEndOfRowset%2A> メソッドを呼び出します。 データ フロー タスクは、コンポーネントに提供する出力バッファーを管理し、バッファーがいっぱいになると、バッファー内の行を自動的に次のコンポーネントに移動します。 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> メソッドは、繰り返し呼び出される <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> メソッドと異なり、コンポーネントごとに 1 回ずつ呼び出されます。  
  
 次のコード例では、コンポーネントが <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> メソッドで出力バッファーに行を追加し、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetEndOfRowset%2A> メソッドを呼び出す方法を示します。  
  
```csharp  
public override void PrimeOutput( int outputs, int []outputIDs,PipelineBuffer []buffers)  
{  
    for( int x=0; x < outputs; x++ )  
    {  
        IDTSOutput100 output = ComponentMetaData.OutputCollection.GetObjectByID( outputIDs[x]);  
        PipelineBuffer buffer = buffers[x];  
  
        // TODO: Add rows to the output buffer.  
    }  
    foreach( PipelineBuffer buffer in buffers )  
    {  
        /// Notify the data flow task that no more rows are coming.  
        buffer.SetEndOfRowset();  
    }  
}  
```  
  
```vb  
public overrides sub PrimeOutput( outputs as Integer , outputIDs() as Integer ,buffers() as PipelineBuffer buffers)  
  
    For x As Integer = 0 To outputs.MaxValue  
  
        Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection.GetObjectByID(outputIDs(x))  
        Dim buffer As PipelineBuffer = buffers(x)  
  
        ' TODO: Add rows to the output buffer.  
  
    Next  
  
    For Each buffer As PipelineBuffer In buffers  
  
        ' Notify the data flow task that no more rows are coming.  
        buffer.SetEndOfRowset()  
  
    Next  
  
End Sub  
```  
  
 出力バッファーに行を追加するコンポーネントの開発の詳細については、「[カスタム変換元コンポーネントの開発](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)」および「[非同期出力型のカスタム変換コンポーネントの開発](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)」を参照してください。  
  
### <a name="receiving-rows"></a>行の受信  
 コンポーネントは、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> オブジェクト内の上流コンポーネントから行を受け取ります。 データ フロー タスクでは、上流コンポーネントがデータ フローに追加する行が含まれる <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> オブジェクトが、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> メソッドに渡されるパラメーターとして用意されています。 この入力バッファーを使用して、バッファー内の行および列を検証して変更することはできますが、行を追加したり削除することはできません。 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> メソッドは、渡されるバッファーがなくなるまで繰り返し呼び出されます。 このメソッドが最後に呼び出されたとき、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> プロパティは `true` になります。 バッファーを次の行に進める <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.NextRow%2A> メソッドを使用することにより、バッファー内の行のコレクションを反復処理できます。 バッファーがコレクション内の最後の行にある場合、このメソッドは `false` を返します。 データの最後の行が処理された後にさらに操作を実行する必要がある場合を除き、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> プロパティを確認する必要はありません。  
  
 次のテキストは、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.NextRow%2A> メソッドと <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> プロパティを使用する正しいパターンを示しています。  
  
 `while (buffer.NextRow())`  
  
 `{`  
  
 `// Do something with each row.`  
  
 `}`  
  
 `if (buffer.EndOfRowset)`  
  
 `{`  
  
 `// Optionally, do something after all rows have been processed.`  
  
 `}`  
  
 次のコード例では、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> メソッドの実行中に、コンポーネントが入力バッファー内の行を処理する方法を示します。  
  
```csharp  
public override void ProcessInput( int inputID, PipelineBuffer buffer )  
{  
    {  
        IDTSInput100 input = ComponentMetaData.InputCollection.GetObjectByID(inputID);  
        while( buffer.NextRow())  
        {  
            // TODO: Examine the columns in the current row.  
        }  
}  
```  
  
```vb  
Public Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)  
  
        Dim input As IDTSInput100 = ComponentMetaData.InputCollection.GetObjectByID(inputID)  
        While buffer.NextRow() = True  
  
            ' TODO: Examine the columns in the current row.  
        End While  
  
End Sub  
```  
  
 入力バッファー内の行を受け取るコンポーネントの開発の詳細については、「[カスタム変換先コンポーネントの開発](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)」および「[同期出力型のカスタム変換コンポーネントの開発](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)」を参照してください。  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>関連項目  
 [データ フロー コンポーネントのデザイン時のメソッド](design-time-methods-of-a-data-flow-component.md)  
  
  
