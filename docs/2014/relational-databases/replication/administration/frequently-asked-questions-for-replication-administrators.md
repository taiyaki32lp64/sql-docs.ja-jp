---
title: レプリケーションの管理者に関してよく寄せられる質問 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- administering replication, frequently asked questions
- replication [SQL Server], administering
ms.assetid: 5a9e4ddf-3cb1-4baf-94d6-b80acca24f64
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce7e9249ec7ba97fdd159a743be30036847882b3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63207070"
---
# <a name="frequently-asked-questions-for-replication-administrators"></a>レプリケーションの管理者に関してよく寄せられる質問
  ここでは、レプリケートされたデータベースの管理者が行うさまざまな作業についての指針となるような質問と回答を掲載します。  
  
## <a name="configuring-replication"></a>レプリケーションの構成  
  
### <a name="does-activity-need-to-be-stopped-on-a-database-when-it-is-published"></a>データベースをパブリッシュするときに、データベースに対する操作を停止する必要がありますか。  
 No. パブリケーションの作成中でもデータベースの操作を継続することができます。 ただし、スナップショットの生成には大量のリソースが必要な点に注意してください。そのため、スナップショットはデータベースでの操作が少ない時間帯に生成することをお勧めします (既定では、パブリケーションの新規作成ウィザードを終了するとスナップショットが生成されます)。  
  
### <a name="are-tables-locked-during-snapshot-generation"></a>テーブルはスナップショット生成中にロックされますか。  
 ロックが設定される時間の長さは、使用するレプリケーションの種類によって以下のように異なります。  
  
-   マージ パブリケーションの場合、スナップショット エージェントはロックを設定しません。  
  
-   トランザクション パブリケーションの場合、既定では、スナップショット エージェントによりスナップショット生成の初期フェーズの間だけロックが設定されます。  
  
-   スナップショット パブリケーションの場合、スナップショット エージェントがスナップショット生成処理の間中、ロックを設定します。  
  
 ロックが設定されると他のユーザーがテーブルを更新できなくなるため、特にスナップショット パブリケーションの場合、データベースに対する操作が少ない時間帯にスナップショット エージェントを起動するようにスケジュールを設定することをお勧めします。  
  
### <a name="when-is-a-subscription-available-when-can-the-subscription-database-be-used"></a>サブスクリプションはいつ利用可能になりますか。また、サブスクリプション データベースはいつ利用可能になりますか。  
 サブスクリプションは、スナップショットがサブスクリプション データベースに適用された後で利用可能になります。 それ以前にもサブスクリプション データベースにアクセスできますが、スナップショットの適用が完了するまではデータベースを使用しないでください。 スナップショットの生成と適用の状態を確認するには、レプリケーション モニターを使用します。  
  
-   スナップショットはスナップショット エージェントによって生成されます。 パブリケーションのスナップショットの生成状態は、レプリケーション モニターの **[エージェント]** タブで確認します。 詳細については、「[レプリケーション モニターを使用して情報を表示し、タスクを実行する](../monitor/view-information-and-perform-tasks-replication-monitor.md)」を参照してください。  
  
-   スナップショットはディストリビューション エージェントまたはマージ エージェントによって適用されます。 スナップショットの適用状態は、レプリケーション モニターの **[ディストリビューション エージェント]** ページまたは **[マージ エージェント]** ページで確認します。 
  
### <a name="what-happens-if-the-snapshot-agent-has-not-completed-when-the-distribution-or-merge-agent-starts"></a>ディストリビューション エージェントまたはマージ エージェントの開始時にスナップショット エージェントが完了していなかったらどうなりますか。  
 ディストリビューション エージェントまたはマージ エージェントがスナップショット エージェントと同時に実行されてもエラーになることはありません。 ただし、以下の点に注意してください。  
  
-   ディストリビューション エージェントまたはマージ エージェントが連続して実行されるように構成されている場合は、スナップショット エージェントが終了した後でスナップショットが自動的に適用されます。  
  
