---
title: 実行プランおよびバッファーの割り当て | Microsoft Docs
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
- custom data flow components [Integration Services], buffer allocations
- custom data flow components [Integration Services], execution plans
- buffer allocations [Integration Services]
- data flow components [Integration Services], buffer allocations
- data flow components [Integration Services], execution plans
- execution plans [Integration Services]
ms.assetid: 679d9ff0-641e-47c3-abb8-d1a7dcb279dd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: dba5ae3bf996f469f18a9802dd8cc8232a5bc885
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297239"
---
# <a name="execution-plan-and-buffer-allocation"></a>実行プランおよびバッファーの割り当て

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  実行前に、データ フロー タスクはそのコンポーネントを確認し、コンポーネントの各処理手順に応じて、実行プランを生成します。 このセクションでは、実行プラン、プランの表示方法、および実行プランに基づいて入力および出力バッファーを割り当てる方法に関する詳細について説明します。  
  
## <a name="understanding-the-execution-plan"></a>実行プランについて  
 実行プランには、ソース スレッドと作業スレッドが含まれています。各スレッドには作業一覧が含まれており、ソース スレッドには出力作業一覧が、作業スレッドには入力と出力の作業一覧が指定されています。 実行プラン内のソース スレッドは、データ フロー内の変換元コンポーネントを表し、実行プラン内では *SourceThreadn* によって識別されます。ここで *n* は、0 から始まるソース スレッドの番号を示します。  
  
 各ソース スレッドはバッファーを作成してリスナーを設定し、変換元コンポーネントで <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> メソッドを呼び出します。 ここで、実行が開始されてデータが生成され、データ フロー タスクによって用意された出力バッファーに、変換元コンポーネントが行を追加し始めます。 ソース スレッドが実行されると、作業スレッド間で作業の負荷が分散されます。  
  
 作業スレッドは、入力および出力の両方の作業一覧を含む場合があり、実行プラン内では *WorkThreadn* によって識別されます。ここで *n* は、0 から始まる作業スレッドの番号を示します。 非同期出力型のコンポーネントがグラフに含まれている場合、このスレッドには出力作業一覧が含まれます。  
  
 次のサンプル実行プランは、変換元コンポーネントが非同期出力型の変換に連結され、その変換が変換先コンポーネントに連結されているデータ フローを示しています。 この例では、変換コンポーネントに非同期出力が含まれているので、WorkThread0 には出力作業一覧が含まれます。  
  
```  
SourceThread0   
    Influences: 72 158   
    Output Work List   
        CreatePrimeBuffer of type 1 for output id 10   
        SetBufferListener: "WorkThread0" for input ID 73   
        CallPrimeOutput on component "OLE DB Source" (1)   
    End Output Work List   
    This thread drives 0 distributors   
End SourceThread0   
WorkThread0   
    Influences: 72 158   
    Input Work list, input ID 73   
        CallProcessInput on input ID 73 on component "Sort" (72) for view type 2   
    End Input Work list for input 73   
    Output Work List   
        CreatePrimeBuffer of type 3 for output id 74   
        SetBufferListener: "WorkThread1" for input ID 171with internal handoff   
        CallPrimeOutput on component "Sort" (72)   
    End Output Work List   
    This thread drives 0 distributors   
End WorkThread0   
WorkThread1   
    Influences: 158   
    Input Work list, input ID 171  
        CallProcessInput on input ID 171 on component "OLE DB Destination" (158) for view type 4  
    End Input Work list for input 171   
    Output Work List   
    End Output Work List   
    This thread drives 0 distributors   
End WorkThread1  
```  
  
> [!NOTE]  
>  実行プランはパッケージが実行されるたびに生成され、ログ プロバイダーをパッケージに追加し、ログ記録を有効にして **PipelineExecutionPlan** イベントを選択することにより、実行プランをキャプチャできます。  
  
## <a name="understanding-buffer-allocation"></a>バッファーの割り当てについて  
 実行プランに基づき、データ フロー タスクは、データ フロー コンポーネントの出力で定義された列を格納するバッファーを作成します。 このバッファーは、非同期出力型のコンポーネントを検出するまで、コンポーネントの処理手順を通じてデータ フロー内で再使用されます。 次に、新しいバッファーが作成され、非同期出力の出力列と下流コンポーネントの出力列が格納されます。  
  
 実行中、コンポーネントは現在のソース スレッドまたは作業スレッド内のバッファーにアクセスできます。 そのバッファーは、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> メソッドによって提供される入力バッファーか、または <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> メソッドによって提供される出力バッファーのどちらかです。 各バッファーは、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.Mode%2A> の <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> プロパティにより、入力バッファーまたは出力バッファーに識別されます。  
  
 非同期出力型の変換コンポーネントは、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> メソッドから既存の入力バッファーを受け取り、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> メソッドから新しい出力バッファーを受け取ります。 非同期出力型の変換コンポーネントは、入力バッファーおよび出力バッファーの両方を受け取る、唯一のデータ フロー コンポーネントです。  
  
 コンポーネントに提供されるバッファーには、コンポーネントの入力列コレクションまたは出力列コレクションにない列が含まれる場合があるため、コンポーネントの開発者は、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> メソッドを呼び出し、列の **LineageID** を指定することによってバッファー内の列を探すことができます。  
  
