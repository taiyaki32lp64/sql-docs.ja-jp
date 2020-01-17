---
title: 同期出力型のカスタム変換コンポーネントの開発 | Microsoft Docs
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
- ProcessInput method
- buffer allocations [Integration Services]
- synchronous outputs [Integration Services]
- transformation components [Integration Services]
- output columns [Integration Services]
- data flow components [Integration Services], transformation components
ms.assetid: b694d21f-9919-402d-9192-666c6449b0b7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 785ca6c05bc221e1449607b9dc3deaa93aa667bf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62896584"
---
# <a name="developing-a-custom-transformation-component-with-synchronous-outputs"></a>同期出力型のカスタム変換コンポーネントの開発
  同期出力型の変換コンポーネントは、上流コンポーネントから行を受け取り、これらの行の列の値を読み取ったり変更したりして、下流コンポーネントに渡します。 このコンポーネントは、上流コンポーネントから提供される列から派生する、別の出力列も定義しますが、データ フローに行を追加することはありません。 同期コンポーネントと非同期コンポーネントの相違点の詳細については、「[同期変換と非同期変換について](../understanding-synchronous-and-asynchronous-transformations.md)」を参照してください。  
  
 この種類のコンポーネントは、データがコンポーネントに提供されたときにインラインで変更され、処理する前にコンポーネントがすべての行を確認する必要がないタスクに適しています。 通常、同期出力型の変換では、外部データ ソースへの接続、外部メタデータ列の管理、および出力バッファーへの行の追加は行われないため、このコンポーネントを開発するのは最も簡単です。  
  
 同期出力型の変換コンポーネントを作成するには、コンポーネント用に選択された上流列を格納する <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100> オブジェクトと、コンポーネントによって作成された派生列を格納する <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> オブジェクトを追加します。 さらに、デザイン時のメソッドを実装し、実行中に受信バッファー行内の列を読み取ったり変更するコードを設定します。  
  
 このセクションでは、カスタム変換コンポーネントの実装に必要な情報、および概念の理解に役立つコード例を提供します。  
  
## <a name="design-time"></a>デザイン時  
 このコンポーネントのデザイン時のコードでは、入力と出力の作成、コンポーネントが生成するすべての出力の追加、および、コンポーネントの構成の検証を行います。  
  
### <a name="creating-the-component"></a>コンポーネントの作成  
 コンポーネントの入力、出力、およびカスタム プロパティは、通常、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> メソッドの実行中に作成します。 同期出力型の変換コンポーネントの入力および出力を追加するには、2 つの方法があります。 メソッドの基本クラスの実装を使用して、作成された既定の入力および出力を変更する方法と、入力と出力を手動で明示的に追加する方法です。  
  
 次のコード例は、入力および出力オブジェクトを明示的に追加する <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> を実装します。 同様の処理を行うために呼び出す基本クラスについては、コメントに記載されています。  
  
```csharp  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsPipelineComponent(DisplayName = "SynchronousComponent", ComponentType = ComponentType.Transform)]  
    public class SyncComponent : PipelineComponent  
    {  
  
        public override void ProvideComponentProperties()  
        {  
            // Add the input.  
            IDTSInput100 input = ComponentMetaData.InputCollection.New();  
            input.Name = "Input";  
  
            // Add the output.  
            IDTSOutput100 output = ComponentMetaData.OutputCollection.New();  
            output.Name = "Output";  
            output.SynchronousInputID = input.ID;  
  
            // Alternatively, you can let the base class add the input and output  
            // and set the SynchronousInputID of the output to the ID of the input.  
            // base.ProvideComponentProperties();  
        }  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime  
  
<DtsPipelineComponent(DisplayName:="SynchronousComponent", ComponentType:=ComponentType.Transform)> _  
Public Class SyncComponent  
    Inherits PipelineComponent  
  
    Public Overrides Sub ProvideComponentProperties()  
  
        ' Add the input.  
        Dim input As IDTSInput100 = ComponentMetaData.InputCollection.New()  
        input.Name = "Input"  
  
        ' Add the output.  
        Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection.New()  
        output.Name = "Output"  
        output.SynchronousInputID = Input.ID  
  
        ' Alternatively, you can let the base class add the input and output  
        ' and set the SynchronousInputID of the output to the ID of the input.  
        ' base.ProvideComponentProperties();  
  
    End Sub  
  
End Class  
```  
  
### <a name="creating-and-configuring-output-columns"></a>出力列の作成と設定  
 同期出力型の変換コンポーネントでは、バッファーに行は追加されません。ただし、コンポーネントの出力に出力列を追加することはできます。 通常、コンポーネントが出力列を追加すると、新しい出力列の値は、実行時に上流コンポーネントから渡される 1 つ以上の列に含まれるデータから取得されます。  
  
 出力列が作成されたら、データ型のプロパティを設定する必要があります。 出力列のデータ型のプロパティを設定するには特別な処理が必要で、その処理は、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.SetDataTypeProperties%2A> メソッドを呼び出して実行します。 このメソッドが必要になるのは、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.Length%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.Precision%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.CodePage%2A> のプロパティがそれぞれ互いの設定に依存しているため、個別に読み取り専用であるからです。 このメソッドを使用すると、プロパティの値を確実に矛盾なく設定でき、データ フロー タスクにより、正しく設定されていることが検証されます。  
  
 列の <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A> により、他のプロパティに設定される値が決定されます。 次の表は、各 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A> の依存するプロパティの要件を示しています。 ここに示されていないデータ型の場合、依存するプロパティは 0 に設定されます。  
  
