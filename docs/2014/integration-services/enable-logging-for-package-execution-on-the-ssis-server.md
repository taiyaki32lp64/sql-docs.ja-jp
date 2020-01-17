---
title: SSIS サーバー上でパッケージ実行のログ記録を有効にする |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8930c63c-bc6f-46c2-b428-b3c29ee89a7d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 47f74d4510b46b984eb58706ff4ac159cb8b1352
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059368"
---
# <a name="enable-logging-for-package-execution-on-the-ssis-server"></a>SSIS サーバーでのパッケージ実行のログ記録を有効にする
  この手順では、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーに配置したパッケージを実行するときに、パッケージのログ記録レベルを設定または変更する方法について説明します。 パッケージを実行するときに設定したログ記録レベルは、[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] を使用して構成したパッケージのログ記録レベルをオーバーライドします。 詳細については、「 [SQL Server Data Tools でパッケージのログ記録を有効にする](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md) 」を参照してください。  
  
 ログ記録レベルを指定するには、次のいずれかの方法を使用します。 このトピックでは最初の方法について説明します。  
  
-   [パッケージの実行] ダイアログ ボックスを使用してパッケージ実行インスタンスを構成する  
  
-   [catalog.set_execution_parameter_value &#40;SSISDB データベース&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database) を使用して、実行のインスタンスのパラメーターを設定する  
  
-   [新しいジョブ ステップ] ダイアログ ボックスを使用してパッケージ実行用の SQL Server エージェント ジョブを構成する  
  
### <a name="to-set-the-logging-level-for-a-package-by-using-the-execute-package-dialog-box"></a>[パッケージの実行] ダイアログ ボックスを使用してパッケージのログ記録レベルを設定するには  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]のオブジェクト エクスプローラーで、パッケージに移動します。  
  
2.  パッケージを右クリックし、 **[実行]** をクリックします。  
  
3.  **[パッケージの実行]** ダイアログ ボックスで、 **[詳細設定]** タブをクリックします。  
  
4.  **[ログ記録レベル]** で、ログ記録レベルを選択します。 設定できる値については、次の表を参照してください。  
  
5.  他のパッケージの構成を完了し、 **[OK]** をクリックしてパッケージを実行します。  
  
 設定できるログ記録レベルは次のとおりです。  
  
|[ログ記録レベル]|説明|  
|-------------------|-----------------|  
|なし|ログ記録をオフにします。 パッケージの実行状態のみがログに記録されます。|  
|Basic|カスタム イベントと診断イベントを除く、すべてのイベントをログに記録します。 これが既定値です。|  
|パフォーマンス|パフォーマンス統計、および OnError イベントと OnWarning のイベントのみをログに記録します。<br /><br /> **"実行のパフォーマンス"** レポートは、パッケージ データ フロー コンポーネントのアクティブな時間と合計時間を示します。 この情報は、最後のパッケージの実行のログ記録レベルが **[パフォーマンス]** または **[詳細]** に設定されていた場合にのみ表示されます。 詳細については、「 [Reports for the Integration Services Server](../../2014/integration-services/reports-for-the-integration-services-server.md)」を参照してください。<br /><br /> [catalog.execution_component_phases](/sql/integration-services/system-views/catalog-execution-component-phases) ビューは、実行の各フェーズでのデータ フロー コンポーネントの開始時刻と終了時刻を表示します。 これらのコンポーネントの情報は、パッケージの実行のログ記録レベルが **[パフォーマンス]** または **[詳細]** に設定されている場合にのみ、このビューに表示されます。|  
|"詳細"|カスタム イベントと診断イベントを含む、すべてのイベントをログに記録されます。<br /><br /> DiagnosticEx イベントは、診断イベントの例です。 パッケージ実行タスクでは、子パッケージを実行するたびに、このイベントを記録します。 イベント メッセージは、子パッケージに渡されるパラメーターの値で構成されています<br /><br /> DiagnosticEx のメッセージ列の値は XML テキストです。 . パッケージ実行のメッセージ テキストを表示するには、[catalog.operation_messages &#40;SSISDB データベース&#41;](/sql/integration-services/system-views/catalog-operation-messages-ssisdb-database) ビューのクエリを実行します。<br /><br /> 注:カスタム イベントには、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] タスクによってログに記録されるイベントが含まれます。 詳細については、「 [Custom Messages for Logging](../../2014/integration-services/custom-messages-for-logging.md)」を参照してください。<br /><br /> [catalog.execution_data_statistics](../relational-databases/statistics/statistics.md) ビューは、パッケージ実行で、データ フロー コンポーネントが下流コンポーネントへデータを送信するたびに 1 行を表示します。 ビューにこの情報を取得するには、ログ記録レベルを **[詳細]** に設定する必要があります。|  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; のログ記録](performance/integration-services-ssis-logging.md)   
 [SQL Server Data Tools でパッケージのログ記録を有効にする](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md)  
  
  
