---
title: sp_addmergepullsubscription_agent (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepullsubscription_agent
- sp_addmergepullsubscription_agent_TSQL
helpviewer_keywords:
- sp_addmergepullsubscription_agent
ms.assetid: a2f4b086-078d-49b5-8971-8a1e3f6a6feb
author: stevestein
ms.author: sstein
ms.openlocfilehash: f8073fcb4c92861ffb09da8739c7c9f8064d9d70
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769146"
---
# <a name="sp_addmergepullsubscription_agent-transact-sql"></a>sp_addmergepullsubscription_agent (Transact-SQL)

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  マージ パブリケーションに対するプル サブスクリプションの同期化をスケジュールするための、新しいエージェント ジョブを追加します。 このストアドプロシージャは、サブスクライバー側のサブスクリプションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addmergepullsubscription_agent [ [ @name = ] 'name' ]   
        , [ @publisher = ] 'publisher'   
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication =] 'publication'   
    [ , [ @publisher_security_mod e= ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @publisher_encrypted_password = ] publisher_encrypted_password ]   
    [ , [ @subscriber = ] 'subscriber' ]   
    [ , [ @subscriber_db = ] 'subscriber_db' ]   
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]   
    [ , [ @subscriber_login = ] 'subscriber_login' ]   
    [ , [ @subscriber_password= ] 'subscriber_password' ]   
    [ , [ @distributor = ] 'distributor' ]   
    [ , [ @distributor_security_mode = ] distributor_security_mode ]   
    [ , [ @distributor_login = ] 'distributor_login' ]   
    [ , [ @distributor_password = ] 'distributor_password' ]   
    [ , [ @encrypted_password = ] encrypted_password ]   
    [ , [ @frequency_type = ] frequency_type ]   
    [ , [ @frequency_interval = ] frequency_interval ]   
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]   
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]   
    [ , [ @frequency_subday = ] frequency_subday ]   
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]   
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]   
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @optional_command_line = ] 'optional_command_line' ]   
    [ , [ @merge_jobid = ] merge_jobid ]   
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]   
    [ , [ @ftp_address = ] 'ftp_address' ]   
    [ , [ @ftp_port = ] ftp_port ]   
    [ , [ @ftp_login = ] 'ftp_login' ]   
    [ , [ @ftp_password = ] 'ftp_password' ]    
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]   
    [ , [ @working_directory = ] 'working_directory' ]   
    [ , [ @use_ftp = ] 'use_ftp' ]   
    [ , [ @reserved = ] 'reserved' ]   
    [ , [ @use_interactive_resolver = ] 'use_interactive_resolver' ]   
    [ , [ @offloadagent = ] 'remote_agent_activation' ]   
    [ , [ @offloadserver = ] 'remote_agent_server_name']   
    [ , [ @job_name = ] 'job_name' ]   
    [ , [ @dynamic_snapshot_location = ] 'dynamic_snapshot_location' ]  
    [ , [ @use_web_sync = ] use_web_sync ]  
        [ , [ @internet_url = ] 'internet_url' ]  
    [ , [ @internet_login = ] 'internet_login' ]  
        [ , [ @internet_password = ] 'internet_password' ]  
    [ , [ @internet_security_mode = ] internet_security_mode ]  
        [ , [ @internet_timeout = ] internet_timeout ]  
    [ , [ @hostname = ] 'hostname' ]  
        [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @name = ] 'name'`エージェントの名前を指定します。 *名前* は **sysname** 、既定値は NULL です。  
  
`[ @publisher = ] 'publisher'`パブリッシャーサーバーの名前を指定します。 *パブリッシャー* は **sysname** 、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'`パブリッシャーデータベースの名前を指定します。 *publisher_db* は **sysname** 、既定値はありません。  
  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @publisher_security_mode = ] publisher_security_mode`同期時にパブリッシャーに接続するときに使用するセキュリティモードを示します。 *publisher_security_mode*は**int**,、既定値は1です。 **0**の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証を指定します。 **1**の場合、Windows 認証を指定します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'`同期時にパブリッシャーに接続するときに使用するログインを示します。 *publisher_login* は **sysname** 、既定値は NULL です。  
  
`[ @publisher_password = ] 'publisher_password'`パブリッシャーに接続するときに使用するパスワードを入力します。 *publisher_password* は **sysname** 、既定値は NULL です。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
`[ @publisher_encrypted_password = ]publisher_encrypted_password`*Publisher_encrypted_password*の設定はサポートされなくなりました。 この**ビット**パラメーターを**1**に設定しようとすると、エラーが発生します。  
  
