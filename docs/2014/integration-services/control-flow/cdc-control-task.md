---
title: CDC 制御タスク | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdccontroltask.f1
ms.assetid: 6404dc7f-550c-47cc-b901-c072742f430a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e1ddc919b4658395c6a4268f03131bc92291f1b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62832884"
---
# <a name="cdc-control-task"></a>CDC 制御タスク
  CDC 制御タスクは、変更データ キャプチャ (CDC) パッケージのライフ サイクルの制御に使用します。 CDC 制御タスクは、初期読み込みパッケージと CDC パッケージとの同期処理を行い、CDC パッケージの実行で処理されるログ シーケンス番号 (LSN) 範囲を管理します。 また、エラー シナリオおよび復旧の処理も行います。  
  
 CDC 制御タスクは CDC パッケージの状態を SSIS パッケージ変数に保持します。また、データベース テーブルに保存して、アクティブ化されるパッケージ間および共通の CDC プロセスを実行する複数のパッケージ間 (たとえば、あるタスクが初期読み込みを実行し、別のタスクがトリクル フィード更新を実行する場合) で状態が維持されるようにすることもできます。  
  
 CDC 制御タスクでは、2 つのグループの操作がサポートされます。 1 つ目のグループは初期読み込みと変更処理との間の同期処理を行い、もう 1 つのグループは CDC パッケージ実行時の LSN の変更処理範囲の管理と正常に処理された範囲の追跡を行います。  
  
 次の操作は、初期読み込みと変更処理との間の同期処理を行います。  
  
