---
title: ALTER RESOURCE POOL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_RESOURCE_POOL_TSQL
- ALTER RESOURCE POOL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER RESOURCE POOL
ms.assetid: 9c1c4cfb-0e3b-4f01-bf57-3fce94c7d1d4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 57849c8d99700f61c251177c3c3195b2277163ae
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982087"
---
# <a name="alter-resource-pool-transact-sql"></a>ALTER RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、既存の Resource Governor リソース プールの構成を変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>構文  
  
```  
ALTER RESOURCE POOL { pool_name | "default" }  
[WITH  
    ( [ MIN_CPU_PERCENT = value ]  
    [ [ , ] MAX_CPU_PERCENT = value ]   
    [ [ , ] CAP_CPU_PERCENT = value ]   
    [ [ , ] AFFINITY {
                        SCHEDULER = AUTO 
                      | ( <scheduler_range_spec> ) 
                      | NUMANODE = ( <NUMA_node_range_spec> )
                      }]   
    [ [ , ] MIN_MEMORY_PERCENT = value ]  
    [ [ , ] MAX_MEMORY_PERCENT = value ]   
    [ [ , ] MIN_IOPS_PER_VOLUME = value ]  
    [ [ , ] MAX_IOPS_PER_VOLUME = value ]  
)]   
[;]  
  
<scheduler_range_spec> ::=  
{SCHED_ID | SCHED_ID TO SCHED_ID}[,...n]  
  
<NUMA_node_range_spec> ::=  
{NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID}[,...n]  
```  
  
## <a name="arguments"></a>引数  
 { *pool_name* |  **"default"** }  
 既存のユーザー定義のリソース プール、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールする際に作成される既定のリソース プールの名前です。  
  
 "default" を ALTER RESOURCE POOL で使用する場合は、システム予約語の DEFAULT と競合しないように引用符 ("") または角かっこ ([]) で囲む必要があります。 詳細については、「[データベース識別子](../../relational-databases/databases/database-identifiers.md)」を参照してください。  
  
> [!NOTE]  
>  定義済みのワークロード グループおよびリソース プールはすべて、"default" などの小文字の名前を使用しています。 大文字と小文字を区別する照合順序を使用するサーバーでは、これを考慮する必要があります。 SQL_Latin1_General_CP1_CI_AS など、大文字と小文字を区別しない照合順序を使用するサーバーでは、"default" と "Default" が同じものと見なされます。  
  
 MIN_CPU_PERCENT =*value*  
 CPU の競合がある場合に、リソース プールのすべての要求に保証される平均 CPU 帯域幅を指定します。 *value* は整数で、既定の設定は 0 です。 *value* の許容範囲は 0 から 100 までです。  
  
 MAX_CPU_PERCENT =*value*  
 CPU の競合がある場合に、このリソース プールのすべての要求に割り当てられる最大平均 CPU 帯域幅を指定します。 *value* は整数で、既定の設定は 100 です。 *value* の許容範囲は 1 から 100 までです。  
  
 CAP_CPU_PERCENT =*value*  
 **適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。  
  
 リソース プールでは、要求のターゲットの最大 CPU 容量を指定します。 *value* は整数で、既定の設定は 100 です。 *value* の許容範囲は 1 ～ 100 です。  
  
> [!NOTE]  
>  CPU の管理の統計の性質により、CAP_CPU_PERCENT で指定された値を超える不定期な急増に気付く場合があります。  
  
 AFFINITY {SCHEDULER = AUTO | (Scheduler_range_spec) | NUMANODE = (NUMA_node_range_spec)}  
 **適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。  
  
 リソース プールを特定のスケジューラにアタッチします。 既定値は AUTO です。  
  
 AFFINITY SCHEDULER = (Scheduler_range_spec) は、指定した ID によって識別される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スケジューラにリソース プールをマップします。 これらの ID は、[sys.dm_os_schedulers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md) の scheduler_id 列の値にマップされます。  
  
 AFFINITY NAMANODE = (NUMA_node_range_spec) を使用すると、リソース プールは、指定した NUMA ノードまたはノードの範囲に対応する物理 CPU にマップされた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスケジューラに関連付けられます。 次の Transact-SQL クエリを使用して、物理 NUMA 構成と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スケジューラ ID のマッピングを検出できます。  
  