`[ @subscriber = ] 'subscriber'`サブスクライバーの名前を指定します。 *サブスクライバー* は **sysname** 、既定値は NULL です。  
  
`[ @subscriber_db = ] 'subscriber_db'`サブスクリプションデータベースの名前を指定します。 *subscriber_db* は **sysname** 、既定値は NULL です。  
  
`[ @subscriber_security_mode = ] subscriber_security_mode`同期時にサブスクライバーに接続するときに使用するセキュリティモードを示します。 *subscriber_security_mode*は**int**,、既定値は1です。 **0**の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証を指定します。 **1**の場合、Windows 認証を指定します。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 マージエージェントは、常に Windows 認証を使用してローカルサブスクライバーに接続します。 このパラメーターに値が指定されている場合は、警告メッセージが返されますが、値は無視されます。  
  
`[ @subscriber_login = ] 'subscriber_login'`サブスクライバーに接続して同期するときに使用するサブスクライバーログインを示します。 *subscriber_login* 場合は必須です *subscriber_security_mode* に設定されている **0** します。 *subscriber_login* は **sysname** 、既定値は NULL です。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このパラメーターに値が指定されている場合は、警告メッセージが返されますが、値は無視されます。  
  
`[ @subscriber_password = ] 'subscriber_password'`認証用の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サブスクライバーパスワードを入力します。 *subscriber_password* 場合は必須です *subscriber_security_mode* に設定されている **0** します。 *\@subscriber_password* は **sysname** 、既定値は NULL です。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このパラメーターに値が指定されている場合は、警告メッセージが返されますが、値は無視されます。  
  
`[ @distributor = ] 'distributor'`ディストリビューターの名前を指定します。 *ディストリビューター* は **sysname** 、既定値は *パブリッシャー*; は、パブリッシャーがディストリビューターでも。  
  
`[ @distributor_security_mode = ] distributor_security_mode`は、同期時にディストリビューターに接続するときに使用するセキュリティモードです。 *distributor_security_mode*は**int**,、既定値は0です。 **0**は[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証を指定します。 **1** Windows 認証を指定します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @distributor_login = ] 'distributor_login'`ディストリビューターへの接続時に、同期時に使用するディストリビューターログインを示します。 *distributor_login* 場合は必須です *distributor_security_mode* に設定されている **0** します。 *distributor_login* は **sysname** 、既定値は NULL です。  
  
`[ @distributor_password = ] 'distributor_password'`ディストリビューターパスワードを入力します。 *distributor_password* 場合は必須です *distributor_security_mode* に設定されている **0** します。 *distributor_password* は **sysname** 、既定値は NULL です。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
`[ @encrypted_password = ] encrypted_password`*Encrypted_password*の設定はサポートされなくなりました。 この**ビット**パラメーターを**1**に設定しようとすると、エラーが発生します。  
  
`[ @frequency_type = ] frequency_type`マージエージェントをスケジュールする頻度を指定します。 *frequency_type*は**int**,、値は次のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|指定日時|  
|**2**|[要求時]|  
|**4**|毎日。|  
|**8**|毎週。|  
|**16**|毎月。|  
|**32**|月単位の相対|  
|**64**|自動開始|  
|**128**|定期|  
|NULL (既定値)||  
  
> [!NOTE]  
>  値**64**を指定すると、マージエージェントが連続モードで実行されます。 これは、エージェントの **-Continuous**パラメーターの設定に対応しています。 詳細については、「 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)」を参照してください。  
  
`[ @frequency_interval = ] frequency_interval`マージエージェントが実行される日または日。 *frequency_interval*は**int**,、これらの値のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|日曜日|  
|**2**|月曜日|  
|**3**|火曜日|  
|**4**|水曜日|  
|**5**|木曜日|  
|**6**|金曜日|  
|**7**|土曜日|  
|**8**|Day|  
|**9**|平日|  
|"**10**"|週末|  
|NULL (既定値)||  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`マージエージェントの日付を指定します。 このパラメーターが使用されるときに *frequency_type* に設定されている **32** (月単位)。 *frequency_relative_interval*は**int**,、これらの値のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|First|  
|**2**|第 2 週|  
|**4**|サードパーティ|  
|**8**|4 番目|  
|**16**|Last|  
|NULL (既定値)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*によって使用される定期実行係数を示します。 *frequency_recurrence_factor*は**int**,、既定値は NULL です。  
  
