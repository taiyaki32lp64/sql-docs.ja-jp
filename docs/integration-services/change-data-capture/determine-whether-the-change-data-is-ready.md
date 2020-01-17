---
title: 変更データの準備ができているかどうかを判断する | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],determining readiness
ms.assetid: 04935f35-96cc-4d70-a250-0fd326f8daff
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 025961e39a4f0b1beb0588f0dc7ef2c668bd09a2
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294770"
---
# <a name="determine-whether-the-change-data-is-ready"></a>データの変更の準備ができているかどうかを判断する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  変更データの増分読み込みを実行する [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの制御フローにおいて、2 番目のタスクは、選択した間隔の変更データが準備できていることを確認することです。 選択したエンドポイントまでの変更が非同期キャプチャ プロセスでまだ一部処理されていない可能性があるため、この手順が必要となります。  
  
> [!NOTE]  
>  制御フローの最初のタスクは、変更間隔のエンドポイントを計算することです。 このタスクに関する詳細については、「[変更データの間隔を指定する](../../integration-services/change-data-capture/specify-an-interval-of-change-data.md)」を参照してください。 制御フローをデザインするプロセス全体の説明については、「[変更データ キャプチャ &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)」を参照してください。  
  
## <a name="understanding-the-components-of-the-solution"></a>ソリューションのコンポーネントについて  
 このトピックで説明するソリューションでは、次の 4 つの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントを使用します。  
  
-   SQL 実行タスクの出力を繰り返し評価する For ループ コンテナー。  
  
-   変更データ キャプチャ プロセスによって保持されている特殊なテーブルに対してクエリを実行し、この情報を使用してデータが準備できているかどうかを判断する SQL 実行タスク。  
  
-   データが準備できていない場合に処理の遅延を実装するコンポーネント。 このコンポーネントは、スクリプト タスクまたは SQL 実行タスクのいずれかになります。  
  
-   (省略可) SQL 実行タスクによってエラーまたはタイムアウト状態を示す値が返されたときにエラーまたはタイムアウトを報告するコンポーネント。  
  
 これらのコンポーネントによって、いくつかのパッケージ変数の値が設定されるか読み取られ、ループ内およびパッケージの後続の実行フローが制御されます。  
  
#### <a name="to-set-up-package-variables"></a>パッケージ変数を設定するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]の **[変数]** ウィンドウで、次の変数を作成します。  
  
    1.  SQL 実行タスクによって返される状態値を格納する整数データ型の変数を作成します。  
  
         この例では、初期値が 0 である DataReady という名前の変数を使用します。  
  
    2.  データが準備できていない場合の遅延時間を格納する変数を作成します。 スクリプト タスクを使用して遅延を実装する場合、変数には整数データ型が格納されます。 WAITFOR ステートメントを実行する SQL 実行タスクを使用する場合、変数には文字列データ型が格納され、"00:00:10" などの値を設定できます。  
  
         この例では、初期値が 10 である DelaySeconds という名前の変数を使用します。  
  
    3.  ループの現在の反復を格納する整数データ型の変数を作成します。  
  
         この例では、初期値が 0 である TimeoutCount という名前の変数を使用します。  
  
    4.  タイムアウト状態を報告する前にループでデータをテストする回数を指定する整数データ型の変数を作成します。  
  
         この例では、初期値が 20 である TimeoutCeiling という名前の変数を使用します。  
  
    5.  (省略可) 変更データの最初の読み込みを示すために使用できる整数データ型の変数を作成します。  
  
         この例では、IntervalID という名前の変数を使用し、値が最初の読み込みを示す 0 であることだけをチェックします。  
  
## <a name="configuring-a-for-loop-container"></a>For ループ コンテナーの構成  
 変数を設定したら、まず For ループ コンテナーを追加します。  
  
#### <a name="to-configure-a-for-loop-container-to-wait-until-change-data-is-ready"></a>変更データが準備できるまで待機するように For ループ コンテナーを構成するには  
  
1.  **デザイナーの** [制御フロー] [!INCLUDE[ssIS](../../includes/ssis-md.md)] タブで、For ループ コンテナーを制御フローに追加します。  
  
2.  間隔のエンドポイントを計算する SQL 実行タスクを For ループ コンテナーに連結します。  
  
3.  **[For ループ エディター]** で、次のオプションを選択します。  
  
    1.  **[InitExpression]** に「 `@DataReady = 0`」と入力します。  
  
         この式によって、ループ変数の初期値が設定されます。  
  
    2.  **[EvalExpression]** に「 `@DataReady == 0`」と入力します。  
  
         この式が **False**と評価されると、実行がループの外に移り、増分読み込みが開始されます。  
  
