---
title: スナップショット レプリケーションおよびトランザクション レプリケーションのバックアップと復元の方式 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- backups [SQL Server replication], snapshot replication
- restoring [SQL Server replication], transactional replication
- snapshot replication [SQL Server], backup and restore
- restoring [SQL Server replication], snapshot replication
- recovery [SQL Server replication], transactional replication
- transactional replication, backup and restore
- recovery [SQL Server replication], snapshot replication
- sync with backup [SQL Server replication]
- backups [SQL Server replication], transactional replication
ms.assetid: a8afcdbc-55db-4916-a219-19454f561f9e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b5011daf52b7eb5a14fb97ff3d39691caf4a563c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210775"
---
# <a name="strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication"></a>スナップショット レプリケーションおよびトランザクション レプリケーションのバックアップと復元の方式
  スナップショット レプリケーションおよびトランザクション レプリケーションのバックアップと復元の方式を計画する場合には、以下の 3 点を考慮する必要があります。  
  
-   バックアップ対象のデータベース  
  
-   トランザクション レプリケーションのバックアップ設定  
  
-   データベースを復元するために必要な手順。 この手順は、レプリケーションの種類と選択したオプションによって異なります。  
  
 このトピックでは、これらの各項目について、以下の 3 つのセクションで説明します。 Oracle パブリッシングのバックアップと復元については、「[Oracle パブリッシャーのバックアップと復元](../non-sql/backup-and-restore-for-oracle-publishers.md)」を参照してください。  
  
## <a name="backing-up-databases"></a>データベースのバックアップ  
 スナップショット レプリケーションおよびトランザクション レプリケーションの場合は、以下のデータベースを定期的にバックアップする必要があります。  
  
-   パブリッシャーにあるパブリケーション データベース  
  
-   ディストリビューターにあるディストリビューション データベース  
  
-   サブスクライバーにあるサブスクリプション データベース  
  
-   パブリッシャー、ディストリビューター、およびすべてのサブスクライバーにある **master** および **msdb** システム データベース。 これらのデータベースは、相互に関連するレプリケーション データベースとして、同時にバックアップする必要があります。 たとえば、パブリッシャーでパブリケーション データベースをバックアップするときに、 **master** および **msdb** データベースも同時にバックアップします。 パブリケーション データベースが復元されるときに、 **master** および **msdb** データベースのレプリケーションの構成と設定が、パブリケーション データベースと一致していることを確認します。  
  
 定期的なログ バックアップを実行する場合は、レプリケーション関連の変更をログ バックアップでキャプチャする必要があります。 ログ バックアップを実行しない場合は、レプリケーションに関連する設定を変更するたびに、バックアップを実行する必要があります。 詳細については、「 [Common Actions Requiring an Updated Backup](common-actions-requiring-an-updated-backup.md)」を参照してください。  
  
## <a name="backup-settings-for-transactional-replication"></a>トランザクション レプリケーションのバックアップ設定  
 トランザクション レプリケーションには " **sync with backup** " オプションが用意されており、ディストリビューション データベースおよびパブリケーション データベースで設定できます。  
  
-   ディストリビューション データベースでは、常にこのオプションを設定することをお勧めします。  
  
     ディストリビューション データベースでこのオプションを設定すると、パブリケーション データベースのログに記録されたトランザクションは、ディストリビューション データベース内のバックアップが終了するまで切り捨てられることはありません。 ディストリビューション データベースは前回のバックアップに復元できます。失われたトランザクションは、パブリケーション データベースからディストリビューション データベースに配信されます。 レプリケーションは影響を受けることなく継続されます。  
  
     ディストリビューション データベースでこのオプションを設定しても、レプリケーションの待機時間には影響しません。 ただし、ディストリビューション データベース内の対応するトランザクションがバックアップされるまで、パブリケーション データベースでのログの切り捨てが遅延されます (この結果、パブリケーション データベースのトランザクション ログのサイズが増加する可能性があります)。  
  