|DataType|長さ|Scale|有効桁数|CodePage|  
|--------------|------------|-----------|---------------|--------------|  
|DT_DECIMAL|0|0 より大きく 28 以下。|0|0|  
|DT_CY|0|0|0|0|  
|DT_NUMERIC|0|0 より大きく 28 以下で、有効桁数の値未満|1 以上 38 以下|0|  
|DT_BYTES|0 より大きい|0|0|0|  
|DT_STR|0 より大きく 8000 未満|0|0|0 以外の有効なコード ページ|  
|DT_WSTR|0 より大きく 4000 未満|0|0|0|  
  
 データ型プロパティの制約は出力列のデータ型に基づくため、マネージド型を処理する場合、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の正しいデータ型を選択する必要があります。 基本クラスには、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ConvertBufferDataTypeToFitManaged%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferTypeToDataRecordType%2A>、および <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.DataRecordTypeToBufferType%2A> の 3 つのヘルパー メソッドがあり、これを使用すると、マネージド コンポーネントの開発者は、マネージド型に対応する [!INCLUDE[ssIS](../../includes/ssis-md.md)] のデータ型を適切に選択できます。 これらのメソッドは、マネージド データ型と [!INCLUDE[ssIS](../../includes/ssis-md.md)] のデータ型を相互に変換します。  
  
## <a name="run-time"></a>実行時間  
 一般的に、コンポーネントのランタイム部分の実装は、コンポーネントの入力および出力列をバッファー内で検索するタスクと、受信バッファー行内にあるこれらの列の値を読み取りまたは書き込みするタスクの 2 つに分類されます。  
  
### <a name="locating-columns-in-the-buffer"></a>バッファー内の列の検索  
 実行中にコンポーネントに提供されるバッファー内の列数は、コンポーネントの入力または出力コレクション内の列数よりも大きい場合があります。 各バッファーには、データ フローのコンポーネントで定義されているすべての出力列が含まれているためです。 バッファーの列が入力または出力の列と正しく一致していることを確認するには、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> の <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> メソッドを使用する必要があります。 このメソッドは、特定のバッファー内の列を系列 ID によって検索します。 通常、列は <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> の実行中に検索されます。これは、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> プロパティが使用できるようになる最初の実行時メソッドであるためです。  
  
 次のコード例は、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> の実行中に、入力および出力列のコレクションで列のインデックスを検索するコンポーネントを示します。 列インデックスは整数の配列に格納され、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> の実行中にコンポーネントからアクセスできます。  
  
```csharp  
int []inputColumns;  
int []outputColumns;  
  
public override void PreExecute()  
{  
    IDTSInput100 input = ComponentMetaData.InputCollection[0];  
    IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
  
    inputColumns = new int[input.InputColumnCollection.Count];  
    outputColumns = new int[output.OutputColumnCollection.Count];  
  
    for(int col=0; col < input.InputColumnCollection.Count; col++)  
    {  
        IDTSInputColumn100 inputColumn = input.InputColumnCollection[col];  
        inputColumns[col] = BufferManager.FindColumnByLineageID(input.Buffer, inputColumn.LineageID);  
    }  
  
    for(int col=0; col < output.OutputColumnCollection.Count; col++)  
    {  
        IDTSOutputColumn100 outputColumn = output.OutputColumnCollection[col];  
        outputColumns[col] = BufferManager.FindColumnByLineageID(input.Buffer, outputColumn.LineageID);  
    }  
  
}  
```  
  
```vb  
Public Overrides Sub PreExecute()  
  
    Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)  
    Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
  
    ReDim inputColumns(input.InputColumnCollection.Count)  
    ReDim outputColumns(output.OutputColumnCollection.Count)  
  
    For col As Integer = 0 To input.InputColumnCollection.Count  
  
        Dim inputColumn As IDTSInputColumn100 = input.InputColumnCollection(col)  
        inputColumns(col) = BufferManager.FindColumnByLineageID(input.Buffer, inputColumn.LineageID)  
    Next  
  
    For col As Integer = 0 To output.OutputColumnCollection.Count  
  
        Dim outputColumn As IDTSOutputColumn100 = output.OutputColumnCollection(col)  
        outputColumns(col) = BufferManager.FindColumnByLineageID(input.Buffer, outputColumn.LineageID)  
    Next  
  
End Sub  
```  
  
