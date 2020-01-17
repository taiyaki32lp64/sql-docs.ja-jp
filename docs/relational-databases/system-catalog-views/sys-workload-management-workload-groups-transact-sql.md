---
title: sys.workload_management_workload_groups (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 76b5b09a07189db127c970e75dac2894fdbea1ae
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73633446"
---
# <a name="sysworkload_management_workload_groups-transact-sql"></a>sys.workload_management_workload_groups (Transact-sql)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

 ワークロードグループの詳細を返します。  
  
|列名|[データ型]|説明|範囲|  
|-----------------|---------------|-----------------|-----------|
|group_id|**int**|ワークロード グループの一意の ID。 NULL 値は許可されません。||
|name|**sysname**|ワークロードグループの名前。 インスタンスに対して一意である必要があります。  NULL 値は許可されません。||
|importance|**nvarchar(128)**|は、このワークロードグループ内の要求の相対的な重要度であり、共有リソースの複数のワークロードグループにまたがっています。 NULL 値は許可されません。|low、below_normal、normal (既定)、above_normal、high||
|min_percentage_resource|**tinyint**|ワークロードグループ内の要求に対して確保されるリソースの量。 リソースは、他のワークロードグループと共有されません。 NULL 値は許可されません。||
|cap_percentage_resource|**tinyint**|ワークロードグループ内の要求に対するリソース割り当ての割合 (%)。 指定されたレベルに割り当てられるリソースの最大数を制限します。 値の許容範囲は、1 ~ 100 です。||
|request_min_resource_grant_percent|**decimal (5, 2)**|要求に割り当てられるリソースの最小量を指定します。 値の許容範囲は 0.75 ~ 100 です。||
|request_max_resource_grant_percent |**decimal (5, 2)**|要求に割り当てられるリソースの最大量を指定します。||
|query_execution_timeout_sec|**int**|クエリが取り消されるまでの実行時間の長さ (秒単位)。  実行の戻りフェーズに達した後は、クエリを取り消すことはできません。  query_execution_timeout_sec には、キューに置かれた時間は含まれません。|
|query_wait_timeout_sec|**int**|内部使用||
|create_time|**datetime**|ワークロードグループが作成された時刻。 NULL 値は許可されません。||
modify_time|**datetime**|ワークロードグループが最後に変更された時刻。 NULL 値は許可されません。||
|&nbsp;||||
  
## <a name="permissions"></a>アクセス許可

VIEW SERVER STATE 権限が必要です。

## <a name="next-steps"></a>次の手順

 SQL Data Warehouse と並列データウェアハウスのすべてのカタログビューの一覧については、「 [SQL Data Warehouse および並列データウェアハウスのカタログビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)」を参照してください。 ワークロードグループを作成するには、「[ワークロードグループの作成](../../t-sql/statements/create-workload-group-transact-sql.md)」を参照してください。 ワークロードの分類の詳細については、「[ワークロードの分離](/azure/sql-data-warehouse/sql-data-warehouse-workload-isolation)」を参照してください。
