---
title: データ フロー コンポーネント用ユーザー インターフェイスの開発 | Microsoft Docs
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
- data flow components [Integration Services], custom editors
- user interfaces [Integration Services]
- custom data flow components [Integration Services], custom editors
- custom component editors [Integration Services]
- IDtsComponentUI interface
- UITypeName property
- custom user interface [Integration Services], custom data flow component
- editors [Integration Services]
ms.assetid: 10b829a1-609b-42e3-9070-cfe5a2bb698c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 273e0343fc57af419a349725482047df08619cdd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62896324"
---
# <a name="developing-a-user-interface-for-a-data-flow-component"></a>データ フロー コンポーネント用ユーザー インターフェイスの開発
  コンポーネント開発者は、コンポーネント用のカスタム ユーザー インターフェイスを作成し、コンポーネントを編集するときに [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] に表示させることができます。 カスタム ユーザー インターフェイスを実装すると、データ フロー タスクでコンポーネントが追加または削除されたとき、またはコンポーネントに関するヘルプが要求されたときに通知されます。  
  
 コンポーネント用のカスタム ユーザー インターフェイスを提供しない場合でも、ユーザーは、詳細エディターを使用することで、コンポーネントおよびそのカスタム プロパティを構成することができます。 詳細エディターでユーザーがカスタム プロパティ値を適切に変更できるようにするには、必要に応じて、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.TypeConverter%2A> の <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.UITypeEditor%2A> および <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100> プロパティを使用します。 詳細については、「[データ フロー コンポーネントのデザイン時のメソッド](design-time-methods-of-a-data-flow-component.md)」の「カスタム プロパティの作成」を参照してください。  
  
