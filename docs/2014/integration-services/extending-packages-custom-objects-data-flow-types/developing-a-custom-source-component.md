---
title: カスタム変換元コンポーネントの開発 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- validation [Integration Services], components
- external data sources [Integration Services]
- data flow components [Integration Services], source components
- output columns [Integration Services]
- custom data flow components [Integration Services], source components
- custom sources [Integration Services]
- source components [Integration Services]
ms.assetid: 4dc0f631-8fd6-4007-b573-ca67f58ca068
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3ea069983515564225d0cf6b74e3660f6ef0829e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768946"
---
# <a name="developing-a-custom-source-component"></a>カスタム変換元コンポーネントの開発
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] を使用することで、開発者は、データ フロー タスクでカスタム データ ソースに接続して、変換元のデータを他のコンポーネントに提供する変換元コンポーネントを記述できます。 カスタム変換元を作成できると、既存の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 変換元のいずれかを使用してアクセスできないデータ ソースに接続する必要がある場合に便利です。  
  
 変換元コンポーネントには 1 つ以上の出力がありますが、入力はありません。 デザイン時には、変換元コンポーネントを使用して接続を作成、設定し、外部データ ソースから列メタデータを読み取って、外部データ ソースに基づいて変換元の出力列を設定します。 実行時には、外部データ ソースに接続し、出力バッファーに行を追加します。 データ フロー タスクは、次にデータ行のバッファーを下流コンポーネントに渡します。  
  
 データ フロー コンポーネントの開発全般の概要については、「[カスタム データ フロー コンポーネントの開発](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)」を参照してください。  
  
## <a name="design-time"></a>デザイン時  
 変換元コンポーネントのデザイン時の機能を実装する作業には、外部データ ソースへの接続の指定、データ ソースを反映する出力列の追加と設定、およびコンポーネントが実行可能かどうかの検証が含まれます。 定義上、変換元コンポーネントには入力がなく、1 つ以上の非同期出力があります。  
  
### <a name="creating-the-component"></a>コンポーネントの作成  
 変換元コンポーネントは、パッケージで定義された <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> オブジェクトを使用して、外部データ ソースに接続します。 変換元コンポーネントで、接続マネージャーに対する要求を示すには、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> プロパティの <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> コレクションに要素を追加します。 このコレクションには 2 つの目的があります。それは、コンポーネントが使用する、パッケージ内の接続マネージャーへの参照を保持することと、接続マネージャーの必要性をデザイナーに通知することです。 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100> がコレクションに追加されると、 **[詳細エディター]** に **[接続プロパティ]** タブが表示されます。このタブを使用することで、ユーザーはパッケージ内で接続を選択したり、作成したりすることができます。  
  
 次のコード例は、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> に出力と <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100> オブジェクトを追加する <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> の実装を示します。  
  
```csharp  
using System;  
using System.Collections;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.OleDb;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsPipelineComponent(DisplayName = "MySourceComponent",ComponentType = ComponentType.SourceAdapter)]  
    public class MyComponent : PipelineComponent  
    {  
        public override void ProvideComponentProperties()  
        {  
            // Reset the component.  
            base.RemoveAllInputsOutputsAndCustomProperties();  
            ComponentMetaData.RuntimeConnectionCollection.RemoveAll();  
  
            IDTSOutput100 output = ComponentMetaData.OutputCollection.New();  
            output.Name = "Output";  
  
            IDTSRuntimeConnection100 connection = ComponentMetaData.RuntimeConnectionCollection.New();  
            connection.Name = "ADO.NET";  
        }  
```  
  
```vb  
Imports System.Data  
Imports System.Data.SqlClient  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
<DtsPipelineComponent(DisplayName:="MySourceComponent", ComponentType:=ComponentType.SourceAdapter)> _  
Public Class MySourceComponent  
    Inherits PipelineComponent  
  
    Public Overrides Sub ProvideComponentProperties()  
  
        ' Allow for resetting the component.  
        RemoveAllInputsOutputsAndCustomProperties()  
        ComponentMetaData.RuntimeConnectionCollection.RemoveAll()  
  
        Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection.New()  
        output.Name = "Output"  
  
        Dim connection As IDTSRuntimeConnection100 = ComponentMetaData.RuntimeConnectionCollection.New()  
        connection.Name = "ADO.NET"  
  
    End Sub  
End Class  
```  
  