### <a name="processing-rows"></a>行の処理  
 コンポーネントは、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> メソッドで、行および列を含む <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> オブジェクトを受け取ります。 このメソッドではバッファー内の行が繰り返され、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> が読み取られて変更されている間に列が識別されます。 このメソッドは、上流コンポーネントから行が渡されなくなるまで、データ フロー タスクによって繰り返し呼び出されます。  
  
 バッファー内の列は、配列のインデクサーにアクセスする方法を使用するか、`Get` または `Set` メソッドのいずれかを使用することにより、個別に読み取りまたは書き込みが行われます。 バッファー内の列のデータ型がわかっている場合には、`Get` および `Set` メソッドの方が効率的であり、こちらを使用するようお勧めします。  
  
 次のコード例では、受信行を処理する <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> メソッドを実装します。  
  
```csharp  
public override void ProcessInput( int InputID, PipelineBuffer buffer)  
{  
       while( buffer.NextRow())  
       {  
            for(int x=0; x < inputColumns.Length;x++)  
            {  
                if(!buffer.IsNull(inputColumns[x]))  
                {  
                    object columnData = buffer[inputColumns[x]];  
                    // TODO: Modify the column data.  
                    buffer[inputColumns[x]] = columnData;  
                }  
            }  
  
      }  
}  
```  
  
```vb  
Public Overrides Sub ProcessInput(ByVal InputID As Integer, ByVal buffer As PipelineBuffer)  
  
        While (buffer.NextRow())  
  
            For x As Integer = 0 To inputColumns.Length  
  
                if buffer.IsNull(inputColumns(x)) = false then  
  
                    Dim columnData As Object = buffer(inputColumns(x))  
                    ' TODO: Modify the column data.  
                    buffer(inputColumns(x)) = columnData  
  
                End If  
            Next  
  
        End While  
End Sub  
```  
  
## <a name="sample"></a>サンプル  
 次のサンプルは、すべての文字列型の列の値を大文字に変換する、簡単な同期出力型の変換コンポーネントを示しています。 ただし、この例ではここで説明したメソッドや機能のすべてが使われているわけではありません。 同期出力型の変換コンポーネントで必ずオーバーライドしなければならない重要なメソッドは示していますが、デザイン時の検証のためのコードは含まれていません。  
  
```csharp  
using System;  
using System.Collections;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
namespace Uppercase  
{  
  [DtsPipelineComponent(DisplayName = "Uppercase")]  
  public class Uppercase : PipelineComponent  
  {  
    ArrayList m_ColumnIndexList = new ArrayList();  
  
    public override void ProvideComponentProperties()  
    {  
      base.ProvideComponentProperties();  
      ComponentMetaData.InputCollection[0].Name = "Uppercase Input";  
      ComponentMetaData.OutputCollection[0].Name = "Uppercase Output";  
    }  
  
    public override void PreExecute()  
    {  
      IDTSInput100 input = ComponentMetaData.InputCollection[0];  
      IDTSInputColumnCollection100 inputColumns = input.InputColumnCollection;  
  
      foreach (IDTSInputColumn100 column in inputColumns)  
      {  
        if (column.DataType == DataType.DT_STR || column.DataType == DataType.DT_WSTR)  
        {  
          m_ColumnIndexList.Add((int)BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID));  
        }  
      }  
    }  
  
    public override void ProcessInput(int inputID, PipelineBuffer buffer)  
    {  
      while (buffer.NextRow())  
      {  
        foreach (int columnIndex in m_ColumnIndexList)  
        {  
          string str = buffer.GetString(columnIndex);  
          buffer.SetString(columnIndex, str.ToUpper());  
        }  
      }  
    }  
  }  
}  
```  
  
```vb  
Imports System   
Imports System.Collections   
Imports Microsoft.SqlServer.Dts.Pipeline   
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper   
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper   
Namespace Uppercase   
  
 <DtsPipelineComponent(DisplayName="Uppercase")> _   
 Public Class Uppercase   
 Inherits PipelineComponent   
   Private m_ColumnIndexList As ArrayList = New ArrayList   
  
   Public  Overrides Sub ProvideComponentProperties()   
     MyBase.ProvideComponentProperties   
     ComponentMetaData.InputCollection(0).Name = "Uppercase Input"   
     ComponentMetaData.OutputCollection(0).Name = "Uppercase Output"   
   End Sub   
  
   Public  Overrides Sub PreExecute()   
     Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)   
     Dim inputColumns As IDTSInputColumnCollection100 = input.InputColumnCollection   
     For Each column As IDTSInputColumn100 In inputColumns   
       If column.DataType = DataType.DT_STR OrElse column.DataType = DataType.DT_WSTR Then   
         m_ColumnIndexList.Add(CType(BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID), Integer))   
       End If   
     Next   
   End Sub   
  
   Public  Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)   
     While buffer.NextRow   
       For Each columnIndex As Integer In m_ColumnIndexList   
         Dim str As String = buffer.GetString(columnIndex)   
         buffer.SetString(columnIndex, str.ToUpper)   
       Next   
     End While   
   End Sub   
 End Class   
End Namespace  
```  
  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [非同期出力型のカスタム変換コンポーネントの開発](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)   
 [同期変換と非同期変換について](../understanding-synchronous-and-asynchronous-transformations.md)   
 [スクリプト コンポーネントによる同期変換の作成](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md) 
  
  
