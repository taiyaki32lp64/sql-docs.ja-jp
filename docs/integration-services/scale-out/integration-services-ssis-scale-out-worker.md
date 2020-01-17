---
title: SQL Server Integration Services (SSIS) Scale Out Worker | Microsoft Docs
description: この記事では、SSIS Scale Out の Scale Out Master コンポーネントについて説明します
ms.custom: performance
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: 1f2be60ff216b65afbb50c0e97da4edfb4239aec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68082071"
---
# <a name="integration-services-ssis-scale-out-worker"></a>Integration Services (SSIS) Scale Out Worker

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Scale Out Worker は Scale Out Worker サービスを実行し、Scale Out Master から実行タスクをプルします。 次に、ワーカーは `ISServerExec.exe` を利用し、ローカルでパッケージを実行します。

## <a name="configure-the-scale-out-worker-service"></a>Scale Out Worker サービスを構成する
`\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config` ファイルを使用して、Scale Out Worker サービスを構成できます。 構成ファイルの更新後に、サービスを再起動する必要があります。

|構成  |[説明]  |既定値|
|---------|---------|---------|
|DisplayName|Scale Out Worker の表示名。 **[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017 では使用しません。**|コンピューター名|
|[説明]|Scale Out Worker の説明。 **[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017 では使用しません。**|空|
|MasterEndpoint|Scale Out Master に接続するエンドポイント。|Scale Out Worker のインストール時に設定されるエンドポイント|
|MasterHttpsCertThumbprint|Scale Out Master の認証に使用されるクライアント SSL 証明書のサムプリント|Scale Out Worker のインストール時に指定されるクライアント証明書のサムプリント。|
|WorkerHttpsCertThumbprint|Scale Out Master の認証に使用される Scale Out Master 証明書のサムプリント。|Scale Out Worker のインストール時に自動的に作成され、インストールされる証明書のサムプリント|
|StoreLocation|ワーカー証明書ストアの場所。|LocalMachine|
|StoreName|ワーカー証明書ストアの名前。|My|
|AgentHeartbeatInterval|Scale Out Worker ハートビートの間隔。|00:01:00|
|TaskHeartbeatInterval|Scale Out Worker でのタスク状態のレポート間隔。|00:00:10|
|HeartbeatErrorTolerance|最後の正常なタスク ハートビート以降、この時間が経過すると、ハートビートのエラー応答が受信された場合にタスクは終了します。|00:10:00|
|TaskRequestMaxCPU|Scale Out Worker のタスク要求時の CPU の上限。|70.0|
|TaskRequestMinMemory|Scale Out Worker のタスク要求時のメモリの下限 (MB 単位)。|100.0|
|MaxTaskCount|Scale Out Worker が保持できるタスクの最大数。|10|
|LeaseInterval|Scale Out Worker によって保持されているタスクのリース間隔。|00:01:00|
|TasksRootFolder|タスク ログのフォルダー。 値が空の場合、`\<drive\>:\Users\[account]\AppData\Local\SSIS\Cluster\Tasks` フォルダー パスが使用されます。 [アカウント] は、Scale Out Worker サービスを実行するアカウントです。 既定のアカウントは SSISScaleOutWorker140 です。|空|
|TaskLogLevel|Scale Out Worker のタスク ログ レベル。 (Verbose 0x01、Information 0x02、Warning 0x04、Error 0x08、Progress 0x10、CriticalError 0x20、Audit 0x40)|126 (Information、Warning、Error、Progress、CriticalError、Audit)|
|TaskLogSegment|タスク ログ ファイルの期間。|00:00:00|
|TaskLogEnabled|タスク ログが有効かどうかを示します。|true|
|ExecutionLogCacheFolder|パッケージ実行ログのキャッシュに使用するフォルダー。 値が空の場合、`\<drive\>:\Users\[account]\AppData\Local\SSIS\Cluster\Agent\ELogCache` フォルダー パスが使用されます。 [アカウント] は、Scale Out Worker サービスを実行するアカウントです。 既定のアカウントは SSISScaleOutWorker140 です。|空|
|ExecutionLogMaxBufferLogCount|メモリ内の 1 つの実行ログ バッファーの、キャッシュされる実行ログの最大数。|10000|
|ExecutionLogMaxInMemoryBufferCount|実行ログ用のメモリ内の実行ログ バッファーの最大数。|10|
|ExecutionLogRetryCount|実行ログに失敗した場合の再試行回数。|3|
|ExecutionLogRetryTimeout|実行ログに失敗した場合の再試行タイムアウト。 ExecutionLogRetryTimeout に達した場合、ExecutionLogRetryCount は無視されます。 |7.00:00:00 (7 日)|
|AgentId|Scale Out Worker の Worker Agent ID|自動生成|
||||    

## <a name="view-the-scale-out-worker-log"></a>Scale Out Worker ログの表示
Scale Out Worker サービスのログ ファイルは `\<drive\>:\Users\\[account]\AppData\Local\SSIS\ScaleOut\Agent` フォルダーにあります。

個別タスクのログの場所は `TasksRootFolder` の `WorkerSettings.config` ファイルで構成されます。 値を指定しない場合、ログは `\<drive\>:\Users\\[account]\AppData\Local\SSIS\ScaleOut\Tasks` フォルダーに置かれます。 

*[account]* パラメーターは、Scale Out Worker サービスを実行するアカウントです。 既定では、アカウントは `SSISScaleOutWorker140` です。

## <a name="next-steps"></a>次の手順
[Integration Services (SSIS) Scale Out Master](integration-services-ssis-scale-out-master.md)