### <a name="connecting-to-an-external-data-source"></a>外部データ ソースへの接続  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> に接続を追加した後、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> メソッドをオーバーライドして、外部データ ソースへの接続を確立します。 このメソッドは、デザイン時と実行時の両方で呼び出されます。 コンポーネントは、実行時の接続によって指定された接続マネージャーへの接続を確立し、続いて外部データ ソースへの接続を確立する必要があります。  
  
 接続は、確立後にコンポーネントによって内部でキャッシュされ、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A> メソッドの呼び出し時に解放される必要があります。 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A> メソッドは、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> メソッドと同様、デザイン時と実行時に呼び出されます。 開発者はこのメソッドをオーバーライドし、コンポーネントが確立した接続を <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> の実行中に解放します。  
  
 次のコード例では、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> メソッドで ADO.NET 接続へ接続し、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A> で接続を閉じるコンポーネントを示します。  
  
```csharp  
private SqlConnection sqlConnection;  
  
public override void AcquireConnections(object transaction)  
{  
    if (ComponentMetaData.RuntimeConnectionCollection[0].ConnectionManager != null)  
    {  
        ConnectionManager cm = Microsoft.SqlServer.Dts.Runtime.DtsConvert.GetWrapper(ComponentMetaData.RuntimeConnectionCollection[0].ConnectionManager);  
        ConnectionManagerAdoNet cmado = cm.InnerObject as ConnectionManagerAdoNet;  
  
        if (cmado == null)  
            throw new Exception("The ConnectionManager " + cm.Name + " is not an ADO.NET connection.");  
  
        sqlConnection = cmado.AcquireConnection(transaction) as SqlConnection;  
        sqlConnection.Open();  
    }  
}  
  
public override void ReleaseConnections()  
{  
    if (sqlConnection != null && sqlConnection.State != ConnectionState.Closed)  
        sqlConnection.Close();  
}  
```  
  
```vb  
Private sqlConnection As SqlConnection  
  
Public Overrides Sub AcquireConnections(ByVal transaction As Object)  
  
    If Not IsNothing(ComponentMetaData.RuntimeConnectionCollection(0).ConnectionManager) Then  
  
        Dim cm As ConnectionManager = Microsoft.SqlServer.Dts.Runtime.DtsConvert.GetWrapper(ComponentMetaData.RuntimeConnectionCollection(0).ConnectionManager)  
        Dim cmado As ConnectionManagerAdoNet = CType(cm.InnerObject, ConnectionManagerAdoNet)  
  
        If IsNothing(cmado) Then  
            Throw New Exception("The ConnectionManager " + cm.Name + " is not an ADO.NET connection.")  
        End If  
  
        sqlConnection = CType(cmado.AcquireConnection(transaction), SqlConnection)  
        sqlConnection.Open()  
  
    End If  
End Sub  
  
Public Overrides Sub ReleaseConnections()  
  
    If Not IsNothing(sqlConnection) And sqlConnection.State <> ConnectionState.Closed Then  
        sqlConnection.Close()  
    End If  
  
End Sub  
```  
  
