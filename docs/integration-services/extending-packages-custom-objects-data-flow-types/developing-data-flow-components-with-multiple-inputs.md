---
title: 複数の入力を持つデータ フロー コンポーネントの開発 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 3c7b50e8-2aa6-4f6a-8db4-e8293bc21027
author: chugugrace
ms.author: chugu
ms.openlocfilehash: df06f7dad35edcbdd299794a7724b3e52e7974f0
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71287713"
---
# <a name="developing-data-flow-components-with-multiple-inputs"></a>複数の入力を持つデータ フロー コンポーネントの開発

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  複数の入力によってデータが不均一なレートで生成される場合に、複数の入力があるデータ フローコンポーネントによって過度にメモリが消費されることがあります。 複数の入力をサポートするカスタム データ フロー コンポーネントを開発するときは、Microsoft.SqlServer.Dts.Pipeline 名前空間の次のメンバーを使用してこのメモリの負荷を管理できます。  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> プロパティ。 カスタム データ フロー コンポーネントに必要なコードを実装して不均一なレートのデータ フローを管理する場合は、このプロパティの値を **true** に設定します。  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> メソッド。 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> プロパティを **true** に設定する場合は、このメソッドを実装する必要があります。 実装しない場合、データ フロー エンジンは実行時に例外を発生させます。  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> メソッド。 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> プロパティを **true** に設定し、カスタム コンポーネントが複数の入力をサポートしている場合は、このメソッドも実装する必要があります。 実装しない場合、ユーザーが複数の入力をアタッチすると、データ フロー エンジンは実行時に例外を発生させます。  
  
 また、これらのメンバーを使用すると、マージ変換およびマージ結合変換用にマイクロソフトが開発したような、メモリ負荷のためのソリューションを開発できます。  
  
## <a name="setting-the-supportsbackpressure-property"></a>SupportsBackPressure プロパティの設定  
 複数の入力をサポートするカスタム データ フロー コンポーネントでより効率的なメモリ管理を実装するための最初の手順は、<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> で <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> プロパティの値を **true** に設定することです。 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> の値が **true** の場合、データ フロー エンジンは <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> メソッドを呼び出し、複数の入力があるときは、実行時に <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> メソッドも呼び出します。  
  
### <a name="example"></a>例  
 次のコード例では、<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> を実装して、<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> の値を **true** に設定します。  
  
```csharp  
[DtsPipelineComponent(ComponentType = ComponentType.Transform,  
        DisplayName = "Shuffler",  
        Description = "Shuffle the rows from input.",  
        SupportsBackPressure = true,  
        LocalizationType = typeof(Localized),  
        IconResource = "Microsoft.Samples.SqlServer.Dts.MIBPComponent.ico")  
]  
public class Shuffler : Microsoft.SqlServer.Dts.Pipeline.PipelineComponent  
        {  
          ...  
        }  
```  
  
## <a name="implementing-the-isinputready-method"></a>IsInputReady メソッドの実装  
 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> オブジェクトの <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> プロパティの値を **true** に設定する場合は、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> メソッドも実装する必要があります。  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> メソッドの実装では、基本クラスで実装を呼び出す必要はありません。 基本クラスでのこのメソッドの既定の実装では、**NotImplementedException** を発生させるだけです。  
  
 このメソッドを実装し、コンポーネントの各入力に対して Boolean 型の *canProcess* 配列で要素の状態を設定します (入力は *inputIDs* 配列内の ID 値によって識別されます)。入力に対して *canProcess* 配列の要素の値を **true** に設定すると、データ フロー エンジンは、コンポーネントの <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> メソッドを呼び出し、指定した入力に対して追加データを提供します。  
  
 アップストリーム データを追加で使用できますが、少なくとも 1 つの入力に対して *canProcess* 配列要素の値を常に **true** に設定する必要があります。設定しない場合は、処理が停止します。  
  
 データ フロー エンジンは、データの各バッファーを送信する前に <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> メソッドを呼び出して、追加データの受信を待機している入力を判断します。 入力がブロックされていることが戻り値によって示された場合、データ フロー エンジンは、バッファーをコンポーネントに送信する代わりに、入力データの追加バッファーを一時的にキャッシュします。  
  
> [!NOTE]  
>  独自に記述するコード内で、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> または <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> メソッドは呼び出しません。 データ フロー エンジンはコンポーネントを実行するとき、これらのメソッドやオーバーライドする **PipelineComponent** クラスのその他のメソッドを呼び出します。  
  
