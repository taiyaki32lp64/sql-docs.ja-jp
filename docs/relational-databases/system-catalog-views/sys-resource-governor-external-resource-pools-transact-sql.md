---
title: sys.resource_governor_external_resource_pools (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_external_resource_pools
- sys.resource_governor_external_resource_pools_TSQL
- resource_governor_external_resource_pools
- resource_governor_external_resource_pools_TSQL
helpviewer_keywords:
- sys.resource_governor_external_resource_pools
- resource_governor_external_resource_pools
ms.assetid: 75063e36-a91b-496f-9936-88f3d57bd447
author: stevestein
ms.author: sstein
ms.openlocfilehash: 379dae51b913fc02a16a562037776620b1e0433c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904475"
---
# <a name="sysresourcegovernorexternalresourcepools-transact-sql"></a>sys.resource_governor_external_resource_pools (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**適用対象:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] および [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

格納されている外部リソース プールの構成を返します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 ビューの各行は、プールの構成を決定します。
  
|列名|データ型|説明|
|-----------------|---------------|-----------------|
|pool_id|**int**|リソース プールの一意の ID。 NULL 値は許可されません。<br /><br /> **注:** 後で、名前変更可能性があります。|
|NAME|**sysname**|リソース プールの名前。 NULL 値は許可されません。|
|max_cpu_percent|**int**|最大平均 CPU 帯域幅 CPU の競合がある場合に、リソース プールのすべての要求に許可します。 NULL 値は許可されません。|
|max_memory_percent|**int**|このリソース プールの要求で使用できる合計サーバー メモリの割合。 NULL 値は許可されません。 効果的な最大値は、プールの最小値に依存します。 たとえば、max_memory_percent を 100 に設定できますが、効果的な最大値は低くなります。|
|max_processes|**int**|同時実行の外部プロセスの最大数。 既定値は 0 で、制限がないことを示します。 NULL 値は許可されません。|
|version|**bigint**|内部バージョン番号です。|
  
## <a name="permissions"></a>アクセス許可

VIEW SERVER STATE 権限が必要です。

## <a name="see-also"></a>関連項目

[SQL Server での Machine Learning のリソース管理](../../advanced-analytics/r/resource-governance-for-r-services.md)

[リソース ガバナーのカタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)

[sys.dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)

[リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)

[sys.dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[external scripts enabled サーバー構成オプション](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
