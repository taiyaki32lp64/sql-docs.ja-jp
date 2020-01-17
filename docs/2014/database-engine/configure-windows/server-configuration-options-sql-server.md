---
title: サーバー構成オプション (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/29/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- surface area configuration [SQL Server], sp_configure
- configuration options [SQL Server], when take effect
- server management [SQL Server], configuration options
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], configuring
- configuration options [SQL Server], setting
- options [SQL Server], configuration
- RECONFIGURE statement
- performance [SQL Server], servers
- configuration options [SQL Server]
- RECONFIGURE WITH OVERRIDE statement
- SQL Server, configuring
- sp_configure
- stored procedures [SQL Server], configuration options
- server configuration [SQL Server]
- administering SQL Server, configuration options
ms.assetid: 9f38eba6-39b1-4f1d-ba24-ee4f7e2bc969
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 645aee1374f7dbf3c290500bb35ca47115983670
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62809570"
---
# <a name="server-configuration-options-sql-server"></a>サーバー構成オプション (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソースの管理および最適化を行うには、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または sp_configure システム ストアド プロシージャを使用して、構成オプションを設定します。 最も一般的に使用されるサーバー構成オプションは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]から使用できます。また、sp_configure を使用するとすべての構成オプションにアクセスできます。 システムへの影響を慎重に検討したうえで、これらのオプションを設定してください。 詳細については、「[サーバー プロパティの表示または変更 &#40;SQL Server&#41;](view-or-change-server-properties-sql-server.md)」を参照してください。  
  
> [!IMPORTANT]  
>  詳細設定オプションは、熟練したデータベース管理者または認定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術者だけが変更するようにしてください。  
  
## <a name="categories-of-configuration-options"></a>構成オプションのカテゴリ  
 構成オプションは、次のいずれかの場合に有効になります。  
  
-   オプションを設定し、RECONFIGURE ステートメントまたは場合によっては RECONFIGURE WITH OVERRIDE ステートメントを実行した直後。  
  
     \- または -  
  
-   上の操作を行い、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを再起動した後。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の再起動を必要とするオプションについては、最初に、変更された値が value 列だけに表示されます。 再起動後に、その新しい値が value 列と value_in_use 列の両方に表示されます。  
  
 オプションの中には、新しい構成を有効にするために、サーバーを再起動する必要があるものもあります。 新しい値を設定し sp_configure を実行した後にサーバーを再起動した場合、新しい値は構成オプションの value_in_use 列ではなく value 列に表示されます。 サーバーの再起動後は、新しい値が value_in_use  列に表示されます。  
  
 自己構成オプションは、システムのニーズに合わせて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が調整するオプションです。 このため、ほとんどの場合、値を手動で変更する必要はありません。 たとえば、min server memory、max server memory、user connections などの各オプションがあります。  
  
## <a name="configuration-options-table"></a>構成オプションの表  
 次の表は、使用可能なすべての構成オプション、設定可能範囲、および既定値を示しています。 構成オプションには文字コードを付けています。その内容を次に示します。  
  
-   A = 詳細設定オプション。熟練したデータベース管理者または認定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術者だけがこのオプションを変更するようにしてください。また、show advanced options を 1 に設定する必要があります。  
  
-   RR = [!INCLUDE[ssDE](../../includes/ssde-md.md)]の再起動が必要なオプション。  
  
