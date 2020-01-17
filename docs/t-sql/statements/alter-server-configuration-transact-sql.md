---
title: ALTER SERVER CONFIGURATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER SERVER CONFIGURATION
- ALTER_SERVER_CONFIGURATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SERVER CONFIGURATION, ALTER
- process affinity, setting
- ALTER SERVER CONFIGURATION statement
- setting process affinity
ms.assetid: f3059e42-5f6f-4a64-903c-86dca212a4b4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ef4bf385e2ce0ecd140ad402c43d0039669c56e8
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72006066"
---
# <a name="alter-server-configuration-transact-sql"></a>ALTER SERVER CONFIGURATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で現在のサーバーのグローバル構成設定を変更します。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  

```  
ALTER SERVER CONFIGURATION  
SET <optionspec>   
[;]  
  
<optionspec> ::=  
{  
     <process_affinity>  
   | <diagnostic_log>  
   | <failover_cluster_property>  
   | <hadr_cluster_context>  
   | <buffer_pool_extension>  
   | <soft_numa>  
   | <memory_optimized>
}  
  
<process_affinity> ::=   
   PROCESS AFFINITY   
   {  
     CPU = { AUTO | <CPU_range_spec> }   
   | NUMANODE = <NUMA_node_range_spec>   
   }  
   <CPU_range_spec> ::=   
      { CPU_ID | CPU_ID  TO CPU_ID } [ ,...n ]   
  
   <NUMA_node_range_spec> ::=   
      { NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID } [ ,...n ]  
  
<diagnostic_log> ::=   
   DIAGNOSTICS LOG   
   {   
     ON    
   | OFF    
   | PATH = { 'os_file_path' | DEFAULT }    
   | MAX_SIZE = { 'log_max_size' MB | DEFAULT }    
   | MAX_FILES = { 'max_file_count' | DEFAULT }    
   }  
  
<failover_cluster_property> ::=   
   FAILOVER CLUSTER PROPERTY <resource_property>  
   <resource_property> ::=  
      {  
        VerboseLogging = { 'logging_detail' | DEFAULT }    
      | SqlDumperDumpFlags = { 'dump_file_type' | DEFAULT }  
      | SqlDumperDumpPath = { 'os_file_path'| DEFAULT }  
      | SqlDumperDumpTimeOut = { 'dump_time-out' | DEFAULT }  
      | FailureConditionLevel = { 'failure_condition_level' | DEFAULT }  
      | HealthCheckTimeout = { 'health_check_time-out' | DEFAULT }  
      }  
  
<hadr_cluster_context> ::=  
   HADR CLUSTER CONTEXT = { 'remote_windows_cluster' | LOCAL }  
  
<buffer_pool_extension>::=  
    BUFFER POOL EXTENSION   
    { ON ( FILENAME = 'os_file_path_and_name' , SIZE = <size_spec> )   
    | OFF }  
  
    <size_spec> ::=  
        { size [ KB | MB | GB ] }  
  
<soft_numa> ::=  
    SOFTNUMA  
    { ON | OFF }  

<memory-optimized> ::=   
   MEMORY_OPTIMIZED   
   {   
     ON 
   | OFF
   | [ TEMPDB_METADATA = { ON [(RESOURCE_POOL='resource_pool_name')] | OFF }
   | [ HYBRID_BUFFER_POOL = { ON | OFF }
   }  
```  
  
## <a name="arguments"></a>引数  
**\<process_affinity> ::=**  
  
PROCESS AFFINITY  
CPU へのハードウェア スレッドの関連付けを有効にします。  
  
CPU = { AUTO | \<CPU_range_spec> }  
指定された範囲内の個々の CPU に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のワーカー スレッドを配分します。 指定された範囲外の CPU にはスレッドの割り当ては行われません。  
  
AUTO  
CPU へのスレッドの割り当てを一切行いません。 サーバーのワークロードに基づいて、オペレーティング システムが複数の CPU 間で自由にスレッドを移動できます。 これは既定の設定であり、推奨されます。  
  
\<CPU_range_spec> ::=  
スレッドを割り当てる CPU または CPU の範囲を指定します。  
  