-   ディストリビューション エージェントまたはマージ エージェントが、スケジュールまたは要求時に実行されるように構成されており、エージェント起動時には利用可能なスナップショットがなかった場合には、エージェントはスナップショットが利用できないことを示すメッセージを表示して終了します。 スナップショットを適用するためには、スナップショット エージェントが完了した後でエージェントを再度実行する必要があります。 エージェントの実行については、「[Synchronize a Push Subscription](../synchronize-a-push-subscription.md)」 (プッシュ サブスクリプションの同期)、「[Synchronize a Pull Subscription](../synchronize-a-pull-subscription.md)」 (プル サブスクリプションの同期)、「[Replication Agent Executables Concepts](../concepts/replication-agent-executables-concepts.md)」 (レプリケーション エージェント実行可能ファイルの概念) を参照してください。  
  
### <a name="should-i-script-my-replication-configuration"></a>レプリケーションの構成をスクリプト化する必要がありますか。  
 可能。 レプリケーション構成をスクリプト化するのは、レプリケーション トポロジのディザスター リカバリー計画の重要な部分です。 スクリプト作成の詳細については、「 [Scripting Replication](../scripting-replication.md)」を参照してください。  
  
### <a name="what-recovery-model-is-required-on-a-replicated-database"></a>レプリケートされたデータベースでは、どの復旧モデルが必要ですか。  
 単純復旧モデル、一括ログ復旧モデル、完全復旧モデルのいずれの復旧モデルでも、レプリケーションは正常に機能します。 マージ レプリケーションでは、メタデータ テーブルに情報を格納することで変更が追跡されます。 トランザクション レプリケーションでは、トランザクション ログにマークを付けることにより変更が追跡されますが、復旧モデルによってこのマーク設定処理が影響を受けることはありません。  
  
### <a name="why-does-replication-add-a-column-to-replicated-tables-will-it-be-removed-if-the-table-isnt-published"></a>レプリケーションによって列が追加されるのはなぜですか。この列は、テーブルのパブリッシュをやめると削除されますか。  
 変更を追跡するため、マージ レプリケーションとキュー更新サブスクリプションを使用したトランザクション レプリケーションでは、パブリッシュされたすべてのテーブルのすべての行を一意に識別できる必要があります。 これには、以下を行う必要があります。  
  
-   マージ レプリケーションでは、列 **rowguid** がすべてのテーブルに追加されます。ただし、データ型が **uniqueidentifier** で **ROWGUIDCOL** プロパティが設定されている列が、テーブルに既にある場合を除きます (このような列がある場合は、その列が使用されます)。 テーブルがパブリケーションから削除されると、 **rowguid** 列も削除されます。既存の列を追跡に使用していた場合は、その列は削除されません。  
  
-   トランザクション パブリケーションがキュー更新サブスクリプションをサポートしている場合は、レプリケーションによってすべてのテーブルに **msrepl_tran_version** 列が追加されます。 テーブルがパブリケーションから削除されても、 **msrepl_tran_version** 列は削除されません。  
  
-   フィルターには、レプリケーションで行の識別に使用される `rowguidcol` を含めることはできません。 既定では、これはマージ レプリケーションのセットアップ時に追加される列であり、 **rowguid**という名前が付けられます。  
  
### <a name="how-do-i-manage-constraints-on-published-tables"></a>パブリッシュされたテーブルの制約はどのように管理すればよいですか。  
 パブリッシュされたテーブル上の制約については、注意すべき問題がいくつかあります。  
  
-   トランザクション レプリケーションでは、パブリッシュされた各テーブルで主キー制約が必要です。 マージ レプリケーションでは主キーは不要ですが、もし主キーがある場合には、レプリケートする必要があります。 スナップショット レプリケーションでは主キーは不要です。  
  
-   既定では、主キー制約、インデックス、および CHECK 制約がサブスクライバーにレプリケートされます。  
  
