---
title: ディストリビューションデータベースにレプリケートされたコマンドおよびその他の情報を表示する (レプリケーション Transact-sql プログラミング) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_browsereplcmds
- transactional replication, monitoring
- distribution databases [SQL Server replication], viewing replicated commands
- viewing replicated commands
ms.assetid: 9c20acec-8fab-4483-b9c1-dfe3768f85dd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 86ced6fd281da2e47ddaa31cab7fa977767b98d6
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74164955"
---
# <a name="view-replicated-commands-and-other-information-in-the-distribution-database-replication-transact-sql-programming"></a>レプリケートされたコマンドなどディストリビューション データベースに格納されている情報を表示する (レプリケーション Transact-SQL プログラミング)
  トランザクション レプリケーションでは、トランザクション コマンドが、ディストリビューション エージェントによってすべてのサブスクライバーに反映されるか、サブスクライバーのディストリビューション エージェントによって変更が抽出されるまで、ディストリビューション データベースに格納されます。 ディストリビューション データベース内で保留状態のコマンドは、レプリケーションのストアド プロシージャを使用してプログラムから表示できます。 詳細については、「[Replication Stored Procedures &#40;Transact-SQL&#41; (レプリケーションのストアド プロシージャ &#40;Transact-SQL&#41;)](/sql/relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql)」を参照してください。  
  
### <a name="to-view-replicated-commands-from-all-transactional-publications-in-the-distribution-database"></a>すべてのトランザクション パブリケーションからディストリビューション データベース内のレプリケートされたコマンドを表示するには  
  
1.  ディストリビューターのディストリビューション データベースで [sp_browsereplcmds](/sql/relational-databases/system-stored-procedures/sp-browsemergesnapshotfolder-transact-sql)を実行します。  
  
### <a name="to-view-replicated-commands-in-the-distribution-database-from-a-specific-article-or-from-a-specific-database-published-using-transactional-replication"></a>トランザクション レプリケーションを使用してパブリッシュされた特定のアーティクルまたは特定のデータベースから、ディストリビューション データベース内のレプリケートされたコマンドを表示するには  
  
1.  (省略可) パブリッシャーのパブリケーション データベースで [sp_helparticle](/sql/relational-databases/system-stored-procedures/sp-helparticle-transact-sql)を実行します。 **\@パブリケーション**と **\@アーティクル**を指定します。 結果セットの **article id** の値を確認します。  
  
2.  ディストリビューターのディストリビューション データベースで [sp_browsereplcmds](/sql/relational-databases/system-stored-procedures/sp-browsemergesnapshotfolder-transact-sql)を実行します。 Optional **\@article_id**については、手順 2. のアーティクル ID を指定します。 Optional **\@publisher_database_id**のパブリケーションデータベースの ID を指定します。この ID は、[データベース](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)カタログビューの**database_id**列から取得できます。  
  
## <a name="see-also"></a>参照  
 [Programmatically Monitor Replication (プログラムによるレプリケーションの監視)](../monitoring-replication.md)  
  
  
