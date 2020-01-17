---
title: スクリプト タスクによるパフォーマンス カウンターの監視 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- performance counters [Integration Services]
- SSIS Script task, performance counters
- custom performance counters [Integration Services]
- Script task [Integration Services], examples
- Script task [Integration Services], performance counters
- counters [Integration Services]
ms.assetid: 86609bf1-cae6-435e-a58d-41bdfc521e94
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ed4bca496d48e5fe268c1a425223fe03c8fcc6e7
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297037"
---
# <a name="monitoring-performance-counters-with-the-script-task"></a>スクリプト タスクによるパフォーマンス カウンターの監視

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  システム管理者は、大容量のデータ上で複雑な変換を実行する [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのパフォーマンスを監視する必要が生じる場合があります。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の **System.Diagnostics** 名前空間には、既存のパフォーマンス カウンターを使用したり、ユーザー独自のパフォーマンス カウンターを作成するためのクラスが用意されています。  
  
 パフォーマンス カウンターはアプリケーションのパフォーマンス情報を格納するので、これを使用して、時間経過に伴うソフトウェアのパフォーマンスを分析できます。 パフォーマンス カウンターは **[パフォーマンス モニター]** ツールを使用して、ローカルまたはリモートで監視できます。 パフォーマンス カウンターの値を変数に格納して、後でパッケージ内で制御フローを分岐するために使用できます。  
  
 パフォーマンス カウンターを使用する代わりに、**Dts** オブジェクトの <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> プロパティを介して、<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A> イベントを発生させることができます。 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A> イベントは、進捗状況および完了した割合に関する情報を、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ランタイムに返します。  
  
> [!NOTE]  
>  複数のパッケージでより簡単に再利用できるタスクを作成する場合は、このスクリプト タスク サンプルのコードを基にした、カスタム タスクの作成を検討してください。 詳細については、「 [カスタム タスクの開発](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)」を参照してください。  
  
## <a name="description"></a>[説明]  
 次の例では、カスタム パフォーマンス カウンターを作成し、カウンターの値を増やします。 最初に、パフォーマンス カウンターが既に存在しているかどうかを判別します。 パフォーマンス カウンターが作成されていない場合、スクリプトは **PerformanceCounterCategory** オブジェクトの **Create** メソッドを呼び出してパフォーマンス カウンターを作成します。 パフォーマンス カウンターが作成されたら、スクリプトはそのカウンターの値を増やします。 最後に、この例ではベスト プラクティスに従って、パフォーマンス カウンターが不要になると、そのカウンターに対して **Close** メソッドを呼び出します。  
  
> [!NOTE]  
>  パフォーマンス カウンター カテゴリとパフォーマンス カウンターを新しく作成するには、管理権限が必要です。 また、新しいカテゴリとカウンターは、作成後もコンピューターに保存されます。  
  
#### <a name="to-configure-this-script-task-example"></a>このスクリプト タスクの例を構成するには  
  
-   コードで **Imports** ステートメントを使用し、**System.Diagnostics** 名前空間をインポートします。  
  
### <a name="example-code"></a>コード例  
  
```vb  
Public Sub Main()  
  
    Dim myCounter As PerformanceCounter  
  
    Try  
        'Create the performance counter if it does not already exist.  
        If Not _  
        PerformanceCounterCategory.Exists("TaskExample") Then  
            PerformanceCounterCategory.Create("TaskExample", _  
                "Task Performance Counter Example", "Iterations", _  
                "Number of times this task has been called.")  
        End If  
  
        'Initialize the performance counter.  
        myCounter = New PerformanceCounter("TaskExample", _  
            "Iterations", String.Empty, False)  
  
        'Increment the performance counter.  
        myCounter.Increment()  
  
         myCounter.Close()  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, _  
            "Task Performance Counter Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
```  
  
```csharp  
  
public class ScriptMain  
{  
  
public void Main()  
        {  
  
            PerformanceCounter myCounter;  
  
            try  
            {  
                //Create the performance counter if it does not already exist.  
                if (!PerformanceCounterCategory.Exists("TaskExample"))  
                {  
                    PerformanceCounterCategory.Create("TaskExample", "Task Performance Counter Example", "Iterations", "Number of times this task has been called.");  
                }  
  
                //Initialize the performance counter.  
                myCounter = new PerformanceCounter("TaskExample", "Iterations", String.Empty, false);  
  
                //Increment the performance counter.  
                myCounter.Increment();  
  
                myCounter.Close();  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                Dts.Events.FireError(0, "Task Performance Counter Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
  
```  