-   外部キー制約と CHECK 制約に対しては、NOT FOR REPLICATION オプションが既定で指定されます。この制約は、ユーザー操作に対しては適用されますが、エージェント操作には適用されません。  
  
 制約がレプリケートされるかどうかを制御するスキーマ オプションの設定の詳細については、「 [Specify Schema Options](../publish/specify-schema-options.md)」を参照してください。  
  
### <a name="how-do-i-manage-identity-columns"></a>ID 列はどのように管理すればよいですか。  
 サブスクライバーでの更新を含むレプリケーション トポロジでは、自動 ID 範囲管理が提供されます。 詳細については、「[Replicate Identity Columns](../publish/replicate-identity-columns.md)」 (ID 列のレプリケート) を参照してください。  
  
### <a name="can-the-same-objects-be-published-in-different-publications"></a>同じオブジェクトを複数のパブリケーションでパブリッシュすることはできますか。  
 はい。ただし、制限があります。 詳細については、「[Publish Data and Database Objects](../publish/publish-data-and-database-objects.md)」 (データとデータベース オブジェクトのパブリッシュ) の「Publishing Tables in More Than One Publication」 (複数のパブリケーションでのテーブルのパブリッシュ) を参照してください。  
  
### <a name="can-multiple-publications-use-the-same-distribution-database"></a>複数のパブリケーションで同じディストリビューション データベースを使用できますか。  
 可能。 同じディストリビューション データベースを使用するパブリケーションの数や種類に制限はありません。 指定されたパブリッシャーのすべてのパブリケーションで、同じディストリビューターとディストリビューション データベースを使用する必要があります。  
  
 複数のパブリケーションがある場合は、ディストリビューターで複数のディストリビューション データベースを構成することにより、各ディストリビューション データベースのデータ フローを、単一のパブリケーションから渡すことができます。 **[ディストリビューターのプロパティ]** ダイアログ ボックスまたは [sp_adddistributiondb &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql) を使用して、分散データベースを追加します。 このダイアログ ボックスへのアクセスの詳細については、「[View and Modify Distributor and Publisher Properties](../view-and-modify-distributor-and-publisher-properties.md)」 (ディストリビューターとパブリッシャーのプロパティの表示および変更) を参照してください。  
  
### <a name="how-do-i-find-information-on-the-distributor-and-publisher-such-as-which-objects-in-a-database-are-published"></a>データベース内のどのオブジェクトがパブリッシュされているかなどの、ディストリビューターとパブリッシャーについての情報は、どうすれば参照できますか。  
 この情報は、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]およびいくつかのレプリケーション ストアド プロシージャを使用して参照できます。 詳細については、「 [Distributor and Publisher Information Script](distributor-and-publisher-information-script.md)」を参照してください。  
  
### <a name="does-replication-encrypt-data"></a>レプリケーションではデータが暗号化されますか。  
 No. レプリケーションでは、データベースに格納されるデータやネットワーク経由で転送されるデータは暗号化されません。 詳細については、トピックの「暗号化」セクションを参照してください。 [SQL Server レプリケーションのセキュリティ](../security/view-and-modify-replication-security-settings.md)します。  
  
### <a name="how-do-i-replicate-data-over-the-internet"></a>インターネット経由でデータをレプリケートするにはどうすればよいですか。  
 インターネット経由のデータのレプリケーションでは、以下を使用します。  
  
-   仮想プライベート ネットワーク (VPN)。 詳細については、「[Publish Data over the Internet Using VPN](../publish-data-over-the-internet-using-vpn.md)」 (VPN を使用したインターネット経由のデータのパブリッシュ) を参照してください。  
  
