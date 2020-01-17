---
title: スクリプト タスクによるパフォーマンス カウンターの監視 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5de911200c7fbe91c912c7ac7a321f79226b6452
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768508"
---
# <a name="monitoring-performance-counters-with-the-script-task"></a>スクリプト タスクによるパフォーマンス カウンターの監視
  システム管理者は、大容量のデータ上で複雑な変換を実行する [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのパフォーマンスを監視する必要が生じる場合があります。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の **System.Diagnostics** 名前空間には、既存のパフォーマンス カウンターを使用したり、ユーザー独自のパフォーマンス カウンターを作成するためのクラスが用意されています。  
  
 パフォーマンス カウンターはアプリケーションのパフォーマンス情報を格納するので、これを使用して、時間経過に伴うソフトウェアのパフォーマンスを分析できます。 パフォーマンス カウンターは **[パフォーマンス モニター]** ツールを使用して、ローカルまたはリモートで監視できます。 パフォーマンス カウンターの値を変数に格納して、後でパッケージ内で制御フローを分岐するために使用できます。  
  
 パフォーマンス カウンターを使用する代わりに、`Dts` オブジェクトの <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A> プロパティを介して、<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> イベントを発生させることができます。 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A> イベントは、進捗状況および完了した割合に関する情報を、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ランタイムに返します。  
  
> [!NOTE]  
>  複数のパッケージでより簡単に再利用できるタスクを作成する場合は、このスクリプト タスク サンプルのコードを基にした、カスタム タスクの作成を検討してください。 詳細については、「 [カスタム タスクの開発](../extending-packages-custom-objects/task/developing-a-custom-task.md)」を参照してください。  
  
## <a name="description"></a>説明  
 次の例では、カスタム パフォーマンス カウンターを作成し、カウンターの値を増やします。 最初に、パフォーマンス カウンターが既に存在しているかどうかを判別します。 パフォーマンス カウンターが作成されていない場合、スクリプトは `Create` オブジェクトの `PerformanceCounterCategory` メソッドを呼び出してパフォーマンス カウンターを作成します。 パフォーマンス カウンターが作成されたら、スクリプトはそのカウンターの値を増やします。 最後に、この例ではベスト プラクティスに従って、パフォーマンス カウンターが不要になると、そのカウンターに対して `Close` メソッドを呼び出します。  
  
> [!NOTE]  
>  パフォーマンス カウンター カテゴリとパフォーマンス カウンターを新しく作成するには、管理権限が必要です。 また、新しいカテゴリとカウンターは、作成後もコンピューターに保存されます。  
  
#### <a name="to-configure-this-script-task-example"></a>このスクリプト タスクの例を構成するには  
  
-   使用して、`Imports`をインポートする、コード内のステートメント、 **System.Diagnostics**名前空間。  
  
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
  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
  
