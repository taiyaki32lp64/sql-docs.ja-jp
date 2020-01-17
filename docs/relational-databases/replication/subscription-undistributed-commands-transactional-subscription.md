---
title: サブスクリプション、[未配布のコマンド] (トランザクション サブスクリプション) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.subscription.performance.f1
ms.assetid: 5451561e-0ce3-4bb5-844a-88cd15b0b371
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 48a5742ab40b9b3f4a210b16939caddaf6fa3ed6
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769420"
---
# <a name="subscription-undistributed-commands-transactional-subscription"></a>サブスクリプション、[未配布のコマンド]\(トランザクション サブスクリプション)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **[未配布のコマンド]** タブには、ディストリビューション データベース内のコマンドで、選択したサブスクライバーにまだ配布されていないコマンドの数や、これらのコマンドを配布するのに要すると推定される時間についての情報が表示されます。 ディストリビューション データベース内のコマンドを表示する方法については、「[sp_replshowcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md)」を参照してください。  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>オプション  
 **[このサブスクライバーへの適用を待機しているディストリビューション データベース内のコマンド数]**  
 ディストリビューション データベース内のコマンドで、選択したサブスクライバーにまだ配布されていないコマンドの数を示します。 コマンドは、1 つの Transact-SQL データ操作言語 (DML) ステートメントまたは 1 つのデータ定義言語 (DDL) ステートメントから構成されます。  
  
 **[以前のパフォーマンスに基づく、これらのコマンドの適用にかかる推定時間]**  
 コマンドをサブスクライバーに配布するのに要すると推定される時間を示します。 スナップショットを生成してサブスクライバーに適用するのに必要な時間よりもこの値が大きい場合は、サブスクライバーの再初期化を検討してください。 詳細については、「 [サブスクリプションの再初期化](../../relational-databases/replication/reinitialize-subscriptions.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [レプリケーション モニターの開始](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [レプリケーション モニターを使用したパフォーマンスの監視](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [レプリケーションの監視](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
