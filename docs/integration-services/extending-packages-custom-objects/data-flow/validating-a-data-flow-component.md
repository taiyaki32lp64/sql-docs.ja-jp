---
title: データ フロー コンポーネントの検証 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ReinitializeMetaData method
- Validate method
- component validation [Integration Services]
- custom data flow components [Integration Services], validating
- validation [Integration Services], components
- data flow components [Integration Services], validating
- validation [Integration Services]
ms.assetid: 1a7d5925-b387-4e31-af7f-c7f3c5151040
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5ad9f44e88f92242e516001457d15ba1d93ad9ce
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71287383"
---
# <a name="validating-a-data-flow-component"></a>データ フロー コンポーネントの検証

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  基本クラス <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> の <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> メソッドを使用すると、正しく構成されていないコンポーネントが実行されることを防止できます。 このメソッドを使用すると、コンポーネントが想定どおりの数の入出力オブジェクトを持ち、カスタム プロパティの値が許容範囲内で、接続が必要な場合はそれが指定されていることを検証できます。 また、入出力コレクションの各列のデータ型が正しいこと、各列の <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSUsageType> がコンポーネント用に正しく設定されていることも検証できます。 この基本クラスを実装すると、コンポーネントの入力列コレクションをチェックし、コレクションの各列が上流コンポーネントの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputCollection100> にある列を参照していることを確認できるため、検証プロセスの作業に役立ちます。  
  
