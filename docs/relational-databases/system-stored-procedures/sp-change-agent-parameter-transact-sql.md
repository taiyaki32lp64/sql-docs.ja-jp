---
title: sp_change_agent_parameter (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_change_agent_parameter_TSQL
- sp_change_agent_parameter
helpviewer_keywords:
- sp_change_agent_parameter
ms.assetid: f1fbecc7-e64f-405c-8067-6b38c1f3c0a0
author: stevestein
ms.author: sstein
ms.openlocfilehash: cd737be5a1e71e46750f6c80fd68ad254cb6436f
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768944"
---
# <a name="spchangeagentparameter-transact-sql"></a>sp_change_agent_parameter (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  [MSagent_parameters](../../relational-databases/system-tables/msagent-parameters-transact-sql.md)システムテーブルに格納されているレプリケーションエージェントプロファイルのパラメーターを変更します。 このストアドプロシージャは、任意のデータベース上でエージェントが実行されているディストリビューターで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_change_agent_parameter [ @profile_id= ] profile_id, [ @parameter_name= ] 'parameter_name', [ @parameter_value= ] 'parameter_value'  
```  
  
## <a name="arguments"></a>引数  
`[ @profile_id = ] profile_id,`プロファイルの ID を示します。 *profile_id*は**int**,、既定値はありません。  
  
`[ @parameter_name = ] 'parameter_name'`パラメーターの名前を指定します。 *parameter_name*は**sysname**,、既定値はありません。 システムプロファイルの場合、変更可能なパラメーターはエージェントの種類によって異なります。 この*profile_id*が表すエージェントの種類を確認するには、 **Msagent_profiles**テーブルで*profile_id*列を見つけ、 *agent_type*値をメモします。  
  
> [!NOTE]  
>  パラメーターが特定の*agent_type*に対してサポートされていても、エージェントプロファイルで定義されていない場合は、エラーが返されます。 エージェントプロファイルにパラメーターを追加するには、 [sp_add_agent_parameter](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)を実行する必要があります。  
  
 スナップショットエージェント (*agent_type*=**1**) の場合、プロファイルで定義されている場合、次のプロパティを変更できます。  
  
-   **70Subscribers**  
  
-   **BcpBatchSize**  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **MaxBcpThreads**  
  
-   **MaxNetworkOptimization**  
  
-   **出力**  
  
-   **OutputVerboseLevel**  
  
-   **PacketSize**  
  
-   **QueryTimeout**  
  
-   **StartQueueTimeout**  
  
-   **UsePerArticleContentsView**  
  
 ログリーダーエージェント (*agent_type*=**2**) の場合、プロファイルで定義されている場合、次のプロパティを変更できます。  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **MessageInterval**  
  
-   **出力**  
  
-   **OutputVerboseLevel**  
  
-   **PacketSize**  
  
-   **PollingInterval**  
  
-   **QueryTimeout**  
  
-   **ReadBatchSize**  
  
-   **ReadBatchThreshold**  
  
 ディストリビューションエージェント (*agent_type*=**3**) の場合、プロファイルで定義されている場合、次のプロパティを変更できます。  
  
-   **BcpBatchSize**  
  
-   **CommitBatchSize**  
  
-   **CommitBatchThreshold**  
  
-   **FileTransferType**  
  
-   **HistoryVerboseLevel**  
  
-   **Keep、Vemessageinterval**  
  
-   **LoginTimeout**  
  
-   **MaxBcpThreads**  
  
-   **MaxDeliveredTransactions**  
  
-   **MessageInterval**  
  
-   **出力**  
  
-   **OutputVerboseLevel**  
  
-   **PacketSize**  
  
-   **PollingInterval**  
  
-   **QueryTimeout**  
  
-   **QuotedIdentifier**  
  
-   **SkipErrors**  
  
-   **TransactionsPerHistory**  
  
 マージエージェント (*agent_type*=**4**) の場合、プロファイルで定義されている場合、次のプロパティを変更できます。  
  
-   **AltSnapshotFolder**  
  
-   **BcpBatchSize**  
  
-   **すべての履歴**  
  
-   **DestThreads**  
  
-   **DownloadGenerationsPerBatch**  
  
-   **Downloadreadの Perbatch**  
  
-   **DownloadWriteChangesPerBatch**  
  
-   **DynamicSnapshotLocation**  
  
-   **ExchangeType**  
  
-   **FastRowCount**  
  
-   **FileTransferType**  
  
-   **GenerationChangeThreshold**  
  
-   **HistoryVerboseLevel**  
  
-   **InputMessageFile**  
  
-   **相互に対話のための方法**  
  
-   **InterruptOnMessagePattern**  
  
-   **Keep、Vemessageinterval**  
  
-   **LoginTimeout**  
  
-   **MaxBcpThreads**  
  
-   **MaxDownloadChanges**  
  
-   **MaxUploadChanges**  
  
-   **MetadataRetentionCleanup**  
  
-   **NumDeadlockRetries**  
  
-   **出力**  
  
-   **OutputMessageFile**  
  
-   **OutputVerboseLevel**  
  
-   **PacketSize**  
  
-   **ParallelUploadDownload**  
  
-   **PauseOnMessagePattern**  
  
-   **PauseTime**  
  
-   **PollingInterval**  
  
-   **ProcessMessagesAtPublisher**  
  
-   **ProcessMessagesAtSubscriber**  
  
-   **QueryTimeout**  
  
-   **QueueSizeMultiplier**  
  
-   **SrcThreads**  
  
-   **StartQueueTimeout**  
  
-   **SyncToAlternate**  
  
-   **UploadGenerationsPerBatch**  
  
-   **UploadReadChangesPerBatch**  
  
-   **UploadWriteChangesPerBatch**  
  
-   **UseInprocLoader**  
  
-   **[検証]**  
  
-   **ValidateInterval**  
  
 キューリーダーエージェント (*agent_type*=**9**) の場合、プロファイルで定義されている場合、次のプロパティを変更できます。  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **出力**  
  
-   **OutputVerboseLevel**  
  
-   **PollingInterval**  
  
-   **QueryTimeout**  
  
-   **ResolverState**  
  
-   **SQLQueueMode**  
  
 特定のプロファイルに対して定義されているパラメーターを確認するには、 **sp_help_agent_profile**を実行し、 *profile_id*に関連付けられている*profile_name*を確認します。 適切な*profile_id*を使用して、次にその*profile_id*を使用して**sp_help_agent_parameters**を実行し、プロファイルに関連付けられているパラメーターを確認します。 パラメーターをプロファイルに追加するには、 [sp_add_agent_parameter](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)を実行します。  
  
`[ @parameter_value = ] 'parameter_value'`パラメーターの新しい値を指定します。 *parameter_value*は**nvarchar (255)** ,、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_change_agent_parameter**は、すべての種類のレプリケーションで使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_change_agent_parameter**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション エージェント プロファイル](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [レプリケーション ディストリビューション エージェント](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [レプリケーション ログ リーダー エージェント](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [レプリケーション マージ エージェント](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [レプリケーション キュー リーダー エージェント](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)   
 [sp_add_agent_parameter &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_drop_agent_parameter &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_help_agent_parameter &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