### <a name="creating-and-configuring-output-columns"></a>出力列の作成と設定  
 変換元コンポーネントの出力列は、実行中にコンポーネントがデータ フローに追加する外部データ ソースの列を反映しています。 デザイン時は、外部データ ソースに接続するようにコンポーネントを設定した後で、出力列を追加します。 出力コレクションに列を追加するため、デザイン時にコンポーネントが使用するメソッドは、そのコンポーネントの要件に応じて異なります。ただし、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> や <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A> の実行中には追加しないでください。 たとえば、コンポーネントのデータセットを制御するカスタム プロパティに SQL ステートメントが含まれると、コンポーネントは <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.SetComponentProperty%2A> メソッドで出力列を追加できます。 コンポーネントは接続がキャッシュされているかどうかを確認し、キャッシュされている場合、データ ソースに接続して出力列を生成します。  
  
 出力列を作成したら、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.SetDataTypeProperties%2A> メソッドを呼び出して、そのデータ型プロパティを設定します。 このメソッドが必要なのは、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.Length%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.Precision%2A>、および <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.CodePage%2A> の各プロパティが読み取り専用で、各プロパティの設定が他の設定に依存しているためです。 このメソッドを使用すると、これらの値に対する要件が一貫性を持つように設定され、データ フロー タスクで、設定が正しいかどうか検証されます。  
  
 列の <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A> により、他のプロパティに設定される値が決定されます。 次の表は、各 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A> の依存するプロパティの要件を示しています。 ここに示されていないデータ型の場合、依存するプロパティは 0 に設定されます。  
  
|DataType|長さ|Scale|有効桁数|CodePage|  
|--------------|------------|-----------|---------------|--------------|  
|DT_DECIMAL|0|0 より大きく 28 以下。|0|0|  
|DT_CY|0|0|0|0|  
|DT_NUMERIC|0|0 より大きく 28 以下で、有効桁数の値未満|1 以上 38 以下|0|  
|DT_BYTES|0 より大きい|0|0|0|  
|DT_STR|0 より大きく 8000 未満|0|0|0 以外の有効なコード ページ|  
|DT_WSTR|0 より大きく 4000 未満|0|0|0|  
  
 データ型プロパティの制約は出力列のデータ型に基づくため、マネージド型を処理する場合、[!INCLUDE[ssIS](../../includes/ssis-md.md)] の正しいデータ型を選択する必要があります。 基本クラスでは、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ConvertBufferDataTypeToFitManaged%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferTypeToDataRecordType%2A>、および <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.DataRecordTypeToBufferType%2A> の 3 つのヘルパー メソッドが提供され、これを使用すると、マネージド コンポーネントの開発者は、マネージド型に対応する [!INCLUDE[ssIS](../../includes/ssis-md.md)] のデータ型を適切に選択できます。 これらのメソッドは、マネージド データ型と [!INCLUDE[ssIS](../../includes/ssis-md.md)] のデータ型を相互に変換します。  
  
 次のコード例は、テーブルのスキーマに基づいて、コンポーネントの出力列コレクションを作成します。 基本クラスのヘルパー メソッドを使用して列のデータ型を設定し、そのデータ型に基づいて依存するプロパティを設定します。  
  