```  
SELECT osn.memory_node_id AS [numa_node_id], sc.cpu_id, sc.scheduler_id  
FROM sys.dm_os_nodes AS osn  
INNER JOIN sys.dm_os_schedulers AS sc 
   ON osn.node_id = sc.parent_node_id 
      AND sc.scheduler_id < 1048576;  
```  
  
 MIN_MEMORY_PERCENT =*value*  
 このリソース プール用に確保され、他のリソース プールとは共有できないメモリ量の最小値を指定します。 *value* は整数で、既定の設定は 0 です。 *value* の許容範囲は 0 から 100 までです。  
  
 MAX_MEMORY_PERCENT =*value*  
 このリソース プールの要求で使用できる合計サーバー メモリを指定します。 *value* は整数で、既定の設定は 100 です。 *value* の許容範囲は 1 から 100 までです。  
  
 MIN_IOPS_PER_VOLUME =*value*  
 **適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。  
  
 リソース プール用に確保するために、ディスク ボリュームごとに、1 秒あたりの最小 I/O 操作 (IOPS) を指定します。 *value* の許容範囲は 0 から 2^31-1 (2,147,483,647) までです。 プールに最小しきい値を指定しない場合は 0 を指定します。  
  
 MAX_IOPS_PER_VOLUME =*value*  
 **適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。  
  
 リソース プールに許された、ディスク ボリュームごとの 1 秒あたりの最大 I/O 操作 (IOPS) 回数を指定します。 *value* の許容範囲は 0 から 2^31-1 (2,147,483,647) までです。 プールに無制限のしきい値を設定する場合は 0 を指定します。 既定値は 0 です。  
  
 プールの MAX_IOPS_PER_VOLUME を 0 に設定した場合、プールはまったく管理されなくなり、他のプールで MIN_IOPS_PER_VOLUME が設定されていても、システムですべての IOPS を行うことがあります。 この場合、IO についてこのプールが管理されるようにするには、このプールの MAX_IOPS_PER_VOLUME の値をより大きな数値 (たとえば、最大値 2^31-1) に設定することをお勧めします。  
  
## <a name="remarks"></a>Remarks  
 MAX_CPU_PERCENT と MAX_MEMORY_PERCENT には、それぞれ MIN_CPU_PERCENT と MIN_MEMORY_PERCENT 以上の値を指定する必要があります。  
  
 MAX_CPU_PERCENT は、使用可能になる場合、MAX_CPU_PERCENT の値を上回る CPU 容量を使用できます。 CAP_CPU_PERCENT を上回る急増が定期的に発生する場合がありますが、追加の CPU 容量が使用可能な場合でも、長時間にわたって CAP_CPU_PERCENT を超えることはありません。  
  
 関連付けられた各コンポーネント (スケジューラまたは NUMA ノード) の CPU 使用率の合計が 100% を超えることはできません。  
  
 DDL ステートメントを実行する場合、Resource Governor の状態について詳しく理解しておくことをお勧めします。 詳細については、「[リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)」を参照してください。  
  
 プランを変更し、設定に影響が出るとき、新しい設定は、DBCC FREEPROCCACHE (*pool_name*) の実行後にのみ、前にキャッシュされたプランに反映されます。*pool_name* は Resource Governor リソース プールの名前です。  
  
-   複数のスケジューラから 1 つのスケジューラに AFFINITY を変更する場合、並列プランは直列モードで実行できるため、DBCC FREEPROCCACHE を実行する必要はありません。 ただし、直列プランとしてコンパイルされたプランほど効率的ではない可能性があります。  
  
-   1 つのスケジューラから複数のスケジューラに AFFINITY を変更する場合、DBCC FREEPROCCACHE を実行する必要はありません。 ただし、直列プランは並列で実行できません。そのため、個々のキャッシュを消去すると、場合によっては、新しいプランを並列処理でコンパイルできます。  
  
> [!CAUTION]  
>  複数のワークロード グループに関連付けられているリソース プールからキャッシュされているプランを消去すると、ユーザー定義のリソース プールが *pool_name* で識別されているすべてのワークロード グループに影響します。  
  
## <a name="permissions"></a>アクセス許可  
 CONTROL SERVER 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、`MAX_CPU_PERCENT` を `25` に変更する以外は、すべて `default` プールの既定のリソース プール設定が保持されます。  
  
```  
ALTER RESOURCE POOL "default"  
WITH  
     ( MAX_CPU_PERCENT = 25);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
 次の例では、`CAP_CPU_PERCENT` はハード キャップを 80% に設定し、`AFFINITY SCHEDULER` は個別値 8 と範囲 12 ～ 16 に設定されています。  
  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。  
  
```  
ALTER RESOURCE POOL Pool25  
WITH(   
     MIN_CPU_PERCENT = 5,  
     MAX_CPU_PERCENT = 10,       
     CAP_CPU_PERCENT = 80,  
     AFFINITY SCHEDULER = (8, 12 TO 16),   
     MIN_MEMORY_PERCENT = 5,  
     MAX_MEMORY_PERCENT = 15  
);  
  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
  
```  
  
## <a name="see-also"></a>参照  
 [リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