|操作|説明|  
|---------------|-----------------|  
|ResetCdcState|この操作は、現在の CDC コンテキストに関連付けられた、永続的な CDC の状態をリセットするために使用されます。 この操作の実行後に、LSN-timestamp `sys.fn_cdc_get_max_lsn` テーブルの現在の最大 LSN が次の処理範囲の開始位置になります。 この操作には、ソース データベースへの接続が必要です。|  
|MarkInitialLoadStart|この操作は初期読み込みパッケージの開始時に使用され、ソース データベースで現在の LSN を記録します。その後、初期読み込みパッケージがソース テーブルの読み取りを開始します。 この操作には、 `sys.fn_cdc_get_max_lsn`を呼び出すための、ソース データベースへの接続が必要です。<br /><br /> (Oracle ではなく) [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC での作業時に MarkInitialLoadStart を選択した場合、接続マネージャーで指定されたユーザーは、db_owner か sysadmin である必要があります。|  
|MarkInitialLoadEnd|この操作は初期読み込みパッケージの終了時に使用され、初期読み込みパッケージがソース テーブルの読み取りを終了した後で、ソース データベースで現在の LSN を記録します。 この LSN を特定するために、この操作が発生したときの時刻が記録され、CDC データベース内の `cdc.lsn_time_`マッピング テーブルに対するクエリにより、その時刻より後に行われた変更が検索されます。<br /><br /> (Oracle ではなく) [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC での作業時に MarkInitialLoadEnd を選択した場合、接続マネージャーで指定されたユーザーは、db_owner か sysadmin である必要があります。|  
|MarkCdcStart|この操作は、初期読み込みがスナップショット データベースから行われるときに使用されます。 この場合、変更処理は、スナップショット LSN の直後から開始されます。 使用するスナップショット データベースの名前と、スナップショット LSN に関するクエリを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] に対して実行する CDC 制御タスクを使用できます。 また、スナップショット LSN を直接指定するオプションもあります。<br /><br /> (Oracle ではなく) [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC での作業時に MarkCdcStart を選択した場合、接続マネージャーで指定されたユーザーは、db_owner か sysadmin である必要があります。|  
  
 処理範囲の管理には、次の操作を使用します。  
  
|操作|説明|  
|---------------|-----------------|  
|GetProcessingRange|この操作は、CDC ソース データ フローを使用するデータ フローを呼び出す前に使用されます。 この操作は、呼び出し時に CDC ソース データ フローが読み取る LSN の範囲を設定します。 範囲は、データ フローの処理中に CDC ソースによって使用される SSIS パッケージ変数に格納されます。<br /><br /> 格納される状態の詳細については、「 [状態変数の定義](../data-flow/define-a-state-variable.md)」を参照してください。|  
|MarkProcessedRange|:この操作は、CDC 実行で完全に処理された最後の LSN を記録するために、各 CDC の実行後 (CDC データ フローが正常に完了した後) に実行されます。 GetProcessingRange を次に実行する際、この位置が次の処理範囲の開始位置になります。|  
  
## <a name="handling-cdc-state-persistency"></a>CDC 状態の永続性の処理  
 CDC 制御タスクは、アクティブ化のたびに永続的な状態を維持します。 CDC 状態に格納される情報を使用して CDC パッケージの処理範囲およびエラー条件を検出する処理範囲を決定し、管理します。 永続的な状態は文字列として格納されます。 詳細については、「 [状態変数の定義](../data-flow/define-a-state-variable.md)」を参照してください。  
  
 CDC 制御タスクは、2 種類の状態の永続性をサポートします。  
  
-   手動の状態の永続性: この場合、CDC 制御タスクがパッケージ変数に格納されている状態を管理しますが、パッケージ開発者は、CDC 制御を呼び出す前に永続的なストアから変数を読み取り、CDC 制御が最後に呼び出され、CDC の実行が完了した後で変数に書き戻す必要があります。  
  
-   自動の状態の永続性: CDC 状態はデータベースのテーブルに格納されます。 状態は、 **[状態の格納に使用するテーブル]** プロパティに指定されたテーブルに、 **StateName** プロパティに指定されている名前で格納されます。これは、状態を格納するために選択した接続マネージャー内にあります。 既定ではソース接続マネージャーですが、ターゲット接続マネージャーにするのが一般的です。 CDC 制御タスクは状態テーブルの状態値を更新し、アンビエント トランザクションの一環としてコミットされます。  
  
## <a name="error-handling"></a>エラー処理  
 CDC 制御タスクは、次の場合にエラーを報告することがあります。  
  
-   永続的な CDC 状態の読み取りに失敗したとき、または永続的な状態の更新が失敗したとき。  
  
-   ソース データベースからの現在の LSN 情報の読み取りに失敗したとき。  
  
-   読み取った CDC 状態に一貫性がないとき。  
  
 このような場合、CDC 制御タスクはエラーを報告します。このエラーは、SSIS が制御フローのエラーを処理する標準的な方法で処理できます。  
  
 CDC 制御タスクは、GetProcessingRange 操作の直後、MarkProcessedRange が呼び出される前に別の GetProcessingRange 操作が呼び出された場合に、警告も報告します。 これは、先に実行された操作が失敗した状況、または、別の CDC パッケージが同じ CDC 状態名を使用して実行されている状況を示します。  
  
## <a name="configuring-the-cdc-control-task"></a>CDC 制御タスクの構成  
 プロパティは、SSIS デザイナーを使用して、またはプログラムによって設定できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [CDC 制御タスク エディター](../cdc-control-task-editor.md)  
  
-   [CDC 制御タスクのカスタム プロパティ](cdc-control-task-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [状態変数の定義](../data-flow/define-a-state-variable.md)  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   social.technet.microsoft.com の技術記事「 [Microsoft SQL Server 2012 Change Data Capture for Oracle by Attunity のインストール](https://go.microsoft.com/fwlink/?LinkId=252958)」  
  
-   social.technet.microsoft.com の技術記事「 [Microsoft Change Data Capture for Oracle by Attunity の構成の問題のトラブルシューティング](https://go.microsoft.com/fwlink/?LinkId=252960)」  
  
-   social.technet.microsoft.com の技術記事「 [Microsoft Change Data Capture for Oracle by Attunity の CDC インスタンス エラーのトラブルシューティング](https://go.microsoft.com/fwlink/?LinkId=252961)」  
  
  