```csharp  
SqlCommand sqlCommand;  
  
private void CreateColumnsFromDataTable()  
{  
    // Get the output.  
    IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
  
    // Start clean, and remove the columns from both collections.  
    output.OutputColumnCollection.RemoveAll();  
    output.ExternalMetadataColumnCollection.RemoveAll();  
  
    this.sqlCommand = sqlConnection.CreateCommand();  
    this.sqlCommand.CommandType = CommandType.Text;  
    this.sqlCommand.CommandText = (string)ComponentMetaData.CustomPropertyCollection["SqlStatement"].Value;  
    SqlDataReader schemaReader = this.sqlCommand.ExecuteReader(CommandBehavior.SchemaOnly);  
    DataTable dataTable = schemaReader.GetSchemaTable();  
  
    // Walk the columns in the schema,   
    // and for each data column create an output column and an external metadata column.  
    foreach (DataRow row in dataTable.Rows)  
    {  
        IDTSOutputColumn100 outColumn = output.OutputColumnCollection.New();  
        IDTSExternalMetadataColumn100 exColumn = output.ExternalMetadataColumnCollection.New();  
  
        // Set column data type properties.  
        bool isLong = false;  
        DataType dt = DataRecordTypeToBufferType((Type)row["DataType"]);  
        dt = ConvertBufferDataTypeToFitManaged(dt, ref isLong);  
        int length = 0;  
        int precision = (short)row["NumericPrecision"];  
        int scale = (short)row["NumericScale"];  
        int codepage = dataTable.Locale.TextInfo.ANSICodePage;  
  
        switch (dt)  
        {  
            // The length cannot be zero, and the code page property must contain a valid code page.  
            case DataType.DT_STR:  
            case DataType.DT_TEXT:  
                length = precision;  
                precision = 0;  
                scale = 0;  
                break;  
  
            case DataType.DT_WSTR:  
                length = precision;  
                codepage = 0;  
                scale = 0;  
                precision = 0;  
                break;  
  
            case DataType.DT_BYTES:  
                precision = 0;  
                scale = 0;  
                codepage = 0;  
                break;  
  
            case DataType.DT_NUMERIC:  
                length = 0;  
                codepage = 0;  
  
                if (precision > 38)  
                    precision = 38;  
  
                if (scale > 6)  
                    scale = 6;  
                break;  
  
            case DataType.DT_DECIMAL:  
                length = 0;  
                precision = 0;  
                codepage = 0;  
                break;  
  
            default:  
                length = 0;  
                precision = 0;  
                codepage = 0;  
                scale = 0;  
                break;  
  
        }  
  
        // Set the properties of the output column.  
        outColumn.Name = (string)row["ColumnName"];  
        outColumn.SetDataTypeProperties(dt, length, precision, scale, codepage);  
    }  
}  
```  
  
```vb  
Private sqlCommand As SqlCommand  
  
Private Sub CreateColumnsFromDataTable()  
  
    ' Get the output.  
    Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
  
    ' Start clean, and remove the columns from both collections.  
    output.OutputColumnCollection.RemoveAll()  
    output.ExternalMetadataColumnCollection.RemoveAll()  
  
    Me.sqlCommand = sqlConnection.CreateCommand()  
    Me.sqlCommand.CommandType = CommandType.Text  
    Me.sqlCommand.CommandText = CStr(ComponentMetaData.CustomPropertyCollection("SqlStatement").Value)  
  
    Dim schemaReader As SqlDataReader = Me.sqlCommand.ExecuteReader(CommandBehavior.SchemaOnly)  
    Dim dataTable As DataTable = schemaReader.GetSchemaTable()  
  
    ' Walk the columns in the schema,   
    ' and for each data column create an output column and an external metadata column.  
    For Each row As DataRow In dataTable.Rows  
  
        Dim outColumn As IDTSOutputColumn100 = output.OutputColumnCollection.New()  
        Dim exColumn As IDTSExternalMetadataColumn100 = output.ExternalMetadataColumnCollection.New()  
  
        ' Set column data type properties.  
        Dim isLong As Boolean = False  
        Dim dt As DataType = DataRecordTypeToBufferType(CType(row("DataType"), Type))  
        dt = ConvertBufferDataTypeToFitManaged(dt, isLong)  
        Dim length As Integer = 0  
        Dim precision As Integer = CType(row("NumericPrecision"), Short)  
        Dim scale As Integer = CType(row("NumericScale"), Short)  
        Dim codepage As Integer = dataTable.Locale.TextInfo.ANSICodePage  
  
        Select Case dt  
  
            ' The length cannot be zero, and the code page property must contain a valid code page.  
            Case DataType.DT_STR  
            Case DataType.DT_TEXT  
                length = precision  
                precision = 0  
                scale = 0  
  
            Case DataType.DT_WSTR  
                length = precision  
                codepage = 0  
                scale = 0  
                precision = 0  
  
            Case DataType.DT_BYTES  
                precision = 0  
                scale = 0  
                codepage = 0  
  
            Case DataType.DT_NUMERIC  
                length = 0  
                codepage = 0  
  
                If precision > 38 Then  
                    precision = 38  
                End If  
  
                If scale > 6 Then  
                    scale = 6  
                End If  
  
            Case DataType.DT_DECIMAL  
                length = 0  
                precision = 0  
                codepage = 0  
  
            Case Else  
                length = 0  
                precision = 0  
                codepage = 0  
                scale = 0  
        End Select  
  
        ' Set the properties of the output column.  
        outColumn.Name = CStr(row("ColumnName"))  
        outColumn.SetDataTypeProperties(dt, length, precision, scale, codepage)  
    Next  
End Sub  
```  
  
