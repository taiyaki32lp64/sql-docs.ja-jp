---
title: レプリケーション、変更の追跡、変更データ キャプチャ、および AlwaysOn 可用性グループ (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- change tracking [SQL Server], AlwaysOn Availability Groups
- change data capture [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: e17a9ca9-dd96-4f84-a85d-60f590da96ad
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c52283ce9d512da6dc2e5ad05a4c8356524bef01
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62814058"
---
# <a name="replication-change-tracking-change-data-capture-and-alwayson-availability-groups-sql-server"></a>レプリケーション、変更の追跡、変更データ キャプチャ、および AlwaysOn 可用性グループ (SQL Server)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]のレプリケーション、変更データ キャプチャ (CDC)、および変更の追跡 (CT) がサポートされています。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] は、高可用性と追加のデータベース復旧機能を提供します。  
  
 
  
##  <a name="Overview"></a> AlwaysOn 可用性グループのレプリケーションの概要  
  
###  <a name="PublisherRedirect"></a> パブリッシャー リダイレクト  
 パブリッシュされたデータベースが [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]に対応している場合、パブリッシング データベースへのエージェント アクセス権を提供するディストリビューターは、redirected_publishers エントリで構成されます。 これらのエントリは、パブリッシャーとパブリッシング データベースへの接続に可用性グループ リスナー名を使用して、最初に構成されていたパブリッシャー/データベース ペアをリダイレクトします。 可用性グループ リスナー名を介して確立された接続は、フェールオーバーに失敗します。 フェールオーバー後にレプリケーション エージェントを再起動すると、接続は自動的に新しいプライマリにリダイレクトされます。  
  
 AlwaysOn 可用性グループでセカンダリ データベースをパブリッシャーにすることはできません。 レプリケーションを [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]と組み合わせている場合、再パブリッシュはサポートされません。  
  
 パブリッシュされたデータベースが可用性グループのメンバーであり、パブリッシャーをリダイレクトする場合は、その可用性グループに関連付けられている可用性グループ リスナー名にリダイレクトする必要があります。 明示的なノードにリダイレクトさせることはできません。  
  
> [!NOTE]  
>  セカンダリ レプリカにフェールオーバーした後、レプリケーション モニターは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のパブリッシング インスタンスの名前を調整できないため、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の元のプライマリ インスタンスの名前を引き続き使ってレプリケーション情報が表示されます。 フェールオーバー後は、トレーサー トークンはレプリケーション モニターを使用して入力できませんが、新しいパブリッシャーで [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して入力されたトレース トークンがレプリケーション モニターに表示されます。  
  
###  <a name="Changes"></a> AlwaysOn 可用性グループをサポートするためにレプリケーション エージェントへの変更の概要  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]をサポートするために、3 つのレプリケーション エージェントが変更されました。 ログ リーダー、スナップショット、およびマージ エージェントは、リダイレクトされたパブリッシャーについてディストリビューション データベースにクエリを実行し、リダイレクトされたパブリッシャーが宣言されていた場合は、返された可用性グループ リスナー名を使用してデータベース パブリッシャーに接続するように変更されました。  
  
 既定では、エージェントがディストリビューターにクエリを実行して、元のパブリッシャーがリダイレクトされたかどうかを判断する場合、リダイレクトされたホストがエージェントに戻る前に、現在のターゲットまたはリダイレクトの適合性が検証されます。 これは推奨される動作です。 ただし、エージェントの起動が非常に頻繁に行われる場合、検証ストアド プロシージャに関連するオーバーヘッドのコストが高くなる可能性があります。 新しいコマンド ライン スイッチ *BypassPublisherValidation*が、ログ リーダー、スナップショット、およびマージ エージェントに追加されました。 スイッチが使用される場合、リダイレクトされたパブリッシャーはエージェントに即時に戻り、検証ストアド プロシージャの実行が省略されます。  
  
 検証ストアド プロシージャから返されるエラーは、エージェントの履歴ログに記録されます。 重大度が 16 以上のエラーが発生すると、エージェントが終了します。 新しいプライマリにフェールオーバーするときに、パブリッシュされたデータベースからの予期される切断を処理するために、いくつかの再試行機能がエージェントに組み込まれています。  
  
#### <a name="log-reader-agent-modifications"></a>ログ リーダー エージェントの変更  
 ログ リーダー エージェントでは次の点が変更されています。  
  
-   **レプリケートされたデータベースの一貫性**  
  
     パブリッシュされたデータベースが AlwaysOn 可用性グループのメンバーである場合、既定では、ログ リーダーはすべての可用性グループ セカンダリ レプリカでまだ書き込まれていないログ レコードを処理しません。 こうすることで、フェールオーバー時にサブスクライバーにレプリケートされるすべての行が、新しいプライマリにも存在することが保証されます。  
  
     パブリッシャーに AlwaysOn 可用性レプリカが 2 つ (プライマリが 1 つとセカンダリが 1 つ) しかない場合にフェールオーバーが発生すると、すべてのセカンダリ データベースがオンラインに戻るか、エラーが発生したセカンダリ レプリカが可用性グループから削除されるまでログ リーダーが前へ進まないため、元のプライマリ レプリカはダウンしたままになります。 AlwaysOn がセカンダリ データベースに変更を書き込むことができないので、セカンダリ データベースに対して実行されているログ リーダーは前へ進みません。 ディザスター リカバリー機能を維持しながら、ログ リーダーが前へ進めるようにするには、ALTER AVAILABITY GROUP <group_name> REMOVE REPLICA を使用して、元のプライマリ レプリカを可用性グループから削除します。 その後、新しいセカンダリ レプリカを可用性グループに追加します。  
  
-   **トレース フラグ 1448**  
  
     トレース フラグ 1448 は、非同期セカンダリ レプリカで変更の受信が確認されていない場合でも、レプリケーション ログ リーダーが前へ進めるようにします。 このトレース フラグが有効でも、ログ リーダーは常に同期セカンダリ レプリカを待機します。 ログ リーダーは同期セカンダリ レプリカの最小 ack を超えることはありません。 このトレース フラグは、可用性グループ、可用性データベース、またはログ リーダー インスタンスだけでなく、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスにも適用されます。 再起動しなくても、トレース フラグはすぐに有効になります。 このトレース フラグは、事前にアクティブにすることも、非同期セカンダリ レプリカで障害が発生したときにアクティブにすることもできます。  
  
###  <a name="StoredProcs"></a> AlwaysOn をサポートするストアド プロシージャ  
  
-   **sp_redirect_publisher**  
  
     ストアド プロシージャ **sp_redirect_publisher** を使用すると、既存のパブリッシャー/データベース ペアのリダイレクトされたパブリッシャーを指定できます。 パブリッシャー データベースが可用性グループに属している場合、リダイレクトされたパブリッシャーは可用性グループ リスナー名です。  
  
-   **sp_get_redirected_publisher**  
  
     ストアド プロシージャ **sp_get_redirected_publisher** は、パブリッシャー/データベース ペアに定義済みのリダイレクトされたパブリッシャーがあるかどうかを判断するために、レプリケーション エージェントがディストリビューターに対してクエリを実行するときに使用されます。 このストアド プロシージャには、2 つの目的があります。 1 つ目は、元のパブリッシャーがリダイレクトされたかどうかをエージェントが判断できるようにすることです。 2 つ目は、リダイレクトの対象ノードが、指定されたデータベースのパブリッシャーとして適しているかどうかを検証する、ディストリビューターで実行される検証ストアド プロシージャ (**sp_validate_redirected_publisher**) を開始することです。  
  
     このストアド プロシージャを実行するには、呼び出し元はディストリビューション データベースの **sysadmin** サーバー ロールおよび **db_owner** データベース ロールのメンバーであるか、パブリッシャー データベースと関連付けられている定義済みパブリケーションの **パブリケーション アクセス リスト** のメンバーである必要があります。  
  
-   **sp_validate_redirected_publisher**  
  
     このストアド プロシージャは、パブリッシュされたデータベースを現在のパブリッシャーがホストできることを検証しようとします。 パブリッシュされたデータベースの現在のホストがレプリケーションをサポートできることを確認するために、いつでも呼び出すことができます。  
  
-   **sp_validate_replicate_hosts_as_publishers**  
  
     現在のプライマリがパブリッシャー データベースのレプリケーション パブリッシャーとして機能できることを確認できるのはエージェントにとって便利ですが、AlwaysOn 可用性データベースのレプリケーション トポロジ全体の有効性を確立するには、より一般的な検証機能が必要です。 ストアド プロシージャ **sp_validate_replica_hosts_as_publishers** は、このニーズを満たすように設計されています。  
  
     このストアド プロシージャは、常に手動で実行されます。 呼び出し元は、ディストリビューターでの **sysadmin** であるか、ディストリビューション データベースの **dbowner** であるか、またはパブリッシャー データベースのパブリケーションの **パブリケーション アクセス リスト** のメンバーである必要があります。 また、呼び出し元のログインは、すべての可用性レプリカ ホストに対して有効なログインであり、パブリッシャー データベースに関連付けられている可用性データベースに対する select 特権を持っている必要があります。  
  
###  <a name="CDC"></a> 変更データ キャプチャ  
 障害が発生してもデータベースを引き続き使用できるだけでなく、データベース テーブルへの変更も引き続き監視され、CDC 変更テーブルに格納されることを保証するために、変更データ キャプチャ (CDC) が有効になっているデータベースで [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] を利用できます。 CDC と [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の構成順序は重要ではありません。 CDC 対応データベースは [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]に追加でき、AlwaysOn 可用性グループのメンバーであるデータベースでは CDC を有効にできます。 ただし、どちらの場合も、CDC 構成は常に現在または目的のプライマリ レプリカで実行されます。 CDC はログ リーダー エージェントを使用するため、このトピックの「 **ログ リーダー エージェントの変更** 」に記載されているのと同じ制限事項があります。  
  
-   **レプリケーションなしでの変更データ キャプチャの変更の取得**  
  
     データベースで CDC が有効になっていて、レプリケーションは有効になっていない場合、ログから変更を取得して CDC 変更テーブルに格納するために使用されるキャプチャ プロセスは、CDC ホストで独自の SQL エージェント ジョブとして実行されます。  
  
     フェールオーバー後に変更の取得を再開するには、ローカル キャプチャ ジョブを作成するために、新しいプライマリでストアド プロシージャ **sp_cdc_add_job** を実行する必要があります。  
  
     次の例では、キャプチャ ジョブを作成します。  
  
    ```  
    EXEC sys.sp_cdc_add_job @job_type = 'capture';  
    ```  
  
-   **レプリケーションを使用した変更データ キャプチャの変更の取得**  
  
     データベースで CDC とレプリケーションの両方が有効になっている場合は、ログ リーダーが CDC 変更テーブルのデータ設定を処理します。 この場合、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] を利用するためにレプリケーションで使用される手法によって、フェールオーバー後も引き続き変更がログから取得され、CDC 変更テーブルに格納されることが保証されます。 変更テーブルにデータが設定されるようにするために、この構成の CDC に対して何も追加で行う必要はありません。  
  
-   **変更データ キャプチャのクリーンアップ**  
  
     新しいプライマリ データベースで適切なクリーンアップが確実に行われるように、ローカル クリーアップ ジョブを必ず作成する必要があります。 次の例では、クリーンアップ ジョブを作成します。  
  
    ```  
    EXEC sys.sp_cdc_add_job @job_type = 'cleanup';  
    ```  
  
    > [!NOTE]  
    >  フェールオーバーの前にすべてのフェールオーバー ターゲット候補でジョブを作成し、ホストの可用性レプリカが新しいプライマリ レプリカになるまで無効としてマークしておく必要があります。 ローカル データベースがセカンダリ データベースになったときに、古いプライマリ データベースで実行されている CDC ジョブも無効にする必要があります。 ジョブを無効/有効にするには、[sp_update_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql) の *@enabled* オプションを使用します。 CDC ジョブの作成の詳細については、「 [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql)のレプリケーション、変更データ キャプチャ (CDC)、および変更の追跡 (CT) がサポートされています。  
  
-   **AlwaysOn プライマリ データベースのレプリカへの CDC ロールの追加**  
  
     CDC に対してテーブルを有効にした場合は、データベース ロールをキャプチャ インスタンスに関連付けることができます。 ロールが指定されている場合、CDC テーブル値関数を使用してテーブルの変更にアクセスするユーザーは、追跡されるテーブル列への選択アクセス権を持つだけでなく、名前付きロールのメンバーでもある必要があります。 指定したロールが存在しない場合は、ロールが作成されます。 AlwaysOn プライマリ データベースにデータベース ロールが自動的に追加されると、ロールは可用性グループのセカンダリ データベースにも反映されます。  
  
-   **CDC 変更データにアクセスするクライアント アプリケーションと Always On**  
  
     変更テーブル データにアクセスするためにテーブル値関数 (TVF) またはリンク サーバーを使用するクライアント アプリケーションには、フェールオーバー後に適切な CDC ホストを検索する機能も必要です。 可用性グループ リスナー名は、接続のターゲットを別のホストに透過的に再指定できるようにするために、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] によって提供されるメカニズムです。 可用性グループに関連付けられた可用性グループ リスナー名は、TCP 接続文字列で使用できるようになります。 2 つの異なる接続シナリオが、可用性グループ リスナー名を通じてサポートされます。  
  
    -   接続要求が常に現在のプライマリ レプリカに送られることを保証する。  
  
    -   接続要求が読み取り専用セカンダリ レプリカに送られることを保証する。  
  
     読み取り専用セカンダリ レプリカの検索にルーティング リストを使用する場合は、可用性グループの読み取り専用ルーティング リストも定義する必要があります。 読み取り可能セカンダリへのルーティングアクセスの詳細については、「 [読み取り専用ルーティングの可用性レプリカを構成するには](../../listeners-client-connectivity-application-failover.md#ConfigureARsForROR)」を参照してください。  
  
    > [!NOTE]  
    >  可用性グループ データベース レプリカにアクセスするには、可用性グループ リスナー名の作成およびクライアント アプリケーションによる可用性グループ リスナー名の使用に関連するいくらかの伝達の遅延があります。  
  
     次のクエリを使用して、可用性グループ リスナー名が CDC データベースをホストしている可用性グループに対して定義されているかどうかを確認します。 クエリは、可用性グループ リスナー名が作成されている場合に、それを返します。  
  
    ```  
    SELECT dns_name   
    FROM sys.availability_group_listeners AS l  
    INNER JOIN sys.availability_databases_cluster AS d  
        ON l.group_id = d.group_id  
    WHERE d.database_name = N'MyCDCDB';  
    ```  
  
-   **読み取り可能なセカンダリ レプリカへのクエリ負荷のリダイレクト**  
  
     多くの場合、クライアント アプリケーションは常に現在のプライマリ レプリカに接続しようとしますが、これが [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を利用する唯一の方法というわけではありません。 可用性グループが読み取り可能なセカンダリ レプリカをサポートするように構成されている場合、変更データはセカンダリ ノードからも収集できます。  
  
     可用性グループが構成されている場合は、SECONDARY_ROLE に関連付けられている ALLOW_CONNECTIONS 属性を使用して、サポートされているセカンダリ アクセスの種類を指定します。 ALL として構成した場合、セカンダリへのすべての接続が許可されますが、成功するのは読み取り専用アクセスを必要とする接続だけです。 READ_ONLY として構成した場合、接続を成功させるには、セカンダリ データベースへの接続時に読み取り専用の目的を指定する必要があります。 詳細については、「[可用性レプリカでの読み取り専用アクセスの構成 &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)」を参照してください。  
  
     次のクエリを使用して、読み取り可能なセカンダリ レプリカに接続するために読み取り専用の目的が必要かどうかを確認できます。  
  
    ```  
    SELECT g.name AS AG, replica_server_name, secondary_role_allow_connections_desc  
    FROM sys.availability_replicas AS r  
    JOIN sys.availability_groups AS g  
        ON r.group_id = g.group_id  
    WHERE g.name = N'MY_AG_NAME;  
    ```  
  
     可用性グループ リスナー名または明示的なノード名を使用してセカンダリ レプリカを検索できます。 可用性グループ リスナー名を使用すると、アクセスは適切なセカンダリ レプリカに送られます。  
  
     ときに`sp_addlinkedserver`セカンダリにアクセスするリンク サーバーを作成するために使用、 *@datasrc* 、可用性グループ リスナー名または明示的なサーバー名、パラメーターを使用し、  *@provstr* パラメーターを使用して読み取り専用の目的を指定します。  
  
    ```  
    EXEC sp_addlinkedserver   
    @server = N'linked_svr',   
    @srvproduct=N'SqlServer',  
    @provider=N'SQLNCLI11',   
    @datasrc=N'AG_Listener_Name',   
    @provstr=N'ApplicationIntent=ReadOnly',   
    @catalog=N'MY_DB_NAME';  
    ```  
  
-   **CDC 変更データとドメイン ログインへのクライアント アクセス**  
  
     一般に、AlwaysOn 可用性グループのメンバーであるデータベースに存在する変更データへのクライアント アクセスには、ドメイン ログインを使用する必要があります。 フェールオーバー後に変更データへの継続的なアクセスを保証するには、ドメイン ユーザーに、可用性グループ レプリカをサポートするすべてのホストに対するアクセス権限が必要です。 データベース ユーザーがプライマリ レプリカのデータベースに追加され、ユーザーがドメイン ログインに関連付けられている場合、データベース ユーザーはセカンダリ データベースに反映され、引き続き指定されたドメイン ログインに関連付けられます。 新しいデータベース ユーザーが SQL Server 認証ログインに関連付けられている場合、セカンダリ データベースのユーザーはログインなしで反映されます。 関連付けられた [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証ログインを使用して、データベース ユーザーが最初に定義されたプライマリの変更データにアクセスできますが、ノードはアクセスが可能な唯一のノードです。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証ログインは、セカンダリ データベースのデータにアクセスすることも、データベース ユーザーが定義された元のデータベース以外の新しいプライマリ データベースのデータにアクセスすることもできません。  
  
###  <a name="CT"></a> 変更の追跡  
 変更の追跡 (CT) が有効になっているデータベースは、AlwaysOn 可用性グループに含めることができます。 追加の構成は必要ありません。 変更データにアクセスするために CDC テーブル値関数 (TVF) を使用する変更の追跡クライアント アプリケーションには、フェールオーバー後にプライマリ レプリカを検索する機能が必要です。 クライアント アプリケーションが可用性グループ リスナー名を通じて接続する場合、接続要求は常に現在のプライマリ レプリカに適切に送られます。  
  
> [!NOTE]  
>  変更の追跡データは、常にプライマリ レプリカから取得する必要があります。 セカンダリ レプリカから変更データにアクセスしようとすると、次のエラーが発生します。  
>   
>  メッセージ 22117、レベル 16、状態 1、行 1  
>   
>  セカンダリ レプリカのメンバーであるデータベース (セカンダリ データベース) では、変更の追跡はサポートされていません。 変更の追跡クエリをプライマリ レプリカのデータベースに対して実行します。  
  
##  <a name="Prereqs"></a> レプリケーションの使用に関する前提条件、制限、および考慮事項  
 ここでは、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]でレプリケーションを配置する際の前提条件、制限、推奨などの考慮事項について説明します。  
  
### <a name="prerequisites"></a>前提条件  
  
-   単一の可用性グループ内でトランザクション レプリケーションとパブリッシング データベースを使用する場合は、パブリッシャーとディストリビューターの両方が少なくとも [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]を実行する必要があります。 サブスクライバーは、それより低いレベルの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]を使用することもできます。  
  
-   単一の可用性グループ内でマージ レプリケーションとパブリッシング データベースを使用する場合は、次のことが適用されます。  
  
    -   プッシュ サブスクリプション: パブリッシャーとディストリビューターの両方が少なくとも [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] を実行する必要があります。  
  
    -   プル サブスクリプション: パブリッシャー、ディストリビューター、およびサブスクライバー データベースは、少なくとも [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 上にある必要があります。 これは、可用性グループがセカンダリにフェールオーバーする方法を、サブスクライバー上のマージ エージェントが把握しておく必要があることが原因です。  
  
-   ディストリビューション データベースを可用性グループに配置することはサポートされていません。  
  
-   パブリッシャーのインスタンスは、AlwaysOn 可用性グループに参加するために必要なすべての前提条件を満たす必要があります。 詳細については、「[AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)」を参照してください。  
  
### <a name="restrictions"></a>制限  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]のレプリケーションでサポートされている組み合わせは次のとおりです。  
  
|||||  
|-|-|-|-|  
||**パブリッシャー**|**ディストリビューター** <sup>3</sup>|**サブスクライバー (Subscriber)**|  
|**トランザクション**|可<sup>1</sup>|いいえ|はい<sup>2</sup>|  
|**P2P**|いいえ|いいえ|いいえ|  
|**Merge**|はい|いいえ|はい<sup>2</sup>|  
|**スナップショット**|はい|いいえ|はい<sup>2</sup>|  
  
 <sup>1</sup>双方向相互トランザクション レプリケーションのサポートは含まれません。  
  
 <sup>2</sup>レプリカ データベースへのフェールオーバーは手動で行います。 自動フェールオーバーは提供されていません。  
  
 <sup>3</sup>で使用するディストリビューター データベースはサポートされていません[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]またはデータベース ミラーリングします。  
  
### <a name="considerations"></a>考慮事項  
  
-   [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] またはデータベース ミラーリングでディストリビューション データベースを使用することはできません。 レプリケーション構成は、ディストリビューターが構成された SQL Server インスタンスと結び付けられます。そのため、ディストリビューション データベースはミラー化またはレプリケートできません。 ディストリビューターの高可用性を実現するには、SQL Server のフェールオーバー クラスターを使用します。 詳細については、「[Always On フェールオーバー クラスター インスタンス (SQL Server)](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)」を参照してください。  
  
-   セカンダリ データベースへのサブスクライバーのフェールオーバーはサポートされていますが、かなり複雑な手動での手順になります。 手順は、ミラー化されたサブスクライバー データベースをフェールオーバーするために使用される方法と本質的には同じです。 可用性グループに参加するには、サブスクライバーは [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 以降を実行している必要があります。  
  
-   ログイン、ジョブ、リンク サーバーなど、データベースの外部に存在するメタデータやオブジェクトはセカンダリ レプリカに反映されません。 フェールオーバー後に新しいプライマリ データベースでこれらのメタデータやオブジェクトが必要な場合は、手動でコピーする必要があります。 詳細については、「 [可用性グループのデータベースのためのログインとジョブの管理 &#40;SQL Server&#41;](../../logins-and-jobs-for-availability-group-databases.md)と呼ばれるプロセスで交換されることがあります。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **レプリケーション**  
  
-   [AlwaysOn 可用性グループ (SQL Server) のレプリケーションを構成します。](always-on-availability-groups-sql-server.md)  
  
-   [AlwaysOn パブリケーション データベースのメンテナンス&#40;SQL Server&#41;](maintaining-an-always-on-publication-database-sql-server.md)  
  
-   [レプリケーション管理に関する FAQ](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)  
  
 **Change data capture**  
  
-   [変更データ キャプチャの有効化と無効化 &#40;SQL Server&#41;](../../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)  
  
-   [変更データ キャプチャの管理と監視 &#40;SQL Server&#41;](../../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
-   [変更データの処理 &#40;SQL Server&#41;](../../../relational-databases/track-changes/work-with-change-data-sql-server.md)  
  
 **Change tracking**  
  
-   [変更の追跡の有効化と無効化 &#40;SQL Server&#41;](../../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)  
  
-   [変更の追跡の管理 &#40;SQL Server&#41;](../../../relational-databases/track-changes/manage-change-tracking-sql-server.md)  
  
-   [変更の追跡のしくみ &#40;SQL Server&#41;](../../../relational-databases/track-changes/work-with-change-tracking-sql-server.md)  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション サブスクライバーと AlwaysOn 可用性グループ&#40;SQL Server&#41;](replication-subscribers-and-always-on-availability-groups-sql-server.md)   
 [前提条件、制限事項、および AlwaysOn 可用性グループの推奨事項&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループ:相互運用性 (SQL Server)](always-on-availability-groups-interoperability-sql-server.md) [AlwaysOn フェールオーバー クラスター インスタンス (SQL Server)](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)   
 [変更データ キャプチャについて &#40;SQL Server&#41;](../../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [変更の追跡について &#40;SQL Server&#41;](../../../relational-databases/track-changes/about-change-tracking-sql-server.md)   
 [SQL Server のレプリケーション](../../../relational-databases/replication/sql-server-replication.md)   
 [データ変更の追跡 &#40;SQL Server&#41;](../../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql)  
  
  
