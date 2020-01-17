---
title: 状態変数の定義 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 45d66152-883a-49a7-a877-2e8ab45f8f79
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4b0dcc3c1709943207834aab6ef4b39453b2d89d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62827564"
---
# <a name="define-a-state-variable"></a>状態変数の定義
  この手順では、CDC 状態が格納されるパッケージ変数を定義する方法について説明します。  
  
 CDC 状態変数は CDC 制御タスクによって読み込まれ、初期化され、更新されます。また、CDC ソース データ フロー コンポーネントによって使用され、変更レコードの現在の処理範囲が決まります。 CDC 状態変数は、CDC 制御タスクおよび CDC ソースに共通のコンテナーで定義できます。 これはパッケージ レベルですが、ループ コンテナーのような他のコンテナーに対しても設定できます。  
  
 CDC 状態変数の値を手動で変更することは推奨されませんが、その内容を理解しておくと便利です。  
  
 次の表に、CDC 状態変数値の各要素の概要を示します。  
  
|コンポーネント|説明|  
|---------------|-----------------|  
|`<state-name>`|現在の CDC 状態の名前です。|  
|`CS`|現在の処理範囲の始点 (Current Start) を示します。|  
|`<cs-lsn>`|前回の CDC 実行で処理された最後のログ シーケンス番号 (LSN) です。|  
|`CE`|現在の処理範囲の終点 (Current End) を示します。 CDC 状態に CE 要素が存在するかどうかにより、CDC パッケージが現在処理中であるか、または CDC 処理範囲が完全に処理される前に CDC パッケージが失敗したことが示されます。|  
|`<ce-lsn>`|現在の CDC 実行で処理される最後の LSN です。 処理対象の最後のシーケンス番号は最大値 (0xFFF...) であることが常に想定されます。|  
|`IR`|初期処理範囲を示します。|  
|`<ir-start>`|初期読み込みが開始した直前の変更の LSN です。|  
|`<ir-end>`|初期読み込みが終了した直後の変更の LSN です。|  
|`TS`|CDC 状態の最後の更新のタイムスタンプを示します。|  
|**\<timestamp>**|64 ビットの System.DateTime.UtcNow プロパティの 10 進数表記です。|  
|`ER`|直前の操作が失敗した場合に表示され、エラーの原因の簡単な説明が含まれます。 この要素が存在する場合は、常に最後に表示されます。|  
|`<short-error-text>`|エラーの簡単な説明です。|  
  
 LSN とシーケンス番号はそれぞれ、Binary(10) の LSN 値を表す最大 20 桁の 16 進数文字列としてエンコードされます。  
  
 次の表に、使用可能な CDC 状態値を示します。  
  
|状態|説明|  
|-----------|-----------------|  
|(INITIAL)|現在の CDC グループでパッケージが実行される前の初期状態です。 CDC 状態が空のときの状態でもあります。|  
|ILSTART (Initial Load Started)|CDC 制御タスクに対する `MarkInitialLoadStart` 操作の呼び出し後、初期読み込みパッケージが開始したときの状態です。|  
|ILEND (Initial Load Ended)|CDC 制御タスクに対する `MarkInitialLoadEnd` 操作の呼び出し後、初期読み込みパッケージが正常に終了したときの状態です。|  
|ILUPDATE (Initial Load Update)|初期読み込みの後にトリクル フィード更新パッケージが実行され、まだ初期処理範囲を処理しているときの状態です。 CDC 制御タスクに対する `GetProcessingRange` 操作の呼び出し後に、この状態になります。<br /><br /> __$reprocessing 列を使用している場合は、既にターゲットに存在する行をパッケージが再処理している可能性があることを示す 1 に設定されます。|  
|TFEND (Trickle-Feed Update Ended)|定期的な CDC の実行で期待される状態です。 前の実行が正常に完了していることと、新しい実行を新しい処理範囲で開始できることを表します。|  
|TFSTART|CDC 制御タスクに対する `GetProcessingRange` 操作の呼び出し後、トリクル フィード更新パッケージの後続実行を行ったときの状態です。<br /><br /> 定期的な CDC の実行を開始したものの、まだ完了していないことを表します (`MarkProcessedRange`)。|  
|TFREDO (Reprocessing Trickle-Feed Updates)|TFSTART の後に `GetProcessingRange` が行われたときの状態です。 前の実行が正常に完了しなかったことを表します。<br /><br /> __$reprocessing 列を使用している場合は、既にターゲットに存在する行をパッケージが再処理している可能性があることを示す 1 に設定されます。|  
|ERROR|CDC グループはエラー状態です。|  
  
 次に、CDC 状態変数値の例を示します。  
  
-   ILSTART/IR/0x0000162B158700000000//TS/2011-08-07T17:10:43.0031645/  
  
-   ILSTART/IR/0x0000162B158700000000//TS/2011-08-07T17:10:43.0031645/  
  
-   TFEND/CS/0x0000025B000001BC0003/TS/2011-07-17T12:05:58.1001145/  
  
-   TFSTART/CS/0x0000030D000000AE0003/CE/0x0000159D1E0F01000000/TS/2011-08-09T05:30:43.9344900/  
  
-   TFREDO/CS/0x0000030D000000AE0003/CE/0x0000159D1E0F01000000/TS/2011-08-09T05:30:59.5544900/  
  
### <a name="to-define-a-cdc-state-variable"></a>CDC 状態変数を定義するには  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で、変数を定義する必要がある CDC フローを含む [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] パッケージを開きます。  
  
2.  **[パッケージ エクスプ ローラー]** タブをクリックして、新しい変数を追加します。  
  
3.  変数に、状態変数として識別できる名前を付けます。  
  
4.  変数を **String** データ型に設定します。  
  
 定義するときに、変数に値を設定しないでください。 値は、CDC 制御タスクで設定する必要があります。  
  
 **[状態の自動保持]** を指定して CDC 制御タスクを使用する予定の場合、CDC 状態変数は指定するデータベース状態テーブルから読み取られ、値の変更時に同じテーブルの値が更新されます。 状態テーブルの詳細については、「 [CDC Control Task](../control-flow/cdc-control-task.md)」および「 [CDC Control Task Editor](../cdc-control-task-editor.md)」を参照してください。  
  
 [状態の自動保持] を指定して CDC 制御タスクを使用しない場合は、パッケージが最後に実行されたときに変数の値が保存された永続ストレージからその値を読み込み、現在の処理範囲の処理が終了したときに永続ストレージにその値を書き戻す必要があります。  
  
## <a name="see-also"></a>参照  
 [CDC Control Task](../control-flow/cdc-control-task.md)   
 [CDC Control Task Editor](../cdc-control-task-editor.md)  
  
  
