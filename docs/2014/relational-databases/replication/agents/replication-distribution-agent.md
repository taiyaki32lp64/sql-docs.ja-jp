---
title: レプリケーション ディストリビューション エージェント | Microsoft Docs
ms.custom: ''
ms.date: 10/29/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Distribution Agent, executables
- agents [SQL Server replication], Distribution Agent
- Distribution Agent, parameter reference
- command prompt [SQL Server replication]
ms.assetid: 7b4fd480-9eaf-40dd-9a07-77301e44e2ac
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0a1bdbe715aa970f87596060a774ac2b1ed8df15
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210740"
---
# <a name="replication-distribution-agent"></a>レプリケーション ディストリビューション エージェント
  レプリケーション ディストリビューション エージェントは、ディストリビューション データベース テーブルに登録されたスナップショット (スナップショット レプリケーションの場合) とトランザクション (トランザクション レプリケーションの場合) を、サブスクライバーのレプリケーション先のテーブルに移動する実行可能ファイルです。  
  
> [!NOTE]  
>  パラメーターは任意の順序で指定できます。 省略可能なパラメーターを省略する場合、ローカル コンピューターであらかじめ定義されているレジストリ設定の値が使用されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
      distrib [-?]  
-Publisherserver_name[\instance_name]  
-PublisherDBpublisher_database-Subscriberserver_name[\instance_name]  
-SubscriberDBsubscriber_database   
[-AltSnapshotFolderalt_snapshot_folder_path]   
[-BcpBatchSizebcp_batch_size]  
[-CommitBatchSizecommit_batch_size]  
[-CommitBatchThresholdcommit_batch_threshold]  
[-Continuous]  
[-DefinitionFiledef_path_and_file_name]  
[-Distributordistributor]  
[-DistributorLogindistributor_login]  
[-DistributorPassworddistributor_password]  
[-DistributorSecurityMode [0|1]]  
[-EncryptionLevel [0|1|2]]  
[-ErrorFileerror_path_and_file_name]  
[-ExtendedEventConfigFileconfiguration_path_and_file_name]  
[-FileTransferType [0|1]]  
[-FtpAddressftp_address]  
[-FtpPasswordftp_password]   
[-FtpPortftp_port]  
[-FtpUserNameftp_user_name]  
[-HistoryVerboseLevel [0|1|2|3]]  
[-Hostnamehost_name]  
[-KeepAliveMessageIntervalkeep_alive_message_interval_seconds]  
[-LoginTimeOutlogin_time_out_seconds]  
[-MaxBcpThreads]  
[-MaxDeliveredTransactionsnumber_of_transactions]  
[-MessageIntervalmessage_interval]  
[-OledbStreamThresholdoledb_stream_threshold]  
[-Outputoutput_path_and_file_name]  
[-OutputVerboseLevel [0|1|2]]  
[-PacketSizepacket_size]  
[-PollingIntervalpolling_interval]  
[-ProfileNameprofile_name]  
[-Publicationpublication]  
[-QueryTimeOutquery_time_out_seconds]  
[-QuotedIdentifierquoted_identifier]  
[-SkipErrorsnative_error_id [:...n]]  
[-SubscriberDatabasePathsubscriber_path]  
[-SubscriberLoginsubscriber_login]  
[-SubscriberPasswordsubscriber_password]  
[-SubscriberSecurityMode [0|1]]  
[-SubscriberType [0|1|3]]  
[-SubscriptionStreams [1|2|...64]]  
[-SubscriptionTableNamesubscription_table]  
[-SubscriptionType [0|1|2]]  
[-TransactionsPerHistory [0|1|...10000]]  
[-UseDTS]  
[-UseInprocLoader]  
[-UseOledbStreaming]  
```  
  
## <a name="arguments"></a>引数  
 **-?**  
 使用できるすべてのパラメーターを表示します。  
  
 **-Publisher** _server_name_[ **\\** _instance_name_]  
 パブリッシャーの名前です。 サーバー上の *server_name* の既定のインスタンスの場合は、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を指定します。 サーバー上の _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の既定のインスタンスの場合は、server_name を指定します。  
  
 **-PublisherDB** _publisher_database_  
 パブリッシャー データベースの名前です。  
  
 **-Subscriber** _server_name_[ **\\** _instance_name_]  
 サブスクライバーの名前です。 サーバー上の *server_name* の既定のインスタンスの場合は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を指定します。 サーバー上の _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の既定のインスタンスの場合は、server_name を指定します。  
  
 **-SubscriberDB** _subscriber_database_  
 サブスクライバー データベースの名前です。  
  
 **-AltSnapshotFolder** _alt_snapshot_folder_path_  
 サブスクリプションの初期スナップショットが含まれるフォルダーへのパスです。  
  
 **-BcpBatchSize** _bcp_batch_size_  
 一括コピー操作によって送られる行の数です。 **bcp in** 操作を実行する場合、バッチ サイズは 1 つのトランザクションとしてサーバーに送る行数です。ディストリビューション エージェントが **bcp** 実行状況メッセージをログに記録する前に、これらの行数を送る必要があります。 **bcp out** 操作を実行する場合は、固定バッチ サイズ **1000** が使用されます。  
  
 **-CommitBatchSize** _commit_batch_size_  
 COMMIT ステートメントを実行する前に、サブスクライバーに対して実行するトランザクションの数です。 既定値は、100 です。  
  
 **-CommitBatchThreshold**  _commit_batch_threshold_  
 COMMIT ステートメントを実行する前に、サブスクライバーに対して実行するレプリケーション コマンドの数です。 既定値は 1000 です。  
  
 **-Continuous**  
 エージェントがレプリケートされたトランザクションの呼び出しを継続的に試みるかどうかを指定します。 このパラメーターを指定する場合、保留されているトランザクションがなくても、エージェントはポーリング間隔でレプリケートされたトランザクションをソースから呼び出します。  
  
 **-DefinitionFile** _def_path_and_file_name_  
 エージェント定義ファイルのパスです。 エージェント定義ファイルには、エージェントのコマンド プロンプト引数が含まれます。 ファイルの内容は実行可能ファイルとして解析されます。 二重引用符 (") を使用して、任意の文字を含む引数値を指定します。  
  
 **-Distributor** _distributor_  
 ディストリビューターの名前です。 ディストリビューター (プッシュ) ディストリビューションの場合、既定値はローカル ディストリビューターの名前になります。  
  
 **-DistributorLogin** _distributor_login_  
 ディストリビューターのログイン名です。  
  
 **-DistributorPassword** _distributor_password_  
 ディストリビューターのパスワードです。  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 ディストリビューターのセキュリティ モードを指定します。 値 0 は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証モードを指定し、値 1 は Windows 認証モード (既定値) を指定します。  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 接続確立時にディストリビューション エージェントが使用する SSL (Secure Sockets Layer) の暗号化レベルです。  
  
|EncryptionLevel の値|説明|  
|---------------------------|-----------------|  
|**0**|SSL は使用されません。|  
|**1**|SSL は使用されますが、信頼できる発行者によって SSL サーバー証明が署名されているかどうかを検証しません。|  
|**2**|SSL が使用され、証明書の確認が行われます。|  
 
 > [!NOTE]  
 >  有効な SSL 証明書には、SQL Server の完全修飾ドメイン名が定義されます。 -EncryptionLevel を 2 に設定したときにエージェントが正しく接続されるようにするには、ローカルの SQL Server 上に別名を作成します。 'Alias Name' パラメーターはサーバー名にし、'Server' パラメーターは SQL Server の完全修飾名に設定する必要があります。

 詳細については、次を参照してください。 [SQL Server レプリケーションのセキュリティ](../security/view-and-modify-replication-security-settings.md)します。  
  
 **-ErrorFile** _error_path_and_file_name_  
 ディストリビューション エージェントが作成するエラー ファイルのパスとファイル名です。 このファイルは、サブスクライバーでレプリケーション トランザクションを適用しているときに、エラーが発生すると生成されます。パブリッシャーまたはディストリビューターで発生したエラーについては、このファイルには記録されません。 このファイルには、障害が発生したレプリケーション トランザクションおよび関連するエラー メッセージが含まれます。 指定しない場合は、エラー ファイルはディストリビューション エージェントの現在のディレクトリに作成されます。 エラー ファイル名は、ディストリビューション エージェントの名前に .err 拡張子を付けた名前です。 指定したファイル名が既存の場合、エラー メッセージはこのファイルに追加されます。 このパラメーターには最大 256 個の Unicode 文字を指定できます。  
  
 **-ExtendedEventConfigFile** _configuration_path_and_file_name_  
 拡張イベントの XML 構成ファイルのパスとファイル名を指定します。 拡張イベントの構成ファイルによって、追跡に必要なセッションを構成し、イベントを有効にすることができます。  
  
 **-FileTransferType** [ **0**| **1**]  
 ファイル転送の種類を指定します。 **0** の値は UNC (汎用名前付け規則) を示し、 **1** の値は FTP (ファイル転送プロトコル) を示します。  
  
 **-FtpAddress** _ftp_address_  
 ディストリビューター用の FTP サービスのネットワーク アドレスです。 このパラメーターを指定しない場合、 **DistributorAddress** が使用されます。 **DistributorAddress** が指定されていない場合、 **Distributor** が使用されます。  
  
 **-FtpPassword** _ftp_password_  
 FTP サービスに接続するときに使用するユーザー パスワードです。  
  
 **-FtpPort** _ftp_port_  
 ディストリビューター用の FTP サービスのポート番号です。 このパラメーターを指定しない場合、FTP サービスの既定のポート番号 (21) が使用されます。  
  
 **-FtpUserName**  _ftp_user_name_  
 FTP サービスに接続するときに使用するユーザー名です。 指定しない場合、 **anonymous** が使用されます。  
  
 **-HistoryVerboseLevel** [ **0** | **1** | **2** | **3** ]  
 ディストリビューション操作中にログに記録する履歴の量を指定します。 **1**を選択すれば、ログへの履歴の記録がパフォーマンスに与える影響を最小限に抑えることができます。  
  
|HistoryVerboseLevel の値|説明|  
|-------------------------------|-----------------|  
|**0**|進行状況メッセージがコンソールまたは出力ファイルに書き込まれます。 履歴レコードは、ディストリビューション データベースのログに記録されません。|  
|**1**|既定値です。 同じ状態 (startup、progress、success など) を示している以前の履歴メッセージを常に更新します。 前回の記録に同じ状態がない場合は、新しい記録を挿入します。|  
|**2**|アイドル状態や長時間実行を示すメッセージでない場合、新しい履歴レコードを挿入します。アイドル状態などを示すメッセージの場合には、以前のレコードを更新します。|  
|**3**|アイドル状態を示すメッセージの場合以外は、常に新しいレコードを挿入します。|  
  
 **-Hostname** _host_name_  
 パブリッシャーとの接続時に使用するホスト名です。 このパラメーターには最大 128 個の Unicode 文字を指定できます。  
  
 **-KeepAliveMessageInterval** _keep_alive_message_interval_seconds_  
 既存の接続がサーバーからの応答を待機しているかどうかを、履歴スレッドがチェックするまでの秒数です。 この値を小さくすれば、ディストリビューション エージェントが時間のかかるバッチを実行しているとき、照合エージェントによって SUSPECT とマークされるのを防ぐことができます。 既定値は **300** 秒です。  
  
 **-LoginTimeOut** _login_time_out_seconds_  
 ログインがタイムアウトになるまでの秒数です。既定値は **15** 秒です。  
  
 **-MaxBcpThreads** _number_of_threads_  
 並列実行できる一括コピーの操作数を指定します。 同時に存在するスレッドと ODBC 接続の最大数は、 **MaxBcpThreads** の値と、ディストリビューション データベースの同期トランザクションに示されている一括コピー要求の数の小さい方の値になります。 **MaxBcpThreads** は **0** よりも大きくする必要がありますが、上限はありません。 既定値は、プロセッサ数の **2** 倍の値です。最大値は、 **8**になります。 パブリッシャー側で同時実行スナップショット オプションを使って生成されたスナップショットを適用する場合は、 **MaxBcpThreads**に指定した値に関係なく、単一のスレッドが使用されます。  
  
 **-MaxDeliveredTransactions** _number_of_transactions_  
 1 回の同期でサブスクライバーに適用するプッシュまたはプル トランザクションの最大数です。 値 **0** は、トランザクション数に制限がないことを示します。 その他の値は、サブスクライバーがパブリッシャーからプルする同期の経過時間を短縮するときに使用できます。  
  
> [!NOTE]  
>  -MaxDeliveredTransactions と -Continuous を両方とも指定すると、ディストリビューション エージェントは、指定した数のトランザクションを配信してから、停止します (-Continuous が指定されている場合であっても)。 ジョブが完了した後、ディストリビューション エージェントを再起動してください。  
  
 **-MessageInterval**  _message_interval_  
 履歴をログに記録する間隔です。 次のいずれかの場合、履歴イベントはログに記録されます。  
  
-   最後の履歴イベントをログに記録した後、 **TransactionsPerHistory** の値が経過した場合  
  
-   最後の履歴イベントをログに記録した後、 **MessageInterval** の値が経過した場合  
  
 ソースに利用可能なレプリケートされたトランザクションがない場合、エージェントはディストリビューターに対してトランザクションなしのメッセージを報告します。 このオプションは、エージェントが次にトランザクションなしのメッセージを報告するまでの待ち時間を指定します。 前回レプリケートされたトランザクションを処理した後で、ソースに利用可能なトランザクションがないことを検出すると、エージェントは必ずトランザクションなしのメッセージを報告します。 既定値は 60 秒です。  
  
 **-OledbStreamThreshold** _oledb_stream_threshold_  
 BLOB データの最小バイト サイズを指定します。この値を超えると、データはストリームとしてバインドされます。 このパラメーターを使用するためには、 **-UseOledbStreaming** を指定する必要があります。 400 バイトから 1048576 バイトまでの値を指定できます。既定値は 16384 バイトです。  
  
 **-Output** _output_path_and_file_name_  
 エージェントの出力ファイルのパスです。 ファイル名が指定されていない場合、出力はコンソールに送られます。 指定された名前のファイルが存在する場合、出力はそのファイルに追加されます。  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 出力を詳細表示にするかどうかを指定します。 詳細レベルが **0**の場合、エラー メッセージだけが出力されます。 詳細レベルが **1**の場合、すべての実行状況報告メッセージが出力されます。 詳細レベルが **2** (既定値) の場合、すべてのエラー メッセージと実行状況報告メッセージが出力されます。これはデバッグ時に便利です。  
  
 **-PacketSize** _packet_size_  
 パケット サイズをバイト単位で指定します。 既定値は 4096 (バイト) です。  
  
 **-PollingInterval** _polling_interval_  
 レプリケートされたトランザクションに関してディストリビューション データベースをクエリする間隔を秒単位で示します。 既定値は 5 秒です。  
  
 **-ProfileName** _profile_name_  
 エージェント パラメーターに使用するエージェント プロファイルを指定します。 **ProfileName** が NULL の場合、このエージェント プロファイルは無効になります。 **ProfileName** を指定しない場合、エージェントの種類に応じた既定のプロファイルが使われます。 詳細については、「[レプリケーション エージェント プロファイル](replication-agent-profiles.md)」を参照してください。  
  
 **-Publication**  _publication_  
 パブリケーションの名前です。 このパラメーターは、新規または再初期化されたサブスクリプションのスナップショットを常に利用できるようにパブリケーションを設定している場合にのみ有効です。  
  
 **-QueryTimeOut** _query_time_out_seconds_  
 クエリがタイムアウトになるまでの秒数です。既定値は 1800 秒です。  
  
 **-QuotedIdentifier** _quoted_identifier_  
 使用する引用符で囲まれた識別子を指定します。 値の最初の文字は、ディストリビューション エージェントが使用する値を示します。 値を指定せずに **QuotedIdentifier** を使用する場合、ディストリビューション エージェントはスペースを使用します。 **QuotedIdentifier** を使用しない場合には、ディストリビューション エージェントはサブスクライバーがサポートしている引用符で囲まれた識別子を使用します。  
  
 **-SkipErrors** _native_error_id_ [ **:** _...n_]  
 このエージェントでスキップされる一連のエラー番号をコロンで区切って指定します。  
  
 **-SubscriberDatabasePath** _subscriber_database_path_  
 **SubscriberType** が **2** の場合、Jet データベース (.mdb) ファイルへのパスを指定します。この指定では、ODBC データ ソース名 (DSN) なしで Jet データベースに接続することができます。  
  
 **-SubscriberLogin** _subscriber_login_  
 サブスクライバーのログイン名です。 **SubscriberSecurityMode** が **0** ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証モード) の場合は、このパラメーターを指定しなければなりません。  
  
 **-SubscriberPassword** _subscriber_password_  
 サブスクライバーのパスワードです。 **SubscriberSecurityMode** が **0** ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証モード) の場合は、このパラメーターを指定しなければなりません。  
  
 **-SubscriberSecurityMode** [ **0**| **1**]  
 サブスクライバーのセキュリティ モードを指定します。 値 **0** は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証モードを指定し、値 **1** は Windows 認証モード (既定値) を指定します。  
  
 **-SubscriberType** [ **0**| **1**| **3**]  
 ディストリビューション エージェントが使用するサブスクライバー接続の種類を指定します。  
  
|サブスクライバーの種類|説明|  
|--------------------------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|  
|**1**|ODBC データ ソース (ODBC data source)|  
|**3**|OLE DB データ ソース|  
  
 **-SubscriptionStreams** [**0**|**1**|**2**|...**64**]  
 単一のスレッドを使用しているときに、トランザクションに関連したさまざまな特性を維持しながら、サブスクライバーに対してバッチ変更を適用することのできる、ディストリビューション エージェントあたりの接続数です。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] パブリッシャーの場合、1 から 64 までの値がサポートされます。 このパラメーターは、パブリッシャーとディストリビューターが [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のバージョンで実行されている場合にのみ使用できます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーまたはピア ツー ピア サブスクリプションの場合は、このパラメーターを使用しないか、0 にする必要があります。  
  
> [!NOTE]  
>  いずれかの接続が実行またはコミットに失敗した場合、進行中のバッチがすべての接続について中止されます。その場合、エージェントは、単一のストリームを使用して、失敗したバッチを再試行します。 この再試行フェーズが完了するまでは、サブスクライバー側に、トランザクションの一時的な不整合が存在する可能性があります。 サブスクライバーのトランザクション一貫性は、前回失敗したバッチが正常にコミットされた後で復元されます。  
  
> [!IMPORTANT]  
>  **-SubscriptionStreams**に対して 2 以上の値を指定すると、サブスクライバー側でトランザクションが受信される順序が、パブリッシャー側でトランザクションが作成された順序と異なる場合があります。 この動作が原因で同期中に制約違反が発生する場合は、NOT FOR REPLICATION オプションを使用して同期中の制約の適用を無効にする必要があります。 詳細については、「[同期中にトリガと制約の動作を制御する方法 &#40;レプリケーション Transact-SQL プログラミング&#41;](../control-behavior-of-triggers-and-constraints-in-synchronization.md)」を参照してください。  
  
> [!NOTE]  
>  Subscriptionstreams は、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]を渡すように構成されたアーティクルでは使用できません。 subscriptionstreams を使用するには、代わりにストアド プロシージャの呼び出しを渡すようにアーティクルを構成します。  
  
 **-SubscriptionTableName** _subscription_table_  
 指定したサブスクライバーで作成または使用するサブスクリプション テーブルの名前です。 指定しない場合、[MSreplication_subscriptions &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/msreplication-subscriptions-transact-sql) テーブルが使用されます。 長いファイル名をサポートしないデータベース管理システム (DBMS) にはこのオプションを使用します。  
  
 **-SubscriptionType** [ **0**| **1**| **2**]  
 ディストリビューションのサブスクリプションの種類を指定します。 値 **0** はプッシュ サブスクリプションを、値 **1** はプル サブスクリプションを、値 **2** は匿名サブスクリプションを示します。  
  
 **-TransactionsPerHistory** [ **0**| **1**|...**10000**]  
 履歴をログに記録するトランザクション間隔を指定します。 最後に履歴をログに記録してからコミットしたトランザクションの数がこのオプションより多い場合、履歴メッセージがログに記録されます。 既定値は、100 です。 値 **0** は、 **TransactionsPerHistory**が無制限であることを指定します。 上記の **-MessageInterval** パラメーターを参照してください。  
  
 **-UseDTS**  
 データ変換を許可するパブリケーションでは、このパラメーターを指定する必要があります。  
  
 **-UseInprocLoader**  
 ディストリビューション エージェントがスナップショット ファイルをサブスクライバーに適用するときに、BULK INSERT コマンドが使用され、初期スナップショットのパフォーマンスが向上します。 このパラメーターは XML データ型との互換性がないため非推奨とされます。 XML データをレプリケートしない場合にのみ、このパラメーターを使用できます。 このパラメーターを、キャラクター モードのスナップショットや、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーで使用することはできません。 このパラメーターを使用する場合は、サブスクライバー側の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントに、スナップショットの .bcp データ ファイルが格納されたディレクトリの読み取り権限が必要です。 このパラメーターを使用しない場合、これらのファイルが、エージェント ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のサブスクライバーの場合) またはエージェントが読み込む ODBC ドライバー ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サブスクライバーの場合) によって読み取られるため、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントのセキュリティ コンテキストは使用されません。  
  
 **-UseOledbStreaming**  
 指定した場合、BLOB データをストリームとしてバインドできるようになります。 ストリームが使用されるしきい値 (バイト サイズ) を指定するには、 **-OledbStreamThreshold** を使用します。  
  
## <a name="remarks"></a>コメント  
  
> [!IMPORTANT]  
>  ドメイン ユーザー アカウント (既定値) ではなくローカル システム アカウントで実行するように [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントをインストールした場合、サービスはローカル コンピューターにのみアクセスできます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスへのログイン時に、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]エージェントの下で実行するディストリビューション エージェントで、Windows 認証モードを使用するように構成すると、ディストリビューション エージェントは失敗します。 既定の設定は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証です。 セキュリティ アカウント変更の詳細については、「 [View and Modify Replication Security Settings](../security/view-and-modify-replication-security-settings.md)」を参照してください。  
  
 ディストリビューション エージェントを起動するには、コマンド プロンプトから **distrib.exe** を実行します。 詳細については、「[レプリケーション エージェント実行可能ファイルの概念](../concepts/replication-agent-executables-concepts.md)」を参照してください。  
  
## <a name="change-history"></a>変更履歴  
  
|変更内容|  
|---------------------|  
|**-ExtendedEventConfigFile** パラメーターを追加しました。|  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェントの管理](replication-agent-administration.md)  
  
  
