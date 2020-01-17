---
title: レプリケートされたコマンドとディストリビューション データベースの情報の表示
description: レプリケートされたコマンドなど、SQL Server のディストリビューション データベースに格納されているレプリケーション関連情報を表示する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine
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
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 5ef4e316e27ddd77ee126549e21fc3e5efb988cd
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322215"
---
# <a name="view-replicated-commands-and-information-in-distribution-database"></a>レプリケートされたコマンドとディストリビューション データベースの情報の表示
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  トランザクション レプリケーションでは、トランザクション コマンドが、ディストリビューション エージェントによってすべてのサブスクライバーに反映されるか、サブスクライバーのディストリビューション エージェントによって変更が抽出されるまで、ディストリビューション データベースに格納されます。 ディストリビューション データベース内で保留状態のコマンドは、レプリケーションのストアド プロシージャを使用してプログラムから表示できます。 詳細については、「[Replication Stored Procedures &#40;Transact-SQL&#41; (レプリケーションのストアド プロシージャ &#40;Transact-SQL&#41;)](../../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)」を参照してください。  
  
### <a name="to-view-replicated-commands-from-all-transactional-publications-in-the-distribution-database"></a>すべてのトランザクション パブリケーションからディストリビューション データベース内のレプリケートされたコマンドを表示するには  
  
1.  ディストリビューターのディストリビューション データベースで [sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md)を実行します。  
  
### <a name="to-view-replicated-commands-in-the-distribution-database-from-a-specific-article-or-from-a-specific-database-published-using-transactional-replication"></a>トランザクション レプリケーションを使用してパブリッシュされた特定のアーティクルまたは特定のデータベースから、ディストリビューション データベース内のレプリケートされたコマンドを表示するには  
  
1.  (省略可) パブリッシャーのパブリケーション データベースで [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)を実行します。 `@publication` および `@article` を指定します。 結果セットの **article id** の値を確認します。  
  
2.  ディストリビューターのディストリビューション データベースで [sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md)を実行します。 (省略可) 手順 2 のアーティクル ID を `@article_id` に指定します。 (省略可) パブリケーション データベースの ID を `@publisher_database_id` に指定します。この ID は、[sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) カタログ ビューの **database_id** 列で確認できます。  
  
## <a name="see-also"></a>参照  
 [プログラムによるレプリケーションの監視](../../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
