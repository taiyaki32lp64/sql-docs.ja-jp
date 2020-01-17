---
title: CREATE RESOURCE POOL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE RESOURCE POOL
- RESOURCE POOL
- CREATE_RESOURCE_POOL_TSQL
- RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE RESOURCE POOL
ms.assetid: 82712505-c6f9-4a65-a469-f029b5a2d6cd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2830c7ae4166ee0b71b1ddfb9de953c57be2452d
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982686"
---
# <a name="create-resource-pool-transact-sql"></a>CREATE RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でリソース ガバナー リソース プールを作成します。 リソース プールは、データベース エンジンのインスタンスに関する物理リソース (メモリ、CPU、および IO) のサブセットを表します。 データベース管理者は、リソース ガバナーを使用することで、サーバー リソースを最大 64 個までのリソース プールに分散できます。 リソース ガバナーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>構文  
```  
CREATE RESOURCE POOL pool_name  
[ WITH  
    (  
        [ MIN_CPU_PERCENT = value ]  
        [ [ , ] MAX_CPU_PERCENT = value ]   
        [ [ , ] CAP_CPU_PERCENT = value ]   
        [ [ , ] AFFINITY {SCHEDULER =  
                  AUTO 
                | ( <scheduler_range_spec> )   
                | NUMANODE = ( <NUMA_node_range_spec> )
                } ]   
        [ [ , ] MIN_MEMORY_PERCENT = value ]  
        [ [ , ] MAX_MEMORY_PERCENT = value ]  
        [ [ , ] MIN_IOPS_PER_VOLUME = value ]  
        [ [ , ] MAX_IOPS_PER_VOLUME = value ]  
    )   
]  
[;]  
  
<scheduler_range_spec> ::=  
{ SCHED_ID | SCHED_ID TO SCHED_ID }[,...n]  
  
<NUMA_node_range_spec> ::=  
{ NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID }[,...n]  
```  
  
