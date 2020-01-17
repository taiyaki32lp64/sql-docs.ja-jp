---
title: 非同期出力型のカスタム変換コンポーネントの開発 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom data flow components [Integration Services], transformation components
- asynchronous outputs [Integration Services]
- ProcessInput method
- cache [Integration Services]
- buffer allocations [Integration Services]
- transformation components [Integration Services]
- output columns [Integration Services]
- PrimeOutput method
- data flow components [Integration Services], transformation components
ms.assetid: 1c3e92c7-a4fa-4fdd-b9ca-ac3069536274
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5bb52fc5c8a3789cc945a2ea850d0849335917e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62896633"
---
# <a name="developing-a-custom-transformation-component-with-asynchronous-outputs"></a>非同期出力型のカスタム変換コンポーネントの開発
  非同期出力型変換コンポーネントは、変換が入力行をすべて受け取るまで行を出力できないようにする場合や、変換が入力として受信した各行に対して必ずしも 1 つずつ出力行を生成しない場合に使用します。 たとえば、集計変換では、行をすべて読み込むまではすべての行の合計を計算できません。 これに対し、同期出力型コンポーネントは、データが渡されるたびに各データ行を変更する場合に使用します。 各行のデータを順に変更したり、1 つまたは複数の列を新規作成して、各列にすべての入力行ごとの値を設定したりできます。 同期コンポーネントと非同期コンポーネントの相違点の詳細については、「[同期変換と非同期変換について](../understanding-synchronous-and-asynchronous-transformations.md)」を参照してください。  
  
 非同期出力型変換コンポーネントは、変換先コンポーネントと変換元コンポーネントの、両方の機能を果たすという特徴があります。 この種のコンポーネントは、上流コンポーネントから行を受け取り、下流コンポーネントで使用される行を追加します。 これらの操作を両方とも行うデータ フロー コンポーネントは、他にはありません。  
  
 上流コンポーネントの列が同期出力型コンポーネントで使用可能な場合、自動的に、その下流にあるコンポーネントでも使用可能となります。 したがって、同期出力型コンポーネントでは、出力列を定義しなくても次のコンポーネントに行や列を渡すことができます。 これに対し、非同期出力型コンポーネントでは、下流コンポーネントに行を渡すために出力列を定義する必要があります。 したがって、非同期出力型コンポーネントの方が、デザイン時や実行時に必要な処理が多いため、開発者はより多くのコードを実装する必要があります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には非同期出力型の変換がいくつか組み込まれています。 たとえば並べ替え変換では、並べ替えを行う前に行がすべて必要であるため、非同期出力を使用して変換を実行しています。 行をすべて受け取ったら並べ替えを実行し、出力に行を追加します。  
  
 ここでは、非同期出力型の変換を開発する方法の詳細について説明します。 変換元コンポーネントの開発の詳細については、「[カスタム変換元コンポーネントの開発](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)」を参照してください。  
  
## <a name="design-time"></a>デザイン時  
  
### <a name="creating-the-component"></a>コンポーネントの作成  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A> オブジェクトの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> プロパティは、同期出力か非同期出力かの区別を示します。 非同期出力を作成するには、コンポーネントに出力を追加し、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A> プロパティを 0 に設定します。 また、このプロパティを設定することにより、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> オブジェクトをコンポーネントの入出力の両方に割り当てるか、単一のバッファーを割り当てて 2 つのオブジェクトで共有するかをデータ フロー タスクが判断します。  
  
 次のサンプル コードは、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> を実装し、非同期出力を作成するコンポーネントを示します。  
  
```csharp  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsPipelineComponent(DisplayName = "AsyncComponent",ComponentType = ComponentType.Transform)]  
    public class AsyncComponent : PipelineComponent  
    {  
        public override void ProvideComponentProperties()  
        {  
            // Call the base class, which adds a synchronous input  
            // and output.  
            base.ProvideComponentProperties();  
  
            // Make the output asynchronous.  
            IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
            output.SynchronousInputID = 0;  
        }  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime  
  
<DtsPipelineComponent(DisplayName:="AsyncComponent", ComponentType:=ComponentType.Transform)> _  
Public Class AsyncComponent  
    Inherits PipelineComponent  
  
    Public Overrides Sub ProvideComponentProperties()  
  
        ' Call the base class, which adds a synchronous input  
        ' and output.  
        Me.ProvideComponentProperties()  
  
        ' Make the output asynchronous.  
        Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
        output.SynchronousInputID = 0  
  
    End Sub  
  
End Class  
```  
  
