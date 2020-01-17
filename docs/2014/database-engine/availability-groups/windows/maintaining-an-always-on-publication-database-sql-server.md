---
title: AlwaysOn パブリケーション データベース (SQL Server) のメンテナンス |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 55b345fe-2eb9-4b04-a900-63d858eec360
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a862c5c9cea1087f54a4dbff13b6c39eb5e39385
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62791991"
---
# <a name="maintaining-an-alwayson-publication-database-sql-server"></a>AlwaysOn パブリケーション データベースのメンテナンス (SQL Server)
  このトピックでは、AlwaysOn 可用性グループを使用するときのパブリケーション データベースのメンテナンスについての特別な考慮事項について説明します。  
  
 
  
##  <a name="MaintainPublDb"></a> 可用性グループでのパブリッシュされたデータベースのメンテナンス  
 AlwaysOn パブリケーション データベースのメンテナンスは、通常のパブリケーション データベースのメンテナンスと基本的に同じです。ただし、次の点を考慮する必要があります。  
  
-   管理は、プライマリ レプリカ ホストで行う必要があります。 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]では、プライマリ レプリカ ホストと読み取り可能なセカンダリ レプリカの **[ローカル パブリケーション]** フォルダーにパブリケーションが表示されます。 フェールオーバー後、プライマリに昇格したセカンダリが読み取り不可である場合は、変更を反映させるために [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] を手動で更新する必要がある場合があります。  
  
-   レプリケーション モニターは、常に元のパブリッシャーの下でパブリケーション情報を表示します。 ただし、元のパブリッシャーをサーバーとして追加することで、この情報を任意のレプリカからレプリケーション モニターで表示することができます。  
  
-   ストアド プロシージャまたはレプリケーション管理オブジェクト (RMO) を使用して現在のプライマリでレプリケーションを管理する場合、パブリッシャー名を指定する際には、データベースのレプリケーションを有効にしたインスタンス (元のパブリッシャー) の名前を指定する必要があります。 適切な名前を決定するには、`PUBLISHINGSERVERNAME` 関数を使用します。 パブリッシング データベースを可用性グループに参加させると、セカンダリ データベース レプリカに格納されているレプリケーション メタデータは、プライマリにあるレプリケーション メタデータと同一になります。 その結果、プライマリでレプリケーションが有効なパブリケーション データベースでは、セカンダリのシステム テーブルに格納されるパブリッシャー インスタンス名は、セカンダリではなくプライマリの名前になります。 これにより、パブリケーション データベースがセカンダリにフェールオーバーした場合に、レプリケーションの構成およびメンテナンスに影響が出ます。 たとえば、フェールオーバー後は、セカンダリでストアド プロシージャでレプリケーションを構成して、別のレプリカで有効化されたパブリケーション データベースへのプル サブスクリプションが必要の場合は、代わりに元のパブリッシャーの名前を指定する必要があります、として現在のパブリッシャー、 *@publisher* パラメーターの`sp_addpullsubscription`または`sp_addmergepulllsubscription`します。 ただし、フェールオーバー後にパブリケーション データベースを有効にした場合、システム テーブルに格納されるパブリッシャー インスタンス名は、現在のプライマリ ホストの名前になります。 この場合、 *@publisher* パラメーターに現在のプライマリ レプリカのホスト名を使用します。  
  
    > [!NOTE]  
    >  一部のプロシージャなど`sp_addpublication`、 *@publisher* パラメーターがのインスタンスではないパブリッシャーに対してのみサポートされている[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]; このような場合は関係しません[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]AlwaysOn。  
  
-   フェールオーバー後に [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] でサブスクリプションを同期するには、サブスクライバーからプル サブスクリプションを同期し、アクティブなパブリッシャーからプッシュ サブスクリプションを同期します。  
  
##  <a name="RemovePublDb"></a> 可用性グループからのパブリッシュされたデータベースの削除  
 パブリッシュされたデータベースを可用性グループから削除する場合、またはパブリッシュされたメンバー データベースを含む可用性グループを削除する場合、次の点を考慮します。  
  
-   実行する必要がある元のパブリッシャーでパブリケーション データベースを可用性グループのプライマリ レプリカから削除する場合`sp_redirect_publisher`の値を指定せず、 *@redirected_publisher* パラメーターを削除するには、パブリッシャー/データベース ペアをリダイレクトします。  
  
    ```  
    EXEC sys.sp_redirect_publisher   
        @original_publisher = 'MyPublisher',  
        @published_database = 'MyPublishedDB';  
    ```  
  
     データベースはプライマリで復旧中の状態のままとなり、復元する必要があります。 データベースを復元すると、レプリケーションは元のパブリッシャーに対して変更なしで動作します。  
  
