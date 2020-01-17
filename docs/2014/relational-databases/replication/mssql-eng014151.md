---
title: MSSQL_ENG014151 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014151 error
ms.assetid: 54b45e70-46b3-4c7a-a5bf-06f6dd028ceb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1f292841c227db26f1c518b2eaef896f7ce3570c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63191461"
---
# <a name="mssqleng014151"></a>MSSQL_ENG014151
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|14151|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|レプリケーション-%s: エージェント %s は失敗しました。 %s|  
  
## <a name="explanation"></a>説明  
 このエラーは、すべてのレプリケーション エージェントのエラーに対して発生します。 メッセージの最後のテキストは、エラーのコンテキストに依存します。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーはさまざまな状況で発生します。必要に応じて、以下の方法を使用してください。  
  
-   失敗したエージェントを再起動し、問題なく実行されるかどうかを確認します。 詳細については、「[レプリケーション エージェントを起動および停止する &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)」および「[レプリケーション エージェント実行可能ファイルの概念](concepts/replication-agent-executables-concepts.md)」を参照してください。  
  
-   エージェント履歴およびジョブ履歴を参照し、同時期に発生したその他のエラーを確認します。 レプリケーション モニターでのエージェントの状態やエラーの詳細の表示について詳しくは、「[レプリケーション モニターを使用して情報を表示し、タスクを実行する](monitor/view-information-and-perform-tasks-replication-monitor.md)」を参照してください。  
  
-   エージェントがアクセスするコンピューター間で基本的な接続が機能していることを確認し、 [sqlcmd Utility](../../tools/sqlcmd-utility.md)などのユーティリティにより各コンピューターを接続します。 接続の際には、エージェントが接続に使用するものと同じアカウントを使用します。 各エージェント アカウントで必要な権限の詳細については、「 [Replication Agent Security Model](security/replication-agent-security-model.md)」を参照してください。  
  
-   スナップショットの作成中または適用中にエラーが発生した場合は、スナップショット ディレクトリのファイルにエラーがないかどうかを確認します。  
  
-   エラーの発生が継続する場合は、エージェントのログ記録を増やし、ログの出力ファイルを指定します。 エラーのコンテキストによっては、エラーや他のエラー メッセージにつながる手順が示される可能性もあります。  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェントの管理](agents/replication-agent-administration.md)   
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](errors-and-events-reference-replication.md)   
 [レプリケーション ディストリビューション エージェント](agents/replication-distribution-agent.md)   
 [レプリケーション ログ リーダー エージェント](agents/replication-log-reader-agent.md)   
 [レプリケーション マージ エージェント](agents/replication-merge-agent.md)   
 [レプリケーション キュー リーダー エージェント](agents/replication-queue-reader-agent.md)   
 [レプリケーション スナップショット エージェント](agents/replication-snapshot-agent.md)  
  
  