-   アプリケーションがレプリケーションの待機時間の延長を許容できる場合は、パブリケーション データベースでこのオプションを設定することをお勧めします。  
  
     パブリケーション データベースでこのオプションを設定すると、パブリケーション データベースでのバックアップが終了するまで、トランザクションがディストリビューション データベースに配信されることはなくなります。 その後、パブリッシャーでパブリケーション データベースを前回のバックアップに復元できます。復元されたパブリケーション データベースにないトランザクションが、ディストリビューション データベースに存在する可能性は一切ありません。  
  
     パブリッシャーでのバックアップが終了するまでの間、トランザクションがディストリビューション データベースに配信されなくなるため、レプリケーションの待機時間とスループットが影響を受けます。 たとえば、トランザクション ログが 5 分ごとにバックアップされる場合、パブリッシャーでトランザクションがコミットされてから、パブリッシャーからディストリビューション データベース、その後サブスクライバーにトランザクションが配信されるまでの間に、さらに 5 分間の待機時間が発生します。  
  
    > [!NOTE]  
    >  " **sync with backup** " オプションを設定すると、パブリケーション データベースとディストリビューション データベースの一貫性が確保されますが、データの損失が発生しなくなるわけではありません。 たとえば、トランザクション ログが見つからない場合、トランザクション ログの前回のバックアップ以降にコミットされたトランザクションを、パブリケーション データベースまたはディストリビューション データベースで利用することはできません。 これは、レプリケートされていないデータベースと同様の動作です。  
  
 **"sync with backup" オプションを設定するには**  
  
-   レプリケーション [!INCLUDE[tsql](../../../includes/tsql-md.md)] プログラミング: [トランザクション レプリケーションの連携バックアップの有効化 (レプリケーション Transact-SQL プログラミング)](enable-coordinated-backups-for-transactional-replication.md)  
  
## <a name="restoring-databases-involved-in-replication"></a>レプリケーションに関連するデータベースの復元  
 最新のバックアップが利用可能で適切な手順が実行された場合、レプリケーション トポロジ内のすべてのデータベースを復元できます。 パブリケーション データベースの復元手順は、使用するレプリケーションの種類とオプションによって異なります。ただし、パブリケーション データベース以外のデータベースの復元手順は、レプリケーションの種類とオプションに依存しません。  
  
 レプリケーションでは、レプリケートされたデータベースをバックアップ作成元のサーバーおよびデータベースに復元する操作がサポートされます。 レプリケートされたデータベースのバックアップを別のサーバーまたはデータベースに復元する場合は、レプリケーションの設定は保存できません。 この場合、バックアップの復元後にすべてのパブリケーションおよびサブスクリプションを再作成する必要があります。  
  
### <a name="publisher"></a>発行元  
 以下の種類のレプリケーションについては、復元手順が用意されています。  
  
-   スナップショット レプリケーション  
  
-   読み取り専用トランザクション レプリケーション  
  
-   更新サブスクリプションを使用するトランザクション レプリケーション  
  
-   ピア ツー ピア トランザクション レプリケーション  
  
 **msdb** データベースおよび **master** データベースの復元方法についてもこのセクションで説明しますが、上記の 4 種類のレプリケーションについてはすべて同じ方法です。  
  
#### <a name="publication-database-snapshot-replication"></a>パブリケーション データベース: スナップショット レプリケーション  
  
1.  パブリケーション データベースの最新バックアップを復元します。 手順 2 に進みます。  
  
2.  すべてのパブリケーションおよびサブスクリプションに対する最新の構成がパブリケーション データベースのバックアップに含まれていますか。 答えが「はい」の場合、復元は完了です。 「いいえ」の場合は、手順 3. に進みます。  
  
3.  パブリッシャー、ディストリビューター、およびサブスクライバーで、レプリケーション構成を削除した後、再作成を行います。 復元が完了します。  
  
     レプリケーションを削除する方法の詳細については、「[sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql)」を参照してください。  
  
#### <a name="publication-database-read-only-transactional-replication"></a>パブリケーション データベース: 読み取り専用トランザクション レプリケーション  
  
1.  パブリケーション データベースの最新バックアップを復元します。 手順 2 に進みます。  
  
2.  障害の発生前に、パブリケーション データベースで " **sync with backup** " 設定が有効になっていましたか。 答えが「はい」の場合は、手順 3 に進みます。「いいえ」の場合は、手順 5 に進みます。  
  
     設定が有効の場合、 `SELECT DATABASEPROPERTYEX('<PublicationDatabaseName>', 'IsSyncWithBackup')` クエリが "1" を返します。  
  
3.  復元されたバックアップは完全かつ最新ですか。 すべてのパブリケーションおよびサブスクリプションに対する最新の構成がこのバックアップに含まれていますか。 答えが「はい」の場合、復元は完了です。 「いいえ」の場合は、手順 4 に進みます。  
  