### <a name="creating-and-configuring-output-columns"></a>出力列の作成と設定  
 前述したように、非同期型コンポーネントは出力列コレクションに列を追加し、下流コンポーネントに列を渡します。 コンポーネントの要件に応じて、デザイン時に選択できる方法はいくつかあります。 たとえば、上流コンポーネントからすべての列をそのまま下流コンポーネントに渡す場合は、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.OnInputPathAttached%2A> メソッドをオーバーライドして列を追加します。これが、コンポーネントで入力列が使用可能となる最初のメソッドだからです。  
  
 入力列として選択した列に基づいてコンポーネントが出力列を作成する場合は、出力列を選択してそれらの使い方を示すように、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.SetUsageType%2A> メソッドをオーバーライドします。  
  
 非同期型出力型コンポーネントで、上流コンポーネントの列に基づいて出力列を作成する場合、使用できる上流の列が変更されると、コンポーネントは出力列のコレクションを更新する必要があります。 変更は <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> メソッド内で検出され、更新は <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> メソッド内で行われます。  
  
> [!NOTE]  
>  出力列コレクションからある出力列を削除すると、データ フローの下流に位置し、この列を参照しているコンポーネントに悪影響を及ぼします。 下流コンポーネントが悪影響を受けないようにするには、列を削除して再作成する方法を取らずに、出力列を修復する必要があります。 たとえば、ある列のデータ型を変更した場合、データ型を更新する必要があります。  
  
 次のコード例では、上流コンポーネントから渡される各列に対して出力列を作成し、出力列コレクションに追加する方法を示しています。  
  
```csharp  
public override void OnInputPathAttached(int inputID)  
{  
   IDTSInput100 input = ComponentMetaData.InputCollection.GetObjectByID(inputID);  
   IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
   IDTSVirtualInput100 vInput = input.GetVirtualInput();  
  
   foreach (IDTSVirtualInputColumn100 vCol in vInput.VirtualInputColumnCollection)  
   {  
      IDTSOutputColumn100 outCol = output.OutputColumnCollection.New();  
      outCol.Name = vCol.Name;  
      outCol.SetDataTypeProperties(vCol.DataType, vCol.Length, vCol.Precision, vCol.Scale, vCol.CodePage);  
   }  
}  
```  
  
```vb  
Public Overrides Sub OnInputPathAttached(ByVal inputID As Integer)  
  
    Dim input As IDTSInput100 = ComponentMetaData.InputCollection.GetObjectByID(inputID)  
    Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
    Dim vInput As IDTSVirtualInput100 = input.GetVirtualInput()  
  
    For Each vCol As IDTSVirtualInputColumn100 In vInput.VirtualInputColumnCollection  
  
        Dim outCol As IDTSOutputColumn100 = output.OutputColumnCollection.New()  
        outCol.Name = vCol.Name  
        outCol.SetDataTypeProperties(vCol.DataType, vCol.Length, vCol.Precision, vCol.Scale, vCol.CodePage)  
  
    Next  
End Sub  
```  
  
## <a name="run-time"></a>実行時間  
 非同期出力型コンポーネントは、他の種類のコンポーネントとは実行時における処理手順も異なります。 まず、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> と <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> の両方のメソッドに対する呼び出しを受信するのは、この型のコンポーネントのみです。 また、非同期出力型コンポーネントは、処理を開始する前に入力行すべてにアクセスできるようになっている必要があります。そのため、すべての行が読み取られるまで、入力行を内部キャッシュに保存する必要があります。 最後に、他のコンポーネントとは異なり、非同期出力型コンポーネントは入力用と出力用の両方のバッファーを受け取ります。  
  
