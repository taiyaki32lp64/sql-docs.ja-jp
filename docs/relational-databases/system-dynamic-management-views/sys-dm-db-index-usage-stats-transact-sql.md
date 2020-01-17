---
title: sys.dm_db_index_usage_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_index_usage_stats_TSQL
- sys.dm_db_index_usage_stats
- sys.dm_db_index_usage_stats_TSQL
- dm_db_index_usage_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_index_usage_stats dynamic management view
ms.assetid: d06a001f-0f72-4679-bc2f-66fff7958b86
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 491ec37d96cf6bdb2b074efb42a54406beb1fd20
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264402"
---
# <a name="sysdm_db_index_usage_stats-transact-sql"></a>sys.dm_db_index_usage_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  さまざまな種類のインデックス操作の数と、各種の操作が前回実行された時刻を返します。  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]では、動的管理ビューでデータベースの包含に影響を与える情報を公開することや、ユーザーがアクセスできる他のデータベースに関する情報を公開することはできません。 この情報を公開することを避けるため、接続されているテナントに属していないデータが含まれるすべての行はフィルターで除外します。  
  
> [!NOTE]  
>  **sys.dm_db_index_usage_stats**メモリ最適化インデックスに関する情報は返されません。 メモリ最適化インデックスの使用方法については、[sys.dm_db_xtp_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md) を参照してください。  
  
> [!NOTE]  
>  このビューからの呼び出しに[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]を使用して、 **sys.dm_pdw_nodes_db_index_usage_stats**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**smallint**|テーブルまたはビューが定義されているデータベースの ID。|  
|**object_id**|**int**|インデックスが定義されているテーブルまたはビューの ID。|  
|**index_id**|**int**|インデックスの ID。|  
|**user_seeks**|**bigint**|ユーザー クエリによるシーク数。|  
|**user_scans**|**bigint**|使用していないユーザー クエリによるスキャン数 'シーク' 述語。|  
|**user_lookups**|**bigint**|ユーザー クエリによるブックマーク参照数。|  
|**user_updates**|**bigint**|ユーザー クエリによる更新数。 これは、Insert、Delete が含まれていて、実際に影響を受ける行にない実行された操作の数を表すを更新します。 たとえば、1 つのステートメントで 1000 行を削除する場合は、このカウントを 1 増や|  
|**last_user_seek**|**datetime**|前回のユーザー シークの時刻。|  
|**last_user_scan**|**datetime**|前回のユーザー スキャンの時刻。|  
|**last_user_lookup**|**datetime**|前回のユーザー参照の時刻。|  
|**last_user_update**|**datetime**|前回のユーザー更新の時刻。|  
|**system_seeks**|**bigint**|システム クエリによるシーク数。|  
|**system_scans**|**bigint**|システム クエリによるスキャン数。|  
|**system_lookups**|**bigint**|システム クエリによる参照数。|  
|**system_updates**|**bigint**|システム クエリによる更新数。|  
|**last_system_seek**|**datetime**|前回のシステム シークの時刻。|  
|**last_system_scan**|**datetime**|前回のシステム スキャンの時刻。|  
|**last_system_lookup**|**datetime**|前回のシステム参照の時刻。|  
|**last_system_update**|**datetime**|前回のシステム更新の時刻。|  
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="remarks"></a>コメント  
 指定したインデックスに対し、1 回のクエリ実行でシーク、スキャン、参照、または更新が行われるたび、その操作はインデックスの使用としてカウントされ、このビュー内の対応するカウンターが 1 増えます。 情報は、ユーザーが送信したクエリによる操作と、統計収集のスキャンなど内部生成されたクエリによる操作の両方についてレポートされます。  
  
 **User_updates**カウンターは、挿入によって、インデックスのメンテナンスのレベルを示します、更新、または基になるテーブルまたはビューに対する操作を削除します。 このビューを使用して、アプリケーションであまり使用されないインデックスを特定できます。 また、メンテナンスのオーバーヘッドの原因になっているインデックスも特定できます。 メンテナンスのオーバーヘッドの原因になっており、クエリでほとんどまたはまったく使用されないインデックスが特定できれば、インデックスの削除を検討することもできます。  
  
 各カウンターは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) サービスが開始されるたびに初期化され、空になります。 また、AUTO_CLOSE が ON に設定されているなどの理由によりデータベースがデタッチまたはシャットダウンされた場合は常に、そのデータベースに関連付けられた行がすべて削除されます。  
  
 インデックスを使用すると、行に追加されます**sys.dm_db_index_usage_stats**行が既にインデックスに存在しない場合。 行が追加されるときに、カウンターが 0 に初期設定されます。  
  
 アップグレード中に[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、または[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]sys.dm_db_index_usage_stats でエントリが削除されます。 以降で[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]より前のバージョンと同様に、エントリが保持される[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]します。  
  
## <a name="permissions"></a>アクセス許可  
[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。  
  
## <a name="see-also"></a>関連項目  

 [インデックス関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  