-   マージ レプリケーション用の Web 同期オプション。 詳細については、「 [Web Synchronization for Merge Replication](../web-synchronization-for-merge-replication.md)」を参照してください。  
  
 すべての種類の [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーションは VPN 経由でデータをレプリケートできますが、マージ レプリケーションを使用している場合は Web 同期を検討してください。  
  
### <a name="does-replication-resume-if-a-connection-is-dropped"></a>接続が切断された場合にレプリケーションは再開されますか。  
 可能。 接続が切断された場合には、中断した時点からレプリケーション処理が再開されます。 不安定なネットワーク経由でマージ レプリケーションを使用している場合は、論理レコードの利用を検討してください。これにより、関連する変更が 1 つの単位として処理されるようになります。 詳細については、「[Group Changes to Related Rows with Logical Records](../merge/group-changes-to-related-rows-with-logical-records.md)」 (論理レコードによる関連行への変更のグループ化) を参照してください。  
  
### <a name="does-replication-work-over-low-bandwidth-connections-does-it-use-compression"></a>低帯域接続経由でもレプリケーションは機能しますか。 圧縮は行われますか。  
 はい。低帯域接続経由でもレプリケーションは機能します。 TCP/IP 経由の接続では、プロトコルによって提供される圧縮を利用しますが、それ以外の圧縮は行われません。 HTTPS 経由の Web 同期接続の場合は、プロトコルで提供される圧縮に加え、変更をレプリケートするために使用する XML ファイルの圧縮も使用されます。  
  
## <a name="logins-and-object-ownership"></a>ログインとオブジェクトの所有権  
  
### <a name="are-logins-and-passwords-replicated"></a>ログインとパスワードはレプリケートされますか。  
 No. ただし、DTS パッケージを作成することで、ログインとパスワードをパブリッシャーから 1 つ以上のサブスクライバーに転送することができます。  
  
### <a name="what-are-schemas-and-how-are-they-replicated"></a>スキーマとは何ですか。また、スキーマはどのようにレプリケートされますか。  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], *スキーマ* には次の 2 つの意味があります。  
  
-   CREATE TABLE ステートメントなどの、オブジェクトの定義。 既定では、レプリケートされるすべてのオブジェクトの定義がサブスクライバーにコピーされます。  
  
-   オブジェクトが作成される\<Database>.\<Schema>.\<Object> の名前空間です。 スキーマは、CREATE SCHEMA ステートメントで定義します。  
  
-   既定では、パブリケーションの新規作成ウィザードは、スキーマとオブジェクトの所有権に関して、以下のように動作します。  
  
-   互換性レベル 90 以上のマージ パブリケーションと、スナップショット パブリケーション、およびトランザクション パブリケーションのアーティクルの場合、既定では、サブスクライバーでのオブジェクト所有者は、パブリッシャーでの対応するオブジェクトの所有者と同じになります。 オブジェクトを所有するスキーマがサブスクライバーに存在しない場合は、スキーマが自動的に作成されます。  
  
-   互換性レベルが 90 未満のマージ パブリケーションのアーティクルの場合。既定では、所有者名は空白のままなり、サブスクライバーにオブジェクトを作成する際に **dbo** と指定されます。  
  
-   Oracle パブリケーションのアーティクルの場合。既定では、所有者名が **dbo**と指定されます。  
  
-   キャラクター モードのスナップショット ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のバージョンのサブスクライバーや [!INCLUDE[ssEW](../../../includes/ssew-md.md)] サブスクライバーで使用されます) を使用するパブリケーションのアーティクルの場合。既定では、所有者は空白のままになります。 既定の所有者は、サブスクライバーに接続しているディストリビューション エージェントまたはマージ エージェントで使用されるアカウントに関連付けられている所有者になります。  
  
 オブジェクトの所有者は、 **[アーティクルのプロパティ - \<***Article***>]** ダイアログ ボックスと、ストアド プロシージャの **sp_addarticle**、**sp_addmergearticle**、**sp_changearticle**、**sp_changemergearticle** で変更できます。 詳細については、「[View and Modify Publication Properties](../publish/view-and-modify-publication-properties.md)」 (パブリケーション プロパティの表示および変更)、「[Define an Article](../publish/define-an-article.md)」 (アーティクルの定義)、および「[View and Modify Article Properties](../publish/view-and-modify-article-properties.md)」 (アーティクルのプロパティの表示および変更) を参照してください。  
  