### <a name="understanding-the-buffers"></a>バッファーについて  
 コンポーネントが入力バッファーを受け取るのは、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> メソッドの実行中です。 このバッファーには、上流コンポーネントによってバッファーに追加された行が格納されます。 また、このバッファーには、上流コンポーネントの出力に存在しながら、非同期型コンポーネントの入力コレクションに含まれていない列を含め、コンポーネントの入力の列が格納されます。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> メソッドからコンポーネントに提供される出力バッファーには、最初は行が格納されていません。 コンポーネントは行をこのバッファーに追加し、バッファーがいっぱいになった時点で下流コンポーネントに渡します。 出力バッファーには、他の下流コンポーネントが出力に追加したすべての列を含め、出力列コレクションで定義されている列が格納されます。  
  
 この動作は、単一のバッファーを共有する同期出力型コンポーネントの動作とは異なります。 同期出力型コンポーネントの共有バッファーには、上流コンポーネントと下流コンポーネントの出力に追加された列を含め、コンポーネントの入力列および出力列の両方が格納されます。  
  
### <a name="processing-rows"></a>行の処理  
  
#### <a name="caching-input-rows"></a>入力行のキャッシュ  
 非同期出力型コンポーネントを記述する場合、出力バッファーに行を追加するには 3 つの方法があります。 それは、入力行を受け取るたびに追加する方法、上流コンポーネントから行をすべて受け取るまでキャッシュする方法、またはコンポーネントを処理するうえで適切な時点で追加する方法です。 方法は、コンポーネントの要求に応じて選択します。 たとえば並べ替えコンポーネントの場合、上流から行をすべて受け取ってからでないと並べ替え処理はできません。 したがって、すべての行が読み取られるまで待機してから、出力バッファーに行を追加します。  
  
 入力バッファーで受け取った行は、処理の準備ができるまで、コンポーネントの内部にキャッシュする必要があります。 入力バッファー内の行は、データ テーブルや多次元配列のほか、コンポーネントの内部構造の任意の場所にキャッシュできます。  
  
#### <a name="adding-output-rows"></a>出力行の追加  
 出力バッファーへの行の追加は、出力バッファーで <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.AddRow%2A> メソッドを呼び出すことによって行います。これは、行を受け取るたびに出力バッファーに追加する場合でも、すべての行を受け取ってから追加する場合でも同じです。 行を追加したら、新しい行の各列に値を設定します。  
  
 出力バッファーには、コンポーネントの出力列コレクションにはない列が含まれる場合があるため、値を設定するには、バッファーの該当する列のインデックスを探す必要があります。 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> プロパティの <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> メソッドは、バッファー行のうち、指定された系列 ID を持つ列のインデックスを返します。これを使用して、バッファー列に値を割り当てます。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> メソッドは、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> メソッドまたは <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> メソッドの前に呼び出されますが、ここで初めて <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> プロパティが使用可能になり、初めて入力バッファーおよび出力バッファーの各列のインデックスを探すことができるようになります。  
  
## <a name="sample"></a>サンプル  
 次の例は、行を受け取るたびに出力バッファーに行を追加する、非同期出力型の簡単な変換コンポーネントを示しています。 ただし、この例ではここで説明したメソッドや機能のすべてが使われているわけではありません。 カスタムの非同期出力型変換コンポーネントでオーバーライドしなければならない重要なメソッドは示していますが、デザイン時の検証のためのコードは含まれていません。 また、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> メソッド内のコードは、入力列コレクションの各列に対応して、出力列コレクションに 1 つずつ出力列があるものと想定しています。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
   [DtsPipelineComponent(DisplayName = "AsynchronousOutput")]  
   public class AsynchronousOutput : PipelineComponent  
   {  
      PipelineBuffer outputBuffer;  
      int[] inputColumnBufferIndexes;  
      int[] outputColumnBufferIndexes;  
  
      public override void ProvideComponentProperties()  
      {  
         // Let the base class add the input and output objects.  
         base.ProvideComponentProperties();  
  
         // Name the input and output, and make the  
         // output asynchronous.  
         ComponentMetaData.InputCollection[0].Name = "Input";  
         ComponentMetaData.OutputCollection[0].Name = "AsyncOutput";  
         ComponentMetaData.OutputCollection[0].SynchronousInputID = 0;  
      }  
      public override void PreExecute()  
      {  
         IDTSInput100 input = ComponentMetaData.InputCollection[0];  
         IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
  
         inputColumnBufferIndexes = new int[input.InputColumnCollection.Count];  
         outputColumnBufferIndexes = new int[output.OutputColumnCollection.Count];  
  
         for (int col = 0; col < input.InputColumnCollection.Count; col++)  
            inputColumnBufferIndexes[col] = BufferManager.FindColumnByLineageID(input.Buffer, input.InputColumnCollection[col].LineageID);  
  
         for (int col = 0; col < output.OutputColumnCollection.Count; col++)  
            outputColumnBufferIndexes[col] = BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection[col].LineageID);  
  
      }  
  
      public override void PrimeOutput(int outputs, int[] outputIDs, PipelineBuffer[] buffers)  
      {  
         if (buffers.Length != 0)  
            outputBuffer = buffers[0];  
      }  
      public override void ProcessInput(int inputID, PipelineBuffer buffer)  
      {  
            // Advance the buffer to the next row.  
            while (buffer.NextRow())  
            {  
               // Add a row to the output buffer.  
               outputBuffer.AddRow();  
               for (int x = 0; x < inputColumnBufferIndexes.Length; x++)  
               {  
                  // Copy the data from the input buffer column to the output buffer column.  
                  outputBuffer[outputColumnBufferIndexes[x]] = buffer[inputColumnBufferIndexes[x]];  
               }  
            }  
         if (buffer.EndOfRowset)  
         {  
            // EndOfRowset on the input buffer is true.  
            // Set EndOfRowset on the output buffer.  
            outputBuffer.SetEndOfRowset();  
         }  
      }  
   }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
  
