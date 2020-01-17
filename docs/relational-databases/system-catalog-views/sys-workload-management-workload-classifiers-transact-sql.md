---
title: workload_management_workload_classifiers (Transact-sql) |Microsoft Docs
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
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 585eb4551fb688f4f6a620729310b0245462cbff
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632962"
---
# <a name="sysworkload_management_workload_classifiers-transact-sql"></a>workload_management_workload_classifiers (Transact-sql)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

 ワークロード分類子の詳細を返します。  
  
|列名|[データ型]|説明|範囲|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|分類子の一意の ID。 Null 値はありません||
group_name|**sysname**|分類子が割り当てられているワークロードグループの名前。 NULL 値は許可されません。 Workload_management_workload_groups に参加可能 ||
name|**sysname**|分類子の名前。 インスタンスに対して一意である必要があります。 NULL 値は許可されません。||
|importance|**sysname**|は、このワークロードグループ内の要求の相対的な重要度であり、共有リソースの複数のワークロードグループにまたがっています。  分類子で指定された重要度は、ワークロードグループの重要度の設定よりも優先されます。 NULL 値が許可されます。  Null の場合、ワークロードグループの重要度の設定が使用されます。|low、below_normal、normal (既定)、above_normal、high |
|create_time|**datetime**|分類子が作成された時刻。 NULL 値は許可されません。||
modify_time|**datetime**|分類子が最後に変更された時刻。 NULL 値は許可されません。||
is_enabled|**bit**|イントラネット||
|&nbsp;||||
  
## <a name="permissions"></a>アクセス許可

VIEW SERVER STATE 権限が必要です。

## <a name="next-steps"></a>次の手順

 SQL Data Warehouse と並列データウェアハウスのすべてのカタログビューの一覧については、「 [SQL Data Warehouse および並列データウェアハウスのカタログビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)」を参照してください。 ワークロード分類子を作成するには、「[ワークロード分類子を作成](../../t-sql/statements/create-workload-classifier-transact-sql.md)する」を参照してください。 ワークロードの分類の詳細については、「[ワークロードの分類](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)」を参照してください。
