---
title: master データベースの復元 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- master database [SQL Server], restoring
ms.assetid: c83d802c-e84e-4458-b3ca-173d9ba32f73
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 823a6455616b412a41179d831b565e10b3286fb7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62875137"
---
# <a name="restore-the-master-database-transact-sql"></a>master データベースの復元 (Transact-SQL)
  このトピックでは、データベースの完全バックアップから **master** データベースを復元する方法について説明します。  
  
### <a name="to-restore-the-master-database"></a>master データベースを復元するには  
  
1.  サーバー インスタンスをシングル ユーザー モードで起動します。  
  
     シングル ユーザー スタートアップ パラメーター ( **-m**) の指定方法の詳細については、「[サーバーのスタートアップ オプションの構成 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)」を参照してください。  
  
2.  **master**データベースの完全バックアップを復元するには、次の [RESTORE DATABASE](/sql/t-sql/statements/restore-statements-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用します:  
  
     `RESTORE DATABASE master FROM`  *< backup_device >*  `WITH REPLACE`  
  
     REPLACE オプションは、指定したデータベースと同じ名前のデータベースが既に存在していても、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でデータベースを復元することを指定します。 既存のデータベースがある場合は削除されます。 シングル ユーザー モードでは、 [sqlcmd ユーティリティ](../../tools/sqlcmd-utility.md)で RESTORE DATABASE ステートメントを入力することをお勧めします。 詳細については、「 [sqlcmd Utility の使用](../scripting/sqlcmd-use-the-utility.md)」を参照してください。  
  
    > [!IMPORTANT]  
    >  **master** の復元後、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスがシャットダウンされ、 **sqlcmd** プロセスが終了します。 サーバー インスタンスを再起動する前に、シングル ユーザーの起動時のパラメーターを削除してください。 詳細については、「[サーバーのスタートアップ オプションの構成 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)」を参照してください。  
  
3.  サーバー インスタンスを再起動し、他のデータベースの復元、データベースのインポート、ユーザーの不一致の修正など、残りの復旧手順を実行します。  
  
## <a name="example"></a>例  
 次の例では、既定のサーバー インスタンスで `master` データベースを復元します。 この例では、サーバー インスタンスが既にシングル ユーザー モードで実行されていることを前提としています。 この例は、 `sqlcmd` を起動し、ディスク デバイス `RESTORE DATABASE` から `master` データベースの完全バックアップを復元する `Z:\SQLServerBackups\master.bak`ステートメントを実行します。  
  
> [!NOTE]
>  名前付きインスタンスの場合、**sqlcmd** コマンドでは、 **-S** _\<ComputerName>_ \\ *\<InstanceName>* オプションを指定する必要があります。  
  
```  
  
      C:\> sqlcmd  
1> RESTORE DATABASE master FROM DISK = 'Z:\SQLServerBackups\master.bak' WITH REPLACE;  
2> GO  
```  
  
## <a name="see-also"></a>参照  
 [データベースの全体復元 &#40;単純復旧モデル&#41;](complete-database-restores-simple-recovery-model.md)   
 [データベースの全体復元 &#40;完全復旧モデル&#41;](complete-database-restores-full-recovery-model.md)   
 [孤立ユーザーのトラブルシューティング &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)   
 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](../databases/database-detach-and-attach-sql-server.md)   
 [システム データベースの再構築](../databases/system-databases.md)   
 [データベース エンジン サービスのスタートアップ オプション](../../database-engine/configure-windows/database-engine-service-startup-options.md)   
 [SQL Server 構成マネージャー](../sql-server-configuration-manager.md)   
 [システム データベースのバックアップと復元 &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [シングル ユーザー モードでの SQL Server の起動](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)  
  
  
