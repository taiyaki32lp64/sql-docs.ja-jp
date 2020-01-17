---
title: データベース ミラーリングとレプリケーション (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- replication [SQL Server], database mirroring and
ms.assetid: 82796217-02e2-4bc5-9ab5-218bae11a2d6
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e957d0ae199375ffe13a756cc1a8b0872aa962e3
ms.sourcegitcommit: 97e94b76f9f48d161798afcf89a8c2ac0f09c584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2019
ms.locfileid: "68661431"
---
# <a name="database-mirroring-and-replication-sql-server"></a>データベース ミラーリングとレプリケーション (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  データベース ミラーリングとレプリケーションを組み合わせて使用すると、パブリケーション データベースの可用性を高めることができます。 データベース ミラーリングでは単一データベースの 2 つのコピーを使用します。通常、これらのコピーは異なるコンピューターに配置されます。 クライアントが任意の時点において使用できるデータベースのコピーは 1 つだけです。 このコピーはプリンシパル データベースと呼ばれます。 クライアントがプリンシパル データベースに対して加えた更新は、ミラー データベースと呼ばれるもう一方のコピー データベースに適用されます。 プリンシパル データベースに対して行われた挿入、更新、および削除はすべてトランザクション ログに記録され、ミラーリングによってこのトランザクション ログがミラー データベースに適用されます。  
  
 ミラーに対するレプリケーション フェールオーバーはパブリケーション データベースでのみ完全にサポートされ、サブスクリプション データベースでは制限付きでサポートされます。 データベース ミラーリングは、ディストリビューション データベースではサポートされていません。 レプリケーションを再構成することなく、ディストリビューション データベースおよびサブスクリプション データベースを復旧する場合の詳細については、「 [レプリケートされたデータベースのバックアップと復元](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)」を参照してください。   
  
> [!NOTE]  
>  フェールオーバー後には、ミラーがプリンシパルになります。 このトピックでは、"プリンシパル" および "ミラー" という言葉は常に、元のプリンシパルとミラーを表します。  
  
## <a name="requirements-and-considerations-for-using-replication-with-database-mirroring"></a>レプリケーションとデータベース ミラーリングを併用する場合の要件および注意事項  
 レプリケーションとデータベース ミラーリングを併用する場合、以下の要件および考慮事項に注意してください。  
  
-   プリンシパルとミラーはディストリビューターを共有する必要があります。 このディストリビューターにはリモート ディストリビューターを使用することをお勧めします。こうすることによって、パブリッシャーに予定外のフェールオーバーが発生した場合のフォールト トレランスが向上します。  
  
-   マージ レプリケーション、および読み取り専用サブスクライバーまたはキュー更新サブスクライバーを使用するトランザクション レプリケーションでは、パブリケーション データベースのミラーリングがサポートされます。 即時更新サブスクライバー、Oracle パブリッシャー、ピア ツー ピア トポロジのパブリッシャー、および再パブリッシュはサポートされません。  
  
-   ログイン、ジョブ、リンク サーバーなど、データベースの外部に存在するメタデータやオブジェクトはミラーにコピーされません。 これらのメタデータやオブジェクトをミラーで必要とする場合、手動でコピーする必要があります。 詳細については、「[役割の交代後のログインとジョブの管理 &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)」を参照してください。  
  
## <a name="configuring-replication-with-database-mirroring"></a>データベース ミラーリングを使用するレプリケーションの構成  
 レプリケーションとデータベース ミラーリングの構成には、以下の 5 つの手順があります。 各手順の詳細については、以下のセクションで説明します。  
  
1.  パブリッシャーを構成します。  
  
2.  データベース ミラーリングを構成します。  
  
3.  プリンシパルと同じディストリビューターを使用するようにミラーを構成します。  
  
4.  フェールオーバー用にレプリケーション エージェントを構成します。  
  
5.  プリンシパルおよびミラーをレプリケーション モニターに追加します。  
  
 手順 1. と手順 2. の実行順序は逆にすることもできます。  
  
#### <a name="to-configure-database-mirroring-for-a-publication-database"></a>パブリケーション データベースのデータベース ミラーリングを構成するには  
  
1.  パブリッシャーを構成します。  
  
    1.  リモート ディストリビューターの使用をお勧めします。 ディストリビューションの構成の詳細については、「 [ディストリビューションの構成](../../relational-databases/replication/configure-distribution.md)」を参照してください。  
  
    2.  スナップショット パブリケーション、トランザクション パブリケーション、およびマージ パブリケーションのデータベースを有効化できます。 複数の種類のパブリケーションを含むミラー データベースの場合、同一ノード上で [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)を使用し、両方の種類のパブリケーションに対してデータベースを有効化する必要があります。 たとえば、以下のストアド プロシージャの呼び出しをプリンシパルで実行できます。  
  
        ```  
        exec sp_replicationdboption @dbname='<PublicationDatabase>', @optname='publish', @value=true;  
        exec sp_replicationdboption @dbname='<PublicationDatabase>', @optname='mergepublish', @value=true;  
        ```  
  
         パブリケーションの作成の詳細については、「 [データとデータベース オブジェクトのパブリッシュ](../../relational-databases/replication/publish/publish-data-and-database-objects.md)」を参照してください。  
  
2.  データベース ミラーリングを構成します。 詳細については、「[Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)」および「[データベース ミラーリングの設定 &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)」を参照してください。  
  
3.  ディストリビューションをミラー用に構成します。 ミラー名をパブリッシャーとして指定し、プリンシパルと同一のディストリビューターおよびスナップショット フォルダーを指定します。 たとえば、ストアド プロシージャを使用してレプリケーションを構成する場合、ディストリビューターで [sp_adddistpublisher](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md) を実行し、次にミラーで [sp_adddistributor](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) を実行します。 **sp_adddistpublisher**の場合は、以下の手順を実行します。  
  
    -   **\@publisher** パラメーターの値にミラーのネットワーク名を設定します。  
  
    -   **\@working_directory** パラメーターの値にプリンシパルで使用するスナップショット フォルダーを設定します。  
  
4.  **-PublisherFailoverPartner** エージェント パラメーターの値にミラー名を指定します。 フェールオーバーの後、以下のエージェントでミラーを特定する場合にこのエージェント パラメーターが必要になります。  
  
    -   スナップショット エージェント (すべてのパブリケーション用)  
  
    -   ログ リーダー エージェント (すべてのトランザクション パブリケーション用)  
  
    -   キュー リーダー エージェント (キュー更新サブスクリプションをサポートするトランザクション パブリケーション用)  
  
    -   マージ エージェント (マージ サブスクリプション用)  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーション リスナー (replisapi.dll : Web 同期を使用して同期したマージ サブスクリプション用)  
  
    -   SQL マージ ActiveX コントロール (このコントロールを使用して同期したマージ サブスクリプション用)  
  
     ディストリビューション エージェントおよびディストリビューション ActiveX コントロールはパブリッシャーに接続しないため、このパラメーターがありません。  
  
     エージェント パラメーターの変更は、エージェントの次回起動時に反映されます。 エージェントを継続して実行している場合は、そのエージェントを停止して再起動する必要があります。 パラメーターは、エージェント プロファイルおよびコマンド プロンプトで指定できます。 詳細については、以下をご覧ください。  
  
    -   [レプリケーション エージェント コマンド プロンプト パラメーターを表示および変更する &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
     **-PublisherFailoverPartner** をエージェント プロファイルに追加して、プロファイルにミラー名を指定することをお勧めします。 たとえば、ストアド プロシージャを使用してレプリケーションを構成する場合、以下のように指定します。  
  
    ```  
    -- Execute sp_help_agent_profile in the context of the distribution database to get the list of profiles.  
    -- Select the profile id of the profile that needs to be updated from the result set.  
    -- In the agent_type column returned by sp_help_agent_profile:   
    -- 1 = Snapshot Agent; 2 = Log Reader Agent; 3 = Distribution Agent; 4 = Merge Agent; 9 = Queue Reader Agent.  
  
    exec sp_help_agent_profile;  
  
    -- Setting the -PublisherFailoverPartner parameter in the default Snapshot Agent profile (profile 1).  
    -- Execute sp_add_agent_parameter in the context of the distribution database.  
    exec sp_add_agent_parameter @profile_id = 1, @parameter_name = N'-PublisherFailoverPartner', @parameter_value = N'<Failover Partner Name>';  
  
    -- Setting the -PublisherFailoverPartner parameter in the default Merge Agent profile (profile 6).  
    -- Execute sp_add_agent_parameter in the context of the distribution database.  
    exec sp_add_agent_parameter @profile_id = 6, @parameter_name = N'-PublisherFailoverPartner', @parameter_value = N'<Failover Partner Name>';  
    ```  
  
5.  プリンシパルおよびミラーをレプリケーション モニターに追加します。 詳細については、「 [レプリケーション モニターのパブリッシャーの追加および削除](../../relational-databases/replication/monitor/add-and-remove-publishers-from-replication-monitor.md)」を参照してください。  
  
## <a name="maintaining-a-mirrored-publication-database"></a>ミラー化したパブリケーション データベースのメンテナンス  
 ミラー化したパブリケーション データベースのメンテナンスは、ミラー化していないデータベースの場合と基本的に同じです。ただし、以下の点に注意する必要があります。  
  
-   アクティブなサーバーで管理および監視を行う必要があります。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]では、アクティブなサーバーだけで、 **[ローカル パブリケーション]** フォルダー以下にパブリケーションが表示されます。 たとえば、ミラーへのフェールオーバーが発生した場合、パブリケーションがミラーで表示され、プリンシパルでは表示されなくなります。 データベースでミラーへのフェールオーバーが発生した場合、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] およびレプリケーション モニターを手動で更新して、変更を反映することが必要になる場合もあります。  
  
