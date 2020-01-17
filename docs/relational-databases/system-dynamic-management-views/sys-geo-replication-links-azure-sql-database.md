---
title: sys.geo_replication_links (Azure SQL データベース) |Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- dm_geo_replication_links_TSQL
- dm_geo_replication_links
- sys.dm_geo_replication_links
- sys.dm_geo_replication_links_TSQL
helpviewer_keywords:
- sys.dm_geo_replication_links dynamic management view
- dm_geo_replication_links dynamic management view
ms.assetid: 58911798-1d60-4f28-87ab-2def2bfc3de7
author: mashamsft
ms.author: mathoma
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 6e768f447cd53321861eae91bbe40e2e34ad12f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68043163"
---
# <a name="sysgeoreplicationlinks-azure-sql-database"></a>sys.geo_replication_links (Azure SQL Database)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Geo レプリケーション パートナーシップのプライマリとセカンダリ データベース間のレプリケーション リンクごとに 1 行が含まれています。 このビューは、論理マスター データベースに存在します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|database_id|**int**|Sys.databases ビューの現在のデータベースの ID。|  
|start_date|**datetimeoffset**|データベースのレプリケーションが開始されたときに地域別の SQL データベース datacenter の UTC 時刻|  
|modify_date|**datetimeoffset**|SQL Database にデータ センター データベースの geo レプリケーションが完了したときに地域における UTC 時刻。 新しいデータベースはこの時点で、プライマリ データベースと同期します。 .|  
|link_guid|**uniqueidentifier**|Geo レプリケーション リンクの一意の ID。|  
|partner_server|**sysname**|Geo レプリケートされたデータベースを含む SQL データベース サーバーの名前です。|  
|partner_database|**sysname**|リンクされた SQL データベース サーバーを geo レプリケートされたデータベースの名前。|  
|replication_state|**tinyint**|このデータベースは、いずれかの geo レプリケーションの状態: です。<br /><br /> 0 = 保留中です。 アクティブなセカンダリ データベースの作成がスケジュールされているが、必要な準備手順がまだ完了していません。<br /><br /> 1 = シード処理します。 Geo レプリケーションの対象がシード中は、2 つのデータベースがまだ同期されていません。 シードが完了するまでセカンダリ データベースに接続することはできません。 プライマリからセカンダリ データベースを削除すると、シード処理操作が取り消されます。<br /><br /> 2 = キャッチアップします。 セカンダリ データベースでは、状態の一貫性があり、常に、プライマリ データベースと同期中します。|  
|replication_state_desc|**nvarchar (256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|ロール (role)|**tinyint**|1 つの Geo レプリケーション ロール:<br /><br /> 0 = プライマリです。 Database_id は、geo レプリケーション パートナーシップのプライマリ データベースを指します。<br /><br /> 1 = セカンダリ。  Database_id は、geo レプリケーション パートナーシップのプライマリ データベースを指します。|  
|role_desc|**nvarchar (256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|1 つのセカンダリ型。<br /><br /> 0 = いいえ。 フェールオーバーまでに、セカンダリ データベースにアクセスできません。<br /><br /> 1 = 読み取り専用です。 セカンダリ データベースは ApplicationIntent でクライアント接続のみがアクセスできる = 読み取り専用です。<br /><br /> 2 = すべて。 セカンダリ データベースにはクライアントの接続にアクセスします。|  
|secondary_allow_connections _desc|**nvarchar (256)**|いいえ<br /><br /> All<br /><br /> 読み取り専用|  
  
## <a name="permissions"></a>アクセス許可

このビューはのみ利用可能、**マスター**データベース、サーバー レベル プリンシパル ログインをします。  
  
## <a name="example"></a>例

Geo レプリケーション リンクと共にすべてのデータベースを表示します。  

```sql
SELECT
     database_id  
   , start_date  
   , partner_server  
   , partner_database  
   , replication_state  
   , role_desc  
   , secondary_allow_connections_desc
FROM sys.geo_replication_links;  
```

## <a name="see-also"></a>関連項目

 [ALTER DATABASE (Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [sys.dm_geo_replication_link_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [sys.dm_operation_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
