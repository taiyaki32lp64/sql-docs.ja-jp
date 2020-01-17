---
title: sp_changepublication (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changepublication
- sp_changepublication_TSQL
helpviewer_keywords:
- sp_changepublication
ms.assetid: c36e5865-25d5-42b7-b045-dc5036225081
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1e5b128a38fc32b16cca9d0a8e59f09aef88676c
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68762424"
---
# <a name="spchangepublication-transact-sql"></a>sp_changepublication (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  パブリケーションのプロパティを変更します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_changepublication [ [ @publication = ] 'publication' ]  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *publication*は**sysname**,、既定値は NULL です。  
  
`[ @property = ] 'property'`変更するパブリケーションプロパティを設定します。 *プロパティ*は**nvarchar (255)** です。  
  
`[ @value = ] 'value'`新しいプロパティ値を指定します。 *値*は**nvarchar (255)** ,、既定値は NULL です。  
  
 次の表に、変更可能なパブリケーションのプロパティと、プロパティの値に関する制限を示します。  
  
|プロパティ|値|説明|  
|--------------|-----------|-----------------|  
|**allow_anonymous**|**true**|指定されたパブリケーションに対して匿名サブスクリプションを作成できます。また、 *immediate_sync*も**true**である必要があります。 ピアツーピアパブリケーションの場合は変更できません。|  
||**false**|指定されたパブリケーションに対して匿名サブスクリプションを作成することはできません。 ピアツーピアパブリケーションの場合は変更できません。|  
|**allow_initialize_from_backup**|**true**|サブスクライバーでは、初期スナップショットではなくバックアップから、このパブリケーションへのサブスクリプションを初期化できます。 このプロパティは、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
||**false**|サブスクライバーは初期スナップショットを使用する必要があります。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
|**allow_partition_switch**|**true**|テーブルの変更...パブリッシュされたデータベースに対して SWITCH ステートメントを実行できます。 詳細については、「[パーティション テーブルとパーティション インデックスのレプリケート](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)」を参照してください。|  
||**false**|テーブルの変更...パブリッシュされたデータベースに対して SWITCH ステートメントを実行することはできません。|  
|**allow_pull**|**true**|指定されたパブリケーションでは、プルサブスクリプションが許可されます。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
||**false**|指定したパブリケーションに対してプル サブスクリプションを許可しません。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
|**allow_push**|**true**|指定したパブリケーションに対してプッシュ サブスクリプションを許可します。|  
||**false**|指定したパブリケーションに対してプッシュ サブスクリプションを許可しません。|  
|**allow_subscription_copy**|**true**|このパブリケーションをサブスクライブするデータベースをコピーする機能を有効にします。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
||**false**|このパブリケーションにサブスクライブするデータベースをコピーできないようにします。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
|**alt_snapshot_folder**||スナップショットの代替フォルダーの場所。|  
|**centralized_conflicts**|**true**|競合レコードはパブリッシャーに格納されます。 アクティブなサブスクリプションがない場合にのみ変更できます。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
||**false**|競合レコードは、競合の原因となったパブリッシャーとサブスクライバーの両方に保存されます。 アクティブなサブスクリプションがない場合にのみ変更できます。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
|**compress_snapshot**|**true**|代替スナップショット フォルダーにあるスナップショットは .cab ファイル形式に圧縮されます。 既定のスナップショットフォルダー内のスナップショットは圧縮できません。|  
||**false**|スナップショットは圧縮されません。これはレプリケーションの既定の動作です。|  
|**conflict_policy**|**pub wins**|パブリッシャーが競合で優先される場合に、サブスクライバーの更新で競合を解決する方法です。 このプロパティは、アクティブなサブスクリプションがない場合にのみ変更できます。 Oracle パブリッシャーではサポートされていません。|  
||**サブ reinit**|サブスクライバーの更新で競合が発生した場合は、サブスクリプションを再初期化する必要があります。 このプロパティは、アクティブなサブスクリプションがない場合にのみ変更できます。 Oracle パブリッシャーではサポートされていません。|  
||**サブ wins**|サブスクライバーが競合で優先される場合に、サブスクライバーの更新で競合を解決する方法です。 このプロパティは、アクティブなサブスクリプションがない場合にのみ変更できます。 Oracle パブリッシャーではサポートされていません。|  
|**conflict_retention**||競合の保有期間を日数で指定する**int**です。 既定の保有期間は14日です。 **0**は、競合のクリーンアップが必要ないことを意味します。 Oracle パブリッシャーではサポートされていません。|  
|**description**||パブリケーションを説明する省略可能なエントリです。|  
|**enabled_for_het_sub**|**true**|パブリケーションで以外の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サブスクライバーをサポートできるようにします。 パブリケーションへのサブスクリプションが存在する場合、 **enabled_for_het_sub**を変更することはできません。 **Enabled_for_het_sub**を true に設定する前に、次の要件に準拠するために、[レプリケーションストアドプロシージャ (transact-sql)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)の実行が必要になる場合があります。<br /> - **allow_queued_tran**は**false**である必要があります。<br /> - **allow_sync_tran**は**false**である必要があります。<br /> **Enabled_for_het_sub**を**true**に変更すると、既存のパブリケーション設定が変更される可能性があります。 詳細については、「 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)」を参照してください。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
||**false**|パブリケーションは、以外の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サブスクライバーをサポートしていません。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
|**enabled_for_internet**|**true**|パブリケーションはインターネットに対して有効であり、ファイル転送プロトコル (FTP) を使用して、スナップショットファイルをサブスクライバーに転送できます。 パブリケーションの同期ファイルは、次のディレクトリに格納されます。C:\Program Files\Microsoft SQL Server\MSSQL\Repldata\ftp. *ftp_address*を NULL にすることはできません。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
||**false**|パブリケーションはインターネットに対応していません。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
|**enabled_for_p2p**|**true**|パブリケーションは、ピアツーピアレプリケーションをサポートしています。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。<br /> **Enabled_for_p2p**を**true**に設定するには、次の制限が適用されます。<br /> - **allow_anonymous**は**false**である必要があります<br /> - **allow_dts**は**false**である必要があります。<br /> - **allow_initialize_from_backup**は**true**である必要があります<br /> - **allow_queued_tran**は**false**である必要があります。<br /> - **allow_sync_tran**は**false**である必要があります。<br /> - **enabled_for_het_sub**は**false**である必要があります。<br /> - **independent_agent**は**true**である必要があります。<br /> - **repl_freq**は**連続**している必要があります。<br /> - **replicate_ddl**は**1**である必要があります。|  
||**false**|パブリケーションでピア ツー ピア レプリケーションがサポートされません。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
|**ftp_address**||パブリケーションスナップショットファイルの FTP アクセス可能な場所です。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
|**ftp_login**||FTP サービスへの接続に使用するユーザー名です。値 ANONYMOUS は許可されます。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
|**ftp_password**||FTP サービスへの接続に使用するユーザー名のパスワード。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
|**ftp_port**||ディストリビューター用 FTP サービスのポート番号。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
|**ftp_subdirectory**||パブリケーションが FTP を使用したスナップショットの配布をサポートしている場合にスナップショットファイルを作成する場所を指定します。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
|**immediate_sync**|**true**|スナップショットエージェントを実行するたびに、パブリケーションの同期ファイルが作成または再作成されます。 サブスクリプションの前にスナップショットエージェントが完了している場合、サブスクライバーはサブスクリプションの直後に同期ファイルを受け取ることができます。 新しいサブスクリプションは、最近実行されたスナップショット エージェントによって生成された最新の同期ファイルを取得します。 *independent_agent*も**true**である必要があります。 **Immediate_sync**の詳細については、以下の解説を参照してください。|  
||**false**|同期ファイルは、新しいサブスクリプションがある場合にのみ作成されます。 スナップショットエージェントが開始されて完了するまで、サブスクライバーはサブスクリプションの後に同期ファイルを受け取ることができません。|  
|**independent_agent**|**true**|パブリケーションに専用のディストリビューション エージェントがあります。|  
||**false**|パブリケーションでは共有ディストリビューション エージェントが使用されます。パブリケーションおよびサブスクリプション データベースの各ペアには 1 つの共有エージェントがあります。|  
|**p2p_continue_onconflict**|**true**|競合が検出された場合、ディストリビューションエージェントは引き続き変更を処理します。<br /> **注意:** の`FALSE`既定値を使用することをお勧めします。 このオプションがに`TRUE`設定されている場合、ディストリビューションエージェントは、発信元 ID が最も大きいノードから競合する行を適用して、トポロジ内のデータを収束しようとします。 この方法では、収束は保証されません。 競合が検出された後、トポロジが一貫していることを確認する必要があります。 詳細については、「 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)」の「競合の処理」を参照してください。|  
||**false**|ディストリビューションエージェントは、競合が検出された場合に、変更の処理を停止します。|  
|**post_snapshot_script**||ディストリビューション エージェントで実行される [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト ファイルの場所を指定します。このスクリプトの実行は、初期同期で、レプリケートされたすべてのオブジェクト スクリプトとデータが適用された後で行われます。|  
|**pre_snapshot_script**||ディストリビューション エージェントで実行される [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト ファイルの場所を指定します。このスクリプトの実行は、初期同期で、レプリケートされたすべてのオブジェクト スクリプトとデータが適用される前に行われます。|  
|**publish_to_ActiveDirectory**|**true**|このパラメーターは、旧バージョンのスクリプトとの互換性を保つために用意されており、非推奨とされます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory にパブリケーション情報を追加できなくなりました。|  
||**false**|Active Directory からパブリケーション情報を削除します。|  
|**queue_type**|**sql**|トランザクション[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を格納するために使用します。 このプロパティは、アクティブなサブスクリプションがない場合にのみ変更できます。<br /><br /> 注:[!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing (MSMQ) の使用は現在サポートされていません。 *値*に**msmq**の値を指定すると、エラーが発生します。|  
|**repl_freq**|**連続**|ログ ベースのすべてのトランザクションの出力をパブリッシュします。|  
||**ショット**|スケジュールされた同期イベントのみをパブリッシュします。|  
|**replicate_ddl**|**1**|パブリッシャーで実行されるデータ定義言語 (DDL) ステートメントはレプリケートされます。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。|  
||**0**|DDL ステートメントはレプリケートされません。 このプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のパブリケーションに対しては変更できません。 スキーマ変更のレプリケーションは、ピア ツー ピア レプリケーションを使用する場合は無効にできません。|  
|**replicate_partition_switch**|**true**|テーブルの変更...パブリッシュされたデータベースに対して実行される SWITCH ステートメントは、サブスクライバーにレプリケートする必要があります。 このオプションは、 *allow_partition_switch*が TRUE に設定されている場合にのみ有効です。 詳細については、「[パーティション テーブルとパーティション インデックスのレプリケート](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)」を参照してください。|  
||**false**|テーブルの変更...SWITCH ステートメントをサブスクライバーにレプリケートすることはできません。|  
|**保有**||サブスクリプションアクティビティの保有期間を時間単位で表す**int**です。 保有期間内にサブスクリプションがアクティブでない場合は、削除されます。|  
|**snapshot_in_defaultfolder**|**true**|スナップショットファイルは、既定のスナップショットフォルダーに格納されます。 *Alt_snapshot_folder*も指定した場合、スナップショットファイルは既定の場所と代替の場所の両方に格納されます。|  
||**false**|スナップショットファイルは、 *alt_snapshot_folder*によって指定された別の場所に格納されます。|  
|**status**|**能動的**|パブリケーション データはパブリケーションが作成された直後にサブスクライバーで使用できます。 Oracle パブリッシャーではサポートされていません。|  
||**稼動**|パブリケーションデータは、パブリケーションの作成時にサブスクライバーで使用することはできません。 Oracle パブリッシャーではサポートされていません。|  
|**sync_method**|**native**|サブスクリプションの同期時に、すべてのテーブルのネイティブ モード一括コピー出力を使用します。|  
||**character**|サブスクリプションを同期するときに、すべてのテーブルのキャラクターモードの一括コピー出力を使用します。|  
||**同時**|すべてのテーブルについてネイティブ モード BCP 出力を使用しますが、スナップショット生成処理中にテーブルをロックしません。 スナップショットレプリケーションでは無効です。|  
||**concurrent_c**|すべてのテーブルについてキャラクター モード BCP 出力を使用しますが、スナップショット生成処理中にテーブルをロックしません。 スナップショットレプリケーションでは無効です。|  
|**taskid**||このプロパティは非推奨とされており、サポートされなくなりました。|  
|**allow_drop**|**true**|トランザクション`DROP TABLE`レプリケーションに含まれるアーティクルの DLL サポートを有効にします。 サポートされる最小バージョン:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]Service pack 2 以上、 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] service pack 1 以上。 その他の参照:[KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactional-replication-in-sql-server-2014-or-in-sql-server-2016-sp1)|
||**false**|トランザクション`DROP TABLE`レプリケーションに含まれるアーティクルの DLL サポートを無効にします。 これは、このプロパティの**既定**値です。|
|**NULL**標準||*プロパティ*に対してサポートされている値の一覧を返します。|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`このストアドプロシージャによって実行される操作によって既存のスナップショットが無効になる可能性があることを確認します。 *force_invalidate_snapshot*は**ビット**,、既定値は**0**です。  
  - **0**を指定すると、アーティクルへの変更によってスナップショットが無効になることはありません。 変更に新しいスナップショットが必要であることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。  
  - **1**に設定すると、アーティクルへの変更によってスナップショットが無効になることがあります。 新しいスナップショットを必要とする既存のサブスクリプションがある場合、この値によって、既存のスナップショットが古いバージョンとしてマークされ、新しいスナップショットが生成されます。   
変更時に新しいスナップショットの生成が必要になるプロパティについては、「解説」を参照してください。  
  
**[@force_reinit_subscription =** ] *force_reinit_subscription*  
 このストアドプロシージャによって実行されるアクションで、既存のサブスクリプションの再初期化が必要になる可能性があることを確認します。 *force_reinit_subscription*は**ビット**で、既定値は**0**です。  
  - **0**に設定すると、アーティクルへの変更によってサブスクリプションが再初期化されることはありません。 変更によって既存のサブスクリプションが再初期化される必要があることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。  
  - **1**に設定すると、アーティクルへの変更によって既存のサブスクリプションが再初期化され、サブスクリプションの再初期化が許可されます。  
  
`[ @publisher = ] 'publisher'`以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーを指定します。 *publisher*は**sysname**で、既定値は NULL です。  
  
  > [!NOTE]  
  >  パブリッシャーでアーティクルの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]プロパティを変更する場合は、パブリッシャーを使用しないでください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_changepublication**は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
 次のいずれかのプロパティを変更した後で、新しいスナップショットを生成する必要があります。また、 *force_invalidate_snapshot*パラメーターに値**1**を指定する必要があります。  
-   **alt_snapshot_folder**  
-   **compress_snapshot**  
-   **enabled_for_het_sub**  
-   **ftp_address**  
-   **ftp_login**  
-   **ftp_password**  
-   **ftp_port**  
-   **ftp_subdirectory**  
-   **post_snapshot_script**  
-   **pre_snapshot_script**  
-   **snapshot_in_defaultfolder**  
-   **sync_mode**  
  
**Publish_to_active_directory**パラメーター [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を使用して Active Directory 内のパブリケーションオブジェクトを一覧表示するには、Active Directory にオブジェクトが既に作成されている必要があります。  
  
## <a name="impact-of-immediate-sync"></a>即時同期の影響  
 即時同期をオンにすると、サブスクリプションがない場合でも、初期スナップショットが生成された直後にログ内のすべての変更が追跡されます。 ログに記録された変更は、顧客がバックアップを使用して新しいピアノードを追加しているときに使用されます。 バックアップが復元されると、そのピアは、バックアップの作成後に発生した他の変更と同期されます。 コマンドはディストリビューションデータベースで追跡されるため、同期ロジックは最後にバックアップされた LSN を確認し、これを開始点として使用します。これは、バックアップが最大保有期間内に作成された場合にコマンドが使用可能であることを把握するためのものです。 (最小保有期間の既定値は0時間で、最大保有期間は24時間です)。  
  
 即時同期がオフの場合、変更は少なくとも最小の保有期間に保持され、既にレプリケートされているすべてのトランザクションに対してすぐにクリーンアップされます。 即時同期が無効で、既定の保有期間で構成される場合、バックアップの作成後に必要な変更がクリーンアップされたため、新しいピア ノードが正しく初期化されない可能性があります。 残された唯一のオプションがトポロジの停止です。 即時同期を有効に設定すると、柔軟性が向上するため、これは P2P アプリケーションにお勧めの設定です。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_changepublication](../../relational-databases/replication/codesnippet/tsql/sp-changepublication-tra_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_changepublication**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [パブリケーション プロパティの表示および変更](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [パブリケーションとアーティクルのプロパティの変更](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addpublication &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_droppublication &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
