---
title: MSSQL_ENG014150 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014150 error
ms.assetid: c3dd3109-abf3-4b38-a4e9-ef48d0235656
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 74e43b8d816fe2cfdbf9d35ea1815517f186b736
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68766224"
---
# <a name="mssqleng014150"></a>MSSQL_ENG014150
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|14150|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|レプリケーション-%s: エージェント %s が成功しました。 %s|  
  
## <a name="explanation"></a>説明  
 このメッセージは、レプリケーション エージェントの実行が正常に完了したことを示しています。 レプリケーションでは、次のエージェントを使用します。  
  
-   スナップショット エージェント。 すべてのパブリケーションで使用されます。  
  
-   ログ リーダー エージェント。 すべてのトランザクション パブリケーションで使用されます。  
  
-   キュー リーダー エージェント。 キュー更新サブスクリプションに有効なトランザクション パブリケーションで使用されます。  
  
-   ディストリビューション エージェント。 サブスクリプションをトランザクション パブリケーションおよびスナップショット パブリケーションと同期します。  
  
-   マージ エージェント。 サブスクリプションをマージ パブリケーションと同期します。  
  
-   レプリケーション メンテナンス ジョブ。  
  
## <a name="user-action"></a>ユーザーの操作  
 通常、ログ リーダー エージェント、キュー リーダー エージェント、およびディストリビューション エージェントは連続実行しますが、他のエージェントは、要求時に実行するかスケジュールに合わせて実行します。 エージェントが実行を完了したかどうかわからない場合は、エージェントの状態を確認します。 詳細については、「[レプリケーション エージェントの監視](../../relational-databases/replication/monitor/monitor-replication-agents.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェントの管理](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [レプリケーション ディストリビューション エージェント](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [レプリケーション ログ リーダー エージェント](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [レプリケーション マージ エージェント](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [レプリケーション キュー リーダー エージェント](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [レプリケーション スナップショット エージェント](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
