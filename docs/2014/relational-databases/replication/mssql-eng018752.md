---
title: MSSQL_ENG018752 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG018752 error
ms.assetid: 405b2655-acb4-4e15-bcc6-b8f86bb22b37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0558ded6ed10284df39270ddeca9d92434daf40e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63057545"
---
# <a name="mssqleng018752"></a>MSSQL_ENG018752
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|18752|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|同時にデータベースに接続できるログ リーダー エージェントまたはログ関連のプロシージャ (sp_repldone、sp_replcmds、および sp_replshowcmds) は 1 つだけです。 ログ関連のプロシージャを実行した場合、そのプロシージャが実行された接続を削除するか、その接続に対して sp_replflush を実行してから、ログ リーダー エージェントを開始するか、別のログ関連のプロシージャを実行してください。|  
  
## <a name="explanation"></a>説明  
 複数の現在の接続が、 **sp_repldone**、 **sp_replcmds**、 **sp_replshowcmds**のいずれかを実行しようとしています。 ストアド プロシージャの [sp_repldone &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-repldone-transact-sql) と [sp_replcmds &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replcmds-transact-sql) は、パブリッシュされたデータベース内のレプリケートされたトランザクションに関する情報を検索および更新するために、ログ リーダー エージェントによって使用されるストアド プロシージャです。 ストアド プロシージャ [sp_replshowcmds &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql) は、トランザクション レプリケーションに関する特定のタイプの問題点に対するトラブルシューティングを行うために使用されます。  
  
 このエラーは、次の状況で発生します。  
  
-   パブリッシュされたデータベースのログ リーダー エージェントが実行されており、2 番目のログ リーダー エージェントの実行を同じデータベースに対して試みた場合、2 番目のエージェントに対してエラーが発生し、エージェント履歴に表示されます。  
  
     複数のエージェントが存在する状況では、いずれかのエージェントは孤立したプロセスが原因の可能性があります。  
  
-   パブリッシュされたデータベースに対してログ リーダー エージェントが起動されており、ユーザーが **sp_repldone**、 **sp_replcmds**、または **sp_replshowcmds** を同じデータベースに対して実行する場合は、ストアド プロシージャ ( **sqlcmd**など) が実行されるとアプリケーションでエラーが発生します。  
  
-   パブリッシュされたデータベースに対してログ リーダー エージェントが実行されておらず、ユーザーが **sp_repldone**、 **sp_replcmds**、または **sp_replshowcmds** を実行してから、プロシージャを実行した接続を閉じない場合は、ログ リーダー エージェントによってデータベースへの接続が試行されるとエラーが発生します。  
  
## <a name="user-action"></a>ユーザーの操作  
 次の手順を実行して、この問題に対するトラブルシューティングに役立てることができます。 いずれかの手順によって、ログ リーダー エージェントをエラーを発生させないで起動できるようになった場合は、残りの手順を実行する必要はありません。  
  
-   このエラーの発生原因となる可能性があるその他のエラーについて、ログ リーダー エージェントの履歴を確認します。 レプリケーション モニターでのエージェントの状態やエラーの詳細の表示について詳しくは、「[レプリケーション モニターを使用して情報を表示し、タスクを実行する](monitor/view-information-and-perform-tasks-replication-monitor.md)」を参照してください。  
  
-   パブリッシュされたデータベースに接続されている特定のプロセス識別番号 (SPID) に対応する [sp_who &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql) の出力を確認します。 **sp_repldone**、 **sp_replcmds**、または **sp_replshowcmds**を実行していた可能性のある接続をすべて閉じます。  
  
-   ログ リーダー エージェントを再起動します。 詳細については、「[レプリケーション エージェントを起動および停止する &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)」を参照してください。  
  
-   ディストリビューターで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを再起動します (クラスター内でオフラインまたはオンラインにします)。 スケジュールされたジョブがその他の **インスタンスから**sp_repldone **、** sp_replcmds **、または** sp_replshowcmds [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行した可能性がある場合は、これらのインスタンスに対しても [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを再起動します。 詳細については、「[SQL Server エージェント サービスの開始、停止、または一時停止](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)」を参照してください。  
  
-   パブリケーション データベース上のパブリッシャーで [sp_replflush &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replflush-transact-sql) を実行してから、ログ リーダー エージェントを再起動します。  
  
-   エラーの発生が継続する場合は、エージェントのログ記録を増やし、ログの出力ファイルを指定します。 エラーのコンテキストによっては、エラーや他のエラー メッセージにつながる手順が示される可能性もあります。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](errors-and-events-reference-replication.md)   
 [レプリケーション ログ リーダー エージェント](agents/replication-log-reader-agent.md)  
  
  
