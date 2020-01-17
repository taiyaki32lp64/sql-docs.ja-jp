---
title: サーバー メモリの構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Virtual Memory Manager
- max server memory option
- virtual memory [SQL Server]
- VMM
- server memory options [SQL Server]
- servers [SQL Server], memory
- buffer pools [SQL Server]
- min server memory option
- manual memory options [SQL Server]
- memory [SQL Server], servers
ms.assetid: 29ce373e-18f8-46ff-aea6-15bbb10fb9c2
author: pmasl
ms.author: mikeray
ms.openlocfilehash: a9e617488ac0543dd7794cce37137518c1422c80
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028739"
---
# <a name="server-memory-configuration-options"></a>サーバー メモリの構成オプション
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**min server memory** および **max server memory**の 2 つのサーバー メモリ オプションを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスで使用される SQL Server プロセス用に SQL Server Memory Manager によって管理されるメモリ量を MB 単位で再構成します。  
  
**min server memory** の既定の設定は 0 MB で、**max server memory** の既定の設定は 2,147,483,647 MB です。 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は使用可能なシステム リソースに基づいて、必要なメモリを動的に変更できます。 詳細については、「[動的メモリ管理](../../relational-databases/memory-management-architecture-guide.md#dynamic-memory-management)」を参照してください。 

**max server memory** に設定できる最小メモリは 128 MB です。
  
> [!IMPORTANT]  
> **max server memory** 値の設定が高すぎると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の単一インスタンスと、同じホストの他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスでメモリの競合が発生することがあります。 ただし、この値の設定が低すぎても、メモリやパフォーマンス関連の大きな問題が発生する可能性があります。 **max server memory** を最小値に設定すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が起動できなくなることもあります。 このオプションの変更後に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を起動できなくなった場合は、 **_-f_** 起動オプションを使用して起動し、**max server memory** を元の値に戻します。 詳細については、「 [データベース エンジン サービスのスタートアップ オプション](../../database-engine/configure-windows/database-engine-service-startup-options.md)」を参照してください。  
    
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はメモリを動的に使用できますが、手動でメモリ オプションを設定して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がアクセスできるメモリの量を制限こともできます。 この場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用のメモリ量を設定する前に、OS に必要なメモリ、max_server_memory で制御されないメモリ割り当てに必要なメモリ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の他のインスタンス (およびコンピューターが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 専用でない場合は他のシステム) に必要なメモリの量を物理メモリ全体から差し引いて適切なメモリ設定を決定します。 この差が、現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに割り当てることができる最大メモリ量です。  
 
## <a name="setting-the-memory-options-manually"></a>メモリ オプションの手動設定  
サーバー オプションの **min server memory** と **max server memory** を設定して、メモリ範囲を与えることができます。 この方法は、システム管理者またはデータベース管理者が同じホスト上で実行する他のアプリケーションまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の他のインスタンスに必要なメモリと合わせて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを構成する場合に便利です。

> [!NOTE]
> **min server memory** および **max server memory** は拡張オプションです。 **sp_configure** システム ストアド プロシージャを使用してこれらの設定を変更するには、 **show advanced options** を 1 に設定する必要があります。 これらの設定は、サーバーを再起動しなくてもすぐに有効になります。  
  
<a name="min_server_memory"></a> **min_server_memory** を使用すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス用に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Memory Manager で使用できる最小メモリ量を確保できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、 **min server memory** で指定されたメモリ量を起動時にすぐに割り当てるわけではありません。 ただし、クライアントの負荷によってメモリの使用量がこの値に達すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] min server memory **の値を小さくしない限り、** はメモリを解放できません。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンスが同じホストに同時に存在するとき、インスタンスのメモリを予約する目的で、max_server_memory の代わりに min_server_memory パラメーターを設定します。 また、基礎をなすホストからのメモリ負荷が高いために、ゲスト [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仮想マシン (VM) のバッファー プールから十分なパフォーマンスに必要な量を超えるメモリが割り当て解除される事態を回避するために、min_server_memory 値の設定は仮想環境で必要不可欠となります。

>[!NOTE]
>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、**min server memory** で指定されたメモリ量を必ず割り当てるわけではありません。 サーバーの負荷が **min server memory**で指定されたメモリ量の割り当てを必要としない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はより少ないメモリで実行します。

<a name="max_server_memory"></a> **max_server_memory** を利用し、OS に好ましくないメモリ負荷が発生しないようにします。 最大サーバー メモリ構成を設定するには、メモリ要件を判断する目的で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の全体的使用量を観察します。 単一インスタンスでこのような計算をより精確に行うには:
- OS のメモリ合計から、1GB ～ 4GB を OS 自体に予約します。
- 次に、**max server memory** で制御されない、潜在的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メモリ割り当てに相当するメモリ量を差し引きます。この相当するメモリ量は、**スタック サイズ <sup>1</sup> \* 最大ワーカー スレッド <sup>2</sup>** です。 残ったものが単一インスタンス セットアップの max_server_memory 設定になります。

<sup>1</sup> アーキテクチャあたりのスレッド スタック サイズについては、「[メモリ管理アーキテクチャ ガイド](../../relational-databases/memory-management-architecture-guide.md#stacksizes)」を参照してください。

<sup>2</sup> 現在のホストで関連付けられている所与の CPU 数に対して計算される既定のワーカー スレッドについては、ドキュメント ページの「[max worker threads サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)」を参照してください。

## <a name="how-to-configure-memory-options-using-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を利用してメモリ オプションを構成する方法  
**min server memory** および **max server memory**の 2 つのサーバー メモリ オプションを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス用に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Memory Manager によって管理されるメモリ量を MB 単位で再構成します。 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は使用可能なシステム リソースに基づいて、必要なメモリを動的に変更できます。  
  
### <a name="procedure-for-configuring-a-fixed-amount-of-memory-not-recommended"></a>固定量のメモリを構成する手順 (非推奨)  
固定量のメモリを設定するには:  
  
1.  オブジェクト エクスプローラーで、サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[メモリ]** ノードをクリックします。  
  
3.  **[サーバー メモリ オプション]** で、 **[最小サーバー メモリ]** と **[最大サーバー メモリ]** と同じ量を入力します。  
  
     既定の設定を使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が使用できるシステム リソースに基づいて、そのメモリ要求を動的に変更できるようになります。 **max server memory** は[上記](#max_server_memory)のように設定することが推奨されます。 
  
## <a name="lock-pages-in-memory-lpim"></a>Lock Pages in Memory (LPIM) 
この Windows ポリシーにより、プロセスを使用して物理メモリにデータを保持できるアカウントを指定し、ディスク上の仮想メモリへのデータのページングを防止します。 メモリ内のページをロックすると、ディスクへのメモリのページングが発生した際に、サーバーの応答性を維持できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard エディション以上のインスタンスでは、sqlservr.exe の実行権限があるアカウントに Windows の *Lock Pages in Memory* (LPIM) ユーザー権利が付与されている場合、**Lock Pages in Memory** オプションはオンに設定されます。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **Lock Pages In Memory** オプションを無効にするには、sqlservr.exe ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 開始アカウント) 開始アカウントを実行する特権のあるアカウントに関して、*Lock Pages in Memory* ユーザー権利を削除します。  
 
このオプションを設定しても、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [動的メモリ管理](../../relational-databases/memory-management-architecture-guide.md#dynamic-memory-management)には影響が出ません。他のメモリ クラークの要求で拡大縮小できます。 *Lock Pages in Memory* ユーザー権利を使用するとき、[上記](#max_server_memory)のように **max server memory** の上限を設定することが推奨されます。

> [!IMPORTANT]
> このオプションの設定は、必要なときにのみ、具体的には、sqlservr プロセスがページ アウトされているという兆候があるときにのみ使用します。その場合、次の例のようなエラー 17890 がエラー ログで報告されます。`A significant part of sql server process memory has been paged out. This may result in a performance degradation. Duration: #### seconds. Working set (KB): ####, committed (KB): ####, memory utilization: ##%.`
> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降では、Standard Edition で Lock Pages を使用するのに[トレース フラグ 845](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) は必要ありません。 
  
### <a name="to-enable-lock-pages-in-memory"></a>Lock Pages in Memory を有効にするには  
lock pages in memory オプションを有効にするには:  
  
1.  **[スタート]** メニューの **[ファイル名を指定して実行]** をクリックします。 **[開く]** ボックスに「 **gpedit.msc**」と入力します。  
  
     **[グループ ポリシー]** ダイアログ ボックスが開きます。  
  
2.  **[グループ ポリシー]** コンソールで **[コンピューターの構成]** を展開し、次に **[Windows の設定]** を展開します。  
  
3.  **[セキュリティの設定]** を展開し、 **[ローカル ポリシー]** を展開します。  
  
4.  **[ユーザー権利の割り当て]** フォルダーをクリックします。  
  
     ポリシーが詳細ペインに表示されます。  
  
5.  詳細ペインで、 **[メモリ内のページのロック]** をダブルクリックします。  
  
6.  **[ローカル セキュリティ ポリシーの設定]** ダイアログ ボックスで、sqlservr.exe の実行権限のあるアカウント ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 開始アカウント) を追加します。  
  
## <a name="running-multiple-instances-of-includessnoversionincludesssnoversion-mdmd"></a>複数の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの実行  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の複数のインスタンスを実行する場合は、3 つの方法でメモリを管理できます。  
  
-   **max server memory** を使用し、[上記](#max_server_memory)のようにメモリ使用量を制御します。 許可する値の合計がコンピューターの合計物理メモリを超えないように注意して、各インスタンスの最大値を設定します。 予測されるワークロードまたはデータベース サイズに比例して、各インスタンスにメモリを割り当てることができます。 この方法の利点は、新しいプロセスまたはインスタンスが起動したときに、直ちに空きメモリを使用できることです。 欠点は、実行していないインスタンスがある場合、残っている空きメモリを実行中のインスタンスが利用できないことです。  
  
-   **min server memory** を使用し、[上記](#min_server_memory)のようにメモリ使用量を制御します。 最小値の合計がコンピューターの合計物理メモリよりも 1 ～ 2 GB 少なくなるように、各インスタンスの最小値を設定します。 この場合も、インスタンスの予測される負荷に比例して、最小値を設定できます。 この方法の利点は、一度にすべてのインスタンスを実行しない場合に、実行中のインスタンスが残っている空きメモリを使用できることです。 また、この方法は、コンピューターの別のプロセスがメモリを集中的に使用する場合にも有効です。少なくとも、妥当なメモリ量を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が使用できることが保証されます。 欠点は、新しいインスタンス (または他のプロセス) が起動するときに、実行中のインスタンスがメモリを解放するのにしばらく時間がかかる場合があることです。特に、変更されたページをデータベースに書き戻す必要がある場合は時間がかかります。  
  
-   何も行いません (非推奨)。 ワークロードを伴う最初のインスタンスに、すべてのメモリが割り当てられる傾向があります。 アイドル状態のインスタンスまたは後から起動したインスタンスは、使用可能な最小限のメモリ量だけで実行することになります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、インスタンス間でメモリ使用量の調整を図ることはありません。 ただし、すべてのインスタンスは、Windows の Memory Notification シグナルに対応して、メモリ使用量を調整します。 Memory Notification API を使用して Windows がアプリケーション間のメモリを調整することはありません。 システムで使用できるメモリに関するグローバルなフィードバックを提供するだけです。  
  
 これらの設定はインスタンスを再起動しなくても変更できるので、簡単にいろいろな設定を試して、使用パターンに最適な設定を見つけることができます。  
  
## <a name="providing-the-maximum-amount-of-memory-to-sql-server"></a>SQL Server に対する最大メモリ容量の指定  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのエディションで、プロセス仮想アドレス空間の制限までメモリを構成できます。 詳細については、「[Memory Limits for Windows and Windows Server Releases](/windows/desktop/Memory/memory-limits-for-windows-releases#physical-memory-limits-windows-server-2016)」 (Windows リリースと Windows Server リリースのメモリ上限) を参照してください。

## <a name="examples"></a>使用例

### <a name="example-a-set-the-max-server-memory-option-to-4-gb"></a>例 A: max server memory オプションを 4 GB に設定する
 次の例では、`max server memory` オプションを 4 GB に設定します。  `sp_configure` ではオプションの名前は `max server memory (MB)` として指定されますが、例では `(MB)` が省略されていることに注目してください。

```sql
sp_configure 'show advanced options', 1;
GO
RECONFIGURE;
GO
sp_configure 'max server memory', 4096;
GO
RECONFIGURE;
GO
```
これにより、次のようなステートメントが出力されます:

> 構成オプション 'max server memory (MB)' は 2147483647 から 4096 に変更されました。 RECONFIGURE ステートメントを実行してインストールしてください。

### <a name="example-b-determining-current-memory-allocation"></a>例 B: 現在のメモリ割り当てを確認する  
 次のクエリでは、現在割り当てられているメモリに関する情報を返します。  

```sql  
SELECT 
  physical_memory_in_use_kb/1024 AS sql_physical_memory_in_use_MB, 
    large_page_allocations_kb/1024 AS sql_large_page_allocations_MB, 
    locked_page_allocations_kb/1024 AS sql_locked_page_allocations_MB,
    virtual_address_space_reserved_kb/1024 AS sql_VAS_reserved_MB, 
    virtual_address_space_committed_kb/1024 AS sql_VAS_committed_MB, 
    virtual_address_space_available_kb/1024 AS sql_VAS_available_MB,
    page_fault_count AS sql_page_fault_count,
    memory_utilization_percentage AS sql_memory_utilization_percentage, 
    process_physical_memory_low AS sql_process_physical_memory_low, 
    process_virtual_memory_low AS sql_process_virtual_memory_low
FROM sys.dm_os_process_memory;  
```  

### <a name="example-c-determining-value-for-max-server-memory-mb"></a>例 C: 'max server memory (MB)' の値を確認する
次のクエリでは、現在構成されている値と SQL Server で使用中の値に関する情報が返されます。  このクエリでは、'show advanced options' が true であるかどうかに関係なく結果が返されます。

```sql
SELECT c.value, c.value_in_use
FROM sys.configurations c WHERE c.[name] = 'max server memory (MB)'
```
  
## <a name="see-also"></a>参照  
 [メモリ管理アーキテクチャ ガイド](../../relational-databases/memory-management-architecture-guide.md)   
 [パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [データベース エンジン サービスのスタートアップ オプション](../../database-engine/configure-windows/database-engine-service-startup-options.md)   
 [エディションと SQL Server 2016 のサポートされる機能](../../sql-server/editions-and-components-of-sql-server-2016.md#Cross-BoxScaleLimits)   
 [エディションと SQL Server 2017 のサポートされる機能](../../sql-server/editions-and-components-of-sql-server-2017.md#Cross-BoxScaleLimits)   
 [Linux 上の SQL Server 2017 のエディションとサポートされる機能](../../linux/sql-server-linux-editions-and-components-2017.md#Cross-BoxScaleLimits)   
 [Windows リリースと Windows Server リリースのメモリ上限](/windows/desktop/Memory/memory-limits-for-windows-releases)
