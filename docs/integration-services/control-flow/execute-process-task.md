---
title: プロセス実行タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.executeprocesstask.f1
- sql13.dts.designer.executeprocesstask.general.f1
- sql13.dts.designer.executeprocesstask.process.f1
helpviewer_keywords:
- Execute Process task [Integration Services]
ms.assetid: aca5a0b5-34a9-45bc-a234-8e63ea51a1ee
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 214f28fbb977414d4e14fdd14f2be53e9b705bc1
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298335"
---
# <a name="execute-process-task"></a>プロセス実行タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  プロセス実行タスクは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ ワークフローの一部として、アプリケーションまたはバッチ ファイルを実行します。 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] や [!INCLUDE[ofprword](../../includes/ofprword-md.md)]などの標準的なアプリケーションを開くためにプロセス実行タスクを使用することもできますが、一般に、このタスクはデータ ソースを処理対象とするビジネス アプリケーションやバッチ ファイルを実行する場合に使用します。 たとえば、プロセス実行タスクを使用して、圧縮されたテキスト ファイルを展開できます。 さらに、そのテキスト ファイルをパッケージ内のデータ フローのデータ ソースとして使用できます。 その他の例として、プロセス実行タスクを使用し、毎日の売り上げレポートを生成するカスタムの [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] アプリケーションを実行することもできます。 その後、このレポートをメール送信タスクに添付し、配信リストに転送できます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、パッケージの実行など、ワークフロー操作を実行するその他のタスクが含まれます。 詳細については、「 [パッケージ実行タスク](../../integration-services/control-flow/execute-package-task.md)」を参照してください。  
  
## <a name="custom-log-entries-available-on-the-execute-process-task"></a>プロセス実行タスクで使用できるカスタム ログ エントリ  
 次の表は、プロセス実行タスクのカスタム ログ エントリの一覧です。 詳細については、「[Integration Services (SSIS) のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)」をご覧ください。  
  
|ログ エントリ|Description|  
|---------------|-----------------|  
|**ExecuteProcessExecutingProcess**|タスクで実行するように構成されているプロセスに関する情報を提供します。<br /><br /> 2 つのログ エントリが書き込まれます。 1 つのエントリには、タスクで実行される実行可能ファイルの名前と場所が含まれ、その他のエントリは、実行可能ファイルの終了を記録します。|  
|**ExecuteProcessVariableRouting**|実行可能ファイルの入力と出力にルーティングされる変数に関する情報を提供します。 ログ エントリは、stdin (入力)、stdout (出力)、および stderr (エラー出力) に書き込まれます。|  
  
## <a name="configuration-of-the-execute-process-task"></a>プロセス実行タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
### <a name="property-settings"></a>プロパティの設定  
 プロセス実行タスクがカスタム アプリケーションを実行するとき、アプリケーションには、次のいずれかまたは両方の方法で入力が提供されます。  
  
-   **StandardInputVariable** プロパティの設定で指定された変数。 変数の詳細については、「[Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)」と「[パッケージで変数を使用する](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)」を参照してください。  
  
