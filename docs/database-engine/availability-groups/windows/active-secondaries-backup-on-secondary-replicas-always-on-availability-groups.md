---
title: バックアップをセカンダリ可用性グループ レプリカにオフロードする
description: Always On 可用性グループのセカンダリ レプリカにバックアップをオフロードする場合に、サポートされているさまざまなバックアップの種類について学習します。
ms.custom: seo-lt-2019
ms.date: 09/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- backup priority
- backup on secondary replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], backup on secondary replicas
- active secondary replicas [SQL Server], backup on
- automated backup preference
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 82afe51b-71d1-4d5b-b20a-b57afc002405
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 19118cde56109895213a733127b202c49feb23c1
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822414"
---
# <a name="offload-supported-backups-to-secondary-replicas-of-an-availability-group"></a>可用性グループのセカンダリ レプリカにサポートされているバックアップをオフロードする
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] のアクティブなセカンダリ機能では、セカンダリ レプリカでのバックアップの作成をサポートしています。 バックアップ操作では、(バックアップ圧縮により) I/O と CPU に大きな負荷がかかる場合があります。 同期済みまたは同期中のセカンダリ レプリカへバックアップをオフロードすることで、ワークロードが最も多いプライマリ レプリカをホストするサーバー インスタンスでリソースを使用できるようにします。  

> [!NOTE]  
>  可用性グループのプライマリ データベースとセカンダリ データベースでは、RESTORE ステートメントを使用できません。  
  
 
##  <a name="SupportedBuTypes"></a> セカンダリ レプリカでサポートされるバックアップの種類  
  
-   セカンダリ レプリカで実行されたときに **BACKUP DATABASE** でサポートされるのは、データベース、ファイル、またはファイル グループのコピーのみの完全バックアップだけです。 コピーのみのバックアップはログ チェーンには影響しません。また、差分ビットマップは消去されません。  
  
-   差分バックアップは、セカンダリ レプリカではサポートされていません。

-   同時バックアップ (プライマリ レプリカでトランザクション ログ バックアップを実行しながら、セカンダリ レプリカでデータベースの完全バックアップを実行するなど) は、現在サポートされていません。 
  
-   **BACKUP LOG** でサポートされるのは通常のログ バックアップだけです (セカンダリ レプリカでのログ バックアップでは、COPY_ONLY オプションはサポートされていません)。  
  
     可用性モード (同期コミットまたは非同期コミット) に関係なく、任意のレプリカ (プライマリまたはセカンダリ) で取得されたログ バックアップ全体にわたって一貫性のあるログ チェーンが保証されます。  
  
-   セカンダリ データベースをバックアップするには、セカンダリ レプリカがプライマリ レプリカと通信可能で、 **同期済み** または **同期中**であることが必要です。  

分散型可用性グループでは、アクティブ プライマリ レプリカと同じ可用性グループのセカンダリ レプリカ、またはセカンダリ可用性グループのいずれかのプライマリ レプリカでバックアップを実行できます。 セカンダリ レプリカは自身の可用性グループ内のプライマリ レプリカのみと通信するため、セカンダリ可用性グループ内のセカンダリ レプリカでバックアップを実行することはできません。 グローバル プライマリ レプリカと直接通信するレプリカのみがバックアップ操作を実行できます。

##  <a name="WhereBuJobsRun"></a> バックアップ ジョブを実行する場所の構成  
 セカンダリ レプリカでバックアップを実行してプライマリ運用サーバーからバックアップ ワークロードをオフロードすると、非常に大きな利点があります。 ただし、セカンダリ レプリカでバックアップを実行する場合は、バックアップ ジョブを実行する場所を決定するプロセスは非常に複雑です。 これに対処するには、バックアップ ジョブを実行する場所を次のように構成します。  
  
1.  可用性グループを構成して、バックアップを優先的に実行する可用性レプリカを指定します。 詳細については、「 *CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;* 」または「 *ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;* 」の [CREATE AVAILABILITY GROUP &amp;#40;Transact-SQL&amp;#41;](../../../t-sql/statements/create-availability-group-transact-sql.md) または [ALTER AVAILABILITY GROUP &amp;#40;Transact-SQL&amp;#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)であることが必要です。  
  
2.  バックアップの実行の候補である可用性レプリカをホストするすべてのサーバー インスタンス上のすべての可用性データベースに対して、スクリプト化されたバックアップ ジョブを作成します。 詳細については、「[可用性レプリカでのバックアップの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)」の「補足情報: セカンダリ レプリカでバックアップを構成した後」を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **セカンダリ レプリカでバックアップを構成するには**  
  
-   [可用性レプリカでのバックアップの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
 **現在のレプリカが推奨されるバックアップ レプリカであるかどうかを判別するには**  
  
-   [sys.fn_hadr_backup_is_preferred_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)  
  
 **バックアップ ジョブを作成するには**  
  
-   [メンテナンス プラン ウィザードの使用](../../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
-   [ジョブの実装](../../../ssms/agent/implement-jobs.md)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [コピーのみのバックアップ &#40;SQL Server&#41;](../../../relational-databases/backup-restore/copy-only-backups-sql-server.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
