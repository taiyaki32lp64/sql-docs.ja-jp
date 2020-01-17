---
title: サーバー メモリの構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d4f7302da7be80038478c887a01bb32037503fc0
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028687"
---
# <a name="server-memory-configuration-options"></a>サーバー メモリの構成オプション
  **min server memory** および **max server memory**の 2 つのサーバー メモリ オプションを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスで使用される SQL Server プロセス用に SQL Server Memory Manager によって管理されるメモリ量を MB 単位で再構成します。  
  
 **min server memory** の既定の設定は 0 MB で、 **max server memory** の既定の設定は 2,147,483,647 MB です。 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は使用可能なシステム リソースに基づいて、必要なメモリを動的に変更できます。  
  
> [!NOTE]  
> **max server memory** を最小値に設定すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパフォーマンスが極端に悪化し、場合によっては起動できなくなります。 このオプションの変更後に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を起動できなくなった場合は、 **-f** 起動オプションを使用して起動し、**max server memory** を元の値に戻します。 詳細については、「 [データベース エンジン サービスのスタートアップ オプション](database-engine-service-startup-options.md)」を参照してください。  
  
 メモリを動的に使用する場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はシステムに定期的にクエリして、メモリの空き容量を確認します。 このようにメモリの空き容量を維持することによって、オペレーティング システム (OS) のページングが防止されます。 空きメモリが少ない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は OS に対してメモリを解放します。 空きメモリが多い場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はより多くのメモリを割り当てることができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってメモリが追加されるのは、ワークロードが高いためにメモリを増やす必要がある場合だけです。アクティブでないサーバーの仮想アドレス空間のサイズは増えません。  
  
 現在使用されているメモリを返すクエリについては、例 B を参照してください。 **max server memory** は、バッファー プール、コンパイル メモリ、すべてのキャッシュ、qe メモリ許可、ロック マネージャーのメモリ、および clr メモリ (基本的に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sys.dm_os_memory_clerks **でクラークが見つけたすべてのメモリ) を含む**メモリ割り当てを制御します。 スレッド スタックのメモリ、メモリ ヒープ、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外のリンクされているサーバーのプロバイダー、および非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DLL によって割り当てられたメモリは、最大サーバー メモリによって制御されません。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、メモリ通知 API **QueryMemoryResourceNotification** を使用して、いつ SQL Server Memory Manager がメモリの割り当てまたは解放を行うことができるかを判断します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がメモリを動的に使用できるようにする方法をお勧めしますが、手動でメモリ オプションを設定して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がアクセスできるメモリの量を制限することもできます。 この場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用のメモリ量を設定する前に、OS および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の他のインスタンス (およびコンピューターが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]専用でない場合は他のシステム) が使用するメモリの量を物理メモリ全体から差し引いて適切なメモリ設定を決定します。 この差が、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に割り当てることができる最大メモリ量です。  
  
## <a name="setting-the-memory-options-manually"></a>メモリ オプションの手動設定  
サーバー オプションの **min server memory** と **max server memory** を設定して、メモリ範囲を与えることができます。 この方法は、システム管理者またはデータベース管理者が同じホスト上で実行する他のアプリケーションまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の他のインスタンスに必要なメモリと合わせて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを構成する場合に便利です。

> [!NOTE]
> **min server memory** および **max server memory** は拡張オプションです。 **sp_configure** システム ストアド プロシージャを使用してこれらの設定を変更するには、 **show advanced options** を 1 に設定する必要があります。 これらの設定は、サーバーを再起動しなくてもすぐに有効になります。  
  
