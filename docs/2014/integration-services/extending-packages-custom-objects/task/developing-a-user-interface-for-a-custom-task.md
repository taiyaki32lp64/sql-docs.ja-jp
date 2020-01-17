---
title: カスタム タスク用ユーザー インターフェイスの開発 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom user interfaces [Integration Services]
- IDtsTaskUI interface
- DtsTaskAttribute attribute
- custom tasks [Integration Services], user interface
- custom user interface [Integration Services], custom tasks
- user interface [Integration Services]
- SSIS custom tasks, user interface
ms.assetid: 1e940cd1-c5f8-4527-b678-e89ba5dc398a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6268fe16c31c931dc71ad1a62bd72e08b1ecb537
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768918"
---
# <a name="developing-a-user-interface-for-a-custom-task"></a>カスタム タスク用ユーザー インターフェイスの開発
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のオブジェクト モデルを使用すると、カスタム タスクの開発者は、タスク用のユーザー インターフェイスを容易に作成できます。作成後、このユーザー インターフェイスは [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] に統合して表示することができます。 このユーザー インターフェイスでは、[!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーのユーザーに役に立つ情報を提供でき、カスタム タスクのプロパティや設定を正しく構成するための指針とすることができます。  
  
 タスク用のカスタム ユーザー インターフェイスを開発するには、2 つの重要なクラスを使用します。 次の表は、これらのクラスを示しています。  
  
|クラス|説明|  
|-----------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>|マネージド タスクを識別する属性。この属性のプロパティによってデザイン時の情報を提供し、[!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでのオブジェクトの表示方法と操作方法を制御します。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI>|タスクとカスタム ユーザー インターフェイスを関連付けるためにタスクが使用するインターフェイス。|  
  
 このセクションでは、ユーザー インターフェイスを開発する際の <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 属性および <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI> インターフェイスの役割について説明し、[!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでタスクを作成、統合、配置、デバッグする方法について詳細に説明します。  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーには、タスクのユーザー インターフェイスへの複数のエントリ ポイントがあります。つまり、ショートカット メニューの **[編集]** を選択し、タスクをダブルクリックするか、プロパティ シートの下部にある **[エディターの表示]** リンクをクリックできます。 これらのエントリ ポイントのいずれかにアクセスすると、[!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーはタスク用のユーザー インターフェイスが含まれているアセンブリを探して読み込みます。 タスクのユーザー インターフェイスには、[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] で表示されるプロパティ ダイアログ ボックスを作成する役割があります。  
  
 タスクとそのユーザー インターフェイスは個別のエンティティです。 ローカライズ、配置、メンテナンスなどの作業を容易にするため、タスクとユーザー インターフェイスは個別のアセンブリに実装する必要があります。 タスク DLL は、ユーザー インターフェイスの読み込み、呼び出しを行わず、これには通常、ユーザー インターフェイスに関するいかなる情報も含まれていません。ただし、タスク内でコード化された <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 属性値に含まれる情報は例外です。 タスクとユーザー インターフェイスは、この方法によってのみ関連付けられます。  
  
## <a name="the-dtstask-attribute"></a>DtsTask 属性  
 タスク クラス コードに含まれている <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 属性により、タスクはユーザー インターフェイスと関連付けられます。 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでは、タスクをデザイナーに表示する方法を判別するために、属性のプロパティが使用されます。 これらのプロパティには、表示する名前やアイコン (存在する場合) が含まれます。  
  
 次の表は、<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 属性のプロパティを示しています。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute.DisplayName%2A>|制御フロー ツールボックスに表示するタスク名。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute.Description%2A>|タスクの説明 (<xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute> から継承)。 ツールヒントに表示されるプロパティです。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.IconResource%2A>|[!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーに表示するアイコン。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.RequiredProductLevel%2A>|使用する場合は、<xref:Microsoft.SqlServer.Dts.Runtime.DTSProductLevel> 列挙のいずれかの値に設定します。 たとえば、`RequiredProductLevel = DTSProductLevel.None` のようにします。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.TaskContact%2A>|タスクでテクニカル サポートが必要な場合の連絡先に関する情報。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.TaskType%2A>|タスクに割り当てる型。|  
|Attribute.TypeId|派生クラスに実装した場合、この属性の一意の識別子を取得します。 詳細については、.NET Framework クラス ライブラリの「`Attribute.TypeID` プロパティ」を参照してください。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.UITypeName%2A>|アセンブリのタイプ名。[!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーがアセンブリを読み込むために使用します。 このプロパティは、タスクのユーザー インターフェイス アセンブリを見つけるために使用します。|  
  
 次のコード例は、<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> を示します。この例でわかるように、この属性はクラス定義よりも前にコード化されています。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
namespace Microsoft.SSIS.Samples  
{  
  [DtsTask  
  (  
   DisplayName = "MyTask",  
   IconResource = "MyTask.MyTaskIcon.ico",  
   UITypeName = "My Custom Task," +  
   "Version=1.0.0.0," +  
   "Culture = Neutral," +  
   "PublicKeyToken = 12345abc6789de01",  
   TaskType = "PackageMaintenance",  
   TaskContact = "MyTask; company name; any other information",  
   RequiredProductLevel = DTSProductLevel.None  
   )]  
  public class MyTask : Task  
  {  
    // Your code here.  
  }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
  
<DtsTask(DisplayName:="MyTask", _  
 IconResource:="MyTask.MyTaskIcon.ico", _  
 UITypeName:="My Custom Task," & _  
 "Version=1.0.0.0,Culture=Neutral," & _  
 "PublicKeyToken=12345abc6789de01", _  
 TaskType:="PackageMaintenance", _  
 TaskContact:="MyTask; company name; any other information", _  
 RequiredProductLevel:=DTSProductLevel.None)> _  
Public Class MyTask  
  Inherits Task  
  
  ' Your code here.  
  
End Class 'MyTask  
```  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーはこの属性の <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.UITypeName%2A> プロパティを参照して、グローバル アセンブリ キャッシュ (GAC) からアセンブリを探し、読み込んでデザイナーで使用します。このプロパティには、アセンブリ名、タイプ名、バージョン、カルチャ、および公開キー トークンが含まれています。  
  
 アセンブリが見つかると、[!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーは属性内の他のプロパティを使用し、タスクの名前、アイコン、説明など、タスクに関する追加情報を [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーに表示します。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute.DisplayName%2A>、<xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute.Description%2A>、および <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.IconResource%2A> プロパティは、ユーザーに対してタスクをどのように表示するかを指定します。 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.IconResource%2A> プロパティには、ユーザー インターフェイス アセンブリに埋め込まれたアイコンのリソース ID が含まれます。 デザイナーはこの ID を基にしてアセンブリからアイコン リソースを読み込み、タスクがパッケージに追加されたとき、ツールボックスやデザイナー画面で、タスク名の隣にアイコンを表示します。 タスクがアイコン リソースを提供しない場合、デザイナーはタスク用に既定のアイコンを使用します。  
  
## <a name="the-idtstaskui-interface"></a>IDTSTaskUI インターフェイス  
 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI> インターフェイスでは、[!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーが呼び出し、タスクに関連付けられたユーザー インターフェイスを初期化して表示するための、一連のメソッドやプロパティが定義されます。 タスクのユーザー インターフェイスが起動されると、デザイナーは <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI.Initialize%2A> メソッドを呼び出します。このメソッドは、ユーザーが記述した際にタスク ユーザー インターフェイスに実装されたものです。次に、タスクの <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> コレクション、およびパッケージの <xref:Microsoft.SqlServer.Dts.Runtime.Connections> コレクションを、パラメーターとして渡します。 このコレクションはローカルに保存され、後で <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI.GetView%2A> メソッド内で使用されます。  
  
 デザイナーは <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI.GetView%2A> メソッドを呼び出して、[!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーで表示するウィンドウを要求します。 タスクは、タスクのユーザー インターフェイスを含むウィンドウのインスタンスを作成し、ユーザー インターフェイスをデザイナーに返して表示させます。 通常、オーバーロードされたコンストラクターを介して、<xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> オブジェクトおよび <xref:Microsoft.SqlServer.Dts.Runtime.Connections> オブジェクトがウィンドウに渡されるため、これを使用してタスクを構成できます。  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーはタスク ユーザー インターフェイスの <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI.GetView%2A> メソッドを呼び出して、タスク用のユーザー インターフェイスを表示します。 タスク ユーザー インターフェイスはこのメソッドから Windows フォームを返し、[!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーは、このフォームをモーダル ダイアログ ボックスとして表示します。 フォームを閉じると、[!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーはフォームの `DialogResult` プロパティの値を確認し、タスクが変更されたかどうか、およびその変更を保存する必要があるかどうかを判断します。 `DialogResult` プロパティの値が `OK` の場合、[!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーはタスクの持続メソッドを呼び出して変更を保存します。それ以外の場合は、変更は破棄されます。  
  
 次のコード例は、<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI> インターフェイスを実装します。ここでは、SampleTaskForm という名前の Windows フォーム クラスが存在するものと想定しています。  
  
```csharp  
using System;  
using System.Windows.Forms;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Runtime.Design;  
  
namespace Sample  
{  
   public class HelloWorldTaskUI : IDtsTaskUI  
   {  
      TaskHost   taskHost;  
      Connections connections;  
      public void Initialize(TaskHost taskHost, IServiceProvider serviceProvider)  
      {  
         this.taskHost = taskHost;  
         IDtsConnectionService cs = serviceProvider.GetService  
         ( typeof( IDtsConnectionService ) ) as   IDtsConnectionService;   
         this.connections = cs.GetConnections();  
      }  
      public ContainerControl GetView()  
      {  
        return new HelloWorldTaskForm(this.taskHost, this.connections);  
      }  
     public void Delete(IWin32Window parentWindow)  
     {  
     }  
     public void New(IWin32Window parentWindow)  
     {  
     }  
   }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Runtime.Design  
Imports System.Windows.Forms  
  
Public Class HelloWorldTaskUI  
  Implements IDtsTaskUI  
  
  Dim taskHost As TaskHost  
  Dim connections As Connections  
  
  Public Sub Initialize(ByVal taskHost As TaskHost, ByVal serviceProvider As IServiceProvider) _  
    Implements IDtsTaskUI.Initialize  
  
    Dim cs As IDtsConnectionService  
  
    Me.taskHost = taskHost  
    cs = DirectCast(serviceProvider.GetService(GetType(IDtsConnectionService)), IDtsConnectionService)  
    Me.connections = cs.GetConnections()  
  
  End Sub  
  
  Public Function GetView() As ContainerControl _  
    Implements IDtsTaskUI.GetView  
  
    Return New HelloWorldTaskForm(Me.taskHost, Me.connections)  
  
  End Function  
  
  Public Sub Delete(ByVal parentWindow As IWin32Window) _  
    Implements IDtsTaskUI.Delete  
  
  End Sub  
  
  Public Sub [New](ByVal parentWindow As IWin32Window) _  
    Implements IDtsTaskUI.[New]  
  
  End Sub  
  
End Class  
```  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [カスタム タスクの作成](creating-a-custom-task.md)   
 [カスタム タスクのコーディング](coding-a-custom-task.md)   
 [カスタム タスク用ユーザー インターフェイスの開発](developing-a-user-interface-for-a-custom-task.md)  
  
  
