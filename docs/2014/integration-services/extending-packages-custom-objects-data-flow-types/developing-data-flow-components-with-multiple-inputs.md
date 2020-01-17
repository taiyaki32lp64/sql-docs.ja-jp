---
title: 複数の入力を持つデータ フロー コンポーネントの開発 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 3c7b50e8-2aa6-4f6a-8db4-e8293bc21027
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 74bcf1549cdd97752c805f1c6a9cc774ef1a9e52
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62896032"
---
# <a name="developing-data-flow-components-with-multiple-inputs"></a>複数の入力を持つデータ フロー コンポーネントの開発
  複数の入力によってデータが不均一なレートで生成される場合に、複数の入力があるデータ フローコンポーネントによって過度にメモリが消費されることがあります。 複数の入力をサポートするカスタム データ フロー コンポーネントを開発するときは、Microsoft.SqlServer.Dts.Pipeline 名前空間の次のメンバーを使用してこのメモリの負荷を管理できます。  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> プロパティ。 カスタム データ フロー コンポーネントに必要なコードを実装して不均一なレートのデータ フローを管理する場合は、このプロパティの値を `true` に設定します。  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> メソッド。 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> プロパティを `true` に設定する場合は、このメソッドを実装する必要があります。 実装しない場合、データ フロー エンジンは実行時に例外を発生させます。  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> メソッド。 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> プロパティを `true` に設定し、カスタム コンポーネントが複数の入力をサポートしている場合は、このメソッドも実装する必要があります。 実装しない場合、ユーザーが複数の入力をアタッチすると、データ フロー エンジンは実行時に例外を発生させます。  
  
 また、これらのメンバーを使用すると、マージ変換およびマージ結合変換用にマイクロソフトが開発したような、メモリ負荷のためのソリューションを開発できます。  
  
## <a name="setting-the-supportsbackpressure-property"></a>SupportsBackPressure プロパティの設定  
 複数の入力をサポートするカスタム データ フロー コンポーネントでより効率的なメモリ管理を実装するための最初の手順は、<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> で <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> プロパティの値を `true` に設定することです。 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> の値が `true` の場合、データ フロー エンジンは <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> メソッドを呼び出し、複数の入力があるときは、実行時に <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> メソッドも呼び出します。  
  
### <a name="example"></a>例  
 次のコード例では、<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> を実装して、<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> の値を `true` に設定します。  
  
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
 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> オブジェクトの <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> プロパティの値を `true` に設定する場合は、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> メソッドも実装する必要があります。  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> メソッドの実装では、基本クラスで実装を呼び出す必要はありません。 基本クラスでのこのメソッドの既定の実装では、`NotImplementedException` を発生させるだけです。  
  
 このメソッドを実装し、コンポーネントの各入力に対して Boolean 型の *canProcess* 配列で要素の状態を設定します (入力は *inputIDs* 配列内の ID 値によって識別されます)。内の要素の値を設定すると、 *canProcess*配列`true`入力に対して、データ フロー エンジンによってコンポーネントの<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>メソッドと、指定した入力に対してより多くのデータを提供します。  
  
 アップ ストリーム データが使用中の値、 *canProcess*の少なくとも 1 つの入力配列の要素は常にあります`true`、処理が停止します。  
  
 データ フロー エンジンは、データの各バッファーを送信する前に <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> メソッドを呼び出して、追加データの受信を待機している入力を判断します。 入力がブロックされていることが戻り値によって示された場合、データ フロー エンジンは、バッファーをコンポーネントに送信する代わりに、入力データの追加バッファーを一時的にキャッシュします。  
  
> [!NOTE]  
>  独自に記述するコード内で、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> または <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> メソッドは呼び出しません。 データ フロー エンジンはコンポーネントを実行するとき、これらのメソッドやオーバーライドする `PipelineComponent` クラスのその他のメソッドを呼び出します。  
  
### <a name="example"></a>例  
 次の例では、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> の実装により、以下の条件に該当する場合に入力が追加のデータを待っていることを示します。  
  
-   入力に対する追加の上流データがある (`!inputEOR`)。  
  
-   コンポーネントが、受信済みのバッファーで入力に対して処理できるデータを現在持っていない (`inputBuffers[inputIndex].CurrentRow() == null`)。  
  
 入力がより多くのデータを受信するを待機している場合、データ フロー コンポーネントを示しますこの設定することによって`true`内の要素の値、 *canProcess*入力に対応している配列。  
  
 逆に、コンポーネントが入力に対して処理できるデータを持っている場合、この例では入力の処理を中断します。 この例では設定することによってこの`false`内の要素の値、 *canProcess*入力に対応している配列。  
  
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
  
 前の例は、Boolean 型の `inputEOR` 配列を使用して、各入力で追加のアップストリーム データを使用できるかどうかを示します。 配列名の `EOR` は "行セットの末尾 (end of rowset)" を示し、データ フロー バッファーの <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> プロパティを参照します。 ここに含まれていない例の部分では、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> メソッドを使用して、受信するデータの各バッファーに対して <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> プロパティの値を確認します。 値 `true` によって、入力でこれ以上のアップストリーム データを利用できないことが示された場合、その入力の `inputEOR` 配列要素の値を `true` に設定します。 この例の<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>メソッドの対応する要素の値を設定、 *canProcess*配列を`false`入力の場合の値、`inputEOR`配列の要素ことを示していないアップ ストリームデータの入力を利用できません。  
  
## <a name="implementing-the-getdependentinputs-method"></a>GetDependentInputs メソッドの実装  
 カスタム データ フロー コンポーネントが複数の入力をサポートしている場合は、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> メソッドも実装する必要があります。  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> メソッドの実装では、基本クラスで実装を呼び出す必要はありません。 基本クラスでのこのメソッドの既定の実装では、`NotImplementedException` を発生させるだけです。  
  
 データ フロー エンジンは、ユーザーが 3 つ以上の入力をコンポーネントにアタッチする場合に、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> メソッドを呼び出すだけです。 コンポーネントの 2 つの入力であるときに、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>メソッドでは、1 つの入力がブロックされていることを示します (*canProcess* = `false`)、データ フロー エンジンは、他の入力データの受信を待機していることを認識します。 ただし、入力が 2 つより多い場合に、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> メソッドによって 1 つの入力がブロックされていることが示されたときは、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> の追加のコードはどの入力が追加データの受信を待機しているかを示します。  
  
> [!NOTE]  
>  独自に記述するコード内で、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> または <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> メソッドは呼び出しません。 データ フロー エンジンはコンポーネントを実行するとき、これらのメソッドやオーバーライドする `PipelineComponent` クラスのその他のメソッドを呼び出します。  
  
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
  
  
