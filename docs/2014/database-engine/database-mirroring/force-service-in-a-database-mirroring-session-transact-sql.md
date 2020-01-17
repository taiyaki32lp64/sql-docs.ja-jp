---
title: データベース ミラーリング セッションでのサービスの強制 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- forced service [SQL Server]
- database mirroring [SQL Server], forcing service
ms.assetid: 8b6ffe77-35f3-4e2a-a658-8a38a8e1c794
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ef1a7101a0bd16c3ee2868f47a8dc15f29092621
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62806714"
---
# <a name="force-service-in-a-database-mirroring-session-transact-sql"></a>データベース ミラーリング セッションでのサービスの強制 (Transact-SQL)
  高パフォーマンス モードおよび自動フェールオーバーを伴わない高い安全性モードでは、ミラー サーバーが使用可能であるときにプリンシパル サーバーで障害が発生した場合、データベース所有者はサービスを強制的にミラー データベースにフェールオーバーして、データベースを直ちに使用可能な状態にできます (ただし、データが損失する場合があります)。 この方法は、次のすべての条件に一致する場合にのみ使用できます。  
  
-   プリンシパル サーバーが停止している。  
  
-   WITNESS が OFF に設定されているか、またはミラーリング監視サーバーがミラー サーバーに接続されている。  
  
> [!CAUTION]  
>  サービスの強制は、厳密にはディザスター リカバリーの方法です。 サービスを強制すると、一部のデータが損失する場合があります。 このため、サービスを強制するのは、データベースに対するサービスを直ちに復元するためにデータの損失を許容できる場合のみに限定します。 サービスの強制によって重要なデータを失うリスクがある場合は、ミラーリングを停止してデータベースを手動で再同期することをお勧めします。 サービスの強制によるリスクの詳細については、「 [データベース ミラーリングの動作モード](database-mirroring-operating-modes.md)」を参照してください。  
  
 サービスを強制すると、セッションが中断して新しい復旧分岐が始まります。 サービスの強制による効果は、ミラーリングを削除して以前のプリンシパル データベースを復旧する効果に似ています。 ただし、サービスを強制した場合は、ミラーリング再開時のデータベースの再同期が容易になります (データが損失する可能性があります)。  
  
### <a name="to-force-service-in-a-database-mirroring-session"></a>データベース ミラーリング セッションでサービスを強制するには  
  
1.  ミラー サーバーに接続します。  
  
2.  次のステートメントを実行します。  
  
     ALTER DATABASE *<database_name>* SET PARTNER FORCE_SERVICE_ALLOW_DATA_LOSS  
  
     ここで、 *<database_name>* はミラー化されたデータベースです。  
  
     ミラー サーバーは、直ちにプリンシパル サーバーに切り替わり、ミラーリングが中断されます。  
  
## <a name="see-also"></a>関連項目  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [データベース ミラーリングの動作モード](database-mirroring-operating-modes.md)  
  
  