### <a name="how-can-grants-on-the-subscription-database-be-configured-to-match-grants-on-the-publication-database"></a>サブスクリプション データベースの権限をパブリケーション データベースの権限に一致させるには、どのように構成すればよいですか。  
 既定では、レプリケーションではサブスクリプション データベース上で GRANT ステートメントは実行されません。 サブスクリプション データベース上の権限をパブリケーション データベース上の権限に一致させる場合は、次のいずれかの方法を使用します。  
  
-   サブスクリプション データベース上で GRANT ステートメントを直接実行します。  
  
-   ポストスナップショット スクリプトを使用してステートメントを実行します。 詳細については、「[スナップショットが適用される前および後のスクリプトの実行](../snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)」を参照してください。  
  
-   ストアド プロシージャ [sp_addscriptexec](/sql/relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql) を使用してステートメントを実行します。  
  
### <a name="what-happens-to-permissions-granted-in-a-subscription-database-if-a-subscription-is-reinitialized"></a>サブスクリプションを再初期化すると、サブスクリプション データベースに付与された権限はどうなりますか。  
 既定では、サブスクリプションを再初期化すると、サブスクライバーのオブジェクトは削除され、その後、再作成されます。それらのオブジェクトに対して付与された権限は削除されます。 これに対処するには、2 つの方法があります。  
  
-   再初期化後に、前のセクションで説明した方法を使用して、権限を再適用します。  
  
-   サブスクリプションを再初期化するときに、オブジェクトを削除しないように指定します。 再初期化の前に、次のいずれかを実行します。  
  
    -   [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql) または [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)を実行します。 **@property** パラメーターの値として 'pre_creation_cmd' (**sp_changearticle**) または 'pre_creation_command' (**sp_changemergearticle**) を指定し、 **@value** パラメーターの値として 'none'、'delete'、または 'truncate' を指定します。  
  
    -   **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスの **[対象オブジェクト]** セクションで、 **[既存のオブジェクトを変更せずに保持します]** 、 **[データを削除します。アーティクルに行フィルターがある場合は、フィルターに一致するデータのみを削除します]** または **[既存のオブジェクト内にあるすべてのデータを切り捨てます]** を **[名前が使用中である場合のアクション]** 」で選択します。 このダイアログ ボックスへのアクセスの詳細については、「[View and Modify Publication Properties](../publish/view-and-modify-publication-properties.md)」 (パブリケーションのプロパティの表示および変更) を参照してください。  
  
## <a name="database-maintenance"></a>データベースのメンテナンス  
  
### <a name="why-cant-i-run-truncate-table-on-a-published-table"></a>パブリッシュされたテーブルで TRUNCATE TABLE を実行できないのはなぜですか。  
 TRUNCATE TABLE はログに記録されない操作であり、トリガーも起動されません。 操作による変更を追跡できないため、TRUNCATE TABLE は許可されていません。トランザクション レプリケーションでは、トランザクション ログを通じて変更が追跡され、マージ レプリケーションでは、パブリッシュされたテーブルのトリガーを通じて変更が追跡されます。  
  
### <a name="what-is-the-effect-of-running-a-bulk-insert-command-on-a-replicated-database"></a>レプリケートされたデータベース上で一括挿入コマンドを実行するとどのような影響がありますか。  
 トランザクション レプリケーションの場合、他の挿入と同様に一括挿入も追跡およびレプリケートされます。 マージ レプリケーションでは、変更を追跡するメタデータが正しく更新されるようにする必要があります。  
  
### <a name="are-there-any-replication-considerations-for-backup-and-restore"></a>バックアップと復元を行うときにレプリケーションに関する注意点はありますか。  
 可能。 データベースのレプリケーションに関係する特別な注意点がいくつかあります。 詳細については、「 [レプリケートされたデータベースのバックアップと復元](back-up-and-restore-replicated-databases.md)」を参照してください。  
  
