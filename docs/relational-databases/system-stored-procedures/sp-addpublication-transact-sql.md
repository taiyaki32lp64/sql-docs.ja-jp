---
title: sp_addpublication (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpublication_TSQL
- sp_addpublication
helpviewer_keywords:
- sp_addpublication
ms.assetid: c7167ed1-2b7e-4824-b82b-65f4667c4407
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5e6e7232d718d5cf6cb1791783f105f31dc2f4ec
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769096"
---
# <a name="sp_addpublication-transact-sql"></a>sp_addpublication (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  スナップショットパブリケーションまたはトランザクションパブリケーションを作成します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addpublication [ @publication = ] 'publication'  
    [ , [ @taskid = ] tasked ]  
    [ , [ @restricted = ] 'restricted' ]  
    [ , [ @sync_method = ] 'sync_method' ]  
    [ , [ @repl_freq = ] 'repl_freq' ]  
    [ , [ @description = ] 'description' ]  
    [ , [ @status = ] 'status' ]  
    [ , [ @independent_agent = ] 'independent_agent' ]  
    [ , [ @immediate_sync = ] 'immediate_sync' ]  
    [ , [ @enabled_for_internet = ] 'enabled_for_internet' ]  
    [ , [ @allow_push = ] 'allow_push'  
    [ , [ @allow_pull = ] 'allow_pull' ]  
    [ , [ @allow_anonymous = ] 'allow_anonymous' ]  
    [ , [ @allow_sync_tran = ] 'allow_sync_tran' ]  
    [ , [ @autogen_sync_procs = ] 'autogen_sync_procs' ]  
    [ , [ @retention = ] retention ]  
    [ , [ @allow_queued_tran= ] 'allow_queued_updating' ]  
    [ , [ @snapshot_in_defaultfolder= ] 'snapshot_in_default_folder' ]  
    [ , [ @alt_snapshot_folder= ] 'alternate_snapshot_folder' ]  
    [ , [ @pre_snapshot_script= ] 'pre_snapshot_script' ]  
    [ , [ @post_snapshot_script= ] 'post_snapshot_script' ]  
    [ , [ @compress_snapshot= ] 'compress_snapshot' ]  
    [ , [ @ftp_address = ] 'ftp_address' ]  
    [ , [ @ftp_port= ] ftp_port ]  
    [ , [ @ftp_subdirectory = ] 'ftp_subdirectory' ]  
    [ , [ @ftp_login = ] 'ftp_login' ]  
    [ , [ @ftp_password = ] 'ftp_password' ]  
    [ , [ @allow_dts = ] 'allow_dts' ]  
    [ , [ @allow_subscription_copy = ] 'allow_subscription_copy' ]  
    [ , [ @conflict_policy = ] 'conflict_policy' ]  
    [ , [ @centralized_conflicts = ] 'centralized_conflicts' ]   
    [ , [ @conflict_retention = ] conflict_retention ]  
    [ , [ @queue_type = ] 'queue_type' ]  
    [ , [ @add_to_active_directory = ] 'add_to_active_directory' ]  
    [ , [ @logreader_job_name = ] 'logreader_agent_name' ]  
    [ , [ @qreader_job_name = ] 'queue_reader_agent_name' ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @allow_initialize_from_backup = ] 'allow_initialize_from_backup' ]  
    [ , [ @replicate_ddl = ] replicate_ddl ]  
    [ , [ @enabled_for_p2p = ] 'enabled_for_p2p' ]  
    [ , [ @publish_local_changes_only = ] 'publish_local_changes_only' ]  
    [ , [ @enabled_for_het_sub = ] 'enabled_for_het_sub' ]  
    [ , [ @p2p_conflictdetection = ] 'p2p_conflictdetection' ]  
    [ , [ @p2p_originator_id = ] p2p_originator_id  
    [ , [ @p2p_continue_onconflict = ] 'p2p_continue_onconflict'  
    [ , [ @allow_partition_switch = ] 'allow_partition_switch'  
    [ , [ @replicate_partition_switch = ]'replicate_partition_switch'  
```  
  
## <a name="arguments"></a>引数  
`[ \@publication = ] 'publication'`作成するパブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。 名前はデータベース内で一意である必要があります。  
  
`[ \@taskid = ] taskid`旧バージョンとの互換性のためにのみサポートされています。[ &#40;sp_addpublication_snapshot&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)を使用します。  
  
`[ \@restricted = ] 'restricted'`旧バージョンとの互換性のためにのみサポートされています。*default_access*を使用します。  
  
`[ \@sync_method = ] _'sync_method'`は同期モードです。 *sync_method*は**nvarchar (13)** ,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**native**|すべてのテーブルのネイティブモードの一括コピープログラム出力を生成します。 *Oracle パブリッシャーではサポートされていません*。|  
|**character**|すべてのテーブルのキャラクターモードの一括コピープログラム出力を生成します。 _Oracle パブリッシャーの_場合**文字**_スナップショットレプリケーションでのみ有効_です。|  
|**同時**|すべてのテーブルのネイティブモードの一括コピープログラム出力を生成しますが、スナップショット中はテーブルをロックしません。 トランザクションパブリケーションでのみサポートされます。 *Oracle パブリッシャーではサポートされていません*。|  
|**concurrent_c**|すべてのテーブルのキャラクターモードの一括コピープログラム出力を生成しますが、スナップショット中はテーブルをロックしません。 トランザクションパブリケーションでのみサポートされます。|  
|**データベーススナップショット**|データベース スナップショットから、すべてのテーブルのネイティブ モードの一括コピー プログラム出力を作成します。 データベーススナップショットは、のすべての[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。|  
|**データベーススナップショットの文字**|データベーススナップショットから、すべてのテーブルのキャラクターモードの一括コピープログラム出力を生成します。 データベーススナップショットは、のすべての[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。|  
|NULL (既定値)|パブリッシャーの [!INCLUDE[msCoName](../../includes/msconame-md.md)] 既定値はnative[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリッシャーの場合、 *repl_freq*の値が**Snapshot**に設定されている場合は**文字**が使用され、それ以外の場合は**concurrent_c**になります。|  
  
`[ \@repl_freq = ] 'repl_freq'`レプリケーション頻度の種類を指定します。 *repl_freq*は**nvarchar (10)** で、次のいずれかの値を指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**継続的**標準|すべてのログベースのトランザクションの出力をパブリッシュする。 以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーの場合は、 *sync_method*を**concurrent_c**に設定する必要があります。|  
|**ショット**|スケジュールされた同期イベントのみをパブリッシュする。 以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーの場合は、 *sync_method*を**character**に設定する必要があります。|  
  
`[ \@description = ] 'description'`パブリケーションの説明を指定します (省略可能)。 *説明*は**nvarchar (255)** ,、既定値は NULL です。  
  
`[ \@status = ] 'status'`パブリケーションデータを使用できるかどうかを指定します。 *状態*は**nvarchar (8)** ,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**能動的**|サブスクライバーでパブリケーション データを直ちに使用できる。|  
|**非アクティブ**標準|パブリケーションが最初に作成されたときは、パブリケーションデータを使用できません (サブスクライブすることはできますが、サブスクリプションは処理されません)。|  
  
 *Oracle パブリッシャーではサポートされていません*。  
  
`[ \@independent_agent = ] 'independent_agent'`このパブリケーションに対してスタンドアロンのディストリビューションエージェントがあるかどうかを指定します。 *independent_agent*は**nvarchar (5)** ,、既定値は FALSE。 **True**の場合、このパブリケーションにはスタンドアロンのディストリビューションエージェントがあります。 **False**の場合、パブリケーションは共有ディストリビューションエージェントを使用し、各パブリッシャーデータベース/サブスクライバーデータベースのペアには1つの共有エージェントが存在します。  
  
`[ \@immediate_sync = ] 'immediate_synchronization'`スナップショットエージェントを実行するたびに、パブリケーションの同期ファイルを作成するかどうかを指定します。 *immediate_synchronization*は**nvarchar (5)** ,、既定値は FALSE。 **True**の場合、スナップショットエージェントが実行されるたびに同期ファイルが作成または再作成されます。 サブスクリプションが作成される前にスナップショットエージェントが完了している場合、サブスクライバーはすぐに同期ファイルを取得できます。 新しいサブスクリプションは、最近実行されたスナップショット エージェントによって生成された最新の同期ファイルを取得します。 *immediate_synchronization*を**true**にするには、 *independent_agent*が**true**である必要があります。 **False**の場合、新しいサブスクリプションがある場合にのみ、同期ファイルが作成されます。 既存のパブリケーションに新しいアーティクルを段階的に追加する場合は、サブスクリプションごとに[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)を呼び出す必要があります。 サブスクリプションの後、スナップショット エージェントが起動して完了するまでは、サブスクライバーでは同期ファイルを取得できません。  
  
`[ \@enabled_for_internet = ] 'enabled_for_internet'`パブリケーションがインターネットに対して有効になっているかどうかを指定し、ファイル転送プロトコル (FTP) を使用してスナップショットファイルをサブスクライバーに転送できるかどうかを指定します。 *enabled_for_internet*は**nvarchar (5)** ,、既定値は FALSE。 **True**の場合、パブリケーションの同期ファイルは C:\PROGRAM are SQL Server\MSSQL\MSSQL.x\Repldata\Ftp ディレクトリに格納されます。 ユーザーは Ftp ディレクトリを作成する必要があります。  
  
`[ \@allow_push = ] 'allow_push'`指定されたパブリケーションに対してプッシュサブスクリプションを作成できるかどうかを指定します。 *allow_push*は**nvarchar (5)** ,、既定値は TRUE の場合、パブリケーションに対してプッシュサブスクリプションを許可します。  
  
`[ \@allow_pull = ] 'allow_pull'`指定されたパブリケーションに対してプルサブスクリプションを作成できるかどうかを指定します。 *allow_pull*は**nvarchar (5)** ,、既定値は FALSE。 **False**の場合、パブリケーションに対するプルサブスクリプションは許可されません。  
  
`[ \@allow_anonymous = ] 'allow_anonymous'`指定されたパブリケーションに対して匿名サブスクリプションを作成できるかどうかを指定します。 *allow_anonymous*は**nvarchar (5)** ,、既定値は FALSE。 **True**の場合、 *immediate_synchronization*も**true**に設定する必要があります。 **False**の場合、パブリケーションに対して匿名サブスクリプションは許可されません。  
  
`[ \@allow_sync_tran = ] 'allow_sync_tran'`パブリケーションで即時更新サブスクリプションを許可するかどうかを指定します。 *allow_sync_tran*は**nvarchar (5)** ,、既定値は FALSE。 *Oracle パブリッシャーでは、true はサポートされていません*。  
  
`[ \@autogen_sync_procs = ] 'autogen_sync_procs'`更新サブスクリプションの同期ストアドプロシージャがパブリッシャーで生成されるかどうかを指定します。 *autogen_sync_procs*は**nvarchar (5)** ,、値は次のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**true**|更新サブスクリプションが有効になっている場合に自動的に設定します。|  
|**false**|更新サブスクリプションが無効の場合、または Oracle パブリッシャーの場合、自動的に生成される。|  
|NULL (既定値)|更新サブスクリプションが有効になっている場合の既定値は**true**で、更新サブスクリプションが有効になっていない場合は**false**になります。|  
  
> [!NOTE]  
>  *Autogen_sync_procs*に対してユーザーが指定した値は、 *allow_queued_tran*および*allow_sync_tran*に指定された値によって上書きされます。  
  
`[ \@retention = ] retention`サブスクリプションアクティビティの保有期間を時間単位で示します。 *リテンション期間*は**int**,、既定値は336時間です。 サブスクリプションは、保有期間内に非アクティブになると、期限切れとなって削除されます。 値は、パブリッシャーによって使用されるディストリビューションデータベースの最大保有期間よりも長くすることができます。 **0**の場合、パブリケーションに対する既知のサブスクリプションは有効期限が切れず、有効期限が切れたサブスクリプションクリーンアップエージェントによって削除されます。  
  
`[ \@allow_queued_tran = ] 'allow_queued_updating'`パブリッシャーで適用できるようになるまで、サブスクライバーでの変更のキュー登録を有効または無効にします。 *allow_queued_updating*は**nvarchar (5)** 既定値は FALSE です。 **False**の場合、サブスクライバーでの変更はキューに登録されません。 *Oracle パブリッシャーでは、true はサポートされていません*。  
  
`[ \@snapshot_in_defaultfolder = ] 'snapshot_in_default_folder'`スナップショットファイルを既定のフォルダーに格納するかどうかを指定します。 *snapshot_in_default_folder*は**nvarchar (5)** 既定値は TRUE です。 **True**の場合、スナップショットファイルは既定のフォルダーにあります。 **False**の場合、スナップショットファイルは*alternate_snapshot_folder*で指定された別の場所に格納されています。 別のサーバー、ネットワークドライブ、またはリムーバブルメディア (CD-ROM やリムーバブルディスクなど) に別の場所を配置することもできます。 スナップショット ファイルを FTP サイトに保存し、後でサブスクライバーで取得することもできます。 このパラメーターは true であっても、  **\@alt_snapshot_folder**パラメーター内に位置があることに注意してください。 この組み合わせでは、スナップショットファイルが既定の場所と代替の場所の両方に格納されることを指定します。  
  
`[ \@alt_snapshot_folder = ] 'alternate_snapshot_folder'`スナップショットの代替フォルダーの場所を指定します。 *alternate_snapshot_folder*は**nvarchar (255)** 既定値は NULL です。  
  
`[ \@pre_snapshot_script = ] 'pre_snapshot_script'` **.Sql**ファイルの場所へのポインターを指定します。 *pre_snapshot_script*は**nvarchar (255),、** 既定値は NULL です。 ディストリビューションエージェントは、サブスクライバーでスナップショットを適用するときに、レプリケートされたオブジェクトスクリプトを実行する前に、プリスナップショットスクリプトを実行します。 このスクリプトは、サブスクリプションデータベースに接続するときに、ディストリビューションエージェントによって使用されるセキュリティコンテキストで実行されます。  
  
`[ \@post_snapshot_script = ] 'post_snapshot_script'` **.Sql**ファイルの場所へのポインターを指定します。 *post_snapshot_script*は**nvarchar (255)** ,、既定値は NULL です。 このディストリビューションエージェントでは、すべてのレプリケートされたオブジェクトスクリプトとデータが初期同期中に適用された後に、ポストスナップショットスクリプトが実行されます。 このスクリプトは、サブスクリプションデータベースに接続するときに、ディストリビューションエージェントによって使用されるセキュリティコンテキストで実行されます。  
  
`[ \@compress_snapshot = ] 'compress_snapshot'` **\@Alt_snapshot_folder**の場所に書き込まれるスナップショットを[!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 形式で圧縮することを指定します。 *compress_snapshot*は**nvarchar (5)** ,、既定値は FALSE。 **false**を指定すると、スナップショットは圧縮されません。**true**を指定すると、スナップショットが圧縮されます。 2 GB を超えるスナップショット ファイルは圧縮できません。 圧縮スナップショットファイルは、ディストリビューションエージェントが実行されている場所で圧縮解除されます。プルサブスクリプションは、通常、ファイルがサブスクライバーで圧縮されないように、圧縮スナップショットと共に使用されます。 既定のフォルダー内のスナップショットは圧縮できません。  
  
`[ \@ftp_address = ] 'ftp_address'`ディストリビューター用の FTP サービスのネットワークアドレスを示します。 *ftp_address*は**sysname**,、既定値は NULL です。 ここでは、サブスクライバーのディストリビューション エージェントまたはマージ エージェントがパブリケーション スナップショット ファイルを取得する場所を指定します。 このプロパティは、各パブリケーションに対して格納されるため、各パブリケーションは異なる*ftp_address*を持つことができます。 パブリケーションは、FTP を使用したスナップショットの配布をサポートしている必要があります。  
  
`[ \@ftp_port = ] ftp_port`ディストリビューターの FTP サービスのポート番号を指定します。 *ftp_port*は**int**,、既定値は21です。 サブスクライバーが取得するディストリビューションエージェントまたはマージエージェントのパブリケーションスナップショットファイルの場所を指定します。 このプロパティは、各パブリケーションに対して格納されるため、各パブリケーションは独自の*ftp_port*を持つことができます。  
  
`[ \@ftp_subdirectory = ] 'ftp_subdirectory'`パブリケーションで FTP を使用したスナップショットの配布がサポートされている場合に、サブスクライバーのディストリビューションエージェントまたはマージエージェントでスナップショットファイルを取得できる場所を指定します。 *ftp_subdirectory*は**nvarchar (255)** ,、既定値は NULL です。 このプロパティはパブリケーションごとに格納されるので、各パブリケーションは独自の*ftp_subdirctory*を持つことができます。または、NULL 値が指定されたサブディレクトリを選択できません。  
  
`[ \@ftp_login = ] 'ftp_login'`FTP サービスへの接続に使用するユーザー名です。 *ftp_login*は**sysname**,、既定値は ANONYMOUS です。  
  
`[ \@ftp_password = ] 'ftp_password'`FTP サービスへの接続に使用するユーザーパスワードを入力します。 *ftp_password*は**sysname**,、既定値は NULL です。  
  
`[ \@allow_dts = ] 'allow_dts'`パブリケーションがデータ変換を許可することを指定します。 サブスクリプションを作成するときに DTS パッケージを指定できます。 *allow_transformable_subscriptions*は**nvarchar (5)** 既定値は FALSE では、DTS 変換はできません。 *Allow_dts*が true の場合、 *sync_method*は**文字**または**concurrent_c**のいずれかに設定する必要があります。  
  
 *Oracle パブリッシャーでは、true はサポートされていません*。  
  
`[ \@allow_subscription_copy = ] 'allow_subscription_copy'`このパブリケーションをサブスクライブするサブスクリプションデータベースをコピーする機能を有効または無効にします。 *allow_subscription_copy*は**nvarchar (5)** ,、既定値は FALSE。  
  
`[ \@conflict_policy = ] 'conflict_policy'`キュー更新サブスクライバーオプションを使用する場合の競合解決ポリシーを指定します。 *conflict_policy*は**nvarchar (100)** 既定値は NULL の場合、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**pub wins**|パブリッシャーを優先。|  
|**サブ reinit**|サブスクライバーを再初期化。|  
|**サブ wins**|サブスクライバーを優先。|  
|NULL (既定値)|NULL の場合、パブリケーションがスナップショットパブリケーションの場合、既定のポリシーは**sub reinit**になります。 NULL の場合、パブリケーションがスナップショットパブリケーションでない場合、既定値は**pub wins**になります。|  
  
 *Oracle パブリッシャーではサポートされていません*。  
  
`[ \@centralized_conflicts = ] 'centralized_conflicts'`競合レコードがパブリッシャーに格納されるかどうかを指定します。 *centralized_conflicts*は**nvarchar (5)** ,、既定値は TRUE です。 **True**の場合、競合レコードはパブリッシャーに格納されます。 **False**の場合、競合レコードは、競合の原因となったパブリッシャーとサブスクライバーの両方に格納されます。 *Oracle パブリッシャーではサポートされていません*。  
  
`[ \@conflict_retention = ] conflict_retention`競合の保有期間を日数で指定します。 これは、ピアツーピアトランザクションレプリケーションおよびキュー更新サブスクリプションの競合メタデータが格納される期間です。 *conflict_retention*は**int**,、既定値は14です。 *Oracle パブリッシャーではサポートされていません*。  
  
`[ \@queue_type = ] 'queue_type'`使用するキューの種類を指定します。 *queue_type*は**nvarchar (10)** ,、既定値は NULL の場合、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**sql**|トランザクション[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を格納するために使用します。|  
|NULL (既定値)|既定値は**sql**です。これは[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、を使用してトランザクションを格納することを指定します。|  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing (MSMQ) の使用は現在サポートされていません。 **Msmq**の値を指定すると、警告が表示され、レプリケーションによって値が自動的に**sql**に設定されます。  
  
 *Oracle パブリッシャーではサポートされていません*。  
  
`[ \@add_to_active_directory = ] 'add\to_active_directory'`このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のためにのみサポートされています。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory にパブリケーション情報を追加できなくなりました。  
  
`[ \@logreader_job_name = ] 'logreader_agent_name'`既存のエージェントジョブの名前を指定します。 *logreader_agent_name*は**sysname**,、既定値は NULL です。 このパラメーターは、ログ リーダー エージェントで、新しく作成されるジョブではなく既存のジョブが使用される場合にのみ指定します。  
  
`[ \@qreader_job_name = ] 'queue_reader_agent_name'`既存のエージェントジョブの名前を指定します。 *queue_reader_agent_name*は**sysname**,、既定値は NULL です。 このパラメーターは、キューリーダーエージェントが新しいジョブを作成するのではなく、既存のジョブを使用する場合にのみ指定します。  
  
`[ \@publisher = ] 'publisher'`以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーを指定します。 *publisher*は**sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーにパブリケーションを追加する場合は、*パブリッシャー*を[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用しないでください。  
  
`[ \@allow_initialize_from_backup = ] 'allow_initialize_from_backup'`サブスクライバーが、初期スナップショットではなくバックアップから、このパブリケーションに対するサブスクリプションを初期化できるかどうかを示します。 *allow_initialize_from_backup*は**nvarchar (5)** ,、次の値のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**true**|バックアップからの初期化を有効にする。|  
|**false**|バックアップからの初期化を無効にします。|  
|NULL (既定値)|ピアツーピアレプリケーショントポロジのパブリケーションでは、既定値は**true**になり、他のすべてのパブリケーションでは**false**になります。|  
  
 詳細については、「[スナップショットを使用しないトランザクション サブスクリプションの初期化](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)」を参照してください。  
  
> [!WARNING]  
>  サブスクライバー データの欠落を回避するために、 **sp_addpublication** で `@allow_initialize_from_backup = N'true'`を使用する場合は、常に `@immediate_sync = N'true'`を使用します。  
  
`[ \@replicate_ddl = ] replicate_ddl`パブリケーションでスキーマレプリケーションがサポートされているかどうかを示します。 *replicate_ddl*は**int**,、既定値は 、パブリッシャー [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の場合は1、以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーの場合は**0**です。 **1**は、パブリッシャーで実行されるデータ定義言語 (DDL) ステートメントがレプリケートされることを示し、 **0**は ddl ステートメントがレプリケートされないことを示します。 *スキーマレプリケーションは、Oracle パブリッシャーではサポートされていません。* 詳細については、「[パブリケーション データベースでのスキーマの変更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)」を参照してください。  
  
 *\@Replicate_ddl* DDL ステートメントは、列を追加するときは、パラメーターを有効にします。 *\@Replicate_ddl* DDL ステートメントが変更または次の理由により、列を削除するときに、パラメーターは無視されます。  
  
-   列が削除された場合、sysarticlecolumns を更新して、新しい DML ステートメントに削除された列が含まれないようにする必要があります。これにより、ディストリビューションエージェントが失敗する原因となります。 *\@Replicate_ddl*レプリケーションは、スキーマの変更を常にレプリケートする必要がありますので、パラメーターは無視されます。  
  
-   列が変更されると、変換元のデータ型または null 値の許容属性が変更され、サブスクライバー側のテーブルと互換性がない可能性のある値が DML ステートメントに含まれる可能性があります。 そうした DML ステートメントは、ディストリビューション エージェントが失敗する原因となる場合があります。 *\@Replicate_ddl*レプリケーションは、スキーマの変更を常にレプリケートする必要がありますので、パラメーターは無視されます。  
  
-   DDL ステートメントによって新しい列が追加された場合、sysarticlecolumns には新しい列は含まれません。 DML ステートメントでは、新しい列のデータのレプリケートは試行されません。 DDL をレプリケートするかどうかを指定できるので、パラメーターは受け入れられます。  
  
`[ \@enabled_for_p2p = ] 'enabled_for_p2p'`ピアツーピアレプリケーショントポロジでパブリケーションを使用できるようにします。 *enabled_for_p2p*は**nvarchar (5)** ,、既定値は FALSE。 **true**は、パブリケーションがピアツーピアレプリケーションをサポートすることを示します。 *Enabled_for_p2p*を**true**に設定すると、次の制限が適用されます。  
  
-   *allow_anonymous*は**false**である必要があります。  
  
-   *allow_dts*は**false**である必要があります。  
  
-   *allow_initialize_from_backup*は**true**である必要があります。  
  
-   *allow_queued_tran*は**false**である必要があります。  
  
-   *allow_sync_tran*は**false**である必要があります。  
  
-   *conflict_policy*は**false**である必要があります。  
  
-   *independent_agent*は**true**である必要があります。  
  
-   *repl_freq*は**連続**している必要があります。  
  
-   *replicate_ddl*は**1**である必要があります。  
  
 詳細については、「 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)」を参照してください。  
  
`[ \@publish_local_changes_only = ] 'publish_local_changes_only'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ \@enabled_for_het_sub = ] 'enabled_for_het_sub'`パブリケーションで以外の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サブスクライバーをサポートできるようにします。 *enabled_for_het_sub*は**nvarchar (5)** 既定値は FALSE です。 値**true**は、パブリケーションが以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のサブスクライバーをサポートすることを意味します。 *Enabled_for_het_sub*が**true**の場合、次の制限が適用されます。  
  
-   *allow_initialize_from_backup*は**false**である必要があります。  
  
-   *allow_push*は**true**である必要があります。  
  
-   *allow_queued_tran*は**false**である必要があります。  
  
-   *allow_subscription_copy*は**false**である必要があります。  
  
-   *allow_sync_tran*は**false**である必要があります。  
  
-   *autogen_sync_procs*は**false**である必要があります。  
  
-   *conflict_policy*は NULL にする必要があります。  
  
-   *enabled_for_internet*は**false**である必要があります。  
  
-   *enabled_for_p2p*は**false**である必要があります。  
  
-   *ftp_address*は NULL にする必要があります。  
  
-   *ftp_subdirectory*は NULL にする必要があります。  
  
-   *ftp_password*は NULL にする必要があります。  
  
-   *pre_snapshot_script*は NULL にする必要があります。  
  
-   *post_snapshot_script*は NULL にする必要があります。  
  
-   *replicate_ddl*は0にする必要があります。  
  
-   *qreader_job_name*は NULL にする必要があります。  
  
-   *queue_type*は NULL にする必要があります。  
  
-   *sync_method*を**ネイティブ**または**同時実行**することはできません。  
  
 詳細については、「 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)」を参照してください。  
  
`[ \@p2p_conflictdetection = ] 'p2p_conflictdetection'`パブリケーションがピアツーピアレプリケーションに対して有効になっている場合に、ディストリビューションエージェントが競合を検出できるようにします。 *p2p_conflictdetection*は**nvarchar (5)** 既定値は TRUE です。 詳細については、「 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)」を参照してください。  
  
`[ \@p2p_originator_id = ] p2p_originator_id`ピアツーピアトポロジ内のノードの ID を指定します。 *p2p_originator_id*は**int**,、既定値は NULL です。 *P2p_conflictdetection*が TRUE に設定されている場合、この ID は競合の検出に使用されます。 トポロジで使用されていない正の0以外の ID を指定してください。 既に使用されている Id の一覧を表示するには、 [sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md)を実行します。  
  
`[ \@p2p_continue_onconflict = ] 'p2p_continue_onconflict'`競合が検出された後もディストリビューションエージェントが変更を処理するかどうかを決定します。 *p2p_continue_onconflict*は**nvarchar (5)** 既定値は FALSE です。  
  
> [!CAUTION]  
>  既定値の FALSE を使用することをお勧めします。 このオプションが TRUE に設定されている場合、ディストリビューションエージェントは、発信元 ID が最も大きいノードから競合する行を適用してトポロジ内のデータを収束しようとします。 この方法では、収束は保証されません。 競合が検出された後、トポロジが一貫していることを確認する必要があります。 詳細については、「 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)」の「競合の処理」を参照してください。  
  
  
`[ \@allow_partition_switch = ] 'allow_partition_switch'`ALTER TABLE...パブリッシュされたデータベースに対して SWITCH ステートメントを実行できます。 *allow_partition_switch*は**nvarchar (5)** 既定値は FALSE です。 詳細については、「[パーティション テーブルとパーティション インデックスのレプリケート](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)」を参照してください。  
  
`[ \@replicate_partition_switch = ] 'replicate_partition_switch'`ALTER TABLE...パブリッシュされたデータベースに対して実行される SWITCH ステートメントは、サブスクライバーにレプリケートする必要があります。 *replicate_partition_switch*は**nvarchar (5)** 既定値は FALSE です。 このオプションは、 *allow_partition_switch*が TRUE に設定されている場合にのみ有効です。  

## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_addpublication**は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
 同じデータベースオブジェクトをパブリッシュする複数のパブリケーションが存在する場合、 *replicate_ddl*値が**1**のパブリケーションだけが ALTER TABLE、ALTER VIEW、ALTER PROCEDURE、ALTER FUNCTION、および alter TRIGGER ddl ステートメントをレプリケートします。 ただし、ALTER TABLE DROP COLUMN DDL ステートメントは、削除された列をパブリッシュしているすべてのパブリケーションによってレプリケートされます。  
  
 パブリケーションに対して ddl レプリケーションが有効になっている場合 (*replicate_ddl* = **1**)、パブリケーションに対してレプリケートされていない ddl 変更を行うには、最初に[sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)を実行して*replicate_ddl*をに**設定する必要があります。0**。 レプリケートされていない DDL ステートメントが発行されると、 [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)を再度実行して ddl レプリケーションを有効に戻すことができます。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-transa_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addpublication**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。 Windows 認証ログインを行うには、Windows ユーザー アカウントを表すユーザー アカウントがデータベースに必要です。 Windows グループを表すユーザーアカウントでは不十分です。  
  
## <a name="see-also"></a>関連項目  
 [sp_addlogreader_agent &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [sp_addpublication_snapshot &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droppublication &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [sp_replicationdboption &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [データとデータベース オブジェクトのパブリッシュ](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