## <a name="arguments"></a>引数  
*pool_name*  
リソース プールのユーザー定義名を指定します。 *pool_name* には英数字を最大 128 文字まで使用できます。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内で一意である必要があり、[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。  
  
MIN_CPU_PERCENT =*value*  
CPU の競合がある場合に、リソース プールのすべての要求に保証される平均 CPU 帯域幅を指定します。 *value* は整数で、既定の設定は 0 です。 *value* の許容範囲は 0 から 100 までです。  
  
MAX_CPU_PERCENT =*value*  
CPU の競合がある場合に、リソース プールのすべての要求に割り当てられる最大平均 CPU 帯域幅を指定します。 *value* は整数で、既定の設定は 100 です。 *value* の許容範囲は 1 ～ 100 です。  
  
CAP_CPU_PERCENT =*value*   
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。  
  
リソース プールのすべての要求に割り当てられる、CPU 帯域幅のハード キャップを指定します。 CPU の最大帯域幅レベルを、指定した値と同じレベルに制限します。 *value* は整数で、既定の設定は 100 です。 *value* の許容範囲は 1 ～ 100 です。  
  
AFFINITY {SCHEDULER = AUTO | ( \<scheduler_range_spec> ) | NUMANODE = (\<NUMA_node_range_spec>)}      
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。  
  
リソース プールを特定のスケジューラにアタッチします。 既定値は AUTO です。  
  
AFFINITY SCHEDULER = **(** \<scheduler_range_spec> **)** は、指定した ID によって識別される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スケジュールにリソース プールをマップします。 これらの ID は、[sys.dm_os_schedulers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md) の scheduler_id 列の値にマップされます。 
  
AFFINITY NUMANODE = **(** \<NUMA_node_range_spec> **)** を使用すると、リソース プールは、指定した NUMA ノードまたはノードの範囲に対応する物理 CPU にマップされた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスケジューラに関連付けられます。 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリを使用して、物理 NUMA 構成と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スケジューラ ID のマッピングを検出できます。 
  
```sql  
SELECT osn.memory_node_id AS [numa_node_id], sc.cpu_id, sc.scheduler_id  
FROM sys.dm_os_nodes AS osn  
INNER JOIN sys.dm_os_schedulers AS sc   
    ON osn.node_id = sc.parent_node_id   
    AND sc.scheduler_id < 1048576;  
```  
  
MIN_MEMORY_PERCENT =*value*    
このリソース プール用に確保され、他のリソース プールとは共有できないメモリ量の最小値を指定します。 *value* は整数で、既定の設定は 0 です。*value* の許容範囲は 0 から 100 です。  
  
MAX_MEMORY_PERCENT =*value*    
このリソース プールの要求で使用できる合計サーバー メモリを指定します。 *value* は整数で、既定の設定は 100 です。 *value* の許容範囲は 1 ～ 100 です。  
  
MIN_IOPS_PER_VOLUME =*value*    
**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。  
  
リソース プール用に確保するために、ディスク ボリュームごとに、1 秒あたりの最小 I/O 操作 (IOPS) を指定します。 *value* の許容範囲は 0 から 2^31-1 (2,147,483,647) までです。 プールに最小しきい値を指定しない場合は 0 を指定します。 既定値は 0 です。  
  
MAX_IOPS_PER_VOLUME =*value*    
**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。  
  
リソース プールに許された、ディスク ボリュームごとの 1 秒あたりの最大 I/O 操作 (IOPS) 回数を指定します。 *value* の許容範囲は 0 から 2^31-1 (2,147,483,647) までです。 プールに無制限のしきい値を設定する場合は 0 を指定します。 既定値は 0 です。  
  
プールの `MAX_IOPS_PER_VOLUME` を 0 に設定した場合、プールは管理されなくなり、他のプールで MIN_IOPS_PER_VOLUME が設定されていても、システムですべての IOPS を行うことがあります。 この場合、IO についてこのプールが管理されるようにするには、このプールの `MAX_IOPS_PER_VOLUME` の値をより大きな数値 (たとえば、最大値 2^31-1) に設定することをお勧めします。  
  
## <a name="remarks"></a>Remarks  
`MIN_IOPS_PER_VOLUME` と `MAX_IOPS_PER_VOLUME` は、1 秒あたりに行われる読み取りまたは書き込みの最小数と最大数を指定します。 これらの読み取りと書き込みでは任意のサイズを処理できます。これらの値は、最小または最大のスループットを示すものではありません。  
  
`MAX_CPU_PERCENT` と `MAX_MEMORY_PERCENT` の値は、それぞれ `MIN_CPU_PERCENT` と `MIN_MEMORY_PERCENT` の値以上である必要があります。  
  
`CAP_CPU_PERCENT` と `MAX_CPU_PERCENT` の違いは、プールに関連付けられているワークロードが使用する CPU 処理量が、`MAX_CPU_PERCENT` の値を超えることはできても (利用可能な場合)、`CAP_CPU_PERCENT` の値を超えることはできない点です。  
  
関連付けられた各コンポーネント (スケジューラまたは NUMA ノード) の CPU 使用率の合計が 100% を超えることはできません。  
  
## <a name="permissions"></a>アクセス許可  
`CONTROL SERVER` 権限が必要です。  
  
## <a name="examples"></a>使用例  
### <a name="1-shows-how-to-create-a-resource-pool"></a>1.リソース プールを作成する方法について説明します

次の例では、"bigPool" というリソース プールを作成します。 このプールは、Resource Governor の既定の設定を使用します。  
  
```sql  
CREATE RESOURCE POOL bigPool;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
### <a name="2-set-the-cap_cpu_percent-to-a-hard-cap-and-set-affinity-scheduler"></a>2.CAP_CPU_PERCENT をハード キャップに設定し、AFFINITY SCHEDULER を設定します

CAP_CPU_PERCENT を 30% のハード キャップに設定し、AFFINITY SCHEDULER を 0-63、128-191 の範囲に設定します。 
  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。  
  
```sql  
CREATE RESOURCE POOL PoolAdmin  
WITH (  
     MIN_CPU_PERCENT = 10,  
     MAX_CPU_PERCENT = 20,  
     CAP_CPU_PERCENT = 30,  
     AFFINITY SCHEDULER = (0 TO 63, 128 TO 191),  
     MIN_MEMORY_PERCENT = 5,  
     MAX_MEMORY_PERCENT = 15  
      );  
```  
  
### <a name="3-set-min_iops_per_volume-and-max_iops_per_volume"></a>3.MIN_IOPS_PER_VOLUME と MAX_IOPS_PER_VOLUME を設定します   

MIN_IOPS_PER_VOLUME を 20 に、MAX_IOPS_PER_VOLUME を 100 に設定します。 これらの値は、リソース プールで使用できる物理 I/O の読み取りと書き込みの操作を制御します。  
  
**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。  
  
```sql  
CREATE RESOURCE POOL PoolAdmin  
WITH (  
    MIN_IOPS_PER_VOLUME = 20,  
    MAX_IOPS_PER_VOLUME = 100  
      );  
```  
  
## <a name="see-also"></a>参照  
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)     
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)     
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)     
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)     
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)     
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)     
 [リソース ガバナー リソース プール](../../relational-databases/resource-governor/resource-governor-resource-pool.md)     
 [リソース プールの作成](../../relational-databases/resource-governor/create-a-resource-pool.md)    
  
