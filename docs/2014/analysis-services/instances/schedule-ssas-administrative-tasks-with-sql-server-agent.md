---
title: SQL Server エージェントで SSAS 管理タスクのスケジュール |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2d1484b3-51d9-48a0-93d2-0c3e4ed22b87
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9b24e99ac31b126888a1fa49f3ef5547a4f82dda
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079682"
---
# <a name="schedule-ssas-administrative-tasks-with-sql-server-agent"></a>SQL Server エージェントで SSAS 管理タスクのスケジュール設定を行う
  SQL Server エージェント サービスを使用すると、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の管理タスクのスケジュールを設定して、必要なときに必要な順序で実行できます。 定期タスクは、一定の周期または指定した周期で実行されるプロセスを自動化するのに役立ちます。 キューブ処理などの管理タスクは、ビジネス活動が盛んでない時間帯に実行されるようにスケジュールできます。 また、SQL Server エージェント ジョブでジョブ ステップを作成することにより、タスクの実行順序を指定できます。 たとえば、キューブを処理した後でバックアップを実行できます。  
  
 ジョブ ステップを使用すると、実行フローを制御できます。 あるジョブが失敗した場合に、残りのタスクを引き続き実行するか、実行を停止するように、SQL Server エージェントを構成できます。 また SQL Server エージェントを、ジョブ実行の成否についての通知を送信するように構成することもできます。  
  
 このトピックでは、SQL Server エージェントを使用して XMLA スクリプトを実行する方法を 2 つ紹介します。 最初の例では、単一のディメンションの処理をスケジュール設定する方法を示します。 2 番目の例では、スケジュールに従って実行される単一のスクリプトに複数の処理タスクを組み合わせる方法を示します。 このチュートリアルを完了するには、次の条件を満たす必要があります。  
  