-   レプリケーション モニターでは、プリンシパルとミラーの両方に対するオブジェクト ツリー内にパブリッシャー ノードが表示されます。 プリンシパルがアクティブなサーバーの場合、パブリケーション情報はレプリケーション モニターのプリンシパル ノード以下のみに表示されます。  
  
     ミラーがアクティブなサーバーの場合は、次のように表示されます。  
  
    -   エージェントでエラーが発生している場合、エラーはプリンシパル ノードでのみ示され、ミラー ノードでは示されません。  
  
    -   プリンシパルが使用不可の場合、プリンシパル ノードとミラー ノードで、パブリケーションの同一の一覧が表示されます。 監視は、ミラー ノードのパブリケーションで実行する必要があります。  
  
-   ストアド プロシージャまたはレプリケーション管理オブジェクト (RMO) を使用して、ミラーでレプリケーションを管理する場合、パブリッシャー名を指定する際にはレプリケーションを有効にしたデータベースが使用するインスタンス名を指定する必要があります。 適切な名前を決定するには、 [publishingservername](../../t-sql/functions/replication-functions-publishingservername.md)関数を使用します。  
  
     パブリケーション データベースをミラー化した場合、ミラー データベースに格納されるレプリケーション メタデータとプリンシパル データベースに格納されるメタデータが同一になります。 その結果、プリンシパルでレプリケーションが有効なパブリケーション データベースでは、ミラーのシステム テーブルに格納されるパブリッシャーのインスタンス名は、ミラーではなくプリンシパルの名前になります。 これにより、パブリケーション データベースでミラーへのフェールオーバーが発生した場合のレプリケーションの構成およびメンテナンスが影響を受けます。 たとえば、フェールオーバーの後、ストアド プロシージャを使用してレプリケーションを構成し、プリンシパルで有効化されたパブリケーション データベースにプル サブスクリプションを追加する場合、**sp_addpullsubscription** または **sp_addmergepullsubscription** の **\@publisher** パラメーターにミラー名ではなくプリンシパル名を指定する必要があります。  
  
     ミラーへのフェールオーバーの後、ミラーでパブリケーション データベースを有効化する場合、システム テーブルに格納されるパブリッシャーのインスタンス名はミラー名となります。この場合、 **\@publisher** パラメーターにはミラー名を指定します。  
  
    > [!NOTE]  
    >  **sp_addpublication** などを使用する場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリッシャーに対してのみ **\@publisher** パラメーターがサポートされます。このような場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータベース ミラーリングとは無関係になります。  
  
