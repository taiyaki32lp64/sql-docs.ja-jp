---
title: サブスクリプション、未配布のコマンド (トランザクション サブスクリプション、SQL Server 2005 以降) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.subscription.performance.f1
ms.assetid: 5451561e-0ce3-4bb5-844a-88cd15b0b371
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a1f957c417c5c63766dfbffa923edd6935d1eb5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151481"
---
# <a name="subscription-undistributed-commands-transactional-subscription-sql-server-2005-and-later"></a>サブスクリプション、[未配布のコマンド] (トランザクション サブスクリプション、SQL Server 2005 以降)
  **[未配布のコマンド]** タブには、ディストリビューション データベース内のコマンドで、選択したサブスクライバーにまだ配布されていないコマンドの数や、これらのコマンドを配布するのに要すると推定される時間についての情報が表示されます。 ディストリビューション データベース内のコマンドを表示する方法については、「[sp_replshowcmds &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql)」を参照してください。  
  
## <a name="options"></a>および  
 **[このサブスクライバーへの適用を待機しているディストリビューション データベース内のコマンド数]**  
 ディストリビューション データベース内のコマンドで、選択したサブスクライバーにまだ配布されていないコマンドの数を示します。 コマンドは、1 つの Transact-SQL データ操作言語 (DML) ステートメントまたは 1 つのデータ定義言語 (DDL) ステートメントから構成されます。  
  
 **[以前のパフォーマンスに基づく、これらのコマンドの適用にかかる推定時間]**  
 コマンドをサブスクライバーに配布するのに要すると推定される時間を示します。 スナップショットを生成してサブスクライバーに適用するのに必要な時間よりもこの値が大きい場合は、サブスクライバーの再初期化を検討してください。 詳細については、「 [サブスクリプションの再初期化](reinitialize-subscriptions.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション モニターの開始](monitor/start-the-replication-monitor.md)   
 [レプリケーション モニターを使用したパフォーマンスの監視](monitor/monitor-performance-with-replication-monitor.md)   
 [レプリケーションの監視](monitoring-replication.md)  
  
  
