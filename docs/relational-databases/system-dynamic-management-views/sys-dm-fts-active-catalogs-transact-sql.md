---
title: sys.dm_fts_active_catalogs (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_active_catalogs_TSQL
- dm_fts_active_catalogs
- dm_fts_active_catalogs_TSQL
- sys.dm_fts_active_catalogs
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_active_catalogs dynamic management view
ms.assetid: 40ab5453-040c-4d2e-bb49-e340cf90c3ee
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 31dd240f15d9d778cbab43f6b4b1bfda2e4e1857
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265974"
---
# <a name="sysdmftsactivecatalogs-transact-sql"></a>sys.dm_fts_active_catalogs (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  サーバー上で進行中の作成操作である、フルテキスト カタログ情報を返します。  
  
> [!NOTE]
>  次の列は将来のバージョンで削除する[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: is_paused、previous_status、previous_status_description、row_count_in_thousands、状態、status_description、および worker_count します。 新しい開発作業でこれらの列を使用しないようにして、現在これらのいずれかを使用しているアプリケーションの変更を検討してください。  
  
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|アクティブなフルテキスト カタログを含むデータベースの ID。|  
|**catalog_id**|**int**|アクティブなフルテキスト カタログの ID。|  
|**memory_address**|**varbinary(8)**|このフルテキスト カタログに関連する作成操作に割り当てられたメモリ バッファーのアドレス。|  
|**name**|**nvarchar(128)**|アクティブなフルテキスト カタログの名前。|  
|**is_paused**|**bit**|アクティブなフルテキスト カタログの作成が一時停止されているかどうかを示します。|  
|**status**|**int**|フルテキスト カタログの現在の状態。 次のいずれかです。<br /><br /> 0 = 初期化しています<br /><br /> 1 = 準備完了<br /><br /> 2 = 一時停止<br /><br /> 3 = 一時エラー<br /><br /> 4 = 再マウントが必要<br /><br /> 5 = シャットダウン<br /><br /> 6 = バックアップのための停止<br /><br /> 7 = カタログからのバックアップ完了<br /><br /> 8 = カタログが破損しています|  
|**status_description**|**nvarchar(120)**|アクティブなフルテキスト カタログの現在の状態に関する説明。|  
|**previous_status**|**int**|フルテキスト カタログの以前の状態。 次のいずれかです。<br /><br /> 0 = 初期化しています<br /><br /> 1 = 準備完了<br /><br /> 2 = 一時停止<br /><br /> 3 = 一時エラー<br /><br /> 4 = 再マウントが必要<br /><br /> 5 = シャットダウン<br /><br /> 6 = バックアップのための停止<br /><br /> 7 = カタログからのバックアップ完了<br /><br /> 8 = カタログが破損しています|  
|**previous_status_description**|**nvarchar(120)**|アクティブなフルテキスト カタログの以前の状態の説明です。|  
|**worker_count**|**int**|このフルテキスト カタログで現在動作しているスレッドの数。|  
|**active_fts_index_count**|**int**|登録されている場合は、フルテキスト インデックスの数。|  
|**auto_population_count**|**int**|このフルテキスト カタログに対して進行中の自動作成テーブルの数。|  
|**manual_population_count**|**int**|このフルテキスト カタログに対して進行中の手動作成のテーブルの数。|  
|**full_incremental_population_count**|**int**|このフルテキスト カタログに対して実行中、フルまたは増分作成のテーブルの数。|  
|**row_count_in_thousands**|**int**|このフルテキスト カタログのすべてのフルテキスト インデックスで (1,000 単位) 内の行の推定数。|  
|**is_importing**|**bit**|フルテキスト カタログがインポートされているかどうかを示します。<br /><br /> 1 = カタログがインポートされています。<br /><br /> 2 = カタログがインポートされていません。|  
  
## <a name="remarks"></a>コメント  
 Is_importing 列はで新しく追加された[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]します。  
  
## <a name="permissions"></a>アクセス許可  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   
   
## <a name="physical-joins"></a>物理結合  
 ![この動的管理ビューの重要な結合](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-active-catalogs-1.gif "この動的管理ビューの重要な結合")  
  
## <a name="relationship-cardinalities"></a>リレーションシップの基数  
  
|From|変換先|リレーションシップ|  
|----------|--------|------------------|  
|dm_fts_active_catalogs.database_id|dm_fts_index_population.database_id|一対一|  
|dm_fts_active_catalogs.catalog_id|dm_fts_index_population.catalog_id|一対一|  
  
## <a name="examples"></a>使用例  
 次の例では、現在のデータベースに対するアクティブなフルテキスト カタログに関する情報を返します。  
  
```  
SELECT catalog.name, catalog.is_importing, catalog.auto_population_count,  
  OBJECT_NAME(population.table_id) AS table_name,  
  population.population_type_description, population.is_clustered_index_scan,  
  population.status_description, population.completion_type_description,  
  population.queued_population_type_description, population.start_time,  
  population.range_count   
FROM sys.dm_fts_active_catalogs catalog   
CROSS JOIN sys.dm_fts_index_population population   
WHERE catalog.database_id = population.database_id   
AND catalog.catalog_id = population.catalog_id   
AND catalog.database_id = (SELECT dbid FROM sys.sysdatabases WHERE name = DB_NAME());  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 
 [フルテキスト検索とセマンティック検索の動的管理ビューおよび関数&#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  
