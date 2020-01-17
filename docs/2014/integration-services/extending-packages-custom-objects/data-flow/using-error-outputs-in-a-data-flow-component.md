---
title: データ フロー コンポーネントでのエラー出力の使用 | Microsoft Docs
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
- errors [Integration Services], alternative outputs
- synchronous error outputs [Integration Services]
- alternative error outputs [Integration Services]
- custom data flow components [Integration Services], error outputs
- data flow components [Integration Services], error outputs
- populating error columns [Integration Services]
- redirecting error output [Integration Services]
- error outputs [Integration Services]
- asynchronous error outputs [Integration Services]
ms.assetid: a2a3e7c8-1de2-45b3-97fb-60415d3b0934
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a330fea71ce84e7af82dd2bd92fc2e14f0883a0c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62896052"
---
# <a name="using-error-outputs-in-a-data-flow-component"></a>データ フロー コンポーネントでのエラー出力の使用
  エラー出力と呼ばれる特殊な <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> オブジェクトをコンポーネントに追加すると、コンポーネントは、実行中に処理できない行をリダイレクトできます。 コンポーネントで発生する可能性のある問題は、通常、エラーまたは切り捨てに分類され、各コンポーネントに固有です。 エラー出力を提供するコンポーネントを使用すると、エラー行を結果セットからフィルター選択したり、問題が発生したときにコンポーネントを失敗させたり、エラーを無視して処理を続行するなど、エラー条件を柔軟に処理できます。  
  
 コンポーネントにエラー出力を実装してサポートするには、まず、コンポーネントの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.UsesDispositions%2A> プロパティを `true` に設定する必要があります。 次に、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.IsErrorOut%2A> プロパティを `true` に設定した出力を、コンポーネントに追加する必要があります。 最後に、エラーまたは切り捨てが発生したときに、行をエラー出力にリダイレクトするためのコードを、そのコンポーネントに格納する必要があります。 このトピックでは、これら 3 つの手順、および同期型のエラー出力と非同期型のエラー出力の違いについて説明します。  
  
## <a name="creating-an-error-output"></a>エラー出力の作成  
 エラー出力を作成するには、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputCollection100.New%2A> の <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.OutputCollection%2A> メソッドを呼び出し、新しい出力の <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.IsErrorOut%2A> プロパティを `true` に設定します。 出力が非同期型の場合、出力に対して他の処理を行うことはできません。 出力が同期型で、同じ入力に対して同期する別の出力が存在する場合、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.ExclusionGroup%2A> および <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A> プロパティも設定する必要があります。 両方のプロパティの値は、同じ入力に対して同期する別の出力の値と同じである必要があります。 これらのプロパティの値が 0 でない値に設定されていない場合、入力で提供された行は、その入力に対して同期する両方の出力に送信されます。  
  
 コンポーネントの実行中にエラーまたは切り捨てが発生すると、エラーが発生した入力または出力、あるいは入力列または出力列の <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100.ErrorRowDisposition%2A> および <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100.TruncationRowDisposition%2A> プロパティの設定に基づいて、処理が続行されます。 これらのプロパティの値は、既定で <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition.RD_NotUsed> に設定する必要があります。 コンポーネントのエラー出力が下流コンポーネントに接続されている場合、そのコンポーネントのユーザーがこのプロパティを設定することで、コンポーネントによるエラーまたは切り捨ての処理方法をユーザーが制御できます。  
  
## <a name="populating-error-columns"></a>エラー列の設定  
 エラー出力が作成されると、データ フロー タスクは 2 つの列を出力列のコレクションに自動的に追加します。 これらの列は、エラーまたは切り捨てが発生した列の ID を指定するため、および、コンポーネント固有のエラー コードを提供するために、コンポーネントが使用します。 これらの列は自動的に生成されますが、列に含まれる値はコンポーネントが設定する必要があります。  
  
 これらの列の値を設定するために使用されるメソッドは、エラー出力が同期型か非同期型かによって異なります。 同期出力型のコンポーネントは、次のセクションで詳細を説明するように <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.DirectErrorRow%2A> メソッドを呼び出し、エラー コードとエラー列の値をパラメーターとして提供します。 非同期出力型のコンポーネントでは、2 つの方法でこれらの列の値を設定できます。 つまり、出力バッファーの <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetErrorInfo%2A> メソッドを呼び出して値を設定するか、または <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> を使用してバッファー内のエラー列を探し、列の値を直接設定します。 ただし、列の名前や出力列のコレクションでの列の位置は変更される場合があるため、後者の方法では信頼性が低い可能性があります。 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetErrorInfo%2A> メソッドを使用すると、手動でエラー列を探さなくても自動的にその値を設定できます。  
  
 特定のエラー コードに対応するエラーの説明を取得する必要がある場合、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> インターフェイスの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> メソッドを使用できます。このメソッドは、コンポーネントの <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> プロパティから使用できます。  
  
 次のコード例では、1 つの入力と、2 つの出力 (エラー出力を含む) のあるコンポーネントを示します。 最初の例では、入力に対して同期するエラー出力の作成方法を示します。 2 番目の例では、非同期型のエラー出力の作成方法を示します。  
  
