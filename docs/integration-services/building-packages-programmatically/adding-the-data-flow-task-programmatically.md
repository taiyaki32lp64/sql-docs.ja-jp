---
title: プログラムによるデータ フロー タスクの追加 | Microsoft Docs
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
- adding Data Flow task
- SSIS data flow
- data flow task [Integration Services], adding
- MainPipe object
ms.assetid: 0ca03712-a82e-4aa7-949b-f869a8936ddf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: db9545df35823161dbe6fa64673cac1361c3d34b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294921"
---
# <a name="adding-the-data-flow-task-programmatically"></a>プログラムによるデータ フロー タスクの追加

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] にはデータ フロー タスクというタスクがあります。これは、オブジェクト モデルでは <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper> 名前空間として表されます。 データ フロー タスクは、パッケージの実行時にデータを変換、移動する目的専用の、特殊で高性能なタスクです。 他のタスクと同様、データ フロー タスクは <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> オブジェクトによってラップされており、ランタイム エンジンはこれを単にパッケージ内のタスクの 1 つとして扱います。 ただし、データ フロー内には、別にデータ フロー コンポーネントというオブジェクトもあります。 これは変換元から変換先にデータを移動するコンポーネントで、その際に変換を経由する場合もあります。 コンポーネントには、移動の方向とデータの変換方法が定義されています。 データ フロー タスクを設定するには、タスクにコンポーネントを追加し、それを接続します。これにより、データ フローの確立と目的の変換を実行します。  
  
 データ フロー タスク内のコンポーネントには、 **[データ フローの変換元]** 、 **[データ フロー変換]** 、 **[データ フローの変換先]** の 3 種類があり、[!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナー ツールボックスにこの順序で表示されています。 これらの種類は単に変換元、変換、変換先と呼ばれる場合もあります。 名前からもわかるように、データは変換元から変換へと流れ、次に変換から変換先へと流れます。 これはデータ フローの概念をごく簡単に説明したにすぎません。データ フロー タスクは柔軟で強力なタスクであり、複数の変換元を処理することも、複数の変換先に出力を送信する変換を多数接続することもできます。  
  
 データ フロー タスクをパッケージに追加する方法は、他のタスクの場合と同じです。 タスクを追加したら、コンポーネントをデータ フロー タスクに追加したり、タスク内でコンポーネントを設定および接続することにより、データ フロー タスクを設定します。  
  
## <a name="sample"></a>サンプル  
 次のコード サンプルは、データ フロー タスクをパッケージに追加する方法を示しています。 この例では、Microsoft.SqlServer.PipelineHost、Microsoft.SqlServer.DTSPipelineWrap、および Microsoft.SqlServer.ManagedDTS アセンブリへの参照が必要です。  
  
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
      Package p = new Package();  
      Executable e = p.Executables.Add("STOCK:PipelineTask");  
      TaskHost thMainPipe = e as TaskHost;  
      MainPipe dataFlowTask = thMainPipe.InnerObject as MainPipe;   
    }  
  }  
}  
```  
  
```vb  
Imports System.IO  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    Dim e As Executable = p.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As TaskHost = CType(e, TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
  End Sub  
  
End Module  
```  
  
## <a name="external-resources"></a>外部リソース  
 blogs.msdn.com のブログ「[EzAPI - Updated for SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=243223)」(EzAPI - SQL Server 2012 用の更新)  
  
## <a name="see-also"></a>参照  
 [プログラムによるデータ フロー コンポーネントの検出](../../integration-services/building-packages-programmatically/discovering-data-flow-components-programmatically.md)  
  
  
