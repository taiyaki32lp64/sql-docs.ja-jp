---
title: スクリプト タスクでの変数の使用 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Foreach Loop containers
- Script task [Integration Services], variables
- scripts [Integration Services], variables
- Variables property
- Variable object
- SSIS Script task, variables
- variables [Integration Services], Script task
ms.assetid: 593b5961-4bfa-4ce1-9531-a251c34e89d3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c01695891e1d41fed5e1e5c293a18f74462a4151
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285984"
---
# <a name="using-variables-in-the-script-task"></a>スクリプト タスクでの変数の使用

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  スクリプト タスクで変数を使用すると、パッケージ内の別のオブジェクトとデータを交換できます。 詳細については、「 [Integration Services &#40;SSIS&#41; の変数](../../../integration-services/integration-services-ssis-variables.md)」を参照してください。  
  
 スクリプト タスクは、**Dts** オブジェクトの <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> プロパティを使用して、パッケージ内の <xref:Microsoft.SqlServer.Dts.Runtime.Variable> オブジェクトからデータを読み取ったり、オブジェクトにデータを書き込んだりします。  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Dts.Runtime.Variable> クラスの <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A> プロパティのデータ型は **Object** です。 スクリプト タスクでは **Option Strict** が有効なので、使用する前に、<xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A> プロパティを適切な型にキャストする必要があります。  
  
 既存の変数は、 **[スクリプト タスク エディター]** の <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadOnlyVariables%2A> の一覧および <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadWriteVariables%2A> の一覧に追加することにより、カスタム スクリプトで使用できるようになります。 変数名の大文字と小文字は区別されることに注意してください。 スクリプト内では、**Dts** オブジェクトの <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> プロパティを介して、両方の種類の変数にアクセスできます。 **Value** プロパティを使用して、各変数に対する読み取りおよび書き込みを行います。 スクリプト タスクは、スクリプトが変数の値を読み取ったり変更するときに、ユーザーに意識させずにロックを管理します。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Variables.Contains%2A> プロパティによって返される <xref:Microsoft.SqlServer.Dts.Runtime.Variables> コレクションの <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> メソッドを使用すると、変数をコードで使用する前に、その変数の存在を確認できます。  
  
 スクリプト タスクで変数を扱うには、<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A> プロパティ (Dts.VariableDispenser) を使用することもできます。 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A> を使用する場合は、コード内で、ロック セマンティクスと、変数値のデータ型のキャストの両方を処理する必要があります。 デザイン時には使用できないが、実行時にプログラムによって生成される変数を扱う必要がある場合は、<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A> プロパティではなく、<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> プロパティを使用する必要が生じる場合があります。  
  
## <a name="using-the-script-task-within-a-foreach-loop-container"></a>Foreach ループ コンテナー内でのスクリプト タスクの使用  
 Foreach ループ コンテナー内でスクリプト タスクを繰り返し実行する場合、そのスクリプトは通常、列挙子内の現在のアイテムの内容を処理する必要があります。 たとえば、Foreach File 列挙子を使用する場合、スクリプトは現在のファイル名を取得する必要があります。また、Foreach ADO 列挙子を使用する場合、スクリプトは現在のデータ行の列の内容を取得する必要があります。  
  
 変数を使用すると、Foreach ループ コンテナーとスクリプト タスク間のこうしたやり取りが可能になります。 **[Foreach ループ エディター]** の **[変数のマッピング]** ページでは、単一の列挙アイテムによって返されたデータの各アイテムに、変数が割り当てられます。 たとえば、Foreach File 列挙子の場合は、ファイル名のみがインデックス 0 で返されるためマッピングが必要な変数は 1 つのみですが、各行の複数のデータ列を返す列挙子の場合は、スクリプト タスクで使用する各列に、個別の変数をマップする必要があります。  
  
 列挙アイテムを変数にマップしたら、マップされた変数をスクリプトで使用できるように、 **[スクリプト タスク エディター]** の **[スクリプト]** ページで、それらの変数を **ReadOnlyVariables** プロパティに追加する必要があります。 フォルダー内の画像ファイルを処理する Foreach ループ コンテナー内のスクリプト タスクの例については、「[スクリプト タスクによる画像の操作](../../../integration-services/extending-packages-scripting-task-examples/working-with-images-with-the-script-task.md)」を参照してください。  
  
## <a name="variables-example"></a>変数の例  
 次の例では、スクリプト タスク内の変数にアクセスし、その変数を使用してパッケージ ワークフローのパスを決定する方法を示します。 このサンプルでは、`CustomerCount` および `MaxRecordCount` という名前の整数型の変数を作成し、 **[スクリプト タスク エディター]** の **ReadOnlyVariables** コレクションに追加してあるものとします。 `CustomerCount` 変数には、インポートされる顧客レコードの数が格納されます。 この値が `MaxRecordCount` の値よりも大きい場合、スクリプト タスクから失敗が報告されます。 `MaxRecordCount` のしきい値を超過したために失敗が発生した場合、ワークフローのエラー パスには、任意の必要なクリーンアップを実装できます。  
  
 サンプルを正常にコンパイルするには、Microsoft.SqlServer.ScriptTask アセンブリへの参照を追加する必要があります。  
  
```vb  
Public Sub Main()  
  
    Dim customerCount As Integer  
    Dim maxRecordCount As Integer  
  
    If Dts.Variables.Contains("CustomerCount") = True AndAlso _  
        Dts.Variables.Contains("MaxRecordCount") = True Then  
  
        customerCount = _  
            CType(Dts.Variables("CustomerCount").Value, Integer)  
        maxRecordCount = _  
            CType(Dts.Variables("MaxRecordCount").Value, Integer)  
  
    End If  
  
    If customerCount > maxRecordCount Then  
            Dts.TaskResult = ScriptResults.Failure  
    Else  
            Dts.TaskResult = ScriptResults.Success  
    End If  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Runtime;  
  
public class ScriptMain  
{  
  
    public void Main()  
    {  
        int customerCount;  
        int maxRecordCount;  
  
        if (Dts.Variables.Contains("CustomerCount")==true&&Dts.Variables.Contains("MaxRecordCount")==true)  
  
        {  
            customerCount = (int) Dts.Variables["CustomerCount"].Value;  
            maxRecordCount = (int) Dts.Variables["MaxRecordCount"].Value;  
  
        }  
  
        if (customerCount>maxRecordCount)  
        {  
            Dts.TaskResult = (int)ScriptResults.Failure;  
        }  
        else  
        {  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
  
    }  
  
}  
  
```  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; の変数](../../../integration-services/integration-services-ssis-variables.md)   
 [パッケージで変数を使用する](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  
