---
title: Oracle CDC データベース | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a96486e9-f79b-4b24-bfaf-56203dd0e435
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 35f07d23facba97288881d7ee3c011c368d4736a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771200"
---
# <a name="the-oracle-cdc-databases"></a>Oracle CDC データベース
  Oracle CDC インスタンスは、ターゲット [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの同名の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに関連付けられます。 このデータベースは、Oracle CDC データベース (または CDC データベース) と呼ばれます。  
  
 CDC データベースは、Oracle CDC デザイナー コンソールを使用して作成および構成されます。このデータベースには次の要素が含まれています。  
  
-   データベースで SQL Server CDC を有効にすると作成される `cdc` スキーマ。  
  
-   Oracle CDC インスタンスによって使用される一連の **cdc.xdbcdc_xxxx** テーブル。  
  
-   ソース Oracle データベースのキャプチャ対象テーブルの定義を含む一連の空のミラー テーブル。  
  
-   SQL Server CDC メカニズムによって生成される一連の変更テーブルと変更アクセス関数。これらは、通常の (Oracle 用ではない) SQL Server CDC で使用されるものと同じです。  
  
 初期状態で `cdc` スキーマにアクセスできるのは、 **dbowner** 固定データベース ロールのメンバーだけです。 変更テーブルと変更関数へのアクセスは、SQL Server CDC と同じセキュリティ モデルによって決まります。 このセキュリティ モデルの詳細については、「 [セキュリティ モデル](https://go.microsoft.com/fwlink/?LinkId=231151)」を参照してください。  
  
## <a name="creating-the-cdc-database"></a>CDC データベースの作成  
 CDC データベースは、CDC デザイナー コンソールを使用して作成されるのが一般的ですが、CDC デザイナー コンソールを使用して生成される CDC 配置スクリプトを使用して作成することもできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のシステム管理者は、このデータベースの設定を必要に応じて変更できます (ストレージ、セキュリティ、可用性のための項目の設定など)。  
  
 CDC デザイナー コンソールを使用してデータベース テーブルと必要なスクリプトを作成する方法の詳細については、「 [新しいインスタンス ウィザードの使用](use-the-new-instance-wizard.md)」を参照してください。  
  
## <a name="cdc-database-user-roles"></a>CDC データベース ユーザーのロール  
 CDC データベースを作成して CDC を有効にすると、CDC データベースに **cdc_service** という名前のデータベース ユーザーが作成され、Oracle CDC Service の構成に使用された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインに関連付けられます。 このユーザーは、 **db_datareader**、 **db_datawriter**、および **db_ddladmin** の各データベース ロールのメンバーになります。 その [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインが `dbo` ユーザーにも関連付けられている場合は、 **cdc_service** は作成されません。  
  
 このロールの割り当てにより、Oracle CDC Service が、キャプチャされたデータと制御情報で `cdc` スキーマのテーブルを更新できるようになります。  
  
 CDC データベースが作成され、CDC ソース Oracle テーブルが設定されたら、CDC データベースの所有者は、ミラー テーブルの SELECT 権限を付与したり、SQL Server CDC ゲーティング ロールを定義したりして、変更データにアクセスできるユーザーを制御できます。  
  
## <a name="mirror-tables"></a>ミラー テーブル  
 Oracle ソース データベースの各キャプチャ対象テーブル (\<schema-name>.\<table-name>) に対して、同じスキーマ名とテーブル名を持つ同様の空のテーブルが CDC データベースに作成されます。 スキーマ名が `cdc` (大文字と小文字は区別されません) の Oracle ソース テーブルはキャプチャできません。 `cdc` の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スキーマは SQL Server CDC のために予約されているためです。  
  
 ミラー テーブルは空です。データは格納されていません。 ミラー テーブルは、Oracle CDC インスタンスによって使用される標準の SQL Server CDC インフラストラクチャを有効にするために使用されます。 ミラー テーブルに対してデータの挿入や更新が行われないようにするために、UPDATE、DELETE、および INSERT のすべての操作が PUBLIC に対して拒否されます。 これにより、ミラー テーブルを変更できないことが保証されます。  
  
## <a name="access-to-change-data"></a>変更データへのアクセス  
 キャプチャ インスタンスに関連付けられている変更データへのアクセスは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセキュリティ モデルによって制御されます。このセキュリティ モデルでは、ユーザーが変更データにアクセスするには、関連付けられているミラー テーブルのすべてのキャプチャ対象列に対する `select` アクセスが許可されている必要があります (元の Oracle テーブルへのアクセスが許可されていても、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の変更テーブルにはアクセスできません)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセキュリティ モデルについては、「 [セキュリティ モデル](https://go.microsoft.com/fwlink/?LinkId=231151)」を参照してください。  
  
 また、キャプチャ インスタンスの作成時にゲーティング ロールが指定されている場合、呼び出し元は、指定されたゲーティング ロールのメンバーである必要もあります。 メタデータにアクセスするためのその他の一般的な変更データ キャプチャ関数には、PUBLIC ロールですべてのデータベース ユーザーがアクセスできます。ただし、通常、返されるメタデータへのアクセスは、基になるソース テーブルに対する select アクセス、および定義されたすべてのゲーティング ロールのメンバーシップに基づいて制限されます。  
  
 変更データを読み取るには、キャプチャ インスタンスの作成時に SQL Server の CDC コンポーネントによって生成される特殊なテーブル ベース関数を呼び出します。 この関数の詳細については、「 [変更データ キャプチャの関数 (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=231152)」を参照してください。  
  
 これらの規則は、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の CDC ソース コンポーネントから CDC データにアクセスする場合にも適用されます。  
  
## <a name="the-cdc-database-tables"></a>CDC データベースのテーブル  
 ここでは、CDC データベースの以下のテーブルについて説明します。  
  
-   [変更テーブル (_CT)](the-oracle-cdc-databases.md#bkmk_change_tables_ct)  
  
-   [cdc.lsn_time_mapping](the-oracle-cdc-databases.md#bkmk_cdclsn_time_mapping)  
  
-   [cdc.xdbcdc_config](the-oracle-cdc-databases.md#bkmk_cdcxdbcdc_config)  
  
-   [cdc.xdbcdc_state](the-oracle-cdc-databases.md#bkmk_cdcxdbcdc_state)  
  
-   [cdc.xdbcdc_trace](the-oracle-cdc-databases.md#bkmk_cdcxdbcdc_trace)  
  
-   [cdc.xdbcdc_staged_transactions](the-oracle-cdc-databases.md#bkmk_cdcxdbcdc_staged_transactions)  
  
###  <a name="bkmk_change_tables_ct"></a> 変更テーブル (_CT)  
 変更テーブルは、ミラー テーブルから作成されます。 変更テーブルには、Oracle データベースからキャプチャされた変更データが含まれます。 テーブルは、次の規則に従って命名されます。  
  
 **[cdc].[\<capture-instance>_CT]**  
  
 テーブル `<schema-name>.<table-name>`に対して最初にキャプチャを有効にしたときの既定のキャプチャ インスタンス名は、 `<schema-name>_<table-name>`です。 たとえば、Oracle HR.EMPLOYEES テーブルの既定のキャプチャ インスタンス名は HR_EMPLOYEES で、関連付けられる変更テーブルは [cdc]. [HR_EMPLOYEES_CT] です。  
  
 キャプチャ テーブルは、Oracle CDC インスタンスによって書き込まれ、 キャプチャ インスタンスの作成時に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって生成される特殊なテーブル値関数を使用して読み取られます たとえば、 `fn_cdc_get_all_changes_HR_EMPLOYEES`のようにします。 これらの CDC 関数の詳細については、「 [変更データ キャプチャの関数 (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=231152)」を参照してください。  
  
###  <a name="bkmk_cdclsn_time_mapping"></a> cdc.lsn_time_mapping  
 **[cdc].[lsn_time_mapping]** テーブルは、SQL Server の CDC コンポーネントによって生成されます。 Oracle CDC の場合、このテーブルの使用方法が通常とは異なります。  
  
 Oracle CDC の場合、このテーブルに格納されている LSN 値は、変更に関連付けられている Oracle システム変更番号 (SCN) の値に基づいています。 LSN 値の最初の 6 バイトは、元の Oracle SCN 番号です。  
  
 また、Oracle CDC を使用する場合は、時刻の列 (`tran_begin_time` および `tran_end_time`) に格納される変更の時刻が UTC 時刻になります (通常の SQL Server CDC ではローカル時刻が格納されます)。 これにより、lsn_time_mapping に格納されているデータが夏時間の変化による影響を受けないことが保証されます。  
  
###  <a name="bkmk_cdcxdbcdc_config"></a> cdc.xdbcdc_config  
 このテーブルには、Oracle CDC インスタンスの構成データが含まれています。 このテーブルは、CDC デザイナー コンソールを使用して更新されます。 このテーブルに含まれる行は 1 つだけです。  
  
 次の表に、 **cdc.xdbcdc_config** テーブルの列を示します。  
  
|アイテム|説明|  
|----------|-----------------|  
|version|CDC インスタンスの構成のバージョンを追跡します。 このテーブルが更新されたり、キャプチャ インスタンスが追加または削除されたりするたびに更新されます。|  
|connect_string|Oracle の接続文字列です。 基本的な例を以下に示します。<br /><br /> `<server>:<port>/<instance>` (例: `erp.contoso.com:1521/orcl`)<br /><br /> 接続文字列で Oracle Net 接続記述子を指定することもできます (例: `(DESCRIPTION=(ADDRESS=(PROTOCOL=tcp) (HOST=erp.contoso.com) (PORT=1521)) (CONNECT_DATA=(SERVICE_NAME=orcl)))`)。<br /><br /> ディレクトリ サーバーまたは tnsnames を使用している場合は、接続文字列を接続の名前にすることができます。<br /><br /> Oracle の接続文字列の詳細については、[https://go.microsoft.com/fwlink/?LinkId=231153](https://go.microsoft.com/fwlink/?LinkId=231153) を参照してください。Oracle CDC Service によって使用される Oracle Instant Client の Oracle データベース接続文字列について詳しく説明されています。|  
|use_windows_authentication|次のいずれかのブール値です。<br /><br /> **0**:認証のために Oracle のユーザー名とパスワードを指定します (既定値)。<br /><br /> **1**:Windows 認証を使用して Oracle データベースに接続します。 このオプションは、Oracle データベースが Windows 認証と連動するように構成されている場合にのみ使用できます。|  
|username|ログ マイニング Oracle データベース ユーザーの名前です。 **use_windows_authentication = 0**の場合のみ必須です。|  
|パスワード|ログ マイニング Oracle データベース ユーザーのパスワードです。 **use_windows_authentication = 0**の場合のみ必須です。|  
|transaction_staging_timeout|メモリに保持されている、コミットされていない Oracle トランザクションが **cdc.xdbcdc_staged_transactions** テーブルに書き込まれるまでの時間 (秒) です。 既定値は 120 秒です。|  
|memory_limit|データをメモリにキャッシュするために使用できるメモリの量の上限 (MB) です。 この値を低くすると、 **cdc.xdbcdc_staged_transactions** テーブルに書き込まれるトランザクションが増加します。 既定値は 50 MB です。|  
|オプション|name[=value][; ] という形式のオプションのリストです。二次的なオプション (トレース、チューニングなど) を指定するために使用されます。 使用できるオプションについては、次の表を参照してください。|  
  
 次の表では、使用可能なオプションについて説明しています。  
  
|名前|既定|Min|Max|静的|説明|  
|----------|-------------|---------|---------|------------|-----------------|  
|trace|False|-|-|False|使用可能な値:<br /><br /> **True**<br /><br /> **False**<br /><br /> **on**<br /><br /> **off**|  
|cdc_update_state_interval|10|1|120|False|トランザクションに割り当てられるメモリのチャンクのサイズ (KB) です (トランザクションは複数のチャンクを割り当てることができます)。 [cdc.xdbcdc_config](the-oracle-cdc-databases.md#bkmk_cdcxdbcdc_config) テーブルの memory_limit 列を参照してください。|  
|target_max_batched_transactions|100|1|1000|True|SQL Server の CT テーブルの更新で 1 つのトランザクションとして処理できる Oracle トランザクションの最大数です。|  
|target_idle_lsn_update_interval|10|0|1|False|キャプチャ対象テーブルで操作が行われていない場合に **lsn_time_mapping** テーブルを更新する間隔 (秒) です。|  
|trace_retention_period|24|1|24*31|False|メッセージをトレース テーブルに保持する時間 (時間) です。|  
|sql_reconnect_interval|2|2|3600|False|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]への再接続が行われるまでの時間 (秒) です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントの接続のタイムアウトに加えて使用されます。|  
|sql_reconnect_limit|-1|-1|-1|False|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への再接続の最大回数です。 既定値 -1 は、プロセスが停止するまで再接続しようとすることを意味します。|  
|cdc_restart_limit|6|-1|3600|False|ほとんどの場合、CDC サービスは、異常終了した CDC インスタンスを自動的に再起動します。 このプロパティは、1 時間に何回失敗したらインスタンスの再起動を中止するかを定義します。 値 -1 は、インスタンスが常に再起動されることを意味します。<br /><br /> 構成テーブルが更新された場合は、インスタンスの再起動が再開されます。|  
|cdc_memory_report|0|0|1000|False|パラメーターの値が変更された場合、CDC インスタンスは、トレース テーブルにそのメモリのレポートを出力します。|  
|target_command_timeout|600|1|3600|False|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を操作するコマンドのタイムアウトです。|  
|source_character_set|-|-|-|True|Oracle データベースのコード ページの代わりに使用する特定の Oracle エンコードを設定できます。 文字データで使用されている実際のエンコードが Oracle データベースのコード ページのエンコードと異なる場合に便利です。|  
|source_error_retry_interval|30|1|3600|False|接続エラー、システム テーブル間の同期の一時的な喪失など、いくつかのエラーで再試行の前に使用されます。|  
|source_prefetch_size|100|1|10000|True|プリフェッチ バッチのサイズです。|  
|source_max_tables_in_query|100|1|10000|True|WHERE 句のテーブルの最大数です。この数を超えると、テーブルをフィルター処理せずに Oracle ログが読み取られます。|  
|source_read_retry_interval|2|1|3600|False|ソースが Oracle トランザクション ログの読み取りを EOF で再試行するまでの時間です。|  
|source_reconnect_interval|30|1|3600|False|ソース データベースへの再接続が試行されるまでの時間 (秒) です。|  
|source_reconnect_limit|-1|-1||False|ソース データベースへの再接続の最大回数です。 既定値 -1 は、プロセスが停止するまで再接続しようとすることを意味します。|  
|source_command_timeout|30|1|3600|False|Oracle を操作する接続のタイムアウトです。|  
|source_connection_timeout|30|1|3600|False|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を操作する接続のタイムアウトです。|  
|trace_data_errors|True|-|-|False|Boolean です。 **True** は、データの変換と切り捨てのエラーをログに記録することを示します。|  
|CDC_stop_on_breaking_schema_changes|False|-|-|False|Boolean です。 **True** は、重大なスキーマ変更が検出されたときに停止することを示します。<br /><br /> **False** は、ミラー テーブルとキャプチャ インスタンスを削除することを示します。|  
|source_oracle_home||-|-|False|特定の Oracle ホーム パスか、CDC インスタンスが Oracle への接続に使用する Oracle ホーム名に設定できます。|  
  
###  <a name="bkmk_cdcxdbcdc_state"></a> cdc.xdbcdc_state  
 このテーブルには、Oracle CDC インスタンスの永続化された状態に関する情報が含まれています。 キャプチャ状態は、復旧およびフェールオーバーのシナリオで使用されるほか、状態の監視にも使用されます。  
  
 次の表に、 **cdc.xdbcdc_state** テーブルの列を示します。  
  
|アイテム|説明|  
|----------|-----------------|  
|status|現在の Oracle CDC インスタンスの現在の状態コードです。 CDC の現在の状態を表します。|  
|sub_status|現在の状態に関する追加情報を提供する二次的な状態です。|  
|active|次のいずれかのブール値です。<br /><br /> **0**:Oracle CDC インスタンス プロセスはアクティブではありません。<br /><br /> **1**:Oracle CDC インスタンス プロセスはアクティブです。|  
|error (エラー)|次のいずれかのブール値です。<br /><br /> **0**:Oracle CDC インスタンス プロセスはエラー状態ではありません。<br /><br /> **1**:Oracle CDC インスタンスはエラー状態です。|  
|status_message|エラーまたは状態の説明を表す文字列です。|  
|TIMESTAMP|キャプチャ状態が最後に更新された時刻 (UTC) のタイムスタンプです。|  
|active_capture_node|現在 Oracle CDC Service と (Oracle トランザクション ログを処理している) Oracle CDC インスタンスを実行しているホストの名前です (クラスターのノードの場合があります)。|  
|last_transaction_timestamp|変更テーブルに最後のトランザクションが書き込まれた時刻 (UTC) のタイムスタンプです。|  
|last_change_timestamp|最新の変更レコードがソース Oracle トランザクション ログから読み取られた時刻 (UTC) のタイムスタンプです。 このタイムスタンプは、CDC プロセスの現在の待機時間を識別するのに役立ちます。|  
|transaction_log_head_cn|Oracle トランザクション ログから読み取られた最新の変更番号 (CN) です。|  
|transaction_log_tail_cn|再起動や復旧が行われた場合に Oracle CDC インスタンスが戻される Oracle トランザクション ログの変更番号 (CN) です。|  
|current_cn|ソース データベースで確認されている最新の変更番号 (CN) です。|  
|software_version|Oracle CDC Service の内部バージョンです。|  
|completed_transactions|CDC が最後にリセットされた後に処理されたトランザクションの数です。|  
|written_changes|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の変更テーブルに書き込まれた変更レコードの数です。|  
|read_changes|ソース Oracle トランザクション ログから読み取られた変更レコードの数です。|  
|staged_transactions|**cdc.xdbcdc_staged_transactions** テーブルにステージングされている、現在アクティブなトランザクションの数です。|  
  
###  <a name="bkmk_cdcxdbcdc_trace"></a> cdc.xdbcdc_trace  
 このテーブルには、CDC インスタンスの操作に関する情報が含まれています。 このテーブルに格納される情報には、エラー レコード、重要な状態変更、トレース レコードが含まれます。 エラーの情報は、 **cdc.xcbcdc_trace** テーブルを使用できない場合にも使用できるように、Windows イベント ログにも書き込まれます。  
  
 次の表に、cdc.xdbcdc_trace テーブルの列を示します。  
  
|アイテム|説明|  
|----------|-----------------|  
|TIMESTAMP|トレース レコードが書き込まれたときの正確な UTC タイムスタンプ。|  
|型|次のいずれかの値が格納されます。<br /><br /> error<br /><br /> INFO<br /><br /> trace|  
|node|レコードが書き込まれたノードの名前。|  
|ステータス|状態テーブルで使用される状態コード。|  
|sub_status|状態テーブルで使用される副状態コード。|  
|status_message|状態テーブルで使用される状態メッセージ。|  
|data|エラー レコードまたはトレース レコードにペイロードが含まれている場合の追加データ (壊れたログ レコードなど)。|  
  
###  <a name="bkmk_cdcxdbcdc_staged_transactions"></a> cdc.xdbcdc_staged_transactions  
 このテーブルには、大きなトランザクションや実行時間の長いトランザクションの変更レコードが、トランザクションのコミットまたはロールバックのイベントがキャプチャされるまで格納されます。 キャプチャされたログ レコードは、まずトランザクションのコミット時間順に並べ替えられ、さらにトランザクションの発生順に並べ替えられます。 同じトランザクションのログ レコードは、トランザクションが終了するまでメモリに格納された後、ターゲット変更テーブルに書き込まれるか、破棄されます (ロールバックの場合)。 使用できるメモリの量は限られているため、大きなトランザクションは、完了するまで **cdc.xdbcdc_staged_transactions** テーブルに書き込まれます。 トランザクションは、実行時間が長い場合にもこのステージング テーブルに書き込まれます。 したがって、Oracle CDC インスタンスが再起動しても、Oracle トランザクション ログから古い変更を再び読み取る必要はありません。  
  
 次の表に、 **cdc.xdbcdc_staged_transactions** テーブルの列を示します。  
  
|アイテム|説明|  
|----------|-----------------|  
|transaction_id|ステージングされるトランザクションの一意なトランザクション識別子です。|  
|seq_num|現在のトランザクションの **xcbcdc_staged_transactions** 行の (0 から始まる) 番号です。|  
|data_start_cn|この行のデータの最初の変更の変更番号 (CN) です。|  
|data_end_cn|この行のデータの最後の変更の変更番号 (CN) です。|  
|data|トランザクションのステージングされた変更です (BLOB 形式)。|  
  
## <a name="see-also"></a>関連項目  
 [Attunity の Change Data Capture Designer for Oracle](change-data-capture-designer-for-oracle-by-attunity.md)  