### <a name="does-replication-affect-the-size-of-the-transaction-log"></a>レプリケーションはトランザクション ログの大きさに影響しますか。  
 マージ レプリケーションとスナップショット レプリケーションは、トランザクション ログのサイズには影響しません。ただし、トランザクション レプリケーションは影響する場合があります。 データベースに 1 つ以上のトランザクション パブリケーションが含まれている場合、それらのパブリケーションに関連するすべてのトランザクションがディストリビューション データベースに配布されるまで、トランザクション ログの切り捨ては行われません。 トランザクション ログが大きくなりすぎ、ログ リーダー エージェントをスケジュールによって実行している場合は、実行間隔を短くすることを検討してください。 または、連続モードで実行するように設定してください。 連続モードで実行するように設定されている場合は (既定値)、実行中であることを確認してください。 ログ リーダー エージェントの状態を確認する方法の詳細については、次を参照してください。[情報を表示し、レプリケーション モニターを使用してタスクを実行する](../monitor/view-information-and-perform-tasks-replication-monitor.md)します。  
  
 また、パブリケーション データベースまたはディストリビューション データベース上で "sync with backup" オプションを設定している場合は、すべてのトランザクションのバックアップが完了するまでトランザクション ログの切り捨ては行われません。 トランザクション ログが大きくなりすぎ、かつ、このオプションを設定している場合は、トランザクション ログのバックアップ間隔を短くしてください。 トランザクション レプリケーションに関係するデータベースのバックアップと復元の詳細については、「[Strategies for Backing Up and Restoring Snapshot and Transactional Replication](strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)」 (スナップショット レプリケーションおよびトランザクション レプリケーションのバックアップと復元の方式) を参照してください。  
  
### <a name="how-do-i-rebuild-indexes-or-tables-in-replicated-databases"></a>レプリケートされたデータベースのインデックスやテーブルを再構築するにはどうすればよいですか。  
 インデックスの再構築にはいくつかのメカニズムがあります。 どのメカニズムもレプリケーションに関して特別な注意をせずに使用できます。ただし、トランザクション パブリケーションのテーブルでは主キーが必要なため、主キーの削除や再作成を行うことはできません。  
  
### <a name="how-do-i-add-or-change-indexes-on-publication-and-subscription-databases"></a>パブリケーション データベースとサブスクリプション データベース上でインデックスを追加または変更するにはどうすればよいですか。  
 レプリケーションに関して特別な注意をしなくても、パブリッシャーまたはサブスクライバーでインデックスを追加できます (インデックスがパフォーマンスに影響する点に注意してください)。 CREATE INDEX および ALTER INDEX はレプリケートされないため、たとえばパブリッシャーでインデックスを追加または変更した場合、サブスクライバーに反映するためには、同じ追加または変更を行う必要があります。  
  
### <a name="how-do-i-move-or-rename-files-for-databases-involved-in-replication"></a>レプリケーションに関連するデータベースのファイルは、どのように移動または名前の変更を行うのですか。  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] より前のバージョンの [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]では、データベース ファイルの移動または名前の変更を行うには、データベースのデタッチと再アタッチが必要でした。 レプリケートされたデータベースはデタッチできないため、まずデータベースからレプリケーションを削除する必要がありました。 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]以降では、データベースのデタッチと再アタッチを行わなくてもファイルの移動や名前の変更が行え、レプリケーションに影響を与えることもありません。 ファイルの移動と名前の変更については、「[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)」を参照してください。  
  
### <a name="how-do-i-drop-a-table-that-is-being-replicated"></a>レプリケートされているテーブルを削除するにはどうすればよいですか。  
 まず [sp_droparticle](/sql/relational-databases/system-stored-procedures/sp-droparticle-transact-sql)、[sp_dropmergearticle](/sql/relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql)、 **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスのいずれかを使用してパブリケーションからアーティクルを削除し、次に `DROP <Object>` を使用してデータベースからアーティクルを削除します。 サブスクリプションを追加した後で、スナップショット パブリケーションまたはトランザクション パブリケーションからアーティクルを削除することはできません。まずサブスクリプションを削除する必要があります。 詳細については、「[Add Articles to and Drop Articles from Existing Publications](../publish/add-articles-to-and-drop-articles-from-existing-publications.md)」 (既存のパブリケーションでのアーティクルの追加および削除) を参照してください。  
  
