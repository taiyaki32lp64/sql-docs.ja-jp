---
title: パラメーター化されたフィルターを使用したスナップショットの作成 (マージ)
description: パラメーター化されたフィルターを使用して、マージ パブリケーションのスナップショットを作成する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- parameterized filters [SQL Server replication], snapshots
- snapshots [SQL Server replication], parameterized filters and
- filters [SQL Server replication], parameterized
ms.assetid: 00dfb229-f1de-4d33-90b0-d7c99ab52dcb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 88c43b8d37861e52b5bda5afc0a38753f2b70d6e
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321834"
---
# <a name="create-a-snapshot-for-a-merge-publication-with-parameterized-filters"></a>パラメーター化されたフィルターを使用したパブリケーションのスナップショットの作成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、パラメーター化されたフィルターでマージ パブリケーションのスナップショットを作成する方法ついて説明します。  

パラメーター化された行フィルターがマージ パブリケーションで使用される場合、レプリケーションは 2 つの要素から成るスナップショットを持つ各サブスクリプションを初期化します。 まず、レプリケーションに必要なすべてのオブジェクトとパブリッシュされたオブジェクトのスキーマが含まれるスキーマ スナップショットが作成されます。ただしデータは含まれません。 次に、スキーマ スナップショットからのオブジェクトとスキーマが含まれるスナップショットと、サブスクリプションのパーティションに属するデータを使用して、各サブスクリプションが初期化されます。 複数のサブスクリプションが特定のパーティションを受信する場合 (つまり、同じスキーマとデータを受信する場合)、そのパーティションのスナップショットは 1 回しか作成されません。複数のサブスクリプションは、同じスナップショットから初期化されます。 パラメーター化された行フィルターの詳細については、「 [パラメーター化された行フィルター](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」を参照してください。  
  
 次の 3 つの方法のいずれかで、パラメーター化されたフィルターを使用して、パブリケーションのスナップショットを作成できます。  
  
-   **各パーティションのスナップショットを事前に生成します。** このオプションを使用すると、スナップショットが生成されたときに制御できます。    
     スナップショットがスケジュールに従って更新されるように選択することもできます。 スナップショットの作成対象となったパーティションをサブスクライブする新しいサブスクライバーは、最新のスナップショットを受信します。   
-   サブスクライバーが初めて同期されたときに、**スナップショットの生成と適用を要求できるようにします。** このオプションを使用すると、新しいサブスクライバーは管理者の介入を必要としないで同期できます (スナップショットを生成するには[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがパブリッシャーで実行されている必要があります)。  
  
    > [!NOTE]  
    >  パブリケーション内の 1 つ以上のアーティクルにフィルターを適用して、各サブスクリプション固有の重複しないパーティションが得られる場合、マージ エージェントが実行されるたびにメタデータがクリーンアップされます。 これは、パーティション スナップショットの有効期間が短時間で切れてしまうことを意味します。 このオプションを使用する場合は、サブスクライバーに対してスナップショットの生成と配信を許可することを検討する必要があります。 フィルター オプションの詳細については、「 [パラメーター化された行フィルター](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」を参照してください。  
  
-   **スナップショット エージェントを使用して、手動で各サブスクライバーのスナップショットを生成します**。 サブスクライバーは、マージ エージェントが正しいスナップショットを取得および適用できるように、スナップショットの場所をマージ エージェントに提供する必要があります。  
  
    > [!NOTE]  
    >  このオプションは、旧バージョンとの互換性のためにサポートされており、FTP スナップショット共有を使用できません。  
  
 最も柔軟性の高い方法は、事前に生成され、サブスクライバーに要求されるスナップショット オプションの組み合わせを使用することです。スナップショットは、スケジュールに基づいて (通常はオフピーク時に) 事前生成および更新されますが、新しいパーティションを必要とするサブスクリプションが作成された場合は、サブスクライバーが独自のスナップショットを生成できます。  
  
 各店舗に在庫を配送する移動営業部署のある [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]について考えてみましょう。 各営業担当者は、各自のログインに基づいてサブスクリプションを受信し、各自が担当する店舗についてのデータを取得します。 管理者は、スナップショットを事前に生成し、毎週日曜日に更新するように選択しています。 場合によっては、新しいユーザーがシステムに追加され、スナップショットを使用できないパーティションのデータが必要になります。 管理者の選択により、サブスクライバーが開始するスナップショットで、スナップショットがまだ使用できないためにサブスクライバーがパブリケーションをサブスクライブできない状況を回避することもできます。 新しいサブスクライバーが初めて接続すると、指定されたパーティションに対してスナップショットが生成され、サブスクライバーで適用されます (スナップショットを生成できるようにするには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがパブリッシャーで実行されている必要があります)。  
  
 パラメーター化されたフィルターを使用してパブリケーションのスナップショットを作成するには、「 [パラメーター化されたフィルターを使用したパブリケーションのスナップショットの作成](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」を参照してください。  
  
## <a name="security-settings-for-the-snapshot-agent"></a>スナップショット エージェントに対するセキュリティの設定  
 スナップショット エージェントは各パーティションのスナップショットを作成します。 事前に生成されるスナップショットとサブスクライバーによって要求されるスナップショットの場合、エージェントが実行され、パブリケーションのスナップショット エージェント ジョブ作成時に指定された資格情報に基づいて接続が作成されます (このジョブは、パブリケーションの新規作成ウィザードまたは **sp_addpublication_snapshot**によって作成されます)。 資格情報を変更するには、 **sp_changedynamicsnapshot_job**を使用します。 詳しくは、「[sp_changedynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql.md)」をご覧ください。  

  
##  <a name="Recommendations"></a> 推奨事項  
  
-   パラメーター化されたフィルターを使用してマージ パブリケーションのスナップショットを生成する際には、最初にすべてのパブリッシュ済みデータとサブスクリプションのサブスクライバー メタデータを含む標準 (スキーマ) スナップショットを生成する必要があります。 詳しくは、「 [初期スナップショットの作成および適用](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」をご覧ください。 スキーマ スナップショットを作成した後で、パブリッシュ済みデータのサブスクライバー固有のパーティションを含むスナップショットを作成できます。  
  
-   パブリケーション内の 1 つ以上のアーティクルにフィルターを適用して、各サブスクリプション固有の重複しないパーティションが得られる場合、マージ エージェントが実行されるたびにメタデータがクリーンアップされます。 これは、パーティション スナップショットの有効期間が短時間で切れてしまうことを意味します。 このオプションを使用する場合は、サブスクライバーに対してスナップショットの生成と配信を許可することを検討する必要があります。 
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[データ パーティション]** ページでパーティションのスナップショットを作成します。 このダイアログ ボックスへのアクセス方法の詳細については、「[パブリケーション プロパティの表示および変更](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」を参照してください。 サブスクライバーには、スナップショットの生成と配信の開始や、スナップショットの生成を許可できます。  
  
 1 つ以上のパーティションに対してスナップショットを生成する前に、以下の作業を行う必要があります。  
  
1.  新規パブリーケーション ウィザードを使用してマージ パブリケーションを作成し、ウィザードの **[フィルターの追加]** ページで 1 つ以上のパラメーター化された行フィルターを指定します。 詳しくは、「 [マージ アーティクルのパラメーター化された行フィルターの定義および変更](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)」をご覧ください。  
  
2.  パブリケーションのスキーマ スナップショットを生成します。 既定では、新規パブリケーション ウィザードが完了すると、スキーマ スナップショットが生成されます。また、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]からスキーマ スナップショットを生成することもできます。  

#### <a name="to-generate-a-schema-snapshot"></a>スキーマ スナップショットを生成するには  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[パブリケーション]** フォルダーを展開します。  
  
3.  スナップショットを作成するパブリケーションを右クリックして、 **[スナップショット エージェントの状態の表示]** をクリックします。  
  
4.  **[スナップショット エージェントの状態の表示 - \<Publication>]** ダイアログ ボックスで **[開始]** をクリックします。  
  
     スナップショット エージェントによるスナップショットの生成が完了すると、"[100%] 17 個のアーティクルのスナップショットが生成されました。" などのメッセージが表示されます。  
  
#### <a name="to-allow-subscribers-to-initiate-snapshot-generation-and-delivery"></a>サブスクライバーにスナップショットの生成と配信を許可するには  
  
1.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[データ パーティション]** ページで、 **[新規サブスクライバーで同期を行うとき、パーティションを自動的に定義し、必要に応じてスナップショットを生成する]** を選択します。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### <a name="to-generate-and-refresh-snapshots"></a>スナップショットの生成と更新を行うには  
  
1.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[データ パーティション]** ページで **[追加]** をクリックします。  
  
2.  スナップショットを作成するパーティションに関連付けられた **HOST_NAME()** と **SUSER_SNAME()** に値を入力します。  
  
3.  オプションでスナップショットの更新スケジュールを指定します。  
  
    1.  **[以下のスケジュールでこのパーティションのスナップショット エージェントを実行する]** を選択します。  
  
    2.  スナップショットの既定の更新スケジュールをそのまま使用するか、または **[変更]** をクリックして別のスケジュールを指定します。  
  
4.  **[OK]** をクリックして、 **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスに戻ります。  
  
5.  プロパティ グリッドでパーティションを選択し、 **[今すぐ選択したスナップショットを生成する]** をクリックします。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 ストアド プロシージャとスナップショット エージェントを使用して、次を実行できます。  
  
-   サブスクライバーが初めて同期されたときに、スナップショットの生成と適用を要求できるようにします。  
  
-   各パーティションのスナップショットを事前に生成します。  
  
-   各サブスクライバーのスナップショットを手動で生成できます。  
  
    > [!IMPORTANT]  
    >  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
#### <a name="to-create-a-publication-that-allows-subscribers-to-initiate-snapshot-generation-and-delivery"></a>サブスクライバーでスナップショットの生成と配信を開始するためのパブリケーションを作成するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、[sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) を実行します。 次のパラメーターを指定します。  
  
    -   **\@publication** のパブリケーションの名前。  
  
    -   **\@allow_subscriber_initiated_snapshot** に、**true** を指定します。これにより、サブスクライバーがスナップショット プロセスを開始できるようになります。  
  
    -   (省略可能) **\@max_concurrent_dynamic_snapshots** に、同時に実行できる動的スナップショット プロセスの数を指定します。 最大限の数のプロセスが実行しているときに、サブスクライバーがスナップショットを生成しようとすると、そのプロセスはキューに格納されます。 既定では、同時プロセスの数に限度はありません。  
  
2.  パブリッシャーで [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) を実行します。 手順 1. で使用したパブリケーション名を **\@publication** に指定し、[レプリケーション スナップショット エージェント](../../relational-databases/replication/agents/replication-snapshot-agent.md)を実行するときに使用される [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 資格情報を **\@job_login** と **\@password** に指定します。 エージェントがパブリッシャーに接続する際に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合は、さらに **\@publisher_security_mode** に **0** を指定し、 **\@publisher_login** と **\@publisher_password** に [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン情報を指定する必要があります。 これにより、パブリケーション用のスナップショット エージェント ジョブが作成されます。 初期スナップショットの作成と、スナップショット エージェントのカスタム スケジュールの定義については、「 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」を参照してください。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
3.  [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) を実行して、パブリケーションにアーティクルを追加します。 このストアド プロシージャは、パブリケーション内の各アーティクルについて 1 回ずつ実行する必要があります。 パラメーター化されたフィルターを使用する場合には、 **\@subset_filterclause** パラメーターを使用して 1 つ以上のアーティクルにパラメーター化された行フィルターを指定する必要があります。 詳しくは、「 [マージ アーティクルのパラメーター化された行フィルターの定義および変更](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)」をご覧ください。  
  
4.  他のアーティクルがパラメーター化された行フィルターに基づいてフィルター選択される場合、[sp_addmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) を実行して、アーティクル間の結合レコード リレーションシップまたは論理レコード リレーションシップを定義します。 このストアド プロシージャは、定義する各リレーションシップにつき 1 回ずつ実行する必要があります。 詳しくは、「 [マージ アーティクル間の結合フィルターの定義および変更](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)」をご覧ください。  
  
5.  マージ エージェントでサブスクライバーを初期化するためにスナップショットが必要な場合、要求側のサブスクリプションのパーティションのスナップショットが自動的に生成されます。  
  
#### <a name="to-create-a-publication-and-pre-generate-or-automatically-refresh-snapshots"></a>パブリケーションを作成し、スナップショットを事前に生成、または自動更新するには  
  
1.  [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) を実行して、パブリケーションを作成します。 詳しくは、「 [パブリケーションを作成](../../relational-databases/replication/publish/create-a-publication.md)」をご覧ください。  
  
2.  パブリッシャーで [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) を実行します。 手順 1. で使用したパブリケーション名を **\@publication** に指定し、スナップショット エージェントを実行するときに使用される Windows 資格情報を **\@job_login** と **\@password** に指定します。 エージェントがパブリッシャーに接続する際に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合、さらに **\@publisher_security_mode** に **0** を指定し、 **\@publisher_login** と **\@publisher_password** に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン情報を指定する必要があります。 これにより、パブリケーション用のスナップショット エージェント ジョブが作成されます。 初期スナップショットの作成と、スナップショット エージェントのカスタム スケジュールの定義については、「 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」を参照してください。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
3.  [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) を実行して、パブリケーションにアーティクルを追加します。 このストアド プロシージャは、パブリケーション内の各アーティクルについて 1 回ずつ実行する必要があります。 パラメーター化されたフィルターを使用する場合には、 **\@subset_filterclause** パラメーターを使用して 1 つのアーティクルにパラメーター化された行フィルターを指定する必要があります。 詳しくは、「 [マージ アーティクルのパラメーター化された行フィルターの定義および変更](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)」をご覧ください。  
  
4.  他のアーティクルがパラメーター化された行フィルターに基づいてフィルター選択される場合、[sp_addmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) を実行して、アーティクル間の結合レコード リレーションシップまたは論理レコード リレーションシップを定義します。 このストアド プロシージャは、定義する各リレーションシップにつき 1 回ずつ実行する必要があります。 詳しくは、「 [マージ アーティクル間の結合フィルターの定義および変更](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)」をご覧ください。  
  
5.  パブリケーション データベースのパブリッシャーで [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md) を実行し、手順 1 の **\@publication** の値を指定します。 結果セットの **snapshot_jobid** の値を確認します。  
  
6.  手順 5. で得られた **snapshot_jobid** の値を、 **uniqueidentifier**に変換します。  
  
7.  パブリッシャーの **msdb** データベースに対して、[sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md) を実行します。 **\@job_id** には、手順 6 で得られた変換済みの値を指定します。  
  
8.  パブリッシャー側のパブリケーション データベースに対して、[sp_addmergepartition &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md) を実行します。 手順 1. のパブリケーション名を **\@publication** に指定します。パーティションの定義に使用する値には、フィルター句で [SUSER_SNAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sname-transact-sql.md) が使用されている場合は **\@suser_sname**、フィルター句で [HOST_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/host-name-transact-sql.md) が使用されている場合は **\@host_name** を指定します。  
  
9. パブリッシャー側のパブリケーション データベースに対して、[sp_adddynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md) を実行します。 手順 1 のパブリケーション名を **\@publication** に指定します。手順 8. で使用した **\@suser_sname** または **\@host_name** の値を指定し、ジョブのスケジュールを指定します。 これにより、指定されたパーティションにパラメーター化スナップショットを生成するジョブが作成されます。 詳細については、「 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)」を参照してください。  
  
    > [!NOTE]  
    >  このジョブは、手順 2. で定義した初期スナップショット ジョブと同じ Windows アカウントを使用して実行されます。 このパラメーター化されたスナップショット ジョブおよび関連するデータ パーティションを削除するには、[sp_dropdynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md) を実行します。  
  
10. パブリッシャー側のパブリケーション データベースに対して、[sp_helpmergepartition &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md) を実行し、手順 1 の **\@publication** の値および手順 8 の **\@suser_sname** または **\@host_name** の値を指定します。 結果セットの **dynamic_snapshot_jobid** の値を確認します。  
  
11. ディストリビューターの **msdb** データベースに対して、[sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md) を実行します。 **\@job_id** には、手順 9 で得られた値を指定します。 これにより、そのパーティションに対してパラメーター化されたスナップショット ジョブが開始されます。  
  
12. 手順 8. ～ 11. を繰り返し実行して、各サブスクリプションについてパーティション スナップショットを生成します。  
  
#### <a name="to-create-a-publication-and-manually-create-snapshots-for-each-partition"></a>パブリケーションを作成し、各パーティションのスナップショットを手動で作成するには  
  
1.  [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) を実行して、パブリケーションを作成します。 詳しくは、「 [パブリケーションを作成](../../relational-databases/replication/publish/create-a-publication.md)」をご覧ください。  
  
2.  パブリッシャーで [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) を実行します。 手順 1. で使用したパブリケーション名を **\@publication** に指定し、スナップショット エージェントを実行するときに使用される Windows 資格情報を **\@job_login** と **\@password** に指定します。 エージェントがパブリッシャーに接続する際に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合、さらに **\@publisher_security_mode** に **0** を指定し、 **\@publisher_login** と **\@publisher_password** に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン情報を指定する必要があります。 これにより、パブリケーション用のスナップショット エージェント ジョブが作成されます。 初期スナップショットの作成と、スナップショット エージェントのカスタム スケジュールの定義については、「 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」を参照してください。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
3.  [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) を実行して、パブリケーションにアーティクルを追加します。 このストアド プロシージャは、パブリケーション内の各アーティクルについて 1 回ずつ実行する必要があります。 パラメーター化されたフィルターを使用する場合には、 **\@subset_filterclause** パラメーターを使用して 1 つ以上のアーティクルにパラメーター化された行フィルターを指定する必要があります。 詳しくは、「 [マージ アーティクルのパラメーター化された行フィルターの定義および変更](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)」をご覧ください。  
  
4.  他のアーティクルがパラメーター化された行フィルターに基づいてフィルター選択される場合、[sp_addmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) を実行して、アーティクル間の結合レコード リレーションシップまたは論理レコード リレーションシップを定義します。 このストアド プロシージャは、定義する各リレーションシップにつき 1 回ずつ実行する必要があります。 詳しくは、「 [マージ アーティクル間の結合フィルターの定義および変更](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)」をご覧ください。  
  
5.  スナップショット ジョブを開始するか、コマンド プロンプトからレプリケーション スナップショット エージェントを実行して、標準のスナップショット スキーマおよびその他のファイルを生成します。 詳しくは、「 [初期スナップショットの作成および適用](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」をご覧ください。  
  
6.  再びコマンド プロンプトからレプリケーション スナップショット エージェントを実行し、一括コピー (.bcp) ファイルを生成します。パーティション スナップショットの場所を **-DynamicSnapshotLocation** に指定し、次の 2 つのプロパティを指定して、パーティションを定義します。  
  
    -   **-DynamicFilterHostName** - [HOST_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/host-name-transact-sql.md) が使用される場合の値。  
  
    -   **-DynamicFilterLogin** - [SUSER_SNAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sname-transact-sql.md) が使用される場合の値。  
  
7.  手順 6. を繰り返し実行して、各サブスクリプションについてパーティション スナップショットを生成します。  
  
8.  サブスクリプションごとにマージ エージェントを実行して、初期のパーティション スナップショットをサブスクライバーに適用します。次のプロパティを指定します。  
  
    -   **-Hostname** - HOST_NAME の実際の値がオーバーライドされている場合にパーティションの定義に使用する値。  
  
    -   **-DynamicSnapshotLocation** - このパーティションの動的スナップショットの場所。  
  
> [!NOTE]  
>  レプリケーション エージェントのプログラミングの詳細については、「[Replication Agent Executables Concepts](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)」(レプリケーション エージェントの実行可能ファイルの概念) を参照してください。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、サブスクライバーによってスナップショット生成プロセスが開始される場合に、パラメーター化されたフィルターを使用してマージ パブリケーションを作成します。 **\@job_login** と **\@job_password** に指定する値は、スクリプト変数を使用して渡されます。  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_1.sql)]  
  
 次の例では、パラメーター化されたフィルターを使用してパブリケーションを作成します。各サブスクライバーでは [sp_addmergepartition](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md) を実行することでパーティションを定義し、パーティション情報を渡して [sp_adddynamicsnapshot_job](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md) を実行することで、フィルター選択したスナップショット ジョブを作成します。 **\@job_login** と **\@job_password** に指定する値は、スクリプト変数を使用して渡されます。  
  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_2.sql)]  
  
 次の例では、各サブスクライバーでパーティション情報を入力してデータ パーティションとフィルター選択したスナップショット ジョブを作成する必要がある場合に、パラメーター化されたフィルターを使用してパブリケーションを作成します。 レプリケーション エージェントを手動で実行する場合、サブスクライバーではコマンド ライン パラメーターを使用してパーティション情報を入力します。 この例では、パブリケーションに対するサブスクリプションも作成されることを想定しています。  
  
 [!code-sql[HowTo#sp_MergeDynamicPubPartitionManual](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_3.sql)]  
  
```  
  
REM Line breaks are added to improve readability.   
REM In a batch file, commands must be made in a single line.  
REM Run the Snapshot agent from the command line to generate the standard snapshot   
REM schema and other files.   
SET DistPub=%computername%  
SET PubDB=AdventureWorks2012   
SET PubName=AdvWorksSalesPersonMerge  
  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %PubName%    
-Publisher %DistPub% -Distributor  %DistPub%  -PublisherDB %PubDB%  -ReplicationType 2    
-OutputVerboseLevel 1  -DistributorSecurityMode 1  
  
PAUSE  
  
```  
  
```  
  
REM Run the Snapshot agent from the command line, this time to generate   
REM the bulk copy (.bcp) data for each Subscriber partition.    
SET DistPub=%computername%  
SET PubDB=AdventureWorks2012   
SET PubName=AdvWorksSalesPersonMerge  
SET SnapshotDir=\\%DistPub%\repldata\unc\fernando  
  
MD %SnapshotDir%  
  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %PubName%    
-Publisher %DistPub%  -Distributor  %DistPub%  -PublisherDB %PubDB%  -ReplicationType 2    
-OutputVerboseLevel 1  -DistributorSecurityMode 1  -DynamicFilterHostName "adventure-works\Fernando"    
-DynamicSnapshotLocation %SnapshotDir%  
  
PAUSE  
  
```  
  
```  
  
REM Run the Merge Agent for each subscription to apply the partitioned   
REM snapshot for each Subscriber.    
SET Publisher = %computername%  
SET Subscriber = %computername%  
SET PubDB = AdventureWorks2012   
SET SubDB = AdventureWorks2012Replica   
SET PubName = AdvWorksSalesPersonMerge   
SET SnapshotDir=\\%DistPub%\repldata\unc\fernando  
  
"C:\Program Files\Microsoft SQL Server\120\COM\REPLMERG.EXE" -Publisher  %Publisher%    
-Subscriber  %Subscriber%  -Distributor %Publisher%  -PublisherDB %PubDB%    
-SubscriberDB %SubDB% -Publication %PubName%  -PublisherSecurityMode 1  -OutputVerboseLevel 3    
-Output -SubscriberSecurityMode 1  -SubscriptionType 3 -DistributorSecurityMode 1    
-Hostname "adventure-works\Fernando"  -DynamicSnapshotLocation %SnapshotDir%  
  
PAUSE  
  
```  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 パーティション スナップショットは、プログラムからレプリケーション管理オブジェクト (RMO) を使用して生成できます。その方法を次に示します。  
  
-   サブスクライバーが初めて同期されたときに、スナップショットの生成と適用を要求できるようにします。  
  
-   各パーティションのスナップショットを事前に生成します。  
  
-   スナップショット エージェントを実行してサブスクライバーごとにスナップショットを手動で生成できます。  
  
> [!NOTE]  
>  アーティクルをフィルター選択して、サブスクリプションごとに一意の重複しないパーティションを取得する場合 (マージ アーティクルの作成時、 F:Microsoft.SqlServer.Replication.PartitionOptions.NonOverlappingSingleSubscription の値に P:Microsoft.SqlServer.Replication.MergeArticle.PartitionOption を指定した場合)、マージ エージェントの実行時に常にメタデータがクリーンアップされます。 これは、パーティション スナップショットの有効期間が短時間で切れてしまうことを意味します。 このオプションを使用する場合は、サブスクライバーからスナップショットの生成を要求できるようにする必要があります。 詳細については、「 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」の「適切なフィルター選択オプションの使用」を参照してください。  
  
> [!IMPORTANT]  
>  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 資格情報を保存する必要がある場合は、 [Windows .NET&#xA0;Framework に用意されている](https://go.microsoft.com/fwlink/?LinkId=34733) 暗号化サービス [!INCLUDE[msCoName](../../includes/msconame-md.md)] を使用します。  
  
#### <a name="to-create-a-publication-that-allows-subscribers-to-initiate-snapshot-generation-and-delivery"></a>サブスクライバーでスナップショットの生成と配信を開始するためのパブリケーションを作成するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  パブリケーション データベースに <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> クラスのインスタンスを作成するには、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに手順 1. の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> インスタンスを設定し、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出します。 If <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> から **false**が返された場合は、データベースが存在していることを確認してください。  
  
3.  If <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> プロパティが **false**の場合は、このプロパティに **\@allow_subscriber_initiated_snapshot** を設定して、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>」をご覧ください。  
  
4.  <xref:Microsoft.SqlServer.Replication.MergePublication> クラスのインスタンスを作成し、このオブジェクトに次のプロパティを設定します。  
  
    -   手順 1. の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>に指定します。  
  
    -   パブリッシュするデータベースの名前を <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>に指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>にパブリケーションの名前を指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergePublication.MaxConcurrentDynamicSnapshots%2A>に、実行する動的スナップショット ジョブの最大数を指定します。 サブスクライバーがスナップショットを要求するタイミングは不定です。そのため、同時に複数のサブスクライバーがパーティション スナップショットを要求した場合に、このプロパティを使って、同時に実行できるスナップショット エージェント ジョブの数を制限します。 実行中のジョブが最大数に達した場合は、パーティション スナップショットに対するそれ以降の要求は、実行されているいずれかのジョブが完了するまでキューに格納されます。  
  
    -   ビットごとの論理和演算 (Visual C# の場合は **|** 、Visual Basic の場合は **Or** ) を使用して、 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowSubscriberInitiatedSnapshot> 値を <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A>」をご覧ください。  
  
    -   <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> の <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> フィールドに、スナップショット エージェント ジョブの実行に使用する [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントの資格情報を指定します。  
  
        > [!NOTE]  
        >  パブリケーションが固定サーバー ロール <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> のメンバーによって作成された場合、 **P:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity** を設定することをお勧めします。 詳細については、「 [レプリケーション エージェント セキュリティ モデル](../../relational-databases/replication/security/replication-agent-security-model.md)」を参照してください。  
  
5.  <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> メソッドを呼び出して、パブリケーションを作成します。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>を含むすべてのプロパティに指定された値がディストリビューターにプレーンテキストとして送信されます。 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> メソッドを呼び出す前に、パブリッシャーとリモート ディストリビューター間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
6.  <xref:Microsoft.SqlServer.Replication.MergeArticle> プロパティを使用して、アーティクルをパブリケーションに追加します。 パラメーター化されたフィルターを定義する <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> プロパティを少なくとも 1 つのアーティクルについて指定します。 (省略可) アーティクル間の結合フィルターを定義する <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> オブジェクトを作成します。 詳しくは、「 [アーティクルを定義](../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
7.  <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> の値が **false** の場合は、<xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> を呼び出して、このパブリケーション用の初期スナップショット エージェント ジョブを作成します。  
  
8.  手順 4. で作成した <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> オブジェクトの <xref:Microsoft.SqlServer.Replication.MergePublication> メソッドを呼び出します。 これにより、初期スナップショットを生成するエージェント ジョブが開始されます。 初期スナップショットの作成と、スナップショット エージェントのカスタム スケジュールの定義については、「 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」を参照してください。  
  
9. (省略可) 初期スナップショットが使用できる状態にあるかを調べるには、 **\@allow_subscriber_initiated_snapshot** プロパティの値が <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> であることを確認します。  
  
10. サブスクライバーのマージ エージェントの初回接続時に、パーティション スナップショットが自動的に生成されます。  
  
#### <a name="to-create-a-publication-and-pregenerate-or-automatically-refresh-snapshots"></a>パブリケーションを作成し、スナップショットを事前に生成したり、自動的に更新するには  
  
1.  <xref:Microsoft.SqlServer.Replication.MergePublication> クラスのインスタンスを使用して、マージ パブリケーションを定義します。 詳しくは、「 [パブリケーションを作成](../../relational-databases/replication/publish/create-a-publication.md)」をご覧ください。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeArticle> プロパティを使用して、アーティクルをパブリケーションに追加します。 パラメーター化されたフィルターを定義する <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> プロパティを少なくとも 1 つのアーティクルについて指定し、さらに、必要に応じて、アーティクル間の結合フィルターを定義する <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> オブジェクトを作成します。 詳しくは、「 [アーティクルを定義](../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
3.  <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> の値が **false** の場合は、<xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> を呼び出して、このパブリケーション用のスナップショット エージェント ジョブを作成します。  
  
4.  手順 1. で作成した <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> オブジェクトの <xref:Microsoft.SqlServer.Replication.MergePublication> メソッドを呼び出します。 このメソッドにより、初期スナップショットを生成するエージェント ジョブが開始されます。 初期スナップショットを生成する方法、およびスナップショット エージェントのカスタム スケジュールを定義する方法については、「 [初期スナップショットの作成および適用](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」を参照してください。  
  
5.  <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> プロパティの値が **true** であることを確認し、初期スナップショットが使用できる状態にあるかを調べます。  
  
6.  <xref:Microsoft.SqlServer.Replication.MergePartition> クラスのインスタンスを作成し、次のいずれかまたは両方のプロパティを使って、サブスクライバー用のパラメーター化されたフィルター条件を設定します。  
  
    -   サブスクライバーのパーティションが [SUSER_SNAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sname-transact-sql.md) の結果によって定義される場合は、<xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterLogin%2A> を使用します。  
  
    -   サブスクライバーのパーティションが [HOST_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/host-name-transact-sql.md) またはこの関数のオーバーロードの結果によって定義される場合は、<xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterHostName%2A> を使用します。  
  
7.  <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> クラスのインスタンスを作成し、手順 6. と同じプロパティを設定します。  
  
8.  <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule> クラスを使用し、サブスクライバーのパーティションに対してフィルター選択されたスナップショットを生成するスケジュールを定義します。  
  
9. 手順 1. で作成した <xref:Microsoft.SqlServer.Replication.MergePublication> のインスタンスを使用して、 <xref:Microsoft.SqlServer.Replication.MergePublication.AddMergePartition%2A>を呼び出します。 手順 6. の <xref:Microsoft.SqlServer.Replication.MergePartition> オブジェクトを渡します。  
  
10. 手順 1. で作成した <xref:Microsoft.SqlServer.Replication.MergePublication> のインスタンスを使用して、 <xref:Microsoft.SqlServer.Replication.MergePublication.AddMergeDynamicSnapshotJob%2A> メソッドを呼び出します。 このとき、手順 7. の <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> オブジェクトと、手順 8. の <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule> オブジェクトを引数として指定します。  
  
11. <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergeDynamicSnapshotJobs%2A>を呼び出し、返された配列から <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> オブジェクトを検索し、パーティション スナップショットを要求するジョブが新たに追加されていないか確認します。  
  
12. このジョブの <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob.Name%2A> プロパティを取得します。  
  
13. <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、ディストリビューターへの接続を作成します。  
  
14. SQL Server 管理オブジェクト (SMO) の <xref:Microsoft.SqlServer.Management.Smo.Server> クラスのインスタンスを作成し、手順 13. の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトを渡します。  
  
15. <xref:Microsoft.SqlServer.Management.Smo.Agent.Job> クラスのインスタンスを作成し、手順 14. の <xref:Microsoft.SqlServer.Management.Smo.Server.JobServer%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Server> プロパティと、手順 12. のジョブ名を渡します。  
  
16. <xref:Microsoft.SqlServer.Management.Smo.Agent.Job.Start%2A> メソッドを呼び出して、パーティション スナップショットを要求するジョブを開始します。  
  
17. 手順 6. から手順 16. を各サブスクライバーについて繰り返します。  
  
#### <a name="to-create-a-publication-and-manually-create-snapshots-for-each-partition"></a>パブリケーションを作成し、各パーティションのスナップショットを手動で作成するには  
  
1.  <xref:Microsoft.SqlServer.Replication.MergePublication> クラスのインスタンスを使用して、マージ パブリケーションを定義します。 詳しくは、「 [パブリケーションを作成](../../relational-databases/replication/publish/create-a-publication.md)」をご覧ください。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeArticle> プロパティを使用して、パブリケーションにアーティクルを追加します。パラメーター化されたフィルターを定義する <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> プロパティを少なくとも 1 つのアーティクルについて指定し、さらに、必要に応じて、アーティクル間の結合フィルターを定義する <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> オブジェクトを作成します。 詳しくは、「 [アーティクルを定義](../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
3.  初期スナップショットを生成します。 詳しくは、「 [初期スナップショットの作成および適用](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」をご覧ください。  
  
4.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> クラスのインスタンスを作成し、次の必須プロパティを設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - パブリッシャーの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - パブリケーション データベースの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - パブリケーションの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - ディストリビューターの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> - 値 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> (Windows 統合認証を使用する場合) または値 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> (SQL Server 認証を使用する場合)  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> - 値 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> (Windows 統合認証を使用する場合) または値 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> (SQL Server 認証を使用する場合)  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> に <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>を設定します。  
  
6.  次に示したプロパティを少なくとも 1 つ設定し、パーティションのパラメーターを定義します。  
  
    -   サブスクライバーのパーティションが [SUSER_SNAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sname-transact-sql.md) の結果によって定義される場合は、<xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DynamicFilterLogin%2A> を使用します。  
  
    -   サブスクライバーのパーティションが [HOST_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/host-name-transact-sql.md) またはこの関数のオーバーロードの結果によって定義される場合は、<xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DynamicFilterHostName%2A> を使用します。  
  
7.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> メソッドを呼び出します。  
  
8.  手順 4. から手順 7. を各サブスクライバーについて繰り返します。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 次の例では、サブスクライバーがスナップショット生成を要求できるマージ パブリケーションを作成します。  
  
 [!code-cs[HowTo#rmo_CreateMergePub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
 次の例では、手動でサブスクライバーのパーティションを作成し、さらに、パラメーター化された行フィルターを使って、マージ パブリケーションのフィルター選択されたスナップショットを作成します。  
  
 [!code-cs[HowTo#rmo_CreateMergePartition](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepartition)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePartition](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepartition)]  
  
 次の例では、手動でスナップショット エージェントを起動し、パラメーター化された行フィルターを使って、マージ パブリケーションのサブスクライバー用にフィルター選択されたデータ スナップショットを生成します。  
  
 [!code-cs[HowTo#rmo_GenerateFilteredSnapshot](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatefilteredsnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateFilteredSnapshot](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatefilteredsnapshot)]  
  
## <a name="see-also"></a>参照  
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Replication System Stored Procedures Concepts](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [レプリケーション セキュリティの推奨事項](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