## <a name="configuring-the-execute-sql-task-that-queries-for-change-data"></a>変更データのクエリを実行する SQL 実行タスクの構成  
 For ループ コンテナー内に SQL 実行タスクを追加します。 このタスクでは、変更データ キャプチャ プロセスがデータベースに保持しているテーブルに対してクエリを実行します。 このクエリの結果は、変更データが準備できているかどうかを示す状態値です。  
  
 次の表の 1 列目は、サンプルの Transact-SQL クエリによって SQL 実行タスクから返される値を示しています。 2 列目は、その他のコンポーネントがこれらの値に応答する方法を示しています。  
  
|戻り値|意味|応答|  
|------------------|-------------|--------------|  
|0|変更データが準備できていないことを示します。<br /><br /> 選択した間隔の終了時点より後に変更データ キャプチャ レコードがありません。|遅延を実装するコンポーネントから実行が継続されます。 その後、制御が For ループ コンテナーに戻り、返される値が 0 である限り引き続きコンテナーによって SQL 実行タスクがチェックされます。|  
|1|間隔全体にわたって変更データがキャプチャされていないか、変更データが削除されていることを示します。 これは、エラー状態として扱われます。<br /><br /> 選択した間隔の開始時点より前に変更データ キャプチャ レコードがありません。|エラーをログに記録するオプションのコンポーネントから実行が継続されます。|  
|2|データが準備できていることを示します。<br /><br /> 選択した間隔の開始時点より前にも終了時点より後にも変更データ キャプチャ レコードがあります。|実行が For ループ コンテナーの外に移り、増分読み込みが開始されます。|  
|3|使用可能なすべての変更データの最初の読み込みを示します。<br /><br /> この値は、このためだけに使用される特殊なパッケージ変数から条件ロジックによって取得されます。|実行が For ループ コンテナーの外に移り、増分読み込みが開始されます。|  
|5|TimeoutCeiling に達したことを示します。<br /><br /> 指定された回数だけループでデータがテストされましたが、データはまだ使用できません。 このテストまたは同様のテストを実行しないと、パッケージが無期限に実行される可能性があります。|タイムアウトをログに記録するオプションのコンポーネントから実行が継続されます。|  
  
#### <a name="to-configure-an-execute-sql-task-to-query-whether-change-data-is-ready"></a>変更データが準備できているかどうかをクエリするように SQL 実行タスクを構成するには  
  
1.  For ループ コンテナー内に SQL 実行タスクを追加します。  
  
2.  **[SQL 実行タスク エディター]** の **[全般]** ページで、次のオプションを選択します。  
  
    1.  **[ResultSet]** で **[単一行]** を選択します。  
  
    2.  ソース データベースへの有効な接続を構成します。  
  
    3.  **[SQLSourceType]** で **[直接入力]** を選択します。  
  
    4.  **[SQLStatement]** に、次の SQL ステートメントを入力します。  
  
        ```  
        declare @DataReady int, @TimeoutCount int  
  
        if not exists (select tran_end_time from cdc.lsn_time_mapping  
                where tran_end_time > ?  )  
            select @DataReady = 0  
        else  
            if ? = 0  
                select @DataReady = 3   
        else  
            if not exists (select tran_end_time from cdc.lsn_time_mapping  
                    where tran_end_time <= ? )  
                select @DataReady = 1   
        else  
            select @DataReady = 2  
  
        select @TimeoutCount = ?  
        if (@DataReady = 0)  
            select @TimeoutCount = @TimeoutCount + 1  
        else  
            select @TimeoutCount = 0  
  
        if (@TimeoutCount > ?)  
            select @DataReady = 5  
  
        select @DataReady as DataReady, @TimeoutCount as TimeoutCount  
  
        ```  
  
3.  **[SQL 実行タスク エディター]** の **[パラメーター マッピング]** ページで、次のマッピングを行います。  
  
    1.  ExtractEndTime 変数をパラメーター 0 にマップします。  
  
    2.  IntervalID 変数をパラメーター 1 にマップします。  
  
    3.  ExtractStartTime 変数をパラメーター 2 にマップします。  
  
    4.  TimeoutCount 変数をパラメーター 3 にマップします。  
  
    5.  TimeoutCeiling 変数をパラメーター 4 にマップします。  
  
4.  **[SQL 実行タスク エディター]** の **[結果セット]** ページで、DataReady の結果を DataReady 変数に、TimeoutCount の結果を TimeoutCount 変数にマップします。  
  
## <a name="waiting-until-the-change-data-is-ready"></a>変更データが準備できるまでの待機  
 いくつかある方法のうちいずれかを使用して、変更データが準備できていない場合に遅延を実装することができます。 次の 2 つの手順は、スクリプト タスクまたは SQL 実行タスクを使用して遅延を実装する方法を示しています。  
  
