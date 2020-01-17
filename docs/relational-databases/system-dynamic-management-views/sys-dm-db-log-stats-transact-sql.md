---
title: sys.dm_db_log_stats (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 05/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_log_stats_TSQL
- sys.dm_db_log_stats
- sys.dm_db_log_stats_TSQL
- dm_db_log_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_stats dynamic management function
ms.assetid: ''
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b23eea391c7de1f02eacec7f8c8625211dfeea3d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004838"
---
# <a name="sysdm_db_log_stats-transact-sql"></a>sys.dm_db_log_stats (Transact-SQL)   
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

データベースのトランザクション ログ ファイルに関する概要レベルの属性と情報を返します。 この情報を使用してトランザクション ログの正常性の監視と診断。   
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
 sys.dm_db_log_stats ( database_id )
```  
  
## <a name="arguments"></a>引数  

*database_id* | NULL | **DEFAULT**

データベースの ID です。 `database_id` は `int` です。 有効な値は、データベースの ID 番号`NULL`、または`DEFAULT`します。 既定値は `NULL` です。 `NULL` `DEFAULT`は現在のデータベースのコンテキストで同じ値になります。  
組み込み関数[DB_ID](../../t-sql/functions/db-id-transact-sql.md)を指定できます。 使用する場合`DB_ID`データベース名を指定せず、現在のデータベースの互換性レベルを 90 以上にする必要があります。

  
## <a name="tables-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|database_id    |**int**    |データベース ID |  
|recovery_model |**nvarchar(60)**   |   データベースの復旧モデルです。 有効な値は次のとおりです。 <br /> SIMPLE<br /> BULK_LOGGED <br /> FULL |  
|log_min_lsn    |**nvarchar(24)**   |   現在の開始[ログ シーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)トランザクション ログにします。|  
|log_end_lsn    |**nvarchar(24)**   |   [ログ シーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)のトランザクション ログの最後のログ レコード。|  
|current_vlf_sequence_number    |**bigint** |   現在[仮想ログ ファイル (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)の実行時にシーケンス番号。|  
|current_vlf_size_mb    |**float**  |   現在[仮想ログ ファイル (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)サイズ (MB 単位)。|   
|total_vlf_count    |**bigint** |   合計数[仮想ログ ファイル (Vlf)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)トランザクション ログにします。 |  
|total_log_size_mb  |**float**  |   トランザクションの合計ログのサイズ (mb)。 |  
|active_vlf_count   |**bigint** |   アクティブな数の合計[仮想ログ ファイル (Vlf)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)トランザクション ログにします。|  
|active_log_size_mb |**float**  |   合計アクティブなトランザクション ログのサイズ (mb)。|  
|log_truncation_holdup_reason   |**nvarchar(60)**   |   ログ切り捨てホールド アップの理由です。 値が同じ`log_reuse_wait_desc`の列`sys.databases`します。  (詳細なこれらの値の説明についてを参照してください。[トランザクション ログ](../../relational-databases/logs/the-transaction-log-sql-server.md))。 <br />有効な値は次のとおりです。 <br />NOTHING<br />CHECKPOINT<br />LOG_BACKUP<br />ACTIVE_BACKUP_OR_RESTORE<br />ACTIVE_TRANSACTION<br />DATABASE_MIRRORING<br />REPLICATION<br />DATABASE_SNAPSHOT_CREATION<br />LOG_SCAN<br />AVAILABILITY_REPLICA<br />OLDEST_PAGE<br />XTP_CHECKPOINT<br />その他の一時的なもの |  
|log_backup_time    |**datetime**   |   前回トランザクション ログのバックアップ時刻。|   
|log_backup_lsn |**nvarchar(24)**   |   最後のトランザクション ログ バックアップ[ログ シーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)します。|   
|log_since_last_log_backup_mb   |**float**  |   ログのサイズを mb 単位で最後のトランザクション ログ バックアップ以降[ログ シーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)します。|  
|log_checkpoint_lsn |**nvarchar(24)**   |   最後のチェックポイント[ログ シーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)します。|  
|log_since_last_checkpoint_mb   |**float**  |   ログのサイズを mb 単位で最後のチェックポイント以降[ログ シーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)します。|  
|log_recovery_lsn   |**nvarchar(24)**   |   復旧[ログ シーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)データベース。 場合`log_recovery_lsn`チェックポイントの LSN を前に発生します`log_recovery_lsn`、最も古いアクティブなトランザクション LSN、それ以外の場合は、`log_recovery_lsn`はチェックポイントの LSN です。|  
|log_recovery_size_mb   |**float**  |   ログのサイズを mb 単位でログを復旧してから[ログ シーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)します。|  
|recovery_vlf_count |**bigint** |   合計数[仮想ログ ファイル (Vlf)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)フェールオーバーやサーバーの再起動があった場合に回復します。 |  


## <a name="remarks"></a>コメント
実行時に`sys.dm_db_log_stats`セカンダリ レプリカとして可用性グループに参加しているデータベースに対して上記で説明したフィールドのサブセットのみが返されます。  現時点では、のみ`database_id`、 `recovery_model`、および`log_backup_time`がセカンダリ データベースに対して実行したときに返されます。   

## <a name="permissions"></a>アクセス許可  
必要があります、`VIEW DATABASE STATE`データベースの権限。   
  
## <a name="examples"></a>使用例  

### <a name="a-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-high-number-of-vlfs"></a>A. 内のデータベースを決定する、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Vlf の数が多いとインスタンス   
次のクエリでは、ログ ファイルで 100 個の Vlf を使用してデータベースを返します。 多数の Vlf データベースの起動、復元、および回復の時間に影響を与えることができます。

```sql  
SELECT name AS 'Database Name', total_vlf_count AS 'VLF count' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id) 
WHERE total_vlf_count  > 100;
```   

### <a name="b-determining-databases-in-a-includessnoversionincludesssnoversion-mdmd-instance-with-transaction-log-backups-older-than-4-hours"></a>B. 内のデータベースを決定する、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 4 時間よりも古いトランザクション ログのバックアップを持つインスタンス   
次のクエリは、インスタンス内のデータベースの前回のログ バックアップ時刻を決定します。

```sql  
SELECT name AS 'Database Name', log_backup_time AS 'last log backup time' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id); 
```

## <a name="see-also"></a>関連項目  
[動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[データベース関連の動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
  
