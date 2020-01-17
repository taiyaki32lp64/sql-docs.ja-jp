---
title: スクリプト タスクのコーディングおよびデバッグ | Microsoft Docs
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
- Script task [Integration Services], debugging
- SSIS Script task, development environment
- SSIS Script task, debugging
- Script task [Integration Services], development environment
- Script task [Integration Services], coding
- debugging [Integration Services], scripts
- VSTA
- SSIS Script task, coding
ms.assetid: 687c262f-fcab-42e8-92ae-e956f3d92d69
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1a437704946f379f38aa590ccbf53f240fad94cc
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296915"
---
# <a name="coding-and-debugging-the-script-task"></a>スクリプト タスクのコーディングおよびデバッグ

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **[スクリプト タスク エディター]** でスクリプト タスクを構成したら、スクリプト タスク開発環境でカスタム コードを記述します。  
  
## <a name="script-task-development-environment"></a>スクリプト タスク開発環境  
 スクリプト タスクは、スクリプト自体の開発環境として、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) を使用します。  
  
 スクリプト コードは、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic または [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# で記述されます。 スクリプト言語を指定するには、**スクリプト タスク エディター**で **[ScriptLanguage]** プロパティを設定します。 その他のプログラミング言語を使用する場合は、選択した言語でカスタム アセンブリを作成し、スクリプト タスク内のコードからその機能を呼び出すことができます。  
  
 スクリプト タスクで作成したスクリプトは、パッケージ定義に格納されます。 スクリプト ファイルが別途存在するわけではありません。 したがって、スクリプト タスクを使用してもパッケージの配置には影響しません。  
  
> [!NOTE]  
>  パッケージをデザインしてスクリプトをデバッグする際、スクリプト コードは一時的にプロジェクト ファイルに書き込まれます。 機密情報をファイルに保存することはセキュリティ上危険であるため、パスワードなどの重要な情報はスクリプト コードに書き込まないことをお勧めします。  
  
 既定では、 **[Option Strict]** が IDE で無効になっています。  
  
## <a name="script-task-project-structure"></a>スクリプト タスク プロジェクトの構造  
 スクリプト タスクに格納されているスクリプトを作成または変更する場合、VSTA は空の新しいプロジェクトを開くか、または既存のプロジェクトを再度開きます。 この VSTA プロジェクトを作成しても、パッケージの配置に影響はありません。このプロジェクトはパッケージ ファイル内部に保存され、スクリプト タスクは追加ファイルを作成しないためです。  
  
### <a name="project-items-and-classes-in-the-script-task-project"></a>スクリプト タスク プロジェクトのプロジェクト アイテムおよびクラス  
 VSTA の [プロジェクト エクスプローラー] ウィンドウに表示されるスクリプト タスク プロジェクトには、既定で **ScriptMain** という単一のアイテムが格納されます。 **ScriptMain** アイテムには、同じく **ScriptMain** という名前の単一のクラスが格納されます。 このクラスのコード要素は、スクリプト タスクに対して選択したプログラミング言語に応じて異なります。  
  
-   スクリプト タスクが [!INCLUDE[vb_orcas_long](../../../includes/vb-orcas-long-md.md)] プログラミング言語用に構成されている場合は、**ScriptMain** クラスにパブリック サブルーチン **Main** が含まれます。 **ScriptMain.Main** サブルーチンは、ユーザーのスクリプト タスクを実行するときにランタイムが呼び出すメソッドです。  
  
     既定では、新しいスクリプトの **Main** サブルーチン内にあるコードは、行 `Dts.TaskResult = ScriptResults.Success` のみです。 この行は、タスクの処理が正常に実行されたことをランタイムに通知します。 **Dts.TaskResult** プロパティは、「[スクリプト タスクから結果を返す](../../../integration-services/extending-packages-scripting/task/returning-results-from-the-script-task.md)」で説明されています。  
  
-   スクリプト タスクが Visual C# プログラミング言語用に構成されている場合は、**ScriptMain** クラスにパブリック メソッド **Main** が含まれます。 このメソッドは、スクリプト タスク実行時に呼び出されます。  
  
     既定では、**Main** メソッドに `Dts.TaskResult = (int)ScriptResults.Success` という行が含まれます。 この行は、タスクの処理が正常に実行されたことをランタイムに通知します。  
  
 **ScriptMain** アイテムには、**ScriptMain** クラス以外のクラスを格納できます。 クラスは、そのクラスが含まれているスクリプト タスクでのみ使用できます。  
  
 既定では、**ScriptMain** プロジェクト アイテムには、次のコードが自動生成されます。 コード テンプレートでも、スクリプト タスクの概要、および、変数、イベント、接続など、SSIS オブジェクトを取得および操作する方法に関する追加情報を提供します。  
  
```vb  
' Microsoft SQL Server Integration Services Script Task  
' Write scripts using Microsoft Visual Basic 2008.  
' The ScriptMain is the entry point class of the script.  
  
Imports System  
Imports System.Data  
Imports System.Math  
Imports Microsoft.SqlServer.Dts.Runtime.VSTAProxy  
  
<System.AddIn.AddIn("ScriptMain", Version:="1.0", Publisher:="", Description:="")> _  
Partial Class ScriptMain  
  
Private Sub ScriptMain_Startup(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Startup  
  
End Sub  
  
Private Sub ScriptMain_Shutdown(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Shutdown  
Try  
' Unlock variables from the read-only and read-write variable collection properties  
If (Dts.Variables.Count <> 0) Then  
Dts.Variables.Unlock()  
End If  
Catch ex As Exception  
        End Try  
End Sub  
  
Enum ScriptResults  
Success = DTSExecResult.Success  
Failure = DTSExecResult.Failure  
End Enum  
  
' The execution engine calls this method when the task executes.  
' To access the object model, use the Dts property. Connections, variables, events,  
' and logging features are available as members of the Dts property as shown in the following examples.  
'  
' To reference a variable, call Dts.Variables("MyCaseSensitiveVariableName").Value  
' To post a log entry, call Dts.Log("This is my log text", 999, Nothing)  
' To fire an event, call Dts.Events.FireInformation(99, "test", "hit the help message", "", 0, True)  
'  
' To use the connections collection use something like the following:  
' ConnectionManager cm = Dts.Connections.Add("OLEDB")  
' cm.ConnectionString = "Data Source=localhost;Initial Catalog=AdventureWorks;Provider=SQLNCLI10;Integrated Security=SSPI;Auto Translate=False;"  
'  
' Before returning from this method, set the value of Dts.TaskResult to indicate success or failure.  
'   
' To open Help, press F1.  
  
Public Sub Main()  
'  
' Add your code here  
'  
Dts.TaskResult = ScriptResults.Success  
End Sub  
  
End Class  
```  
  
```csharp  
/*  
   Microsoft SQL Server Integration Services Script Task  
   Write scripts using Microsoft Visual C# 2008.  
   The ScriptMain is the entry point class of the script.  
*/  
  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Runtime.VSTAProxy;  
using System.Windows.Forms;  
  
namespace ST_1bcfdbad36d94f8ba9f23a10375abe53.csproj  
{  
    [System.AddIn.AddIn("ScriptMain", Version = "1.0", Publisher = "", Description = "")]  
    public partial class ScriptMain  
    {  
        private void ScriptMain_Startup(object sender, EventArgs e)  
        {  
  
        }  
  
        private void ScriptMain_Shutdown(object sender, EventArgs e)  
        {  
            try  
            {  
                // Unlock variables from the read-only and read-write variable collection properties  
                if (Dts.Variables.Count != 0)  
                {  
                    Dts.Variables.Unlock();  
                }  
            }  
            catch  
            {  
            }  
        }  
  
        #region VSTA generated code  
        private void InternalStartup()  
        {  
            this.Startup += new System.EventHandler(ScriptMain_Startup);  
            this.Shutdown += new System.EventHandler(ScriptMain_Shutdown);  
        }  
        enum ScriptResults  
        {  
            Success = DTSExecResult.Success,  
            Failure = DTSExecResult.Failure  
        };  
  
        #endregion  
  
        /*  
The execution engine calls this method when the task executes.  
To access the object model, use the Dts property. Connections, variables, events,  
and logging features are available as members of the Dts property as shown in the following examples.  
  
To reference a variable, call Dts.Variables["MyCaseSensitiveVariableName"].Value;  
To post a log entry, call Dts.Log("This is my log text", 999, null);  
To fire an event, call Dts.Events.FireInformation(99, "test", "hit the help message", "", 0, true);  
  
To use the connections collection use something like the following:  
ConnectionManager cm = Dts.Connections.Add("OLEDB");  
cm.ConnectionString = "Data Source=localhost;Initial Catalog=AdventureWorks;Provider=SQLNCLI10;Integrated Security=SSPI;Auto Translate=False;";  
  
Before returning from this method, set the value of Dts.TaskResult to indicate success or failure.  
  
To open Help, press F1.  
*/  
  
        public void Main()  
        {  
            // TODO: Add your code here  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
    }  
```  
  
### <a name="additional-project-items-in-the-script-task-project"></a>スクリプト タスク プロジェクトのその他のプロジェクト アイテム  
 スクリプト タスク プロジェクトには、既定の **ScriptMain** アイテム以外のアイテムを格納できます。 プロジェクトには、クラス、モジュール、およびコード ファイルを追加できます。 また、フォルダーを使用してアイテムのグループを整理できます。 追加したすべてのアイテムは、パッケージ内部に保存されます。  
  
### <a name="references-in-the-script-task-project"></a>スクリプト タスク プロジェクトの参照  
 参照をマネージド アセンブリに追加するには、 **[プロジェクト エクスプローラー]** でスクリプト タスク プロジェクトを右クリックし、 **[参照の追加]** をクリックします。 詳しくは、「[スクリプティング ソリューションでの他のアセンブリの参照](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)」をご覧ください。  
  
> [!NOTE]  
>  プロジェクト参照は、VSTA IDE の **[クラス ビュー]** または**プロジェクト エクスプローラー**で表示できます。 どちらのウィンドウも **[表示]** メニューから開きます。 新しい参照は、 **[プロジェクト]** メニュー、**プロジェクト エクスプローラー**、または **[クラス ビュー]** から追加できます。  
  
## <a name="interacting-with-the-package-in-the-script-task"></a>スクリプト タスク内でのパッケージとの対話  
 スクリプト タスクは、<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> クラスのインスタンスであるグローバル オブジェクト **Dts**、およびそのメンバーを使用して、内部のパッケージや [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] ランタイムとやり取りします。  
  
 次の表は、<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> クラスのプリンシパルのパブリック メンバーの一覧です。このクラスは、グローバル オブジェクト **Dts** を介してスクリプト タスクのコードに公開されます。 このセクションのトピックでは、これらのメンバーを使用する方法についてさらに詳しく説明します。  
  
|メンバー|用途|  
|------------|-------------|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A>|パッケージで定義されている接続マネージャーへのアクセスを提供します。|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A>|スクリプト タスクでエラー、警告、および情報メッセージを発生させるためのイベント インターフェイスを提供します。|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A>|**TaskResult** のほか、ワークフローの分岐にも使用できる単一のオブジェクトをランタイムに返す簡単な方法を提供します。|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A>|タスクの進行状況や結果などの情報を、有効なログ プロバイダーに記録します。|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A>|タスクの成功または失敗をレポートします。|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Transaction%2A>|タスクのコンテナーを実行しているトランザクションが存在する場合、それを提供します。|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>|スクリプトで使用するため、**ReadOnlyVariables** および **ReadWriteVariables** タスク プロパティの一覧に含まれる変数へのアクセスを提供します。|  
  
 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> クラスには、使用しない可能性のあるパブリック メンバーも含まれています。  
  
|メンバー|[説明]|  
|------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A>|変数にアクセスするには、<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> プロパティの方が便利です。 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A> も使用できますが、読み書きする変数をロックおよびロック解除するためのメソッドを明示的に呼び出す必要があります。 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> プロパティを使用すると、スクリプト タスクにより自動的にロック セマンティクスが処理されます。|  
  
## <a name="debugging-the-script-task"></a>スクリプト タスクのデバッグ  
 スクリプト タスクのコードをデバッグするには、コードに少なくとも 1 つのブレークポイントを設定し、VSTA IDE を閉じて [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] でパッケージを実行します。 パッケージが実行されてスクリプト タスクが開始されると、VSTA IDE が再度開き、読み取り専用モードでコードが表示されます。 実行によりブレークポイントに到達したら、変数の値の検証や、残りのコードのステップ スルーができます。  
  
> [!WARNING]  
>  64 ビット モードでパッケージを実行すると、スクリプト タスクをデバッグすることができません。  
  
> [!NOTE]  
>  スクリプト タスクをデバッグするには、パッケージを実行する必要があります。 個別のタスクのみを実行する場合、スクリプト タスク コードのブレークポイントは無視されます。  
  
> [!NOTE]  
>  パッケージ実行タスクから実行されている子パッケージの一部としてスクリプト タスクを実行する場合は、スクリプト タスクをデバッグできません。 このような場合は、子パッケージのスクリプト タスク内で設定したブレークポイントは無視されます。 子パッケージを単独で実行することにより、通常どおりパッケージをデバッグできます。  
  
> [!NOTE]  
>  複数のスクリプト タスクが含まれるパッケージをデバッグする場合、デバッガーによってデバッグされるスクリプト タスクは 1 つです。 Foreach ループまたは For ループ コンテナーの場合と同様に、デバッガーが完了した場合、システムは別のスクリプト タスクをデバッグできます。  
  
## <a name="external-resources"></a>外部リソース  
  
-   blogs.msdn.com のブログ「[VSTA setup and configuration troubles for SSIS 2008 and R2 installations](https://go.microsoft.com/fwlink/?LinkId=215661)」(SSIS 2008 インストールおよび R2 インストールでの VSTA のセットアップと構成に関する問題)。  
  
## <a name="see-also"></a>参照  
 [スクリプティング ソリューションでの他のアセンブリの参照](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)   
 [スクリプト タスク エディターでのスクリプト タスクの構成](../../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)  
  
  