> [!NOTE]  
>  発生するオーバーヘッドは、SQL 実行タスクよりも事前コンパイルしたスクリプトの方が少なくなります。  
  
#### <a name="to-implement-a-delay-by-using-a-script-task"></a>スクリプト タスクを使用して遅延を実装するには  
  
1.  For ループ コンテナー内にスクリプト タスクを追加します。  
  
2.  変更データが準備できているかどうかを判断するためにクエリを実行する SQL 実行タスクを新しいスクリプト タスクに連結します。  
  
3.  SQL 実行タスクをスクリプト タスクに連結する優先順位制約のために、 **[優先順位制約エディター]** を開いて次のオプションを選択します。  
  
    1.  **[評価操作]** で **[式と制約]** を選択します。  
  
    2.  **[値]** で **[成功]** を選択します。  
  
         制約値 **[成功]** は、前のタスクの成功を表します。 この場合は、SQL 実行タスクの成功を表します。  
  
    3.  **[式]** に「`@DataReady == 0 && @TimeoutCount <= @TimeoutCeiling`」と入力します。  
  
    4.  **[論理 AND (すべての制約が True と評価される必要があります)** ] が選択されていない場合は、選択します。  
  
4.  **[スクリプト タスク エディター]** の **[スクリプト]** ページの **[ReadOnlyVariables]** で、 **[User::DelaySeconds]** 整数変数を一覧から選択します。  
  
5.  **[スクリプト タスク エディター]** の **[スクリプト]** ページで、 **[スクリプトの編集]** をクリックしてスクリプト開発環境を開きます。  
  
6.  Main プロシージャに、次のいずれかのコード行を入力します。  
  
    -   C# でプログラミングしている場合は、次のコード行を入力します。  
  
        ```  
        System.Threading.Thread.Sleep((int)Dts.Variables["DelaySeconds"].Value * 1000);  
        ```  
  
         \- - または -  
  
    -   [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]でプログラミングしている場合は、次のコード行を入力します。  
  
        ```  
        System.Threading.Thread.Sleep(Ctype(Dts.Variables("DelaySeconds").Value, Integer) * 1000)  
  
        ```  
  
        > [!NOTE]  
        >  **Thread.Sleep** メソッドは、ミリ秒単位で指定される引数を想定しています。  
  
7.  スクリプトの実行から **DtsExecResult.Success** を返す既定のコード行はそのまま使用します。  
  
8.  スクリプト開発環境と **[スクリプト タスク エディター]** を閉じます。  
  
#### <a name="to-implement-a-delay-by-using-an-execute-sql-task"></a>SQL 実行タスクを使用して遅延を実装するには  
  
1.  For ループ コンテナー内に SQL 実行タスクを追加します。  
  
2.  変更データが準備できているかどうかを判断するためにクエリを実行する SQL 実行タスクを新しい SQL 実行タスクに連結します。  
  
3.  2 つの SQL 実行タスクを連結する優先順位制約のために、 **[優先順位制約エディター]** を開いて次のオプションを選択します。  
  
    1.  **[評価操作]** で **[式と制約]** を選択します。  
  
    2.  **[値]** で **[成功]** を選択します。  
  
         制約値 **[成功]** は、前の SQL 実行タスクの成功を表します。  
  
    3.  **[式]** に「 `@DataReady == 0`」と入力します。  
  
    4.  **[論理 AND (すべての制約が True と評価される必要があります)** ] が選択されていない場合は、選択します。  
  
         この選択により、制約と式の両方の条件が True であることが必要になります。  
  
4.  **[SQL 実行タスク エディター]** の **[全般]** ページで、次のオプションを選択します。  
  
    1.  **[ResultSet]** で **[単一行]** を選択します。  
  
    2.  ソース データベースへの有効な接続を構成します。  
  
    3.  **[SQLSourceType]** で **[直接入力]** を選択します。  
  
    4.  **[SQLStatement]** に、次の SQL ステートメントを入力します。  
  
        ```  
        WAITFOR DELAY ?  
  
        ```  
  
5.  エディターの **[パラメーター マッピング]** ページで、DelaySeconds 文字列変数をパラメーター 0 にマップします。  
  
## <a name="handling-an-error-condition"></a>エラー状態の処理  
 必要に応じて、エラーまたはタイムアウト状態をログに記録するようにループ内に追加のコンポーネントを構成することができます。  
  
-   このコンポーネントでは、DataReady 変数の値が 1 の場合にエラー状態をログに記録できます。 この値は、選択した間隔の開始前に使用可能な変更データがないことを示します。  
  
-   このコンポーネントでは、TimeoutCeiling 変数の値に達した場合にタイムアウト状態をログに記録することもできます。 この値は、指定された回数だけループでデータがテストされたが、データがまだ使用できないことを示します。 このテストまたは同様のテストを実行しないと、パッケージが無期限に実行される可能性があります。  
  
