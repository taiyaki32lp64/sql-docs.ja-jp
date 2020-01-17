---
title: sys.dm_db_log_info (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_db_log_info
- sys.dm_db_log_info_TSQL
- dm_db_log_info
- dm_db_log_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_info dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
author: savjani
ms.author: pariks
manager: ajayj
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7cb87d2d5677085edc8e6bd998f20c3c45013823
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262078"
---
# <a name="sysdm_db_log_info-transact-sql"></a>sys.dm_db_log_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

返します[仮想ログ ファイル (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)のトランザクション ログの情報。 すべてのトランザクション ログ ファイルは、テーブルの出力にまとめられていますに注意してください。 出力の各行は、トランザクション ログ内の VLF を表し、その VLF をログに関連する情報を提供します。

## <a name="syntax"></a>構文  
  
```  
sys.dm_db_log_info ( database_id )  
``` 

## <a name="arguments"></a>引数  
 *database_id* | NULL | DEFAULT  
 データベースの ID です。 *database_id* は **int** です。有効な値は、データベース、null の場合、または既定の ID 番号です。 既定値は NULL です。 NULL および DEFAULT は現在のデータベースのコンテキストで同じ値になります。
 
 現在のデータベースの VLF 情報を返す NULL を指定します。

 組み込み関数[DB_ID](../../t-sql/functions/db-id-transact-sql.md)を指定できます。 使用する場合`DB_ID`データベース名を指定せず、現在のデータベースの互換性レベルを 90 以上にする必要があります。  

## <a name="table-returned"></a>返されるテーブル  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|database_id|**int**|データベース ID。|
|file_id|**smallint**|トランザクション ログのファイル id。|  
|vlf_begin_offset|**bigint** |オフセットの位置を[仮想ログ ファイル (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)トランザクション ログ ファイルの先頭から。|
|vlf_size_mb |**float** |[仮想ログ ファイル (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)サイズ (mb)、小数点以下 2 桁に丸められます。|     
|vlf_sequence_number|**bigint** |[仮想ログ ファイル (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)シーケンス番号が作成された順序で。 ログ ファイルの Vlf を一意に識別するために使用します。|
|vlf_active|**bit** |示すかどうか[仮想ログ ファイル (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)使用されていますか。 <br />0 - VLF 使用されていません。<br />1-VLF がアクティブです。|
|vlf_status|**int** |状態、[仮想ログ ファイル (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)します。 使用可能な値が含まれます <br />0 - VLF がアクティブではありません。 <br />1-VLF が初期化されますが、使用されていません。 <br /> 2-VLF がアクティブです。|
|vlf_parity|**tinyint** |同等の[仮想ログ ファイル (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)します。内部的には、使用すると、VLF 内のログの末尾を決定します。|
|vlf_first_lsn|**nvarchar(48)** |[ログ シーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)で最初のログ レコードの[仮想ログ ファイル (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)します。|
|vlf_create_lsn|**nvarchar(48)** |[ログ シーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)ログの記録を作成した、[仮想ログ ファイル (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)します。|
|vlf_encryptor_thumbprint|**varbinary(20)**| **適用対象:** [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] <br><br> 使用して、VLF を暗号化するかどうか、VLF の暗号化機能の拇印を表示[Transparent Data Encryption](../../relational-databases/security/encryption/transparent-data-encryption.md),、それ以外の場合は NULL です。 |

## <a name="remarks"></a>コメント
`sys.dm_db_log_info`動的管理関数は、`DBCC LOGINFO`ステートメント。    
 
## <a name="permissions"></a>アクセス許可  
必要があります、`VIEW DATABASE STATE`データベースの権限。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>A. Vlf の数が多いと、SQL Server インスタンス内のデータベースの判別
次のクエリは、ログ ファイルは、データベースの起動、復元、および回復の時間に影響が 100 を超える Vlf を使用してデータベースを決定します。

```sql
SELECT [name], COUNT(l.database_id) AS 'vlf_count' 
FROM sys.databases s
CROSS APPLY sys.dm_db_log_info(s.database_id) l
GROUP BY [name]
HAVING COUNT(l.database_id) > 100
```

### <a name="b-determing-the-position-of-the-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. 最後の位置を判別`VLF`ログ ファイルを圧縮する前にトランザクション ログ

トランザクション ログが圧縮できるかを判断するトランザクション ログの shrinkfile を実行する前に最新のアクティブな VLF の位置を決定するのには、次のクエリを使用できます。

```sql
USE AdventureWorks2016
GO

;WITH cte_vlf AS (
SELECT ROW_NUMBER() OVER(ORDER BY vlf_begin_offset) AS vlfid, DB_NAME(database_id) AS [Database Name], vlf_sequence_number, vlf_active, vlf_begin_offset, vlf_size_mb
    FROM sys.dm_db_log_info(DEFAULT)),
cte_vlf_cnt AS (SELECT [Database Name], COUNT(vlf_sequence_number) AS vlf_count,
    (SELECT COUNT(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 0) AS vlf_count_inactive,
    (SELECT COUNT(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS vlf_count_active,
    (SELECT MIN(vlfid) FROM cte_vlf WHERE vlf_active = 1) AS ordinal_min_vlf_active,
    (SELECT MIN(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS min_vlf_active,
    (SELECT MAX(vlfid) FROM cte_vlf WHERE vlf_active = 1) AS ordinal_max_vlf_active,
    (SELECT MAX(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS max_vlf_active
    FROM cte_vlf
    GROUP BY [Database Name])
SELECT [Database Name], vlf_count, min_vlf_active, ordinal_min_vlf_active, max_vlf_active, ordinal_max_vlf_active,
((ordinal_min_vlf_active-1)*100.00/vlf_count) AS free_log_pct_before_active_log,
((ordinal_max_vlf_active-(ordinal_min_vlf_active-1))*100.00/vlf_count) AS active_log_pct,
((vlf_count-ordinal_max_vlf_active)*100.00/vlf_count) AS free_log_pct_after_active_log
FROM cte_vlf_cnt
GO
```

## <a name="see-also"></a>関連項目  
[動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[データベース関連の動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)