## <a name="setting-the-uitypename-property"></a>UITypeName プロパティの設定  
 カスタム ユーザー インターフェイスを提供するには、<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.UITypeName%2A> の <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> プロパティに、<xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI> インターフェイスを実装したクラスの名前を登録する必要があります。 このプロパティがコンポーネントによって設定されると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] の [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでコンポーネントを編集する際に、カスタム ユーザー インターフェイスが読み込まれ、必要な処理が呼び出されます。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.UITypeName%2A> プロパティは、型の完全修飾名を示すコンマ区切り形式の文字列です。 次の一覧は、型を識別する要素を順に示したものです。  
  
-   種類の名前。  
  
-   アセンブリ名  
  
-   ファイル バージョン  
  
-   カルチャ  
  
-   パブリック キー トークン  
  
 次のコード サンプルは、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 基本クラスから派生し、<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.UITypeName%2A> プロパティを指定するクラスを示します。  
  
```csharp  
[DtsPipelineComponent(  
DisplayName="SampleComponent",  
UITypeName="MyNamespace.MyComponentUIClassName,MyAssemblyName,Version=1.0.0.0,Culture=neutral,PublicKeyToken=abcd...",  
ComponentType = ComponentType.Transform)]  
public class SampleComponent : PipelineComponent  
{  
//TODO: Implement the component here.  
}  
```  
  
```vb  
<DtsPipelineComponent(DisplayName="SampleComponent", _  
UITypeName="MyNamespace.MyComponentUIClassName,MyAssemblyName,Version=1.0.0.0,Culture=neutral,PublicKeyToken=abcd...", ComponentType=ComponentType.Transform)> _   
Public Class SampleComponent   
 Inherits PipelineComponent   
End Class  
```  
  
## <a name="implementing-the-idtscomponentui-interface"></a>IDtsComponentUI インターフェイスの実装  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI> インターフェイスには、コンポーネントが追加、削除、および編集されたときに [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーが呼び出すメソッドがあります。 コンポーネント開発者は、これらのメソッドを実装する際にコードを記述することにより、ユーザーがコンポーネントを対話的に操作できるようにできます。  
  
 このクラスは通常、コンポーネント自体とは別個のアセンブリに実装します。 別個のアセンブリの使用は必須ではありませんが、これを使用することで、開発者はコンポーネントとユーザー インターフェイスを相互に独立に作成および配置することができ、コンポーネントのバイナリの占有領域を少なく抑えることができます。  
  
 カスタム ユーザー インターフェイスを実装すると、[!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでコンポーネントを編集する場合に比べ、コンポーネントの制御に関して開発者の意図をより反映することができます。 たとえば <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.New%2A> メソッドにコードを追加し、データ フロー タスクに最初にコンポーネントが追加されたときにこのコードを呼び出して、コンポーネントの初期設定の手順を示すウィザードを表示することができます。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI> インターフェイスを実装するクラスを作成した後、ユーザーがコンポーネントに対して操作を行ったときに応答するコードを追加する必要があります。 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Initialize%2A> メソッドは、コンポーネントの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> インターフェイスを提供するもので、<xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.New%2A> メソッドや <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Edit%2A> メソッドの実行前に呼び出されます。 この参照は、プライベート メンバー変数に保存しておき、後でコンポーネントのメタデータを修正する際に使用します。  
  
## <a name="modifying-a-component-and-persisting-changes"></a>コンポーネントの修正と変更の保存  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> インターフェイスは、パラメーターとして <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Initialize%2A> メソッドに渡されます。 この参照は、ユーザー インターフェイスを実装するコードによってメンバー変数にキャッシュされ、このユーザー インターフェイスに対するユーザー操作に応じてコンポーネントを修正するために使用されます。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> インターフェイスを介してコンポーネントを直接修正することも可能ですが、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapper> メソッドを使用して、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.Instantiate%2A> のインスタンスを作成することをお勧めします。 インターフェイスを使用してコンポーネントを直接編集すると、コンポーネントの検証処理が省略されるためです。 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapper> を介してコンポーネントのデザイン時インスタンスを使用する利点は、コンポーネントに加えられた変更が確実にコンポーネント側で制御されるという点です。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Edit%2A> メソッドの戻り値は、コンポーネントに加えられた変更が保存されたか、破棄されたかを示します。 このメソッドによって `false` が返される場合、変更はすべて破棄されます。`true` の場合、コンポーネントに対する変更が保存され、パッケージを保存する必要があることを示すマークが付けられます。  
  
### <a name="using-the-services-of-the-ssis-designer"></a>SSIS デザイナーのサービスの使用  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Initialize%2A> メソッドの `IServiceProvider` パラメーターにより、[!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーの、次のサービスにアクセスすることができます。  
  
|サービス|説明|  
|-------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Design.IDtsClipboardService>|コンポーネントがコピー/貼り付け、または切り取り/貼り付け操作の一部として生成されたかどうかを判別するために使用します。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionService>|パッケージ内の既存の接続へのアクセス、または新しい接続の作成に使用します。|  
|<xref:Microsoft.SqlServer.Dts.Design.IErrorCollectionService>|最後に発生したエラーまたは警告だけを受け取るのではなく、コンポーネントで生成されたすべてのエラーおよび警告をキャプチャする必要がある場合に、データ フロー コンポーネントからのイベントをキャプチャするために使用します。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsVariableService>|パッケージ内の既存の変数へのアクセス、または新しい変数の作成に使用します。|  
|<xref:Microsoft.SqlServer.Dts.Design.IDtsPipelineEnvironmentService>|データ フロー コンポーネントで親データ フロー タスクおよびデータ フロー内の他のコンポーネントにアクセスするために使用します。 この機能は、必要に応じて追加のデータ フロー コンポーネントを作成して接続するための、緩やかに変化するディメンション ウィザードなどのコンポーネントを開発する際に使用できます。|  
  
 コンポーネント開発者は、これらのサービスを利用することにより、コンポーネントを読み込むパッケージ内のオブジェクトへのアクセスやオブジェクトの作成を行えます。  
  
## <a name="sample"></a>サンプル  
 次のコード例では、<xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI> インターフェイスを実装したカスタム ユーザー インターフェイス クラスと、コンポーネントのエディターとして使用できる Windows フォームの統合を示します。  
  
### <a name="custom-user-interface-class"></a>カスタム ユーザー インターフェイス クラス  
 次のコードは、<xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI> インターフェイスを実装するクラスを示します。 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Edit%2A> メソッドは、コンポーネント エディターを作成し、そのフォームを表示します。 フォームの戻り値により、コンポーネントに対する変更が保持されるかどうかが決定されます。  
  
```csharp  
using System;  
using System.Windows.Forms;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Pipeline.Design;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    public class SampleComponentUI : IDtsComponentUI  
    {  
        IDTSComponentMetaData100 md;  
        IServiceProvider sp;  
  
        public void Help(System.Windows.Forms.IWin32Window parentWindow)  
        {  
        }  
        public void New(System.Windows.Forms.IWin32Window parentWindow)  
        {  
        }  
        public void Delete(System.Windows.Forms.IWin32Window parentWindow)  
        {  
        }  
        public bool Edit(System.Windows.Forms.IWin32Window parentWindow, Variables vars, Connections cons)  
        {  
            // Create and display the form for the user interface.  
            SampleComponentUIForm componentEditor = new SampleComponentUIForm(cons, vars, md);  
  
            DialogResult result  = componentEditor.ShowDialog(parentWindow);  
  
            if (result == DialogResult.OK)  
                return true;  
  
            return false;  
        }  
        public void Initialize(IDTSComponentMetaData100 dtsComponentMetadata, IServiceProvider serviceProvider)  
        {  
            // Store the component metadata.  
            this.md = dtsComponentMetadata;  
        }  
    }  
}  
```  
  
```vb  
Imports System   
Imports System.Windows.Forms   
Imports Microsoft.SqlServer.Dts.Runtime   
Imports Microsoft.SqlServer.Dts.Pipeline.Design   
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper   
  
Namespace Microsoft.Samples.SqlServer.Dts   
  
 Public Class SampleComponentUI   
 Implements IDtsComponentUI   
   Private md As IDTSComponentMetaData100   
   Private sp As IServiceProvider   
  
   Public Sub Help(ByVal parentWindow As System.Windows.Forms.IWin32Window)   
   End Sub   
  
   Public Sub New(ByVal parentWindow As System.Windows.Forms.IWin32Window)   
   End Sub   
  
   Public Sub Delete(ByVal parentWindow As System.Windows.Forms.IWin32Window)   
   End Sub   
  
   Public Function Edit(ByVal parentWindow As System.Windows.Forms.IWin32Window, ByVal vars As Variables, ByVal cons As Connections) As Boolean   
     ' Create and display the form for the user interface.  
     Dim componentEditor As SampleComponentUIForm = New SampleComponentUIForm(cons, vars, md)   
     Dim result As DialogResult = componentEditor.ShowDialog(parentWindow)   
     If result = DialogResult.OK Then   
       Return True   
     End If   
     Return False   
   End Function   
  
   Public Sub Initialize(ByVal dtsComponentMetadata As IDTSComponentMetaData100, ByVal serviceProvider As IServiceProvider)   
     Me.md = dtsComponentMetadata   
   End Sub   
 End Class   
  
End Namespace  
```  
  
### <a name="custom-editor"></a>カスタム エディター  
 次のコードは、<xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Edit%2A> メソッドを呼び出すと表示される Windows フォームの実装を示しています。  
  
```csharp  
using System;  
using System.Drawing;  
using System.Collections;  
using System.ComponentModel;  
using System.Windows.Forms;  
using System.Data;  
  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    public partial class SampleComponentUIForm : System.Windows.Forms.Form  
    {  
        private Connections connections;  
        private Variables variables;  
        private IDTSComponentMetaData100 metaData;  
        private CManagedComponentWrapper designTimeInstance;  
        private System.ComponentModel.IContainer components = null;  
  
        public SampleComponentUIForm( Connections cons, Variables vars, IDTSComponentMetaData100 md)  
        {  
            variables = vars;  
            connections = cons;  
            metaData = md;  
        }  
  
        private void btnOk_Click(object sender, System.EventArgs e)  
        {  
            if (designTimeInstance == null)  
                designTimeInstance = metaData.Instantiate();  
  
            designTimeInstance.SetComponentProperty( "CustomProperty", txtCustomPropertyValue.Text);  
  
            this.Close();  
        }  
  
        private void btnCancel_Click(object sender, System.EventArgs e)  
        {  
            this.Close();  
        }  
    }  
}  
```  
  
```vb  
Imports System   
Imports System.Drawing   
Imports System.Collections   
Imports System.ComponentModel   
Imports System.Windows.Forms   
Imports System.Data   
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper   
Imports Microsoft.SqlServer.Dts.Runtime   
  
Namespace Microsoft.Samples.SqlServer.Dts   
  
 Public Partial Class SampleComponentUIForm   
  Inherits System.Windows.Forms.Form   
   Private connections As Connections   
   Private variables As Variables   
   Private metaData As IDTSComponentMetaData100   
   Private designTimeInstance As CManagedComponentWrapper   
   Private components As System.ComponentModel.IContainer = Nothing   
  
   Public Sub New(ByVal cons As Connections, ByVal vars As Variables, ByVal md As IDTSComponentMetaData100)   
     variables = vars   
     connections = cons   
     metaData = md   
   End Sub   
  
   Private Sub btnOk_Click(ByVal sender As Object, ByVal e As System.EventArgs)   
     If designTimeInstance Is Nothing Then   
       designTimeInstance = metaData.Instantiate   
     End If   
     designTimeInstance.SetComponentProperty("CustomProperty", txtCustomPropertyValue.Text)   
     Me.Close   
   End Sub   
  
   Private Sub btnCancel_Click(ByVal sender As Object, ByVal e As System.EventArgs)   
     Me.Close   
   End Sub   
 End Class   
  
End Namespace  
```  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>関連項目  
 [カスタム データ フロー コンポーネントの作成](creating-a-custom-data-flow-component.md)  
  
  
