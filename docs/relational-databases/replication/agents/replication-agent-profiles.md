---
title: レプリケーション エージェント プロファイル | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Distribution Agent, profiles
- replication [SQL Server], agents and profiles
- replication agent profiles [SQL Server]
- Merge Agent, profiles
- agents [SQL Server replication], profiles
- Queue Reader Agent, profiles
- profiles [SQL Server], replication agents
- Snapshot Agent, profiles
- Log Reader Agent, profiles
ms.assetid: 0e980725-e42f-4283-94cb-d8a6dba5df62
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 3a329c8d8564e92319be773250761085f34643df
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770795"
---
# <a name="replication-agent-profiles"></a>レプリケーション エージェント プロファイル
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  レプリケーションを構成すると、エージェント プロファイルのセットがディストリビューターにインストールされます。 エージェント プロファイルには、エージェントが実行されるたびに使用されるパラメーターのセットが含まれています。スタートアップ処理中に各エージェントはディストリビューターにログインし、各エージェントのプロファイルのパラメーターをクエリします。 Web 同期を使用するマージ サブスクリプションの場合、プロファイルはダウンロードされてサブスクライバーに格納されます。 プロファイルが変更されると、次回マージ エージェントが実行されたときにサブスクライバーのプロファイルが更新されます。 Web 同期の詳細については、「 [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md)」を参照してください。  
  
 レプリケーションでは、各エージェント用の既定のプロファイルの他に、ログ リーダー エージェント、ディストリビューション エージェント、およびマージ エージェント用の追加の定義済みプロファイルが利用できます。 提供されているプロファイルに加えて、アプリケーションの要件に合わせてプロファイルを作成することもできます。 エージェント プロファイルを利用すると、そのプロファイルに関連付けられたすべてのエージェントの主要なパラメーターを簡単に変更できます。 たとえば、20 個のスナップショット エージェントがあり、クエリのタイムアウト値 ( **-QueryTimeout** パラメーター) を変更する場合は、スナップショット エージェントが使用するプロファイルを更新すれば、関連付けられたすべてのエージェントが次回の実行時から自動的に新しい値を使用します。  
  
 1 つのエージェントの別々のインスタンスに対して、別々のプロファイルを設定することもできます。 たとえば、ダイヤルアップ接続を介してパブリッシャーおよびディストリビューターに接続するマージ エージェントは、 **低速リンク** プロファイルを使用して低速の通信リンクに適したパラメーター セットを使用することができます。  
  
> [!NOTE]  
>  コマンド ラインでエージェント パラメーターの値を指定した場合、その値はエージェント プロファイルの同じパラメーターの設定値をオーバーライドします。  
  
 **エージェント プロファイルを使用および変更するには**  
  
-   [レプリケーション エージェント プロファイルの操作](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
## <a name="snapshot-agent-profiles"></a>スナップショット エージェント プロファイル  
 次の表は、スナップショット エージェントの既定のプロファイルに定義されているパラメーターを示しています。 これらのパラメーターの詳細については、「 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)」を参照してください。  
  
||既定値 (default)|  
|-|-------------|  
|**-BcpBatchSize**|100000|  
|**-HistoryVerboseLevel**|2|  
|**-LoginTimeout**|15|  
|**-QueryTimeout**|1800|  
  
## <a name="log-reader-agent-profiles"></a>ログ リーダー エージェント プロファイル  
 次の表は、ログ リーダー エージェントのプロファイルに定義されているパラメーターを示しています。 表の各列は名前付きプロファイルを表しています。 これらのパラメーターの詳細については、「 [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)」を参照してください。  
  
||既定値 (default)|詳細履歴|  
|-|-------------|---------------------|  
|**-HistoryVerboseLevel**|1|2|  
|**-LoginTimeout**|15|15|  
|**-LogScanThreshold**|500000|500000|  
|**-PollingInterval**|5|5|  
|**-QueryTimeout**|1800|1800|  
|**-ReadBatchSize**|500|500|  
  
## <a name="distribution-agent-profiles"></a>ディストリビューション エージェント プロファイル  
 次の表は、ディストリビューション エージェントのプロファイルに定義されているパラメーターを示しています。 表の各列は名前付きプロファイルを表しています。 これらのパラメーターの詳細については、「 [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)」を参照してください。  
  
