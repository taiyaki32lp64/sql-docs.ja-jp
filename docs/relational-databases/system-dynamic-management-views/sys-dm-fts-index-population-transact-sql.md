---
title: dm_fts_index_population (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_population
- dm_fts_index_population
- sys.dm_fts_index_population_TSQL
- dm_fts_index_population_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_index_population dynamic management view
ms.assetid: 82d1c102-efcc-4b60-9a5e-3eee299bcb2b
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7af62bc20e96d3c9ab9508b89244d6401356d7ef
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983112"
---
# <a name="sysdm_fts_index_population-transact-sql"></a>sys.dm_fts_index_population (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で現在実行中の、フルテキスト インデックス作成およびセマンティック キー フレーズ作成に関する情報を返します。  
 
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|作成中のフルテキスト インデックスを含むデータベースの ID。|  
|**catalog_id**|**int**|フルテキスト インデックスを含む、フルテキスト カタログの ID。|  
|**table_id**|**int**|フルテキスト インデックスを設定しているテーブルの ID。|  
|**memory_address**|**varbinary(8)**|アクティブな設定を表すときに使用される内部データ構造のメモリ アドレス。|  
|**population_type**|**int**|設定の種類。 次のいずれかです。<br /><br /> 1 = 完全設定<br /><br /> 2 = タイムスタンプに基づく増分設定<br /><br /> 3 = 追跡した変更の手動更新<br /><br /> 4 = 追跡した変更のバックグラウンド更新|  
|**population_type_description**|**nvarchar(120)**|設定の種類の説明。|  
|**is_clustered_index_scan**|**bit**|設定では、クラスター化されたインデックスでのスキャンが行われるかどうかを示します。|  
|**range_count**|**int**|インデックス設定が並列処理されたサブ範囲の数。|  
|**completed_range_count**|**int**|処理が完了した範囲の数。|  
|**outstanding_batch_count**|**int**|このインデックス設定で現在未解決のバッチの数。 詳細については、「 [sys &#40;. dm_fts_outstanding_batches transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md)」を参照してください。|  
|**ステータス**|**int**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> 設定の状態。 注 : 状態によっては、一時的なものもあります。 次のいずれかです。<br /><br /> 3 = 開始<br /><br /> 5 = 正常に処理中<br /><br /> 7 = 処理を停止<br /><br /> たとえば、この状態は自動マージの進行中に発生します。<br /><br /> 11 = 作成が中止されました<br /><br /> 12 = セマンティックな類似性の抽出を実行中|  
|**status_description**|**nvarchar(120)**|作成の状態の説明。|  
|**completion_type**|**int**|設定の完了の状態。|  
|**completion_type_description**|**nvarchar(120)**|完了の種類の説明。|  
|**worker_count**|**int**|この値は常に 0 です。|  
|**queued_population_type**|**int**|現在のインデックス設定の次に設定が行われる場合、追跡した変更に基づく設定の種類。|  
|**queued_population_type_description**|**nvarchar(120)**|次にインデックス設定が行われる場合、その説明。 たとえば、CHANGE TRACKING = AUTO が設定されており、最初の完全設定が進行中の場合、この列には "Auto population" と表示されます。|  
|**start_time**|**datetime**|設定を開始した時刻。|  
|**incremental_timestamp**|**timestamp**|完全設定の開始タイムスタンプ。 他の作成の種類の場合、この値は作成の進行状況を表す、最後にコミットされたチェックポイントの値になります。|  
  
## <a name="remarks"></a>Remarks  
 フルテキスト インデックス作成に加えて統計的セマンティック インデックス作成が有効になっている場合は、キー フレーズのセマンティックな抽出と作成、およびドキュメントの類似性データの抽出が、フルテキスト インデックス作成と同時に実行されます。 ドキュメントの類似性に関するインデックスの作成は、2 番目のフェーズで実行されます。 詳細については、「[セマンティック検索の管理と監視](../../relational-databases/search/manage-and-monitor-semantic-search.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]では、`VIEW SERVER STATE` のアクセス許可が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、データベースの `VIEW DATABASE STATE` アクセス許可が必要です。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard レベルと Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
  
## <a name="physical-joins"></a>物理結合  
 ![この動的管理ビューの重要な結合](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-index-population-1.gif "この動的管理ビューの重要な結合")  
  
## <a name="relationship-cardinalities"></a>リレーションシップの基数  
  
|From|変換先|[リレーションシップ]|  
|----------|--------|------------------|  
|dm_fts_active_catalogs.database_id|dm_fts_index_population.database_id|一対一|  
|dm_fts_active_catalogs.catalog_id|dm_fts_index_population.catalog_id|一対一|  
|dm_fts_population_ranges.parent_memory_address|dm_fts_index_population.memory_address|多対一|  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [フルテキスト検索とセマンティック検索の動的管理ビューおよび関数&#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  

