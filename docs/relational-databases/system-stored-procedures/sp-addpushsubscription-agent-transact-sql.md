---
title: sp_addpushsubscription_agent (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpushsubscription_agent_TSQL
- sp_addpushsubscription_agent
helpviewer_keywords:
- sp_addpushsubscription_agent
ms.assetid: 1fdd2052-50d8-4318-8aa7-fc635d5cad18
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8073d51fb4376acbdc19724422f6ef7543e3c403
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68894040"
---
# <a name="sp_addpushsubscription_agent-transact-sql"></a>sp_addpushsubscription_agent (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  トランザクション パブリケーションに対してプッシュ サブスクリプションを同期するために使用する、新たにスケジュールされたエージェント ジョブを追加します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
> [!IMPORTANT]  
>  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addpushsubscription_agent [ @publication= ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]  
    [ , [ @subscriber_login = ] 'subscriber_login' ]  
    [ , [ @subscriber_password = ] 'subscriber_password' ]  
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
    [ , [ @job_name = ] 'job_name' ]   
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
    [ , [ @dts_package_name = ] 'dts_package_name' ]  
    [ , [ @dts_package_password = ] 'dts_package_password' ]  
    [ , [ @dts_package_location = ] 'dts_package_location' ]  
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]  
    [ , [ @distribution_job_name = ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @subscriber_provider = ] 'subscriber_provider' ]   
    [ , [ @subscriber_datasrc = ] 'subscriber_datasrc' ]   
    [ , [ @subscriber_location = ] 'subscriber_location' ]  
    [ , [ @subscriber_provider_string = ] 'subscriber_provider_string' ]   
    [ , [ @subscriber_catalog = ] 'subscriber_catalog' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @subscriber = ] 'subscriber'`サブスクライバーインスタンスの名前を指定します。または、サブスクライバーデータベースが可用性グループの場合は、AG リスナーの名前を指定します。 *サブスクライバー* は **sysname** 、既定値は NULL です。 
  
`[ @subscriber_db = ] 'subscriber_db'`サブスクリプションデータベースの名前を指定します。 *subscriber_db* は **sysname** 、既定値は NULL です。 SQL Server 以外のサブスクライバーの場合は、 *subscriber_db*に対して **(既定の転送先)** の値を指定します。  
  
`[ @subscriber_security_mode = ] subscriber_security_mode`同期時にサブスクライバーに接続するときに使用するセキュリティモードを示します。 *subscriber_security_mode*は**int**,、既定値は1です。 **0**は[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証を指定します。 **1** Windows 認証を指定します。  
  
> [!IMPORTANT]  
>  キュー更新サブスクリプションの場合、サブスクライバーへの接続には [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用し、各サブスクライバーへの接続にはそれぞれ異なるアカウントを指定してください。 他のすべてのサブスクリプションでは、Windows 認証を使用します。  
  
`[ @subscriber_login = ] 'subscriber_login'`サブスクライバーに接続して同期するときに使用するサブスクライバーログインを示します。 *subscriber_login* は **sysname** 、既定値は NULL です。  
  
`[ @subscriber_password = ] 'subscriber_password'`サブスクライバーパスワードを入力します。 *subscriber_password* 場合は必須です *subscriber_security_mode* に設定されている **0** します。 *subscriber_password* は **sysname** 、既定値は NULL です。 サブスクライバーパスワードが使用されている場合は、自動的に暗号化されます。  
  
> [!IMPORTANT]  
>  空白のパスワードは使用しないでください。 強力なパスワードを使用してください。 可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
`[ @job_login = ] 'job_login'`エージェントを実行するアカウントのログインを指定します。 Azure SQL Database Managed Instance SQL Server アカウントを使用します。 *job_login*は**nvarchar (257)** ,、既定の値は NULL です。 この Windows アカウントは、エージェントがディストリビューターに接続するとき、および Windows 統合認証を使用してサブスクライバーに接続するときに必ず使用されます。  
  
`[ @job_password = ] 'job_password'`エージェントを実行するアカウントのパスワードを指定します。 *job_password* は **sysname** 、既定値はありません。  
  
> [!IMPORTANT]  
>  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
`[ @job_name = ] 'job_name'`既存のエージェントジョブの名前を指定します。 *job_name* は **sysname** 既定値は NULL です。 このパラメーターは、新しく作成されたジョブ (既定値) ではなく、既存のジョブを使用してサブスクリプションを同期する場合にのみ指定します。 **Sysadmin**固定サーバーロールのメンバーでない場合は、 *job_name*を指定するときに、 *job_login*と*job_password*を指定する必要があります。  
  
`[ @frequency_type = ] frequency_type`ディストリビューションエージェントをスケジュールする頻度を指定します。 *frequency_type*は**int**,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|指定日時|  
|**2**|[要求時]|  
|**4**|毎日。|  
|**8**|毎週。|  
|**16**|毎月。|  
|**32**|月単位の相対|  
|**64** (既定値)|自動開始|  
|**128**|定期|  
  
> [!NOTE]  
>  値**64**を指定すると、ディストリビューションエージェントが連続モードで実行されます。 これは、エージェントの **-Continuous**パラメーターの設定に対応しています。 詳細については、「 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)」を参照してください。  
  
`[ @frequency_interval = ] frequency_interval`*Frequency_type*によって設定された頻度に適用する値を指定します。 *frequency_interval*は**int**,、既定値は1です。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`ディストリビューションエージェントの日付を指定します。 このパラメーターが使用されるときに *frequency_type* に設定されている **32** (月単位)。 *frequency_relative_interval*は**int**,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1** (既定値)|First|  
|**2**|第 2 週|  
|**4**|サードパーティ|  
|**8**|4 番目|  
|**16**|Last|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*によって使用される定期実行係数を示します。 *frequency_recurrence_factor*は**int**,、既定値は0です。  
  
