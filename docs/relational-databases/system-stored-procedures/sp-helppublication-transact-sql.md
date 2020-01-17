---
title: sp_helppublication (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppublication_TSQL
- sp_helppublication
helpviewer_keywords:
- sp_helppublication
ms.assetid: e801c3f0-dcbd-4b4a-b254-949a05f63518
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1f7f75d37762f5e6df971f3139eea118c6a3fdf2
ms.sourcegitcommit: 82a1ad732fb31d5fa4368c6270185c3f99827c97
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/21/2019
ms.locfileid: "72689046"
---
# <a name="sp_helppublication-transact-sql"></a>sp_helppublication (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  パブリケーションに関する情報を返します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パブリケーションの場合、このストアドプロシージャはパブリッシャー側でパブリケーションデータベースに対して実行されます。 Oracle パブリケーションの場合、このストアド プロシージャは、任意のデータベース上のディストリビューター側で実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helppublication [ [ @publication = ] 'publication' ]  
    [ , [ @found=] found OUTPUT]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` 表示するパブリケーションの名前を指定します。 *publication*のデータ型は sysname で、既定値は **%** です。これにより、すべてのパブリケーションに関する情報が返されます。  
  
`[ @found = ] 'found' OUTPUT` は、行を返すことを示すフラグです。 *見つかった*は**int**と出力パラメーターで、既定値は**23456**です。 **1**は、パブリケーションが見つかったことを示します。 **0**は、パブリケーションが見つからないことを示します。  
  
`[ @publisher = ] 'publisher'` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリッシャーを指定します。 *publisher*は sysname で、既定値は NULL です。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パブリッシャーからのパブリケーション情報を要求するときに、*パブリッシャー*を指定することはできません。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|pubid|**int**|パブリケーションの ID。|  
|name|**sysname**|パブリケーションの名前。|  
|restricted|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|ステータス|**tinyint**|パブリケーションの現在の状態です。<br /><br /> **0** = 非アクティブ。<br /><br /> **1** = アクティブ。|  
|タスク (task)||旧バージョンとの互換性のために用意されています。|  
|レプリケーションの頻度|**tinyint**|レプリケーション周期の種類。<br /><br /> **0** = トランザクション<br /><br /> **1** = スナップショット|  
|同期方法|**tinyint**|同期化モード。<br /><br /> **0** = ネイティブ一括コピープログラム (**bcp**ユーティリティ)<br /><br /> **1** = 文字一括コピー<br /><br /> **3** = 同時実行。ネイティブ一括コピー (**bcp**ユーティリティ) が使用されますが、スナップショットの実行中にテーブルがロックされることはありません。<br /><br /> **4** = Concurrent_c。文字一括コピーが使用されますが、スナップショットの実行中にテーブルがロックされないことを意味します。|  
|description|**nvarchar (255)**|パブリケーションの説明です (省略可)。|  
|immediate_sync|**bit**|スナップショット エージェントを実行するたびに、同期ファイルを作成または再作成するかどうかを示します。|  
|enabled_for_internet|**bit**|ファイル転送プロトコル (FTP) やその他のサービスによって、パブリケーション用の同期ファイルをインターネット上で公開するかどうかを示します。|  
|allow_push|**bit**|パブリケーションに対してプッシュ サブスクリプションを許可するかどうかを示します。|  
|allow_pull|**bit**|パブリケーションでプルサブスクリプションを許可するかどうかを指定します。|  
|allow_anonymous|**bit**|パブリケーションで匿名サブスクリプションが許可されているかどうか。|  
|independent_agent|**bit**|このパブリケーションに対してスタンドアロンのディストリビューションエージェントがあるかどうか。|  
|immediate_sync_ready|**bit**|スナップショット エージェントが、新しいサブスクリプションでそのまま使用できるスナップショットを作成するかどうかを示します。 このパラメーターは、パブリケーションが、新規または再初期化されたサブスクリプションで常にスナップショットを使用できるように設定されている場合にのみ定義されます。|  
|allow_sync_tran|**bit**|パブリケーションで即時更新サブスクリプションが許可されているかどうか。|  
|autogen_sync_procs|**bit**|サブスクリプションの即時更新をサポートするストアド プロシージャを自動的に生成するかどうかを示します。|  
|snapshot_jobid|**binary(16)**|スケジュールされたタスク ID。|  
|retention|**int**|指定されたパブリケーションに対して保存する変更の量 (時間単位)。|  
|has subscription|**bit**|パブリケーションにアクティブなサブスクリプションがあるかどうかを示します。 **1**はパブリケーションにアクティブなサブスクリプションがあることを示し、 **0**はパブリケーションにサブスクリプションがないことを示します。|  
|allow_queued_tran|**bit**|パブリッシャーで適用できるようになるまで、サブスクライバーでの変更のキューを無効にするかどうかを指定します。 **0**の場合、サブスクライバーでの変更はキューに登録されません。|  
|snapshot_in_defaultfolder|**bit**|スナップショットファイルを既定のフォルダーに格納するかどうかを指定します。 **0**の場合、スナップショットファイルは*alternate_snapshot_folder*によって指定された別の場所に格納されています。 **1**の場合、スナップショットファイルは既定のフォルダーにあります。|  
|alt_snapshot_folder|**nvarchar (255)**|スナップショットの代替フォルダーの場所を指定します。|  
|pre_snapshot_script|**nvarchar (255)**|**.Sql**ファイルの場所へのポインターを指定します。 ディストリビューションエージェントは、サブスクライバーでスナップショットを適用するときに、レプリケートされたオブジェクトスクリプトを実行する前に、プリスナップショットスクリプトを実行します。|  
|post_snapshot_script|**nvarchar (255)**|**.Sql**ファイルの場所へのポインターを指定します。 このディストリビューションエージェントでは、すべてのレプリケートされたオブジェクトスクリプトとデータが初期同期中に適用された後に、ポストスナップショットスクリプトが実行されます。|  
|compress_snapshot|**bit**|*Alt_snapshot_folder*の場所に書き込まれるスナップショットを [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 形式に圧縮することを指定します。 **0**を指定すると、スナップショットは圧縮されません。|  
|ftp_address|**sysname**|ディストリビューター用の FTP サービスのネットワークアドレス。 ここでは、サブスクライバーのディストリビューション エージェントまたはマージ エージェントがパブリケーション スナップショット ファイルを取得する場所を指定します。|  
|ftp_port|**int**|ディストリビューターの FTP サービスのポート番号。|  
|ftp_subdirectory|**nvarchar (255)**|パブリケーションで FTP を使用したスナップショットの配布がサポートされている場合に、サブスクライバーのディストリビューションエージェントまたはマージエージェントでスナップショットファイルを取得できる場所を指定します。|  
|ftp_login|**sysname**|FTP サービスへの接続に使用するユーザー名。|  
|allow_dts|**bit**|パブリケーションでデータを変換できるかどうかを指定します。 **0**は、DTS 変換が許可されないことを指定します。|  
|allow_subscription_copy|**bit**|パブリケーションにサブスクライブするサブスクリプション データベースをコピーする機能が有効かどうかを示します。 **0**は、コピーが許可されていないことを示します。|  
|centralized_conflicts|**bit**|競合レコードがパブリッシャーに格納されるかどうかを示します。<br /><br /> **0** = 競合レコードは、競合の原因となったパブリッシャーとサブスクライバーの両方に格納されます。<br /><br /> **1** = 競合レコードはパブリッシャーに格納されます。|  
|conflict_retention|**int**|競合の保有期間を日数で指定します。|  
|conflict_policy|**int**|キュー更新サブスクライバーオプションを使用する場合の競合解決ポリシーを指定します。 次のいずれかの値を指定できます。<br /><br /> **1** = パブリッシャー優先。<br /><br /> **2** = サブスクライバー優先。<br /><br /> **3** = サブスクリプションは再初期化されます。|  
|queue_type||使用されるキューの種類。 次のいずれかの値を指定できます。<br /><br /> **msmq** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] メッセージキューを使用してトランザクションを格納します。<br /><br /> **sql** = トランザクションを格納するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用します。<br /><br /> 注: メッセージキューのサポートは廃止されました。|  
|backward_comp_level||データベースの互換性レベル。次のいずれかの値をとります。<br /><br /> **90** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_AD|**bit**|パブリケーションが [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory にパブリッシュされるかどうかを示します。 値**1**は公開されていることを示し、値**0**は発行されていないことを示します。|  
|allow_initialize_from_backup|**bit**|サブスクライバーでは、最初のスナップショットではなくバックアップから、このパブリケーションへのサブスクリプションを初期化できるかどうかを示します。 **1**は、サブスクリプションをバックアップから初期化できることを意味します。 **0**は、サブスクリプションが使用できないことを意味します。 詳細については、「スナップショットを使用しない[トランザクションサブスクリプションの初期化](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)スナップショットを使用しないトランザクションサブスクライバー」を参照してください。|  
|replicate_ddl|**int**|パブリケーションでスキーマレプリケーションがサポートされているかどうかを示します。 **1**は、パブリッシャーで実行されるデータ定義言語 (DDL) ステートメントがレプリケートされることを示し、 **0**は ddl ステートメントがレプリケートされないことを示します。 詳細については、「[パブリケーション データベースでのスキーマの変更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)」を参照してください。|  
|enabled_for_p2p|**int**|ピア ツー ピア レプリケーション トポロジでパブリケーションを使用できるかどうかを示します。 **1**は、パブリケーションがピアツーピアレプリケーションをサポートしていることを示します。 詳細については、「 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)」を参照してください。|  
|publish_local_changes_only|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|enabled_for_het_sub|**int**|パブリケーションで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーがサポートされるかどうかを示します。 値**1**は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のサブスクライバーがサポートされることを意味します。 値**0**は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のサブスクライバーのみがサポートされることを意味します。 詳細については、「 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)」を参照してください。|  
|enabled_for_p2p_conflictdetection|**int**|ピア ツー ピア レプリケーションが有効になっているパブリケーションでの競合をディストリビューション エージェントが検出するかどうかを指定します。 値**1**は、競合が検出されたことを意味します。 詳細については、「 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)」を参照してください。|  
|originator_id|**int**|ピア ツー ピア トポロジ内のノードの ID を指定します。 **Enabled_for_p2p_conflictdetection**が**1**に設定されている場合、この ID は競合の検出に使用されます。 既に使用されている ID を確認するには、 [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) システム テーブルに対してクエリを実行します。|  
|p2p_continue_onconflict|**int**|競合が検出された場合に、ディストリビューションエージェントが変更の処理を続行するかどうかを指定します。 値**1**は、エージェントが変更を処理し続けることを意味します。<br /><br /> **\*\* 注意 \*\*** 既定値の**0**を使用することをお勧めします。 このオプションが**1**に設定されている場合、ディストリビューションエージェントは、発信元 ID が最も大きいノードから競合する行を適用してトポロジ内のデータを収束しようとします。 この方法では、収束は保証されません。 競合が検出された後、トポロジが一貫していることを確認する必要があります。 詳細については、「 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)」の「競合の処理」を参照してください。|  
|allow_partition_switch|**int**|ALTER TABLE...パブリッシュされたデータベースに対して SWITCH ステートメントを実行できます。 詳細については、「[パーティション テーブルとパーティション インデックスのレプリケート](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)」を参照してください。|  
|replicate_partition_switch|**int**|ALTER TABLE...パブリッシュされたデータベースに対して実行される SWITCH ステートメントは、サブスクライバーにレプリケートする必要があります。 このオプションは、 *allow_partition_switch*が**1**に設定されている場合にのみ有効です。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>Remarks  
 sp_helppublication は、スナップショットおよびトランザクション レプリケーションで使用します。  
  
 sp_helppublication では、このプロシージャを実行するユーザーが所有しているすべてのパブリケーションに関する情報が返されます。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_helppublication](../../relational-databases/replication/codesnippet/tsql/sp-helppublication-trans_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 sp_helppublication を実行できるのは、パブリッシャーの sysadmin 固定サーバー ロールのメンバー、パブリケーション データベースの db_owner 固定データベース ロールのメンバー、またはパブリケーション アクセス リスト (PAL) のユーザーだけです。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリッシャーの場合、sp_helppublication を実行できるのは、ディストリビューター側の固定サーバーロール sysadmin のメンバー、またはディストリビューションデータベースの db_owner 固定データベースロールのメンバー、または PAL のユーザーだけです。  
  
## <a name="see-also"></a>参照  
 [パブリケーション プロパティの表示および変更](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
