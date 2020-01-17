---
title: sp_addmergepublication (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepublication
- sp_addmergepublication_TSQL
helpviewer_keywords:
- sp_addmergepublication
ms.assetid: 28a629a1-7374-4614-9b04-279d290a942a
author: stevestein
ms.author: sstein
ms.openlocfilehash: a296f5b4cb20768d5aa244646e584bede110d26a
ms.sourcegitcommit: 710d60e7974e2c4c52aebe36fceb6e2bbd52727c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2019
ms.locfileid: "72278352"
---
# <a name="sp_addmergepublication-transact-sql"></a>sp_addmergepublication (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  新しいマージパブリケーションを作成します。 このストアドプロシージャは、パブリッシャー側でパブリッシュされているデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addmergepublication [ @publication = ] 'publication'   
    [ , [ @description = ] 'description'   
    [ , [ @retention = ] retention ]   
    [ , [ @sync_mode = ] 'sync_mode' ]   
    [ , [ @allow_push = ] 'allow_push' ]   
    [ , [ @allow_pull = ] 'allow_pull' ]   
    [ , [ @allow_anonymous = ] 'allow_anonymous' ]   
    [ , [ @enabled_for_internet = ] 'enabled_for_internet' ]   
    [ , [ @centralized_conflicts = ] 'centralized_conflicts' ]   
    [ , [ @dynamic_filters = ] 'dynamic_filters' ]   
    [ , [ @snapshot_in_defaultfolder = ] 'snapshot_in_default_folder' ]   
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]   
    [ , [ @pre_snapshot_script = ] 'pre_snapshot_script' ]   
    [ , [ @post_snapshot_script = ] 'post_snapshot_script' ]   
    [ , [ @compress_snapshot = ] 'compress_snapshot' ]   
    [ , [ @ftp_address = ] 'ftp_address' ]   
    [ , [ @ftp_port = ] ftp_port ]   
    [ , [ @ftp_subdirectory = ] 'ftp_subdirectory' ]   
    [ , [ @ftp_login = ] 'ftp_login' ]   
    [ , [ @ftp_password = ] 'ftp_password' ]   
    [ , [ @conflict_retention = ] conflict_retention ]   
    [ , [ @keep_partition_changes = ] 'keep_partition_changes' ]   
    [ , [ @allow_subscription_copy = ] 'allow_subscription_copy' ]   
    [ , [ @allow_synctoalternate = ] 'allow_synctoalternate' ]   
    [ , [ @validate_subscriber_info = ] 'validate_subscriber_info' ]   
    [ , [ @add_to_active_directory = ] 'add_to_active_directory' ]   
    [ , [ @max_concurrent_merge = ] maximum_concurrent_merge ]   
    [ , [ @max_concurrent_dynamic_snapshots = ] max_concurrent_dynamic_snapshots ]  
    [ , [ @use_partition_groups = ] 'use_partition_groups' ]  
    [ , [ @publication_compatibility_level = ] 'backward_comp_level' ]  
    [ , [ @replicate_ddl = ] replicate_ddl ]  
    [ , [ @allow_subscriber_initiated_snapshot = ] 'allow_subscriber_initiated_snapshot' ]   
    [ , [ @allow_web_synchronization = ] 'allow_web_synchronization' ]   
    [ , [ @web_synchronization_url = ] 'web_synchronization_url' ]  
    [ , [ @allow_partition_realignment = ] 'allow_partition_realignment' ]  
    [ , [ @retention_period_unit = ] 'retention_period_unit' ]  
    [ , [ @generation_leveling_threshold = ] generation_leveling_threshold ]  
    [ , [ @automatic_reinitialization_policy = ] automatic_reinitialization_policy ]  
    [ , [ @conflict_logging = ] 'conflict_logging' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` には、作成するマージパブリケーションの名前を指定します。 *publication*は**sysname**であり、既定値はありません。キーワード ALL を指定することはできません。 パブリケーションの名前は、データベース内で一意である必要があります。  
  
`[ @description = ] 'description'` パブリケーションの説明です。 *説明*は**nvarchar (255)** ,、既定値は NULL です。  
  
`[ @retention = ] retention` は、指定された*パブリケーション*の変更を保存する保有期間の単位です。 *保有期間*は**int**,、既定値は14単位です。 保有期間の単位は*retention_period_unit*によって定義されます。 保有期間内にサブスクリプションが同期されず、受信した保留中の変更がディストリビューター側でクリーンアップ操作によって削除された場合、サブスクリプションは有効期限切れとなり、再初期化する必要があります。 許容される最大保有期間は、9999年12月31日から現在の日付までの日数です。  
  
> [!NOTE]  
>  マージパブリケーションの保有期間には、異なるタイムゾーンのサブスクライバーに対応するために、24時間の猶予期間があります。 たとえば、保有期間を 1 日に設定した場合、実際の保有期間は 48 時間となります。  
  
`[ @sync_mode = ] 'sync_mode'` は、パブリケーションに対するサブスクライバーの初期同期モードです。 *sync_mode*は**nvarchar (10)** で、次のいずれかの値を指定できます。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**native** (既定値)|すべてのテーブルのネイティブモードの一括コピープログラム出力を生成します。|  
|**character**|すべてのテーブルのキャラクターモードの一括コピープログラム出力を生成します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] および[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーをサポートするために必要です。|  
  
`[ @allow_push = ] 'allow_push'` は、指定されたパブリケーションに対してプッシュサブスクリプションを作成できるかどうかを指定します。 *allow_push*は**nvarchar (5)** ,、既定値は TRUE の場合、パブリケーションに対してプッシュサブスクリプションを許可します。  
  
`[ @allow_pull = ] 'allow_pull'` は、指定されたパブリケーションに対してプルサブスクリプションを作成できるかどうかを指定します。 *allow_pull*は**nvarchar (5)** ,、既定値は TRUE の場合、パブリケーションに対してプルサブスクリプションを許可します。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] サブスクライバーをサポートするには true を指定する必要があります。  
  
`[ @allow_anonymous = ] 'allow_anonymous'` は、指定されたパブリケーションに対して匿名サブスクリプションを作成できるかどうかを指定します。 *allow_anonymous*は**nvarchar (5)** ,、既定値は TRUE の場合、パブリケーションに対して匿名サブスクリプションを許可します。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] サブスクライバーをサポートするには、 **true**を指定する必要があります。  
  
`[ @enabled_for_internet = ] 'enabled_for_internet'` は、パブリケーションがインターネットに対して有効になっているかどうかを指定し、ファイル転送プロトコル (FTP) を使用してスナップショットファイルをサブスクライバーに転送できるかどうかを決定します。 *enabled_for_internet*は**nvarchar (5)** ,、既定値は FALSE です。 **True**の場合、パブリケーションの同期ファイルは C:\PROGRAM are SQL Server\MSSQL\MSSQL.x\Repldata\Ftp ディレクトリに格納されます。 ユーザーは Ftp ディレクトリを作成する必要があります。 **False**の場合、パブリケーションはインターネットアクセスに対して有効になっていません。  
  
`[ @centralized_conflicts = ] 'centralized_conflicts'` このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のためにのみサポートされています。 *Conflict_logging*を使用して、競合レコードを格納する場所を指定します。  
  
`[ @dynamic_filters = ] 'dynamic_filters'` により、マージパブリケーションでパラメーター化された行フィルターを使用できるようになります。 *dynamic_filters*は**nvarchar (5)** ,、既定値は FALSE です。  
  
> [!NOTE]  
>  このパラメーターを指定するのではなく、パラメーター化された行フィルターが使用されているかどうかを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が自動的に判断できるようにする必要があります。 *Dynamic_filters*に**true**を指定した場合は、アーティクルに対してパラメーター化された行フィルターを定義する必要があります。 詳しくは、「 [マージ アーティクルのパラメーター化された行フィルターの定義および変更](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)」をご覧ください。  
  
`[ @snapshot_in_defaultfolder = ] 'snapshot_in_default_folder'` スナップショットファイルを既定のフォルダーに格納するかどうかを指定します。 *snapshot_in_default_folder*は**nvarchar (5)** ,、既定値は TRUE です。 **True**の場合、スナップショットファイルは既定のフォルダーにあります。 **False**の場合、スナップショットファイルは*alternate_snapshot_folder*によって指定された別の場所に格納されます。 代替位置としては、他のサーバー、ネットワーク ドライブ、または CD-ROM やリムーバブル ディスクなどのリムーバブル メディアを指定できます。 スナップショットファイルをファイル転送プロトコル (FTP) サイトに保存して、後でサブスクライバーで取得することもできます。 このパラメーターは true であり、 *alt_snapshot_folder*によって指定された場所を持つことができることに注意してください。 この組み合わせでは、スナップショットファイルが既定の場所と代替の場所の両方に格納されることを指定します。  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'` スナップショットの代替フォルダーの場所を指定します。 *alternate_snapshot_folder*は**nvarchar (255)** ,、既定値は NULL です。  
  
`[ @pre_snapshot_script = ] 'pre_snapshot_script'` **.sql**ファイルの場所へのポインターを指定します。 *pre_snapshot_script*は**nvarchar (255)** ,、既定値は NULL です。 マージ エージェントは、サブスクライバーでスナップショットを適用するときに、レプリケートされたオブジェクト スクリプトより前に、プリスナップショット スクリプトを実行します。 このスクリプトは、サブスクリプションデータベースに接続するときに、マージエージェントによって使用されるセキュリティコンテキストで実行されます。 プリスナップショットスクリプトは [!INCLUDE[ssEW](../../includes/ssew-md.md)] サブスクライバーでは実行されません。  
  
`[ @post_snapshot_script = ] 'post_snapshot_script'` **.sql**ファイルの場所へのポインターを指定します。 *post_snapshot_script*は**nvarchar (255)** ,、既定値は NULL です。 最初の同期のときに、マージ エージェントは、他のすべてのレプリケートされたオブジェクト スクリプトとデータが適用された後に、ポストスナップショット スクリプトを実行します。 このスクリプトは、サブスクリプションデータベースに接続するときに、マージエージェントによって使用されるセキュリティコンテキストで実行されます。 ポストスナップショットスクリプトは [!INCLUDE[ssEW](../../includes/ssew-md.md)] サブスクライバーでは実行されません。  
  
`[ @compress_snapshot = ] 'compress_snapshot'` は **\@alt_snapshot_folder**の場所に書き込まれたスナップショットを [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 形式に圧縮することを指定します。 *compress_snapshot*は**nvarchar (5)** ,、既定値は FALSE です。 **false**を指定すると、スナップショットは圧縮されません。**true**は、スナップショットを圧縮することを指定します。 2 GB より大きいスナップショット ファイルは圧縮できません。 圧縮されたスナップショット ファイルは、マージ エージェントが実行されている場所で解凍されます。一般にプル サブスクリプションでは、サブスクライバーでファイルが解凍されるように、圧縮されたスナップショットが使用されます。 既定のフォルダー内のスナップショットは圧縮できません。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] サブスクライバーをサポートするには、 **false**を指定する必要があります。  
  
`[ @ftp_address = ] 'ftp_address'` は、ディストリビューター用の FTP サービスのネットワークアドレスです。 *ftp_address*は**sysname**,、既定値は NULL です。 サブスクライバーのマージエージェントが取得するパブリケーションスナップショットファイルの場所を指定します。 このプロパティは、各パブリケーションに対して格納されるため、各パブリケーションは異なる*ftp_address*を持つことができます。 パブリケーションは、FTP を使用したスナップショットの配布をサポートしている必要があります。  
  
`[ @ftp_port = ] ftp_port` は、ディストリビューター用の FTP サービスのポート番号です。 *ftp_port*は**int**,、既定値は21です。 サブスクライバーのマージ エージェントが検索するパブリケーション スナップショット ファイルの場所を指定します。 このプロパティはパブリケーションごとに格納されるため、各パブリケーションには独自の*ftp_port*を設定できます。  
  
`[ @ftp_subdirectory = ] 'ftp_subdirectory'` では、パブリケーションが FTP を使用したスナップショットの配布をサポートしている場合に、サブスクライバーのマージエージェントでスナップショットファイルを取得できる場所を指定します。 *ftp_subdirectory*は**nvarchar (255)** ,、既定値は NULL です。 このプロパティはパブリケーションごとに格納されるので、各パブリケーションは独自の*ftp_subdirctory*を持つことも、サブディレクトリを使用しないようにすることもできます。この場合、NULL 値が指定されます。  
  
 パラメーター化されたフィルターを使用してパブリケーションのスナップショットを事前に生成する場合は、各サブスクライバーパーティションのデータスナップショットが独自のフォルダーに存在する必要があります。 FTP を使用して事前に生成されたスナップショットのディレクトリ構造は、次の構造に従う必要があります。  
  
 *alternate_snapshot_folder*\ ftp\\*publisher_publicationDB_publication*\\*partitionID*。  
  
> [!NOTE]  
>  斜体の値は、パブリケーションとサブスクライバーのパーティションの詳細によって異なります。  
  
`[ @ftp_login = ] 'ftp_login'` は、FTP サービスへの接続に使用するユーザー名です。 *ftp_login*は**sysname**で、既定値は ' anonymous ' です。  
  
`[ @ftp_password = ] 'ftp_password'` は、FTP サービスへの接続に使用するユーザーパスワードです。 *ftp_password*は**sysname**,、既定値は NULL です。  
  
> [!IMPORTANT]  
>  空白のパスワードは使用しないでください。 強力なパスワードを使用してください。  
  
`[ @conflict_retention = ] conflict_retention` 競合を保持する保有期間を日数で指定します。 *conflict_retention*は**int**,、既定値は14日、競合行が競合テーブルから削除されます。  
  
事前計算済みパーティションを使用できない場合に、パーティションの変更の最適化を有効にするかどうかを指定 `[ @keep_partition_changes = ] 'keep_partition_changes'` です。 *keep_partition_changes*は**nvarchar (5)** ,、既定値は TRUE です。 **false**は、パーティションの変更が最適化されていないことを意味します。また、事前計算済みパーティションを使用しない場合、すべてのサブスクライバーに送信されるパーティションは、パーティション内のデータが変更されるときに検証されます。 **true**は、パーティションの変更が最適化され、変更されたパーティション内の行を持つサブスクライバーだけが影響を受けることを意味します。 事前計算済みパーティションを使用する場合は、 *use_partition_groups*を**true**に設定し、 *keep_partition_changes*を**false**に設定します。 詳細については、「[事前計算済みパーティションによるパラメーター化されたフィルターのパフォーマンス最適化](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)」を参照してください。  
  
> [!NOTE]  
>  *Keep_partition_changes*に**true**を指定した場合は、スナップショットエージェントパラメーター **-maxnetworkoptimization**に値**1**を指定します。 このパラメーターの詳細については、「 [Replication スナップショットエージェント](../../relational-databases/replication/agents/replication-snapshot-agent.md)」を参照してください。 エージェントパラメーターの指定方法の詳細については、「 [Replication Agent Administration](../../relational-databases/replication/agents/replication-agent-administration.md)」を参照してください。  
  
 [!INCLUDE[ssEW](../../includes/ssew-md.md)] のサブスクライバーでは、 *keep_partition_changes*を true に設定して、削除が正しく反映されるようにする必要があります。 false に設定すると、サブスクライバーに予想よりも多くの行が含まれる場合があります。  
  
`[ @allow_subscription_copy = ] 'allow_subscription_copy'` は、このパブリケーションをサブスクライブするサブスクリプションデータベースをコピーする機能を有効または無効にします。 *allow_subscription_copy*は**nvarchar (5)** ,、既定値は FALSE です。 コピーするサブスクリプションデータベースのサイズは 2 gb 未満である必要があります。  
  
`[ @allow_synctoalternate = ] 'allow_synctoalternate'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @validate_subscriber_info = ] 'validate_subscriber_info'` には、パラメーター化された行フィルターが使用されている場合に、パブリッシュされたデータのサブスクライバーパーティションを定義するために使用される関数が一覧表示されます。 *validate_subscriber_info*は**nvarchar (500)** ,、既定値は NULL です。 この情報は、マージ エージェントがサブスクライバーのパーティションを検証するときに使用されます。 たとえば、パラメーター化された行フィルターで[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)が使用されている場合、パラメーターは `@validate_subscriber_info=N'SUSER_SNAME()'`である必要があります。  
  
> [!NOTE]  
>  このパラメーターは指定しないで、代わりに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がフィルター選択条件を自動的に決定できるようにしてください。  
  
`[ @add_to_active_directory = ] 'add_to_active_directory'` このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のためにのみサポートされています。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory には、パブリケーション情報を追加できなくなりました。  
  
同時に実行できるマージプロセスの最大数 `[ @max_concurrent_merge = ] maximum_concurrent_merge` ます。 *maximum_concurrent_merge*は**int**で、既定値は0です。 このプロパティの値が**0**の場合は、特定の時点で同時に実行されているマージプロセスの数に制限がないことを意味します。 このプロパティは、マージパブリケーションに対して一度に実行できる同時マージプロセスの数に制限を設定します。 同時にスケジュールに組み込まれているマージ処理の数が、指定された実行可能な数より大きい場合、余分なジョブは待ち行列に挿入され、現在実行されているマージ処理が終わるまで待機状態に置かれます。  
  
サブスクライバーパーティションのフィルター選択されたデータスナップショットを生成するために同時に実行できるスナップショットエージェントセッションの最大数を `[ @max_concurrent_dynamic_snapshots = ] max_concurrent_dynamic_snapshots` します。 *maximum_concurrent_dynamic_snapshots*は**int**で、既定値は0です。 **0**の場合、スナップショットセッションの数に制限はありません。 同時にスケジュールに組み込まれているスナップショット処理の数が、指定された実行可能な数より大きい場合、余分なジョブは待ち行列に挿入され、現在実行されているスナップショット処理が終わるまで待機状態に置かれます。  
  
`[ @use_partition_groups = ] 'use_partition_groups'` は、同期プロセスを最適化するために事前計算済みパーティションを使用する必要があることを指定します。 *use_partition_groups*は**nvarchar (5)** で、次のいずれかの値を指定できます。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**true**|パブリケーションは事前計算済みパーティションを使用します。|  
|**false**|パブリケーションは事前計算済みパーティションを使用しません。|  
|NULL (既定値)|システムがパーティション分割ストラテジを決定します。|  
  
 既定では、事前計算済みパーティションが使用されます。 事前計算済みパーティションを使用しないようにするには、 *use_partition_groups*を**false**に設定する必要があります。 NULL の場合、システムは事前計算済みパーティションを使用できるかどうかを決定します。 事前計算済みパーティションを使用できない場合、この値は、エラーが生成されることなく、実質的に**false**になります。 このような場合は、 *keep_partition_changes*を**true**に設定して、いくつかの最適化を行うことができます。 詳細については、「パラメーター化された[行フィルター](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md) 」および「[事前計算済みパーティションによるパラメーター化されたフィルターのパフォーマンスの最適化](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)  
  
`[ @publication_compatibility_level = ] backward_comp_level` は、パブリケーションの旧バージョンとの互換性を示します。 *backward_comp_level*は**nvarchar (6)** で、次のいずれかの値を指定できます。  
  
|ReplTest1|Version|  
|-----------|-------------|  
|**90RTM**|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|  
|**100RTM**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
  
`[ @replicate_ddl = ] replicate_ddl` は、パブリケーションに対してスキーマレプリケーションがサポートされているかどうかを示します。 *replicate_ddl*は**int**,、既定値は1です。 **1**は、パブリッシャーで実行されるデータ定義言語 (DDL) ステートメントがレプリケートされることを示し、 **0**は ddl ステートメントがレプリケートされないことを示します。 詳細については、「[パブリケーション データベースでのスキーマの変更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)」を参照してください。  
  
 *\@Replicate_ddl* DDL ステートメントは、列を追加するときは、パラメーターを有効にします。 *\@Replicate_ddl* DDL ステートメントが変更または次の理由により、列を削除するときに、パラメーターは無視されます。  
  
-   列が削除された場合、sysarticlecolumns を更新して、新しい DML ステートメントに削除された列が含まれないようにする必要があります。これにより、ディストリビューションエージェントが失敗する原因となります。 *\@Replicate_ddl*レプリケーションは、スキーマの変更を常にレプリケートする必要がありますので、パラメーターは無視されます。  
  
-   列が変更されると、変換元のデータ型または null 値の許容属性が変更され、サブスクライバー側のテーブルと互換性がない可能性のある値が DML ステートメントに含まれる可能性があります。 そうした DML ステートメントは、ディストリビューション エージェントが失敗する原因となる場合があります。 *\@Replicate_ddl*レプリケーションは、スキーマの変更を常にレプリケートする必要がありますので、パラメーターは無視されます。  
  
-   DDL ステートメントによって新しい列が追加された場合、sysarticlecolumns には新しい列は含まれません。 DML ステートメントでは、新しい列のデータのレプリケートは試行されません。 DDL をレプリケートするかどうかを指定できるので、パラメーターは受け入れられます。  
  
`[ @allow_subscriber_initiated_snapshot = ] 'allow_subscriber_initiated_snapshot'` は、このパブリケーションのサブスクライバーが、データパーティションのフィルター選択されたスナップショットを生成するスナップショットプロセスを開始できるかどうかを示します。 *allow_subscriber_initiated_snapshot*は**nvarchar (5)** ,、既定値は FALSE です。 **true**は、サブスクライバーがスナップショットプロセスを開始できることを示します。  
  
`[ @allow_web_synchronization = ] 'allow_web_synchronization'` は、パブリケーションで Web 同期を有効にするかどうかを指定します。 *allow_web_synchronization*は**nvarchar (5)** ,、既定値は FALSE です。 **true**を指定すると、このパブリケーションへのサブスクリプションを HTTPS 経由で同期できます。 詳細については、「 [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)」を参照してください。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] サブスクライバーをサポートするには、 **true**を指定する必要があります。  
  
`[ @web_synchronization_url = ] 'web_synchronization_url'` Web 同期に使用するインターネット URL の既定値を指定します。 *web_synchronization_url i*s **nvarchar (500)** ,、既定値は NULL です。 [Sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)の実行時に明示的に設定されていない場合は、既定のインターネット URL を定義します。  
  
`[ @allow_partition_realignment = ] 'allow_partition_realignment'` は、パブリッシャーで行を変更するときに、削除をサブスクライバーに送信するかどうかを決定します。 *allow_partition_realignment*は**nvarchar (5)** ,、既定値は TRUE です。 **true**を設定すると、サブスクライバーのパーティションの一部ではなくなったデータを削除することによって、パーティションの変更結果を反映するために、削除がサブスクライバーに送信されます。 **false**を指定すると、サブスクライバー上の古いパーティションのデータは、パブリッシャーでこのデータに加えられた変更がこのサブスクライバーにレプリケートされませんが、サブスクライバーで行われた変更はパブリッシャーにレプリケートされます。 *Allow_partition_realignment*を**false**に設定すると、履歴のためにデータにアクセスする必要がある場合に、古いパーティションからサブスクリプションのデータを保持するために使用されます。  
  
> [!NOTE]  
>  *Allow_partition_realignment*を**false**に設定した結果としてサブスクライバーに残っているデータは、読み取り専用であるかのように処理する必要があります。ただし、これはレプリケーションシステムによって強制されるわけではありません。  
  
`[ @retention_period_unit = ] 'retention_period_unit'`*保有*期間によって設定された保有期間の単位を指定します。 *retention_period_unit*は**nvarchar (10)** で、次のいずれかの値を指定できます。  
  
|ReplTest1|Version|  
|-----------|-------------|  
|**day** (既定値)|保有期間は日数で指定します。|  
|**week**|保有期間は週単位で指定します。|  
|**month**|保有期間は月単位で指定します。|  
|**year**|保有期間は年単位で指定します。|  
  
`[ @generation_leveling_threshold = ] generation_leveling_threshold` は、生成に含まれる変更の数を指定します。 生成とは、パブリッシャーまたはサブスクライバーに配信される変更のコレクションです。 *generation_leveling_threshold*は**int**,、既定値は1000です。  
  
`[ @automatic_reinitialization_policy = ] automatic_reinitialization_policy` は、パブリケーションへの変更に必要な自動再初期化の前に、サブスクライバーから変更をアップロードするかどうかを指定します。この場合、 **\@force_reinit_subscription**には値**1**が指定されています。 *automatic_reinitialization_policy*はビット,、既定値は0です。 **1**は、自動再初期化が行われる前に、変更がサブスクライバーからアップロードされることを意味します。  
  
> [!IMPORTANT]  
>  パラメーター化フィルターを追加、削除、変更する場合は、再初期化の際、サブスクライバーで保留中の変更をパブリッシャーにアップロードできません。 保留中の変更をアップロードしたい場合は、フィルターを変更する前にすべてのサブスクリプションを同期してください。  
  
`[ @conflict_logging = ] 'conflict_logging'` 競合レコードを格納する場所を指定します。 *conflict_logging*は**nvarchar (15)** で、次のいずれかの値を指定できます。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**パブリッシャー**|競合レコードはパブリッシャーに格納されます。|  
|**サブスクライバー**|競合レコードは、競合の原因となったサブスクライバーに保存されます。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] サブスクライバーではサポートされません。|  
|**両方**|競合レコードは、パブリッシャーとサブスクライバーの両方に保存されます。|  
|NULL (既定値)|レプリケーションでは、値*backward_comp_level*が**90rtm**で、その他すべての場合に**パブリッシャー**に対して、 *conflict_logging*が**自動的に設定**されます。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>Remarks  
 **sp_addmergepublication**は、マージレプリケーションで使用します。  
  
 **\@add_to_active_directory**パラメーターを使用して Active Directory にパブリケーションオブジェクトを一覧表示するには、Active Directory に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトをあらかじめ作成しておく必要があります。  
  
 同じデータベースオブジェクトをパブリッシュする複数のパブリケーションが存在する場合は、 *replicate_ddl*値が**1**のパブリケーションだけが ALTER TABLE、ALTER VIEW、ALTER PROCEDURE、ALTER FUNCTION、および alter TRIGGER ddl ステートメントをレプリケートします。 ただし、ALTER TABLE DROP COLUMN DDL ステートメントは、削除された列をパブリッシュしているすべてのパブリケーションによってレプリケートされます。  
  
 [!INCLUDE[ssEW](../../includes/ssew-md.md)] のサブスクライバーの場合、 *alternate_snapshot_folder*の値は*snapshot_in_default_folder*の値が**false**の場合にのみ使用されます。  
  
 パブリケーションに対して ddl レプリケーションが有効になっている (_replicate_ddl_ **= 1**) 場合、パブリケーションに対してレプリケートされていない ddl 変更を行うには[ &#40;sp_changemergepublication&#41; ](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) 、最初に transact-sql を実行して*replicate_ddl*を**0**に設定する必要があります。 レプリケートされていない DDL ステートメントが発行された後、 **sp_changemergepublication**を再度実行して、ddl レプリケーションを有効に戻すことができます。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_AddMergePub](../../relational-databases/replication/codesnippet/tsql/sp-addmergepublication-t_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addmergepublication**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [データとデータベース オブジェクトのパブリッシュ](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [sp_changemergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
