---
title: プログラムによるタスクの接続 | Microsoft Docs
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
- tasks [Integration Services], precedence constraints
- precedence constraints [Integration Services], connecting tasks
- constraints [Integration Services]
ms.assetid: 23668e88-cef4-4009-a9cf-38e607eab7a2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 51cce76a41cfcc513e633a20b16ca5e861fa492a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71299036"
---
# <a name="connecting-tasks-programmatically"></a>プログラムによるタスクの接続

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  優先順位制約は、<xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> クラスとしてオブジェクト モデル内に表されるもので、パッケージ内での <xref:Microsoft.SqlServer.Dts.Runtime.Executable> オブジェクトの実行順序を確立します。 優先順位制約を使用すると、パッケージ内のコンテナーやタスクを、直前のコンテナーやタスクの実行結果に依存して実行させることができます。 2 つの <xref:Microsoft.SqlServer.Dts.Runtime.Executable> オブジェクト間の優先順位制約は、コンテナー オブジェクトの <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraints.Add%2A> コレクションにある <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraints> メソッドを呼び出すことによって確立されます。 2 つの実行可能オブジェクト間の制約を作成したら、<xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> プロパティを設定して、制約で定義されている 2 番目の実行可能オブジェクトを実行する条件を設定します。  
  
 次の表で説明するように、<xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.EvalOp%2A> プロパティに指定する値に応じて、1 つの優先順位制約内で制約と式の両方を使用できます。  
  
|EvalOp プロパティの値|[説明]|  
|----------------------------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.Constraint>|制約付きコンテナーまたは制約付きタスクを実行するかどうかを実行結果が決定するように指定します。 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> の <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> プロパティを <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 列挙の目的の値に設定します。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.Expression>|制約付きコンテナーまたは制約付きタスクを実行するかどうかを式の値で決定するように指定します。 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Expression%2A> の <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> プロパティを設定します。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.ExpressionAndConstraint>|実行する制約付きコンテナーまたは制約付きタスクに対して、制約結果が発生し、式が評価するように指定します。 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> の <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> プロパティおよび <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Expression%2A> プロパティの両方を設定し、その <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.LogicalAnd%2A> プロパティを **true** に設定します。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.ExpressionOrConstraint>|実行する制約付きコンテナーまたは制約付きタスクに対して、制約結果が発生するか、または式が評価するように指定します。 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> の <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> プロパティおよび <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Expression%2A> プロパティの両方を設定し、その <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.LogicalAnd%2A> プロパティを **false** に設定します。|  
  
 次のコード例では、パッケージにタスクを 2 つ追加します。 次に、タスクの間に <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> を作成し、第 1 のタスクが終了するまで第 2 のタスクは実行しないように設定します。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
  
      // Add a File System task.  
      Executable eFileTask1 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileHost1 = eFileTask1 as TaskHost;  
  
      // Add a second File System task.  
      Executable eFileTask2 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileHost2 = eFileTask2 as TaskHost;  
  
      // Put a precedence constraint between the tasks.  
      // Set the constraint to specify that the second File System task cannot run  
      // until the first File System task finishes.  
      PrecedenceConstraint pcFileTasks =   
        p.PrecedenceConstraints.Add((Executable)thFileHost1, (Executable)thFileHost2);  
      pcFileTasks.Value = DTSExecResult.Completion;  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    ' Add a File System task.  
    Dim eFileTask1 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileHost1 As TaskHost = CType(eFileTask1, TaskHost)  
  
    ' Add a second File System task.  
    Dim eFileTask2 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileHost2 As TaskHost = CType(eFileTask2, TaskHost)  
  
    ' Put a precedence constraint between the tasks.  
    ' Set the constraint to specify that the second File System task cannot run  
    ' until the first File System task finishes.  
    Dim pcFileTasks As PrecedenceConstraint = _  
      p.PrecedenceConstraints.Add(CType(thFileHost1, Executable), CType(thFileHost2, Executable))  
    pcFileTasks.Value = DTSExecResult.Completion  
  
  End Sub  
  
End Module  
```
  
## <a name="see-also"></a>参照  
 [プログラムによるデータ フロー タスクの追加](../../integration-services/building-packages-programmatically/adding-the-data-flow-task-programmatically.md)  
  
  