||既定値 (default)|詳細履歴|Windows 同期マネージャー|データ一貫性エラー時続行|OLE DB ストリーム用ディストリビューション プロファイル|  
|-|-------------|---------------------|-------------------------------------|-----------------------------------------|----------------------------------------------|  
|**-BcpBatchSize**|100000|100000|1000|100000|2147473647|  
|**-CommitBatchSize**|100|100|100|100|100|  
|**-CommitBatchThreshold**|1000|1000|1000|1000|1000|  
|**-HistoryVerboseLevel**|1|2|1|1|1|  
|**-KeepAliveMessageInterval**|300|300|300|300|300|  
|**-LoginTimeout**|15|15|15|15|15|  
|**-MaxBcpThreads**|1|1|1|1|1|  
|**-MaxDeliveredTransactions**|0|0|0|0|0|  
|**-OledbStreamThreshold**|NULL|NULL|NULL|NULL|32768|  
|**-PacketSize**|NULL|NULL|NULL|NULL|32768|  
|**-PollingInterval**|5|5|5|5|5|  
|**-QueryTimeout**|1800|1800|1800|1800|1800|  
|**-SkipErrors**|NULL|NULL|NULL|**-SkipErrors** 2601:2627:20598|NULL|  
|**-TransactionsPerHistory**|100|100|100|100|100|  
|**-UseOledbStreaming**|NULL|NULL|NULL|NULL|**-UseOledbStreaming**|  
  
## <a name="merge-agent-profiles"></a>マージ エージェント プロファイル  
 次の表は、マージ エージェントのプロファイルに定義されているパラメーターを示しています。 表の各列は名前付きプロファイルを表しています。 これらのパラメーターの詳細については、「 [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)」を参照してください。  
  
||既定値 (default)|詳細履歴|Windows 同期マネージャー|行数検証|行数とチェックサム検証|低速リンク|高ボリューム サーバー間|  
|-|-------------|---------------------|-------------------------------------|-------------------------|--------------------------------------|---------------|------------------------------------|  
|**-BcpBatchSize**|100000|100000|1000|100000|100000|100000|100000|  
|**-ChangesPerHistory**|100|50|50|100|100|100|1000|  
|**-DestThreads**|2|1|1|1|1|1|4|  
|**-DownloadGenerationsPerBatch**|50|50|50|50|50|1|500|  
|**-DownloadReadChangesPerBatch**|100|100|100|100|100|100|100|  
|**-DownloadWriteChangesPerBatch**|100|100|100|100|100|100|100|  
|**-FastRowCount**|1|1|1|1|1|1|1|  
|**-HistoryVerboseLevel**|2|3|1|1|2|1|2|  
|**-KeepAliveMessageInterval**|300|300|300|300|300|300|300|  
|**-LoginTimeout**|15|15|15|15|15|15|15|  
|**-MaxDownloadChanges**|0|0|0|0|0|0|0|  
|**-MaxUploadChanges**|0|0|0|0|0|0|0|  
|**-MetadataRetentionCleanup**|1|1|1|1|1|1|1|  
|**-NumDeadlockRetries**|5|5|5|5|5|5|5|  
|**-ParallelUploadDownload**|NULL|NULL|NULL|NULL|NULL|NULL|1|  
|**-PollingInterval**|60|60|60|60|60|60|60|  
|**-QueryTimeout**|300|300|300|300|300|300|600|  
|**-QueueSizeMultiplier**|NULL|NULL|NULL|NULL|NULL|NULL|5|  
|**-SrcThreads**|2|2|2|2|2|1|3|  
|**-StartQueueTimeout**|0|0|0|0|0|0|0|  
|**-UploadGenerationsPerBatch**|50|50|50|50|50|1|500|  
|**-UploadReadChangesPerBatch**|100|100|100|100|100|100|100|  
|**-UploadWriteChangesPerBatch**|100|100|100|100|100|100|100|  
|**-Validate**|0|0|0|1|3|0|0|  
|**-ValidateInterval**|60|60|60|60|60|60|60|  
  
## <a name="queue-reader-agent-profiles"></a>キュー リーダー エージェント プロファイル  
 次の表は、キュー リーダー エージェントの既定のプロファイルに定義されているパラメーターを示しています。 これらのパラメーターの詳細については、「 [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)」を参照してください。  
  
||既定値 (default)|  
|-|-------------|  
|**-HistoryVerboseLevel**|1|  
|**-LoginTimeout**|15|  
|**-PollingInterval**|5|  
|**-QueryTimeout**|1800|  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェントの管理](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [レプリケーション エージェント コマンド プロンプト パラメーターを表示および変更する &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)   
 [Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
  