```csharp  
public override void ProvideComponentProperties()  
{  
    // Specify that the component has an error output.  
    ComponentMetaData.UsesDispositions = true;  
    // Create the input.  
    IDTSInput100 input = ComponentMetaData.InputCollection.New();  
    input.Name = "Input";  
    input.ErrorRowDisposition = DTSRowDisposition.RD_NotUsed;  
    input.ErrorOrTruncationOperation = "A string describing the possible error or truncation that may occur during execution.";  
  
    // Create the default output.  
    IDTSOutput100 output = ComponentMetaData.OutputCollection.New();  
    output.Name = "Output";  
    output.SynchronousInputID = input.ID;  
    output.ExclusionGroup = 1;  
  
    // Create the error output.  
    IDTSOutput100 errorOutput = ComponentMetaData.OutputCollection.New();  
    errorOutput.IsErrorOut = true;  
    errorOutput.Name = "ErrorOutput";  
    errorOutput.SynchronousInputID = input.ID;  
    errorOutput.ExclusionGroup = 1;  
  
}  
```  
  
```vb  
Public  Overrides Sub ProvideComponentProperties()   
  
 ' Specify that the component has an error output.  
 ComponentMetaData.UsesDispositions = True   
  
 Dim input As IDTSInput100 = ComponentMetaData.InputCollection.New   
  
 ' Create the input.  
 input.Name = "Input"   
 input.ErrorRowDisposition = DTSRowDisposition.RD_NotUsed   
 input.ErrorOrTruncationOperation = "A string describing the possible error or truncation that may occur during execution."   
  
 ' Create the default output.  
 Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection.New   
 output.Name = "Output"   
 output.SynchronousInputID = input.ID   
 output.ExclusionGroup = 1   
  
 ' Create the error output.  
 Dim errorOutput As IDTSOutput100 = ComponentMetaData.OutputCollection.New   
 errorOutput.IsErrorOut = True   
 errorOutput.Name = "ErrorOutput"   
 errorOutput.SynchronousInputID = input.ID   
 errorOutput.ExclusionGroup = 1   
  
End Sub  
```  
  
 次のコード例では、非同期型のエラー出力を作成します。  
  
```csharp  
public override void ProvideComponentProperties()  
{  
    // Specify that the component has an error output.  
    ComponentMetaData.UsesDispositions = true;  
  
    // Create the input.  
    IDTSInput100 input = ComponentMetaData.InputCollection.New();  
    input.Name = "Input";  
    input.ErrorRowDisposition = DTSRowDisposition.RD_NotUsed;  
    input.ErrorOrTruncationOperation = "A string describing the possible error or truncation that may occur during execution.";  
  
    // Create the default output.  
    IDTSOutput100 output = ComponentMetaData.OutputCollection.New();  
    output.Name = "Output";  
  
    // Create the error output.  
    IDTSOutput100 errorOutput = ComponentMetaData.OutputCollection.New();  
    errorOutput.Name = "ErrorOutput";  
    errorOutput.IsErrorOut = true;  
}  
```  
  
```vb  
Public  Overrides Sub ProvideComponentProperties()   
  
 ' Specify that the component has an error output.  
 ComponentMetaData.UsesDispositions = True   
  
 ' Create the input.  
 Dim input As IDTSInput100 = ComponentMetaData.InputCollection.New   
  
 ' Create the default output.  
 input.Name = "Input"   
 input.ErrorRowDisposition = DTSRowDisposition.RD_NotUsed   
 input.ErrorOrTruncationOperation = "A string describing the possible error or truncation that may occur during execution."   
  
 ' Create the error output.  
 Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection.New   
 output.Name = "Output"   
 Dim errorOutput As IDTSOutput100 = ComponentMetaData.OutputCollection.New   
 errorOutput.Name = "ErrorOutput"   
 errorOutput.IsErrorOut = True   
  
End Sub  
```  
  
