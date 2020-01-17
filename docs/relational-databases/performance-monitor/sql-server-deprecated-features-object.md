---
title: SQL Server:Deprecated Features オブジェクト | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Deprecated Features
- performance counters [SQL Server], deprecated features
- deprecation [SQL Server], performance counters
- Deprecated Features object
ms.assetid: e95de9d6-c950-41cd-8aaa-be529c6de198
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 2dd802097e083adb633549174dbc420b5967fb10
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093590"
---
# <a name="sql-server-deprecated-features-object"></a>SQL Server:Deprecated Features オブジェクト
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の SQLServer:Deprecated Features オブジェクトには、非推奨に指定された機能を監視するためのカウンターがあります。 いずれの場合も、このカウンターは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が最後に起動してから非推奨の機能が検出された回数を示す使用カウントを表示します。  
  
 これらのカウンターの値は、次のステートメントを実行して入手することもできます。  
  
```  
SELECT * FROM sys.dm_os_performance_counters   
WHERE object_name = 'SQLServer:Deprecated Features';  
```  

次の表に、SQL Server **Deprecated Features** パフォーマンス オブジェクトの説明を示します。

|**SQL Server:Deprecated Features カウンター**|Description|  
|-------------|-----------------|  
|**使用方法**|SQL Server の前回起動以降の機能の使用状況。|
  
 次の表に、SQL Server Deprecated Features カウンター インスタンスの説明を示します。  
  
