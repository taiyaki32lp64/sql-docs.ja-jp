---
title: ログ配布とレプリケーション (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], log shipping and
- log shipping [SQL Server], replication and
ms.assetid: 132bebfd-0206-4d23-829a-b38e5ed17bc9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5f505d46526aede97ac01c8f3de1b11450aeed8d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774304"
---
# <a name="log-shipping-and-replication-sql-server"></a>ログ配布とレプリケーション (SQL Server)
  ログ配布では単一のデータベースの 2 つのコピーを使用します。通常、これらのコピーは異なるコンピューターに配置されます。 クライアントが任意の時点において使用できるデータベースのコピーは 1 つだけです。 このコピーはプライマリ データベースと呼ばれます。 クライアントがプライマリ データベースに対して加えた更新は、ログ配布によってセカンダリ データベースと呼ばれるもう一方のコピー データベースに適用されます。 プライマリ データベースに対して行われた挿入、更新、および削除はすべてトランザクション ログに記録され、ログ配布によってこのトランザクション ログがセカンダリ データベースに適用されます。  
  
 ログ配布はレプリケーションと組み合わせて使用できます。ログ配布とレプリケーションを併用した場合の動作を以下に示します。  
  
-   ログ配布でフェールオーバーが発生すると、レプリケーションが停止します。 フェールオーバーが発生した場合、レプリケーション エージェントはセカンダリに接続しません。その結果、トランザクションがサブスクライバーにレプリケートされなくなります。 プライマリへのフェールバックが行われると、レプリケーションが再開されます。 ログ配布によってセカンダリからプライマリにコピーされたすべてのトランザクションがサブスクライバーにレプリケートされます。  
  
-   プライマリが完全に失われた場合、セカンダリの名前を変更してレプリケーションを継続できます。 このトピックの残りの部分では、こうしたケースを処理する場合の要件と手順について説明します。 ログ配布を使用する最も一般的なデータベースであるパブリケーション データベースを例として使用します。ただし、サブスクリプション データベースおよびディストリビューション データベースについても同様の手順を適用できます。  
  
 レプリケーションを再構成することなく、レプリケーションに関連するデータベースを復元する場合の詳細については、「 [レプリケートされたデータベースのバックアップと復元](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)」をご覧ください。  
  