### <a name="how-do-i-add-or-drop-columns-on-a-published-table"></a>パブリッシュされたテーブル上の列を追加または削除するにはどうすればよいですか。  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、列の追加や削除などの、パブリッシュされたオブジェクトに対するスキーマのさまざまな変更がサポートされています。 たとえば、ALTER TABLE …DROP COLUMN をパブリッシャーで実行すると、ステートメントがサブスクライバーにレプリケートされて実行され、列が削除されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] より前のバージョンの [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] が実行されているサブスクライバーでは、ストアド プロシージャ [sp_repladdcolumn](/sql/relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql) および [sp_repldropcolumn](/sql/relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql)で列の追加と削除がサポートされています。 詳細については、「[パブリケーション データベースでのスキーマの変更](../publish/make-schema-changes-on-publication-databases.md)」を参照してください。  
  
## <a name="replication-maintenance"></a>レプリケーションのメンテナンス  
  
### <a name="how-do-i-determine-if-the-data-at-subscribers-is-synchronized-with-data-at-the-publisher"></a>サブスクライバーのデータがパブリッシャーのデータと同期していることはどうすれば判断できますか。  
 検証機能を使用します。 検証では、指定したサブスクライバーがパブリッシャーと同期されているかどうかがレポートされます。 詳細については、「[Validate Replicated Data](../validate-data-at-the-subscriber.md)」 (レプリケートされたデータの検証) を参照してください。 正しく同期されていない行がある場合、検証を行っても、同期されていない行についての情報が表示されませんが、 [tablediff ユーティリティ](../../../tools/tablediff-utility.md) では表示されます。  
  
### <a name="how-do-i-add-a-table-to-an-existing-publication"></a>既存のパブリケーションにテーブルを追加するにはどうすればよいですか。  
 テーブル (または他のオブジェクト) を追加するときに、パブリケーション データベースまたはサブスクリプション データベースに対する操作を停止する必要はありません。 パブリケーションにテーブルを追加するには、 **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスか、ストアド プロシージャ [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) および [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) を使用します。 詳細については、「[Add Articles to and Drop Articles from Existing Publications](../publish/add-articles-to-and-drop-articles-from-existing-publications.md)」 (既存のパブリケーションでのアーティクルの追加および削除) を参照してください。  
  
### <a name="how-do-i-remove-a-table-from-a-publication"></a>パブリケーションからテーブルを削除するにはどうすればよいですか。  
 パブリケーションからテーブルを削除するには、[sp_droparticle](/sql/relational-databases/system-stored-procedures/sp-droparticle-transact-sql)、[sp_dropmergearticle](/sql/relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql)、または **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスを使用します。 サブスクリプションを追加した後で、スナップショット パブリケーションまたはトランザクション パブリケーションからアーティクルを削除することはできません。まずサブスクリプションを削除する必要があります。 詳細については、「[Add Articles to and Drop Articles from Existing Publications](../publish/add-articles-to-and-drop-articles-from-existing-publications.md)」 (既存のパブリケーションでのアーティクルの追加および削除) を参照してください。  
  
### <a name="what-actions-require-subscriptions-to-be-reinitialized"></a>サブスクリプションの再初期化が必要となる操作にはどのようなものがありますか。  
 アーティクルやパブリケーションに対する変更の中には、サブスクリプションの再初期化が必要になるものがあります。 詳細については、「[Change Publication and Article Properties](../publish/change-publication-and-article-properties.md)」 (パブリケーションおよびアーティクルのプロパティの変更) を参照してください。  
  