-   パブリケーション データベースが元のパブリッシャーからレプリカにフェールオーバーし、そのパブリケーション データベースを可用性グループのプライマリ レプリカから削除した場合、ストアド プロシージャ `sp_redirect_publisher` を使用して元のパブリッシャーを新しいパブリッシャーに明示的にリダイレクトします。 データベースは復旧中の状態のままとなり、復元する必要があります。 データベースを復元すると、レプリケーションは可用性グループの下で引き続き機能します。  
  
    ```  
    EXEC sys.sp_redirect_publisher   
        @original_publisher = 'MyPublisher',  
        @published_database = 'MyPublishedDB',  
        @redirected_publisher = 'MyNewPublisher';  
    ```  
  
     元のパブリッシャーのリモート サーバーは、以降にアクセスできなくなる場合でもディストリビューターから削除しないでください。 ディストリビューターでパブリケーション メタデータ クエリに対応するために、元のパブリッシャーのサーバー メタデータが必要です。  
  
-   可用性グループ全体を削除した場合、メンバーであるレプリケートされたデータベースについての動作は、パブリッシュされたデータベースを可用性グループから削除した場合と同じです。 データベースを復元し、リダイレクトを変更すると、レプリケーションを最後のプライマリから再開できます。 データベースを元のパブリッシャーで復元した場合、リダイレクトを削除する必要があります。 データベースを別のホストで復元した場合、新しいホストに対してリダイレクトを明示的に指定する必要があります。  
  
    > [!NOTE]  
    >  メンバー データベースをパブリッシュした可用性グループを削除した場合、またはパブリッシュされたデータベースを可用性グループから削除した場合、パブリッシュされたデータベースのすべてのコピーは復旧中の状態のままとなります。 それぞれを復元すると、パブリッシュされたデータベースとして表示されます。 1 つのコピーだけをパブリケーション メタデータで保持する必要があります。 パブリッシュされたデータベース コピーのレプリケーションを無効にするには、最初にすべてのサブスクリプションとパブリケーションをデータベースから削除します。  
  
     `sp_dropsubscription` を実行してパブリケーション サブスクリプションを削除します。 アクティブなパブリッシング データベースのメタデータをディストリビューターで保持するために、 *@ignore_distributributor* パラメーターを 1 に設定します。  
  
    ```  
    USE MyDBName;  
    GO  
  
    EXEC sys.sp_dropsubscription   
        @subscriber = 'MySubscriber',  
        @publication = 'MyPublication',  
        @article = 'all',  
        @ignore_distributor = 1;  
    ```  
  
     `sp_droppublication` を実行してすべてのパブリケーションを削除します。 この場合も、アクティブなパブリッシング データベースのメタデータをディストリビューターで保持するために、 *@ignore_distributor* パラメーターを 1 に設定します。  
  
    ```  
    EXEC sys.sp_droppublication   
        @publication = 'MyPublication',  
        @ignore_distributor = 1;  
    ```  
  
     `sp_replicationdboption` を実行してデータベースのレプリケーションを無効にします。  
  
    ```  
    EXEC sys.sp_replicationdboption  
        @dbname = 'MyDBName',  
        @optname = 'publish',  
        @value = 'false';  
    ```  
  
     この時点で、パブリッシュされたデータベースのコピーを保持または削除できます。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [AlwaysOn 可用性グループ (SQL Server) のレプリケーションを構成します。](always-on-availability-groups-sql-server.md)  
  
-   [レプリケーション、変更の追跡、変更データ キャプチャ、および AlwaysOn 可用性グループ&#40;SQL Server&#41;](replicate-track-change-data-capture-always-on-availability.md)  
  
-   [レプリケーション管理に関する FAQ](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)  
  
-   [レプリケーション サブスクライバーと AlwaysOn 可用性グループ&#40;SQL Server&#41;](replication-subscribers-and-always-on-availability-groups-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [前提条件、制限事項、および AlwaysOn 可用性グループの推奨事項&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループ:相互運用性 (SQL Server)](always-on-availability-groups-interoperability-sql-server.md)   
 [SQL Server のレプリケーション](../../../relational-databases/replication/sql-server-replication.md)  
  
  