### <a name="validating-the-component"></a>コンポーネントの検証  
 変換元コンポーネントを検証して、出力列コレクションに定義された列が、外部データ ソースの列と一致することを確認する必要があります。 ただし、接続状態でない場合や、サーバーへの長いラウンド トリップを避けたほうがよい場合など、外部データ ソースに対する出力列の検証が不可能なこともあります。 このような状況でも、出力オブジェクトの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.ExternalMetadataColumnCollection%2A> を使用して、出力の列を検証することができます。 詳細については、「[データ フロー コンポーネントの検証](../extending-packages-custom-objects/data-flow/validating-a-data-flow-component.md)」を参照してください。  
  
 このコレクションは入力オブジェクトと出力オブジェクトのどちらにも存在し、外部データ ソースの列によって作成できます。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーがオフラインである場合、コンポーネントが接続されていない場合、または <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> プロパティが `false` の場合に、このコレクションを使用して出力列を検証できます。 コレクションは、出力列の作成と同時に設定しておく必要があります。 外部メタデータ列は初期状態で出力列と一致しているため、コレクションに外部メタデータ列を追加するのは比較的簡単です。 列のデータ型プロパティは、あらかじめ正しく設定されている必要があります。また、プロパティは <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100> オブジェクトに直接コピーすることができます。  
  
 次のコード例は、新しく作成された出力列に基づく外部メタデータ列を追加します。 出力列はあらかじめ作成されているものとします。  
  
```csharp  
private void CreateExternalMetaDataColumn(IDTSOutput100 output, IDTSOutputColumn100 outputColumn)  
{  
  
    // Set the properties of the external metadata column.  
    IDTSExternalMetadataColumn100 externalColumn = output.ExternalMetadataColumnCollection.New();  
    externalColumn.Name = outputColumn.Name;  
    externalColumn.Precision = outputColumn.Precision;  
    externalColumn.Length = outputColumn.Length;  
    externalColumn.DataType = outputColumn.DataType;  
    externalColumn.Scale = outputColumn.Scale;  
  
    // Map the external column to the output column.  
    outputColumn.ExternalMetadataColumnID = externalColumn.ID;  
  
}  
```  
  
```vb  
Private Sub CreateExternalMetaDataColumn(ByVal output As IDTSOutput100, ByVal outputColumn As IDTSOutputColumn100)  
  
        ' Set the properties of the external metadata column.  
        Dim externalColumn As IDTSExternalMetadataColumn100 = output.ExternalMetadataColumnCollection.New()  
        externalColumn.Name = outputColumn.Name  
        externalColumn.Precision = outputColumn.Precision  
        externalColumn.Length = outputColumn.Length  
        externalColumn.DataType = outputColumn.DataType  
        externalColumn.Scale = outputColumn.Scale  
  
        ' Map the external column to the output column.  
        outputColumn.ExternalMetadataColumnID = externalColumn.ID  
  
    End Sub  
```  
  
## <a name="run-time"></a>実行時間  
 実行中、コンポーネントは、データ フロー タスクによって作成され、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> でコンポーネントに渡される出力バッファーに行を追加します。 変換元コンポーネントでこのメソッドが呼び出されると、メソッドは、下流コンポーネントに接続されたコンポーネントの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> ごとに出力バッファーを受け取ります。  
  