|SQL Server Deprecated Features カウンター インスタンス|Description|  
|------------------------------------------------------|-----------------|  
|'#' および ' ##' 一時テーブルおよびストアド プロシージャの名前として|# 以外の文字を含んでいない識別子が見つかりました。 別の文字を少なくとも 1 文字は使用してください。 コンパイルごとに 1 回発生します。|  
|'::' 関数呼び出し構文|テーブル値関数で :: 関数呼び出し構文が見つかりました。 `SELECT column_list FROM` *< function_name>* `()` に置き換えてください。 たとえば、`SELECT * FROM ::fn_virtualfilestats(2,1)` は `SELECT * FROM sys.fn_virtualfilestats(2,1)` に置き換わります。 コンパイルごとに 1 回発生します。|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 識別子としての '\@' と '\@\@' で始まる名前|\@ または \@\@ で始まる識別子が見つかりました。 \@、\@v@、または \@\@ で始まる名前を識別子として使用しないでください。 コンパイルごとに 1 回発生します。|  
|ADDING TAPE DEVICE|非推奨の機能 sp_addumpdevice'**tape**' が見つかりました。 代わりに、sp_addumpdevice'**disk**' を使用してください。 使用するごとに 1 回発生します。|  
|ALL 権限|GRANT ALL、DENY ALL、または REVOKE ALL 構文が見つかった合計回数。 特定の権限を拒否するように構文を変更してください。 クエリごとに 1 回発生します。|  
|ALTER DATABASE WITH TORN_PAGE_DETECTION|サーバー インスタンスの起動後に、ALTER DATABASE の非推奨の機能 TORN_PAGE_DETECTION オプションが使用された合計回数。 代わりに、PAGE_VERIFY 構文を使用してください。 DDL ステートメントで使用するごとに 1 回発生します。|  
|ALTER LOGIN WITH SET CREDENTIAL|非推奨の機能の構文 ALTER LOGIN WITH SET CREDENTIAL または ALTER LOGIN WITH NO CREDENTIAL が見つかりました。 代わりに、ADD または DROP CREDENTIAL 構文を使用してください。 コンパイルごとに 1 回発生します。|  
|Azeri_Cyrilllic_90|イベントは、データベースを起動するごとに 1 回、および照合順序を使用するごとに 1 回発生します。 この照合順序を使用するアプリケーションの変更を計画してください。|  
|Azeri_Latin_90|イベントは、データベースを起動するごとに 1 回、および照合順序を使用するごとに 1 回発生します。 この照合順序を使用するアプリケーションの変更を計画してください。|  
|BACKUP DATABASE または LOG TO TAPE|非推奨の機能 BACKUP { DATABASE &#124; LOG } TO TAPE または BACKUP { DATABASE &#124; LOG } TO *device_that_is_a_tape* が見つかりました。<br /><br /> 代わりに、BACKUP { DATABASE &#124; LOG } TO DISK または BACKUP { DATABASE &#124; LOG } TO *device_that_is_a_disk* を使用してください。 使用するごとに 1 回発生します。|  
|BACKUP DATABASE または LOG WITH MEDIAPASSWORD|非推奨の機能 BACKUP DATABASE WITH MEDIAPASSWORD または BACKUP LOG WITH MEDIAPASSWORD が見つかりました。 WITH MEDIAPASSWORD は使用しないでください。|  
|BACKUP DATABASE または LOG WITH PASSWORD|非推奨の機能 BACKUP DATABASE WITH PASSWORD または BACKUP LOG WITH PASSWORD が見つかりました。 WITH PASSWORD は使用しないでください。|  
|COMPUTE [BY]|COMPUTE または COMPUTE BY 構文が見つかりました。 ROLLUP を指定した GROUP BY を使用してクエリを書き直してください。 コンパイルごとに 1 回発生します。|  
|CREATE FULLTEXT CATLOG IN PATH|IN PATH 句を指定した CREATE FULLTEXT CATLOG ステートメントが見つかりました。 この句は、このバージョンの SQL Server では無効です。 使用するごとに 1 回発生します。|  
|CREATE TRIGGER WITH APPEND|WITH APPEND 句を指定した CREATE TRIGGER ステートメントが見つかりました。 代わりに、トリガー全体を再作成してください。 DDL ステートメントで使用するごとに 1 回発生します。|  
|CREATE_DROP_DEFAULT|CREATE DEFAULT または DROP DEFAULT 構文が見つかりました。 CREATE TABLE または ALTER TABLE の DEFAULT オプションを使用してコマンドを書き直してください。 コンパイルごとに 1 回発生します。|  
|CREATE_DROP_RULE|CREATE RULE 構文が見つかりました。 制約を使用してコマンドを書き直してください。 コンパイルごとに 1 回発生します。|  
|データ型 : text、ntext、または image|**text**、 **ntext**、 **image** データ型が見つかりました。 **varchar(max)** データ型を使うようにアプリケーションを書き直し、 **text**、 **ntext**、 **image** データ型の構文は削除してください。 クエリごとに 1 回発生します。|  
||データベースが互換性レベル 80 に変更された合計回数。 次のリリースの前にデータベースおよびアプリケーションのアップグレードを計画してください。 互換性レベルが 80 のデータベースが起動されるときにも発生します。|  
|データベース互換性レベル 100、110。 120|データベース互換性レベルが変更された合計回数。 今後のリリースでデータベースおよびアプリケーションのアップグレードを計画してください。 また、非推奨の互換性レベルでデータベースが起動されたときにも発生します。|  
|DATABASE_MIRRORING|データベース ミラーリング機能への参照が発生しました。 Always On 可用性グループにアップグレードすることを検討するか、Always On 可用性グループがサポートされないエディションの SQL Server を実行している場合は、ログ配布に移行するようにしてください。|  
|database_principal_aliases|非推奨の sys.database_principal_aliases への参照が見つかりました。 別名の代わりにロールを使用してください。 コンパイルごとに 1 回発生します。|  
|DATABASEPROPERTY|ステートメントで DATABASEPROPERTY が参照されています。 ステートメント DATABASEPROPERTY を DATABASEPROPERTYEX に更新してください。 コンパイルごとに 1 回発生します。|  
|DATABASEPROPERTYEX('IsFullTextEnabled')|ステートメントで DATABASEPROPERTYEX IsFullTextEnabled プロパティが参照されています。 このプロパティの値は無効です。 ユーザー データベースでは、常にフルテキスト検索が有効になっています。 このプロパティは使用しないでください。 コンパイルごとに 1 回発生します。|  
|DBCC [UN]PINTABLE|DBCC PINTABLE または DBCC UNPINTABLE ステートメントが見つかりました。 このステートメントは無効なので、削除してください。 クエリごとに 1 回発生します。|  
|DBCC DBREINDEX|DBCC DBREINDEX ステートメントが見つかりました。 ALTER INDEX の REBUILD オプションを使用してステートメントを書き直してください。 クエリごとに 1 回発生します。|  
|DBCC INDEXDEFRAG|DBCC INDEXDEFRAG ステートメントが見つかりました。 ALTER INDEX の REORGANIZE オプションを使用してステートメントを書き直してください。 クエリごとに 1 回発生します。|  
|DBCC SHOWCONTIG|DBCC SHOWCONTIG ステートメントが見つかりました。 この情報については、sys.dm_db_index_physical_stats をクエリしてください。 クエリごとに 1 回発生します。|  
|既定値としての DEFAULT キーワード|既定値として DEFAULT キーワードを使用する構文が見つかりました。 使用しないでください。 コンパイルごとに 1 回発生します。|  
|非推奨の暗号化アルゴリズム|非推奨の暗号化アルゴリズム rc4 は、SQL Server の次のバージョンで削除されます。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションでは変更を検討してください。 RC4 アルゴリズムは弱いアルゴリズムで、旧バージョンとの互換性のためにのみサポートされています。 データベース互換性レベルが 90 または 100 の場合、新しい素材は RC4 または RC4_128 を使用してのみ暗号化できます (非推奨)。AES アルゴリズムのいずれかなど、新しいアルゴリズムを使用してください。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降では、どの互換性レベルでも、RC4 または RC4_128 を使用して暗号化された素材を暗号化解除できます。|  
|非推奨のハッシュ アルゴリズム|MD2、MD4、MD5、SHA、SHA1 アルゴリズムの使用。|  
|DESX アルゴリズム|DESX 暗号化アルゴリズムを使用する構文が見つかりました。 別の暗号化アルゴリズムを使用してください。 コンパイルごとに 1 回発生します。|  
|dm_fts_active_catalogs|sys.dm_fts_active_catalogs ビューの列の中には非推奨ではないものもあるので、dm_fts_active_catalogs カウンターは常に 0 のままです。 非推奨の列を監視するには、dm_fts_active_catalogs.is_paused などの列固有のカウンターを使用してください。|  
|dm_fts_active_catalogs.is_paused|[sys.dm_fts_active_catalogs](../../relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql.md) 動的管理ビューの is_paused 列が見つかりました。 この列は使用しないでください。 サーバー インスタンスによって列への参照が検出されるたびに発生します。|  
|dm_fts_active_catalogs.previous_status|sys.dm_fts_active_catalogs 動的管理ビューの previous_status 列が見つかりました。 この列は使用しないでください。 サーバー インスタンスによって列への参照が検出されるたびに発生します。|  
|dm_fts_active_catalogs.previous_status_description|sys.dm_fts_active_catalogs 動的管理ビューの previous_status_description 列が見つかりました。 この列は使用しないでください。 サーバー インスタンスによって列への参照が検出されるたびに発生します。|  
|dm_fts_active_catalogs.row_count_in_thousands|sys.dm_fts_active_catalogs 動的管理ビューの row_count_in_thousands 列が見つかりました。 この列は使用しないでください。 サーバー インスタンスによって列への参照が検出されるたびに発生します。|  
|dm_fts_active_catalogs.status|sys.dm_fts_active_catalogs 動的管理ビューの status 列が見つかりました。 この列は使用しないでください。 サーバー インスタンスによって列への参照が検出されるたびに発生します。|  
|dm_fts_active_catalogs.status_description|sys.dm_fts_active_catalogs 動的管理ビューの status_description 列が見つかりました。 この列は使用しないでください。 サーバー インスタンスによって列への参照が検出されるたびに発生します。|  
|dm_fts_active_catalogs.worker_count|sys.dm_fts_active_catalogs 動的管理ビューの worker_count 列が見つかりました。 この列は使用しないでください。 サーバー インスタンスによって列への参照が検出されるたびに発生します。|  
|dm_fts_memory_buffers|sys.dm_fts_memory_buffers ビューのほとんどの列が非推奨ではないので、dm_fts_memory_buffers カウンターは常に 0 のままです。 非推奨の列を監視するには、列固有のカウンター dm_fts_memory_buffers.row_count を使用してください。|  
|dm_fts_memory_buffers.row_count|[sys.dm_fts_memory_buffers](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md) 動的管理ビューの row_count 列が見つかりました。 この列は使用しないでください。 サーバー インスタンスによって列への参照が検出されるたびに発生します。|  
|2 部構成の名前が使用された DROP INDEX|DROP INDEX 構文で、DROP INDEX に *table_name.index_name* 形式の構文が含まれています。 DROP INDEX ステートメントで、 *index_name* ON *table_name* 構文に置き換えてください。 コンパイルごとに 1 回発生します。|  
|EXT_CREATE_ALTER_SOAP_ENDPOINT|FOR SOAP オプションを指定した CREATE または ALTER ENDPOINT ステートメントが見つかりました。 ネイティブ XML Web サービスは非推奨とされます。 代わりに Windows Communications Foundation (WCF) または ASP.NET を使用してください。|  
|EXT_endpoint_webmethods|sys.endpoint_webmethods が見つかりました。 ネイティブ XML Web サービスは非推奨とされます。 代わりに Windows Communications Foundation (WCF) または ASP.NET を使用してください。|  
|EXT_soap_endpoints|sys.soap_endpoints が見つかりました。 ネイティブ XML Web サービスは非推奨とされます。 代わりに Windows Communications Foundation (WCF) または ASP.NET を使用してください。|  
|EXTPROP_LEVEL0TYPE|TYPE が level0type で見つかりました。 level0type として SCHEMA、level1type として TYPE を使用してください。 クエリごとに 1 回発生します。|  
|EXTPROP_LEVEL0USER|level1type も指定されている場合に level0type USER が見つかりました。 USER は、拡張プロパティをユーザーに直接追加する場合にのみ level0type として使用してください。 クエリごとに 1 回発生します。|  
|FASTFIRSTROW|FASTFIRSTROW 構文が見つかりました。 OPTION (FAST *n*) 構文を使用してステートメントを書き直してください。 コンパイルごとに 1 回発生します。|  
|FILE_ID|FILE_ID 構文が見つかりました。 FILE_IDEX を使用してステートメントを書き直してください。 コンパイルごとに 1 回発生します。|  
|fn_get_sql|fn_get_sql 関数がコンパイルされました。 代わりに sys.dm_exec_sql_text を使用してください。 コンパイルごとに 1 回発生します。|  
|fn_servershareddrives|fn_servershareddrives 関数がコンパイルされました。 代わりに sys.dm_io_cluster_shared_drives を使用してください。 コンパイルごとに 1 回発生します。|  
|fn_virtualservernodes|fn_virtualservernodes 関数がコンパイルされました。 代わりに sys.dm_os_cluster_nodes を使用してください。 コンパイルごとに 1 回発生します。|  
|fulltext_catalogs|sys.fulltext_catalogs ビューの列の中には非推奨ではないものもあるので、fulltext_catalogs カウンターは常に 0 のままです。 非推奨の列を監視するには、fulltext_catalogs.data_space_id などの列固有のカウンターを使用してください。 サーバー インスタンスによって列への参照が検出されるたびに発生します。|  
|fulltext_catalogs.data_space_id|[sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) カタログ ビューの data_space_id 列が見つかりました。 この列は使用しないでください。 サーバー インスタンスによって列への参照が検出されるたびに発生します。|  
|fulltext_catalogs.file_id|sys.fulltext_catalogs カタログ ビューの file_id 列が見つかりました。 この列は使用しないでください。 サーバー インスタンスによって列への参照が検出されるたびに発生します。|  
|fulltext_catalogs.path|sys.fulltext_catalogs カタログ ビューの path 列が見つかりました。 この列は使用しないでください。 サーバー インスタンスによって列への参照が検出されるたびに発生します。|  
|FULLTEXTCATALOGPROPERTY('LogSize')|FULLTEXTCATALOGPROPERTY 関数の LogSize プロパティが見つかりました。 このプロパティは使用しないでください。|  
|FULLTEXTCATALOGPROPERTY('PopulateStatus')|FULLTEXTCATALOGPROPERTY 関数の PopulateStatus プロパティが見つかりました。 このプロパティは使用しないでください。|  
|FULLTEXTSERVICEPROPERTY('ConnectTimeout')|FULLTEXTSERVICEPROPERTY 関数の ConnectTimeout プロパティが見つかりました。 このプロパティは使用しないでください。|  
|FULLTEXTSERVICEPROPERTY('DataTimeout')|FULLTEXTSERVICEPROPERTY 関数の DataTimeout プロパティが見つかりました。 このプロパティは使用しないでください。|  
|FULLTEXTSERVICEPROPERTY('ResourceUsage')|FULLTEXTSERVICEPROPERTY 関数の ResourceUsage プロパティが見つかりました。 このプロパティは使用しないでください。|  
|GROUP BY ALL|GROUP BY ALL 構文が見つかった合計回数。 特定のテーブルをグループ化するように構文を変更してください。|  
|ヒンディー語|イベントは、データベースを起動するごとに 1 回、および照合順序を使用するごとに 1 回発生します。 この照合順序を使用するアプリケーションの変更を計画してください。 代わりに Indic_General_90 を使用してください。|  
|かっこのない HOLDLOCK テーブル ヒント||  
|IDENTITYCOL|IDENTITYCOL 構文が見つかりました。 $identity 構文を使用してステートメントを書き直してください。 コンパイルごとに 1 回発生します。|  
|COUNT_BIG(\*) がないインデックス付きビューの選択リスト|集計インデックス付きビューの選択リストには、COUNT_BIG (\*) を含める必要があります。|  
|INDEX_OPTION|オプションがかっこで囲まれていない CREATE TABLE、ALTER TABLE、または CREATE INDEX 構文が見つかりました。 現在の構文を使用してステートメントを書き直してください。 クエリごとに 1 回発生します。|  
|INDEXKEY_PROPERTY|INDEXKEY_PROPERTY 構文が見つかりました。 sys.index_columns をクエリするようにステートメントを書き直してください。 コンパイルごとに 1 回発生します。|  
|間接的な TVF ヒント|ビュー経由で複数ステートメントのテーブル値関数 (TVF) を呼び出す、テーブル ヒントの間接アプリケーションは、今後のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では削除される予定です。|  
|TIMESTAMP 列への INSERT NULL|TIMESTAMP 列に NULL 値が挿入されました。 代わりに既定値を使用してください。 コンパイルごとに 1 回発生します。|  
|INSERT_HINTS||  
|Korean_Wansung_Unicode|イベントは、データベースを起動するごとに 1 回、および照合順序を使用するごとに 1 回発生します。 この照合順序を使用するアプリケーションの変更を計画してください。|  
|Lithuanian_Classic|イベントは、データベースを起動するごとに 1 回、および照合順序を使用するごとに 1 回発生します。 この照合順序を使用するアプリケーションの変更を計画してください。|  
|Macedonian|イベントは、データベースを起動するごとに 1 回、および照合順序を使用するごとに 1 回発生します。 この照合順序を使用するアプリケーションの変更を計画してください。 代わりに Macedonian_FYROM_90 を使用してください。|  
|MODIFY FILEGROUP READONLY|MODIFY FILEGROUP READONLY 構文が見つかりました。 READ_ONLY 構文を使用してステートメントを書き直してください。 コンパイルごとに 1 回発生します。|  
|MODIFY FILEGROUP READWRITE|MODIFY FILEGROUP READWRITE 構文が見つかりました。 READ_WRITE 構文を使用してステートメントを書き直してください。 コンパイルごとに 1 回発生します。|  
|3 つ以上の部分で構成される列名|クエリの列リストで 3 部または 4 部構成の名前が使用されています。 標準に準拠した 2 部構成の名前を使用するようにクエリを変更してください。 コンパイルごとに 1 回発生します。|  
|コンマで区切られていない複数のテーブル ヒント|テーブル ヒントの区切り文字としてスペースが使用されています。 代わりにコンマを使用してください。 コンパイルごとに 1 回発生します。|  
|NOLOCK or READUNCOMMITTED in UPDATE or DELETE|UPDATE または DELETE ステートメントの FROM 句で、NOLOCK または READUNCOMMITTED が見つかりました。 FROM 句から NOLOCK または READUNCOMMITTED のテーブル ヒントを削除します。|  
|ANSI ではない外部結合演算子 *= または =\*|*= または =\* 結合構文を使用するステートメントが見つかりました。 ANSI 結合構文を使用してステートメントを書き直してください。 コンパイルごとに 1 回発生します。|  
|numbered_stored_procedures||  
|numbered_procedure_parameters|非推奨の sys.numbered_procedure_parameters への参照が見つかりました。 使用しないでください。 コンパイルごとに 1 回発生します。|  
|numbered_procedures|非推奨の sys.numbered_procedures への参照が見つかりました。 使用しないでください。 コンパイルごとに 1 回発生します。|  
|Oldstyle RAISEERROR|非推奨の RAISERROR (形式:RAISERROR 整数文字列) 構文が見つかりました。 現在の RAISERROR 構文を使用してステートメントを書き直してください。 コンパイルごとに 1 回発生します。|  
|アドホック接続の OLEDB|SQLOLEDB はサポートされないプロバイダーです。 アドホック接続には [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client を使用してください。|  
|PERMISSIONS|PERMISSIONS 組み込み関数への参照が見つかりました。 代わりに sys.fn_my_permissions をクエリしてください。 クエリごとに 1 回発生します。|  
|ProcNums|非推奨の ProcNums 構文が見つかりました。 参照を削除してステートメントを書き直してください。 コンパイルごとに 1 回発生します。|  
|READTEXT|READTEXT 構文が見つかりました。 **varchar(max)** データ型を使うようにアプリケーションを書き直し、 **text** データ型の構文は削除してください。 クエリごとに 1 回発生します。|  
|RESTORE DATABASE または LOG WITH DBO_ONLY|RESTORE ...WITH DBO_ONLY 構文が見つかりました。 代わりに RESTORE ...RESTRICTED_USER を使用してください。|  
|RESTORE DATABASE または LOG WITH MEDIAPASSWORD|RESTORE ...WITH MEDIAPASSWORD 構文が見つかりました。 WITH MEDIAPASSWORD を使用するとセキュリティが脆弱になるので、削除してください。|  
|RESTORE DATABASE または LOG WITH PASSWORD|RESTORE ...WITH PASSWORD 構文が見つかりました。 WITH PASSWORD を使用するとセキュリティが脆弱になるので、削除してください。|  
|トリガーから結果を返す|このイベントは、トリガーを呼び出すごとに 1 回発生します。 結果セットを返さないようにトリガーを書き直してください。|  
|ROWGUIDCOL|ROWGUIDCOL 構文が見つかりました。 $rowguid 構文を使用してステートメントを書き直してください。 コンパイルごとに 1 回発生します。|  
|SET ANSI_NULLS OFF|SET ANSI_NULLS OFF 構文が見つかりました。 この非推奨の構文を削除してください。 コンパイルごとに 1 回発生します。|  
|SET ANSI_PADDING OFF|SET ANSI_PADDING OFF 構文が見つかりました。 この非推奨の構文を削除してください。 コンパイルごとに 1 回発生します。|  
|SET CONCAT_NULL_YIELDS_NULL OFF|SET CONCAT_NULL_YIELDS_NULL OFF 構文が見つかりました。 この非推奨の構文を削除してください。 コンパイルごとに 1 回発生します。|  
|SET DISABLE_DEF_CNST_CHK|SET DISABLE_DEF_CNST_CHK 構文が見つかりました。 これは無効です。 この非推奨の構文を削除してください。 コンパイルごとに 1 回発生します。|  
|SET FMTONLY ON|SET FMTONLY 構文が見つかりました。 この非推奨の構文を削除してください。 コンパイルごとに 1 回発生します。|  
|SET OFFSETS|SET OFFSETS 構文が見つかりました。 この非推奨の構文を削除してください。 コンパイルごとに 1 回発生します。|  
|SET REMOTE_PROC_TRANSACTIONS|SET REMOTE_PROC_TRANSACTIONS 構文が見つかりました。 この非推奨の構文を削除してください。 代わりに、リンク サーバーと sp_serveroption を使用してください。|  
|SET ROWCOUNT|DELETE、INSERT、または UPDATE ステートメントで SET ROWCOUNT 構文が見つかりました。 TOP を使用してステートメントを書き直してください。 コンパイルごとに 1 回発生します。|  
|SETUSER|SET USER ステートメントが見つかりました。 代わりに EXECUTE AS を使用してください。 クエリごとに 1 回発生します。|  
|sp_addapprole|sp_addapprole プロシージャが見つかりました。 代わりに CREATE APPLICATION ROLE を使用してください。 クエリごとに 1 回発生します。|  
|sp_addextendedproc|sp_addextendedproc プロシージャが見つかりました。 代わりに CLR を使用してください。 コンパイルごとに 1 回発生します。|  
|sp_addlogin|sp_addlogin プロシージャが見つかりました。 代わりに CREATE LOGIN を使用してください。 クエリごとに 1 回発生します。|  
|sp_addremotelogin|sp_addremotelogin プロシージャが見つかりました。 代わりにリンク サーバーを使用してください。|  
|sp_addrole|sp_addrole プロシージャが見つかりました。 代わりに CREATE ROLE を使用してください。 クエリごとに 1 回発生します。|  
|sp_addserver|sp_addserver プロシージャが見つかりました。 代わりにリンク サーバーを使用してください。|  
|sp_addtype|sp_addtype プロシージャが見つかりました。 代わりに CREATE TYPE を使用してください。 コンパイルごとに 1 回発生します。|  
|sp_adduser|sp_adduser プロシージャが見つかりました。 代わりに CREATE USER を使用してください。 クエリごとに 1 回発生します。|  
|sp_approlepassword|sp_approlepassword プロシージャが見つかりました。 代わりに ALTER APPLICATION ROLE を使用してください。 クエリごとに 1 回発生します。|  
|sp_attach_db|sp_attach_db プロシージャが見つかりました。 代わりに CREATE DATABASE FOR ATTACH を使用してください。 クエリごとに 1 回発生します。|  
|sp_attach_single_file_db|sp_single_file_db プロシージャが見つかりました。 代わりに CREATE DATABASE FOR ATTACH_REBUILD_LOG を使用してください。 クエリごとに 1 回発生します。|  
|sp_bindefault|sp_bindefault プロシージャが見つかりました。 代わりに、ALTER TABLE または CREATE TABLE の DEFAULT キーワードを使用してください。 コンパイルごとに 1 回発生します。|  
|sp_bindrule|sp_bindrule プロシージャが見つかりました。 代わりに、CHECK 制約を使用してください。 コンパイルごとに 1 回発生します。|  
|sp_bindsession|sp_bindsession プロシージャが見つかりました。 代わりに、複数のアクティブな結果セット (MARS) または分散トランザクションを使用してください。 コンパイルごとに 1 回発生します。|  
|sp_certify_removable|sp_certify_removable プロシージャが見つかりました。 代わりに sp_detach_db を使用してください。 クエリごとに 1 回発生します。|  
|sp_changeobjectowner|sp_changeobjectowner プロシージャが見つかりました。 代わりに、ALTER SCHEMA または ALTER AUTHORIZATION を使用してください。 クエリごとに 1 回発生します。|  
|sp_change_users_login|sp_change_users_login プロシージャが見つかりました。 代わりに ALTER USER を使用してください。 クエリごとに 1 回発生します。|  
|sp_configure 'allow updates'|sp_configure の allow updates オプションが見つかりました。 システム テーブルは更新できなくなりました。 使用しないでください。 クエリごとに 1 回発生します。|  
|sp_configure 'disallow results from triggers'|sp_configure の disallow result sets from triggers オプションが見つかりました。 トリガーが結果セットを返さないようにするには、sp_configure を使用してこのオプションを 1 に設定してください。 クエリごとに 1 回発生します。|  
|sp_configure 'ft crawl bandwidth (max)'|sp_configure の ft crawl bandwidth (max) オプションが見つかりました。 使用しないでください。 クエリごとに 1 回発生します。|  
|sp_configure 'ft crawl bandwidth (min)'|sp_configure の ft crawl bandwidth (min) オプションが見つかりました。 使用しないでください。 クエリごとに 1 回発生します。|  
|sp_configure 'ft notify bandwidth (max)'|sp_configure の ft notify bandwidth (max) オプションが見つかりました。 使用しないでください。 クエリごとに 1 回発生します。|  
|sp_configure 'ft notify bandwidth (min)'|sp_configure の ft notify bandwidth (min) オプションが見つかりました。 使用しないでください。 クエリごとに 1 回発生します。|  
|sp_configure 'locks'|sp_configure の locks オプションが見つかりました。 ロックは構成できなくなりました。 使用しないでください。 クエリごとに 1 回発生します。|  
|sp_configure 'open objects'|sp_configure の open objects オプションが見つかりました。 開いているオブジェクトの数は構成できなくなりました。 使用しないでください。 クエリごとに 1 回発生します。|  
|sp_configure 'priority boost'|sp_configure の priority boost オプションが見つかりました。 使用しないでください。 クエリごとに 1 回発生します。 代わりに、Windows start /high ... program.exe オプションを使用してください。|  
|sp_configure 'remote proc trans'|sp_configure の remote proc trans オプションが見つかりました。 使用しないでください。 クエリごとに 1 回発生します。|  
|sp_configure 'set working set size'|sp_configure の set working set size オプションが見つかりました。 ワーキング セットのサイズは構成できなくなりました。 使用しないでください。 クエリごとに 1 回発生します。|  
|sp_control_dbmasterkey_password|sp_control_dbmasterkey_password ストアド プロシージャでは、マスター キーがあるかどうかは確認されません。 これは下位互換性を確保するために許容されていますが、警告が表示されます。 ただし、この動作は非推奨とされます。 今後のリリースでは、マスター キーは存在する必要があり、ストアド プロシージャ sp_control_dbmasterkey_password で使用されるパスワードはデータベース マスター キーを暗号化するために使用されるパスワードの 1 つと同じである必要があります。|  
|sp_create_removable|sp_create_removable プロシージャが見つかりました。 代わりに CREATE DATABASE を使用してください。 クエリごとに 1 回発生します。|  
|sp_db_vardecimal_storage_format|**vardecimal** ストレージ形式の使用が見つかりました。 代わりにデータ圧縮を使用してください。|  
|sp_dbcmptlevel|sp_dbcmptlevel プロシージャが見つかりました。 ALTER DATABASE ...SET COMPATIBILITY_LEVEL を使用してください。 クエリごとに 1 回発生します。|  
|sp_dbfixedrolepermission|sp_dbfixedrolepermission プロシージャが見つかりました。 使用しないでください。 クエリごとに 1 回発生します。|  
|sp_dboption|sp_dboption プロシージャが見つかりました。 代わりに、ALTER DATABASE および DATABASEPROPERTYEX を使用してください。 コンパイルごとに 1 回発生します。|  
|sp_dbremove|sp_dbremove プロシージャが見つかりました。 代わりに DROP DATABASE を使用してください。 クエリごとに 1 回発生します。|  
|sp_defaultdb|sp_defaultdb プロシージャが見つかりました。 代わりに ALTER LOGIN を使用してください。 コンパイルごとに 1 回発生します。|  
|sp_defaultlanguage|sp_defaultlanguage プロシージャが見つかりました。 代わりに ALTER LOGIN を使用してください。 コンパイルごとに 1 回発生します。|  
|sp_denylogin|sp_denylogin プロシージャが見つかりました。 代わりに ALTER LOGIN DISABLE を使用してください。 クエリごとに 1 回発生します。|  
|sp_depends|sp_depends プロシージャが見つかりました。 代わりに sys.dm_sql_referencing_entities および sys.dm_sql_referenced_entities を使用してください。 クエリごとに 1 回発生します。|  
|sp_detach_db \@keepfulltextindexfile|sp_detach_db ステートメントで \@keepfulltextindexfile 引数が見つかりました。 この引数は使用しないでください。|  
|sp_dropalias|sp_dropalias プロシージャが見つかりました。 別名をユーザー アカウントとデータベース ロールの組み合わせで置き換えてください。 アップグレードされたデータベースで別名を削除するには、sp_dropalias を使用します。 コンパイルごとに 1 回発生します。|  
|sp_dropapprole|sp_dropapprole プロシージャが見つかりました。 代わりに DROP APPLICATION ROLE を使用してください。 クエリごとに 1 回発生します。|  
|sp_dropextendedproc|sp_dropextendedproc プロシージャが見つかりました。 代わりに CLR を使用してください。 コンパイルごとに 1 回発生します。|  
|sp_droplogin|sp_droplogin プロシージャが見つかりました。 代わりに DROP LOGIN を使用してください。 クエリごとに 1 回発生します。|  
|sp_dropremotelogin|sp_dropremotelogin プロシージャが見つかりました。 代わりにリンク サーバーを使用してください。|  
|sp_droprole|sp_droprole プロシージャが見つかりました。 代わりに DROP ROLE を使用してください。 クエリごとに 1 回発生します。|  
|sp_droptype|sp_droptype プロシージャが見つかりました。 代わりに DROP TYPE を使用してください。|  
|sp_dropuser|sp_dropuser プロシージャが見つかりました。 代わりに DROP USER を使用してください。 クエリごとに 1 回発生します。|  
|sp_estimated_rowsize_reduction_for_vardecimal|**vardecimal** ストレージ形式の使用が見つかりました。 代わりにデータ圧縮と sp_estimate_data_compression_savings を使用してください。|  
|sp_fulltext_catalog|sp_fulltext_catalog プロシージャが見つかりました。 代わりに CREATE/ALTER/DROP FULLTEXT CATALOG を使用してください。 コンパイルごとに 1 回発生します。|  
|sp_fulltext_column|sp_fulltext_column プロシージャが見つかりました。 代わりに、ALTER FULLTEXT INDEX を使用してください。 コンパイルごとに 1 回発生します。|  
|sp_fulltext_database|sp_fulltext_database プロシージャが見つかりました。 代わりに ALTER DATABASE を使用してください。 コンパイルごとに 1 回発生します。|  
|sp_fulltext_service \@action=clean_up|sp_fulltext_service プロシージャの clean_up オプションが見つかりました。 クエリごとに 1 回発生します。|  
|sp_fulltext_service \@action=connect_timeout|sp_fulltext_service プロシージャの connect_timeout オプションが見つかりました。 クエリごとに 1 回発生します。|  
|sp_fulltext_service \@action=data_timeout|sp_fulltext_service プロシージャの data_timeout オプションが見つかりました。 クエリごとに 1 回発生します。|  
|sp_fulltext_service \@action=resource_usage|sp_fulltext_service プロシージャの resource_usage オプションが見つかりました。 このオプションには機能がありません。 クエリごとに 1 回発生します。|  
|sp_fulltext_table|sp_fulltext_table プロシージャが見つかりました。 代わりに CREATE/ALTER/DROP FULLTEXT INDEX を使用してください。 コンパイルごとに 1 回発生します。|  
|sp_getbindtoken|sp_getbindtoken プロシージャが見つかりました。 代わりに、複数のアクティブな結果セット (MARS) または分散トランザクションを使用してください。 コンパイルごとに 1 回発生します。|  
|sp_grantdbaccess|sp_grantdbaccess プロシージャが見つかりました。 代わりに CREATE USER を使用してください。 クエリごとに 1 回発生します。|  
|sp_grantlogin|sp_grantlogin プロシージャが見つかりました。 代わりに CREATE LOGIN を使用してください。 クエリごとに 1 回発生します。|  
|sp_help_fulltext_catalog_components|sp_help_fulltext_catalog_components プロシージャが見つかりました。 このプロシージャは空の行を返します。 このプロシージャは使用しないでください。 コンパイルごとに 1 回発生します。|  
|sp_help_fulltext_catalogs|sp_help_fulltext_catalogs プロシージャが見つかりました。 代わりに sys.fulltext_catalogs をクエリしてください。 コンパイルごとに 1 回発生します。|  
|sp_help_fulltext_catalogs_cursor|sp_help_fulltext_catalogs_cursor プロシージャが見つかりました。 代わりに sys.fulltext_catalogs をクエリしてください。 コンパイルごとに 1 回発生します。|  
|sp_help_fulltext_columns|sp_help_fulltext_columns プロシージャが見つかりました。 代わりに sys.fulltext_index_columns をクエリしてください。 コンパイルごとに 1 回発生します。|  
|sp_help_fulltext_columns_cursor|sp_help_fulltext_columns_cursor プロシージャが見つかりました。 代わりに sys.fulltext_index_columns をクエリしてください。 コンパイルごとに 1 回発生します。|  
|sp_help_fulltext_tables|sp_help_fulltext_tables プロシージャが見つかりました。 代わりに sys.fulltext_indexes をクエリしてください。 コンパイルごとに 1 回発生します。|  
|sp_help_fulltext_tables_cursor|sp_help_fulltext_tables_cursor プロシージャが見つかりました。 代わりに sys.fulltext_indexes をクエリしてください。 コンパイルごとに 1 回発生します。|  
|sp_helpdevice|sp_helpdevice プロシージャが見つかりました。 代わりに sys.backup_devices をクエリしてください。 クエリごとに 1 回発生します。|  
|sp_helpextendedproc|sp_helpextendedproc プロシージャが見つかりました。 代わりに CLR を使用してください。 コンパイルごとに 1 回発生します。|  
|sp_helpremotelogin|sp_helpremotelogin プロシージャが見つかりました。 代わりにリンク サーバーを使用してください。|  
|sp_indexoption|sp_indexoption プロシージャが見つかりました。 代わりに ALTER INDEX を使用してください。 コンパイルごとに 1 回発生します。|  
|sp_lock|sp_lock プロシージャが見つかりました。 代わりに sys.dm_tran_locks をクエリしてください。 クエリごとに 1 回発生します。|  
|sp_password|sp_password プロシージャが見つかりました。 代わりに ALTER LOGIN を使用してください。 クエリごとに 1 回発生します。|  
|sp_remoteoption|sp_remoteoption プロシージャが見つかりました。 代わりにリンク サーバーを使用してください。|  
|sp_renamedb|sp_renamedb プロシージャが見つかりました。 代わりに ALTER DATABASE を使用してください。 クエリごとに 1 回発生します。|  
|sp_resetstatus|sp_resetstatus プロシージャが見つかりました。 代わりに ALTER DATABASE を使用してください。 クエリごとに 1 回発生します。|  
|sp_revokedbaccess|sp_revokedbaccess プロシージャが見つかりました。 代わりに DROP USER を使用してください。 クエリごとに 1 回発生します。|  
|sp_revokelogin|sp_revokelogin プロシージャが見つかりました。 代わりに DROP LOGIN を使用してください。 クエリごとに 1 回発生します。|  
|sp_srvrolepermission|非推奨の sp_srvrolepermission プロシージャが見つかりました。 使用しないでください。 クエリごとに 1 回発生します。|  
|sp_unbindefault|sp_unbindefault プロシージャが見つかりました。 代わりに、CREATE TABLE または ALTER TABLE ステートメントで DEFAULT キーワードを使用してください。 コンパイルごとに 1 回発生します。|  
|sp_unbindrule|sp_unbindrule プロシージャが見つかりました。 ルールの代わりに CHECK 制約を使用してください。 コンパイルごとに 1 回発生します。|  
|SQL_AltDiction_CP1253_CS_AS|イベントは、データベースを起動するごとに 1 回、および照合順序を使用するごとに 1 回発生します。 この照合順序を使用するアプリケーションの変更を計画してください。|  
|列の別名としての文字列リテラル|SELECT ステートメントで列の別名として使用されている文字列を含む構文が見つかりました ( `'string' = expression`など)。 使用しないでください。 コンパイルごとに 1 回発生します。|  
|sys.sql_dependencies|sys.sql_dependencies への参照が見つかりました。 代わりに sys.sql_expression_dependencies を使用してください。 コンパイルごとに 1 回発生します。|  
|sysaltfiles|sysaltfiles への参照が見つかりました。 代わりに sys.master_files を使用してください。 コンパイルごとに 1 回発生します。|  
|syscacheobjects|syscacheobjects への参照が見つかりました。 代わりに sys.dm_exec_cached_plans、sys.dm_exec_plan_attributes、および sys.dm_exec_sql_text を使用してください。 コンパイルごとに 1 回発生します。|  
|syscolumns|syscolumns への参照が見つかりました。 代わりに sys.columns を使用してください。 コンパイルごとに 1 回発生します。|  
|syscomments|syscomments への参照が見つかりました。 代わりに sys.sql_modules を使用してください。 コンパイルごとに 1 回発生します。|  
|sysconfigures|sysconfigures テーブルへの参照が見つかりました。 代わりに sys.sysconfigures ビューを参照してください。 コンパイルごとに 1 回発生します。|  
|sysconstraints|sysconstraints への参照が見つかりました。代わりに sys.check_constraints、sys.default_constraints、sys.key_constraints、および sys.foreign_keys を使用してください。 コンパイルごとに 1 回発生します。|  
|syscurconfigs|syscurconfigs への参照が見つかりました。 代わりに sys.configurations を使用してください。 コンパイルごとに 1 回発生します。|  
|sysdatabases|sysdatabases への参照が見つかりました。 代わりに sys.databases を使用してください。 コンパイルごとに 1 回発生します。|  
|sysdepends|sysdepends への参照が見つかりました。 代わりに sys.sql_dependencies を使用してください。 コンパイルごとに 1 回発生します。|  
|sysdevices|sysdevices への参照が見つかりました。 代わりに sys.backup_devices を使用してください。 コンパイルごとに 1 回発生します。|  
|sysfilegroups|sysfilegroups への参照が見つかりました。 代わりに sys.filegroups を使用してください。 コンパイルごとに 1 回発生します。|  
|sysfiles|sysfiles への参照が見つかりました。 代わりに sys.database_files を使用してください。 コンパイルごとに 1 回発生します。|  
|sysforeignkeys|sysforeignkeys への参照が見つかりました。 代わりに sys.foreign_keys を使用してください。 コンパイルごとに 1 回発生します。|  
|sysfulltextcatalogs|sysfulltextcatalogs への参照が見つかりました。 代わりに sys.fulltext_catalogs を使用してください。 コンパイルごとに 1 回発生します。|  
|sysindexes|sysindexes への参照が見つかりました。 代わりに sys.indexes、sys.partitions、sys.allocation_units、および sys.dm_db_partition_stats を使用してください。 コンパイルごとに 1 回発生します。|  
|sysindexkeys|sysindexkeys への参照が見つかりました。 代わりに、sys.index_columns を使用してください。 コンパイルごとに 1 回発生します。|  
|syslockinfo|syslockinfo への参照が見つかりました。 代わりに sys.dm_tran_locks を使用してください。 コンパイルごとに 1 回発生します。|  
|syslogins|syslogins への参照が見つかりました。 代わりに sys.server_principals および sys.sql_logins を使用してください。 コンパイルごとに 1 回発生します。|  
|sysmembers|sysmembers への参照が見つかりました。 代わりに sys.database_role_members を使用してください。 コンパイルごとに 1 回発生します。|  
|sysmessages|sysmessages への参照が見つかりました。 代わりに sys.messages を使用してください。 コンパイルごとに 1 回発生します。|  
|sysobjects|sysobjects への参照が見つかりました。 代わりに sys.objects を使用してください。 コンパイルごとに 1 回発生します。|  
|sysoledbusers|sysoledbusers への参照が見つかりました。 代わりに sys.linked_logins を使用してください。 コンパイルごとに 1 回発生します。|  
|sysopentapes|sysopentapes への参照が見つかりました。 代わりに sys.dm_io_backup_tapes を使用してください。 コンパイルごとに 1 回発生します。|  
|sysperfinfo|sysperfinfo への参照が見つかりました。 代わりに、sys.dm_os_performance_counters を 使用します。 コンパイルごとに 1 回発生します。|  
|syspermissions|syspermissions への参照が見つかりました。 代わりに sys.database_permissions および sys.server_permissions を使用してください。 コンパイルごとに 1 回発生します。|  
|sysprocesses|sysprocesses への参照が見つかりました。 代わりに sys.dm_exec_connections、sys.dm_exec_sessions、および sys.dm_exec_requests を使用してください。 コンパイルごとに 1 回発生します。|  
|sysprotects|sysprotects への参照が見つかりました。 代わりに sys.database_permissions および sys.server_permissions を使用してください。 コンパイルごとに 1 回発生します。|  
|sysreferences|sysreferences への参照が見つかりました。 代わりに sys.foreign_keys を使用してください。 コンパイルごとに 1 回発生します。|  
|sysremotelogins|sysremotelogins への参照が見つかりました。 代わりに sys.remote_logins を使用してください。 コンパイルごとに 1 回発生します。|  
|sysservers|sysservers への参照が見つかりました。 代わりに sys.servers を使用してください。 コンパイルごとに 1 回発生します。|  
|systypes|systypes への参照が見つかりました。 代わりに sys.types を使用してください。 コンパイルごとに 1 回発生します。|  
|sysusers|sysusers への参照が見つかりました。 代わりに sys.database_principals を使用してください。 コンパイルごとに 1 回発生します。|  
|Table hint without WITH|テーブル ヒントを使用しているが WITH キーワードを使用していないステートメントが見つかりました。 WITH キーワードを含めるようにステートメントを変更してください。 コンパイルごとに 1 回発生します。|  
|Text in row テーブル オプション|'text in row' テーブル オプションへの参照が見つかりました。 代わりに sp_tableoption 'large value types out of row' を使用してください。 クエリごとに 1 回発生します。|  
|TEXTPTR|TEXTPTR 関数への参照が見つかりました。 **varchar(max)** データ型を使うようにアプリケーションを書き直し、 **text**、 **ntext**、 **image** データ型の構文は削除してください。 クエリごとに 1 回発生します。|  
|TEXTVALID|TEXTVALID 関数への参照が見つかりました。 **varchar(max)** データ型を使うようにアプリケーションを書き直し、 **text**、 **ntext**、 **image** データ型の構文は削除してください。 クエリごとに 1 回発生します。|  
|timestamp|非推奨の **timestamp** データ型が DDL ステートメントで見つかった合計回数。 代わりに **rowversion** データ型を使用してください。|  
|UPDATETEXT または WRITETEXT|UPDATETEXT または WRITETEXT ステートメントが見つかりました。 **varchar(max)** データ型を使うようにアプリケーションを書き直し、 **text**、 **ntext**、 **image** データ型の構文は削除してください。 クエリごとに 1 回発生します。|  
|USER_ID|USER_ID 関数への参照が見つかりました。 代わりに、DATABASE_PRINCIPAL_ID 関数を使用してください。 コンパイルごとに 1 回発生します。|  
|リンク サーバーに対する OLEDB の使用||  
|vardecimal ストレージ形式|**vardecimal** ストレージ形式の使用が見つかりました。 代わりにデータ圧縮を使用してください。|  
|XMLDATA|FOR XML 構文が見つかりました。 RAW モードと AUTO モードの場合は、XSD 世代を使用してください。 EXPLICIT モードに取って代わるものはありません。 コンパイルごとに 1 回発生します。|  
|XP_API|拡張ストアド プロシージャ ステートメントが見つかりました。 使用しないでください。|  
|xp_grantlogin|xp_grantlogin プロシージャが見つかりました。 代わりに CREATE LOGIN を使用してください。 コンパイルごとに 1 回発生します。|  
|xp_loginconfig|xp_loginconfig プロシージャが見つかりました。 代わりに SERVERPROPERTY の IsIntegratedSecurityOnly 引数を使用してください。 クエリごとに 1 回発生します。|  
|xp_revokelogin|xp_revokelogin プロシージャが見つかりました。 代わりに ALTER LOGIN DISABLE または DROP LOGIN を使用してください。 コンパイルごとに 1 回発生します。|  
  
## <a name="see-also"></a>参照  
 [SQL Server 2016 データベース エンジンの非推奨の機能](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2016 の非推奨のフルテキスト検索機能](../../relational-databases/search/deprecated-full-text-search-features-in-sql-server-2016.md)   
 [Deprecation Announcement イベント クラス](../../relational-databases/event-classes/deprecation-announcement-event-class.md)   
 [Deprecation Final Support イベント クラス](../../relational-databases/event-classes/deprecation-final-support-event-class.md)   
 [SQL Server 2016 で廃止されたデータベース エンジンの機能](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [SQL Server 2016 で廃止されたフルテキスト検索機能](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [SQL Server オブジェクトの使用](../../relational-databases/performance-monitor/use-sql-server-objects.md)  
  
  