<a name="min_server_memory"></a> **min_server_memory** を使用すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス用に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Memory Manager で使用できる最小メモリ量を確保できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、 **min server memory** で指定されたメモリ量を起動時にすぐに割り当てるわけではありません。 ただし、クライアントの負荷によってメモリの使用量がこの値に達すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] min server memory **の値を小さくしない限り、** はメモリを解放できません。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンスが同じホストに同時に存在するとき、インスタンスのメモリを予約する目的で、max_server_memory の代わりに min_server_memory パラメーターを設定します。 また、基礎をなすホストからのメモリ負荷が高いために、ゲスト [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仮想マシン (VM) のバッファー プールから十分なパフォーマンスに必要な量を超えるメモリが割り当て解除される事態を回避するために、min_server_memory 値の設定は仮想環境で必要不可欠となります。
 
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、**min server memory** で指定されたメモリ量を必ず割り当てるわけではありません。 サーバーの負荷が **min server memory**で指定されたメモリ量の割り当てを必要としない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はより少ないメモリで実行します。  
  
<a name="max_server_memory"></a> **max_server_memory** を利用し、OS に好ましくないメモリ負荷が発生しないようにします。 最大サーバー メモリ構成を設定するには、メモリ要件を判断する目的で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の全体的使用量を観察します。 単一インスタンスでこのような計算をより精確に行うには:
 -  OS のメモリ合計から、1GB ～ 4GB を OS 自体に予約します。
 -  次に、**max server memory** で制御されない、潜在的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メモリ割り当てに相当するメモリ量を差し引きます。この相当するメモリ量は、 **_スタック サイズ<sup>1</sup>\* に計算した最大ワーカー スレッド<sup>2</sup> を掛けたものにスタートアップ パラメーター<sup>3</sup> の -g を足して_** 求められます ( *-g* が設定されていない場合、既定で 256MB を足します)。 残ったものが単一インスタンス セットアップの max_server_memory 設定になります。
 
<sup>1</sup> アーキテクチャあたりのスレッド スタック サイズについては、「[メモリ管理アーキテクチャ ガイド](https://docs.microsoft.com/sql/relational-databases/memory-management-architecture-guide#stacksizes)」を参照してください。

<sup>2</sup> 現在のホストで関連付けられている所与の CPU 数に対して計算される既定のワーカー スレッドについては、ドキュメント ページの「[max worker threads サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)」を参照してください。

<sup>3</sup> スタートアップ パラメーター *-g* の詳細については、ドキュメント ページの「[データベース エンジン サービスのスタートアップ オプション](https://docs.microsoft.com/sql/database-engine/configure-windows/database-engine-service-startup-options?view=sql-server-2014)」を参照してください。 32 ビットの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] から [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) にのみ適用できます。

|OS の種類|**Max server memory**に許容される最小メモリ容量|  
|-------------|----------------------------------------------------------------|  
|32 ビット|64 MB|  
|64 ビット|128 MB| 

## <a name="how-to-configure-memory-options-using-sql-server-management-studio"></a>SQL Server Management Studio を使用して、メモリ オプションを構成する方法  
 **min server memory** および **max server memory**の 2 つのサーバー メモリ オプションを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス用に SQL Server Memory Manager によって管理されるメモリ量を MB 単位で再構成します。 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は使用可能なシステム リソースに基づいて、必要なメモリを動的に変更できます。  
  
### <a name="procedure-for-configuring-a-fixed-amount-of-memory"></a>固定量のメモリを構成する手順  
 **固定量のメモリを設定するには:**  
  
1.  オブジェクト エクスプローラーで、サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[メモリ]** ノードをクリックします。  
  
3.  **[サーバー メモリ オプション]** で、 **[最小サーバー メモリ]** と **[最大サーバー メモリ]** に必要な数値を入力します。  
  
     既定の設定を使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が使用できるシステム リソースに基づいて、そのメモリ要求を動的に変更できるようになります。 **min server memory** の既定の設定は 0 MB で、 **max server memory** の既定の設定は 2,147,483,647 MB です。  
  
## <a name="maximize-data-throughput-for-network-applications"></a>ネットワーク アプリケーションのデータ スループットの最大化  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のシステム メモリ使用量を最適化するには、ファイルのキャッシュに使用されるメモリ量を制限する必要があります。 ファイル システム キャッシュを制限するには、 **[ファイル共有のデータ スループットを最大にする]** が選択されていないことを確認します。 最小のファイル システム キャッシュを指定するには、 **[メモリの使用を最小にする]** または **[バランスをとる]** を選択します。  
  
#### <a name="to-check-the-current-setting-on-your-operating-system"></a>オペレーティング システムの現在の設定を確認するには  
  
1.  **[スタート]** ボタンをクリックし、 **[コントロール パネル]** をクリックします。次に **[ネットワーク接続]** をダブルクリックして、 **[ローカル エリア接続]** をダブルクリックします。  
  
2.  **[全般]** タブで **[プロパティ]** をクリックし、 **[Microsoft ネットワーク用ファイルとプリンター共有]** を選択して、 **[プロパティ]** をクリックします。  
  
3.  **[ネットワーク アプリケーションのデータ スループットを最大にする]** が選択されている場合は、他のオプションを選択して **[OK]** をクリックし、すべてのダイアログ ボックスを閉じます。  
  
## <a name="lock-pages-in-memory"></a>lock pages in memory  
 この Windows ポリシーにより、プロセスを使用して物理メモリにデータを保持できるアカウントを指定し、ディスク上の仮想メモリへのデータのページングを防止します。 メモリ内のページをロックすると、ディスクへのメモリのページングが発生した際に、サーバーの応答性を維持できます。 Sqlservr.exe を実行する特権を持つアカウントに Windows の "Locked pages in memory" (LPIM) ユーザー [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]権利が付与されている場合、Standard edition 以降の32ビットおよび64ビットのインスタンスで SQL Server **Lock pages in memory**オプションは ON に設定されます。 それよりも前のバージョンの SQL Server の場合、SQL Server の 32 ビット インスタンスで Lock Pages オプションを設定するには、sqlservr.exe の実行権限があるアカウントに LPIM のユーザー権利があること、さらに、'awe_enabled' 構成オプションがオンに設定されていることが必要となります。  
  
 の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Lock pages in memory**オプションを無効にするには、SQL Server 開始アカウントに対する "Locked pages in memory" ユーザー権利を削除します。  
  
### <a name="to-disable-lock-pages-in-memory"></a>Lock Pages in Memory を無効にするには  
 **Lock pages in memory オプションを無効にするには、次のようにします。**  
  
1.  **[スタート]** メニューの **[ファイル名を指定して実行]** をクリックします。 **[名前]** ボックスに「 `gpedit.msc`」と入力します。  
  
     **[グループ ポリシー]** ダイアログ ボックスが開きます。  
  
2.  **[グループ ポリシー]** コンソールで **[コンピューターの構成]** を展開し、次に **[Windows の設定]** を展開します。  
  
3.  **[セキュリティの設定]** を展開し、 **[ローカル ポリシー]** を展開します。  
  
4.  **[ユーザー権利の割り当て]** フォルダーをクリックします。  
  
     ポリシーが詳細ペインに表示されます。  
  
5.  詳細ペインで、 **[メモリ内のページのロック]** をダブルクリックします。  
  
6.  **[ローカル セキュリティ ポリシーの設定]** ダイアログ ボックスで、sqlservr.exe の実行権限のあるアカウントを選択し、 **[削除]** をクリックします。  
  
## <a name="virtual-memory-manager"></a>仮想メモリ マネージャー  
 32 ビット オペレーティング システムでは、4 GB の仮想アドレス空間にアクセスできます。 仮想メモリの 2 GB はプロセスごとに専有され、アプリケーションで使用できます。 残りの 2 GB はオペレーティング システムが使用するために予約されています。 すべてのオペレーティング システムのエディションには、オペレーティング システム用の仮想メモリを 1 GB に制限して、アプリケーションで 3 GB の仮想アドレス空間にアクセスできるようにするスイッチが含まれています。 スイッチのメモリ構成の使用方法については、4 GB チューニング (4GT) に関する Windows のマニュアルを参照してください。 32 ビットの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を 64 ビット オペレーティング システム上で実行する場合、ユーザーは 4 GB の仮想アドレス空間をすべて使用できます。  
  
 Windows 仮想メモリ マネージャー (VMM) は、使用可能な物理メモリにコミット済みのアドレス空間をマップします。  
  
 さまざまなオペレーティング システムでサポートされている物理メモリ量の詳細については、Windows のマニュアルの「Windows のリリース別のメモリ制限」を参照してください。  
  
 仮想メモリ システムでは、仮想メモリと物理メモリの比率が 1:1 を超えるような物理メモリの設定を許可しています。 その結果、さまざまな物理メモリ構成のコンピューターで大規模なプログラムを実行できます。 しかし、すべてのプロセスの平均ワーキング セットを合わせた容量よりもはるかに大きな仮想メモリを使用すると、パフォーマンスが低下する可能性があります。  
  
 **min server memory** および **max server memory** は拡張オプションです。 **sp_configure** システム ストアド プロシージャを使用してこれらの設定を変更するには、 **show advanced options** を 1 に設定する必要があります。 これらの設定は、サーバーを再起動しなくてもすぐに有効になります。  
  
## <a name="running-multiple-instances-of-sql-server"></a>SQL Server の複数インスタンスの実行  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の複数のインスタンスを実行する場合は、3 つの方法でメモリを管理できます。  
  
-   **max server memory** を使用して、メモリ使用量を制御します。 許可する値の合計がコンピューターの合計物理メモリを超えないように注意して、各インスタンスの最大値を設定します。 予測されるワークロードまたはデータベース サイズに比例して、各インスタンスにメモリを割り当てることができます。 この方法の利点は、新しいプロセスまたはインスタンスが起動したときに、直ちに空きメモリを使用できることです。 欠点は、実行していないインスタンスがある場合、残っている空きメモリを実行中のインスタンスが利用できないことです。  
  
-   **min server memory** を使用して、メモリ使用量を制御します。 最小値の合計がコンピューターの合計物理メモリよりも 1 ～ 2 GB 少なくなるように、各インスタンスの最小値を設定します。 この場合も、インスタンスの予測される負荷に比例して、最小値を設定できます。 この方法の利点は、一度にすべてのインスタンスを実行しない場合に、実行中のインスタンスが残っている空きメモリを使用できることです。 また、この方法は、コンピューターの別のプロセスがメモリを集中的に使用する場合にも有効です。少なくとも、妥当なメモリ量を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が使用できることが保証されます。 欠点は、新しいインスタンス (または他のプロセス) が起動するときに、実行中のインスタンスがメモリを解放するのにしばらく時間がかかる場合があることです。特に、変更されたページをデータベースに書き戻す必要がある場合は時間がかかります。  
  
-   何も行いません (非推奨)。 ワークロードを伴う最初のインスタンスに、すべてのメモリが割り当てられる傾向があります。 アイドル状態のインスタンスまたは後から起動したインスタンスは、使用可能な最小限のメモリ量だけで実行することになります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、インスタンス間でメモリ使用量の調整を図ることはありません。 ただし、すべてのインスタンスは、Windows の Memory Notification シグナルに対応して、メモリ使用量を調整します。 Memory Notification API を使用して Windows がアプリケーション間のメモリを調整することはありません。 システムで使用できるメモリに関するグローバルなフィードバックを提供するだけです。  
  
 これらの設定はインスタンスを再起動しなくても変更できるので、簡単にいろいろな設定を試して、使用パターンに最適な設定を見つけることができます。  
  
## <a name="providing-the-maximum-amount-of-memory-to-sql-server"></a>SQL Server に対する最大メモリ容量の指定  
  
||32 ビット|64 ビット|  
|-|-------------|-------------|  
|コンベンショナル メモリ|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのエディションでプロセス仮想アドレス空間制限まで:<br /><br /> 2 GB<br /><br /> 3 GB ( **/3gb**ブートパラメーター *)<br /><br /> 4 GB (WOW64)\*\*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのエディションでプロセス仮想アドレス空間制限まで:<br /><br /> 8 TB (x64 アーキテクチャの場合)|  
  
 * **/3gb** は、オペレーティング システムのブート パラメーターです。 詳細については、 [MSDN ライブラリ](https://go.microsoft.com/fwlink/?LinkID=10257&clcid=0x409)を参照してください。  
  
 \* * WOW64 (windows on windows 64) は、32 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ビットが64ビットオペレーティングシステムで実行されるモードです。 詳細については、 [MSDN ライブラリ](https://go.microsoft.com/fwlink/?LinkID=10257&clcid=0x409)を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="example-a"></a>例 A  
 次の例では、 `max server memory` オプションを 4 GB に設定します。  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'max server memory', 4096;  
GO  
RECONFIGURE;  
GO  
```  
  
### <a name="example-b-determining-current-memory-allocation"></a>例 B: 現在のメモリ割り当てを確認する  
 次のクエリでは、現在割り当てられているメモリに関する情報を返します。  
  
```  
SELECT  
(physical_memory_in_use_kb/1024) AS Memory_usedby_Sqlserver_MB,  
(locked_page_allocations_kb/1024) AS Locked_pages_used_Sqlserver_MB,  
(total_virtual_address_space_kb/1024) AS Total_VAS_in_MB,  
process_physical_memory_low,  
process_virtual_memory_low  
FROM sys.dm_os_process_memory;  
```  
  
## <a name="see-also"></a>関連項目  
 [パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
