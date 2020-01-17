---
title: dm_geo_replication_link_status
titleSuffix: Azure SQL Database
ms.date: 01/28/2019
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- dm_geo_replication_link_status
- dm_geo_replication_link_status_TSQL
- sys.dm_geo_replication_link_status
- sys.dm_geo_replication_link_status_TSQL
helpviewer_keywords:
- dm_geo_replication_link_status dynamic management view
- sys.dm_geo_replication_link_status dynamic management view
ms.assetid: d763d679-470a-4c21-86ab-dfe98d37e9fd
author: mashamsft
ms.author: mathoma
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: e642fada95ddf20e81f9fcb7da8b6267469ef0c9
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843885"
---
# <a name="sysdm_geo_replication_link_status-azure-sql-database"></a>sys.dm_geo_replication_link_status (Azure SQL Database)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Geo レプリケーションパートナーシップのプライマリデータベースとセカンダリデータベースの間のレプリケーションリンクごとに1行の値を格納します。 これには、プライマリデータベースとセカンダリデータベースの両方が含まれます。 特定のプライマリデータベースに対して複数の連続レプリケーションリンクが存在する場合、このテーブルにはリレーションシップごとに1行のデータが格納されます。 ビューは、論理マスターを含むすべてのデータベースに作成されます。 ただし、論理マスターでこのビューにクエリを実行すると、空のセットが返されます。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|link_guid|**uniqueidentifier**|レプリケーションリンクの一意の ID。|  
|partner_server|**sysname**|リンクデータベースを含む SQL Database サーバーの名前。|  
|partner_database|**sysname**|リンクされた SQL データベース サーバー上にあるリンクされたデータベースの名前。|  
|last_replication|**datetimeoffset**|プライマリデータベースクロックに基づく、セカンダリによる最後のトランザクションの受信確認のタイムスタンプ。 この値は、プライマリデータベースでのみ使用できます。|  
|replication_lag_sec|**int**|プライマリデータベースのクロックに基づいて、last_replication の値とプライマリのトランザクションのコミットのタイムスタンプの間の時間差 (秒単位)。  この値は、プライマリデータベースでのみ使用できます。|  
|replication_state|**tinyint**|このデータベースの geo レプリケーションの状態。次のいずれかになります。<br /><br /> 1 = シード処理。 Geo レプリケーションターゲットはシードされていますが、2つのデータベースがまだ同期されていません。 シード処理が完了するまで、セカンダリデータベースに接続することはできません。 プライマリからセカンダリデータベースを削除すると、シード処理操作が取り消されます。<br /><br /> 2 = キャッチアップ。 セカンダリデータベースはトランザクション一貫性のある状態であり、常にプライマリデータベースと同期されています。<br /><br /> 4 = 中断されています。 これは、アクティブな連続コピーリレーションシップではありません。 通常、この状態は、インターリンクに利用できる帯域幅がプライマリ データベース上のトランザクション アクティビティのレベルに対して不十分であることを示します。 ただし、連続コピーリレーションシップはそのまま残ります。|  
|replication_state_desc|**nvarchar (256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|ロール (role)|**tinyint**|Geo レプリケーションロール。次のいずれかになります。<br /><br /> 0 = プライマリ。 Database_id は、geo レプリケーションパートナーシップのプライマリデータベースを参照します。<br /><br /> 1 = セカンダリ。  Database_id は、geo レプリケーションパートナーシップのプライマリデータベースを参照します。|  
|role_desc|**nvarchar (256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|セカンダリ型。次のいずれかになります。<br /><br /> 0 = セカンダリデータベースへの直接接続は許可されず、データベースを読み取りアクセスに使用することはできません。<br /><br /> 2 = セカンダリ repl 内のデータベースへのすべての接続が許可されます。読み取り専用アクセスの場合は。|  
|secondary_allow_connections_desc|**nvarchar (256)**|[いいえ]<br /><br /> [すべて]|  
|last_commit|**datetimeoffset**|最後のトランザクションがデータベースにコミットされた時刻。 プライマリデータベースで取得された場合は、プライマリデータベースの最後のコミット時刻を示します。 セカンダリデータベースで取得された場合は、セカンダリデータベースの最後のコミット時刻を示します。 レプリケーションリンクのプライマリがダウンしたときにセカンダリデータベースで取得された場合は、セカンダリがどの時点でキャッチされたかを示します。|
  
> [!NOTE]  
>  セカンダリデータベース (セクション 4.2) を削除してレプリケーション関係を終了すると、そのデータベースの行が**dm_geo_replication_link_status**ビューに表示されなくなります。  
  
## <a name="permissions"></a>アクセス許可  
 View_database_state のアクセス許可を持つすべてのアカウントは、 **dm_geo_replication_link_status**に対してクエリを実行できます。  
  
## <a name="example"></a>例  
 セカンダリデータベースのレプリケーションラグと最後のレプリケーション時刻を表示します。  
  
```  
SELECT   
     link_guid  
   , partner_server  
   , last_replication  
   , replication_lag_sec   
FROM sys.dm_geo_replication_link_status;  
```  
  
## <a name="see-also"></a>参照  
 [ALTER database &#40;Azure SQL Database&#41; ](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [geo_replication_links &#40;Azure SQL Database&#41; ](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [dm_operation_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
  
  