## <a name="redirecting-a-row-to-an-error-output"></a>エラー出力への行のリダイレクト  
 エラー出力をコンポーネントに追加したら、コンポーネントに固有のエラーまたは切り捨て条件を処理し、エラー行または切り捨て行をエラー出力にリダイレクトするコードを設定する必要があります。 この方法は、エラー出力が同期型か非同期型かに応じて 2 種類あります。  
  
### <a name="redirecting-a-row-with-synchronous-outputs"></a>同期出力での行のリダイレクト  
 同期出力に行を送信するには、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.DirectErrorRow%2A> クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> メソッドを呼び出します。 メソッドを呼び出すと、エラー出力の ID、コンポーネント定義のエラー コード、およびコンポーネントが処理できなかった列のインデックスがパラメーターとして渡されます。  
  
 次のコード例では、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.DirectErrorRow%2A> メソッドを使用して、バッファー内の行を同期エラー出力に送信する方法を示します。  
  
```csharp  
public override void ProcessInput(int inputID, PipelineBuffer buffer)  
{  
        IDTSInput100 input = ComponentMetaData.InputCollection.GetObjectByID(inputID);  
  
        // This code sample assumes the component has two outputs, one the default,  
        // the other the error output. If the errorOutputIndex returned from GetErrorOutputInfo  
        // is 0, then the default output is the second output in the collection.  
        int defaultOutputID = -1;  
        int errorOutputID = -1;  
        int errorOutputIndex = -1;  
  
        GetErrorOutputInfo(ref errorOutputID,ref errorOutputIndex);  
  
        if (errorOutputIndex == 0)  
            defaultOutputID = ComponentMetaData.OutputCollection[1].ID;  
        else  
            defaultOutputID = ComponentMetaData.OutputCollection[0].ID;  
  
        while (buffer.NextRow())  
        {  
            try  
            {  
                // TODO: Implement code to process the columns in the buffer row.  
  
                // Ideally, your code should detect potential exceptions before they occur, rather  
                // than having a generic try/catch block such as this.   
                // However, because the error or truncation implementation is specific to each component,  
                // this sample focuses on actually directing the row, and not a single error or truncation.  
  
                // Unless an exception occurs, direct the row to the default   
                buffer.DirectRow(defaultOutputID);  
            }  
            catch  
            {  
                // Yes, has the user specified to redirect the row?  
                if (input.ErrorRowDisposition == DTSRowDisposition.RD_RedirectRow)  
                {  
                    // Yes, direct the row to the error output.  
                    // TODO: Add code to include the errorColumnIndex.  
                    buffer.DirectErrorRow(errorOutputID, 0, errorColumnIndex);  
                }  
                else if (input.ErrorRowDisposition == DTSRowDisposition.RD_FailComponent || input.ErrorRowDisposition == DTSRowDisposition.RD_NotUsed)  
                {  
                    // No, the user specified to fail the component, or the error row disposition was not set.  
                    throw new Exception("An error occurred, and the DTSRowDisposition is either not set, or is set to fail component.");  
                }  
                else  
                {  
                    // No, the user specified to ignore the failure so   
                    // direct the row to the default output.  
                    buffer.DirectRow(defaultOutputID);  
                }  
  
            }  
        }  
}  
```  
  
