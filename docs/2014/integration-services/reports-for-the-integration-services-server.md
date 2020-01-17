---
title: Integration Services サーバーのレポート |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.SUMMARY.RENDER.CUSTOM.REPORT.F1
ms.assetid: e976e7c0-a805-4370-bf73-356c8e3becfb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: aa53c012649f983953b61a21901763b9bdd02c8b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056440"
---
# <a name="reports-for-the-integration-services-server"></a>Integration Services サーバーのレポート
  現在のリリースの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]では、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] サーバーに配置された [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトの監視に役立つ標準レポートを [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] で使用できるようになりました。 これらのレポートは、パッケージの状態と履歴を確認したり、必要に応じてパッケージ実行の失敗の原因を特定したりするのに役立ちます。  
  
 各レポート ページの先頭にある戻るアイコンをクリックすると、前に表示されていたページに戻ります。最新の情報に更新アイコンをクリックすると、ページに表示されている情報が更新されます。印刷アイコンをクリックすると、現在のページが印刷されます。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーにパッケージを配置する方法については、「 [Integration Services サーバーへのプロジェクトの配置](../../2014/integration-services/deploy-projects-to-integration-services-server.md)」を参照してください。  
  
## <a name="integration-services-dashboard"></a>Integration Services ダッシュボード  
 " **Integration Services ダッシュボード** " レポートは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンス上で実行されたすべてのパッケージに関する概要を示します。 ダッシュ ボードでは、サーバーで実行されたそれぞれのパッケージに対し、"ズーム イン" 機能を使用して、発生した可能性のあるパッケージ実行エラーの特定の詳細を検索することができます。  
  
 このレポートには、次の情報のセクションが表示されます。  
  
|セクション|説明|  
|-------------|-----------------|  
|**実行情報**|過去 24 時間のさまざまな状態 (失敗、実行中、成功、その他) の実行の数を示します。|  
|**Package Information**|過去 24 時間に実行されたパッケージの合計数を示します。|  
|**接続情報**|過去 24 時間に失敗した実行で使用された接続を示します。|  
|**パッケージの詳細情報**|過去 24 時間に発生した、完了した実行の詳細を示します。 たとえば、このセクションには、失敗した実行の数、実行の総数、実行時間 (秒単位)、および過去 3 か月における実行の平均時間が表示されます。<br /><br /> **[概要]** 、 **[すべてのメッセージ]** 、および **[実行のパフォーマンス]** をクリックすることで、パッケージの追加情報を表示できます。<br /><br /> **"実行のパフォーマンス"** レポートは、最後の実行インスタンスの持続時間、開始時刻、終了時刻、および適用された環境を示します。<br /><br /> **"実行のパフォーマンス"** レポートに含まれるグラフと、関連付けられたテーブルは、パッケージの過去 10 件の成功した実行の持続時間を示します。 テーブルは、3 か月間の平均実行時間も示します。 パッケージのこれらの 10 件の成功した実行には、異なる環境と異なるリテラル値が実行時に適用されている場合があります。<br /><br /> 最後に、 **"実行のパフォーマンス"** レポートは、パッケージ データ フロー コンポーネントのアクティブな時間と合計時間を示します。 アクティブな時間は、コンポーネントがすべてのフェーズで実行に費やした合計時間を指し、合計時間は、1 つのコンポーネントで経過した合計時間を示します。 このパッケージ コンポーネントの情報は、最後のパッケージの実行のログ レベルが [パフォーマンス] または [詳細] に設定されていた場合のみ、レポートに表示されます。<br /><br /> **"概要"** レポートは、パッケージ タスクの状態を示します。 **"メッセージ"** レポートは、パッケージとタスクのイベント メッセージとエラー メッセージを示し、開始時刻、終了時刻、書き込まれた行の数などを報告します。<br /><br /> **"概要"** レポートの **[メッセージの表示]** をクリックして、 **"メッセージ"** レポートに移動することもできます。 **"メッセージ"** レポートの **[概要の表示]** をクリックして、 **"概要"** レポートに移動することもできます。|  
  
 **[フィルター]** をクリックし、 **[フィルターの設定]** ダイアログで条件を選択することにより、各ページに表示されるテーブルにフィルターを適用できます。 使用できるフィルター条件は、表示されるデータによって異なります。 **[フィルターの設定]** ダイアログの並べ替えアイコンをクリックすることで、レポートの並べ替え順序を変更できます。  
  
## <a name="all-executions-report"></a>"すべての実行" レポート  
 **"すべての実行"** レポートには、サーバーで実行されたすべての [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の実行に関する概要が表示されます。 サンプル パッケージが複数回実行されることがあります。 **"Integration Services ダッシュボード"** レポートとは異なり、 **"すべての実行"** レポートは、指定した日付範囲中に開始された実行を示すように構成できます。 複数の日、月、または年の日付を指定できます。  
  
 このレポートには、次の情報のセクションが表示されます。  
  
|セクション|説明|  
|-------------|-----------------|  
|Assert|レポートに適用される現在のフィルターを示します (開始時間範囲など)。|  
|実行情報|各パッケージの実行の開始時刻、終了時刻、および持続時間を示します。パッケージの実行で使用されたパラメーター値 (パッケージ実行タスクで子パッケージに渡された値など) の一覧を表示できます。 パラメーターの一覧を表示するには、[概要] をクリックします。|  
  
 パッケージ実行タスクを使用して子パッケージで値を使用できるようにする方法の詳細については、「[パッケージ実行タスク](control-flow/execute-package-task.md)」を参照してください。  
  
 パラメーターについて詳しくは、「[Integration Services &#40;SSIS&#41; パラメーター](integration-services-ssis-package-and-project-parameters.md)」をご覧ください。  
  
## <a name="all-connections"></a>すべての接続  
 **"すべての接続"** レポートは、失敗した接続と [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスで発生した実行に関する次の情報を提供します。  
  
 このレポートには、次の情報のセクションが表示されます。  
  
|セクション|説明|  
|-------------|-----------------|  
|Assert|レポートに適用される現在のフィルター (指定した文字列を使用し、 **[前回失敗した日時]** 範囲にある接続など) を示します。<br /><br /> 特定の日付範囲中に発生した接続エラーのみを表示するには、 **[前回失敗した日時]** を設定します。 範囲には、複数の日、月、または年を指定できます。|  
|詳細|接続文字列、接続中に失敗した実行の回数、および最後に失敗した日付を示します。|  
  
## <a name="all-operations-report"></a>"すべての操作" レポート  
 **"すべての操作" レポート** には、パッケージの配置、検証、実行、およびその他の管理操作を含む、サーバー上で実行されたあらゆる [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 操作の概要が表示されます。 Integration Services ダッシュボードと同様に、テーブルにフィルターを適用して、表示される情報を絞り込むことができます。  
  
## <a name="all-validations-report"></a>"すべての検証" レポート  
 **"すべての検証" レポート** には、サーバーで実行されたすべての [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の検証の概要が表示されます。 この概要には、状態、開始時刻、終了時刻など、各検証の情報が表示されます。 各概要エントリには、検証中に生成されたメッセージへのリンクが含まれます。 Integration Services ダッシュボードと同様に、テーブルにフィルターを適用して、表示される情報を絞り込むことができます。  
  
## <a name="custom-reports"></a>カスタム レポート  
 **の** [Integration Services カタログ] **ノードの下の** [SSISDB] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]カタログ ノードに、カスタム レポート (.rdl ファイル) を追加できます。 レポートを追加する前に、ソース テーブルなど、参照するオブジェクトを完全修飾するための 3 つの要素で構成される名前付け規則を使用していることを確認します。 そうでない場合、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] でエラーが表示されます。 名前付け規則は、\<データベース>.\<所有者>.\<オブジェクト> です。 たとえば、SSISDB.internal.executions などです。  
  
> [!NOTE]  
>  **[データベース]** ノードの下の **[SSISDB]** ノードにカスタム レポートを追加した場合、SSISDB プレフィックスは必要ありません。  
  
 カスタム レポートの作成および追加方法については、「 [Add a Custom Report to Management Studio](../ssms/object/add-a-custom-report-to-management-studio.md)」(Management Studio へのカスタム レポートの追加) を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 [Integration Services サーバーのレポートの表示](../../2014/integration-services/view-reports-for-the-integration-services-server.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 [パッケージの実行およびその他の操作の監視](performance/monitor-running-packages-and-other-operations.md)  
  
  