## <a name="validate-method"></a>Validate メソッド  
 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> メソッドは、[!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでコンポーネントが編集されるたびに、繰り返し呼び出されます。 コンポーネントのデザイナーやユーザーに対するフィードバックは、列挙型 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus> の戻り値や、警告、エラーの発生によって通知できます。 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus> 列挙に含まれる値のうち 3 つはさまざまな段階での検証失敗を示します。4 番目の <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_ISVALID> という値は、コンポーネントが正しく構成されていて、いつでも実行可能であることを示します。  
  
 値 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_NEEDSNEWMETADATA> は、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> にエラーがあるが、コンポーネントはエラーを修復できることを示します。 コンポーネントがメタデータのエラーを修復できる場合でも、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> メソッドのエラーは修復せず、また、検証中に <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> を変更することも避けてください。 代わりに、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> メソッドが <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_NEEDSNEWMETADATA> のみを返し、コンポーネントは <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> メソッドの呼び出し中にエラーを修復するようにします。詳細についてはこのセクションの後半で説明します。  
  
 値 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_ISBROKEN> は、コンポーネントにエラーがあるが、デザイナーで編集することにより修復できることを示します。 このエラーが発生するのは、通常、カスタム プロパティまたは必要な接続が指定されていない、または正しく設定されていないためです。  
  
 値 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_ISCORRUPT> は、パッケージ XML の編集、またはオブジェクト モデルの使用により、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> プロパティが直接修正された場合にのみ発生するエラーがコンポーネントで見つかったことを示します。 たとえば、コンポーネントに入力が 1 つしか追加されていないのに、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> に複数の入力が存在することが検証で確認された場合、この種のエラーが発生します。 この戻り値を生成するエラーを修正するには、 **[詳細エディター]** ダイアログ ボックスで **[リセット]** をクリックして、コンポーネントをリセットするしか方法がありません。  
  
 戻り値としてエラーを返す以外に、検証中に警告やエラーを通知し、コンポーネントにフィードバックを送信する方法もあります。 このメカニズムは、<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireWarning%2A> メソッドおよび <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireError%2A> メソッドによって提供されます。 これらのメソッドが呼び出されると、[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] の **[エラー一覧]** ウィンドウにイベントが表示されます。 コンポーネント開発者は、発生したエラーに関するフィードバックや、必要に応じて、修正方法を直接ユーザーに通知することもできます。  
  
 次のコード例は、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> メソッドをオーバーライドして実装する方法を示しています。  
  
```csharp  
public override DTSValidationStatus Validate()  
{  
    bool pbCancel = false;  
  
    // Validate that there is one input.  
    if (ComponentMetaData.InputCollection.Count != 1)  
    {  
    ComponentMetaData.FireError(0, ComponentMetaData.Name, "Incorrect number of inputs.", "", 0, out pbCancel);  
    return DTSValidationStatus.VS_ISCORRUPT;  
    }  
  
    // Validate that the UserName custom property is set.  
    if (ComponentMetaData.CustomPropertyCollection["UserName"].Value == null || ((string)ComponentMetaData.CustomPropertyCollection["UserName"].Value).Length == 0)  
    {  
        ComponentMetaData.FireError(0, ComponentMetaData.Name, "The UserName property must be set.", "", 0, out pbCancel);  
        return DTSValidationStatus.VS_ISBROKEN;  
    }  
  
    // Validate that there is one output.  
    if (ComponentMetaData.OutputCollection.Count != 1)  
    {  
        ComponentMetaData.FireError(0, ComponentMetaData.Name, "Incorrect number of outputs.", "", 0, out pbCancel);  
        return DTSValidationStatus.VS_ISCORRUPT;  
    }  
  
    // Let the base class verify that the input column reflects the output   
    // of the upstream component.  
    return base.Validate();  
}  
```  
  
```vb  
Public  Overrides Function Validate() As DTSValidationStatus   
  
 Dim pbCancel As Boolean = False  
  
 ' Validate that there is one input.  
 If Not (ComponentMetaData.InputCollection.Count = 1) Then   
   ComponentMetaData.FireError(0, ComponentMetaData.Name, "Incorrect number of inputs.", "", 0, pbCancel)   
   Return DTSValidationStatus.VS_ISCORRUPT   
 End If   
  
 ' Validate that the UserName custom property is set.  
 If ComponentMetaData.CustomPropertyCollection("UserName").Value Is Nothing OrElse CType(ComponentMetaData.CustomPropertyCollection("UserName").Value, String).Length = 0 Then   
   ComponentMetaData.FireError(0, ComponentMetaData.Name, "The UserName property must be set.", "", 0, pbCancel)   
   Return DTSValidationStatus.VS_ISBROKEN   
 End If   
  
 ' Validate that there is one output.  
 If Not (ComponentMetaData.OutputCollection.Count = 1) Then   
   ComponentMetaData.FireError(0, ComponentMetaData.Name, "Incorrect number of outputs.", "", 0, pbCancel)   
   Return DTSValidationStatus.VS_ISCORRUPT   
 End If   
  
 ' Let the base class verify that the input column reflects the output   
 ' of the upstream component.  
  
 Return MyBase.Validate   
  
End Function  
```  
  
## <a name="reinitializemetadata-method"></a>ReinitializeMetaData メソッド  
 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> メソッドは、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_NEEDSNEWMETADATA> メソッドの戻り値が <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> のコンポーネントを編集する場合に、常に [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーによって呼び出されます。 コンポーネントには、検証中に見つかった問題を検出して修正するコードを含める必要があります。  
  
 次の例は、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> メソッドで、検証中に問題を検出して修正するコンポーネントを示しています。  
  
```csharp  
private bool areInputColumnsValid = true;  
public override DTSValidationStatus Validate()  
{  
    IDTSInput100 input = ComponentMetaData.InputCollection[0];  
    IDTSVirtualInput100 vInput = input.GetVirtualInput();  
  
    bool Cancel = false;  
    foreach (IDTSInputColumn100 column in input.InputColumnCollection)  
    {  
        try  
        {  
            IDTSVirtualInputColumn100 vColumn = vInput.VirtualInputColumnCollection.GetVirtualInputColumnByLineageID(column.LineageID);  
        }  
        catch  
        {  
            ComponentMetaData.FireError(0, ComponentMetaData.Name, "The input column " + column.IdentificationString + " does not match a column in the upstream component.", "", 0, out Cancel);  
            areInputColumnsValid = false;  
            return DTSValidationStatus.VS_NEEDSNEWMETADATA;  
        }  
    }  
  
    return DTSValidationStatus.VS_ISVALID;  
}  
public override void ReinitializeMetaData()  
{  
    if (!areInputColumnsValid)  
    {  
        IDTSInput100 input = ComponentMetaData.InputCollection[0];  
        IDTSVirtualInput100 vInput = input.GetVirtualInput();  
  
        foreach (IDTSInputColumn100 column in input.InputColumnCollection)  
        {  
            IDTSVirtualInputColumn100 vColumn = vInput.VirtualInputColumnCollection.GetVirtualInputColumnByLineageID(column.LineageID);  
  
            if (vColumn == null)  
                input.InputColumnCollection.RemoveObjectByID(column.ID);  
        }  
        areInputColumnsValid = true;  
    }  
}  
```  
  
```vb  
Private areInputColumnsValid As Boolean = True   
  
Public  Overrides Function Validate() As DTSValidationStatus   
 Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)   
 Dim vInput As IDTSVirtualInput100 = input.GetVirtualInput   
 Dim Cancel As Boolean = False   
 For Each column As IDTSInputColumn100 In input.InputColumnCollection   
   Try   
     Dim vColumn As IDTSVirtualInputColumn100 = vInput.VirtualInputColumnCollection.GetVirtualInputColumnByLineageID(column.LineageID)   
   Catch   
     ComponentMetaData.FireError(0, ComponentMetaData.Name, "The input column " + column.IdentificationString + " does not match a column in the upstream component.", "", 0, Cancel)   
     areInputColumnsValid = False   
     Return DTSValidationStatus.VS_NEEDSNEWMETADATA   
   End Try   
 Next   
 Return DTSValidationStatus.VS_ISVALID   
End Function   
  
Public  Overrides Sub ReinitializeMetaData()   
 If Not areInputColumnsValid Then   
   Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)   
   Dim vInput As IDTSVirtualInput100 = input.GetVirtualInput   
   For Each column As IDTSInputColumn100 In input.InputColumnCollection   
     Dim vColumn As IDTSVirtualInputColumn100 = vInput.VirtualInputColumnCollection.GetVirtualInputColumnByLineageID(column.LineageID)   
     If vColumn Is Nothing Then   
       input.InputColumnCollection.RemoveObjectByID(column.ID)   
     End If   
   Next   
   areInputColumnsValid = True   
 End If   
End Sub  
```  
  
