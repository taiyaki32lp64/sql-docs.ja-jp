---
title: サーバーのポーリング | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- target servers [SQL Server], polling interval
- polling master servers [SQL Server]
- server polling [SQL Server]
- master servers [SQL Server], polling
- polling interval [SQL Server]
ms.assetid: 96f5fd43-3edd-4418-9dd0-4d34e618890e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ae75dc8af9364a619113d2c38071a441e15351be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63062210"
---
# <a name="poll-servers"></a>サーバーのポーリング
  マルチサーバー管理を実装している場合、ターゲット サーバーからマスター サーバーに定期的にアクセスし、既に実行したジョブの情報をアップロードして新しいジョブをダウンロードします。 マスター サーバーにアクセスする処理は *サーバー ポーリング* と呼ばれ、定期的な *ポーリング間隔*で行われます。  
  
## <a name="polling-intervals"></a>ポーリング間隔  
 ターゲット サーバーからマスター サーバーに接続し、命令をダウンロードしてジョブの実行結果をアップロードする頻度をポーリング間隔 (既定値は 1 分) で制御します。  
  
 ターゲット サーバーからマスター サーバーにポーリングするとき、ターゲット サーバーに割り当てられる操作を **msdb** データベースの **sysdownloadlist** テーブルから読み取ります。 読み取った操作により、マルチサーバー ジョブやターゲット サーバーのさまざまな動作を制御します。 操作の例には、ジョブの削除、ジョブの挿入、ジョブの開始、ターゲット サーバーのポーリング間隔の更新などがあります。  
  
 操作は次のいずれかの方法で **sysdownloadlist** テーブルに書き込まれます。  
  
-   **sp_post_msx_operation** ストアド プロシージャを使用して明示的に行います。  
  
-   他のジョブ ストアド プロシージャを使用して暗黙的に行います。  
  
 ジョブ ストアド プロシージャを使用してマルチサーバー ジョブ スケジュールやジョブ ステップを変更する場合、または SQL-DMO (SQL 分散管理オブジェクト) を使用してマルチサーバー ジョブを制御する場合、マルチサーバー ジョブのステップやスケジュールを変更してから次のコマンドを実行します。  
  
```  
EXECUTE msdb.dbo.sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
 このコマンドを実行すると、現在のジョブ定義がターゲット サーバーと同期されます。  
  
 次の場合、操作を明示的に書き込む必要はありません。  
  
-   Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してマルチサーバー ジョブを制御する場合。  
  
-   ジョブ スケジュールまたはジョブ ステップを変更しないジョブ ストアド プロシージャの場合。  
  
 **対象サーバーからマスター サーバーにポーリングさせるには**  
  
-   [SQL Server Management Studio](force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql)  
  
## <a name="see-also"></a>参照  
 [イベントの管理](manage-events.md)  
  
  
