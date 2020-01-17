---
title: dm_os_sys_info (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_sys_info_TSQL
- dm_os_sys_info
- dm_os_sys_info_TSQL
- sys.dm_os_sys_info
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_sys_info dynamic management view
- time [SQL Server], instance started
- starting time
ms.assetid: 20f6bc9c-839a-4fa4-b3f3-a6c47d1b69af
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0ddc70ef475eb5e4ddc91095ce251c383ca4cdbf
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983162"
---
# <a name="sysdm_os_sys_info-transact-sql"></a>sys.dm_os_sys_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  コンピューターに関する有用な情報のセット、および [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] で使用/消費されるリソースに関する有用な情報のセットを返します。  
  
> **注:** [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]から呼び出すには、「 **sys. dm_pdw_nodes_os_sys_info**」という名前を使用します。  
  
|列名|データ型|説明とバージョン固有の注意事項 |  
|-----------------|---------------|-----------------|  
|**cpu_ticks**|**bigint**|現在の CPU のティック数を指定します。 CPU のティックは、プロセッサの RDTSC カウンターから取得されます。 この数値は単純に増加します。 Null 値は許容されません。|  
|**ms_ticks**|**bigint**|コンピューターを起動した時点から経過した時間を指定します (ミリ秒単位)。 Null 値は許容されません。|  
|**cpu_count**|**int**|システム上の論理 CPU の数を指定します。 Null 値は許容されません。|  
|**hyperthread_ratio**|**int**|1 つの物理プロセッサ パッケージによって公開されている論理コアまたは物理コアの数の比率を指定します。 Null 値は許容されません。|  
|**physical_memory_in_bytes**|**bigint**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /><br /> コンピューターに搭載されている物理メモリの合計を指定します。 Null 値は許容されません。|  
|**physical_memory_kb**|**bigint**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> コンピューターに搭載されている物理メモリの合計を指定します。 Null 値は許容されません。|  
|**virtual_memory_in_bytes**|**bigint**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /><br /> ユーザー モードのプロセスで使用できる仮想メモリの量。 これを使用すると、SQL Server が 3-GB スイッチを使用して起動されたかどうかを判別できます。|  
|**virtual_memory_kb**|**bigint**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> ユーザー モードのプロセスで使用できる仮想アドレス空間の合計量を指定します。 Null 値は許容されません。|  
|**bpool_commited**|**int**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /><br /> メモリ マネージャーでコミット済みのメモリの量を表します (KB 単位)。 メモリ マネージャー内の予約済みメモリは含まれません。 Null 値は許容されません。|  
|**committed_kb**|**int**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> メモリ マネージャーでコミット済みのメモリの量を表します (KB 単位)。 メモリ マネージャー内の予約済みメモリは含まれません。 Null 値は許容されません。|  
|**bpool_commit_target**|**int**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /><br /> SQL Server のメモリ マネージャーによって使用できるメモリの量を表します (KB 単位)。|  
|**committed_target_kb**|**int**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> SQL Server のメモリ マネージャーによって使用できるメモリの量を表します (KB 単位)。 ターゲットの量は、次のような各種の入力を使用して計算されます。<br /><br /> -システムの負荷を含むシステムの現在の状態<br /><br /> -現在のプロセスによって要求されたメモリ<br /><br /> -コンピューターにインストールされているメモリの量<br /><br /> -構成パラメーター<br /><br /> **Committed_target_kb**が**committed_kb**より大きい場合、メモリマネージャーは追加のメモリを取得しようとします。 **Committed_target_kb**が**committed_kb**より小さい場合、メモリマネージャーはコミットされたメモリの量を減らします。 **Committed_target_kb**には、常に盗難および予約されたメモリが含まれます。 Null 値は許容されません。|  
|**bpool_visible**|**int**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /><br /> プロセス仮想アドレス空間内で直接アクセスできる、バッファー プールの 8 KB バッファーの数。 AWE (Address Windowing Extensions) を使用していない状態で、バッファー プールで目標とするメモリが確保された場合 (bpool_committed = bpool_commit_target)、bpool_visible の値は bpool_committed の値に等しくなります。SQL Server の 32 ビット環境で AWE を使用している場合、bpool_visible は、バッファー プールによって割り当てられている物理メモリへのアクセスに使用される AWE マッピング ウィンドウのサイズを表します。 このマッピング ウィンドウのサイズはプロセスのアドレス空間にバインドされています。したがって、参照可能なメモリの量はコミット済みメモリの量よりも小さくなります。また、データベース ページ以外の目的でメモリを使用する初期コンポーネントによって、さらに小さくなる可能性があります。 bpool_visible の値が小さ過ぎる場合は、メモリ不足のエラーが返されることがあります。|  
|**visible_target_kb**|**int**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> は**committed_target_kb**と同じです。 Null 値は許容されません。|  
|**stack_size_in_bytes**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって作成された各スレッドの呼び出し履歴のサイズを指定します。 Null 値は許容されません。|  
|**os_quantum**|**bigint**|非プリエンプティブ タスクのクォンタムを表します (ミリ秒単位)。 クォンタム (秒) = **os_quantum** /CPU クロック速度。 Null 値は許容されません。|  
|**os_error_mode**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスのエラー モードを指定します。 Null 値は許容されません。|  
|**os_priority_class**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスの優先度クラスを指定します。 Nullable.<br /><br /> 32 = 通常 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は通常の優先度ベース (= 7) で起動しています)。<br /><br /> 128 = 高 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は高い優先度ベースで実行しています。  (=13).)<br /><br /> 詳細については、「 [priority boost サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md)」を参照してください。|  
|**max_workers_count**|**int**|作成可能なワーカーの最大数を表します。 Null 値は許容されません。|  
|**scheduler_count**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス内で構成されたユーザー スケジューラの数を表します。 Null 値は許容されません。|  
|**scheduler_total_count**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内のスケジューラの総数を表します。 Null 値は許容されません。|  
|**deadlock_monitor_serial_number**|**int**|現在のデッドロック監視シーケンスの ID を指定します。 Null 値は許容されません。|  
|**sqlserver_start_time_ms_ticks**|**bigint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が最後に開始されたときの**ms_tick**番号を表します。 現在の ms_ticks 列と比較します。 Null 値は許容されません。|  
|**sqlserver_start_time**|**datetime**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が最後に起動された日時を指定します。 Null 値は許容されません。|  
|**affinity_type**|**int**|**適用対象**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 以降。<br /><br /> 現在使用中のサーバー CPU プロセス関係の種類を指定します。 Null 値は許容されません。 詳細については、「 [ALTER &#40;SERVER CONFIGURATION transact-sql&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)」を参照してください。<br /><br /> 1 = MANUAL<br /><br /> 2 = AUTO|  
|**affinity_type_desc**|**varchar(60)**|**適用対象**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 以降。<br /><br /> **Affinity_type**列について説明します。 Null 値は許容されません。<br /><br /> MANUAL = 少なくとも 1 台の CPU に関係が設定されています。<br /><br /> AUTO = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は CPU 間で自由にスレッドを移動できます。|  
|**process_kernel_time_ms**|**bigint**|**適用対象**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 以降。<br /><br /> すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スレッドがカーネル モードで費やした合計時間 (ミリ秒)。 この値にはサーバー上のすべてのプロセッサの時間が含まれるため、単一のプロセッサ クロックより大きくなる場合があります。 Null 値は許容されません。|  
|**process_user_time_ms**|**bigint**|**適用対象**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 以降。<br /><br /> すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スレッドがユーザー モードで費やした合計時間 (ミリ秒)。 この値にはサーバー上のすべてのプロセッサの時間が含まれるため、単一のプロセッサ クロックより大きくなる場合があります。 Null 値は許容されません。|  
|**time_source**|**int**|**適用対象**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 以降。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がウォール クロック時間の取得に使用している API を示します。 Null 値は許容されません。<br /><br /> 0 = QUERY_PERFORMANCE_COUNTER<br /><br /> 1 = MULTIMEDIA_TIMER|  
|**time_source_desc**|**nvarchar(60)**|**適用対象**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 以降。<br /><br /> **Time_source**列について説明します。 Null 値は許容されません。<br /><br /> QUERY_PERFORMANCE_COUNTER = [Queryperformancecounter](https://go.microsoft.com/fwlink/?LinkId=163095) API は、ウォールクロック時間を取得します。<br /><br /> MULTIMEDIA_TIMER = ウォールクロック時間を取得する[マルチメディアタイマー](https://go.microsoft.com/fwlink/?LinkId=163094) API。|  
|**virtual_machine_type**|**int**|**適用対象**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 以降。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が仮想化環境で実行されているかどうかを示します。  Null 値は許容されません。<br /><br /> 0 = NONE<br /><br /> 1 = HYPERVISOR<br /><br /> 2 = OTHER|  
|**virtual_machine_type_desc**|**nvarchar(60)**|**適用対象**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 以降。<br /><br /> **Virtual_machine_type**列について説明します。 Null 値は許容されません。<br /><br /> NONE = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は仮想マシン内で実行されていません。<br /><br /> ハイパーバイザー = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、ハイパーバイザーを実行している OS (ハードウェア依存の仮想化を採用したホスト OS) によってホストされる仮想マシン内で実行されています。<br /><br /> OTHER = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、Microsoft Virtual PC などのハードウェアアシスタントを使用しない OS によってホストされる仮想マシン内で実行されています。|  
|**softnuma_configuration**|**int**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。<br /><br /> NUMA ノードの構成方法を指定します。 Null 値は許容されません。<br /><br /> 0 = OFF はハードウェアの既定値を示します。<br /><br /> 1 = 自動ソフト NUMA<br /><br /> 2 = レジストリを使用した手動ソフト NUMA|  
|**softnuma_configuration_desc**|**nvarchar(60)**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。<br /><br /> OFF = ソフト NUMA 機能はオフです。<br /><br /> ON = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、ソフト NUMA の NUMA ノードのサイズを自動的に決定します。<br /><br /> MANUAL = 手動で構成されたソフト NUMA|
|**process_physical_affinity**|**nvarchar(3072)** |**適用対象:** [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]から開始します。<br /><br />今後登場する情報です。 |
|**sql_memory_model**|**int**|**適用対象:** [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降。<br /><br />メモリを割り当てるために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって使用されるメモリモデルを指定します。 Null 値は許容されません。<br /><br />1 = 従来のメモリモデル<br />2 = メモリ内のページをロックする<br /> 3 = メモリ内の大きなページ|
|**sql_memory_model_desc**|**nvarchar(120)**|**適用対象:** [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降。<br /><br />メモリを割り当てるために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって使用されるメモリモデルを指定します。 Null 値は許容されません。<br /><br />**従来**の = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、メモリの割り当てに従来のメモリモデルが使用されています。 これは、起動時に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスアカウントにメモリ特権のロックページがない場合の既定の sql メモリモデルです。<br />**LOCK_PAGES** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がメモリ内のロックページを使用してメモリを割り当てています。 これは、SQL Server の起動時にサービスアカウントに Lock Pages in Memory 特権がある場合の既定の sql memory manager です。 SQL Server ます。<br /> **LARGE_PAGES** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、メモリ内の大きなページを使用してメモリを割り当てています。 SQL Server は、サーバーの起動時とトレースフラグ834が有効になっているときに SQL Server サービスアカウントがメモリのロックページを保持しているときに、Large Pages アロケーターを使用して Enterprise edition でのみメモリを割り当てます。|
|**pdw_node_id**|**int**|**適用対象:** [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
|**socket_count** |**int** | **適用対象:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 以降。<br /><br />システムで使用可能なプロセッサソケットの数を指定します。 |  
|**cores_per_socket** |**int** | **適用対象:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 以降。<br /><br />システムで使用可能なソケットあたりのプロセッサ数を指定します。 |  
|**numa_node_count** |**int** | **適用対象:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 以降。<br /><br />システムで使用可能な numa ノードの数を指定します。 この列には、物理 numa ノードとソフト numa ノードが含まれています。 |  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]では、`VIEW SERVER STATE` のアクセス許可が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、データベースの `VIEW DATABASE STATE` アクセス許可が必要です。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard レベルと Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [オペレーティングシステム関連の動的管理ビュー &#40;の SQL Server transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  



