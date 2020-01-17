---
title: カスタム データ フロー コンポーネントの作成 | Microsoft Docs
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
- design-time component interface [Integration Services]
- custom data flow components [Integration Services], about data flow components
- custom data flow components [Integration Services]
- data flow components [Integration Services]
- data flow components [Integration Services], developing
ms.assetid: 9d96bcf5-eba8-44bd-b113-ed51ad0d0521
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1703d70b7760cad2198b3565ce3fc47d44cac409
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768943"
---
# <a name="creating-a-custom-data-flow-component"></a>カスタム データ フロー コンポーネントの作成
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のデータ フロー タスクでは、開発者が [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] およびマネージド コードを使用してカスタム データ フロー コンポーネント (変換元、変換、および変換先) を作成するためのオブジェクト モデルが公開されます。  
  
 データ フロー タスクは、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> インターフェイスを含むコンポーネントと、コンポーネント間のデータの移動を定義する <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> オブジェクトのコレクションで構成されています。  
  
> [!NOTE]  
>  カスタム プロバイダーを作成するときに、ProviderDescriptors.xml ファイルをメタデータ列の値で更新する必要があります。  
  
## <a name="design-time-and-run-time"></a>デザイン時および実行時  
 実行前のデータ フロー タスクは、増分的に変更が行われるため、デザイン時の状態にあると言えます。 追加される変更には、コンポーネントの追加または削除、コンポーネントを接続するパス オブジェクトの追加または削除、およびコンポーネントのメタデータに対する変更などが含まれます。 メタデータの変更が発生すると、コンポーネントはその変更を監視して対処できます。 たとえば、コンポーネントは特定の変更を禁止したり、ある変更に応じてさらに変更を加えたりすることができます。 デザイン時に、設計者はデザイン時インターフェイス <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> を介して、コンポーネントとやり取りします。  
  
 データ フロー タスクは、実行時に、コンポーネントの順序の確認、実行プランの準備、および作業プランを実行するワーカー スレッドのプールの管理を行います。 各ワーカー スレッドはデータ フロー タスク内の一部の処理を実行しますが、ワーカー スレッドの主なタスクは、実行時インターフェイス <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100> を介してコンポーネントのメソッドを呼び出すことです。  
  
## <a name="creating-a-component"></a>コンポーネントの作成  
 データ フロー コンポーネントを作成するには、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 基本クラスからクラスを派生し、<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> クラスを適用して、基本クラスの適切なメソッドをオーバーライドします。 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> には <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> および <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100> インターフェイスが実装され、それらのメソッドが公開されているので、ユーザーのコンポーネント内でオーバーライドできます。  
  
 コンポーネントで使用するオブジェクトによっては、次のアセンブリの一部またはすべてに対する参照がプロジェクトに必要です。  
  
|機能|参照するアセンブリ|インポートする名前空間|  
|-------------|---------------------------|-------------------------|  
|データ フロー|Microsoft.SqlServer.PipelineHost|<xref:Microsoft.SqlServer.Dts.Pipeline>|  
|データ フロー ラッパー|Microsoft.SqlServer.DTSPipelineWrap|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>|  
|ランタイム|Microsoft.SQLServer.ManagedDTS|<xref:Microsoft.SqlServer.Dts.Runtime>|  
|ランタイム ラッパー|Microsoft.SqlServer.DTSRuntimeWrap|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper>|  
  
 次のコード例では、基本クラスから派生し、<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> を適用する簡単なコンポーネントを示します。 DTSPipelineWrap アセンブリへの参照を追加する必要があります。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsPipelineComponent(DisplayName = "SampleComponent", ComponentType = ComponentType.Transform )]  
    public class BasicComponent: PipelineComponent  
    {  
        // TODO: Override the base class methods.  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
<DtsPipelineComponent(DisplayName:="SampleComponent", ComponentType:=ComponentType.Transform)> _  
Public Class BasicComponent  
  
    Inherits PipelineComponent  
  
    ' TODO: Override the base class methods.  
  
End Class  
```  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [データ フロー コンポーネント用ユーザー インターフェイスの開発](developing-a-user-interface-for-a-data-flow-component.md)  
  
  
