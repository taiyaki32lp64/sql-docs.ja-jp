---
title: dm_pdw_resource_waits (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/26/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a43ce9a2-5261-41e3-97f0-555ba05ebed9
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 46b1155878aae6cc7f667965cfae065ed1a9cacc
ms.sourcegitcommit: 03884a046aded85c7de67ca82a5b5edbf710be92
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/27/2019
ms.locfileid: "74564742"
---
# <a name="sysdm_pdw_resource_waits-transact-sql"></a>dm_pdw_resource_waits (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  の[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]すべてのリソースの種類の待機情報を表示します。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|待機リスト内の要求の位置。|0から始まる序数。 これは、すべての待機エントリで一意ではありません。|  
|session_id|**nvarchar (32)**|待機状態が発生したセッションの ID。|『 [Transact-sql&#41;&#40;dm_pdw_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)の session_id を参照してください。|  
|型|**nvarchar(255)**|このエントリが表す待機の種類。|指定できる値<br /><br /> 接続<br /><br /> ローカルクエリの同時実行<br /><br /> 分散クエリの同時実行<br /><br /> DMS の同時実行<br /><br /> バックアップの同時実行|  
|object_type|**nvarchar(255)**|待機の影響を受けるオブジェクトの種類。|指定できる値<br /><br /> **素材**<br /><br /> **データベース**<br /><br /> **SYSTEM**<br /><br /> **スキーマ**<br /><br /> **適用**|  
|object_name|**nvarchar (386)**|待機の影響を受けた、指定したオブジェクトの名前または GUID。|テーブルとビューは、3つの部分で構成される名前で表示されます。<br /><br /> インデックスと統計情報は、4つの部分で構成される名前で表示されます。<br /><br /> 名前、プリンシパル、およびデータベースは、文字列名です。|  
|request_id|**nvarchar (32)**|待機状態が発生した要求の ID。|要求の QID 識別子。<br /><br /> 読み込み要求の GUID 識別子。|  
|request_time|**/**|ロックまたはリソースが要求された時刻。||  
|acquire_time|**/**|ロックまたはリソースが取得された時刻。||  
|state|**nvarchar(50)**|待機状態の状態。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**通り**|待機中の項目の優先順位。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|concurrency_slots_used|**通り**|内部|下記の「[リソース待機を監視](#monitor-resource-waits)する」を参照してください。|  
|resource_class|**nvarchar (20)**|内部 |下記の「[リソース待機を監視](#monitor-resource-waits)する」を参照してください。|  
  
## <a name="monitor-resource-waits"></a>リソース待機の監視 
[ワークロードグループ](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-workload-isolation)の導入により、同時実行スロットは適用されなくなりました。  次のクエリと`resources_requested`列を使用して、要求の実行に必要なリソースを把握します。

```sql
select rw.wait_id
      ,rw.session_id
      ,rw.type
      ,rw.object_type
      ,rw.object_name
      ,rw.request_id
      ,rw.request_time
      ,rw.acquire_time
      ,rw.state
      ,resources_requested = s.effective_request_min_resource_grant_percent
      ,r.group_name
  from sys.dm_workload_management_workload_groups_stats s
  join sys.dm_pdw_exec_requests r on r.group_name = s.name collate SQL_Latin1_General_CP1_CI_AS
  join sys.dm_pdw_resource_waits rw on rw.request_id = r.request_id
```

## <a name="see-also"></a>参照  
 [SQL Data Warehouse および並列データウェアハウスの動的管理ビュー &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