### <a name="locating-columns-in-the-buffer"></a>バッファー内の列の検索  
 コンポーネントの出力バッファーには、このコンポーネントで定義されている列、および下流コンポーネントの出力に追加されたすべての列が含まれます。 たとえば、変換元コンポーネントの出力に 3 つの列があり、次のコンポーネントでもう 1 つ出力列を追加している場合、変換元コンポーネントによって提供された出力バッファーには 4 つの列が含まれます。  
  
 バッファー行の列の順序は、出力列コレクション内の出力列のインデックスでは定義されません。 バッファー行で出力列を正確に検索するには、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSBufferManagerClass.FindColumnByLineageID%2A> の <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> メソッドを使用するしか方法がありません。 このメソッドは、指定されたバッファー内で指定された系列 ID の列を検索し、行内の位置を返します。 出力列のインデックスは、通常、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> メソッド内で検索され、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> で使用するために保存されます。  
  
 次のコード例は、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> を呼び出して出力バッファー内の出力列の位置を検索し、内部構造に保存します。 列の名前もこの構造に保存され、このトピックの次のセクションで、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> メソッドのコード例で使用されています。  
  
```csharp  
ArrayList columnInformation;  
  
private struct ColumnInfo  
{  
    public int BufferColumnIndex;  
    public string ColumnName;  
}  
  
public override void PreExecute()  
{  
    this.columnInformation = new ArrayList();  
    IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
  
    foreach (IDTSOutputColumn100 col in output.OutputColumnCollection)  
    {  
        ColumnInfo ci = new ColumnInfo();  
        ci.BufferColumnIndex = BufferManager.FindColumnByLineageID(output.Buffer, col.LineageID);  
        ci.ColumnName = col.Name;  
        columnInformation.Add(ci);  
    }  
}  
```  
  
```vb  
Public Overrides Sub PreExecute()  
  
    Me.columnInformation = New ArrayList()  
    Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
  
    For Each col As IDTSOutputColumn100 In output.OutputColumnCollection  
  
        Dim ci As ColumnInfo = New ColumnInfo()  
        ci.BufferColumnIndex = BufferManager.FindColumnByLineageID(output.Buffer, col.LineageID)  
        ci.ColumnName = col.Name  
        columnInformation.Add(ci)  
    Next  
End Sub  
```  
  
### <a name="processing-rows"></a>行の処理  
 出力バッファーに行を追加するには、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.AddRow%2A> メソッドを呼び出します。このメソッドは、新しいバッファー行を作成して、列に空の値を設定します。 次に、コンポーネントは個々の列に値を割り当てます。 コンポーネントに提供される出力バッファーは、データ フロー タスクによって作成され、監視されます。 バッファーがいっぱいになると、バッファーの行が次のコンポーネントに移動します。 コンポーネント開発者は、データ フロー タスクによる行の移動を意識することがなく、出力バッファーでは <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.RowCount%2A> プロパティは常に 0 のままであるため、行の一部が次のコンポーネントに送られるタイミングを確認する方法はありません。 変換元コンポーネントは、出力バッファーに対する行の追加を終了すると、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetEndOfRowset%2A> の <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> メソッドを呼び出し、バッファー内の残りの行を次のコンポーネントに渡して、追加が終了したことをデータ フロー タスクに通知します。  
  
 変換元コンポーネントが行を外部データ ソースから読み込んでいる間に、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.IncrementPipelinePerfCounter%2A> メソッドを呼び出して "Rows read" または "BLOB bytes read" パフォーマンス カウンターを更新することができます。 これらのパフォーマンス カウンターの詳細については、「 [パフォーマンス カウンター](../performance/performance-counters.md)」を参照してください。  
  
 次のコード例は、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> で出力バッファーに行を追加します。 バッファー内の出力列のインデックスは、先のコード例にある <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 内で検索したものを使用します。  
  