#### <a name="to-configure-an-optional-script-task-to-log-an-error-condition"></a>エラー状態をログに記録するようにオプションのスクリプト タスクを構成するには  
  
1.  メッセージをログに書き込んでエラーまたはタイムアウトを報告する場合は、パッケージのログ記録を構成します。 詳細については、「 [SQL Server Data Tools でパッケージのログ記録を有効にする](../../integration-services/performance/integration-services-ssis-logging.md#ssdt)」を参照してください。  
  
2.  For ループ コンテナー内にスクリプト タスクを追加します。  
  
3.  変更データが準備できているかどうかを判断するためにクエリを実行する SQL 実行タスクを新しいスクリプト タスクに連結します。  
  
4.  SQL 実行タスクをスクリプト タスクに連結する優先順位制約のために、 **[優先順位制約エディター]** を開いて次のオプションを選択します。  
  
    1.  **[評価操作]** で **[式と制約]** を選択します。  
  
    2.  **[値]** で **[成功]** を選択します。  
  
         制約値 **[成功]** は、前のタスクの成功を表します。 この場合は、SQL 実行タスクの成功を表します。  
  
    3.  **[式]** に「`@DataReady == 1 || @DataReady == 5`」と入力します。  
  
    4.  **[論理 AND (すべての制約が True と評価される必要があります)** ] が選択されていない場合は、選択します。  
  
         この選択により、制約と式の両方の条件が True であることが必要になります。  
  
5.  **[スクリプト タスク エディター]** の **[スクリプト]** ページの **[ReadOnlyVariables]** で、 **[User::DataReady]** および **[User::ExtractStartTime]** を一覧から選択し、それらの値をスクリプトに使用できるようにします。  
  
     特定のシステム変数 (System::PackageName など) の情報をログに書き込む情報に含める場合は、それらの変数も選択します。  
  
6.  **[スクリプト タスク エディター]** の **[スクリプト]** ページで、 **[スクリプトの編集]** をクリックしてスクリプト開発環境を開きます。  
  
7.  Main プロシージャに、 **Dts.Log** メソッドを呼び出してエラーをログに記録するコードか、 **Dts.Events** インターフェイスのいずれかのメソッドを呼び出してイベントを発生させるコードを入力します。 `Dts.TaskResult = Dts.Results.Failure`を返すことによってエラーをパッケージに通知します。  
  
     次の例は、メッセージをログに書き込む方法を示しています。 詳細については、「 [スクリプト タスクでのログ記録](../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)」、「 [スクリプト タスクでのイベントの発生](../../integration-services/extending-packages-scripting/task/raising-events-in-the-script-task.md)」、「 [スクリプト タスクから結果を返す](../../integration-services/extending-packages-scripting/task/returning-results-from-the-script-task.md)」を参照してください。  
  
    ```  
    ' User variables.  
    Dim dataReady As Integer = _  
      CType(Dts.Variables("DataReady").Value, Integer)  
    Dim extractStartTime As Date = _  
      CType(Dts.Variables("ExtractStartTime").Value, DateTime)  
  
    ' System variables.  
    Dim packageName As String = _  
      Dts.Variables("PackageName").Value.ToString()  
    Dim executionStartTime As Date = _  
      CType(Dts.Variables("StartTime").Value, DateTime)  
  
    Dim eventMessage As New System.Text.StringBuilder()  
  
    If dataReady = 1 OrElse dataReady = 5 Then  
  
      If dataReady = 1 Then  
        eventMessage.AppendLine("Start Time Error")  
      Else  
        eventMessage.AppendLine("Timeout Error")  
      End If  
  
      With eventMessage  
        .Append("The package ")  
        .Append(packageName)  
        .Append(" started at ")  
        .Append(executionStartTime.ToString())  
        .Append(" and ended at ")  
        .AppendLine(DateTime.Now().ToString())  
        If dataReady = 1 Then  
          .Append("The specified ExtractStartTime was ")  
          .AppendLine(extractStartTime.ToString())  
        End If  
      End With  
  
      System.Windows.Forms.MessageBox.Show(eventMessage.ToString())  
  
      Dts.Log(eventMessage.ToString(), 0, Nothing)  
  
      Dts.TaskResult = Dts.Results.Failure  
  
    Else  
  
      Dts.TaskResult = Dts.Results.Success  
  
    End If  
  
    ```  
  
8.  スクリプト開発環境と **[スクリプト タスク エディター]** を閉じます。  
  
## <a name="next-step"></a>次の手順  
 変更データが準備できていると判断したら、次に変更データのクエリを準備します。  
  
 **次のトピック:** [変更データのクエリを準備する](../../integration-services/change-data-capture/prepare-to-query-for-the-change-data.md)  
  
  