```vb  
Public  Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)   
   Dim input As IDTSInput100 = ComponentMetaData.InputCollection.GetObjectByID(inputID)   
  
   ' This code sample assumes the component has two outputs, one the default,  
   ' the other the error output. If the errorOutputIndex returned from GetErrorOutputInfo  
   ' is 0, then the default output is the second output in the collection.  
   Dim defaultOutputID As Integer = -1   
   Dim errorOutputID As Integer = -1   
   Dim errorOutputIndex As Integer = -1   
  
   GetErrorOutputInfo(errorOutputID, errorOutputIndex)   
  
   If errorOutputIndex = 0 Then   
     defaultOutputID = ComponentMetaData.OutputCollection(1).ID   
   Else   
     defaultOutputID = ComponentMetaData.OutputCollection(0).ID   
   End If   
  
   While buffer.NextRow   
     Try   
       ' TODO: Implement code to process the columns in the buffer row.  
  
       ' Ideally, your code should detect potential exceptions before they occur, rather  
       ' than having a generic try/catch block such as this.   
       ' However, because the error or truncation implementation is specific to each component,  
       ' this sample focuses on actually directing the row, and not a single error or truncation.  
  
       ' Unless an exception occurs, direct the row to the default   
       buffer.DirectRow(defaultOutputID)   
     Catch   
       ' Yes, has the user specified to redirect the row?  
       If input.ErrorRowDisposition = DTSRowDisposition.RD_RedirectRow Then   
         ' Yes, direct the row to the error output.  
         ' TODO: Add code to include the errorColumnIndex.  
         buffer.DirectErrorRow(errorOutputID, 0, errorColumnIndex)   
       Else   
         If input.ErrorRowDisposition = DTSRowDisposition.RD_FailComponent OrElse input.ErrorRowDisposition = DTSRowDisposition.RD_NotUsed Then   
           ' No, the user specified to fail the component, or the error row disposition was not set.  
           Throw New Exception("An error occurred, and the DTSRowDisposition is either not set, or is set to fail component.")   
         Else   
           ' No, the user specified to ignore the failure so   
           ' direct the row to the default output.  
           buffer.DirectRow(defaultOutputID)   
         End If   
       End If   
     End Try   
   End While   
End Sub  
```  
  
### <a name="redirecting-a-row-with-asynchronous-outputs"></a>非同期出力での行のリダイレクト  
 非同期出力型のコンポーネントでは、同期エラー出力で行うように行を出力に送信するのではなく、出力 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> に行を明示的に追加することによって、行をエラー出力に送信します。 非同期エラー出力を使用するコンポーネントを実装するには、下流コンポーネントに提供されるエラー出力に列を追加し、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> メソッドの実行中にコンポーネントに提供される出力バッファーをキャッシュして、エラー出力に送信する必要があります。 非同期出力型のコンポーネントの実装の詳細については、「[非同期出力型のカスタム変換コンポーネントの開発](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)」のトピックで詳しく説明します。 列がエラー出力に明示的に追加されない場合、出力バッファーに追加されるバッファー行には、2 つのエラー列のみが格納されます。  
  
 非同期エラー出力に行を送信するには、エラー出力バッファーに行を追加する必要があります。 場合によっては、既にエラー出力以外の出力バッファーに行が追加されていることがあります。その場合は、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.RemoveRow%2A> メソッドを使用してこの行を削除する必要があります。 次に出力バッファー列の値を設定し、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetErrorInfo%2A> メソッドを呼び出して、コンポーネント固有のエラー コードとエラー列の値を指定します。  
  
 次の例では、非同期出力型のコンポーネントでのエラー出力の使用方法を示します。 シミュレートされたエラーが発生すると、コンポーネントはエラー出力バッファーに行を追加し、エラー出力以外の出力バッファーに既に追加されていた値をエラー出力バッファーへコピーし、エラー出力以外の出力バッファーに追加されていた行を削除します。そして最後に、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetErrorInfo%2A> メソッドを呼び出して、エラー コードおよびエラー列の値を設定します。  
  
```csharp  
int []columnIndex;  
int errorOutputID = -1;  
int errorOutputIndex = -1;  
  
public override void PreExecute()  
{  
    IDTSOutput100 defaultOutput = null;  
  
    this.GetErrorOutputInfo(ref errorOutputID, ref errorOutputIndex);  
    foreach (IDTSOutput100 output in ComponentMetaData.OutputCollection)  
    {  
        if (output.ID != errorOutputID)  
            defaultOutput = output;  
    }  
  
    columnIndex = new int[defaultOutput.OutputColumnCollection.Count];  
  
    for(int col =0 ; col < defaultOutput.OutputColumnCollection.Count; col++)  
    {  
        IDTSOutputColumn100 column = defaultOutput.OutputColumnCollection[col];  
        columnIndex[col] = BufferManager.FindColumnByLineageID(defaultOutput.Buffer, column.LineageID);  
    }  
}  
  
public override void PrimeOutput(int outputs, int[] outputIDs, PipelineBuffer[] buffers)  
{  
    for( int x=0; x < outputs; x++ )  
    {  
        if (outputIDs[x] == errorOutputID)  
            this.errorBuffer = buffers[x];  
        else  
            this.defaultBuffer = buffers[x];  
    }  
  
    int rows = 100;  
  
    Random random = new Random(System.DateTime.Now.Millisecond);  
  
    for (int row = 0; row < rows; row++)  
    {  
        try  
        {  
            defaultBuffer.AddRow();  
  
            for (int x = 0; x < columnIndex.Length; x++)  
                defaultBuffer[columnIndex[x]] = random.Next();  
  
            // Simulate an error.  
            if ((row % 2) == 0)  
                throw new Exception("A simulated error.");  
        }  
        catch  
        {  
            // Add a row to the error buffer.  
            errorBuffer.AddRow();  
  
            // Get the values from the default buffer  
            // and copy them to the error buffer.  
            for (int x = 0; x < columnIndex.Length; x++)  
                errorBuffer[columnIndex[x]] = defaultBuffer[columnIndex[x]];  
  
            // Set the error information.  
            errorBuffer.SetErrorInfo(errorOutputID, 1, 0);  
  
            // Remove the row that was added to the default buffer.  
            defaultBuffer.RemoveRow();  
        }  
    }  
  
    if (defaultBuffer != null)  
        defaultBuffer.SetEndOfRowset();  
  
    if (errorBuffer != null)  
        errorBuffer.SetEndOfRowset();  
}  
```  
  
