---
title: CREATE EXTERNAL RESOURCE POOL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/07/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL RESOURCE POOL
- CREATE EXTERNAL_RESOURCE_POOL_TSQL
- EXTERNAL RESOURCE POOL
- EXTERNAL_RESOURCE_POOL_TSQL
- EXTERNAL RESOURCE
- EXTERNAL_RESOURCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EXTERNAL RESOURCE POOL statement
ms.assetid: 8cc798ad-c395-461c-b7ff-8c561c098808
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 7c55041d7b461406305a7b3a17c0e274270b7c5f
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893891"
---
# <a name="create-external-resource-pool-transact-sql"></a>CREATE EXTERNAL RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

外部プロセス用のリソースの定義に使われる外部プールを作成します。 リソース プールは、データベース エンジン インスタンスの物理リソース (メモリと CPU) のサブセットを表します。 データベース管理者は、リソース ガバナーを使用することで、サーバー リソースを最大 64 個までのリソース プールに分散できます。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] の [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] の場合、外部プールは `rterm.exe`、`BxlServer.exe`、およびそれらにより生成された他のプロセスを管理します。
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] の場合、外部プールは `rterm.exe`、`python.exe`、`BxlServer.exe`、およびそれらにより生成された他のプロセスを管理します。
::: moniker-end
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>構文  
  
```  
CREATE EXTERNAL RESOURCE POOL pool_name  
[ WITH (  
    [ MAX_CPU_PERCENT = value ]  
    [ [ , ] AFFINITY CPU =    
            {  
                AUTO   
              | ( <cpu_range_spec> )   
              | NUMANODE = ( <NUMA_node_id> )   
            } ]   
    [ [ , ] MAX_MEMORY_PERCENT = value ]  
    [ [ , ] MAX_PROCESSES = value ]   
    )   
]  
[ ; ]  
  
<CPU_range_spec> ::=    
{ CPU_ID | CPU_ID  TO CPU_ID } [ ,...n ]  
```  
  
## <a name="arguments"></a>引数

*pool_name*  
外部リソース プールのユーザー定義名を指定します。 *pool_name* には、最大 128 文字の英数字を指定できます。 この引数は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内で一意であり、[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。  

MAX_CPU_PERCENT =*value*  
CPU の競合がある場合に、この外部リソース プールのすべての要求が受け取ることのできる最大平均 CPU 帯域幅を指定します。 *value* は整数です。 *value* の許容範囲は 1 ～ 100 です。

AFFINITY {CPU = AUTO | ( \<CPU_range_spec> ) | NUMANODE = (\<NUMA_node_range_spec>)} Attach the external resource pool to specific CPUs.

AFFINITY CPU = **(** \<CPU_range_spec> **)** maps the external resource pool to the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPUs identified by the given CPU_IDs.

AFFINITY NUMANODE = **(** \<NUMA_node_range_spec> **)** を使うと、外部リソース プールは、指定した NUMA ノードまたはノードの範囲に対応する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物理 CPU に関連付けられます。 

MAX_MEMORY_PERCENT =*value*  
この外部リソース プールの要求で使用できる合計サーバー メモリを指定します。 *value* は整数です。 *value* の許容範囲は 1 ～ 100 です。

MAX_PROCESSES =*value*  
外部リソース プールに許されるプロセスの最大数を指定します。 0 を指定すると、プールのしきい値は無制限になり、その後はコンピューターのリソースによってのみ拘束されます。

## <a name="remarks"></a>Remarks

[ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md) ステートメントを実行すると、[!INCLUDE[ssDE](../../includes/ssde-md.md)]はリソース プールを実装します。

リソース プールの一般的な情報については、「[リソース ガバナー リソース プール](../../relational-databases/resource-governor/resource-governor-resource-pool.md)」、「[sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)」、および「[sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)」をご覧ください。

機械学習で使用される外部リソース プールの管理に固有の情報については、「[Resource governance for machine learning in SQL Server (SQL Server での機械学習のリソース管理)](../../advanced-analytics/r/resource-governance-for-r-services.md)」をご覧ください。 

## <a name="permissions"></a>アクセス許可

`CONTROL SERVER` 権限が必要です。

## <a name="examples"></a>使用例

次のステートメントは、CPU 使用率を 75% に制限する外部プールを定義します。 このステートメントは、最大メモリをコンピューターで使用可能なメモリの 30% にすることも定義します。

```sql
CREATE EXTERNAL RESOURCE POOL ep_1
WITH (  
    MAX_CPU_PERCENT = 75
    , AFFINITY CPU = AUTO
    , MAX_MEMORY_PERCENT = 30
);
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```
  
## <a name="see-also"></a>参照

+ [external scripts enabled サーバー構成オプション](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)
+ [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
+ [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)
+ [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)
+ [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)
+ [リソース ガバナー リソース プール](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
+ [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)
+ [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)
+ [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)