### <a name="what-actions-cause-snapshots-to-be-invalidated"></a>スナップショットが無効になる操作にはどのようなものがありますか。  
 アーティクルやパブリケーションに対する変更の中には、スナップショットが無効になり、新しいスナップショットを生成する必要が生じるものがあります。 詳細については、「[Change Publication and Article Properties](../publish/change-publication-and-article-properties.md)」 (パブリケーションおよびアーティクルのプロパティの変更) を参照してください。  
  
### <a name="how-do-i-remove-replication"></a>レプリケーションを削除するにはどうすればよいですか。  
 データベースからレプリケーションを削除するために必要な操作は、データベースがパブリケーション データベースであるか、サブスクリプション データベースであるか、その両方であるかによって異なります。  
  
### <a name="how-do-i-determine-whether-there-are-transactions-or-rows-to-be-replicated"></a>レプリケートする必要のあるトランザクションまたは行があるかどうかはどうすれば判断できますか。  
 トランザクション レプリケーションの場合は、ストアド プロシージャか、レプリケーション モニターの **[未配布のコマンド]** タブを使用します。 詳細については、次を参照してください[ビューのレプリケートされたコマンドとディストリビューション データベース内のその他の情報&#40;レプリケーション TRANSACT-SQL プログラミング&#41;](../monitor/view-replicated-commands-and-information-in-distribution-database.md)と[情報を表示しを使用したタスクの実行。レプリケーション モニター](../monitor/view-information-and-perform-tasks-replication-monitor.md)します。  
  
 マージ レプリケーションの場合は、ストアド プロシージャ **sp_showpendingchanges**を使用します。 詳細については、「[sp_showpendingchanges &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql)」を参照してください。  
  
### <a name="how-far-behind-is-the-distribution-agent-should-i-reinitialize"></a>ディストリビューション エージェントがどの程度遅れているのか、 再初期化が必要かどうかを確認する方法はありますか。  
 ストアド プロシージャ **sp_replmonitorsubscriptionpendingcmds** か、レプリケーション モニターの **[未配布のコマンド]** タブを使用します。 ストアド プロシージャとタブには、次の内容が表示されます。  
  
-   ディストリビューション データベース内のコマンドで、選択したサブスクライバーにまだ配布されていないコマンドの数を示します。 コマンドは、1 つの Transact-SQL データ操作言語 (DML) ステートメントまたは 1 つのデータ定義言語 (DDL) ステートメントから構成されます。  
  
-   コマンドをサブスクライバーに配布するのに要すると推定される時間を示します。 スナップショットを生成してサブスクライバーに適用するのに必要な時間よりもこの値が大きい場合は、サブスクライバーの再初期化を検討してください。 詳細については、「 [サブスクリプションの再初期化](../reinitialize-subscriptions.md)」を参照してください。  
  
 詳細については、次を参照してください。 [sp_replmonitorsubscriptionpendingcmds &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql)と[情報を表示し、レプリケーション モニターを使用してタスクを実行する](../monitor/view-information-and-perform-tasks-replication-monitor.md)します。  
  
## <a name="replication-and-other-database-features"></a>レプリケーションおよびその他のデータベース機能  
  
### <a name="does-replication-work-in-conjunction-with-log-shipping-and-database-mirroring"></a>レプリケーションはログ配布やデータベース ミラーリングと組み合わせて使用できますか。  
 可能。 詳細については、「[Log Shipping and Replication &#40;SQL Server&#41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md)」(ログ配布とレプリケーション &#40;SQL Server&#41;) および「[Database Mirroring and Replication &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)」(データベース ミラーリングとレプリケーション &#40;SQL Server&#41;) を参照してください。  
  
### <a name="does-replication-work-in-conjunction-with-clustering"></a>レプリケーションはクラスター化と組み合わせて使用できますか。  
 可能。 データはすべてクラスターの 1 つのディスク セットに格納されるため、特別な注意は不要です。  
  
## <a name="see-also"></a>参照  
 [レプリケーション管理に関する FAQ](frequently-asked-questions-for-replication-administrators.md)   
 [Best Practices for Replication Administration](best-practices-for-replication-administration.md)  
  
  
