---
title: プロセス実行タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executeprocesstask.f1
helpviewer_keywords:
- Execute Process task [Integration Services]
ms.assetid: aca5a0b5-34a9-45bc-a234-8e63ea51a1ee
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8b21aa5d2834143ab012b90e0fa6f8a1e22a8314
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62831869"
---
# <a name="execute-process-task"></a>プロセス実行タスク
  プロセス実行タスクは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ ワークフローの一部として、アプリケーションまたはバッチ ファイルを実行します。 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] や [!INCLUDE[ofprword](../../includes/ofprword-md.md)]などの標準的なアプリケーションを開くためにプロセス実行タスクを使用することもできますが、一般に、このタスクはデータ ソースを処理対象とするビジネス アプリケーションやバッチ ファイルを実行する場合に使用します。 たとえば、プロセス実行タスクを使用して、圧縮されたテキスト ファイルを展開できます。 さらに、そのテキスト ファイルをパッケージ内のデータ フローのデータ ソースとして使用できます。 その他の例として、プロセス実行タスクを使用し、毎日の売り上げレポートを生成するカスタムの [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] アプリケーションを実行することもできます。 その後、このレポートをメール送信タスクに添付し、配信リストに転送できます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、パッケージの実行など、ワークフロー操作を実行するその他のタスクが含まれます。 詳細については、「 [パッケージ実行タスク](execute-package-task.md)」を参照してください。  
  
## <a name="custom-log-entries-available-on-the-execute-process-task"></a>プロセス実行タスクで使用できるカスタム ログ エントリ  
 次の表は、プロセス実行タスクのカスタム ログ エントリの一覧です。 詳しくは、「[Integration Services &#40;SSIS&#41; のログ記録](../performance/integration-services-ssis-logging.md)」と「[ログ記録用のカスタム メッセージ](../custom-messages-for-logging.md)」をご覧ください。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`ExecuteProcessExecutingProcess`|タスクで実行するように構成されているプロセスに関する情報を提供します。<br /><br /> 2 つのログ エントリが書き込まれます。 1 つのエントリには、タスクで実行される実行可能ファイルの名前と場所が含まれ、その他のエントリは、実行可能ファイルの終了を記録します。|  
|`ExecuteProcessVariableRouting`|実行可能ファイルの入力と出力にルーティングされる変数に関する情報を提供します。 ログ エントリは、stdin (入力)、stdout (出力)、および stderr (エラー出力) に書き込まれます。|  
  
## <a name="configuration-of-the-execute-process-task"></a>プロセス実行タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[プロセス実行タスク エディター] &#40;[全般] ページ&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [[プロセス実行タスク エディター] &#40;[処理] ページ&#41;](../execute-process-task-editor-process-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
### <a name="property-settings"></a>プロパティの設定  
 プロセス実行タスクがカスタム アプリケーションを実行するとき、アプリケーションには、次のいずれかまたは両方の方法で入力が提供されます。  
  
-   **StandardInputVariable** プロパティの設定で指定された変数。 変数の詳細については、「[Integration Services &#40;SSIS&#41; の変数](../integration-services-ssis-variables.md)」と「[パッケージで変数を使用する](../use-variables-in-packages.md)」を参照してください。  
  
-   **Arguments** プロパティの設定で指定された引数。 たとえば文書を Word で開く場合、引数で .doc ファイルの名前を指定できます。  
  
 1 回のプロセス実行タスクで複数の引数をカスタム アプリケーションに渡すには、それぞれの引数を空白で区切って指定します。 引数そのものに空白を含めることはできません。空白を含めた場合、タスクは実行されません。 変数の値を引数として渡す際には、式を使用できます。 次の例では、式を使って 2 つの変数の値を空白で区切り、引数として渡します。  
  
 `@variable1 + " " + @variable2`  
  
 プロセス実行タスクの各種プロパティを設定する際にも、式を使用できます。  
  
 使用すると、 **StandardInputVariable**入力を提供するプロセス実行タスクを構成するプロパティを呼び出す、`Console.ReadLine`で入力を読み取るアプリケーションからのメソッド。 詳細については、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] クラス ライブラリで、[Console.ReadLine メソッド](https://go.microsoft.com/fwlink/?LinkId=129201)のトピックを参照してください。  
  
 **Arguments** プロパティを使用して入力を提供するようにプロセス実行タスクを構成した場合は、次のいずれかの手順を実行して、引数を取得します。  
  
-   Microsoft Visual Basic を使用してアプリケーションを作成する場合は、`My.Application.CommandLineArgs` プロパティを設定します。 次の例では、`My.Application.CommandLineArgs` プロパティを使用して、2 つの引数を取得しています。  
  
    ```  
    Dim variable1 As String = My.Application.CommandLineArgs.Item(0)  
    Dim variable2 As String = My.Application.CommandLineArgs.Item(1)   
    ```  
  
     詳細については、 [のリファレンスで、](https://go.microsoft.com/fwlink/?LinkId=129200)My.Application.CommandLineArgs プロパティ [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] のトピックを参照してください。  
  
-   Microsoft Visual C# を使用してアプリケーションを作成する場合は、`Main` メソッドを使用します。  
  
     詳細については、『C# プログラミング ガイド』の「 [コマンド ライン引数 (C# プログラミング ガイド)](https://go.microsoft.com/fwlink/?LinkId=129406)」を参照してください。  
  
 プロセス実行タスクには、 **StandardOutputVariable** プロパティおよび **StandardErrorVariable** プロパティがあります。それぞれ、アプリケーションの標準出力とエラー出力を取り込むための変数を指定できます。  
  
 さらに、プロセス実行タスクを構成することにより、作業ディレクトリ、タイムアウト時間、または実行可能ファイルが正常に実行されたことを示す値を指定できます。 また、実行可能ファイルのリターン コードが成功を示す値と一致しない場合、または指定された場所で実行可能ファイルが見つからない場合に、失敗するように構成できます。  
  
## <a name="programmatic-configuration-of-the-execute-process-task"></a>プログラムによるプロセス実行タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteProcess.ExecuteProcess>  
  
## <a name="see-also"></a>参照  
 [Integration Services タスク](integration-services-tasks.md)   
 [制御フロー](control-flow.md)  
  
  
