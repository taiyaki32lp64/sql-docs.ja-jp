---
title: sys.dm_database_copies (Azure SQL データベース) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- dm_database_copies_TSQL
- sys.dm_database_copies
- dm_database_copies
- sys.dm_database_copies_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_database_copies
- sys.dm_database_copies
ms.assetid: d03d4657-86d1-4496-97e6-cc3bc292e0b1
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 0654bd9d15591d994b05ab2c01d9912bc0c56117
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005082"
---
# <a name="sysdmdatabasecopies-azure-sql-database"></a>sys.dm_database_copies (Azure SQL データベース)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  データベースのコピーに関する情報を返します。  
  
使用して、geo レプリケーション リンクに関する情報を返す、 [sys.geo_replication_links](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)または[sys.dm_geo_replication_link_status](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)ビュー (SQL Database V12 で使用可能)。
  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|`sys.databases` ビューの現在のデータベースの ID。|  
|**start_date**|**datetimeoffset**|地域の [!INCLUDE[ssSDS](../../includes/sssds-md.md)] データセンターにおいてデータベース コピーが開始された時刻 (UTC)。|  
|**modify_date**|**datetimeoffset**|地域の [!INCLUDE[ssSDS](../../includes/sssds-md.md)] データセンターにおいてデータベース コピーが完了した時刻 (UTC)。 新しいデータベースは、この時点でプライマリ データベースの一貫性です。 完了情報は、1 分ごとに更新されます。<br /><br />Percent_complete フィールドの最後の更新を反映した UTC 時刻。|  
|**percent_complete**|**real**|コピーされたバイトの割合 (%)。 値の範囲は 0 から 100 です。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] は、フェールオーバーなどのエラーから自動的に復旧した後に、データベース コピーを再開することがあります。 この場合、percent_complete は 0 から再開します。|  
|**error_code**|**int**|値が 0 より大きい場合は、コピー中に発生したエラーを示すコード。 エラーが発生していない場合は、0 と等しいを値します。|  
|**error_desc**|**nvarchar(4096)**|コピー中に発生したエラーの説明です。|  
|**error_severity**|**int**|データベース コピーが失敗した場合は 16 を返します。|  
|**error_state**|**int**|コピーが失敗した場合は 1 を返します。|  
|**copy_guid**|**uniqueidentifier**|コピー操作の一意の ID。|  
|**partner_server**|**sysname**|コピーが作成されている SQL Database サーバーの名前。|  
|**partner_database**|**sysname**|パートナー サーバー上のデータベース コピーの名前です。|  
|**replication_state**|**tinyint**|このデータベースの連続コピー レプリケーションの状態。 値は次のとおりです。<br /><br /> 0 = 保留中です。 データベースのコピーの作成がスケジュールされているが、必要な準備手順がまだ完了していないまたはシード クォータによって一時的にブロックされます。<br /><br /> 1 = シード処理します。 データベースのコピーがシード中同期されていない場合完全ソース データベースとします。 この状態では、コピーに接続することはできません。 実行中のシード処理操作をキャンセルするには、データベースのコピーを削除する必要があります。|  
|**replication_state_desc**|**nvarchar (256)**|Replication_state のいずれかの説明です。<br /><br /> PENDING<br /><br /> SEEDING<br />|  
|**maximum_lag**|**int**|予約済みのフィールド。|  
|**is_continuous_copy**|**bit**|0 = 0 を返します。|  
|**is_target_role**|**bit**|0 = ソース データベース<br /><br /> 1 = データベースのコピー|  
|**is_interlink_connected**|bit|予約済みのフィールド。|  
|**is_offline_secondary**|bit|予約済みのフィールド。|  
  
## <a name="permissions"></a>アクセス許可  
 このビューはのみ利用可能、**マスター**データベース、サーバー レベル プリンシパル ログインをします。  
  
## <a name="remarks"></a>コメント  
 使用することができます、 **sys.dm_database_copies**で表示、**マスター**ソースまたはターゲットのデータベース[!INCLUDE[ssSDS](../../includes/sssds-md.md)]サーバー。 データベースのコピーが正常に完了して、新しいデータベースが内の行では、オンライン、 **sys.dm_database_copies**ビューが自動的に削除されます。  
  
  