{ CPU_ID | CPU_ID  TO  CPU_ID } [ ,...n ]  
1 つ以上の CPU の一覧を指定します。 CPU ID は 0 から始まる **integer** 値です。  
  
NUMANODE = \<NUMA_node_range_spec>  
指定された NUMA ノードまたはノードの範囲に属しているすべての CPU にスレッドを割り当てます。  
  
\<NUMA_node_range_spec> ::=  
NUMA ノードまたは NUMA ノードの範囲を指定します。  
  
{ NUMA_node_ID | NUMA_node_ID  TO NUMA_node_ID } [ ,...n ]  
1 つ以上の NUMA ノードの一覧を指定します。 NUMA ノード ID は 0 から始まる **integer** 値です。  
  
**\<diagnostic_log> ::=**  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降)。  

  
DIAGNOSTICS LOG  
sp_server_diagnostics プロシージャがキャプチャする診断データのログ記録を開始または停止します。 また、この引数はログ ファイルのロールオーバー回数、ログ ファイルのサイズ、ファイルの場所などの SQLDIAG ログ構成パラメーターを設定します。 詳細については、「 [フェールオーバー クラスター インスタンスの診断ログを表示して読む方法](../../sql-server/failover-clusters/windows/view-and-read-failover-cluster-instance-diagnostics-log.md)」を参照してください。  
  
ON  
PATH ファイル オプションで指定された場所に [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] による診断データのログ記録を開始します。 この引数が既定値です。  
  
OFF  
診断データのログ記録を停止します。  
  
PATH = { 'os_file_path' | DEFAULT }  
診断ログの場所を示すパス。 既定の場所は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスのインストール フォルダー内の \<\MSSQL\Log> です。  
  
MAX_SIZE = { 'log_max_size' MB | DEFAULT }  
各診断ログの最大サイズ (MB 単位)。 既定値は 100 MB です。  
  
MAX_FILES = { 'max_file_count' | DEFAULT }  
新しい診断ログとして再利用されるまでにコンピューターに格納できる診断ログ ファイルの最大数。  
  
**\<failover_cluster_property> ::=**  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降)。    
  
FAILOVER CLUSTER PROPERTY  
SQL Server リソース プライベート フェールオーバー クラスターのプロパティを変更します。  
  
VERBOSE LOGGING = { 'logging_detail' | DEFAULT }  
SQL Server フェールオーバー クラスタリングのログ記録レベルを設定します。 オンにすると、トラブルシューティングを目的とした詳細情報をエラー ログに追加できます。  
  
-   0: ログ記録はオフです (既定)  
  
-   1: エラーのみ。  
  
-   2: エラーおよび警告  
  
