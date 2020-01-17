---
title: MSSQL_ENG020557 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020557 error
ms.assetid: c43c6952-5b60-4347-b881-11a0004dce24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6816a0301a03e2c0d01cfe78a5c88213394c445b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63057112"
---
# <a name="mssqleng020557"></a>MSSQL_ENG020557
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|20557|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|エージェントがシャットダウンされました。 詳細については、ジョブ '%s' の SQL Server エージェントのジョブ履歴を参照してください。|  
  
## <a name="explanation"></a>説明  
 レプリケーション エージェントは、原因を適切な履歴テーブルに書き込むことなくシャットダウンされました。つまり、このエージェントは処理の途中でシャットダウンされました。  
  
## <a name="user-action"></a>ユーザーの操作  
  
-   エージェントを再起動し、問題なく実行されるかどうかを確認します。 詳細については、「[レプリケーション エージェントを起動および停止する &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)」および「[レプリケーション エージェント実行可能ファイルの概念](concepts/replication-agent-executables-concepts.md)」を参照してください。  
  
-   エージェント履歴およびジョブ履歴を参照し、同時期に発生したその他のエラーを確認します。 レプリケーション モニターでエージェントの状態やエラーの詳細を表示する方法については、「[レプリケーション モニターを使用して情報を表示し、タスクを実行する](monitor/view-information-and-perform-tasks-replication-monitor.md)」を参照してください。
-   エージェントがアクセスするコンピューター間で基本的な接続が機能していることを確認し、 **sqlcmd** ユーティリティなどのユーティリティを使用して各コンピューターに接続します。 接続時には、エージェントが接続に使用するものと同じアカウントを使用します。 各エージェント アカウントで必要な権限の詳細については、「 [Replication Agent Security Model](security/replication-agent-security-model.md)」を参照してください。  
  
-   スナップショットの作成中または適用中にエラーが発生した場合は、スナップショット ディレクトリのファイルにエラーがないかどうかを確認します。  
  
-   エラーの発生が継続する場合は、エージェントのログ記録を増やし、ログの出力ファイルを指定します。 エラーのコンテキストによっては、エラーや他のエラー メッセージを発生させる手順が示される場合もあります。 レプリケーションのログ記録を構成する方法については、サポート技術情報の資料 [312292](https://support.microsoft.com/kb/312292)を参照してください。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](errors-and-events-reference-replication.md)  
  
  