```csharp  
public override void PrimeOutput(int outputs, int[] outputIDs, PipelineBuffer[] buffers)  
{  
    IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
    PipelineBuffer buffer = buffers[0];  
  
    SqlDataReader dataReader = sqlCommand.ExecuteReader();  
  
    // Loop over the rows in the DataReader,   
    // and add them to the output buffer.  
    while (dataReader.Read())  
    {  
        // Add a row to the output buffer.  
        buffer.AddRow();  
  
        for (int x = 0; x < columnInformation.Count; x++)  
        {  
            ColumnInfo ci = (ColumnInfo)columnInformation[x];  
            int ordinal = dataReader.GetOrdinal(ci.ColumnName);  
  
            if (dataReader.IsDBNull(ordinal))  
                buffer.SetNull(ci.BufferColumnIndex);  
            else  
            {  
                buffer[ci.BufferColumnIndex] = dataReader[ci.ColumnName];  
            }  
        }  
    }  
    buffer.SetEndOfRowset();  
}  
```  
  
```vb  
Public Overrides Sub PrimeOutput(ByVal outputs As Integer, ByVal outputIDs As Integer(), ByVal buffers As PipelineBuffer())  
  
    Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
    Dim buffer As PipelineBuffer = buffers(0)  
  
    Dim dataReader As SqlDataReader = sqlCommand.ExecuteReader()  
  
    ' Loop over the rows in the DataReader,   
    ' and add them to the output buffer.  
    While (dataReader.Read())  
  
        ' Add a row to the output buffer.  
        buffer.AddRow()  
  
        For x As Integer = 0 To columnInformation.Count  
  
            Dim ci As ColumnInfo = CType(columnInformation(x), ColumnInfo)  
  
            Dim ordinal As Integer = dataReader.GetOrdinal(ci.ColumnName)  
  
            If (dataReader.IsDBNull(ordinal)) Then  
                buffer.SetNull(ci.BufferColumnIndex)  
            Else  
                buffer(ci.BufferColumnIndex) = dataReader(ci.ColumnName)  
  
            End If  
        Next  
  
    End While  
  
    buffer.SetEndOfRowset()  
End Sub  
```  
  
## <a name="sample"></a>サンプル  
 次の例は、ファイル接続マネージャーを使用して、ファイルのバイナリ コンテンツをデータ フローに読み込む、簡単な変換元コンポーネントを示しています。 ただし、この例ではここで説明したメソッドや機能のすべてが使われているわけではありません。 変換元コンポーネントが必ずオーバーライドしなければならない重要なメソッドは示していますが、デザイン時の検証のためのコードは含まれていません。  
  
```csharp  
using System;  
using System.IO;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
namespace BlobSrc  
{  
  [DtsPipelineComponent(DisplayName = "BLOB Inserter Source", Description = "Inserts files into the data flow as BLOBs")]  
  public class BlobSrc : PipelineComponent  
  {  
    IDTSConnectionManager100 m_ConnMgr;  
    int m_FileNameColumnIndex = -1;  
    int m_FileBlobColumnIndex = -1;  
  
    public override void ProvideComponentProperties()  
    {  
      IDTSOutput100 output = ComponentMetaData.OutputCollection.New();  
      output.Name = "BLOB File Inserter Output";  
  
      IDTSOutputColumn100 column = output.OutputColumnCollection.New();  
      column.Name = "FileName";  
      column.SetDataTypeProperties(DataType.DT_WSTR, 256, 0, 0, 0);  
  
      column = output.OutputColumnCollection.New();  
      column.Name = "FileBLOB";  
      column.SetDataTypeProperties(DataType.DT_IMAGE, 0, 0, 0, 0);  
  
      IDTSRuntimeConnection100 conn = ComponentMetaData.RuntimeConnectionCollection.New();  
      conn.Name = "FileConnection";  
    }  
  
    public override void AcquireConnections(object transaction)  
    {  
      IDTSRuntimeConnection100 conn = ComponentMetaData.RuntimeConnectionCollection[0];  
      m_ConnMgr = conn.ConnectionManager;  
    }  
  
    public override void ReleaseConnections()  
    {  
      m_ConnMgr = null;  
    }  
  
    public override void PreExecute()  
    {  
      IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
  
      m_FileNameColumnIndex = (int)BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection[0].LineageID);  
      m_FileBlobColumnIndex = (int)BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection[1].LineageID);  
    }  
  
    public override void PrimeOutput(int outputs, int[] outputIDs, PipelineBuffer[] buffers)  
    {  
      string strFileName = (string)m_ConnMgr.AcquireConnection(null);  
  
      while (strFileName != null)  
      {  
        buffers[0].AddRow();  
  
        buffers[0].SetString(m_FileNameColumnIndex, strFileName);  
  
        FileInfo fileInfo = new FileInfo(strFileName);  
        byte[] fileData = new byte[fileInfo.Length];  
        FileStream fs = new FileStream(strFileName, FileMode.Open, FileAccess.Read, FileShare.Read);  
        fs.Read(fileData, 0, fileData.Length);  
  
        buffers[0].AddBlobData(m_FileBlobColumnIndex, fileData);  
  
        strFileName = (string)m_ConnMgr.AcquireConnection(null);  
      }  
  
      buffers[0].SetEndOfRowset();  
    }  
  }  
}  
```  
  