SQLDUMPEREDUMPFLAGS  
SQL Server の SQLDumper ユーティリティによって生成されるダンプ ファイルの種類を決定します。 既定の設定は 0 です。 詳細については、[SQL Server Dumper ユーティリティに関するサポート技術情報の資料](https://go.microsoft.com/fwlink/?LinkId=206173)を参照してください。  
  
SQLDUMPERDUMPPATH = { 'os_file_path' | DEFAULT }  
SQLDumper ユーティリティがダンプ ファイルを保存する場所。 詳細については、[SQL Server Dumper ユーティリティに関するサポート技術情報の資料](https://go.microsoft.com/fwlink/?LinkId=206173)を参照してください。  
  
SQLDUMPERDUMPTIMEOUT = { 'dump_time-out' | DEFAULT }  
SQL Server でエラーが発生した場合の、SQLDumper ユーティリティによるダンプの生成のタイムアウト値 (ミリ秒単位)。 既定値は 0 で、ダンプの完了に時間制限がないことを示します。 詳細については、[SQL Server Dumper ユーティリティに関するサポート技術情報の資料](https://go.microsoft.com/fwlink/?LinkId=206173)を参照してください。  
  
 FAILURECONDITIONLEVEL = { 'failure_condition_level' | DEFAULT }  
 SQL Server フェールオーバー クラスター インスタンスがフェイルオーバーまたは再起動する必要がある状態。 既定値は 3 で、重大なサーバー エラーの発生時に SQL Server リソースがフェールオーバーまたは再起動することを示します。 このエラー状態レベルおよび他のエラー状態レベルについて詳しくは、「[FailureConditionLevel プロパティ設定の構成](../../sql-server/failover-clusters/windows/configure-failureconditionlevel-property-settings.md)」をご覧ください。  
  
HEALTHCHECKTIMEOUT = { 'health_check_time-out' | DEFAULT }  
SQL Server データベース エンジンのリソース DLL が、サーバーの状態情報を待機する時間のタイムアウト値です。この待機時間を経過すると、SQL Server のインスタンスが応答不能と見なされます。 このタイムアウト値は、ミリ秒単位で指定します。 既定値は 60,000 ミリ秒 (60 秒) です。  
  
**\<hadr_cluster_context> ::=**  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降)。   
  
HADR CLUSTER CONTEXT **=** { **'** _remote\_windows\_cluster_ **'** | LOCAL }  
サーバー インスタンスの HADR クラスター コンテキストを、指定した Windows Server フェールオーバー クラスター (WSFC) に切り替えます。 *HADR クラスター コンテキスト*は、サーバー インスタンスによってホストされる可用性レプリカのメタデータを管理する WSFC を決定します。 SET HADR CLUSTER CONTEXT オプションは、[!INCLUDE[ssHADR](../../includes/sshadr-md.md)] を新しい WSFC 上の [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 以降のバージョンのインスタンスに移行するクラスター間での移行中にのみ使用してください。  
  
HADR クラスター コンテキストの切り替えは、ローカル WSFC とリモート WSFC 間でのみ実行できます。 その後、リモート WSFC からローカル WSFC に切り戻すことができます。 HADR クラスター コンテキストは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが可用性レプリカをホストしていない場合のみリモート クラスターに切り替えることができます。  
  
リモート HADR クラスター コンテキストは、いつでもローカル クラスターに切り替えることができます。 ただし、コンテキストは、サーバー インスタンスが可用性レプリカをホストしている限り、再度切り替えることはできません。 
  
切り替え先のクラスターを識別するには、次のいずれかの値を指定します。  
  
*windows_cluster*  
WSFC のネットワーク名。 短い名前または完全なドメイン名を指定できます。 短い名前のターゲット IP アドレスを検出するために、ALTER SERVER CONFIGURATION は DNS 解決を使用します。 状況によっては、短い名前を使用すると混乱が生じ、DNS から誤った IP アドレスが返されることがあります。 完全なドメイン名を指定することをお勧めします。  
  
> [!NOTE] 
> この設定を使用したクラスター間の移行はサポートされなくなりました。 クラスター間の移行を実行するには、分散可用性グループまたは他の方法 (ログ配布など) を使用します。 
  
LOCAL  
ローカル WSFC。  
  
詳しくは、「[サーバー インスタンスの HADR クラスター コンテキストの変更 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/change-the-hadr-cluster-context-of-server-instance-sql-server.md)」をご覧ください。  
  
**\<buffer_pool_extension>::=**  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降)。    
  
ON  
バッファー プール拡張オプションを有効にします。 このオプションは不揮発性記憶域を使用してバッファー プールのサイズを拡張します。 ソリッドステート ドライブ (SSD) などの不揮発性記憶域はプール内にクリーンなデータ ページを保持します。 この機能の詳細については、「[バッファー プール拡張](../../database-engine/configure-windows/buffer-pool-extension.md)」を参照してください。バッファー プール拡張機能は、すべての SQL Server エディションで使用できるとは限りません。 詳細については、「[SQL Server 2016 の各エディションでサポートされる機能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
FILENAME = 'os_file_path_and_name'  
バッファー プール拡張キャッシュ ファイルのディレクトリ パスと名前を定義します。 ファイル拡張子は .BPE と指定する必要があります。 FILENAME を変更する前に BUFFER POOL EXTENSION を無効にします。  
  
SIZE = *size* [ **KB** | MB | GB ]  
キャッシュのサイズを定義します。 既定のサイズの指定は KB です。 最小サイズは最大サーバー メモリのサイズです。 最大値は最大サーバー メモリのサイズの 32 倍です。 最大サーバー メモリの詳細については、「[sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)」を参照してください。  
  
ファイルのサイズを変更する前に BUFFER POOL EXTENSION を無効にします。 現在のサイズより小さいサイズを指定するには、SQL Server のインスタンスを再起動してメモリを再利用する必要があります。 これを行わない場合は、現在のサイズのままにしておくか、現在のサイズより大きいサイズを指定する必要があります。  
  
OFF  
バッファー プール拡張オプションを無効にします。 ファイルのサイズや名前など、関連するパラメーターを変更する場合は、事前にバッファー プール拡張オプションを無効にします。 このオプションを無効にすると、関連するすべての構成情報がレジストリから削除されます。  
  
> [!WARNING]  
>  バッファー プール拡張を無効にすると、バッファー プールのサイズが大幅に縮小されるため、サーバー パフォーマンスにマイナスの影響がある場合があります。  
  
**\<soft_numa>**  

**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降)。  
  
ON  
大きい NUMA ハードウェア ノードを小さい NUMA ノードに分割する自動パーティション分割を有効にします。 実行中の値を変更するには、データベース エンジンの再起動が必要です。  
  
OFF  
大きい NUMA ハードウェア ノードの小さい NUMA ノードへの自動ソフトウェア パーティション分割を無効にします。 実行中の値を変更するには、データベース エンジンの再起動が必要です。  

> [!WARNING]
> ALTER SERVER CONFIGURATION ステートメントと SOFT NUMA オプションおよび SQL Server エージェントの動作に関しては既知の問題があります。  推奨される操作のシーケンスを次に示します。  
> 1) SQL Server エージェントのインスタンスを停止します。  
> 2) ALTER SERVER CONFIGURATION SOFT NUMA オプションを実行します。  
> 3) SQL Server インスタンスを再起動します。  
> 4) SQL Server エージェントのインスタンスを起動します。  
  
