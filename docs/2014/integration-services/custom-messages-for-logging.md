---
title: Custom Messages for Logging |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], custom
- writing log entries
- SSIS packages, logs
- custom messages for logging [Integration Services]
ms.assetid: 3c74bba9-02b7-4bf5-bad5-19278b680730
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a557d3dfddf5989c580b0ba78f9b5d930c548617
ms.sourcegitcommit: 757cda42bce65721a6079fe403add874f9afb31e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2019
ms.locfileid: "67316663"
---
# <a name="custom-messages-for-logging"></a>ログ記録用のカスタム メッセージ
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、パッケージや多くのタスクのログ エントリを書き込むための豊富なカスタム イベントが用意されています。 記録したエントリを使用すれば、定義済みのイベントやユーザー定義メッセージを後の分析用に記録しておくことで、実行の進行状況、結果、および問題点に関する詳細を保管できます。 たとえば、一括挿入の開始時刻と終了時刻を記録しておけば、パッケージ実行時のパフォーマンスの問題を特定できます。  
  
 カスタム ログ エントリとは、パッケージ、すべてのコンテナー、およびタスクに使用できる一連の標準的なログ記録イベントとは異なるエントリのセットです。 カスタム ログ エントリは、パッケージ内の特定のタスクに関する有益な情報を取得するように調整されます。 たとえば、SQL 実行タスクのカスタム ログ エントリの 1 つに、そのタスクで実行される SQL ステートメントをログに記録するものがあります。  
  
 すべてのログ エントリには、パッケージの開始時と終了時に自動的に書き込まれるログ エントリなど、日付と時刻に関する情報が含まれます。 多くのログ イベントでは、ログに複数のエントリが書き込まれます。 通常、イベントにいくつか異なるフェーズが含まれている場合に複数のエントリが書き込まれます。 たとえば、`ExecuteSQLExecutingQuery` ログ イベントでは、3 つのエントリが書き込まれます。1 つ目はタスクがデータベースへの接続を取得した後、2 つ目は SQL ステートメントの準備が開始された後、3 つ目は SQL ステートメントの実行が完了した後に書き込まれます。  
  
 次の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] オブジェクトには、カスタム ログ エントリがあります。  
  
 [[パッケージ]](#Package)  
  
 [一括挿入タスク](#BulkInsert)  
  
 [[データ フロー タスク]](#DataFlow)  
  
 [DTS 2000 実行タスク](#ExecuteDTS200)  
  
 [プロセス実行タスク](#ExecuteProcess)  
  
 [SQL 実行タスク](#ExecuteSQL)  
  
 [ファイル システム タスク](#FileSystem)  
  
 [FTP タスク](#FTP)  
  
 [メッセージ キュー タスク](#MessageQueue)  
  
 [スクリプト タスク](#Script)  
  
 [メール送信タスク](#SendMail)  
  
 [データベース転送タスク](#TransferDatabase)  
  
 [エラー メッセージ転送タスク](#TransferErrorMessages)  
  
 [ジョブ転送タスク](#TransferJobs)  
  
 [ログイン転送タスク](#TransferLogins)  
  
 [Master ストアド プロシージャ転送タスク](#TransferMasterStoredProcedures)  
  
 [SQL Server オブジェクトの転送タスク](#TransferSQLServerObjects)  
  
 [Web サービス タスク](#WebServices)  
  
 [WMI データ リーダー タスク](#WMIDataReader)  
  
 [WMI イベント監視タスク](#WMIEventWatcher)  
  
 [XML タスク](#XML)  
  
## <a name="log-entries"></a>ログ エントリ  
  
###  <a name="Package"></a> [パッケージ]  
 次の表は、パッケージのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`PackageStart`|パッケージの実行が開始されたことを示します。<br /><br /> 注:このログ エントリは自動的にログに書き込まれます。 除外することはできません。|  
|`PackageEnd`|パッケージが完了したことを示します。<br /><br /> 注:このログ エントリは自動的にログに書き込まれます。 除外することはできません。|  
|`Diagnostic`|同時実行できる実行可能ファイル数など、パッケージの実行に影響するシステム構成に関する情報を提供します。<br /><br /> `Diagnostic` ログ エントリに、外部データ プロバイダーの呼び出し前後のエントリも含まれています。 詳細については、「[トラブルシューティング ツールのパッケージ接続](troubleshooting/troubleshooting-tools-for-package-connectivity.md)」を参照してください。|  
  
###  <a name="BulkInsert"></a> 一括挿入タスク  
 次の表は、一括挿入タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`DTSBulkInsertTaskBegin`|一括挿入が開始されたことを示します。|  
|`DTSBulkInsertTaskEnd`|一括挿入が終了したことを示します。|  
|`DTSBulkInsertTaskInfos`|タスクに関する説明情報を提供します。|  
  
###  <a name="DataFlow"></a> [データ フロー タスク]  
 次の表は、データ フロー タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`BufferSizeTuning`|データ フロー タスクでバッファーのサイズが変更されたことを示します。 このログ エントリはサイズ変更の理由を説明し、一時的な新しいバッファー サイズを表示します。|  
|`OnPipelinePostEndOfRowset`|`ProcessInput` メソッドの最終呼び出しで設定される、行セットの終了シグナルがコンポーネントに通知されたことを示します。 エントリは、データ フロー内で入力を処理するコンポーネントごとに書き込まれます。 このエントリには、コンポーネント名が含まれます。|  
|`OnPipelinePostPrimeOutput`|コンポーネントが `PrimeOutput` メソッドの最終呼び出しを完了したことを示します。 データ フローによっては、複数のログ エントリが書き込まれる場合があります。 コンポーネントがソースの場合、コンポーネントが行の処理を完了したことを意味します。|  
|`OnPipelinePreEndOfRowset`|コンポーネントがまもなくの最後の呼び出しで設定される行セットの終了シグナルを受信することを示します、`ProcessInput`メソッド。 エントリは、データ フロー内で入力を処理するコンポーネントごとに書き込まれます。 このエントリには、コンポーネント名が含まれます。|  
|`OnPipelinePrePrimeOutput`|コンポーネントに、`PrimeOutput` メソッドからの呼び出しが通知されたことを示します。 データ フローによっては、複数のログ エントリが書き込まれる場合があります。|  
|`OnPipelineRowsSent`|`ProcessInput` メソッドの呼び出しによってコンポーネント入力に指定された行数を報告します。 ログ エントリにはコンポーネント名が含まれます。|  
|`PipelineBufferLeak`|バッファー マネージャーの終了後もバッファーを保持しているコンポーネントに関する情報を提供します。 つまり、バッファー リソースが解放されていないため、メモリ リークの原因になる可能性があります。 このログ エントリは、コンポーネントの名前とバッファーの ID を含みます。|  
|`PipelineExecutionPlan`|データ フローの実行プランを報告します。 バッファーをコンポーネントに送信する方法に関する情報を提供します。 この情報は、PipelineExecutionTrees エントリと組み合わせて、タスク内での実行内容を示します。|  
|`PipelineExecutionTrees`|データ フロー内のレイアウトの実行ツリーを報告します。 データ フロー エンジンのスケジューラは、このツリーを使用して、データ フローの実行プランを構築します。|  
|`PipelineInitialization`|タスクに関する初期化情報を提供します。 この情報には、BLOB データの一時的な保存に使用するディレクトリ、既定のバッファー サイズ、およびバッファー内の行数が含まれます。 データ フロー タスクの構成によっては、複数のログ エントリが書き込まれる場合があります。|  
  
###  <a name="ExecuteDTS200"></a> DTS 2000 実行タスク  
 次の表は、DTS 2000 実行タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`ExecuteDTS80PackageTaskBegin`|タスクが DTS 2000 パッケージの実行を開始したことを示します。|  
|`ExecuteDTS80PackageTaskEnd`|タスクが終了したことを示します。<br /><br /> 注:DTS 2000 パッケージは、タスク終了後も引き続き実行される場合があります。|  
|`ExecuteDTS80PackageTaskTaskInfo`|タスクに関する説明情報を提供します。|  
|`ExecuteDTS80PackageTaskTaskResult`|タスクで実行された DTS 2000 パッケージの実行結果を報告します。|  
  
###  <a name="ExecuteProcess"></a> プロセス実行タスク  
 次の表は、プロセス実行タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`ExecuteProcessExecutingProcess`|タスクで実行するように構成されている実行可能ファイルの実行プロセスに関する情報を提供します。<br /><br /> 2 つのログ エントリが書き込まれます。 1 つのエントリには、タスクで実行される実行可能ファイルの名前と場所が含まれ、もう 1 つのエントリは、実行可能ファイルの終了を記録します。|  
|`ExecuteProcessVariableRouting`|実行可能ファイルの入力と出力にルーティングされる変数に関する情報を提供します。 ログ エントリは、stdin (入力)、stdout (出力)、および stderr (エラー出力) に書き込まれます。|  
  
###  <a name="ExecuteSQL"></a> SQL 実行タスク  
 次の表では、SQL 実行タスクのカスタム ログ エントリを説明します。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`ExecuteSQLExecutingQuery`|SQL ステートメントの実行フェーズに関する情報を提供します。 タスクがデータベースへの接続を取得したとき、SQL ステートメントの準備が開始されたとき、および SQL ステートメントの実行が完了した後に、ログ エントリが書き込まれます。 準備フェーズのログ エントリには、タスクで使用される SQL ステートメントが含まれます。|  
  
###  <a name="FileSystem"></a> ファイル システム タスク  
 次の表では、ファイル システム タスクのカスタム ログ エントリを説明します。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`FileSystemOperation`|タスクで実行される操作を報告します。 ログ エントリは、ファイル システム操作の開始時に書き込まれます。これには、操作の基になるファイルと操作対象のファイルに関する情報が含まれます。|  
  
###  <a name="FTP"></a> FTP タスク  
 次の表は、FTP タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`FTPConnectingToServer`|タスクで FTP サーバーへの接続が開始されたことを示します。|  
|`FTPOperation`|タスクで実行された FTP 操作の開始および種類を報告します。|  
  
###  <a name="MessageQueue"></a> メッセージ キュー タスク  
 次の表は、メッセージ キュー タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`MSMQAfterOpen`|タスクで開いていたメッセージ キューを終了したことを示します。|  
|`MSMQBeforeOpen`|タスクがメッセージ キューを開く操作を開始したことを示します。|  
|`MSMQBeginReceive`|タスクがメッセージの受信を開始したことを示します。|  
|`MSMQBeginSend`|タスクがメッセージの送信を開始したことを示します。|  
|`MSMQEndReceive`|タスクがメッセージの受信を終了したことを示します。|  
|`MSMQEndSend`|タスクがメッセージの送信を終了したことを示します。|  
|`MSMQTaskInfo`|タスクに関する説明情報を提供します。|  
|`MSMQTaskTimeOut`|タスクがタイムアウトしたことを示します。|  
  
###  <a name="Script"></a> スクリプト タスク  
 次の表では、スクリプト タスクのカスタム ログ エントリを説明します。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`ScriptTaskLogEntry`|スクリプト内でのログ記録の実装結果を報告します。 ログ エントリは、`Log` オブジェクトの `Dts` メソッドを呼び出すたびに書き込まれます。 このエントリは、コードの実行時に書き込まれます。 詳細については、 [「スクリプト タスクでのログ記録」](extending-packages-scripting/task/logging-in-the-script-task.md)をご覧ください。|  
  
###  <a name="SendMail"></a> メール送信タスク  
 次の表は、メール送信タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`SendMailTaskBegin`|タスクが電子メール メッセージの送信を開始したことを示します。|  
|`SendMailTaskEnd`|タスクが電子メール メッセージの送信を終了したことを示します。|  
|`SendMailTaskInfo`|タスクに関する説明情報を提供します。|  
  
###  <a name="TransferDatabase"></a> データベース転送タスク  
 次の表は、データベース転送タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`SourceDB`|タスクでコピーされたデータベースを示します。|  
|`SourceSQLServer`|データベースのコピー元のコンピューターを示します。|  
  
###  <a name="TransferErrorMessages"></a> エラー メッセージ転送タスク  
 次の表は、エラー メッセージ転送タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`TransferErrorMessagesTaskFinishedTransferringObjects`|タスクがエラー メッセージの転送を終了したことを示します。|  
|`TransferErrorMessagesTaskStartTransferringObjects`|タスクがエラー メッセージの転送を開始したことを示します。|  
  
###  <a name="TransferJobs"></a> ジョブ転送タスク  
 次の表は、ジョブ転送タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`TransferJobsTaskFinishedTransferringObjects`|タスクが [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェント ジョブの転送を終了したことを示します。|  
|`TransferJobsTaskStartTransferringObjects`|タスクが [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェント ジョブの転送を開始したことを示します。|  
  
###  <a name="TransferLogins"></a> ログイン転送タスク  
 次の表は、ログイン転送タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`TransferLoginsTaskFinishedTransferringObjects`|タスクがログインの転送を終了したことを示します。|  
|`TransferLoginsTaskStartTransferringObjects`|タスクがログインの転送を開始したことを示します。|  
  
###  <a name="TransferMasterStoredProcedures"></a> Master ストアド プロシージャ転送タスク  
 次の表は、Master ストアド プロシージャ転送タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`TransferStoredProceduresTaskFinishedTransferringObjects`|**master** データベースに格納されている、ユーザー定義ストアド プロシージャの転送をタスクが完了したことを示します。|  
|`TransferStoredProceduresTaskStartTransferringObjects`|**master** データベースに格納されている、ユーザー定義ストアド プロシージャの転送をタスクが開始したことを示します。|  
  
###  <a name="TransferSQLServerObjects"></a> SQL Server オブジェクトの転送タスク  
 次の表は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] オブジェクトの転送タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`TransferSqlServerObjectsTaskFinishedTransferringObjects`|タスクが [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベース オブジェクトの転送を終了したことを示します。|  
|`TransferSqlServerObjectsTaskStartTransferringObjects`|タスクが [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベース オブジェクトの転送を開始したことを示します。|  
  
###  <a name="WebServices"></a> Web サービス タスク  
 次の表は、Web サービス タスクに対して有効にできるカスタム ログ エントリの一覧です。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`WSTaskBegin`|タスクが Web サービスへのアクセスを開始しました。|  
|`WSTaskEnd`|タスクが Web サービス メソッドを完了しました。|  
|`WSTaskInfo`|タスクに関する説明情報を提供します。|  
  
###  <a name="WMIDataReader"></a> WMI データ リーダー タスク  
 次の表は、WMI データ リーダー タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`WMIDataReaderGettingWMIData`|タスクが WMI データの読み取りを開始したことを示します。|  
|`WMIDataReaderOperation`|タスクで実行された WQL クエリを報告します。|  
  
###  <a name="WMIEventWatcher"></a> WMI イベント監視タスク  
 次の表は、WMI イベント監視タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`WMIEventWatcherEventOccurred`|タスクが監視しているイベントが発生したことを示します。|  
|`WMIEventWatcherTimedout`|タスクがタイムアウトしたことを示します。|  
|`WMIEventWatcherWatchingForWMIEvents`|タスクが WQL クエリの実行を開始したことを示します。 このエントリには、クエリが含まれています。|  
  
###  <a name="XML"></a> XML タスク  
 次の表では、XML タスクのカスタム ログ エントリを説明します。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`XMLOperation`|タスクで実行される操作に関する情報を提供します。|   
  
## <a name="see-also"></a>関連項目  
 [Integration Services &#40;SSIS&#41; のログ記録](performance/integration-services-ssis-logging.md)  
  