-   フェールオーバーの後、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] でサブスクリプションを同期するには、サブスクライバーからプル サブスクリプションを同期し、アクティブなパブリッシャーからプッシュ サブスクリプションを同期します。  
  
### <a name="replication-behavior-if-mirroring-is-removed"></a>ミラーリングを解除した場合のレプリケーションの動作  
 パブリッシュされたデータベースからデータベース ミラーリングを解除する場合は、以下の点に注意してください。  
  
-   プリンシパルでパブリケーション データベースが既にミラー化されていない場合、元のプリンシパルに対するレプリケーションはそのまま動作します。  
  
-   パブリケーション データベースでプリンシパルからミラーへのフェールオーバーが発生した後、ミラーリング リレーションシップを無効化または解除した場合、レプリケーション エージェントがミラーに対して機能しなくなります。 プリンシパルが完全に失われた場合、ミラーのレプリケーションをいったん無効化し、その後パブリッシャーとして再構成します。  
  
-   データベース ミラーリングを完全に解除した場合、ミラー データベースが復旧状態になるため、動作させるためには復元を行う必要があります。 復旧したデータベースでレプリケーションがどのように動作するかは、KEEP_REPLICATION オプションを指定したかどうかによって異なります。 このオプションを指定すると、パブリッシュされたデータベースをバックアップが作成されたサーバーと異なるサーバーに復元する場合に、復元操作でレプリケーションの設定が強制的に保存されます。 他のパブリケーション データベースが使用できない場合にのみ、KEEP_REPLICATION オプションを指定してください。 他のパブリケーション データベースが稼働中でレプリケーションを実行中の場合、このオプションはサポートされません。 KEEP_REPLICATION の詳細については、「[RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)」を参照してください。  
  