`[ @frequency_subday = ] frequency_subday`定義した期間中に再スケジュールする頻度を指定します。 *frequency_subday*は**int**,、これらの値のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|1 回。|  
|**2**|第 2 週|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (既定値)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*の間隔を指定します。 *frequency_subday_interval*は**int**,、既定値は NULL です。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`マージエージェントを最初にスケジュール設定する時刻を HHMMSS 形式で指定します。 *active_start_time_of_day* は **int** 、既定値は NULL です。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`マージエージェントのスケジュール設定を停止する時刻を HHMMSS 形式で指定します。 *active_end_time_of_day*は**int**,、既定値は NULL です。  
  
`[ @active_start_date = ] active_start_date`マージエージェントを最初にスケジュール設定する日付を YYYYMMDD 形式で指定します。 *active_start_date*は**int**,、既定値は NULL です。  
  
`[ @active_end_date = ] active_end_date`マージエージェントのスケジュール設定を停止する日付を YYYYMMDD 形式で指定します。 *active_end_date*は**int**,、既定値は NULL です。  
  
`[ @optional_command_line = ] 'optional_command_line'`は省略可能なコマンドプロンプトであり、マージエージェントに提供されます。 *optional_command_line*は**nvarchar (255)** ,、既定値は ' ' です。 追加のパラメーターをマージ エージェントに提供する場合に使用できます。たとえば、次の例では、既定のクエリ タイムアウトを `600` 秒に増やします。  
  
```  
@optional_command_line = N'-QueryTimeOut 600'  
```  
  
`[ @merge_jobid = ] merge_jobid`ジョブ ID の出力パラメーターを指定します。 *merge_jobid*は**binary (16)** ,、既定値は NULL です。  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'`Windows 同期マネージャーを使用してサブスクリプションを同期できるかどうかを指定します。 *enabled_for_syncmgr*は**nvarchar (5)** ,、既定値は FALSE。 **False**の場合、サブスクリプションは同期マネージャーに登録されていません。 **True**の場合、サブスクリプションは同期マネージャーに登録され、を起動[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]せずに同期できます。  
  
`[ @ftp_address = ] 'ftp_address'`旧バージョンとの互換性のためにのみ使用します。  
  
`[ @ftp_port = ] ftp_port`旧バージョンとの互換性のためにのみ使用します。  
  
`[ @ftp_login = ] 'ftp_login'`旧バージョンとの互換性のためにのみ使用します。  
  
`[ @ftp_password = ] 'ftp_password'`旧バージョンとの互換性のためにのみ使用します。  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'`スナップショットファイルを取得する場所を指定します。 *alternate_snapshot_folder*は**nvarchar (255)** ,、既定値は NULL です。 NULL の場合、スナップショットファイルはパブリッシャーによって指定された既定の場所から取得されます。  
  
`[ @working_directory = ] 'working_directory'`FTP を使用してスナップショットファイルを転送するときに、パブリケーションのデータファイルとスキーマファイルを一時的に保存するために使用する作業ディレクトリの名前を指定します。 *working_directory*は**nvarchar (255)** ,、既定値は NULL です。  
  