### <a name="example"></a>例  
 次の例では、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> の実装により、以下の条件に該当する場合に入力が追加のデータを待っていることを示します。  
  
-   入力に対する追加の上流データがある (`!inputEOR`)。  
  
-   コンポーネントが、受信済みのバッファーで入力に対して処理できるデータを現在持っていない (`inputBuffers[inputIndex].CurrentRow() == null`)。  
  
 入力が追加のデータを待っている場合、データ フロー コンポーネントは、この入力に対応する *canProcess* 配列の要素の値を **true** に設定することによってこの状態を示します。  
  
 逆に、コンポーネントが入力に対して処理できるデータを持っている場合、この例では入力の処理を中断します。 この例では、入力に対応する *canProcess* 配列の要素の値を **false** に設定することによってこれを行います。  
  
```csharp  
public override void IsInputReady(int[] inputIDs, ref bool[] canProcess)  
{  
    for (int i = 0; i < inputIDs.Length; i++)  
    {  
        int inputIndex = ComponentMetaData.InputCollection.GetObjectIndexByID(inputIDs[i]);  
  
        canProcess[i] = (inputBuffers[inputIndex].CurrentRow() == null)  
            && !inputEOR[inputIndex];  
    }  
}  
```  
  
 前の例は、Boolean 型の `inputEOR` 配列を使用して、各入力で追加のアップストリーム データを使用できるかどうかを示します。 配列名の `EOR` は "行セットの末尾 (end of rowset)" を示し、データ フロー バッファーの <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> プロパティを参照します。 ここに含まれていない例の部分では、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> メソッドを使用して、受信するデータの各バッファーに対して <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> プロパティの値を確認します。 値 **true** によって、入力でこれ以上のアップストリーム データを利用できないことが示された場合、その入力の `inputEOR` 配列要素の値を **true** に設定します。 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> メソッドのこの例では、`inputEOR` 配列要素の値によって入力に使用できるアップストリーム データがないことが示された場合、*canProcess* 配列の入力に対応する要素の値を **false** に設定します。  
  
## <a name="implementing-the-getdependentinputs-method"></a>GetDependentInputs メソッドの実装  
 カスタム データ フロー コンポーネントが複数の入力をサポートしている場合は、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> メソッドも実装する必要があります。  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> メソッドの実装では、基本クラスで実装を呼び出す必要はありません。 基本クラスでのこのメソッドの既定の実装では、**NotImplementedException** を発生させるだけです。  
  
 データ フロー エンジンは、ユーザーが 3 つ以上の入力をコンポーネントにアタッチする場合に、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> メソッドを呼び出すだけです。 コンポーネントの入力が 2 つしかないときに 1 つの入力がブロックされていることが <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> メソッドによって示される場合 (*canProcess* = **false**)、データ フロー エンジンは、もう一方の入力が追加のデータを待っていることを認識します。 ただし、入力が 2 つより多い場合に、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> メソッドによって 1 つの入力がブロックされていることが示されたときは、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> の追加のコードはどの入力が追加データの受信を待機しているかを示します。  
  
> [!NOTE]  
>  独自に記述するコード内で、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> または <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> メソッドは呼び出しません。 データ フロー エンジンはコンポーネントを実行するとき、これらのメソッドやオーバーライドする **PipelineComponent** クラスのその他のメソッドを呼び出します。  
  
### <a name="example"></a>例  
 ある 1 つの入力がブロックされている場合、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> メソッドの次の実装は、追加データの受信を待機している入力のコレクションを返し、はじめの 1 つの入力はブロッキング状態のままになります。 コンポーネントは、既に受信したバッファー内に、ブロックされている入力以外の入力が処理できるデータが現在ないことをチェックして、ブロックしている入力を特定します (`inputBuffers[i].CurrentRow() == null`)。 次に、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> メソッドは、ブロックしている入力のコレクションを入力 ID のコレクションとして返します。  
  
```csharp  
public override Collection<int> GetDependentInputs(int blockedInputID)  
{  
    Collection<int> currentDependencies = new Collection<int>();  
    for (int i = 0; i < ComponentMetaData.InputCollection.Count; i++)  
    {  
        if (ComponentMetaData.InputCollection[i].ID != blockedInputID  
            && inputBuffers[i].CurrentRow() == null)  
        {  
            currentDependencies.Add(ComponentMetaData.InputCollection[i].ID);  
        }  
    }  
  
    return currentDependencies;  
}  
```  
  
  
