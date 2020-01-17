---
title: プログラムによるデータ フロー コンポーネントの追加| Microsoft Docs
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
- data flow task [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: c06065cf-43e5-4b6b-9824-7309d7f5e35e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 286b37195b200761ce8cd8e941076c8a27e61011
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62836808"
---
# <a name="adding-data-flow-components-programmatically"></a>プログラムによるデータ フロー コンポーネントの追加
  データ フローを作成するには、最初にコンポーネントを追加します。 次に、追加したコンポーネントを構成して相互に接続し、実行時のデータ フローを確立します。 このセクションでは、データ フロー タスクへのコンポーネントの追加、コンポーネントのデザイン時インスタンスの作成、およびコンポーネントの構成について説明します。 コンポーネントの接続方法については、「[プログラムによるデータ フロー コンポーネントの接続](../building-packages-programmatically/connecting-data-flow-components-programmatically.md)」を参照してください。  
  
## <a name="adding-a-component"></a>コンポーネントの追加  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaDataCollection100.New%2A> コレクションの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipeClass.ComponentMetaDataCollection%2A> メソッドを呼び出して新しいコンポーネントを作成し、データ フロー タスクに追加します。 このメソッドは、コンポーネントの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> インターフェイスを返します。 ただしこの時点で、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> には、いずれかのコンポーネントに固有な情報は含まれていません。 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> プロパティを設定し、コンポーネントの種類を識別します。 データ フロー タスクはこのプロパティの値を使用して、実行時にコンポーネントのインスタンスを作成します。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> プロパティの値には、CLSID、PROGID、またはコンポーネントの <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo.CreationName%2A> プロパティを指定できます。 CLSID は通常、コンポーネントの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> プロパティの値として [プロパティ] ウィンドウに表示されます。 このプロパティ、および使用できるコンポーネントの他のプロパティの取得については、「[プログラムによるデータ フロー コンポーネントの検出](../building-packages-programmatically/discovering-data-flow-components-programmatically.md)」を参照してください。  
  
## <a name="adding-a-managed-component"></a>マネージド コンポーネントの追加  
 CLSID または PROGID を使用して、いずれかのマネージド データ フロー コンポーネントをデータ フローに追加することはできません。これらの値はコンポーネント自体ではなく、ラッパーを指しているためです。 その代わり、次のサンプルに示すように、`CreationName` プロパティまたは `AssemblyQualifiedName` プロパティを使用できます。  
  
 `AssemblyQualifiedName` プロパティを使用する場合は、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] プロジェクトで、マネージド コンポーネントを含んでいるアセンブリに参照を追加する必要があります。 これらのアセンブリは、 **[参照の追加]** ダイアログ ボックスの [.NET] タブに一覧表示されません。 通常は、**C:\Program Files\Microsoft SQL Server\100\DTS\PipelineComponents** フォルダーを参照してアセンブリを見つける必要があります。  
  
 組み込みマネージド データ フロー コンポーネントの要素は次のとおりです。  
  
-   [!INCLUDE[vstecado](../../includes/vstecado-md.md)] ソース  
  
-   XML ソース  
  
-   DataReader 変換先  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 変換先  
  