**詳細情報:** SQL Server サービスが再起動する前に ALTER SERVER CONFIGURATION と SET SOFTNUMA コマンドを実行した場合、SQL Server エージェント サービスが停止するときに、エージェントは T-SQL RECONFIGURE コマンドを実行して、SOFTNUMA の設定を ALTER SERVER CONFIGURATION の前の状態に戻します。 

**\<memory_optimized> ::=**

**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降)。

ON <br>
[メモリ内データベース](../../relational-databases/in-memory-database.md)機能ファミリの一部である、インスタンスレベルのすべての機能を有効にします。 これには現在、[メモリ最適化 tempdb メタデータ](../../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata)と[ハイブリッド バッファー プール](../../database-engine/configure-windows/hybrid-buffer-pool.md)が含まれます。 有効にするには再起動が必要です。

OFF <br>
メモリ内データベース機能ファミリの一部である、インスタンスレベルのすべての機能を無効にします。 有効にするには再起動が必要です。

TEMPDB_METADATA = ON | OFF <br>
メモリ最適化 tempdb メタデータのみを有効または無効にします。 有効にするには再起動が必要です。 

RESOURCE_POOL='resource_pool_name' <br>
TEMPDB_METADATA = ON と組み合わせて使用することで、tempdb 用に使用する必要があるユーザー定義リソース プールを指定します。 指定しない場合、tempdb には既定のプールが使用されます。 プールは既に存在している必要があります。 サービスが再起動されたときにプールが使用できない場合、tempdb には既定のプールが使用されます。


HYBRID_BUFFER_POOL = ON | OFF <br>
インスタンス レベルでのハイブリッド バッファー プールを有効または無効にします。 有効にするには再起動が必要です。


## <a name="general-remarks"></a>全般的な解説  
このステートメントでは、明記されていない限り、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の再起動は必要ありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスの場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クラスター リソースを再起動する必要はありません。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
このステートメントは、DDL トリガーをサポートしません。  
  
## <a name="permissions"></a>アクセス許可  
必須:
- プロセス関係オプションに対する `ALTER SETTINGS` 権限。
- 診断ログとフェールオーバー クラスター プロパティのオプションに対する `ALTER SETTINGS` 権限と `VIEW SERVER STATE` 権限。
- HADR クラスター コンテキスト オプションに対する `CONTROL SERVER` 権限。  
- バッファー プール拡張オプションに対する `ALTER SERVER STATE` 権限。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]のリソース DLL は、ローカル システム アカウントで実行されます。 そのため、ローカル システム アカウントには、診断ログ オプションで指定されたパスに対する読み取りアクセス権と書き込みアクセス権が必要です。  
  
