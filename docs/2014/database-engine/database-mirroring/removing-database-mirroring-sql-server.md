---
title: データベース ミラーリングの削除 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], removing
- stopping database mirroring [SQL Server]
- removing database mirroring [SQL Server]
ms.assetid: 40c72091-8f03-4037-8b55-5e95309fe145
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 414cdedb8f2bc3dee4edc792c11b6438306818c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754542"
---
# <a name="removing-database-mirroring-sql-server"></a>データベース ミラーリングの削除 (SQL Server)
  データベース所有者は、いずれのパートナーでもデータベース ミラーリング セッションをいつでも手動で停止できます。  
  
## <a name="impact-of-removing-mirroring"></a>ミラーリングの削除による影響  
 ミラーリングが削除されると、次のような動作が発生します。  
  
-   パートナー間および各パートナーとミラーリング監視サーバー間にリレーションシップがある場合、それらのリレーションシップが完全に解除されます。  
  
     セッションが停止した時点でパートナーどうしが通信している場合、そのリレーションシップは両方のコンピューターですぐに解除されます。 パートナーどうしが通信していない場合、つまり停止時点でデータベースが DISCONNECTED 状態である場合は、ミラーリング停止処理を実行した側のパートナーではリレーションシップがすぐに解除されます。もう一方のパートナーは、再接続を試行したときに、データベース ミラーリング セッションが停止していることがわかります。  
  
-   セッションの一時停止の場合と異なり、ミラーリング セッションについての情報は削除されます。 ミラーリングは、プリンシパル データベースとミラー データベースの両方から削除されます。 **sys.databases** では、**mirroring_state** 列およびその他すべてのミラー化に関する列が NULL に設定されます。 詳細については、「[sys.database_mirroring &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql)」を参照してください。  
  
-   各パートナー サーバー インスタンスには、データベースの個別のコピーが保持されます。  
  
-   ミラー データベースは復元中の状態になります ( **sys.databases** の **state**列を参照)。これは、ミラー データベースが RESTORE WITH NORECOVERY を使用して作成されているためです。 この時点で、古いミラー データベースを削除するか、WITH RECOVERY を使用して復元できます。 データベースを復元すると、古いプリンシパル データベースから分岐が行われます。これは、復旧によって新しい復旧分岐が開始されるためです。  
  
> [!NOTE]  
>  セッション停止後もミラー化を続行するには、新しいデータベース ミラーリング セッションを確立する必要があります。 ミラー化の停止後にログ バックアップを作成する場合は、ミラー化を再開する前にミラー データベースにそのログ バックアップを適用する必要があります。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **データベース ミラーリングを削除するには**  
  
-   [データベース ミラーリングを削除する &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
 **データベース ミラーリングを開始するには**  
  
-   [Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Windows 認証を使用してデータベース ミラーリング セッションを確立する方法 &#40;Transact-SQL&#41;](database-mirroring-establish-session-windows-authentication.md)  
  

  
## <a name="see-also"></a>参照  
 [ALTER DATABASE Database Mirroring &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [データベース ミラーリング &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [データベース ミラーリングの一時停止と再開 &#40;SQL Server&#41;](pausing-and-resuming-database-mirroring-sql-server.md)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
