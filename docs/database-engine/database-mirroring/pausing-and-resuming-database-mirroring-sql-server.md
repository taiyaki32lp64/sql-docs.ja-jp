---
title: データベース ミラーリングの一時停止と再開
description: SQL Server データベース ミラーリング セッションを任意の時点で一時停止して、後で再開する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- sessions [SQL Server], database mirroring
- resuming database mirroring
- database mirroring [SQL Server], pausing
- database mirroring [SQL Server], resuming
- pausing database mirroring
ms.assetid: c67802c6-ee8c-4cbd-a6d4-f7b80413a4ab
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b6a46805e9dfe86d7560a2786f10a99b66344a97
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75254153"
---
# <a name="pausing-and-resuming-database-mirroring-sql-server"></a>データベース ミラーリングの一時停止と再開 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  データベースの所有者は、データベース ミラーリング セッションを任意の時点で一時停止し、後から再開できます。 一時停止では、ミラーリングは中断しますが、セッションの状態は保たれます。 一時停止は、ボトルネックの発生中にプリンシパル サーバーのパフォーマンスを向上させる場合に役立ちます。  
  
 セッションが一時停止されても、プリンシパル データベースは引き続き使用できます。 一時停止によりミラーリング セッションの状態が一時中断に設定されるので、ミラー データベースがプリンシパル データベースの最新状態を反映しなくなり、プリンシパル データベースが危険に曝されることになります。  
  
 一時停止したセッションはすぐに再開することをお勧めします。データベース ミラーリング セッションが一時停止している間は、トランザクション ログの切り捨てが実行されないからです。 したがって、データベース ミラーリング セッションが長時間一時停止になっていると、トランザクション ログがいっぱいになり、データベースを利用できなくなります。 原因の詳細については、このトピックの「一時停止および再開がログ切り捨てに与える影響」を参照してください。  
  
> [!IMPORTANT]  
>  強制されたサービスに続いて元のプリンシパル サーバーが再接続されると、ミラーリングが中断されます。 この状況でミラーリングを再開すると、元のプリンシパル サーバーのデータが失われる可能性があります。 データ損失の可能性への対処の詳細については、「 [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)」を参照してください。  
  
 **このトピックの内容**  
  
-   [一時停止および再開がログ切り捨てに与える影響](#EffectOnLogTrunc)  
  
-   [トランザクション ログがいっぱいになった状態の回避](#AvoidFullLog)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="EffectOnLogTrunc"></a> 一時停止および再開がログ切り捨てに与える影響  
 通常、データベースで自動チェックポイントが実行されている場合は、次のログ バックアップの後、そのチェックポイントまでトランザクション ログが切り捨てられます。 データベース ミラーリング セッションが一時停止している間は、プリンシパル サーバーがミラー サーバーへのログ レコードの送信待ち状態になるため、現在のログ レコードがすべてアクティブなまま保持されます。 セッションが再開されてプリンシパル サーバーがログ レコードをミラー サーバーに送信するまでの間、未送信のログ レコードがプリンシパル データベースのトランザクション ログに蓄積されます。  
  
 セッションが再開されると、プリンシパル サーバーは蓄積されたログ レコードを直ちにミラー サーバーに送信し始めます。 ミラー サーバーが最も古い自動チェックポイントに対応するログ レコードをキューに格納したことを確認したら、プリンシパル サーバーはプリンシパル データベースのログをそのチェックポイントまで切り捨てます。 ミラー サーバーは同じログ レコードの再実行キューを切り捨てます。 連続する各チェックポイントでこのプロセスが繰り返されるため、チェックポイントごとに段階的にログが切り捨てられます。  
  
> [!NOTE]  
>  チェックポイントおよびログ切り捨ての詳細については、「[データベース チェックポイント &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)」を参照してください。  
  
##  <a name="AvoidFullLog"></a> トランザクション ログがいっぱいになった状態の回避  
 最大サイズに到達したか、サーバー インスタンスの領域が不足して、ログがいっぱいになると、データベースではそれ以上の更新を実行できません。 この問題を防ぐには、次の 2 つの方法があります。  
  
-   ログがいっぱいになる前に、データベース ミラーリング セッションを再開します。またはログ領域を増やします。 データベース ミラーリングを再開すると、累積されたアクティブなログがプリンシパル サーバーからミラー サーバーに送信され、ミラー データベースが同期中の状態になります。 次に、ミラー サーバーがログをディスクに固定し、再実行を開始します。  
  
-   ミラー化を解除して、データベース ミラーリング セッションを停止します。  
  
     セッションの一時停止とは異なり、ミラー化を解除することにより、ミラーリング セッションに関するすべての情報が削除されます。 各パートナー サーバー インスタンスでは、データベースの独自のコピーが保持されます。 以前のミラー コピーを復旧した場合、そのコピーは以前のプリンシパル コピーから派生し、セッションが一時停止されてから経過した時間だけ遅延が生じたものになります。 詳細については、「 [データベース ミラーリングの削除 &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)」を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **データベース ミラーリングを一時停止または再開するには**  
  
-   [データベース ミラーリング セッションを一時停止または再開する &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/pause-or-resume-a-database-mirroring-session-sql-server.md)  
  
 **データベース ミラーリングを停止するには**  
  
-   [データベース ミラーリングを削除する &#40;SQL Server&#41;](../../database-engine/database-mirroring/remove-database-mirroring-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [データベース ミラーリングの削除 &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)  
  
  
