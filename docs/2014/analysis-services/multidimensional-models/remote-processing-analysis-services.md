---
title: リモート処理 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d58bcb3c-0b3f-4ab0-81eb-4fdcc86153af
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b383621408cc84a65e5f9c5adb711dd9f047be64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073213"
---
# <a name="remote-processing-analysis-services"></a>リモート処理 (Analysis Services)
  あるコンピューターから発行された処理要求を同じネットワーク上の別のコンピューターで実行する場合、スケジュールされた処理や自動処理をリモートの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスで実行できます。  
  
## <a name="prerequisites"></a>前提条件  
  
-   各コンピューターでそれぞれ異なるバージョンの SQL Server を実行している場合、クライアント ライブラリはモデルを処理する [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスのバージョンと一致する必要があります。 たとえば、 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] インスタンスで処理を行う場合、要求の発行元のコンピューターには [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]に対応するクライアント ライブラリが必要です。 「 [Analysis Services 接続に使用するデータ プロバイダー](../instances/data-providers-used-for-analysis-services-connections.md)」をご覧ください。  
  
-   リモート サーバーでは、 **[このコンピューターへのリモート接続を許可する]** が有効になっている必要があり、処理要求を発行するアカウントは許可されたユーザーとして一覧に表示されている必要があります。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]への着信接続を許可するように Windows ファイアウォール ルールを構成する必要があります。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] を使用してリモートの [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]インスタンスに接続できることを確認します。 「 [Analysis Services のアクセスを許可するための Windows ファイアウォールの構成](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)」をご覧ください。  
  
-   リモート処理を試みる前に、既存のローカル処理エラーを解決します。 処理要求がローカルの場合、外部リレーショナル データ ソースからデータを正常に取得できることを確認します。 データの取得に使用する資格情報を指定する手順については、「[権限借用オプションの設定 &#40;SSAS - 多次元&#41;](set-impersonation-options-ssas-multidimensional.md)」をご覧ください。  
  
## <a name="on-demand-remote-processing"></a>オンデマンドのリモート処理  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の管理者権限を持つユーザー アカウントまたはアプリケーション アカウントからの処理要求を受け入れます。 管理者は、リモート インスタンスに接続し、リモート接続でデータベースを手動で処理できることを確認します。  
  
1.  処理のスケジュールを設定する際に使用するコンピューターで、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を起動し、リモートの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスに接続します。  
  
2.  データベースを右クリックして **[処理]** を選択し、 **[スクリプト]** をポイントして **[スクリプト操作を新規クエリ ウィンドウに保存]** を選択します。 処理の呼び出しに使用するコマンドがクエリ ウィンドウに表示されます。  
  
3.  **[OK]** をクリックして、処理を開始します。  
  
     このタスクが正常に完了すると、スケジュールされたジョブに組み込むことができる XMLA クエリが提供されます。 また、接続の問題が発生していないことも確認されます。  
  
## <a name="schedule-remote-processing-using-sql-server-agent-service"></a>SQL Server エージェント サービスを使用したリモート処理のスケジュール設定  
 既定では、SQL Server エージェント サービスは、コンピューター アカウントを使用して作成されたネットワーク接続によって、仮想アカウントで実行されます。 リモートの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスに対する管理権限をコンピューター アカウントに付与しないようにするには、最小特権のドメイン ユーザー アカウントとして実行するように SQL Server エージェント サービス アカウントを変更する必要があります。  
  
 必要なすべての権限を必ず付与してください。たとえば、サービスを提供するデータベース エンジン インスタンスに対する **sysadmin** 権限をアカウントに付与します。  
  
 次のリンクを使用して権限を設定します。  
  
-   [SQL Server エージェントの構成](../../ssms/agent/configure-sql-server-agent.md)  
  
-   [sysadmin](../../ssms/agent/sql-server-agent.md#Components) 権限を付与することができない場合、 **SQL Server エージェントのコンポーネント** は代替の固定サーバー ロールを提示します。  
  
 アカウントの権限を構成したら、以下の手順を続行します。  
  
#### <a name="grant-the-sql-server-agent-account-administrator-permission-on-ssas"></a>SSAS に対する管理者権限を SQL Server エージェント アカウントに付与する  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]を使用して、リモートの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスに接続します。  
  
2.  サーバー名を右クリックして **[プロパティ]** をクリックし、 **[セキュリティ]** をクリックします。  
  
3.  **[追加]** をクリックして、SQL Server エージェント アカウントを追加します。  
  
#### <a name="create-the-job"></a>ジョブの作成  
  
1.  Management Studio で、ローカルのデータベース エンジン インスタンスに接続します。 SQL Server エージェントは、オブジェクト エクスプローラー内の最後のアイテムです。 必要に応じて、サービスを開始します。  
  
2.  **[ジョブ]** を右クリックして **[新しいジョブ]** をクリックし、名前を入力します。  
  
3.  [ステップ] で **[新規作成]** をクリックし、名前を入力します。  
  
4.  [種類] で **[SQL Server Analysis Services コマンド]** を選択します。  
  
5.  [サーバー] で、リモートの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスの名前を入力します。  
  
6.  [コマンド] でデータベースを処理する XMLA コマンドを貼り付けます。 これは、オンデマンドのリモート処理の検証手順で生成した XMLA スクリプトです。 **[OK]** をクリックしてジョブを保存します。  
  
#### <a name="start-sql-server-profiler"></a>SQL Server Profiler の起動  
  
1.  リモート コンピューターで SQL Server Profiler を起動します。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスに接続し、 **[実行]** をクリックして、既定のイベントを使用してトレースを開始します。  
  
     SQL Server Profiler を使用して、発生した処理イベントを監視します。  
  
2.  必要に応じて、データベース内のファイルまたはテーブルにトレースを送信するようにトレースのプロパティを設定することもできます。  
  
#### <a name="run-the-job"></a>ジョブの実行  
  
1.  ジョブの実行に使用するコンピューターで、ジョブが基本操作を実行できることを確認します。 オブジェクト エクスプローラーで、SQL Server エージェントの下の **[ジョブ]** を展開し、作成したジョブを右クリックして **[ステップでジョブを開始]** をクリックします。 ジョブがすぐに開始されます。 SQL Server Profiler で進行状況を監視できます。  
  
2.  最後の手順として、ジョブを管理するために必要な警告や通知を追加して、定義したスケジュールで実行するようにジョブを変更します。 また、処理スクリプトを調整したり、ジョブ内に複数のステップを作成してオブジェクトを個別に処理したりできます。  
  
## <a name="see-also"></a>参照  
 [sysadmin](../../ssms/agent/sql-server-agent.md#Components)   
 [SQL Server エージェントで SSAS 管理タスクのスケジュール設定を行う](../instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)   
 [バッチ処理 &#40;Analysis Services&#41;](batch-processing-analysis-services.md)   
 [多次元モデル オブジェクトの処理](processing-a-multidimensional-model-analysis-services.md)   
 [オブジェクトの処理 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)  
  
  