Namespace Microsoft.Samples.SqlServer.Dts  
  
    <DtsPipelineComponent(DisplayName:="AsynchronousOutput")> _  
    Public Class AsynchronousOutput  
  
        Inherits PipelineComponent  
  
        Private outputBuffer As PipelineBuffer  
        Private inputColumnBufferIndexes As Integer()  
        Private outputColumnBufferIndexes As Integer()  
  
        Public Overrides Sub ProvideComponentProperties()  
  
            ' Let the base class add the input and output objects.  
            Me.ProvideComponentProperties()  
  
            ' Name the input and output, and make the  
            ' output asynchronous.  
            ComponentMetaData.InputCollection(0).Name = "Input"  
            ComponentMetaData.OutputCollection(0).Name = "AsyncOutput"  
            ComponentMetaData.OutputCollection(0).SynchronousInputID = 0  
        End Sub  
  
        Public Overrides Sub PreExecute()  
  
            Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)  
            Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
  
            ReDim inputColumnBufferIndexes(input.InputColumnCollection.Count)  
            ReDim outputColumnBufferIndexes(output.OutputColumnCollection.Count)  
  
            For col As Integer = 0 To input.InputColumnCollection.Count  
                inputColumnBufferIndexes(col) = BufferManager.FindColumnByLineageID(input.Buffer, input.InputColumnCollection(col).LineageID)  
            Next  
  
            For col As Integer = 0 To output.OutputColumnCollection.Count  
                outputColumnBufferIndexes(col) = BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection(col).LineageID)  
            Next  
  
        End Sub  
        Public Overrides Sub PrimeOutput(ByVal outputs As Integer, ByVal outputIDs As Integer(), ByVal buffers As PipelineBuffer())  
  
            If buffers.Length <> 0 Then  
                outputBuffer = buffers(0)  
            End If  
  
        End Sub  
  
        Public Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)  
  
                ' Advance the buffer to the next row.  
                While (buffer.NextRow())  
  
                    ' Add a row to the output buffer.  
                    outputBuffer.AddRow()  
                    For x As Integer = 0 To inputColumnBufferIndexes.Length  
  
                        ' Copy the data from the input buffer column to the output buffer column.  
                        outputBuffer(outputColumnBufferIndexes(x)) = buffer(inputColumnBufferIndexes(x))  
  
                    Next  
                End While  
  
            If buffer.EndOfRowset = True Then  
                ' EndOfRowset on the input buffer is true.  
                ' Set the end of row set on the output buffer.  
                outputBuffer.SetEndOfRowset()  
            End If  
        End Sub  
    End Class  
End Namespace  
```  
  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [同期出力型のカスタム変換コンポーネントの開発](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)   
 [同期変換と非同期変換について](../understanding-synchronous-and-asynchronous-transformations.md)   
 [スクリプト コンポーネントによる非同期変換の作成](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
  
  