4.  復元されたパブリケーション データベースの構成情報が最新ではありません。 このため、サブスクライバーで未実行のコマンドがすべてディストリビューション データベースに存在することを確認し、レプリケーション構成の削除と再作成を行う必要があります。  
  
    1.  すべてのサブスクライバーがディストリビューション データベース内の未実行のコマンドと同期するまで、ディストリビューション エージェントを実行します。 レプリケーション モニターの **[未配布のコマンド]** タブを使用するか、またはディストリビューション データベース内の [MSdistribution_status](/sql/relational-databases/system-views/msdistribution-status-transact-sql) ビューでクエリを実行して、すべてのコマンドがサブスクライバーに配信されたことを確認します。 手順 b. に進みます。  
  
         ディストリビューション エージェントの実行方法の詳細については、「[レプリケーション エージェントを起動および停止する &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)」および「[レプリケーション エージェント実行可能ファイルの概念](../concepts/replication-agent-executables-concepts.md)」を参照してください。  
  
         コマンドを確認する方法の詳細については、次を参照してください[ビューのレプリケートされたコマンドとディストリビューション データベース内のその他の情報&#40;レプリケーション TRANSACT-SQL プログラミング&#41;](../monitor/view-replicated-commands-and-information-in-distribution-database.md)と[情報の表示。およびレプリケーション モニターを使用してタスクを実行する](../monitor/view-information-and-perform-tasks-replication-monitor.md)します。  
  
    2.  パブリッシャー、ディストリビューター、およびサブスクライバーで、レプリケーション構成を削除した後、再作成を行います。 サブスクリプションを再作成するときには、サブスクライバーにデータが格納済みであることを指定します。 復元が完了します。  
  
         レプリケーションを削除する方法の詳細については、「[sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql)」を参照してください。  
  
         サブスクライバーにデータが格納済みであることを指定する方法の詳細については、「 [Initialize a Subscription Manually](../initialize-a-subscription-manually.md)」を参照してください。  
  
5.  パブリケーション データベースで " **sync with backup** " オプションが設定されていませんでした。 このため、復元されたバックアップに含まれていないトランザクションが、ディストリビューターまたはサブスクライバーに配信された可能性があります。 サブスクライバーで未実行のコマンドがすべてディストリビューション データベースに存在することを確認し、復元されたバックアップに含まれないすべてのトランザクションをパブリケーション データベースに手動で適用する必要があります。  
  
    > [!IMPORTANT]  
    >  この処理を実行することによって、復元対象のパブリッシュされたテーブルを、バックアップから復元されたパブリッシュされていないテーブルよりも新しい状態にすることができます。  
  
    1.  すべてのサブスクライバーがディストリビューション データベース内の未実行のコマンドと同期するまで、ディストリビューション エージェントを実行します。 レプリケーション モニターの **[未配布のコマンド]** タブを使用するか、またはディストリビューション データベース内の [MSdistribution_status](/sql/relational-databases/system-views/msdistribution-status-transact-sql) ビューでクエリを実行して、すべてのコマンドがサブスクライバーに配信されたことを確認します。 手順 b. に進みます。  
  
         ディストリビューション エージェントの実行方法の詳細については、「[レプリケーション エージェントを起動および停止する &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)」および「[レプリケーション エージェント実行可能ファイルの概念](../concepts/replication-agent-executables-concepts.md)」を参照してください。  
  
         コマンドを確認する方法の詳細については、次を参照してください[ビューのレプリケートされたコマンドとディストリビューション データベース内のその他の情報&#40;レプリケーション TRANSACT-SQL プログラミング&#41;](../monitor/view-replicated-commands-and-information-in-distribution-database.md)と[情報の表示。およびレプリケーション モニターを使用してタスクを実行する](../monitor/view-information-and-perform-tasks-replication-monitor.md)します。  
  
    2.  [tablediff ユーティリティ](../../../tools/tablediff-utility.md) またはその他のツールを使用して、パブリッシャーとサブスクライバーを手動で同期します。 これにより、パブリケーション データベースのバックアップに含まれていなかったサブスクリプション データベースのデータを復旧できます。 手順 c. に進みます。  
  
         **tablediff** ユーティリティの詳細については、「[レプリケートされたテーブルを比較して相違があるかどうかを確認する &#40;レプリケーション プログラミング&#41;](compare-replicated-tables-for-differences-replication-programming.md)」を参照してください。  
  
    3.  復元されたバックアップは完全かつ最新ですか。 すべてのパブリケーションおよびサブスクリプションに対する最新の構成がこのバックアップに含まれていますか。 答えが「はい」の場合は、 [sp_replrestart](/sql/relational-databases/system-stored-procedures/sp-replrestart-transact-sql) ストアド プロシージャを実行して、パブリッシャーのメタデータをディストリビューターのメタデータと再同期します。 復元が完了します。 答えが「いいえ」の場合は、手順 d. に進みます。  
  
    4.  パブリッシャー、ディストリビューター、およびサブスクライバーで、レプリケーション構成を削除した後、再作成を行います。 サブスクリプションを再作成するときには、サブスクライバーにデータが格納済みであることを指定します。 復元が完了します。  
  
         レプリケーションを削除する方法の詳細については、「[sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql)」を参照してください。  
  
         サブスクライバーにデータが格納済みであることを指定する方法の詳細については、「 [Initialize a Subscription Manually](../initialize-a-subscription-manually.md)」を参照してください。  
  
#### <a name="publication-database-transactional-replication-with-updating-subscriptions"></a>パブリケーション データベース: 更新サブスクリプションを使用するトランザクション レプリケーション  
  
1.  パブリケーション データベースの最新バックアップを復元します。 手順 2 に進みます。  
  
2.  すべてのサブスクライバーがディストリビューション データベース内の未実行のコマンドと同期するまで、ディストリビューション エージェントを実行します。 レプリケーション モニターの **[未配布のコマンド]** タブを使用するか、またはディストリビューション データベース内の [MSdistribution_status](/sql/relational-databases/system-views/msdistribution-status-transact-sql) ビューでクエリを実行して、すべてのコマンドがサブスクライバーに配信されたことを確認します。 手順 3. に進みます。  
  
     ディストリビューション エージェントの実行方法の詳細については、「[レプリケーション エージェントを起動および停止する &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)」および「[レプリケーション エージェント実行可能ファイルの概念](../concepts/replication-agent-executables-concepts.md)」を参照してください。  
  
     コマンドを確認する方法の詳細については、次を参照してください[ビューのレプリケートされたコマンドとディストリビューション データベース内のその他の情報&#40;レプリケーション TRANSACT-SQL プログラミング&#41;](../monitor/view-replicated-commands-and-information-in-distribution-database.md)と[情報の表示。およびレプリケーション モニターを使用してタスクを実行する](../monitor/view-information-and-perform-tasks-replication-monitor.md)します。  
  
3.  キュー更新サブスクリプションを使用している場合は、各サブスクライバーに接続して、サブスクリプション データベースの [MSreplication_queue &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/msreplication-queue-transact-sql) テーブルからすべての行を削除します。 手順 4 に進みます。  
  
    > [!NOTE]  
    >  キュー更新サブスクリプションおよび ID 列を含むテーブルを使用している場合は、復元後に正しい ID 範囲が割り当てられていることを確認する必要があります。 詳細については、「[Replicate Identity Columns](../publish/replicate-identity-columns.md)」 (ID 列のレプリケート) を参照してください。  
  
4.  サブスクライバーで未実行のコマンドがすべてディストリビューション データベースに存在することを確認し、復元されたバックアップに含まれないすべてのトランザクションをパブリケーション データベースに手動で適用する必要があります。  
  
    > [!IMPORTANT]  
    >  この処理を実行することによって、復元対象のパブリッシュされたテーブルを、バックアップから復元されたパブリッシュされていないテーブルよりも新しい状態にすることができます。  
  
    1.  すべてのサブスクライバーがディストリビューション データベース内の未実行のコマンドと同期するまで、ディストリビューション エージェントを実行します。 レプリケーション モニターを使用するか、またはディストリビューション データベース内の [MSdistribution_status](/sql/relational-databases/system-views/msdistribution-status-transact-sql) ビューでクエリを実行して、すべてのコマンドがサブスクライバーに配信されたことを確認します。 手順 b. に進みます。  
  
    2.  [tablediff Utility](../../../tools/tablediff-utility.md) またはその他のツールを使用して、パブリッシャーとサブスクライバーを手動で同期します。 これにより、パブリケーション データベースのバックアップに含まれていなかったサブスクリプション データベースのデータを復旧できます。 手順 c. に進みます。  
  
         **tablediff** ユーティリティの詳細については、「[レプリケートされたテーブルを比較して相違があるかどうかを確認する &#40;レプリケーション プログラミング&#41;](compare-replicated-tables-for-differences-replication-programming.md)」を参照してください。  
  
    3.  復元されたバックアップは完全かつ最新ですか。 すべてのパブリケーションおよびサブスクリプションに対する最新の構成がこのバックアップに含まれていますか。 答えが「はい」の場合は、 [sp_replrestart](/sql/relational-databases/system-stored-procedures/sp-replrestart-transact-sql) ストアド プロシージャを実行して、パブリッシャーのメタデータをディストリビューターのメタデータと再同期します。 復元が完了します。 答えが「いいえ」の場合は、手順 d. に進みます。  
  
    4.  パブリッシャー、ディストリビューター、およびサブスクライバーで、レプリケーション構成を削除した後、再作成を行います。 サブスクリプションを再作成するときには、サブスクライバーにデータが格納済みであることを指定します。 復元が完了します。  
  
         レプリケーションを削除する方法の詳細については、「[sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql)」を参照してください。  
  
         サブスクライバーにデータが格納済みであることを指定する方法の詳細については、「 [Initialize a Subscription Manually](../initialize-a-subscription-manually.md)」を参照してください。  
  
#### <a name="publication-database-peer-to-peer-transactional-replication"></a>パブリケーション データベース: @loopback_detection  
 以下の手順では、パブリケーション データベース **A**、 **B**、および **C** は、ピア ツー ピア トランザクション レプリケーション トポロジ内にあります。 データベース **A** およびデータベース **C** はオンラインで正常に動作しています。データベース **B** は復元対象のデータベースです。 ここで説明する処理、特に手順 7、10、および 11 は、ピア ツー ピア トポロジにノードを追加するために必要な処理とよく似ています。 これらの手順を最も簡単に実行する方法は、ピア ツー ピア トポロジ構成ウィザードを使用することです。ただし、ストアド プロシージャも使用できます。  
  
1.  ディストリビューション エージェントを実行して、データベース **A** およびデータベース **C** のサブスクリプションを同期します。手順 2 に進みます。  
  
     ディストリビューション エージェントの実行方法の詳細については、「[レプリケーション エージェントを起動および停止する &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)」および「[レプリケーション エージェント実行可能ファイルの概念](../concepts/replication-agent-executables-concepts.md)」を参照してください。  
  
2.  **B** が使用するディストリビューション データベースがまだ利用可能な場合は、ディストリビューション エージェントを実行して、データベース **B** とデータベース **A** の間のサブスクリプション、およびデータベース B とデータベース **C** の間のサブスクリプションを同期します。手順 3. に進みます。  
  
3.  **B** のディストリビューション データベースで [sp_removedistpublisherdbreplication](/sql/relational-databases/system-stored-procedures/sp-removedistpublisherdbreplication-transact-sql) を実行して、**B** が使用するディストリビューション データベースからメタデータを削除します。手順 4 に進みます。  
  
4.  データベース **A** およびデータベース **C** で、データベース **B** のパブリケーションに対するサブスクリプションを削除します。手順 5 に進みます。  
  
     サブスクリプションを削除する方法の詳細については、「 [Subscribe to Publications](../subscribe-to-publications.md)」を参照してください。  
  
5.  データベース **A** のログ バックアップまたは完全バックアップを実行します。手順 6 に進みます。  
  
6.  データベース **A** のバックアップをデータベース **B** で復元します。この場合、データベース **B** にはデータベース **A** のデータが格納されますが、レプリケーション構成は含まれません。 バックアップを別のサーバーに復元すると、レプリケーションは削除されます。データベース **B** からレプリケーションが削除されたのはそのためです。手順 7 に進みます。  
  
7.  データベース **B** でパブリケーションを再作成し、その後にデータベース **A** とデータベース **B** の間のサブスクリプションを再作成します (データベース **C** 関連のサブスクリプションについては後の段階で処理します)。  
  
    1.  データベース **B** でパブリケーションを再作成します。手順 b. に進みます。  
  
    2.  データベース **B** のパブリケーションに対するサブスクリプションをデータベース **A**で再作成します。その際に、バックアップを使用してサブスクリプションを初期化するように指定します ( **sp_addsubscription** の **@sync_type** パラメーターの値を " [initialize with backup](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql)" に指定します)。 手順 c. に進みます。  
  
    3.  データベース **A** のパブリケーションに対するサブスクリプションをデータベース **B**で再作成します。その際に、サブスクライバーにデータが格納済みであることを指定します ( **sp_addsubscription** の **@sync_type** パラメーターの値を " [initialize with backup](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql)" に指定します)。 手順 8 に進みます。  
  
8.  ディストリビューション エージェントを実行して、データベース **A** およびデータベース **B** のサブスクリプションを同期します。パブリッシュされたテーブルに ID 列がある場合は、手順 9. に進みます。 それ以外の場合は、手順 10 に進みます。  
  
9. 復元後、データベース **A** の各テーブルに割り当てた ID 範囲は、データベース **B** でも使用されます。データベース **B** の障害発生後、データベース **A** およびデータベース **C** に反映されたすべての変更を復元されたデータベース **B** に適用し、その後、各テーブルの ID 範囲を再作成します。  
  
    1.  データベース [B](/sql/relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql) のバックアップをデータベース **B** を実行し、出力パラメーター **@request_id** 」を参照してください。 手順 b. に進みます。  
  
    2.  既定では、ディストリビューション エージェントが連続的に実行されるように設定されているため、すべてのノードに自動的にトークンが送信されます。 ディストリビューション エージェントが連続モードで実行されていない場合は、エージェントを実行します。 詳細については、「[レプリケーション エージェント実行可能ファイルの概念](../concepts/replication-agent-executables-concepts.md)」または「[レプリケーション エージェントを起動および停止する &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)」を参照してください。 手順 c. に進みます。  
  
    3.  データベース [@request_id](/sql/relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql)値を指定して **@request_id** を実行します。 すべてのノードがピア要求を受信するまで待機します。 手順 d. に進みます。  
  
    4.  [DBCC CHECKIDENT](/sql/t-sql/database-console-commands/dbcc-checkident-transact-sql) を使用してデータベース **B** の各テーブルを再作成し、適切な範囲が使用されていることを確認します。 手順 10 に進みます。  
  
     ID 範囲を管理する方法の詳細については、「[ID 列のレプリケート](../publish/replicate-identity-columns.md)」の「手動で ID 範囲を管理する場合の範囲の割り当て」を参照してください。  
  
10. この時点では、データベース **B** とデータベース **C** は直接接続されていませんが、両者はデータベース **A** を介して変更を受信します。[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] を実行しているノードがトポロジに含まれている場合は手順 11. に進み、それ以外の場合は手順 12. に進みます。  
  
11. システムを停止し、データベース **B** とデータベース **C** の間のサブスクリプションを再作成します。システムを停止するときには、パブリッシュされたテーブルの利用をすべてのノードで停止し、各ノードが他のすべてのノードの変更を受け取っていることを確認します。  
  
    1.  ピア ツー ピア トポロジ内のパブリッシュされたテーブルの処理をすべて停止します。 手順 b. に進みます。  
  
    2.  データベース [B](/sql/relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql) のバックアップをデータベース **B** を実行し、出力パラメーター **@request_id** 」を参照してください。 手順 c. に進みます。  
  
    3.  既定では、ディストリビューション エージェントが連続的に実行されるように設定されているため、すべてのノードに自動的にトークンが送信されます。 ディストリビューション エージェントが連続モードで実行されていない場合は、エージェントを実行します。 手順 d. に進みます。  
  
    4.  データベース [@request_id](/sql/relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql)値を指定して **@request_id** を実行します。 すべてのノードがピア要求を受信するまで待機します。 手順 e. に進みます。  
  
    5.  データベース **C** のパブリケーションに対するサブスクリプションをデータベース **B**で再作成します。その際に、サブスクライバーにデータが格納済みであることを指定します。 手順 b. に進みます。  
  
    6.  データベース **B** のパブリケーションに対するサブスクリプションをデータベース **C**で再作成します。その際に、サブスクライバーにデータが格納済みであることを指定します。 手順 13 に進みます。  
  
12. データベース **B** とデータベース **C**の間のサブスクリプションを再作成します。  
  
    1.  データベース **B**で [MSpeer_lsns](/sql/relational-databases/system-tables/mspeer-lsns-transact-sql) テーブルにクエリを実行して、データベース **B** がデータベース **C**から受信した最新のトランザクションのログ シーケンス番号 (LSN) を取得します。  
  
    2.  データベース **B** のパブリケーションに対するサブスクリプションをデータベース **C**で再作成します。その際に、LSN に基づいてサブスクリプションを初期化するように指定します ( **sp_addsubscription** の **@sync_type** パラメーターの値を " [initialize with backup](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql)" に指定します)。 手順 b. に進みます。  
  
    3.  データベース **B** のパブリケーションに対するサブスクリプションをデータベース **C**で再作成します。その際に、サブスクライバーにデータが格納済みであることを指定します。 手順 13 に進みます。  
  
13. ディストリビューション エージェントを実行して、データベース **B** およびデータベース **C** のサブスクリプションを同期します。復元が完了します。  
  
#### <a name="msdb-database-publisher"></a>msdb データベース (パブリッシャー)  
  
1.  **msdb** データベースの最新バックアップを復元します。  
  
2.  復元されたバックアップは完全かつ最新ですか。 すべてのパブリケーションおよびサブスクリプションに対する最新の構成がこのバックアップに含まれていますか。 答えが「はい」の場合、復元は完了です。 「いいえ」の場合は、手順 3. に進みます。  
  
3.  レプリケーション スクリプトを使用して、サブスクリプションのクリーンアップ ジョブを再作成します。 復元が完了します。  
  
#### <a name="master-database-publisher"></a>master データベース (パブリッシャー)  
  
1.  **master** データベースの最新バックアップを復元します。  
  
2.  データベースのレプリケーション構成および設定が、パブリケーション データベースと一致していることを確認します。  
  
### <a name="databases-at-the-distributor"></a>ディストリビューターにあるデータベース  
  
#### <a name="distribution-database"></a>ディストリビューション データベース  
  
1.  ディストリビューション データベースの最新バックアップを復元します。  
  
2.  障害の発生前に、ディストリビューション データベースで " **sync with backup** " 設定が有効になっていましたか。 答えが「はい」の場合は、手順 3. に進みます。「いいえ」の場合は、手順 4. に進みます。  
  
     設定が有効の場合、 `SELECT DATABASEPROPERTYEX('<DistributionDatabaseName>', 'IsSyncWithBackup')` クエリが "1" を返します。  
  
3.  復元されたバックアップは完全かつ最新ですか。 すべてのパブリケーションおよびサブスクリプションに対する最新の構成がこのバックアップに含まれていますか。 答えが「はい」の場合、復元は完了です。 「いいえ」の場合は、手順 4 に進みます。  
  
4.  復元されたディストリビューション データベースの構成情報が最新でないか、またはディストリビューション データベースで " **sync with backup** " オプションが設定されていませんでした (復元後に、パブリッシャーでコミットされた後にサブスクライバーに配信されていないトランザクションは、ディストリビューション データベースで見つからない可能性があります)。レプリケーションの削除および再作成を行ってから検証を実行します。  
  
    1.  パブリッシャー、ディストリビューター、およびサブスクライバーで、レプリケーション構成を削除した後、再作成を行います。 サブスクリプションを再作成するときには、サブスクライバーにデータが格納済みであることを指定します。 手順 b. に進みます。  
  
         レプリケーションを削除する方法の詳細については、「[sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql)」を参照してください。  
  
         サブスクライバーにデータが格納済みであることを指定する方法の詳細については、「 [Initialize a Subscription Manually](../initialize-a-subscription-manually.md)」を参照してください。  
  
    2.  検証を行うすべてのパブリケーションにマークを付けます。 検証に失敗したサブスクリプションを再初期化します。 復元が完了します。  
  
         検証の詳細については、「 [Validate Replicated Data](../validate-data-at-the-subscriber.md)」を参照してください。 再初期化の詳細については、「[サブスクリプションの再初期化](../reinitialize-subscriptions.md)」を参照してください。  
  
#### <a name="msdb-database-distributor"></a>msdb データベース (ディストリビューター)  
  
1.  **msdb** データベースの最新バックアップを復元します。  
  
2.  復元されたバックアップは完全かつ最新ですか。 すべてのパブリケーションおよびサブスクリプションに対する最新の構成がこのバックアップに含まれていますか。 答えが「はい」の場合、復元は完了です。 「いいえ」の場合は、手順 3. に進みます。  
  
3.  パブリッシャー、ディストリビューター、およびサブスクライバーで、レプリケーション構成を削除した後、再作成を行います。 サブスクリプションを再作成するときには、サブスクライバーにデータが格納済みであることを指定します。 手順 4 に進みます。  
  
     レプリケーションを削除する方法の詳細については、「[sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql)」を参照してください。  
  
     サブスクライバーにデータが格納済みであることを指定する方法の詳細については、「 [Initialize a Subscription Manually](../initialize-a-subscription-manually.md)」を参照してください。  
  
4.  検証を行うすべてのパブリケーションにマークを付けます。 検証に失敗したサブスクリプションを再初期化します。 復元が完了します。  
  
     検証の詳細については、「 [Validate Replicated Data](../validate-data-at-the-subscriber.md)」を参照してください。 再初期化の詳細については、「[サブスクリプションの再初期化](../reinitialize-subscriptions.md)」を参照してください。  
  
#### <a name="master-database-distributor"></a>master データベース (ディストリビューター)  
  
1.  **master** データベースの最新バックアップを復元します。  
  
2.  データベースのレプリケーション構成および設定が、パブリケーション データベースと一致していることを確認します。  
  
### <a name="databases-at-the-subscriber"></a>サブスクライバーにあるデータベース  
  
#### <a name="subscription-database"></a>サブスクリプション データベース  
  
1.  サブスクリプション データベースの最新バックアップは、ディストリビューション データベースにおけるディストリビューションの最小保有期間の設定よりも新しいですか (これにより、サブスクライバーを最新状態にするために必要なすべてのコマンドがディストリビューターに存在しているかどうかを判断できます)。答えが「はい」の場合は、手順 2. に進みます。 「いいえ」の場合は、サブスクリプションを再初期化します。 復元が完了します。  
  
     ディストリビューションの最大保有期間を確認するには、 [sp_helpdistributiondb](/sql/relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql) を実行し、 **max_distretention** 列から値 (時間単位) を取得します。  
  
     サブスクリプションを再初期化する方法の詳細については、「 [Reinitialize a Subscription](../reinitialize-a-subscription.md)」を参照してください。  
  
2.  サブスクリプション データベースの最新バックアップを復元します。 手順 3. に進みます。  
  
3.  サブスクリプション データベースにプッシュ サブスクリプションのみが含まれている場合は、手順 4. に進みます。 サブスクリプション データベースにプル サブスクリプションが含まれている場合は、次の質問に答えてください。サブスクリプション情報は最新ですか。 障害発生時に設定されていたすべてのテーブルおよびオプションがデータベースに含まれていますか。 「はい」の場合は、手順 4 に進みます。 「いいえ」の場合は、サブスクリプションを再初期化します。 復元が完了します。  
  
4.  サブスクライバーを同期するには、ディストリビューション エージェントを実行します。 復元が完了します。  
  
     ディストリビューション エージェントの実行方法の詳細については、「[レプリケーション エージェントを起動および停止する &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)」および「[レプリケーション エージェント実行可能ファイルの概念](../concepts/replication-agent-executables-concepts.md)」を参照してください。  
  
#### <a name="msdb-database-subscriber"></a>msdb データベース (サブスクライバー)  
  
1.  **msdb** データベースの最新バックアップを復元します。 このサブスクライバーでプル サブスクリプションが使用されていますか。 答えが「いいえ」の場合、復元は完了です。 答えが「はい」の場合は、手順 2. に進みます。  
  
2.  復元されたバックアップは完全かつ最新ですか。 すべてのプル サブスクリプションに対する最新の構成がこのバックアップに含まれていますか。 答えが「はい」の場合、復元は完了です。 「いいえ」の場合は、手順 3. に進みます。  
  
3.  プル サブスクリプションの削除および再作成を行います。 サブスクリプションを再作成するときには、サブスクライバーにデータが格納済みであることを指定します。 復元が完了します。  
  
     サブスクリプションを削除する方法の詳細については、「 [Subscribe to Publications](../subscribe-to-publications.md)」を参照してください。  
  
     サブスクライバーにデータが格納済みであることを指定する方法の詳細については、「 [Initialize a Subscription Manually](../initialize-a-subscription-manually.md)」を参照してください。  
  
#### <a name="master-database-subscriber"></a>master データベース (サブスクライバー)  
  
1.  **master** データベースの最新バックアップを復元します。  
  
2.  データベースのレプリケーション構成および設定が、パブリケーション データベースと一致していることを確認します。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server データベースのバックアップと復元](../../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [レプリケートされたデータベースのバックアップと復元](back-up-and-restore-replicated-databases.md)   
 [[ディストリビューションの構成]](../configure-distribution.md)   
 [データとデータベース オブジェクトのパブリッシュ](../publish/publish-data-and-database-objects.md)   
 [パブリケーションのサブスクライブ](../subscribe-to-publications.md)   
 [サブスクリプションの初期化](../initialize-a-subscription.md)   
 [データの同期](../synchronize-data.md)  
  
  
