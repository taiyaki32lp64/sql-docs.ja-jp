---
title: SQL Server on Linux のパフォーマンスに関するベスト プラクティス
description: この記事では、SQL Server on Linux の実行に関するパフォーマンスのベスト プラクティスとガイドラインを提供します。
author: rgward
ms.author: bobward
ms.reviewer: vanto
ms.date: 09/14/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 543488eada46a088f3c634ce2326c7e2db2a97a5
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68105443"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-on-linux"></a>パフォーマンスのベスト プラクティスと SQL Server on Linux の構成ガイドライン

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、SQL Server on Linux に接続するデータベース アプリケーションのパフォーマンスを最大化するためのベスト プラクティスと推奨事項について説明します。 これらの推奨事項は、Linux プラットフォームでの実行に固有のものです。 インデックスの設計など、通常の SQL Server の推奨事項はすべて引き続き適用されます。

次のガイドラインには、SQL Server と Linux オペレーティング システムの両方を構成する際の推奨事項が含まれています。

## <a name="sql-server-configuration"></a>SQL Server の構成

アプリケーションで最高のパフォーマンスを実現するには、SQL Server on Linux をインストールした後で、次の構成タスクを実行することをお勧めします。

### <a name="best-practices"></a>ベスト プラクティス

- **ノードまたは CPU に PROCESS AFFINITY を使用する**

   Linux オペレーティング システム上の SQL Server (通常はすべてのノードと CPU) に使用しているすべての **NUMANODE**、CPU、または両方に `ALTER SERVER CONFIGURATION` を使用して `PROCESS AFFINITY` を設定することをお勧めします。 プロセッサ関係は、効率的な Linux および SQL スケジューリングの動作を維持するために役立ちます。 **NUMANODE** オプションを使用するのが最も簡単な方法です。 コンピューターに NUMA ノードが 1 つしかない場合でも、**PROCESS AFFINITY** を使用する必要があることに注意してください。  **PROCESS AFFINITY** の設定方法の詳細については、「[ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md)」のドキュメントを参照してください。

- **複数の tempdb データ ファイルを構成する**

   SQL Server on Linux のインストールには複数の tempdb ファイルを構成するオプションが用意されていないため、インストール後に複数の tempdb データ ファイルを作成することを検討することをお勧めします。 詳細については、「[Tempdb データベースを SQL Server に割り当て時の競合を減らすための推奨事項](https://support.microsoft.com/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d)」を参照してください。

### <a name="advanced-configuration"></a>高度な構成

次の推奨事項は、SQL Server on Linux のインストール後に選択できるオプションの構成設定です。 これらの選択肢は、Linux オペレーティング システムのワークロードと構成の要件に基づいています。

- **mssql-conf を使用してメモリ制限を設定する**

   Linux オペレーティング システムに十分な空き物理メモリを確保するために、SQL Server プロセスには既定で物理 RAM の 80% のみが使用されます。 物理 RAM のサイズが大きな一部のシステムの場合、20% でも大きな数値になることがあります。 たとえば、1 TB の RAM が搭載されたシステムでは、既定の設定では約 200 GB の RAM が未使用のままになります。 このような状況では、メモリの制限をより大きな値に構成することができます。 **mssql-conf** ツールと、SQL Server に表示されるメモリ (MB 単位) を制御する [memory.memorylimitmb](sql-server-linux-configure-mssql-conf.md#memorylimit) 設定のドキュメントを参照してください。

   この設定を変更する場合は、この値を高く設定しすぎないように注意してください。 十分なメモリを残さないと場合は、Linux オペレーティング システムやその他の Linux アプリケーションで問題が発生する可能性があります。

## <a name="linux-os-configuration"></a>Linux OS の構成

SQL Server のインストールで最適なパフォーマンスを得るには、次の Linux オペレーティング システムの構成設定を使用することを検討してください。

### <a name="kernel-settings-for-high-performance"></a>ハイ パフォーマンスのためのカーネル設定
これらは、SQL Server インストールのハイ パフォーマンスとスループットに関連する、推奨される Linux オペレーティング システム設定です。 これらの設定を構成するプロセスについては、Linux オペレーティング システムのドキュメントを参照してください。



> [!Note]
> Red Hat Enterprise Linux (RHEL) のユーザーについては、スループットパフォーマンス プロファイルによって (C-States を除く) これらの設定が自動的に構成されます。

次の表に、CPU 設定に関する推奨事項を示します。

| 設定 | [値] | 詳細情報 |
|---|---|---|
| CPU 周波数ガバナー | パフォーマンス | **cpupower** コマンドを参照してください |
| ENERGY_PERF_BIAS | パフォーマンス | **x86_energy_perf_policy** コマンドを参照してください |
| min_perf_pct | 100 | intel p-state に関するドキュメントを参照してください |
| C-States | C1 のみ | C-States が C1 のみに確実に設定する方法については、Linux またはシステムのドキュメントを参照してください |

次の表に、ディスク設定に関する推奨事項を示します。

| 設定 | [値] | 詳細情報 |
|---|---|---|
| ディスク先行読み取り | 4096 | **blockdev** コマンドを参照してください。 |
| sysctl の設定 | kernel.sched_min_granularity_ns = 10000000<br/>kernel.sched_wakeup_granularity_ns = 15000000<br/>vm.dirty_ratio = 40<br/>vm.dirty_background_ratio = 10<br/>vm.swappiness = 10 | **sysctl** コマンドを参照してください |

### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>マルチノード NUMA システムのカーネル設定の自動 numa バランシング

マルチノード **NUMA** システムに SQL Server をインストールすると、次の **kernel.numa_balancing** カーネル設定が既定で有効になります。 **NUMA** システムの効率を最大になるように SQL Server を運用するには、マルチノード NUMA システムでの自動 numa バランシングを無効にします。

```bash
sysctl -w kernel.numa_balancing=0
```

### <a name="kernel-settings-for-virtual-address-space"></a>仮想アドレス空間のカーネル設定

**vm.max_map_count** の既定の設定 (65536) は、SQL Server のインストールに十分な大きさではない可能性があります。 この値 (上限) を 256K に変更します。

```bash
sysctl -w vm.max_map_count=262144
```

### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>ファイル システム上で SQL Server のデータ ファイルとログ ファイルについて最終アクセス日時を無効にする

SQL Server のデータ ファイルとログ ファイルを格納するために使用される任意のファイル システムで **noatime** 属性を使用します。 この属性を設定する方法については、Linux のドキュメントを参照してください。

### <a name="leave-transparent-huge-pages-thp-enabled"></a>Transparent Huge Pages (THP) を有効なままにする

ほとんどの Linux インストールでは、このオプションが既定でオンです。 この構成オプションは有効なままにしておくことをお勧めします。

### <a name="swapfile"></a>swapfile

メモリ不足の問題を回避するには、swapfile が適切に構成されていることを確認します。 swapfile の作成方法と適切なサイズ設定方法については、Linux のドキュメントを参照してください。

### <a name="virtual-machines-and-dynamic-memory"></a>仮想マシンと動的メモリ

仮想マシンで SQL Server on Linux を実行している場合は、仮想マシン用に予約されているメモリの量を修正するオプションを必ず選択してください。 Hyper-V 動的メモリのような機能は使用しないでください。

## <a name="next-steps"></a>次の手順

パフォーマンスを向上させる SQL Server の機能の詳細については、「[パフォーマンス機能の概要](sql-server-linux-performance-get-started.md)」を参照してください。

Linux 上の SQL Server の詳細については、「[SQL Server on Linux の概要](sql-server-linux-overview.md)」を参照してください。