```vb  
Private columnIndex As Integer()   
Private errorOutputID As Integer = -1   
Private errorOutputIndex As Integer = -1   
  
Public  Overrides Sub PreExecute()   
 Dim defaultOutput As IDTSOutput100 = Nothing   
 Me.GetErrorOutputInfo(errorOutputID, errorOutputIndex)   
 For Each output As IDTSOutput100 In ComponentMetaData.OutputCollection   
   If Not (output.ID = errorOutputID) Then   
     defaultOutput = output   
   End If   
 Next   
 columnIndex = New Integer(defaultOutput.OutputColumnCollection.Count) {}   
 Dim col As Integer = 0   
 While col < defaultOutput.OutputColumnCollection.Count   
   Dim column As IDTSOutputColumn100 = defaultOutput.OutputColumnCollection(col)   
   columnIndex(col) = BufferManager.FindColumnByLineageID(defaultOutput.Buffer, column.LineageID)   
   System.Math.Min(System.Threading.Interlocked.Increment(col),col-1)   
 End While   
End Sub   
  
Public  Overrides Sub PrimeOutput(ByVal outputs As Integer, ByVal outputIDs As Integer(), ByVal buffers As PipelineBuffer())   
 Dim x As Integer = 0   
 While x < outputs   
   If outputIDs(x) = errorOutputID Then   
     Me.errorBuffer = buffers(x)   
   Else   
     Me.defaultBuffer = buffers(x)   
   End If   
   System.Math.Min(System.Threading.Interlocked.Increment(x),x-1)   
 End While   
 Dim rows As Integer = 100   
 Dim random As Random = New Random(System.DateTime.Now.Millisecond)   
 Dim row As Integer = 0   
 While row < rows   
   Try   
     defaultBuffer.AddRow   
     Dim x As Integer = 0   
     While x < columnIndex.Length   
       defaultBuffer(columnIndex(x)) = random.Next   
       System.Math.Min(System.Threading.Interlocked.Increment(x),x-1)   
     End While   
     ' Simulate an error.  
     If (row Mod 2) = 0 Then   
       Throw New Exception("A simulated error.")   
     End If   
   Catch   
     ' Add a row to the error buffer.  
     errorBuffer.AddRow   
     ' Get the values from the default buffer  
     ' and copy them to the error buffer.  
     Dim x As Integer = 0   
     While x < columnIndex.Length   
       errorBuffer(columnIndex(x)) = defaultBuffer(columnIndex(x))   
       System.Math.Min(System.Threading.Interlocked.Increment(x),x-1)   
     End While   
     ' Set the error information.  
     errorBuffer.SetErrorInfo(errorOutputID, 1, 0)   
     ' Remove the row that was added to the default buffer.  
     defaultBuffer.RemoveRow   
   End Try   
   System.Math.Min(System.Threading.Interlocked.Increment(row),row-1)   
 End While   
 If Not (defaultBuffer Is Nothing) Then   
   defaultBuffer.SetEndOfRowset   
 End If   
 If Not (errorBuffer Is Nothing) Then   
   errorBuffer.SetEndOfRowset   
 End If   
End Sub  
```  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [データのエラー処理](../../data-flow/error-handling-in-data.md)   
 [データ フロー コンポーネントでのエラー出力の使用](using-error-outputs-in-a-data-flow-component.md)  
  
  
