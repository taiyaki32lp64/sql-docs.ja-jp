---
title: dm_continuous_copy_status
titleSuffix: Azure SQL Database
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_continuous_copy_status_TSQL
- dm_continuous_copy_status_TSQL
- dm_continuous_copy_status
- sys.dm_continuous_copy_status
dev_langs:
- TSQL
helpviewer_keywords:
- dm_continuous_copy_status
- sys.dm_continuous_copy_status
ms.assetid: 411b2e71-4421-4ef5-900d-5af068750899
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: 6d0bda2d1851d7ec7900a23ad6203d4f85beb73f
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844500"
---
# <a name="sysdm_continuous_copy_status-azure-sql-database"></a>sys.dm_continuous_copy_status (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Geo レプリケーションの連続コピーリレーションシップに現在関与しているユーザーデータベース (V11) ごとに1行のデータを返します。 特定のプライマリデータベースに対して複数の連続コピーリレーションシップが開始された場合、このテーブルにはアクティブなセカンダリデータベースごとに1行のデータが格納されます。  
  
SQL Database V12 を使用している場合は、 [dm_geo_replication_link_status](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)を使用する必要があります ( *Sys は dm_continuous_copy_status* V11 にのみ適用されるため)。

  
|列名|[データ型]|[説明]|  
|-----------------|---------------|-----------------|  
|**copy_guid**|**uniqueidentifier**|レプリカデータベースの一意の ID。|  
|**partner_server**|**sysname**|リンクされた SQL データベース サーバーの名前。|  
|**partner_database**|**sysname**|リンクされた SQL データベース サーバー上にあるリンクされたデータベースの名前。|  
|**last_replication**|**datetimeoffset**|最後に適用されたレプリケートされたトランザクションのタイムスタンプ。|  
|**replication_lag_sec**|**int**|現在の時刻と、アクティブなセカンダリデータベースによって確認されていない、プライマリデータベースで最後に正常にコミットされたトランザクションのタイムスタンプとの間の時間差 (秒単位)。|  
|**replication_state**|**tinyint**|このデータベースの連続コピーレプリケーションの状態。 使用可能な値とその説明を次に示します。<br /><br /> 1: シード処理。 レプリケーションターゲットはシード処理中であり、トランザクション一貫性のない状態になっています。 シードが完了するまで、アクティブなセカンダリ データベースに接続できません。 <br />2: キャッチします。 アクティブなセカンダリデータベースは現在、プライマリデータベースをキャッチアップしており、トランザクション一貫性のある状態になっています。<br />3: 再シードします。 回復できないレプリケーションエラーが発生したため、アクティブなセカンダリデータベースが自動的に再シードされています。<br />4: 中断されました。 これは、アクティブな連続コピーリレーションシップではありません。 通常、この状態は、インターリンクに利用できる帯域幅がプライマリ データベース上のトランザクション アクティビティのレベルに対して不十分であることを示します。 ただし、連続コピーリレーションシップはそのまま残ります。|  
|**replication_state_desc**|**nvarchar (256)**|Replication_state の説明。次のいずれかになります。<br /><br /> SEEDING<br /><br /> CATCH_UP<br /><br /> RE_SEEDING<br /><br /> SUSPENDED|  
|**is_rpo_limit_reached**|**bit**|これは常に0に設定されます。|  
|**is_target_role**|**bit**|0 = コピー リレーションシップのソース<br /><br /> 1 = コピーリレーションシップのターゲット|  
|**is_interlink_connected**|**bit**|1 = インターリンクは接続されています。<br /><br /> 0 = インターリンクは切断されています。|  
  
## <a name="permissions"></a>アクセス許可  
 データを取得するには、 **db_owner**データベースロールのメンバーシップが必要です。 Dbo ユーザー、 **dbmanager**データベースロールのメンバー、および sa ログインでも、このビューに対してクエリを実行できます。  
  
## <a name="remarks"></a>Remarks  
 Dm_continuous_copy_status ビューは**リソース**データベースに作成され、論理マスターを含むすべてのデータベースで表示**でき**ます。 ただし、論理マスターでこのビューにクエリを実行すると、空のセットが返されます。  
  
 連続コピーリレーションシップがデータベースで終了した場合、そのデータベースの行は**dm_continuous_copy_status**ビューに表示されなくなります。  
  
 **Dm_database_copies**ビューと同様に、 **dm_continuous_copy_status**には、データベースがプライマリまたはアクティブセカンダリデータベースである連続コピーリレーションシップの状態が反映されます。 **Dm_database_copies**とは異なり、 **sys. dm_continuous_copy_status**には、操作とパフォーマンスに関する詳細情報を提供するいくつかの列が含まれています。 これらの列には、 **last_replication**、および**replication_lag_sec**が含まれます。  
  
## <a name="see-also"></a>参照  
 [dm_database_copies &#40;Azure SQL Database&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)   
 [アクティブ Geo レプリケーションストアドプロシージャ&#40;transact-sql&#41;](https://msdn.microsoft.com/library/81658ee4-4422-4d73-bf7a-86a07422cb0d)  
  
  