```vb  
Imports System   
Imports System.IO   
Imports Microsoft.SqlServer.Dts.Pipeline   
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper   
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper   
Namespace BlobSrc   
  
 <DtsPipelineComponent(DisplayName="BLOB Inserter Source", Description="Inserts files into the data flow as BLOBs")> _   
 Public Class BlobSrc   
 Inherits PipelineComponent   
   Private m_ConnMgr As IDTSConnectionManager100   
   Private m_FileNameColumnIndex As Integer = -1   
   Private m_FileBlobColumnIndex As Integer = -1   
  
   Public  Overrides Sub ProvideComponentProperties()   
     Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection.New   
     output.Name = "BLOB File Inserter Output"   
     Dim column As IDTSOutputColumn100 = output.OutputColumnCollection.New   
     column.Name = "FileName"   
     column.SetDataTypeProperties(DataType.DT_WSTR, 256, 0, 0, 0)   
     column = output.OutputColumnCollection.New   
     column.Name = "FileBLOB"   
     column.SetDataTypeProperties(DataType.DT_IMAGE, 0, 0, 0, 0)   
     Dim conn As IDTSRuntimeConnection90 = ComponentMetaData.RuntimeConnectionCollection.New   
     conn.Name = "FileConnection"   
   End Sub   
  
   Public  Overrides Sub AcquireConnections(ByVal transaction As Object)   
     Dim conn As IDTSRuntimeConnection100 = ComponentMetaData.RuntimeConnectionCollection(0)   
     m_ConnMgr = conn.ConnectionManager   
   End Sub   
  
   Public  Overrides Sub ReleaseConnections()   
     m_ConnMgr = Nothing   
   End Sub   
  
   Public  Overrides Sub PreExecute()   
     Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)   
     m_FileNameColumnIndex = CType(BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection(0).LineageID), Integer)   
     m_FileBlobColumnIndex = CType(BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection(1).LineageID), Integer)   
   End Sub   
  
   Public  Overrides Sub PrimeOutput(ByVal outputs As Integer, ByVal outputIDs As Integer(), ByVal buffers As PipelineBuffer())   
     Dim strFileName As String = CType(m_ConnMgr.AcquireConnection(Nothing), String)   
     While Not (strFileName Is Nothing)   
       buffers(0).AddRow   
       buffers(0).SetString(m_FileNameColumnIndex, strFileName)   
       Dim fileInfo As FileInfo = New FileInfo(strFileName)   
       Dim fileData(fileInfo.Length) As Byte   
       Dim fs As FileStream = New FileStream(strFileName, FileMode.Open, FileAccess.Read, FileShare.Read)   
       fs.Read(fileData, 0, fileData.Length)   
       buffers(0).AddBlobData(m_FileBlobColumnIndex, fileData)   
       strFileName = CType(m_ConnMgr.AcquireConnection(Nothing), String)   
     End While   
     buffers(0).SetEndOfRowset   
   End Sub   
 End Class   
End Namespace  
```  
  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [カスタム変換先コンポーネントの開発](../extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)   
 [スクリプト コンポーネントによる変換元の作成](../extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)  
  
  