-   **Arguments** プロパティの設定で指定された引数。 たとえば文書を Word で開く場合、引数で .doc ファイルの名前を指定できます。  
  
 1 回のプロセス実行タスクで複数の引数をカスタム アプリケーションに渡すには、それぞれの引数を空白で区切って指定します。 引数そのものに空白を含めることはできません。空白を含めた場合、タスクは実行されません。 変数の値を引数として渡す際には、式を使用できます。 次の例では、式を使って 2 つの変数の値を空白で区切り、引数として渡します。  
  
 `@variable1 + " " + @variable2`  
  
 プロセス実行タスクの各種プロパティを設定する際にも、式を使用できます。  
  
 **StandardInputVariable** プロパティを使用して入力を提供するようにプロセス実行タスクを構成した場合は、アプリケーションから **Console.ReadLine** メソッドを呼び出して、入力を読み取ります。 詳細については、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] クラス ライブラリで、[Console.ReadLine メソッド](https://go.microsoft.com/fwlink/?LinkId=129201)のトピックを参照してください。  
  
 **Arguments** プロパティを使用して入力を提供するようにプロセス実行タスクを構成した場合は、次のいずれかの手順を実行して、引数を取得します。  
  
-   Microsoft Visual Basic を使用してアプリケーションを作成する場合は、 **My.Application.CommandLineArgs** プロパティを設定します。 次の例では、 **My.Application.CommandLineArgs** プロパティを使用して、2 つの引数を取得しています。  
  
    ```vb  
    Dim variable1 As String = My.Application.CommandLineArgs.Item(0)  
    Dim variable2 As String = My.Application.CommandLineArgs.Item(1)   
    ```  
  
     詳細については、 [のリファレンスで、](https://go.microsoft.com/fwlink/?LinkId=129200)My.Application.CommandLineArgs プロパティ [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] のトピックを参照してください。  
  
-   Microsoft Visual C# を使用してアプリケーションを作成する場合は、**Main** メソッドを使用します。  
  
     詳細については、『C# プログラミング ガイド』の「 [コマンド ライン引数 (C# プログラミング ガイド)](https://go.microsoft.com/fwlink/?LinkId=129406)」を参照してください。  
  
 プロセス実行タスクには、 **StandardOutputVariable** プロパティおよび **StandardErrorVariable** プロパティがあります。それぞれ、アプリケーションの標準出力とエラー出力を取り込むための変数を指定できます。  
  
 さらに、プロセス実行タスクを構成することにより、作業ディレクトリ、タイムアウト時間、または実行可能ファイルが正常に実行されたことを示す値を指定できます。 また、実行可能ファイルのリターン コードが成功を示す値と一致しない場合、または指定された場所で実行可能ファイルが見つからない場合に、失敗するように構成できます。  
  
## <a name="programmatic-configuration-of-the-execute-process-task"></a>プログラムによるプロセス実行タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteProcess.ExecuteProcess>  
  
## <a name="execute-process-task-editor-general-page"></a>[プロセス実行タスク エディター]\([全般] ページ)
  **[プロセス実行タスク エディター]** ダイアログ ボックスの **[全般]** ページを使用すると、プロセス実行タスクの名前と説明を入力できます。  
  
### <a name="options"></a>および  
 **名前**  
 プロセス実行タスクの固有の名前を指定します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 プロセス実行タスクの説明を入力します。  
  
## <a name="execute-process-task-editor-process-page"></a>Execute Process Task Editor (Process Page)
  **[プロセス実行タスク エディター]** ダイアログ ボックスの **[処理]** ページを使用すると、プロセスを実行する際のオプションを構成できます。 オプションには、実行する実行可能ファイル、そのファイルの場所、コマンド プロンプト引数、入力するための変数、出力をキャプチャする変数などが含まれます。  
  
### <a name="options"></a>および  
 **[RequireFullFileName]**  
 指定した場所に実行可能ファイルが見つからなかった場合に、タスクを中止するかどうかを指定します。  
  
 **[実行可能ファイル]**  
 実行する実行可能ファイルの名前を入力します。  
  
 **引数**  
 コマンド プロンプト引数を指定します。  
  
 **[WorkingDirectory]**  
 実行可能ファイルが置かれているフォルダーのパスを入力するか、参照ボタン ( **[...]** ) をクリックしてフォルダーを指定します。  
  
 **[StandardInputVariable]**  
 プロセスへの入力を指定する変数を選択するか、\<[**新しい変数>]** をクリックして新しい変数を作成します。  
  
 **関連トピック:** [変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
 **[StandardOutputVariable]**  
 プロセスの出力をキャプチャする変数を選択するか、\<[**新しい変数]** をクリックして新しい変数を作成します。  
  
 **[StandardErrorVariable]**  
 プロセッサのエラー出力をキャプチャする変数を選択するか、\<[**新しい変数>]** をクリックして新しい変数を作成します。  
  
 **[FailTaskIfReturnCodeIsNotSuccessValue]**  
 プロセス終了コードが **[SuccessValue]** で指定されている値と異なった場合、タスクを終了するかどうかを指定します。  
  
 **[SuccessValue]**  
 実行可能ファイルが正常に終了した場合に返される値を指定します。 既定では、この値は **0**に設定されます。  
  
 **[TimeOut]**  
 プロセスを実行できる秒数を指定します。 値を **0** に指定すると、タイムアウト値が使用されず、プロセスは完了するかエラーが発生するまで実行されます。  
  
 **[TerminateProcessAfterTimeOut]**  
 **[TimeOut]** オプションで指定されたタイムアウト時間の後に、プロセスを強制終了するかどうかを指定します。 このオプションは、 **[TimeOut]** が **0**以外の場合にのみ使用できます。  
  
 **[WindowStyle]**  
 プロセスを実行する際のウィンドウのスタイルを指定します。  
  
## <a name="see-also"></a>参照  
 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)   
 [制御フロー](../../integration-services/control-flow/control-flow.md)  
  
  