## <a name="examples"></a>使用例  
  
|カテゴリ|主な構文要素|  
|--------------|------------------------------|  
|[プロセス関係を設定する](#Affinity)|CPU、NUMANODE、AUTO|  
|[診断ログ オプションを設定する](#Diagnostic)|ON • OFF • PATH • MAX_SIZE|  
|[フェールオーバー クラスター プロパティを設定する](#Failover)|HealthCheckTimeout|  
|[可用性レプリカのクラスター コンテキストを変更する](#ChangeClusterContextExample)|**'** *windows_cluster* **'**|  
|[バッファー プール拡張を設定する](#BufferPoolExtension)|バッファー プール拡張| 
|[メモリ内データベース オプションの設定](#MemoryOptimized)|MEMORY_OPTIMIZED|

  
###  <a name="Affinity"></a> プロセス関係を設定する  
このセクションの例では、CPU および NUMA ノードにプロセス関係を設定する方法を示します。 この例では、256 個の CPU が、4 つのグループから成る NUMA ノード構成 (4 グループ合計 16 ノード) でサーバーに搭載されていることを想定しています。 スレッドは NUMA ノードにも CPU にも割り当てられていません。  
  
-   グループ 0:NUMA ノード 0 から 3、CPU 0 から 63  
-   グループ 1:NUMA ノード 4 から 7、CPU 64 から 127  
-   グループ 2:NUMA ノード 8 から 12、CPU 128 から 191  
-   グループ 3:NUMA ノード 13 から 16、CPU 192 から 255  
  
#### <a name="a-setting-affinity-to-all-cpus-in-groups-0-and-2"></a>A. グループ 0 とグループ 2 のすべての CPU に関係を設定する  
次の例では、グループ 0 とグループ 2 のすべての CPU に関係を設定します。  
  
```sql  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=0 TO 63, 128 TO 191;  
```  
  
#### <a name="b-setting-affinity-to-all-cpus-in-numa-nodes-0-and-7"></a>B. NUMA ノード 0 と NUMA ノード 7 のすべての CPU に関係を設定する  
次の例では、ノード `0` とノード `7` にのみ CPU 関係を設定します。  
  
```sql  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY NUMANODE=0, 7;  
```  
  
#### <a name="c-setting-affinity-to-cpus-60-through-200"></a>C. CPU 60 ～ 200 に関係を設定する  
次の例では、CPU 60 ～ 200 に関係を設定します。  
  
```sql  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=60 TO 200;  
```  
  
#### <a name="d-setting-affinity-to-cpu-0-on-a-system-that-has-two-cpus"></a>D. CPU が 2 個搭載されたシステムの CPU 0 に関係を設定する  
次の例では、CPU を 2 個搭載しているコンピューターの `CPU=0` に関係を設定します。 次のステートメントを実行する前の内部関係ビットマスクは 00 です。  
  
```sql  
ALTER SERVER CONFIGURATION SET PROCESS AFFINITY CPU=0;  
```  
  
#### <a name="e-setting-affinity-to-auto"></a>E. 関係を AUTO に設定する  
次の例では、関係を `AUTO` に設定します。  
  
```sql  
ALTER SERVER CONFIGURATION  
SET PROCESS AFFINITY CPU=AUTO;  
```  
  
###  <a name="Diagnostic"></a> Setting diagnostic log options  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降)。    
  
このセクションの例では、診断ログ オプションの値を設定する方法を示します。  
  
#### <a name="a-starting-diagnostic-logging"></a>A. 診断ログの記録を開始する  
次の例では、診断データのログ記録を開始します。  
  
```sql  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG ON;  
```  
  
#### <a name="b-stopping-diagnostic-logging"></a>B. 診断ログの記録を停止する  
次の例では、診断データのログ記録を停止します。  
  
```sql  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG OFF;  
```  
  
#### <a name="c-specifying-the-location-of-the-diagnostic-logs"></a>C. 診断ログの場所を指定する  
次の例では、診断ログの場所を、指定されたファイル パスに設定します。  
  
```sql  
ALTER SERVER CONFIGURATION  
SET DIAGNOSTICS LOG PATH = 'C:\logs';  
```  
  
#### <a name="d-specifying-the-maximum-size-of-each-diagnostic-log"></a>D. 各診断ログの最大サイズを指定する  
次の例では、各診断ログの最大サイズを 10 MB に設定します。  
  
```sql  
ALTER SERVER CONFIGURATION   
SET DIAGNOSTICS LOG MAX_SIZE = 10 MB;  
```  
  
###  <a name="Failover"></a> フェールオーバー クラスター プロパティを設定する  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降)。   
  
次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター リソースのプロパティの値を設定します。  
  
#### <a name="a-specifying-the-value-for-the-healthchecktimeout-property"></a>A. HealthCheckTimeout プロパティの値を指定する  
次の例では、`HealthCheckTimeout` オプションを 15,000 ミリ秒 (15 秒) に設定します。  
  
```sql  
ALTER SERVER CONFIGURATION   
SET FAILOVER CLUSTER PROPERTY HealthCheckTimeout = 15000;  
```  
  
###  <a name="ChangeClusterContextExample"></a> B. 可用性レプリカのクラスター コンテキストを変更する  
次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの HADR クラスター コンテキストを変更します。 変更先の WSFC クラスターである `clus01` を指定するため、この例では、完全なクラスター オブジェクト名である `clus01.xyz.com` を指定します。  
  
```sql  
ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT = 'clus01.xyz.com';  
```  
  
### <a name="setting-buffer-pool-extension-options"></a>バッファー プール拡張オプションを設定する  
  
####  <a name="BufferPoolExtension"></a> A. バッファー プール拡張オプションを設定する  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降)。    
  
次の例では、バッファー プール拡張オプションを有効にし、ファイル名とサイズを指定します。  
  
```sql  
ALTER SERVER CONFIGURATION   
SET BUFFER POOL EXTENSION ON  
    (FILENAME = 'F:\SSDCACHE\Example.BPE', SIZE = 50 GB);  
```  
  
#### <a name="b-modifying-buffer-pool-extension-parameters"></a>B. バッファー プール拡張パラメーターを変更する  
次の例は、バッファー プール拡張ファイルのサイズを変更します。 いずれかのパラメーターを変更する場合は、バッファー プール拡張オプションを事前に無効にする必要があります。  
  
```sql  
ALTER SERVER CONFIGURATION   
SET BUFFER POOL EXTENSION OFF;  
GO  
EXEC sp_configure 'max server memory (MB)', 12000;  
GO  
RECONFIGURE;  
GO  
ALTER SERVER CONFIGURATION  
SET BUFFER POOL EXTENSION ON  
    (FILENAME = 'F:\SSDCACHE\Example.BPE', SIZE = 60 GB);  
GO   
```  

### <a name="MemoryOptimized"></a>メモリ内データベース オプションの設定

**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降)。

#### <a name="a-enable-all-in-memory-database-features-with-default-options"></a>A. 既定のオプションを使用してすべてのメモリ内データベース機能を有効にする

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED ON;
GO
```

#### <a name="b-enable-memory-optimized-tempdb-metadata-using-the-default-resource-pool"></a>B. 既定のリソース プールを使用してメモリ最適化 tempdb メタデータを有効にする

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED TEMPDB_METADATA = ON;
GO
```

#### <a name="c-enable-memory-optimized-tempdb-metadata-with-a-user-defined-resource-pool"></a>C. ユーザー定義のリソース プールを使用してメモリ最適化 tempdb メタデータを有効にする

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED TEMPDB_METADATA = ON (RESOURCE_POOL = 'pool_name');
GO
```

#### <a name="d-enable-hybrid-buffer-pool"></a>D. ハイブリッド バッファー プールを有効にする

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = ON;
GO
```

## <a name="see-also"></a>参照  
[ソフト NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)   
[サーバー インスタンスの HADR クラスター コンテキストの変更 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/change-the-hadr-cluster-context-of-server-instance-sql-server.md)   
[sys.dm_os_schedulers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)   
[sys.dm_os_memory_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md)   
[sys.dm_os_buffer_pool_extension_configuration &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-pool-extension-configuration-transact-sql.md)   
[バッファー プール拡張](../../database-engine/configure-windows/buffer-pool-extension.md)  
  
  