-   スクリプト コンポーネント  
  
 次のコード サンプルは、マネージド コンポーネントをデータ フローに追加するための 2 つの方法を示しています。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Microsoft.SqlServer.Dts.Runtime.Package package = new Microsoft.SqlServer.Dts.Runtime.Package();  
      Executable e = package.Executables.Add("STOCK:PipelineTask");  
      Microsoft.SqlServer.Dts.Runtime.TaskHost thMainPipe = (Microsoft.SqlServer.Dts.Runtime.TaskHost)e;  
      MainPipe dataFlowTask = (MainPipe)thMainPipe.InnerObject;  
  
      // The Application object will be used to obtain the CreationName  
      //  of a PipelineComponentInfo from its PipelineComponentInfos collection.  
      Application app = new Application();  
  
      // Add a first ADO NET source to the data flow.  
      //  The CreationName property requires an Application instance.  
      IDTSComponentMetaData100 component1 = dataFlowTask.ComponentMetaDataCollection.New();  
      component1.Name = "DataReader Source";  
      component1.ComponentClassID = app.PipelineComponentInfos["DataReader Source"].CreationName;  
  
      // Add a second ADO NET source to the data flow.  
      //  The AssemblyQualifiedName property requires a reference to the assembly.  
      IDTSComponentMetaData100 component2 = dataFlowTask.ComponentMetaDataCollection.New();  
      component2.Name = "DataReader Source";  
      component2.ComponentClassID = typeof(Microsoft.SqlServer.Dts.Pipeline.DataReaderSourceAdapter).AssemblyQualifiedName;  
    }  
  }  
}  
  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Microsoft.SqlServer.Dts.Runtime.Package = _  
      New Microsoft.SqlServer.Dts.Runtime.Package()  
    Dim e As Executable = package.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As Microsoft.SqlServer.Dts.Runtime.TaskHost = _  
      CType(e, Microsoft.SqlServer.Dts.Runtime.TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
    ' The Application object will be used to obtain the CreationName  
    '  of a PipelineComponentInfo from its PipelineComponentInfos collection.  
    Dim app As New Application()  
  
    ' Add a first ADO NET source to the data flow.  
    '  The CreationName property requires an Application instance.  
    Dim component1 As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    component1.Name = "DataReader Source"  
    component1.ComponentClassID = app.PipelineComponentInfos("DataReader Source").CreationName  
  
    ' Add a second ADO NET source to the data flow.  
    '  The AssemblyQualifiedName property requires a reference to the assembly.  
    Dim component2 As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    component2.Name = "DataReader Source"  
    component2.ComponentClassID = _  
      GetType(Microsoft.SqlServer.Dts.Pipeline.DataReaderSourceAdapter).AssemblyQualifiedName  
  
  End Sub  
  
End Module  
```  
  
## <a name="creating-the-design-time-instance-of-the-component"></a>コンポーネントのデザイン時インスタンスの作成  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.Instantiate%2A> メソッドを呼び出し、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> プロパティによって識別される、コンポーネントのデザイン時インスタンスを作成します。 このメソッドは、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapper> インターフェイスのマネージド ラッパーである <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> オブジェクトを返します。  
  
 可能な限り、コンポーネントのメタデータを直接変更するのではなく、必ずデザイン時インスタンスのメソッドを使用して、コンポーネントを変更する必要があります。 メタデータには、接続など、直接設定する必要のあるアイテムがありますが、メタデータを直接変更すると、コンポーネントが変更を監視および検証する機能がバイパスされるため、一般的にはお勧めしません。  
  
## <a name="assigning-connections"></a>接続の割り当て  
 OLE DB ソース コンポーネントなどの一部のコンポーネントは外部データに接続する必要があるため、パッケージ内にある既存の <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> オブジェクトをこの目的で使用します。 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnectionCollection100.Count%2A> コレクションの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> プロパティは、コンポーネントが必要とする、実行時の <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> オブジェクトの数を示します。 この数が 0 より大きい場合、コンポーネントには接続が必要です。 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100.ConnectionManager%2A> の最初の接続の <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100.Name%2A> および <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> プロパティを指定して、パッケージの接続マネージャーをコンポーネントに割り当てます。 実行時の接続コレクション内にある接続マネージャーの名前は、パッケージから参照される接続マネージャーの名前と一致する必要があります。  
  
## <a name="setting-the-values-of-custom-properties"></a>カスタム プロパティの値の設定  
 コンポーネントのデザイン時インスタンスを作成したら、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ProvideComponentProperties%2A> メソッドを呼び出します。 このメソッドは、コンストラクターと同様、新しく作成されたコンポーネントのカスタム プロパティと入力および出力オブジェクトを作成することにより、そのコンポーネントを初期化します。 コンポーネントがリセットされ、メタデータに加えられた以前の変更が失われるため、1 つのコンポーネントで <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ProvideComponentProperties%2A> を複数回呼び出さないでください。  
  
 コンポーネントの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.CustomPropertyCollection%2A> には、コンポーネント固有の <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100> オブジェクトのコレクションが含まれています。 オブジェクトのプロパティが常に可視である他のプログラミング モデルとは異なり、コンポーネントは <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ProvideComponentProperties%2A> メソッドが呼び出されたときにのみ、そのコンポーネントのカスタム プロパティのコレクションを設定します。 メソッドを呼び出したら、コンポーネントのデザイン時インスタンスの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.SetComponentProperty%2A> メソッドを使用して、コンポーネントのカスタム プロパティに値を割り当てます。 このメソッドは、カスタム プロパティを識別する名前と値のペアを受け取り、新しい値を設定します。  
  
## <a name="initializing-output-columns"></a>出力列の初期化  
 コンポーネントをタスクに追加して構成したら、オブジェクトの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> で列のコレクションを初期化します。 この手順は変換元コンポーネントに特に関連するものです。変換および変換先コンポーネントの列は、一般的に、上流コンポーネントから受け取る列に依存するため、この手順では初期化されない場合があります。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ReinitializeMetaData%2A> メソッドを呼び出し、変換元コンポーネントの出力の列を初期化します。 コンポーネントは外部データ ソースに自動的には接続されないので、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.AcquireConnections%2A> を呼び出す前に <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ReinitializeMetaData%2A> メソッドを呼び出して、コンポーネントに外部データ ソースへのアクセスを提供し、列のメタデータを設定します。 最後に <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ReleaseConnections%2A> メソッドを呼び出し、接続を解放します。  
  
## <a name="next-step"></a>次の手順  
 コンポーネントを追加して構成したら、次の手順としてコンポーネント間のパスを作成します。これについては、トピック「[2 つのコンポーネント間のパスの作成](../building-packages-programmatically/connecting-data-flow-components-programmatically.md)」で説明します。  
  
## <a name="sample"></a>サンプル  
 次のコード例は、OLE DB ソース コンポーネントをデータ フロー タスクに追加し、コンポーネントのデザイン時インスタンスを作成して、コンポーネントのプロパティを構成します。 この例では、アセンブリ Microsoft.SqlServer.DTSRuntimeWrap に対する追加の参照が必要です。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Runtime.Package package = new Runtime.Package();  
      Executable e = package.Executables.Add("STOCK:PipelineTask");  
      Runtime.TaskHost thMainPipe = e as Runtime.TaskHost;  
      MainPipe dataFlowTask = thMainPipe.InnerObject as MainPipe;  
  
      // Add an OLEDB connection manager to the package.  
      ConnectionManager cm = package.Connections.Add("OLEDB");  
      cm.Name = "OLEDB ConnectionManager";  
      cm.ConnectionString = "Data Source=(local);" +   
        "Initial Catalog=AdventureWorks;Provider=SQLOLEDB.1;" +   
        "Integrated Security=SSPI;"  
  
      // Add an OLE DB source to the data flow.  
      IDTSComponentMetaData100 component =   
        dataFlowTask.ComponentMetaDataCollection.New();  
      component.Name = "OLEDBSource";  
      component.ComponentClassID = "DTSAdapter.OleDbSource.1";  
      // You can also use the CLSID of the component instead of the PROGID.  
      //component.ComponentClassID = "{2C0A8BE5-1EDC-4353-A0EF-B778599C65A0}";  
  
      // Get the design time instance of the component.  
      CManagedComponentWrapper instance = component.Instantiate();  
  
      // Initialize the component  
      instance.ProvideComponentProperties();  
  
      // Specify the connection manager.  
      if (component.RuntimeConnectionCollection.Count > 0)  
      {  
        component.RuntimeConnectionCollection[0].ConnectionManager =   
          DtsConvert.GetExtendedInterface(package.Connections[0]);  
        component.RuntimeConnectionCollection[0].ConnectionManagerID =   
          package.Connections[0].ID;      }  
  
      // Set the custom properties.  
      instance.SetComponentProperty("AccessMode", 2);  
      instance.SetComponentProperty("SqlCommand",   
        "Select * from Production.Product");  
  
      // Reinitialize the metadata.  
      instance.AcquireConnections(null);  
      instance.ReinitializeMetaData();  
      instance.ReleaseConnections();  
  
      // Add other components to the data flow and connect them.  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Microsoft.SqlServer.Dts.Runtime.Package = _  
      New Microsoft.SqlServer.Dts.Runtime.Package()  
    Dim e As Executable = package.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As Microsoft.SqlServer.Dts.Runtime.TaskHost = _  
      CType(e, Microsoft.SqlServer.Dts.Runtime.TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
    ' Add an OLEDB connection manager to the package.  
    Dim cm As ConnectionManager = package.Connections.Add("OLEDB")  
    cm.Name = "OLEDB ConnectionManager"  
    cm.ConnectionString = "Data Source=(local);" & _  
      "Initial Catalog=AdventureWorks;Provider=SQLOLEDB.1;" & _  
      "Integrated Security=SSPI;"  
  
    ' Add an OLE DB source to the data flow.  
    Dim component As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    component.Name = "OLEDBSource"  
    component.ComponentClassID = "DTSAdapter.OleDbSource.1"  
    ' You can also use the CLSID of the component instead of the PROGID.  
    'component.ComponentClassID = "{2C0A8BE5-1EDC-4353-A0EF-B778599C65A0}";  
  
    ' Get the design time instance of the component.  
    Dim instance As CManagedComponentWrapper = component.Instantiate()  
  
    ' Initialize the component.  
    instance.ProvideComponentProperties()  
  
    ' Specify the connection manager.  
    If component.RuntimeConnectionCollection.Count > 0 Then  
      component.RuntimeConnectionCollection(0).ConnectionManager = _  
        DtsConvert.GetExtendedInterface(package.Connections(0))  
      component.RuntimeConnectionCollection(0).ConnectionManagerID = _  
        package.Connections(0).ID  
    End If  
  
    ' Set the custom properties.  
    instance.SetComponentProperty("AccessMode", 2)  
    instance.SetComponentProperty("SqlCommand", _  
      "Select * from Production.Product")  
  
    ' Reinitialize the metadata.  
    instance.AcquireConnections(vbNull)  
    instance.ReinitializeMetaData()  
    instance.ReleaseConnections()  
  
    ' Add other components to the data flow and connect them.  
  
  End Sub  
  
End Module  
```  
  
## <a name="external-resources"></a>外部リソース  
 blogs.msdn.com のブログ「[EzAPI - Updated for SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=243223)」(EzAPI - SQL Server 2012 用の更新)  
  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [プログラムによるデータ フロー コンポーネントの接続](../building-packages-programmatically/connecting-data-flow-components-programmatically.md)  
  
  