`[ @frequency_subday = ] frequency_subday`定義した期間中に再スケジュールする頻度を指定します。 *frequency_subday*は**int**,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|1 回。|  
|**2**|Second|  
|**4** (既定値)|Minute|  
|**8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*の間隔を指定します。 *frequency_subday_interval*は**int**,、既定値は5です。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`ディストリビューションエージェントを最初にスケジュール設定する時刻を HHMMSS 形式で指定します。 *active_start_time_of_day*は**int**,、既定値は0です。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`ディストリビューションエージェントのスケジュール設定を停止する時刻を HHMMSS 形式で指定します。 *active_end_time_of_day*は**int**,、既定値は235959です。  
  
`[ @active_start_date = ] active_start_date`ディストリビューションエージェントを最初にスケジュール設定する日付を YYYYMMDD 形式で指定します。 *active_start_date*は**int**,、既定値は0です。  
  
`[ @active_end_date = ] active_end_date`ディストリビューションエージェントのスケジュール設定を停止する日付を YYYYMMDD 形式で指定します。 *active_end_date*は**int**,、既定値は99991231です。  
  
`[ @dts_package_name = ] 'dts_package_name'`データ変換サービス (DTS) パッケージの名前を指定します。 *dts_package_name*は**sysname**で、既定値は NULL です。 たとえば、というパッケージ名`DTSPub_Package`を指定する場合、パラメーター `@dts_package_name = N'DTSPub_Package'`はになります。  
  
`[ @dts_package_password = ] 'dts_package_password'`パッケージを実行するために必要なパスワードを指定します。 *dts_package_password*は**sysname**既定値は NULL です。  
  
> [!NOTE]  
>  *Dts_package_name*を指定する場合は、パスワードを指定する必要があります。  
  
`[ @dts_package_location = ] 'dts_package_location'`パッケージの場所を指定します。 *dts_package_location*は**nvarchar (12)** ,、既定値はディストリビューターです。 パッケージの場所には、**ディストリビューター**または**サブスクライバー**を指定できます。  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'`同期マネージャーを使用して[!INCLUDE[msCoName](../../includes/msconame-md.md)]サブスクリプションを同期できるかどうかを指定します。 *enabled_for_syncmgr*は**nvarchar (5)** ,、既定値は FALSE。 **False**の場合、サブスクリプションは同期マネージャーに登録されていません。 **True**の場合、サブスクリプションは同期マネージャーに登録され、を起動[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]せずに同期できます。  
  
`[ @distribution_job_name = ] 'distribution_job_name'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @publisher = ] 'publisher'`パブリッシャーの名前を指定します。 *publisher*は**sysname**で、既定値は NULL です。  
  
`[ @subscriber_provider = ] 'subscriber_provider'`以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のデータソースの OLE DB プロバイダーが登録されている一意のプログラム識別子 (PROGID) を指定します。 *subscriber_provider*は**sysname**,、既定値は NULL です。 *subscriber_provider*は、ディストリビューターにインストールされている OLE DB プロバイダーに対して一意である必要があります。 *subscriber_provider*は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のサブスクライバーに対してのみサポートされます。  
  
`[ @subscriber_datasrc = ] 'subscriber_datasrc'`OLE DB プロバイダーによって認識されるデータソースの名前を指定します。 *subscriber_datasrc*は**nvarchar (4000)** ,、既定の値は NULL です。 *subscriber_datasrc*は、OLE DB プロバイダーを初期化するために DBPROP_INIT_DATASOURCE プロパティとして渡されます。 *subscriber_datasrc*は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のサブスクライバーに対してのみサポートされます。  
  
`[ @subscriber_location = ] 'subscriber_location'`OLE DB プロバイダーによって認識されるデータベースの場所を指定します。 *subscriber_location*は**nvarchar (4000)** ,、既定の値は NULL です。 *subscriber_location*は、OLE DB プロバイダーを初期化するために DBPROP_INIT_LOCATION プロパティとして渡されます。 *subscriber_location*は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のサブスクライバーに対してのみサポートされます。  
  
`[ @subscriber_provider_string = ] 'subscriber_provider_string'`データソースを識別する OLE DB プロバイダー固有の接続文字列を指定します。 *subscriber_provider_string*は**nvarchar (4000)** ,、既定の値は NULL です。 *subscriber_provider_string*が IDataInitialize に渡されるか、または DBPROP_INIT_PROVIDERSTRING プロパティとして設定され、OLE DB プロバイダーが初期化されます。 *subscriber_provider_string*は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のサブスクライバーに対してのみサポートされます。  
  
`[ @subscriber_catalog = ] 'subscriber_catalog'`OLE DB プロバイダーに接続するときに使用するカタログを指定します。 *対応する、* は**sysname**,、既定値は NULL です。 *対応する、* は、OLE DB プロバイダーを初期化するために DBPROP_INIT_CATALOG プロパティとして渡されます。 *対応する、* は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のサブスクライバーに対してのみサポートされます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_addpushsubscription_agent**は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/sp-addpushsubscription-a_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addpushsubscription_agent**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [SQL Server 以外のサブスクライバーのサブスクリプションの作成](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [パブリケーションのサブスクライブ](../../relational-databases/replication/subscribe-to-publications.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_addsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)   
 [sp_dropsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