## <a name="prerequisites"></a>前提条件  
 SQL Server エージェント サービスがインストールされている必要があります。  
  
 既定では、ジョブはサービス アカウントで実行されます。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、SQL Server エージェントの既定のアカウントは NT service \sqlagent$\<instancename > です。 バックアップまたは処理タスクを実行するには、このアカウントが Analysis Services インスタンスのシステム管理者である必要があります。 詳細については、次を参照してください。[サーバーの管理者アクセス許可の付与&#40;Analysis Services&#41;](grant-server-admin-rights-to-an-analysis-services-instance.md)します。  
  
 操作対象のテスト データベースも必要です。 AdventureWorks 多次元サンプル データベースまたはプロジェクトを Analysis Services 多次元チュートリアルから配置して、このチュートリアルで使用できます。 詳細については、「 [Analysis Services 多次元モデリング チュートリアル用のサンプル データおよびプロジェクトのインストール](../install-sample-data-and-projects.md)」を参照してください。  
  
## <a name="example-1-processing-a-dimension-in-a-scheduled-task"></a>例 1 : スケジュールされたタスクでのディメンションの処理  
 この例では、ディメンションを処理するジョブを作成し、スケジュール設定を行う方法を示します。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の定期タスクは、SQL Server エージェント ジョブに組み込まれる XMLA スクリプトです。 このジョブは、指定した時刻と頻度で実行されるようにスケジュールされます。 SQL Server エージェントは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の一部なので、管理タスクの作成およびスケジュール設定には、データベース エンジンおよび [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] を使用します。  
  
###  <a name="bkmk_CreateScript"></a> SQL Server エージェント ジョブでディメンションを処理するスクリプトを作成する  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]に接続します。 データベース フォルダーを開き、ディメンションを検索します。 ディメンションを右クリックし、 **[処理]** をクリックします。  
  
2.  **[ディメンションの処理]** ダイアログ ボックスにある **[オブジェクト一覧]** の **[処理オプション]** 列で、この列のオプションが **[完全処理]** であることを確認します。 別のオプションが設定されている場合、 **[処理オプション]** 列のオプションをクリックし、表示される一覧から **[完全処理]** を選択します。  
  
3.  **[スクリプト]** をクリックします。  
  
     この手順により、ディメンションを処理する XMLA スクリプトを含む **XML クエリ** ウィンドウが表示されます。  
  
4.  **[ディメンションの処理]** ダイアログ ボックスで、 **[キャンセル]** をクリックしてダイアログ ボックスを閉じます。  
  
5.  **XMLA クエリ** ウィンドウで、強調表示された XMLA スクリプトを右クリックし、 **[コピー]** をクリックします。  
  
     この手順により、XMLA スクリプトが Windows クリップボードにコピーされます。 XMLA スクリプトをクリップボードに残しておくか、メモ帳または別のテキスト エディターに貼り付けます。 XMLA スクリプトの例を次に示します。  
  
    ```  
    <Batch xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
     <Parallel>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <DimensionID>Dim Account</DimensionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
     </Parallel>  
    </Batch>  
    ```  
  
###  <a name="bkmk_ProcessJob"></a> ディメンション処理ジョブを作成してスケジュールを設定する  
  
1.  データベース エンジンのインスタンスに接続し、オブジェクト エクスプローラーを開きます。  
  
2.  **[SQL Server エージェント]** を展開します。  
  
3.  **[ジョブ]** を右クリックし、 **[新しいジョブ]** をクリックします。  
  
4.  **[新しいジョブ]** ダイアログ ボックスで、 **[名前]** ボックスにジョブ名を入力します。  
  
5.  **[ページの選択]** で、 **[ステップ]** を選択し、 **[新規作成]** をクリックします。  
  
6.  **[新しいジョブ ステップ]** ダイアログ ボックスで、 **[ステップ名]** にステップ名を入力します。  
  
7.  **[サーバー]** で、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の既定のインスタンスの **localhost** と、名前付きインスタンスの **localhost\\** \<*インスタンス名*> を入力します。  
  
     リモート コンピューターからジョブを実行する場合は、ジョブが実行されるサーバー名およびインスタンス名を使用します。 形式を使用して\<*サーバー名*> 既定のインスタンスと\<*サーバー名*>\\<*インスタンス名前*> 名前付きインスタンス。  
  
8.  **[種類]** で、 **[SQL Server Analysis Services コマンド]** を選択します。  
  
9. **[コマンド]** で、右クリックして **[貼り付け]** を選択します。 前の手順で生成した XMLA スクリプトがコマンド ウィンドウに表示されます。  
  
10. **[OK]** をクリックします。  
  
11. **[ページの選択]** で、 **[スケジュール]** をクリックし、 **[新規作成]** をクリックします。  
  
12. **[新しいジョブ スケジュール]** ダイアログ ボックスで、 **[名前]** ボックスにスケジュール名を入力し、 **[OK]** をクリックします。  
  
     この手順により、日曜日午前 12 時 00 分のスケジュールが作成されます。 次の手順では、ジョブを手動で実行する方法を示します。 ジョブを監視しているときに、ジョブを実行するスケジュールを指定することもできます。  
  
13. **[新しいジョブ]** ダイアログ ボックスで、 **[OK]** をクリックします。  
  
14. **オブジェクト エクスプローラー**で、 **[ジョブ]** を展開し、作成したジョブを右クリックして、 **[ステップでジョブを開始]** をクリックします。  
  
     このジョブにはステップが 1 つしかないため、すぐにジョブが実行されます。 ジョブに複数のステップが含まれている場合、ジョブを開始するステップを選択できます。  
  
15. ジョブが完了したら、 **[閉じる]** をクリックします。  
  
## <a name="example-2-batch-processing-a-dimension-and-a-partition-in-a-scheduled-task"></a>例 2:ディメンションと、スケジュールされたタスクでのパーティションをバッチ処理  
 この例の手順では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のデータベース ディメンションをバッチ処理するジョブを作成してスケジュールを設定する方法と、そのディメンションに集計で依存するキューブ パーティションを処理する方法を示します。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトのバッチ処理の詳細については、「[バッチ処理 (Analysis Services)](../multidimensional-models/batch-processing-analysis-services.md)」を参照してください。  
  
###  <a name="bkmk_BatchProcess"></a> SQL Server エージェント ジョブでディメンションとパーティションをバッチ処理するスクリプトを作成する  
  
1.  同じデータベースを使用して、 **[ディメンション]** を展開し、 **[Customer]** ディメンションを右クリックして **[処理]** をクリックします。  
  
2.  **[ディメンションの処理]** ダイアログ ボックスにある **[オブジェクト一覧]** の **[処理オプション]** 列で、この列のオプションが **[完全処理]** であることを確認します。  
  
3.  **[スクリプト]** をクリックします。  
  
     この手順により、ディメンションを処理する XMLA スクリプトを含む **XML クエリ** ウィンドウが表示されます。  
  
4.  **[ディメンションの処理]** ダイアログ ボックスで、 **[キャンセル]** をクリックしてダイアログ ボックスを閉じます。  
  
5.  **[キューブ]** 、 **[Adventure Works]** 、 **[メジャー グループ]** 、 **[インターネット販売]** 、 **[パーティション]** の順に展開し、一覧の最後のパーティションを右クリックして **[処理]** をクリックします。  
  
6.  **[パーティションの処理]** ダイアログ ボックスにある **[オブジェクト一覧]** の **[処理オプション]** 列で、この列のオプションが **[完全処理]** であることを確認します。  
  
7.  **[スクリプト]** をクリックします。  
  
     この手順により、パーティションを処理する XMLA スクリプトを含む 2 番目の **XML クエリ** ウィンドウが表示されます。  
  
8.  **[パーティションの処理]** ダイアログ ボックスで、 **[キャンセル]** をクリックしてエディターを閉じます。  
  
     この時点で、2 つのスクリプトをマージし、ディメンションが最初に処理されるようにする必要があります。  
  
    > [!WARNING]  
    >  パーティションが最初に処理された場合、後続のディメンション処理により、パーティションが未処理になる可能性があります。 その場合、パーティションを処理済みの状態にするには、2 番目の処理が必要です。  
  
9. パーティションを処理する XMLA スクリプトを含む **XMLA クエリ** ウィンドウで、 `Batch` タグおよび `Parallel` タグの内側にあるコードを強調表示し、強調表示されたスクリプトを右クリックして **[コピー]** をクリックします。  
  
    ```  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID> Adventure Works DW Multidimensional</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID> Internet_Sales_2004</PartitionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
    ```  
  
10. ディメンションを処理する XMLA スクリプトを含む **XMLA クエリ** ウィンドウを開きます。 スクリプト内で `</Process>` タグの左まで右クリックし、 **[貼り付け]** をクリックします。  
  
     次の例は、変更後の XMLA スクリプトを示しています。  
  
    ```  
    <Batch xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
     <Parallel>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <DimensionID>Dim Customer</DimensionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID>Internet_Sales_2004</PartitionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
     </Parallel>  
    </Batch>  
    ```  
  
11. 変更後の XMLA スクリプトを強調表示し、強調表示されたスクリプトを右クリックして **[コピー]** をクリックします。  
  
12. この手順により、XMLA スクリプトが Windows クリップボードにコピーされます。 XMLA スクリプトをクリップボードに残しておくか、ファイルに保存するか、メモ帳または別のテキスト エディターに貼り付けます。  
  
###  <a name="bkmk_Scheduling"></a> バッチ処理ジョブを作成してスケジュールを設定する  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続し、オブジェクト エクスプローラーを開きます。  
  
2.  **[SQL Server エージェント]** を展開します。 サービスが実行されていない場合は開始します。  
  
3.  **[ジョブ]** を右クリックし、 **[新しいジョブ]** をクリックします。  
  
4.  **[新しいジョブ]** ダイアログ ボックスで、 **[名前]** ボックスにジョブ名を入力します。  
  
5.  **[ステップ]** で、 **[新規作成]** をクリックします。  
  
6.  **[新しいジョブ ステップ]** ダイアログ ボックスで、 **[ステップ名]** にステップ名を入力します。  
  
7.  **[種類]** で、 **[SQL Server Analysis Services コマンド]** を選択します。  
  
8.  **[実行するアカウント名]** で、 **[SQL Server エージェント サービスのアカウント]** を選択します。 「前提条件」で説明したように、このアカウントには Analysis Services に対する管理権限が必要です。  
  
9. **[サーバー]** で、Analysis Services インスタンスのサーバー名を指定します。  
  
10. **[コマンド]** で、右クリックして **[貼り付け]** を選択します。  
  
11. **[OK]** をクリックします。  
  
12. **[スケジュール]** ページで **[新規作成]** をクリックします。  
  
13. **[新しいジョブ スケジュール]** ダイアログ ボックスで、 **[名前]** ボックスにスケジュール名を入力し、 **[OK]** をクリックします。  
  
     この手順により、日曜日午前 12 時 00 分のスケジュールが作成されます。 次の手順では、ジョブを手動で実行する方法を示します。 ジョブを監視しているときに、ジョブを実行するスケジュールを選択することもできます。  
  
14. **[OK]** をクリックしてダイアログ ボックスを閉じます。  
  
15. **オブジェクト エクスプローラー**で、 **[ジョブ]** を展開し、作成したジョブを右クリックして、 **[ステップでジョブを開始]** をクリックします。  
  
     このジョブにはステップが 1 つしかないため、すぐにジョブが実行されます。 ジョブに複数のステップが含まれている場合、ジョブを開始するステップを選択できます。  
  
16. ジョブが完了したら、 **[閉じる]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [処理オプションと設定 (Analysis Services)](../multidimensional-models/processing-options-and-settings-analysis-services.md)   
 [Analysis Services の管理タスクのスクリプト作成](../script-administrative-tasks-in-analysis-services.md)  
  
  
