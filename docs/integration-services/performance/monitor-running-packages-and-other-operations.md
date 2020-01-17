---
title: 実行中のパッケージとその他の操作の監視 | Microsoft Docs
ms.custom: supportability
ms.date: 06/04/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.isoperations.executions.f1
- sql13.ssis.ssms.isoperations.general.f1
ms.assetid: cbbcd79f-ab9b-46ec-84cb-4821c1d16b99
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d7fd62f4f2f82e6dcc3921db7099b4f052db27b3
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295799"
---
# <a name="monitor-running-packages-and-other-operations"></a>実行中のパッケージとその他の操作の監視

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  次の 1 つ以上のツールを使用して、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの実行、プロジェクトの検証、およびその他の操作を監視できます。 データ タップなどの特定のツールは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置されたプロジェクトに対してのみ使用できます。  
  
-   ログ  
  
     詳細については、「[Integration Services (SSIS) のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)」をご覧ください。  
  
-   [レポート]  
  
     詳細については、「 [Reports for the Integration Services Server](#reports)」を参照してください。  
  
-   ビュー  
  
     詳細については、「[ビュー &#40Integration Services カタログ&#41;](../../integration-services/system-views/views-integration-services-catalog.md)」を参照してください。  
  
-   パフォーマンス カウンター  
  
     これらのパフォーマンス カウンターの詳細については、「 [パフォーマンス カウンター](../../integration-services/performance/performance-counters.md)」を参照してください。  
  
-   データ タップ  

> [!NOTE]
> この記事では、実行中の SSIS パッケージを監視する方法 (全般) と、オンプレミスで実行中のパッケージを監視する方法について説明します。 Azure SQL Database で SSIS を実行し、監視することもできます。 詳細については、「[Lift and shift SQL Server Integration Services workloads to the cloud](../lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)」 (SQL Server Integration Services ワークロードをクラウドにリフト アンド シフトする) を参照してください。
>
> Linux でも SSIS パッケージを実行できますが、Linux では監視ツールが提供されません。 詳しくは、「[SSIS で Linux 上のデータの抽出、変換、読み込みを行う](../../linux/sql-server-linux-migrate-ssis.md)」 をご覧ください。

## <a name="operation-types"></a>操作の種類  
 **サーバー上の** SSISDB [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログでは、さまざまな種類の操作が監視されます。 各操作には、複数のメッセージを関連付けることができます。 各メッセージは、複数の種類のうちの 1 つに分類できます。 たとえば、メッセージの種類は、情報、警告、またはエラーとなります。 メッセージの種類の一覧については、Transact-SQL の [catalog.operation_messages &#40;SSISDB Database&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md) ビューに関するドキュメントを参照してください。 操作の種類の一覧については、「[catalog.operations &#40;SSISDB Database&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)」を参照してください。  
  
 9 つの状態の種類を使用して、操作の状態を示します。 状態の種類の一覧については、「[catalog.operations &#40;SSISDB Database&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)」を参照してください。  

## <a name="active_ops"></a> [アクティブな操作] ダイアログ ボックス
  配置、検証、パッケージの実行など、 **サーバー上で現在実行中の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 操作の状態を表示するには、** [アクティブな操作][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ダイアログ ボックスを使用します。 このデータは、SSISDB カタログに格納されます。  
  
 関連 [!INCLUDE[tsql](../../includes/tsql-md.md)] ビューの詳細については、「[catalog.operations (SSISDB データベース)](../../integration-services/system-views/catalog-operations-ssisdb-database.md)」、「[catalog.validations (SSISDB データベース)](../../integration-services/system-views/catalog-validations-ssisdb-database.md)」、「[catalog.executions (SSISDB データベース)](../../integration-services/system-views/catalog-executions-ssisdb-database.md)」を参照してください。  
  
###  <a name="open_dialog"></a> [アクティブな操作] ダイアログ ボックスを開く  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]を開きます。  
  
2.  Microsoft SQL Server データベース エンジンに接続します。  
  
3.  オブジェクト エクスプローラーで、 **[Integration Services]** ノードを展開します。 **[SSISDB]** を右クリックし、 **[アクティブな操作]** をクリックします。  
  
### <a name="configure-the-options"></a>オプションの構成  
  
 **Type**  
 操作の種類を指定します。 **[種類]** フィールドに指定できる値、および Transact-SQL の **catalog.operations** ビューに含まれる operations_type 列の対応する値を次に示します。  
  
|||  
|-|-|  
|Integration Services の初期化|1|  
|操作のクリーンアップ (SQL エージェント ジョブ)|2|  
|プロジェクト バージョンのクリーンアップ (SQL エージェント ジョブ)|3|  
|プロジェクトの配置|101|  
|プロジェクトの復元|106|  
|パッケージ実行の作成および開始|200|  
|操作の停止 (検証または実行の停止)|202|  
|プロジェクトの検証|300|  
|パッケージの検証|301|  
|カタログの構成|1000|  
  
 **[停止]**  
 現在実行中の操作を停止する場合にクリックします。  

## <a name="viewing-and-stopping-packages-running-on-the-integration-services-server"></a>Integration Services サーバーで実行中のパッケージの表示と停止
  **SSISDB** データベースでは、ユーザーに表示されない内部テーブルに実行履歴を格納します。 ただし、必要な情報は、パブリック ビューに対してクエリを実行することで公開されます。 また、パッケージに関連した一般的なタスクを実行するために呼び出すことができるストアド プロシージャも用意されています。  
  
 通常、サーバー上の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] オブジェクトは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で管理します。 また、データベース ビューに対してクエリを実行し、ストアド プロシージャを直接呼び出すことや、マネージド API を呼び出すカスタム コードを記述することもできます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] およびマネージド API では、ビューに対してクエリを実行し、多くのタスクを実行するストアド プロシージャを呼び出します。 たとえば、サーバーで現在実行中の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの一覧を表示し、必要に応じてパッケージの停止を要求できます。  
  
### <a name="viewing-the-list-of-running-packages"></a>実行中のパッケージの一覧の表示  
 **[アクティブな操作]** ダイアログ ボックスでは、サーバーで現在実行中のパッケージの一覧を表示できます。 詳しくは、「 [Active Operations Dialog Box](#active_ops)」をご覧ください。  
  
 実行中のパッケージの一覧を表示するその他の方法については、次のトピックをご覧ください。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] アクセス  
 サーバーで実行中のパッケージの一覧を表示するには、ステータスが 2 のパッケージに対してビュー [catalog.executions (SSISDB データベース)](../../integration-services/system-views/catalog-executions-ssisdb-database.md) をクエリします。  
  
 マネージド API を使用したプログラムによるアクセス  
 <xref:Microsoft.SqlServer.Management.IntegrationServices> 名前空間とそのクラスのトピックをご覧ください。  
  
### <a name="stopping-a-running-package"></a>実行中のパッケージの停止  
 **[アクティブな操作]** ダイアログ ボックスでは、実行中のパッケージを停止するよう要求できます。 詳しくは、「 [Active Operations Dialog Box](#active_ops)」をご覧ください。  
  
 実行中のパッケージを停止するその他の方法については、次のトピックをご覧ください。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] アクセス  
 サーバーで実行中のパッケージを停止するには、ストアド プロシージャ [catalog.stop_operation (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md) を呼び出します。  
  
 マネージド API を使用したプログラムによるアクセス  
 <xref:Microsoft.SqlServer.Management.IntegrationServices> 名前空間とそのクラスのトピックをご覧ください。  
  
### <a name="viewing-the-history-of-packages-that-have-run"></a>実行したパッケージの履歴の表示  
 実行したパッケージの履歴を [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]で確認するには、 **[すべての実行]** レポートを使用します。 **[すべての実行]** レポートとその他の標準レポートの詳細については、「[Integration Services サーバーのレポート](#reports)」を参照してください。  
  
 実行中のパッケージの履歴を表示するその他の方法については、次のトピックをご覧ください。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] アクセス  
 実行したパッケージに関する情報を表示するには、ビュー [catalog.executions (SSISDB データベース)](../../integration-services/system-views/catalog-executions-ssisdb-database.md) をクエリします。  
  
 マネージド API を使用したプログラムによるアクセス  
 <xref:Microsoft.SqlServer.Management.IntegrationServices> 名前空間とそのクラスのトピックをご覧ください。  

## <a name="reports"></a> Reports for the Integration Services Server
  現在のリリースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] サーバーに配置された [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトの監視に役立つ標準レポートを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で使用できるようになりました。 これらのレポートは、パッケージの状態と履歴を確認したり、必要に応じてパッケージ実行の失敗の原因を特定したりするのに役立ちます。  
  
 各レポート ページの先頭にある戻るアイコンをクリックすると、前に表示されていたページに戻ります。最新の情報に更新アイコンをクリックすると、ページに表示されている情報が更新されます。印刷アイコンをクリックすると、現在のページが印刷されます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーにパッケージを配置する方法については、「[Integration Services (SSIS) プロジェクトとパッケージの配置](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)」を参照してください。  
  
### <a name="integration-services-dashboard"></a>Integration Services ダッシュボード  
 " **Integration Services ダッシュボード** " レポートは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス上で実行されたすべてのパッケージに関する概要を示します。 ダッシュ ボードでは、サーバーで実行されたそれぞれのパッケージに対し、"ズーム イン" 機能を使用して、発生した可能性のあるパッケージ実行エラーの特定の詳細を検索することができます。  
  
 このレポートには、次の情報のセクションが表示されます。  
  
|セクション|[説明]|  
|-------------|-----------------|  
|**実行情報**|過去 24 時間のさまざまな状態 (失敗、実行中、成功、その他) の実行の数を示します。|  
|**Package Information**|過去 24 時間に実行されたパッケージの合計数を示します。|  
|**接続情報**|過去 24 時間に失敗した実行で使用された接続を示します。|  
|**パッケージの詳細情報**|過去 24 時間に発生した、完了した実行の詳細を示します。 たとえば、このセクションには、失敗した実行の数、実行の総数、実行時間 (秒単位)、および過去 3 か月における実行の平均時間が表示されます。<br /><br /> **[概要]** 、 **[すべてのメッセージ]** 、および **[実行のパフォーマンス]** をクリックすることで、パッケージの追加情報を表示できます。<br /><br /> **"実行のパフォーマンス"** レポートは、最後の実行インスタンスの持続時間、開始時刻、終了時刻、および適用された環境を示します。<br /><br /> **"実行のパフォーマンス"** レポートに含まれるグラフと、関連付けられたテーブルは、パッケージの過去 10 件の成功した実行の持続時間を示します。 テーブルは、3 か月間の平均実行時間も示します。 パッケージのこれらの 10 件の成功した実行には、異なる環境と異なるリテラル値が実行時に適用されている場合があります。<br /><br /> 最後に、 **"実行のパフォーマンス"** レポートは、パッケージ データ フロー コンポーネントのアクティブな時間と合計時間を示します。 アクティブな時間は、コンポーネントがすべてのフェーズで実行に費やした合計時間を指し、合計時間は、1 つのコンポーネントで経過した合計時間を示します。 このパッケージ コンポーネントの情報は、最後のパッケージの実行のログ レベルが [パフォーマンス] または [詳細] に設定されていた場合のみ、レポートに表示されます。<br /><br /> **"概要"** レポートは、パッケージ タスクの状態を示します。 **"メッセージ"** レポートは、パッケージとタスクのイベント メッセージとエラー メッセージを示し、開始時刻、終了時刻、書き込まれた行の数などを報告します。<br /><br /> **"概要"** レポートの **[メッセージの表示]** をクリックして、 **"メッセージ"** レポートに移動することもできます。 **"メッセージ"** レポートの **[概要の表示]** をクリックして、 **"概要"** レポートに移動することもできます。|  
  
 **[フィルター]** をクリックし、 **[フィルターの設定]** ダイアログで条件を選択することにより、各ページに表示されるテーブルにフィルターを適用できます。 使用できるフィルター条件は、表示されるデータによって異なります。 **[フィルターの設定]** ダイアログの並べ替えアイコンをクリックすることで、レポートの並べ替え順序を変更できます。  
  
### <a name="all-executions-report"></a>"すべての実行" レポート  
 **"すべての実行"** レポートには、サーバーで実行されたすべての [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の実行に関する概要が表示されます。 サンプル パッケージが複数回実行されることがあります。 **"Integration Services ダッシュボード"** レポートとは異なり、 **"すべての実行"** レポートは、指定した日付範囲中に開始された実行を示すように構成できます。 複数の日、月、または年の日付を指定できます。  
  
 このレポートには、次の情報のセクションが表示されます。  
  
|セクション|[説明]|  
|-------------|-----------------|  
|Assert|レポートに適用される現在のフィルターを示します (開始時間範囲など)。|  
|実行情報|各パッケージの実行の開始時刻、終了時刻、および持続時間を示します。パッケージの実行で使用されたパラメーター値 (パッケージ実行タスクで子パッケージに渡された値など) の一覧を表示できます。 パラメーターの一覧を表示するには、[概要] をクリックします。|  
  
 パッケージ実行タスクを使用して子パッケージで値を使用できるようにする方法の詳細については、「 [パッケージ実行タスク](../../integration-services/control-flow/execute-package-task.md)」を参照してください。  
  
 パラメーターの詳細については、「 [Integration Services (SSIS) Package and Project Parameters](../../integration-services/integration-services-ssis-package-and-project-parameters.md)」(Integration Services (SSIS) パッケージとプロジェクト パラメーター) を参照してください。  
  
### <a name="all-connections"></a>すべての接続  
 **"すべての接続"** レポートは、失敗した接続と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで発生した実行に関する次の情報を提供します。  
  
 このレポートには、次の情報のセクションが表示されます。  
  
|セクション|[説明]|  
|-------------|-----------------|  
|Assert|レポートに適用される現在のフィルター (指定した文字列を使用し、 **[前回失敗した日時]** 範囲にある接続など) を示します。<br /><br /> 特定の日付範囲中に発生した接続エラーのみを表示するには、 **[前回失敗した日時]** を設定します。 範囲には、複数の日、月、または年を指定できます。|  
|詳細|接続文字列、接続中に失敗した実行の回数、および最後に失敗した日付を示します。|  
  
### <a name="all-operations-report"></a>"すべての操作" レポート  
 **"すべての操作" レポート** には、パッケージの配置、検証、実行、およびその他の管理操作を含む、サーバー上で実行されたあらゆる [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 操作の概要が表示されます。 Integration Services ダッシュボードと同様に、テーブルにフィルターを適用して、表示される情報を絞り込むことができます。  
  
### <a name="all-validations-report"></a>"すべての検証" レポート  
 **"すべての検証" レポート** には、サーバーで実行されたすべての [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の検証の概要が表示されます。 この概要には、状態、開始時刻、終了時刻など、各検証の情報が表示されます。 各概要エントリには、検証中に生成されたメッセージへのリンクが含まれます。 Integration Services ダッシュボードと同様に、テーブルにフィルターを適用して、表示される情報を絞り込むことができます。  
  
### <a name="custom-reports"></a>カスタム レポート  
 **の** [Integration Services カタログ] **ノードの下の** [SSISDB] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]カタログ ノードに、カスタム レポート (.rdl ファイル) を追加できます。 レポートを追加する前に、ソース テーブルなど、参照するオブジェクトを完全修飾するための 3 つの要素で構成される名前付け規則を使用していることを確認します。 そうでない場合、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でエラーが表示されます。 名前付け規則は、\<データベース>.\<所有者>.\<オブジェクト> です。 たとえば、SSISDB.internal.executions などです。  
  
> [!NOTE]  
>  **[データベース]** ノードの下の **[SSISDB]** ノードにカスタム レポートを追加した場合、SSISDB プレフィックスは必要ありません。  
  
 カスタム レポートの作成および追加方法については、「 [Add a Custom Report to Management Studio](../../ssms/object/add-a-custom-report-to-management-studio.md)」(Management Studio へのカスタム レポートの追加) を参照してください。  

## <a name="view-reports-for-the-integration-services-server"></a>Integration Services サーバーのレポートの表示
  現在のリリースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] サーバーに配置された [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトの監視に役立つ標準レポートを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で使用できるようになりました。  レポートの詳細については、「 [Integration Services サーバーのレポート](#reports)」をご覧ください。  
  
### <a name="to-view-reports-for-the-integration-services-server"></a>Integration Services サーバーのレポートを表示するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のオブジェクト エクスプローラーで、 **[Integration Services カタログ]** ノードを展開します。  
  
2.  **[SSISDB]** を右クリックし、 **[レポート]** をクリックして、 **[標準レポート]** をクリックします。  
  
3.  レポートを表示するには、以下のいずれかをクリックします。  
  
    -   **Integration Services ダッシュボード**  
  
    -   **すべての実行**  
  
    -   **すべての検証**  
  
    -   **すべての操作**  
  
    -   **すべての接続**  

## <a name="see-also"></a>参照  
 [プロジェクトとパッケージの実行](../packages/deploy-integration-services-ssis-projects-and-packages.md)   
 [パッケージ実行のレポートのトラブルシューティング](../troubleshooting/troubleshooting-reports-for-package-execution.md)  