## <a name="log-reader-agent-behavior"></a>ログ リーダー エージェントの動作  
 データベース ミラーリングのさまざまな動作モードに対するログ リーダー エージェントの動作を次の表に示します。  
  
|動作モード|ミラーが使用できない場合のログ リーダー エージェントの動作|  
|--------------------|------------------------------------------------------------|  
|自動フェールオーバーを伴う高い安全性モード|ミラーが使用できない場合、ログ リーダー エージェントはコマンドをディストリビューション データベースに反映します。 ミラーがオンラインに戻り、プリンシパルからすべてのトランザクションを受け取るまで、プリンシパルからミラーへのフェールオーバーは発生しません。|  
|高パフォーマンス モード|ミラーが使用できない場合、プリンシパル データベースは無防備な (つまり、ミラー化されていない) 状態で稼働していることになります。 ただし、ログ リーダー エージェントはミラーで保存されたトランザクションのみをレプリケートします。 サービスが強制され、ミラー サーバーがプリンシパルとしての役割を回復すると、ログ リーダー エージェントがミラーに対して機能し、新しいトランザクションの取得を開始します。<br /><br /> ミラーがプリンシパルより遅れた場合、レプリケーションの待機時間が増大することに注意してください。|  
|自動フェールオーバーを伴わない高い安全性モード|コミット済みのすべてのトランザクションがミラーのディスクに保存されることが保証されます。 ログ リーダー エージェントはミラーで保存されたトランザクションのみをレプリケートします。 ミラーが使用できない場合、プリンシパルのデータベースが停止します。そのため、ログ リーダー エージェントがレプリケートするトランザクションがなくなります。|  
  
## <a name="see-also"></a>参照  
 [SQL Server のレプリケーション](../../relational-databases/replication/sql-server-replication.md)   
 [ログ配布とレプリケーション &#40;SQL Server&#41;](../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md)  
  
  