-   SC = 自己構成オプション。  
  
    |構成オプション|最小値|最大値|既定|  
    |--------------------------|-------------------|-------------------|-------------|  
    |[access check cache bucket count](access-check-cache-server-configuration-options.md) (A)|0|16384|0|  
    |[access check cache quota](access-check-cache-server-configuration-options.md) (A)|0|2147483647|0|  
    |[ad hoc distributed queries](ad-hoc-distributed-queries-server-configuration-option.md) (A)|0|1|0|  
    |[affinity I/O mask](affinity-input-output-mask-server-configuration-option.md) (A、RR)|-2147483648|2147483647|0|  
    |[affinity64 I/O mask](affinity64-input-output-mask-server-configuration-option.md) (A、64 ビット版の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でのみ使用可能)|-2147483648|2147483647|0|  
    |[affinity mask](affinity-mask-server-configuration-option.md) (A)|-2147483648|2147483647|0|  
    |[affinity64 mask](affinity64-mask-server-configuration-option.md) (A、RR)、64 ビット版のでのみ使用可能 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|-2147483648|2147483647|0|  
    |[Agent XPs](agent-xps-server-configuration-option.md) (A)|0|1|0<br /><br /> ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが起動すると 1 に変わります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが自動的に起動するようにセットアップ時に設定されている場合の既定値は 0 です。)|  
    |[allow updates](allow-updates-server-configuration-option.md) (旧バージョンで使用。 使わないでください。 再構成中にエラーが発生する原因になる場合があります。)|0|1|0|  
    |[バックアップ チェックサムの既定](../backup-checksum-default.md)|0|1|0|  
    |[backup compression default](view-or-configure-the-backup-compression-default-server-configuration-option.md)|0|1|0|  
    |[blocked process threshold](blocked-process-threshold-server-configuration-option.md) (A)|0|86400|0|  
    |[c2 audit mode](c2-audit-mode-server-configuration-option.md) (A、RR)|0|1|0|  
    |[clr enabled](clr-enabled-server-configuration-option.md)|0|1|0|  
    |[common criteria compliance enabled](common-criteria-compliance-enabled-server-configuration-option.md) (A、RR)|0|1|0|  
    |[contained database authentication](contained-database-authentication-server-configuration-option.md)|0||0|  
    |[cost threshold for parallelism](configure-the-cost-threshold-for-parallelism-server-configuration-option.md) (A)|0|32767|5|  
    |[cross db ownership chaining](cross-db-ownership-chaining-server-configuration-option.md)|0|1|0|  
    |[cursor threshold](configure-the-cursor-threshold-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[Database Mail XPs](database-mail-xps-server-configuration-option.md) (A)|0|1|0|  
    |[default full-text language](configure-the-default-full-text-language-server-configuration-option.md) (A)|0|2147483647|1033|  
    |[既定の言語 (default language)](configure-the-default-language-server-configuration-option.md)|0|9999|0|  
    |[default trace enabled](default-trace-enabled-server-configuration-option.md) (A)|0|1|1|  
    |[disallow results from triggers](disallow-results-from-triggers-server-configuration-option.md) (A)|0|1|0|  
    |[EKM provider enabled](ekm-provider-enabled-server-configuration-option.md)|0|1|0|  
    |[filestream_access_level](filestream-access-level-server-configuration-option.md)|0|2|0|  
    |[fill factor](configure-the-fill-factor-server-configuration-option.md) (A、RR)|0|100|0|  
    |ft crawl bandwidth (max)、 [ft crawl bandwidth](ft-crawl-bandwidth-server-configuration-option.md)(A) を参照|0|32767|100|  
    |ft crawl bandwidth (min)、 [ft crawl bandwidth](ft-crawl-bandwidth-server-configuration-option.md)(A) を参照|0|32767|0|  
    |ft notify bandwidth (max)、 [ft notify bandwidth](ft-notify-bandwidth-server-configuration-option.md)(A) を参照|0|32767|100|  
    |ft notify bandwidth (min)、 [ft notify bandwidth](ft-notify-bandwidth-server-configuration-option.md)(A) を参照|0|32767|0|  
    |[index create memory](configure-the-index-create-memory-server-configuration-option.md) (A、SC)|704|2147483647|0|  
    |[in-doubt xact resolution](in-doubt-xact-resolution-server-configuration-option.md) (A)|0|2|0|  
    |[lightweight pooling](lightweight-pooling-server-configuration-option.md) (A、RR)|0|1|0|  
    |[locks](configure-the-locks-server-configuration-option.md) (A、RR、SC)|5000|2147483647|0|  
    |[max degree of parallelism](configure-the-max-degree-of-parallelism-server-configuration-option.md) (A)|0|32767|0|  
    |[max full-text crawl range](max-full-text-crawl-range-server-configuration-option.md) (A)|0|256|4|  
    |[max server memory](server-memory-server-configuration-options.md) (A、SC)|16|2147483647|2147483647|  
    |[max text repl size](configure-the-max-text-repl-size-server-configuration-option.md)|0|2147483647|65536|  
    |[max worker threads](configure-the-max-worker-threads-server-configuration-option.md) (A)|128|32767<br /><br /> (32 ビット版の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では 1024 が、64 ビット版の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では 2048 が推奨されます)|0<br /><br /> 0 の場合、"256+( *\<processors>* -4) * 8" という式 (32 ビット版の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の場合。64 ビット版の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の場合はこの倍) を使用して、プロセッサ数に基づいたワーカー スレッドの最大数が自動的に構成されます。|  
    |[media retention](configure-the-media-retention-server-configuration-option.md) (A、RR)|0|365|0|  
    |[min memory per query](configure-the-min-memory-per-query-server-configuration-option.md) (A)|512|2147483647|1024|  
    |[min server memory](server-memory-server-configuration-options.md) (A、SC)|0|2147483647|0|  
    |[入れ子になったトリガー](configure-the-nested-triggers-server-configuration-option.md)|0|1|1|  
    |[network packet size](configure-the-network-packet-size-server-configuration-option.md) (A)|512|32767|4096|  
    |[Ole Automation Procedures](ole-automation-procedures-server-configuration-option.md) (A)|0|1|0|  
    |[open objects](open-objects-server-configuration-option.md) (A、RR、旧バージョンで使用)|0|2147483647|0|  
    |[optimize for ad hoc workloads](optimize-for-ad-hoc-workloads-server-configuration-option.md) (A)|0|1|0|  
    |[PH_timeout](ph-timeout-server-configuration-option.md) (A)|1|3600|60|  
    |[precompute rank](precompute-rank-server-configuration-option.md) (A)|0|1|0|  
    |[priority boost](configure-the-priority-boost-server-configuration-option.md) (A、RR)|0|1|0|  
    |[query governor cost limit](configure-the-query-governor-cost-limit-server-configuration-option.md) (A)|0|2147483647|0|  
    |[query wait](configure-the-query-wait-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[recovery interval](configure-the-recovery-interval-server-configuration-option.md) (A、SC)|0|32767|0|  
    |[remote access](configure-the-remote-access-server-configuration-option.md) (RR)|0|1|1|  
    |[remote admin connections](remote-admin-connections-server-configuration-option.md)|0|1|0|  
    |[remote login timeout](configure-the-remote-login-timeout-server-configuration-option.md)|0|2147483647|10|  
    |[remote proc trans](configure-the-remote-proc-trans-server-configuration-option.md)|0|1|0|  
    |[remote query timeout](configure-the-remote-query-timeout-server-configuration-option.md)|0|2147483647|600|  
    |[Replication XPs](replication-xps-server-configuration-option.md) (A)|0|1|0|  
    |[scan for startup procs](configure-the-scan-for-startup-procs-server-configuration-option.md) (A、RR)|0|1|0|  
    |[server trigger recursion](server-trigger-recursion-server-configuration-option.md)|0|1|1|  
    |[set working set size](set-working-set-size-server-configuration-option.md) (A、RR、旧バージョンで使用)|0|1|0|  
    |[show advanced options](show-advanced-options-server-configuration-option.md)|0|1|0|  
    |[SMO and DMO XPs](smo-and-dmo-xps-server-configuration-option.md) (A)|0|1|1|  
    |[transform noise words](transform-noise-words-server-configuration-option.md) (A)|0|1|0|  
    |[two digit year cutoff](configure-the-two-digit-year-cutoff-server-configuration-option.md) (A)|1753|9999|2049|  
    |[user connections](configure-the-user-connections-server-configuration-option.md) (A、RR、SC)|0|32767|0|  
    |[user options](configure-the-user-options-server-configuration-option.md)|0|32767|0|  
    |[xp_cmdshell](xp-cmdshell-server-configuration-option.md) (A)|0|1|0|  
  
## <a name="see-also"></a>関連項目  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
