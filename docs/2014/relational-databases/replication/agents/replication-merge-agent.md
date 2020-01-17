---
title: レプリケーション マージ エージェント | Microsoft Docs
ms.custom: ''
ms.date: 10/29/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Merge Agent, executables
- Merge Agent, parameter reference
- agents [SQL Server replication], Merge Agent
- command prompt [SQL Server replication]
ms.assetid: fe1e7f60-b0c8-45e9-a5e8-4fedfa73d7ea
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ec21ff98d49cff26bde48452a30fd347c23782fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63216001"
---
# <a name="replication-merge-agent"></a>Replication Merge Agent
  レプリケーション マージ エージェントは、データベース テーブルに保持された初期スナップショットをサブスクライバーに適用するユーティリティ実行可能ファイルです。 さらに、初期スナップショットの作成後にパブリッシャーで発生したデータの増分変更をマージし、ユーザーが構成したルールに従って、またはユーザーが作成したカスタム競合回避モジュールを使用して、競合を調整します。  
  
> [!NOTE]  
>  パラメーターは任意の順序で指定できます。 省略可能なパラメーターを省略する場合、ローカル コンピューターであらかじめ定義されているレジストリ設定の値が使用されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
      replmerg [-?]   
-Publisherserver_name[\instance_name]  
-PublisherDBpublisher_database-Publicationpublication-Subscriberserver_name[\instance_name]  
-SubscriberDBsubscriber_database  
[-AltSnapshotFolderalt_snapshot_folder_path]  
[-Continuous]  
[-DefinitionFiledef_path_and_file_name]  
[-DestThreadsnumber_of_destination_threads]  
[-Distributorserver_name[\instance_name]]  
[-DistributorLogindistributor_login]  
[-DistributorPassworddistributor_password]  
[-DistributorSecurityMode [0|1]]  
[-DownloadGenerationsPerBatchdownload_generations_per_batch]  
[-DownloadReadChangesPerBatchdownload_read_changes_per_batch]  
[-DownloadWriteChangesPerBatchdownload_write_changes_per_batch]  
[-DynamicSnapshotLocationdynamic_snapshot_location]  
[-EncryptionLevel [0|1|2]]  
[-ExchangeType [1|2|3]]  
[-FastRowCount [0|1]]  
[-FileTransferType [0|1]]  
[-ForceConvergenceLevel [0|1|2 (Publisher|Subscriber|Both)]]  
[-FtpAddressftp_address]  
[-FtpPasswordftp_password]  
[-FtpPortftp_port]  
[-FtpUserNameftp_user_name]  
[-HistoryVerboseLevel [0|1|2|3]]  
[-Hostnamehost_name]  
[-InteractiveResolution [0|1]]  
[-InternetLogininternet_login]  
[-InternetPasswordinternet_password]  
[-InternetProxyLogininternet_proxy_login]  
[-InternetProxyPasswordinternet_proxy_password]  
[-InternetProxyServerinternet_proxy_server]  
[-InternetSecurityMode [0|1]]  
[-InternetTimeoutinternet_timeout]  
[-InternetURL internet_url]  
[-KeepAliveMessageIntervalkeep_alive_message_interval_seconds]  
[-LoginTimeOutlogin_time_out_seconds]  
[-MakeGenerationIntervalmake_generation_interval_seconds]  
[-MaxBcpThreadsnumber_of_threads]  
[-MaxDownloadChangesnumber_of_download_changes]  
[-MaxUploadChangesnumber_of_upload_changes]  
[-MetadataRetentionCleanup [0|1]]  
[-Output]  
[-OutputVerboseLevel [0|1|2]]  
[-ParallelUploadDownload [0|1]]  
[-PacketSizepacket_size]   
[-PollingIntervalpolling_interval]  
[-ProfileNameprofile_name]  
[-PublisherFailoverPartnerserver_name[\instance_name] ]  
[-PublisherLoginpublisher_login]  
[-PublisherPassword publisher_password]  
[-PublisherSecurityMode [0|1]]  
[-QueryTimeOutquery_time_out_seconds]  
[-SrcThreadsnumber_of_source_threads]  
[-StartQueueTimeoutstart_queue_timeout_seconds]  
[-SubscriberConflictClean [0|1]]  
[-SubscriberDatabasePathsubscriber_path]  
[-SubscriberDBAddOption [0|1|2|3]]  
[-SubscriberLoginsubscriber_login]  
[-SubscriberPasswordsubscriber_password   
[-SubscriberSecurityMode [0|1]]  
[-SubscriberType [0|1|2|3|4|5|6|7|8|9]]  
[-SubscriptionType [0|1|2]]  
[-SyncToAlternate [0|1]  
[-UploadGenerationsPerBatchupload_generations_per_batch]  
[-UploadReadChangesPerBatchupload_read_changes_per_batch]  
[-UploadWriteChangesPerBatchupload_write_changes_per_batch]  
[-UseInprocLoader]  
[-Validate [0|1|2|3]]  
[-ValidateIntervalvalidate_interval]  
```  
  
## <a name="arguments"></a>引数  
 **-?**  
 使用できるすべてのパラメーターを表示します。  
  
 **-Publisher** _server_name_[ **\\** _instance_name_]  
 パブリッシャーの名前です。 サーバー上の *server_name* の既定のインスタンスの場合は、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を指定します。 サーバー上の _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の既定のインスタンスの場合は、server_name を指定します。  
  
 **-PublisherDB** _publisher_database_  
 パブリッシャー データベースの名前です。  
  
 **-Publication** _publication_  
 パブリケーションの名前です。 このパラメーターは、新規または再初期化されたサブスクリプションのスナップショットを常に利用できるようにパブリケーションを設定している場合にのみ有効です。  
  
 **-Subscriber** _server_name_[ **\\** _instance_name_]  
 サブスクライバーの名前です。 サーバー上の *server_name* の既定のインスタンスの場合は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を指定します。 サーバー上の _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の既定のインスタンスの場合は、server_name を指定します。  
  
 **-SubscriberDB** _subscriber_database_  
 サブスクライバー データベースの名前です。  
  
 **-AltSnapshotFolder** _alt_snapshot_folder_path_  
 サブスクリプションの初期スナップショットが含まれるフォルダーへのパスです。  
  
 **-Continuous**  
 エージェントがレプリケートされたトランザクションの呼び出しを継続的に試みるかどうかを指定します。 このパラメーターを指定する場合、保留されているトランザクションがなくても、エージェントはポーリング間隔でレプリケートされたトランザクションをソースから呼び出します。  
  
 **-DestThreads** _number_of_destination_threads_  
 マージ エージェントが変更の対象で変更を適用するために使用する対象スレッドの数を指定します。 変更の対象は、アップロード実行時はパブリッシャーであり、ダウンロード実行時はサブスクライバーです。 既定値は 4 です。  
  
 **-DefinitionFile** _def_path_and_file_name_  
 エージェント定義ファイルのパスです。 エージェント定義ファイルには、エージェントのコマンド プロンプト引数が含まれます。 ファイルの内容は実行可能ファイルとして解析されます。 二重引用符 (") を使用して、任意の文字を含む引数値を指定します。  
  
 **-Distributor** _server_name_[ **\\** _instance_name_]  
 ディストリビューターの名前です。 サーバー上の *の既定のインスタンスの場合は、* server_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を指定します。 サーバー上の _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の既定のインスタンスの場合は、server_name を指定します。 ディストリビューター (プッシュ) ディストリビューションの場合、既定の名前は、ローカル コンピューターの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の既定のインスタンス名です。  
  
 **-DistributorLogin** _distributor_login_  
 ディストリビューターのログイン名です。  
  
 **-DistributorPassword** _distributor_password_  
 ディストリビューターのパスワードです。  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 ディストリビューターのセキュリティ モードを指定します。 値 **0** は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証モード (既定値) を示し、値 **1** は Windows 認証モードを示します。  
  
 **-DownloadGenerationsPerBatch** _download_generations_per_batch_  
 パブリッシャーからサブスクライバーに変更をダウンロードする間に、1 つのバッチで処理される生成結果の数です。 生成結果は、アーティクルごとに変更の論理グループとして定義されます。 信頼性の高い通信リンクの既定値は 100 です。 信頼性の低い通信リンクの既定値は 10 です。  
  
 **-DownloadReadChangesPerBatch** _download_read_changes_per_batch_  
 パブリッシャーからサブスクライバーに変更をダウンロードする間に、1 つのバッチで読み取られる変更の数です。 既定値は、100 です。  
  
 **-DownloadWriteChangesPerBatch** _download_write_changes_per_batch_  
 パブリッシャーからサブスクライバーに変更をダウンロードする間に、1 つのバッチで適用される変更の数です。 既定値は、100 です。  
  
 **-DynamicSnapshotLocation** _dynamic_snapshot_location_  
 パブリケーションでパラメーター化された行フィルターを使用する場合のフィルター選択されたデータ スナップショット ファイルの位置です。  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 接続時にマージ エージェントで使用される SSL (Secure Sockets Layer) 暗号化のレベルです。  
  
|EncryptionLevel の値|説明|  
|---------------------------|-----------------|  
|**0**|SSL は使用されません。|  
|**1**|SSL は使用されますが、信頼できる発行者によって SSL サーバー証明が署名されているかどうかを検証しません。|  
|**2**|SSL が使用され、証明書の確認が行われます。|  

 > [!NOTE]  
 >  有効な SSL 証明書には、SQL Server の完全修飾ドメイン名が定義されます。 -EncryptionLevel を 2 に設定したときにエージェントが正しく接続されるようにするには、ローカルの SQL Server 上に別名を作成します。 'Alias Name' パラメーターはサーバー名にし、'Server' パラメーターは SQL Server の完全修飾名に設定する必要があります。
  
 詳細については、次を参照してください。 [SQL Server レプリケーションのセキュリティ](../security/view-and-modify-replication-security-settings.md)します。  
  
 **-ExchangeType** [ **1**| **2**| **3**]  
 > [!WARNING]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)]アップロードを制限するには、`@subscriber_upload_options` の `sp_addmergearticle` を代わりに使用します。  
  
 同期中のデータ交換の種類を指定します。次のいずれかを指定できます。  
  
|ExchangeType の値|説明|  
|------------------------|-----------------|  
|**1**|エージェントは、サブスクライバーからパブリッシャーにデータ変更をアップロードします。|  
|**2**|エージェントは、パブリッシャーからサブスクライバーにデータ変更をダウンロードします。|  
|**3** (既定値)|エージェントは最初にサブスクライバーからパブリッシャーにデータ変更をアップロードし、次にパブリッシャーからサブスクライバーにデータ変更をダウンロードします。 このオプションは、Web 同期で使用する必要があります。|  
  
 ダウンロード専用のアーティクルによって、パブリケーション内の個別のアーティクルの同期の動作を制御して、パフォーマンスを向上させることができます。 詳細については、「[ダウンロード専用アーティクルを使用したマージ レプリケーションのパフォーマンス最適化](../merge/optimize-merge-replication-performance-with-download-only-articles.md)」を参照してください。  
  
 `ExchangeType` を使用してマージ レプリケーションのアップロード フェーズとダウンロード フェーズを個別のセッションとして分ける場合は、`ExchangeType` を 1 に設定してマージ エージェントを実行し、その後でこのパラメーターの値を 2 に設定してマージ エージェントを再度実行する必要があります。 どちらのパラメーターを使用してもマージ エージェントの実行が失敗する場合、メタデータが削除され、サブスクリプションの再初期化 (アップロードは行わない) を要求される可能性があります。  
  
 **-FastRowCount** [**0**|**1**]  
 行数の検証に使用する行数計算方法の種類を指定します。 値 **1** (既定) は高速計算法を示します。 値 **0** は、完全行数計算法を示します。  
  
 **-FileTransferType** [**0**|**1**]  
 ファイル転送の種類を指定します。 **0** の値は UNC (汎用名前付け規則) を示し、 **1** の値は FTP (ファイル転送プロトコル) を示します。  
  
 **-ForceConvergenceLevel** [**0**|**1**|**2** ( **Publisher**| **Subscriber**| **Both**)]  
 マージ エージェントが使用する収束のレベルを指定します。次のいずれかを指定できます。  
  
|ForceConvergenceLevel の値|説明|  
|---------------------------------|-----------------|  
|**0** (既定値)|既定値です。 追加の収束なしで標準のマージを実行します。|  
|**1**|すべての生成結果の収束を強制します。|  
|**2**|すべての生成結果の収束を強制し、破損した系列を修正します。 この値を指定する場合は、系列を修正する場所 (パブリッシャー、サブスクライバー、またはパブリッシャーとサブスクライバーの両方) を指定します。|  
  
 **-FtpAddress** _ftp_address_  
 ディストリビューター用の FTP サービスのネットワーク アドレスです。 このパラメーターを指定しない場合、 **Distributor** が使用されます。  
  
 **-FtpPassword** _ftp_password_  
 FTP サービスに接続するときに使用するユーザー パスワードです。  
  
 **-FtpPort** _ftp_port_  
 ディストリビューター用の FTP サービスのポート番号です。 このパラメーターを指定しない場合、FTP サービスの既定のポート番号 (21) が使用されます。  
  
 **-FtpUserName** _ftp_user_name_  
 FTP サービスに接続するときに使用するユーザー名です。 この引数を指定しない場合は、匿名が使用されます。  
  
 **-HistoryVerboseLevel** [**1**|**2**|**3**]  
 マージ操作中にログに記録する履歴の量を指定します。 **1**を選択すれば、ログへの履歴の記録がパフォーマンスに与える影響を最小限に抑えることができます。  
  
|HistoryVerboseLevel の値|説明|  
|-------------------------------|-----------------|  
|**0**|エージェントの状態の最終メッセージ、最終のセッションの詳細、およびすべてのエラーをログに記録します。|  
|**1**|各セッションの状態における増分セッションの詳細をログに記録します。エージェントの状態の最終メッセージ、最終のセッションの詳細、およびすべてのエラーに加えて、進行状況が含まれます。|  
|**2**|既定値です。 各セッションの状態における増分セッションの詳細、およびアーティクル レベルのセッションの詳細をログに記録します。エージェントの状態の最終メッセージ、最終のセッションの詳細、およびすべてのエラーに加えて、進行状況が含まれます。 エージェントの状態のメッセージもログに記録されます。|  
|**3**|**-HistoryVerboseLevel** = **2**と同じですが、より多くのエージェント進行状況メッセージがログに記録されます。|  
  
 **-Hostname** _host_name_  
 ローカル コンピューターのネットワーク名です。 既定値は、ローカル コンピューターの名前になります。  
  
 **-InteractiveResolution** [**0**|**1**]  
 同期中に競合が発生した場合に、インタラクティブ競合回避を使用するかどうかを指定します。 既定値の **0**は、インタラクティブ競合回避を使用しないことを示します。  
  
 **-InternetLogin** _internet_login_  
 認証を必要とする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーション リスナー ISAPI DLL への接続時に使用されるログイン名を指定します。  
  
 **-InternetPassword** _internet_password_  
 認証を必要とする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーション リスナー ISAPI DLL への接続時に使用されるパスワードを指定します。  
  
 **-InternetProxyLogin**  *internet_proxy_login*  
 認証を必要とする、 *internet_proxy_server*で定義されたプロキシ サーバーへの接続時に使用されるログイン名を指定します。  
  
 **-InternetProxyPassword**  *internet_proxy_password*  
 認証を必要とする、 *internet_proxy_server*で定義されたプロキシ サーバーへの接続時に使用されるパスワードを指定します。  
  
 **-InternetProxyServer**  *internet_proxy_server*  
 *internet_url*で指定した HTTP リソースへのアクセス時に使用するプロキシ サーバーを指定します。  
  
 **-InternetSecurityMode** [**0**|**1**]  
 Web 同期時の Web サーバーとの接続に使用される IIS セキュリティ モードを指定します。 値 **0** は基本認証を示し、値 **1** は Windows 統合認証 (既定値) を指定します。  
  
 **-InternetTimeout** _internet_timeout_  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーション リスナー ISAPI DLL がタイムアウトになるまでの秒数です。  
  
 **-InternetURL** _internet_url_  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーション リスナー ISAPI DLL への接続に使用される URL を指定します。 このプロパティの指定は必須です。  
  
 **-KeepAliveMessageInterval** _keep_alive_message_interval_seconds_  
 既存の接続がサーバーからの応答を待機しているかどうかを、履歴スレッドがチェックするまでの秒数です。 長時間実行のときに、照合エージェントがマージ エージェントに SUSPECT のマークを付けないようにするには、この値を小さくします。 既定値は **300** 秒です。  
  
 **-LoginTimeOut** _login_time_out_seconds_  
 ログインがタイムアウトになるまでの秒数です。既定値は **15** 秒です。  
  
 **-MakeGenerationInterval** _make_generation_interval_seconds_  
 クライアントにダウンロードする生成結果 (変更のバッチ) を作成する間隔 (秒) です。 既定値は **1** 秒です。  
  
 Makegeneration は、パブリッシャーの変更をサブスクライバーにダウンロードするように準備するプロセスです。また、ダウンロード中にパフォーマンスのボトルネックになる場合があります。 makegeneration プロセスが **-MakeGenerationInterval**で指定された間隔で既に実行された場合、現在の同期セッションでは、このプロセスはスキップされます。 これは、同期のコンカレンシーに役立つ場合があります。特に、サブスクライバーが変更をダウンロードしない場合に役立ちます。  
  
 **-MaxBcpThreads** _number_of_threads_  
 並列実行できる一括コピーの操作数を指定します。 同時に存在するスレッドおよび ODBC 接続の最大数は、 **MaxBcpThreads** 、またはパブリケーション データベース内のシステム テーブル **sysmergeschemachange** に表示される一括コピー要求数のいずれか少ない方の値になります。 **MaxBcpThreads** の値は、0 よりも大きくする必要がありますが、ハードコーディングされた上限はありません。 既定値は **1**です。  
  
 **-MaxDownloadChanges** _number_of_download_changes_  
 パブリッシャーからサブスクライバーにダウンロードする必要のある変更済みの行の最大数を指定します。 ダウンロードする行数が、指定した最大数より多くなる場合があります。完全な生成結果が処理されること、および並列の対象スレッドが実行されて最初のパスでそれぞれ 100 以上の変更が処理されることが原因です。 既定では、ダウンロードの準備が整っている変更がすべて送信されます。  
  
 **-MaxUploadChanges** _number_of_upload_changes_  
 サブスクライバーからパブリッシャーにアップロードする必要のある変更済みの行の最大数を指定します。 アップロードする行数が、指定した最大数より多くなる場合があります。完全な生成結果が処理されること、および並列の対象スレッドが実行されて最初のパスでそれぞれ 100 以上の変更が処理されることが原因です。 既定では、アップロードの準備が整っている変更がすべて送信されます。  
  
 **-MetadataRetentionCleanup** [**0**|**1**]  
 パブリケーション保有期間に基づいて、メタデータを [MSmerge_genhistory](/sql/relational-databases/system-tables/msmerge-genhistory-transact-sql)、 [MSmerge_contents](/sql/relational-databases/system-tables/msmerge-contents-transact-sql)、 [MSmerge_tombstone](/sql/relational-databases/system-tables/msmerge-tombstone-transact-sql)、 [MSmerge_past_partition_mappings](/sql/relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql)、および [MSmerge_current_partition_mappings](/sql/relational-databases/system-tables/msmerge-current-partition-mappings) から削除するかどうかを指定します。 既定値の **1**は、クリーンアップを行う必要があることを示します。 値 **0** は、クリーンアップを自動的に実行しないことを示します。  
  
 **-Output** _output_path_and_file_name_  
 エージェントの出力ファイルのパスです。 ファイル名が指定されていない場合、出力はコンソールに送られます。 指定された名前のファイルが存在する場合、出力はそのファイルに追加されます。  
  
 **-OutputVerboseLevel** [**0**|**1**|**2**]  
 出力を詳細表示にするかどうかを指定します。 詳細レベルが **0**の場合、エラー メッセージだけが出力されます。 詳細レベルが **1**の場合、すべての実行状況報告メッセージが印刷されます。 詳細レベルが **2** (既定値) の場合、すべてのエラー メッセージと実行状況報告メッセージが出力されます。これはデバッグ時に便利です。  
  
 **-ParallelUploadDownload** [**0**|**1**]  
 パブリッシャーにアップロードする変更とサブスクライバーにダウンロードする変更をマージ エージェントが並列で処理するかどうかを指定します。帯域幅が広いネットワークを使用している大容量環境で有用です。 **ParallelUploadDownload** が **1**の場合は、並列処理が有効です。  
  
 **-PacketSize**  
 パケット サイズをバイト単位で指定します。 既定値は 4096 (バイト) です。  
  
 **-PollingInterval** _polling_interval_  
 パブリッシャーまたはサブスクライバーへのデータ変更をクエリする間隔 (秒数) を示します。 既定値は 60 秒です。  
  
 **-ProfileName** _profile_name_  
 エージェント パラメーターに使用するエージェント プロファイルを指定します。 **ProfileName** が NULL の場合、このエージェント プロファイルは無効になります。 **ProfileName** を指定しない場合、エージェントの種類に応じた既定のプロファイルが使われます。 詳細については、「[レプリケーション エージェント プロファイル](replication-agent-profiles.md)」を参照してください。  
  
 **-PublisherFailoverPartner** _server_name_[ **\\** _instance_name_]  
 パブリケーション データベースとのデータベース ミラーリング セッションに参加する、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー パートナー インスタンスを指定します。 詳細については、「 [データベース ミラーリングとレプリケーション &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)」をご覧ください。  
  
 **-PublisherLogin** _publisher_login_  
 パブリッシャーのログイン名です。 **PublisherSecurityMode** が **0** ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証) の場合、このパラメーターの指定は必須です。  
  
 **-PublisherPassword** _publisher_password_  
 パブリッシャーのパスワードです。 **PublisherSecurityMode** が **0** ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証) の場合、このパラメーターの指定は必須です。  
  
 **-PublisherSecurityMode** [**0**|**1**]  
 パブリッシャーのセキュリティ モードを指定します。 値 **0** は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証モード (既定値) を示し、値 **1** は Windows 認証モードを示します。  
  
 **-QueryTimeOut** _query_time_out_seconds_  
 クエリがタイムアウトになるまでの秒数です。既定では 300 秒です。 マージ エージェントも `QueryTimeout` の値を使用して、この値が 1800 を超える場合にパーティション スナップショットの生成をどのくらいの期間待機するかを判断します。  
  
 **-SrcThreads** _number_of_source_threads_  
 マージ エージェントが変更元から変更を列挙するために使用するソース スレッドの数を指定します。 変更元は、アップロード実行時はサブスクライバーであり、ダウンロード実行時はパブリッシャーです。 既定値は **3**です。  
  
 **-StartQueueTimeout** _start_queue_timeout_seconds_  
 実行中の同時マージ処理数が **@max_concurrent_merge** の **@max_concurrent_merge**」を参照してください。 最長秒数に達したときにマージ エージェントが待機中である場合、マージ エージェントは終了します。 値 0 は、エージェントが無制限に待機することを示します。ただし、キャンセルできます。  
  
 **-SubscriberDatabasePath** _subscriber_database_path_  
 **SubscriberType** が **2** の場合、Jet データベース (.mdb) ファイルへのパスを指定します。この指定では、ODBC データ ソース名 (DSN) なしで Jet データベースに接続することができます。  
  
 **-SubscriberDBAddOption** [**0**| **1**| **2**| **3**]  
 既存のサブスクライバー データベースがあるかどうかを指定します。  
  
|SubscriberDBAddOption の値|説明|  
|---------------------------------|-----------------|  
|**0**|既存のデータベースを使用します (既定値)。|  
|**1**|新しい空のサブスクライバー データベースを作成します。|  
|**2**|新しいデータベースを作成して、指定されたファイルにアタッチします。|  
|**3**|新しいデータベースを作成し、データベースをアタッチして、ファイルに存在する可能性のあるすべてのサブスクリプションを有効にします。|  
  
> [!NOTE]  
>  値 **2** および **3**を使用する場合は、サブスクライバーのデータベース パスを **SubscriberDatabasePath** オプションで指定する必要があります。  
  
 **-SubscriberLogin** _subscriber_login_  
 サブスクライバーのログイン名です。 **SubscriberSecurityMode** が **0** ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証モード) の場合は、このパラメーターを指定しなければなりません。  
  
 **-SubscriberPassword** _subscriber_password_  
 サブスクライバーのパスワードです。 **SubscriberSecurityMode** が **0** ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証モード) の場合は、このパラメーターを指定しなければなりません。  
  
 **-SubscriberSecurityMode** [ **0**| **1**]  
 サブスクライバーのセキュリティ モードを指定します。 値 **0** は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証モード (既定値) を示し、値 **1** は Windows 認証モードを示します。  
  
 **-SubscriberConflictClean** [ **0**| **1**]  
 同期処理中にサブスクライバーで競合テーブルがクリーンアップされるかどうかを示します。値 **1** は、サブスクライバーで競合テーブルがクリーンアップされることを示します。 このパラメーターは、競合のログ記録が集中管理されていないパブリケーションに対するサブスクリプションにのみ使用されます。  
  
 **-SubscriberType** [ **0**| **1**| **3**| **4**| **5**| **6**| **7**| **8**]  
 マージ エージェントによって使用されるサブスクライバー接続の種類を指定します。 このパラメーターでは、既定値の **0** のみがサポートされています。  
  
 **-SubscriptionType**[ **0**| **1**| **2**]  
 ディストリビューションのサブスクリプションの種類を指定します。 値 **0** は、プッシュ サブスクリプション (既定値) を示します。値 **1** はプル サブスクリプションを示し、値 **2** は匿名サブスクリプションを示します。  
  
 **-SyncToAlternate** **[0|1]**  
 マージ エージェントがサブスクリプションと代替パブリッシャー間での同期を実行しているかどうかを指定します。 値 **1** は、これが代替パブリッシャーであることを示します。 既定値は **0**です。  
  
 **-UploadGenerationsPerBatch** _upload_generations_per_batch_  
 サブスクライバーからパブリッシャーに変更をアップロードする間に、1 つのバッチで処理される生成結果の数です。 生成結果は、アーティクルごとに変更の論理グループとして定義されます。 信頼性の高い通信リンクの既定値は **100**です。 信頼性の低い通信リンクの既定値は **1**です。  
  
 **-UploadReadChangesPerBatch** _upload_read_changes_per_batch_  
 サブスクライバーからパブリッシャーに変更をアップロードする間に、1 つのバッチで読み取られる変更の数です。 既定値は **100**です。  
  
 **-UploadWriteChangesPerBatch** _upload_write_changes_per_batch_  
 サブスクライバーからパブリッシャーに変更をアップロードする間に、1 つのバッチで適用される変更の数です。 既定値は **100**です。  
  
 **-UseInprocLoader**  
 マージ エージェントでスナップショット ファイルをサブスクライバーに適用するときに BULK INSERT コマンドを使用することによって、初期スナップショットのパフォーマンスが向上します。 このパラメーターは XML データ型との互換性がないため非推奨とされます。 XML データをレプリケートしない場合にのみ、このパラメーターを使用できます。 このパラメーターは、キャラクター モードのスナップショットでは使用できません。 このパラメーターを使用する場合は、サブスクライバー側の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントに、スナップショットの .bcp データ ファイルが格納されたディレクトリの読み取り権限が必要です。 このパラメーターを使用しない場合、エージェントによって読み込まれた ODBC ドライバーがファイルから読み取るので、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントのセキュリティ コンテキストは使用されません。  
  
 **-Validate** [**0**|**1**|**2**|**3**]  
 マージ セッションの最後に検証を行うかどうかを指定し、行う場合は検証の種類も指定します。 推奨値は **3** です。  
  
|Validate の値|説明|  
|--------------------|-----------------|  
|**0** (既定値)|検証なし。|  
|**1**|行数のみの検証。|  
|**2**|行数とチェックサムの検証。|  
|**3**|行数とバイナリ チェックサムの検証。|  
  
> [!NOTE]  
>  バイナリ チェックサムまたはチェックサムを使用した検証では、データ型がサブスクライバー側とパブリッシャー側とで異なる場合には、誤ってエラーを報告することがあります。 詳細については、「[レプリケートされたデータの検証](../validate-data-at-the-subscriber.md)」の「データ検証に関する注意点」を参照してください。  
  
 **-ValidateInterval** _validate_interval_  
 サブスクリプションが継続モードで検証される間隔 (分) です。 既定値は **60** 分です。  
  
## <a name="remarks"></a>コメント  
  
> [!IMPORTANT]  
>  ドメイン ユーザー アカウント (既定値) ではなくローカル システム アカウントで実行するように [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントがインストールされている場合、サービスがアクセスできるのはローカル コンピューターのみです。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントの下で実行するマージ エージェントで、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]へのログイン時に Windows 認証モードが使用されるように構成すると、マージ エージェントは失敗します。 既定の設定は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証です。  
  
 マージ エージェントを起動するには、コマンド プロンプトから **replmerg.exe** を実行します。 詳細については、「 [レプリケーション エージェント実行可能ファイルのプログラミング](../concepts/replication-agent-executables-concepts.md)」を参照してください。  
  
 現在のセッションのマージ エージェントの履歴は、連続モードでの実行中には削除されません。 エージェントが長時間実行されると、マージ履歴テーブルに多数のエントリが発生し、パフォーマンスに影響する可能性があります。 この問題を解決するには、スケジュールされたモードに切り替えるか、引き続き連続モードを使用する場合は、定期的にマージ エージェントを再起動するための専用のジョブを作成するか、履歴の詳細レベルを下げて行数を減らして、パフォーマンスへの影響を軽減してください。  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェントの管理](replication-agent-administration.md)  
  
  