> [!NOTE]  
>  パブリケーション データベースの可用性を提供することが目的の場合は、ログ配布ではなく、データベース ミラーリングを使用することをお勧めします。 詳細については、「 [データベース ミラーリングとレプリケーション &#40;SQL Server&#41;](../database-mirroring/database-mirroring-and-replication-sql-server.md)」をご覧ください。  
  
## <a name="requirements-and-procedures-for-replicating-from-the-secondary-if-the-primary-is-lost"></a>プライマリが失われた場合にセカンダリからレプリケートを行うための要件と手順  
 以下の要件および考慮事項に注意してください。  
  
-   プライマリに複数のパブリケーション データベースが格納されている場合、すべてのパブリケーション データベースのログが同一のセカンダリに配布されます。  
  
-   セカンダリ サーバー インスタンスのインストール パスは、プライマリ サーバー インスタンスのインストール パスと同一にする必要があります。 セカンダリ サーバー上のユーザー データベースの場所は、プライマリ サーバー上の場所と同一にする必要があります。  
  
-   プライマリでサービス マスター キーをバックアップします。 このキーはセカンダリで復元されます。 詳細については、「[BACKUP SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-service-master-key-transact-sql)」を参照してください。  
  
-   ログ配布では、データ損失の回避は保障されません。 プライマリ データベースで障害が発生した場合、バックアップされていないデータが失われたり、障害時にバックアップ用のデータが失われる可能性があります。  
  
### <a name="log-shipping-with-transactional-replication"></a>トランザクション レプリケーションのログ配布  
 トランザクション レプリケーションの場合、ログ配布の動作は **sync with backup** オプションの設定によって異なります。 このオプションは、パブリケーション データベースおよびディストリビューション データベースで設定できます。パブリッシャーのログ配布では、パブリケーション データベースでの設定のみが関係します。  
  
 パブリケーション データベースでこのオプションを設定すると、パブリケーション データベースでのバックアップが終了するまで、トランザクションがディストリビューション データベースに配信されることはなくなります。 これにより、セカンダリ サーバーでパブリケーション データベースの最後のバックアップを復元したときに、復元されたパブリケーション データベースにないトランザクションが、ディストリビューション データベースに存在する可能性がなくなります。 このオプションを設定すると、パブリッシャーがセカンダリ サーバーにフェールオーバーした場合でも、パブリッシャー、ディストリビューター、およびサブスクライバーの間で一貫性が保持されます。 パブリッシャーでのバックアップが終了するまでの間、トランザクションがディストリビューション データベースに配信されなくなるため、レプリケーションの待機時間とスループットが影響を受けることになります。アプリケーションがこうした待機時間の遅延を許容できる場合は、パブリケーション データベースでこのオプションを設定することをお勧めします。 **sync with backup** オプションが設定されていない場合は、セカンダリ サーバーで復元されたデータベースに含まれていない変更をサブスクライバーが受信する可能性があります。 詳細については、「 [スナップショット レプリケーションおよびトランザクション レプリケーションのバックアップと復元の方式](../../relational-databases/replication/transactional/transactional-replication.md)」を参照してください。  
  
 **sync with backup オプションを使用してトランザクション レプリケーションとログ配布を構成するには**  
  
1.  パブリケーション データベースで sync with backup オプションが設定されていない場合は、 `sp_replicationdboption '<publicationdatabasename>', 'sync with backup', 'true'`を実行します。 詳細については、「[sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql)」を参照してください。  
  
2.  パブリケーション データベースに対してログ配布を構成します。 詳細については、「[ログ配布の構成 &#40;SQL Server&#41;](configure-log-shipping-sql-server.md)」を参照してください。  
  
3.  パブリッシャーに障害が発生した場合は、RESTORE LOG の KEEP_REPLICATION オプションを使用して、データベースの最新のログをセカンダリ サーバーに復元します。 これにより、データベースのレプリケーション設定がすべて保持されます。 詳細については、「[ログ配布のセカンダリへのフェールオーバー &#40;SQL Server&#41;](fail-over-to-a-log-shipping-secondary-sql-server.md)」および「[RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)」を参照してください。  
  
4.  **msdb** データベースおよび **master** データベースをプライマリからセカンダリに復元します。 詳細については、「[システム データベースのバックアップと復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)」を参照してください。 プライマリがディストリビューターでもある場合は、ディストリビューション データベースをプライマリからセカンダリに復元します。  
  
     これらのデータベースのレプリケーション構成およびレプリケーション設定が、プライマリのパブリケーション データベースと一致する必要があります。  
  
5.  セカンダリ サーバーでコンピューター名を変更し、次にプライマリ サーバー名と一致するように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス名を変更します。 コンピューター名の変更の詳細については、Windows のマニュアルを参照してください。 サーバーの名前変更の詳細については、「 [SQL Server のスタンドアロン インスタンスをホストするコンピューターの名前変更](../install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md) 」および「 [SQL Server のフェールオーバー クラスター インスタンスの名前変更](../../sql-server/failover-clusters/install/rename-a-sql-server-failover-cluster-instance.md)」をご覧ください。  
  
6.  プライマリからバックアップしたサービス マスター キーをセカンダリ サーバーで復元します。 詳細については、「[RESTORE SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-service-master-key-transact-sql)」を参照してください。  
  
 **sync with backup オプションを使用しないでトランザクション レプリケーションとログ配布を構成するには**  
  
1.  パブリケーション データベースに対してログ配布を構成します。 詳細については、「[ログ配布の構成 &#40;SQL Server&#41;](configure-log-shipping-sql-server.md)」を参照してください。  
  
2.  パブリッシャーに障害が発生した場合は、RESTORE LOG の KEEP_REPLICATION オプションを使用して、データベースの最新のログをセカンダリ サーバーに復元します。 これにより、データベースのレプリケーション設定がすべて保持されます。 詳細については、「[ログ配布のセカンダリへのフェールオーバー &#40;SQL Server&#41;](fail-over-to-a-log-shipping-secondary-sql-server.md)」および「[RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)」を参照してください。  
  
3.  **msdb** データベースおよび **master** データベースをプライマリからセカンダリに復元します。 詳細については、「[システム データベースのバックアップと復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)」を参照してください。 プライマリがディストリビューターでもある場合は、ディストリビューション データベースをプライマリからセカンダリに復元します。  
  
     これらのデータベースのレプリケーション構成およびレプリケーション設定が、プライマリのパブリケーション データベースと一致する必要があります。  
  
4.  セカンダリ サーバーでコンピューター名を変更し、次にプライマリ サーバー名と一致するように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス名を変更します。 コンピューター名の変更の詳細については、Windows のマニュアルを参照してください。 サーバーの名前変更の詳細については、「 [SQL Server のスタンドアロン インスタンスをホストするコンピューターの名前変更](../install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md) 」および「 [SQL Server のフェールオーバー クラスター インスタンスの名前変更](../../sql-server/failover-clusters/install/rename-a-sql-server-failover-cluster-instance.md)」をご覧ください。  
  
     パブリケーション データベースとディストリビューション データベースが同期していないことを示す、ログ リーダー エージェントのエラー メッセージが表示される場合があります。  
  
5.  プライマリからバックアップしたサービス マスター キーをセカンダリ サーバーで復元します。 詳細については、「[RESTORE SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-service-master-key-transact-sql)」を参照してください。  
  
6.  **sp_replrestart** を実行します。 このストアド プロシージャを使用すると、パブリケーション データベースのログに記録されたレプリケート済みのトランザクションが、ログ リーダー エージェントによってすべて無視されることになります。 ストアド プロシージャが完了した後で適用されたトランザクションは、ログ リーダー エージェントによって処理されます。 詳細については、「[sp_replrestart &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replrestart-transact-sql)」を参照してください。  
  
7.  ストアド プロシージャが正常に終了したら、ログ リーダー エージェントを再起動します。 詳細については、「[レプリケーション エージェントを起動および停止する &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)」を参照してください。  
  
8.  サブスクライバーに既に配信されたトランザクションがパブリッシャーで適用される場合があります。 これらのトランザクションをサブスクライバーで再適用する場合に、ディストリビューション エージェントがエラーで異常終了しないようにするには、" **データ一貫性エラー時続行**" という名前のエージェント プロファイルを指定します。  
  
### <a name="log-shipping-with-merge-replication"></a>マージ レプリケーションのログ配布  
 マージ レプリケーションとログ配布を構成するには、以下の手順を実行します。  
  
 **マージ レプリケーションとログ配布を構成するには**  
  
1.  パブリケーション データベースに対してログ配布を構成します。 詳細については、「 [ログ配布の構成 &#40;SQL Server&#41;](configure-log-shipping-sql-server.md)で導入されました。  
  
2.  パブリッシャーに障害が発生した場合は、セカンダリ サーバーでコンピューター名を変更し、次にプライマリ サーバー名と一致するように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス名を変更します。 コンピューター名の変更の詳細については、Windows のマニュアルを参照してください。 サーバーの名前変更の詳細については、「 [SQL Server のスタンドアロン インスタンスをホストするコンピューターの名前変更](../install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md) 」および「 [SQL Server のフェールオーバー クラスター インスタンスの名前変更](../../sql-server/failover-clusters/install/rename-a-sql-server-failover-cluster-instance.md)」をご覧ください。  
  
3.  RESTORE LOG の KEEP_REPLICATION オプションを使用して、データベースの最新のログをセカンダリ サーバーに復元します。 これにより、データベースのレプリケーション設定がすべて保持されます。 詳細については、「[ログ配布のセカンダリへのフェールオーバー &#40;SQL Server&#41;](fail-over-to-a-log-shipping-secondary-sql-server.md)」および「[RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)」を参照してください。  
  
4.  **msdb** データベースおよび **master** データベースをプライマリからセカンダリに復元します。 詳細については、「[システム データベースのバックアップと復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)」を参照してください。 プライマリがディストリビューターでもある場合は、ディストリビューション データベースをプライマリからセカンダリに復元します。  
  
     これらのデータベースのレプリケーション構成およびレプリケーション設定が、プライマリのパブリケーション データベースと一致する必要があります。  
  
5.  プライマリからバックアップしたサービス マスター キーをセカンダリ サーバーで復元します。 詳細については、「[RESTORE SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-service-master-key-transact-sql)」を参照してください。  
  
6.  パブリケーション データベースを 1 つ以上のサブスクリプション データベースと同期します。 これにより、復元されたバックアップに反映されていないパブリケーション データベースの変更をアップロードできます。 アップロードできるデータは、パブリケーションのフィルター選択方法によって次のように異なります。  
  
    -   パブリケーションがフィルター選択されていない場合は、最新のサブスクライバーと同期することでパブリケーション データベースを最新の状態に更新できます。  
  
    -   パブリケーションがフィルター選択されている場合は、パブリケーションを最新の状態に更新できない場合があります。 各サブスクリプションが 1 つの地域の顧客データのみを受信できるようにパーティション分割されているテーブルがあるとします。北、東、南、西のいずれかです。 データの各パーティションに 1 つ以上のサブスクライバーがある場合、各パーティションのサブスクライバーと同期することにより、パブリケーション データベースを最新の状態に更新できます。 ただし、たとえば、西パーティションのデータがすべてのサブスクライバーにレプリケートされていない場合は、パブリッシャーでこのデータを最新の状態に更新することはできません。 この場合、パブリッシャーとサブスクライバーのデータが集約するように、すべてのサブスクリプションを再初期化することをお勧めします。 詳細については、「 [サブスクリプションの再初期化](../../relational-databases/replication/reinitialize-subscriptions.md)」を参照してください。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] よりも前のバージョンの [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]を実行しているサブスクライバーと同期する場合は、サブスクリプションを匿名にすることはできません。このサブスクリプションはクライアント サブスクリプションまたはサーバー サブスクリプション (以前のリリースではローカル サブスクリプションとグローバル サブスクリプションと呼ばれていました) にする必要があります。 詳細については、「 [データの同期](../../relational-databases/replication/synchronize-data.md)」を参照してください。   
  
## <a name="see-also"></a>参照  
 [SQL Server のレプリケーション](../../relational-databases/replication/sql-server-replication.md)   
 [ログ配布について &#40;SQL Server&#41;](about-log-shipping-sql-server.md)   
 [データベース ミラーリングとレプリケーション &#40;SQL Server&#41;](../database-mirroring/database-mirroring-and-replication-sql-server.md)  
  
  