`[ @use_ftp = ] 'use_ftp'`スナップショットを取得するための一般的なプロトコルではなく、FTP の使用を指定します。 *\@use_ftp* は **nvarchar (5)** 、既定値は FALSE。  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @use_interactive_resolver = ] 'use_interactive_resolver' ]`インタラクティブ競合回避モジュールを使用して、対話的な解決を可能にするすべてのアーティクルの競合を解決します。 *use_interactive_resolver* は **nvarchar (5)** 、既定値は FALSE。  
  
`[ @offloadagent = ] 'remote_agent_activation'`
 > [!NOTE]  
>  リモートエージェントのアクティブ化は非推奨とされており、サポートされなくなりました。 このパラメーターは、スクリプトの旧バージョンとの互換性を維持するためにのみサポートされています。 *Remote_agent_activation*を**false**以外の値に設定すると、エラーが発生します。  
  
`[ @offloadserver = ] 'remote_agent_server_name'`
 > [!NOTE]  
>  リモートエージェントのアクティブ化は非推奨とされており、サポートされなくなりました。 このパラメーターは、スクリプトの旧バージョンとの互換性を維持するためにのみサポートされています。 *Remote_agent_server_name*を NULL 以外の値に設定すると、エラーが発生します。  
  
`[ @job_name = ] 'job_name' ]`既存のエージェントジョブの名前を指定します。 *job_name* は **sysname** 既定値は NULL です。 このパラメーターは、新しく作成されたジョブ (既定値) ではなく、既存のジョブを使用してサブスクリプションを同期する場合にのみ指定します。 **Sysadmin**固定サーバーロールのメンバーでない場合は、 *job_name*を指定するときに、 *job_login*と*job_password*を指定する必要があります。  
  
`[ @dynamic_snapshot_location = ] 'dynamic_snapshot_location' ]`フィルター選択されたデータスナップショットが使用される場合に、スナップショットファイルの読み取り元となるフォルダーのパス。 *dynamic_snapshot_location*は**nvarchar (260)** ,、既定値は NULL です。 詳しくは、「 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」をご覧ください。  
  
`[ @use_web_sync = ] use_web_sync`Web 同期が有効になっていることを示します。 *use_web_sync*は**ビット**,、既定値は0です。 **1**は、HTTP を使用してインターネット経由でプルサブスクリプションを同期できることを指定します。  
  
`[ @internet_url = ] 'internet_url'`レプリケーションリスナーの場所を指定します (REPLISAPI.DLL) を使用します。 *internet_url*は**nvarchar (260)** ,、既定値は NULL です。 *internet_url*は、という形式`http://server.domain.com/directory/replisapi.dll`の完全修飾 url です。 サーバーの構成で、リッスンするポートがポート 80 以外の場合は、`http://server.domain.com:portnumber/directory/replisapi.dll` の形式のポート番号も指定する必要があります。ここで `portnumber` はポートを表します。  
  
`[ @internet_login = ] 'internet_login'`HTTP 基本認証を使用して Web 同期をホストしている Web サーバーに接続するときにマージエージェントが使用するログインを示します。 *internet_login* は **sysname** 、既定値は NULL です。  
  
`[ @internet_password = ] 'internet_password'`は、HTTP 基本認証を使用して Web 同期をホストしている Web サーバーに接続するときにマージエージェントが使用するパスワードです。 *internet_password*は**nvarchar (524)** ,、既定の値は NULL です。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
`[ @internet_security_mode = ] internet_security_mode`は、HTTPS を使用した Web 同期時に Web サーバーに接続するときにマージエージェントによって使用される認証方法です。 *internet_security_mode*は**int**で、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**0**|基本認証が使用されます。|  
|**1** (既定値)|Windows 統合認証を使用|  
  
> [!NOTE]  
>  Web 同期で基本認証を使用することをお勧めします。 Web 認証を使用するには、Web サーバーに SSL で接続する必要があります。 詳しくは、「 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)」をご覧ください。  
  
`[ @internet_timeout = ] internet_timeout`Web 同期要求の有効期限が切れるまでの時間を秒単位で示します。 *internet_timeout*は**int**,、既定値は**300**秒です。  
  
`[ @hostname = ] 'hostname'`パラメーター化されたフィルターの WHERE 句でこの関数を使用する場合は、HOST_NAME () の値をオーバーライドします。 *ホスト名* は **sysname** 、既定値は NULL です。  
  
`[ @job_login = ] 'job_login'`エージェントを実行する Windows アカウントのログインを指定します。 *job_login*は**nvarchar (257)** ,、既定値はありません。 この Windows アカウントは、Windows 統合認証を使用する場合に、サブスクライバーへのエージェント接続、およびディストリビューターとパブリッシャーへの接続に常に使用されます。  
  
`[ @job_password = ] 'job_password'`エージェントを実行する Windows アカウントのパスワードを指定します。 *job_password* は **sysname** 、既定値はありません。  
  
> [!IMPORTANT]  
>  認証情報をスクリプトファイルに保存しないでください。 セキュリティを最大限に高めるには、ログイン名とパスワードを実行時に指定する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_addmergepullsubscription_agent**は、マージレプリケーションで使用され、 [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)と同様の機能を使用します。  
  
 正しく実行するときにセキュリティ設定を指定する方法の例については**sp_addmergepullsubscription_agent**を参照してください[プル サブスクリプションの作成](../../relational-databases/replication/create-a-pull-subscription.md)します。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_1_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addmergepullsubscription_agent**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [プル サブスクリプションの作成](../../relational-databases/replication/create-a-pull-subscription.md)   
 [パブリケーションのサブスクライブ](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
