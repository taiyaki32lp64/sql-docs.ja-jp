---
title: SSIS による Analysis Services の管理タスクの自動化 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Execute DDL Task [Analysis Services]
- Analysis Services Processing task
ms.assetid: e960a9a2-80b4-45da-9369-bc560ecdccac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 23efdeddd568c815ad22ce6cf0b5d2026bab813e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080332"
---
# <a name="automate-analysis-services-administrative-tasks-with-ssis"></a>SSIS による Analysis Services 管理タスクの自動化
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] を使用すると、DDL スクリプト、キューブおよびマイニング モデルの処理タスク、データ マイニング クエリ タスクの実行を自動化できます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は、制御フローおよびメンテナンス タスクの集合と考えることができ、これらをリンクしてシーケンシャルおよび並列のデータ処理ジョブを作成できます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は、データ処理タスク時のデータのクリーンアップと、異なるデータ ソースからのデータの統合を実行できるように設計されています。 キューブおよびマイニング モデルを使用して作業する場合、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、非数値データを数値データに変換し、データ値を期待される範囲内に収めることができます。したがって、ファクト テーブルとディメンションに設定するためのクリーンなデータを作成できます。  
  
## <a name="integration-services-tasks"></a>Integration Services タスク  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のタスクまたはジョブには、制御フロー要素とデータ フロー要素という 2 つの要素があります。 制御フロー要素では、優先順位制約を適用することによってジョブ進行の論理的な順序を定義します。 データ フロー要素は、コンポーネントの出力から後続コンポーネントの入力への接続と、その間でデータに対して行われるデータ変換に関係しています。 データの行き先に関する決定は、優先順位制約に含まれる論理によってどのコンポーネントが出力を受け取るかが指定されます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] タスクには、DDL 実行タスク、Analysis Services 処理タスク、およびデータ マイニング クエリ タスクがあります。 これらの各タスクでは、メール送信タスクを使用して、タスク結果を含む電子メール メッセージを管理者に送信できます。  
  
## <a name="the-execute-ddl-task"></a>DDL 実行タスク  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の DDL 実行タスクを使用すると、DDL スクリプトを [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーに直接送信して、自動的に実行できます。 これによって、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理者は、バックアップ、復元、または同期の操作を [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ内から実行できます。 パッケージは、前に説明した制御フロー要素とデータ フロー要素で構成されています。これらの要素は、タスクに追加できる他の DDL ステートメントと同様に、すべて **定期的に実行**される必要があります。 ここで説明したタスクは夜間に実行される場合が多いため、任意のスケジューリング アプリケーションから簡単に実行できるパッケージを作成すると特に便利です。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] エージェントを使用すると、パッケージを任意の時刻に実行するようにスケジュールできます。 このタスクの実装方法については、「 [Analysis Services DDL 実行タスク](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)」を参照してください。  
  
## <a name="analysis-services-processing-task"></a>Analysis Services 処理タスク  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の Analysis Services 処理タスクを使用すると、ソース リレーショナル データベースの定期更新を実行するときに、キューブに新しい情報を自動的に設定できます。 Analysis Services 処理タスクを使用すると、ディメンション、キューブ、またはパーティション レベルで処理を実行できます。 処理自体の種類は、`incremental` または `full` のいずれかです。どちらの種類かは、ジョブ要件に基づいてユーザーが選択します。 増分処理では、新しいデータを追加し、十分な再計算を実行して、ターゲットを最新の状態に維持する一方、完全処理では、既存のデータを破棄し、完全な最読み込みと再計算を実行します。 完全処理の方が時間はかかりますが、より完全性が高くなります。 このタスクの実装方法については、「 [Analysis Services 処理タスク](../../integration-services/control-flow/analysis-services-processing-task.md)」を参照してください。  
  
## <a name="data-mining-query-task"></a>データ マイニング クエリ タスク  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のデータ マイニング クエリ タスクを使用すると、マイニング モデルから情報を抽出して保存できます。 多くの場合、この情報はリレーショナル データベースに格納され、たとえばターゲット マーケティング キャンペーン用の潜在顧客の一覧を作成するために使用できます。 データ マイニングでは、顧客の値とその顧客が特定のマーケティング ピッチに対して応答する確率を識別できます。 データ マイニング クエリ タスクを使用すると、好みの書式にデータを抽出したり、変更したりできます。 このタスクの実装方法については、「 [データ マイニング クエリ タスク](../../integration-services/control-flow/data-mining-query-task.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [パーティション処理変換先](../../integration-services/data-flow/partition-processing-destination.md)   
 [ディメンション処理変換先](../../integration-services/data-flow/dimension-processing-destination.md)   
 [データ マイニング クエリ変換](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)   
 [多次元モデル オブジェクトの処理](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Analysis Services の管理タスクのスクリプト作成](../script-administrative-tasks-in-analysis-services.md)  
  
  
