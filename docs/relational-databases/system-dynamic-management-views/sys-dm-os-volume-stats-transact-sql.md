---
title: sys.dm_os_volume_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/06/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_volume_stats_TSQL
- dm_os_volume_stats
- sys.dm_os_volume_stats
- sys.dm_os_volume_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_volume_stats dynamic management function
ms.assetid: fa1c58ad-8487-42ad-956c-983f2229025f
author: stevestein
ms.author: sstein
ms.openlocfilehash: e7ec8171b569adbf887c1e153fb2b41619778f48
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899719"
---
# <a name="sysdmosvolumestats-transact-sql"></a>sys.dm_os_volume_stats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-2008R2SP1-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-2008R2sp1-xxxx-xxxx-xxx-md.md)]

  これで指定されたデータベースとファイルを格納します。 オペレーティング システム ボリューム (ディレクトリ) に関する情報を返します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 この動的管理関数は、物理ディスク ドライブの属性を確認する場合や、ディレクトリの使用可能な空き容量に関する情報を取得する場合に使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sys.dm_os_volume_stats (database_id, file_id)  
```  
  
##  <a name="Arguments"></a> 引数  
 *database_id*  
 データベースの ID です。 *database_id* は **int**, 、既定値はありません。 NULL 値は許容されません。  
  
 *file_id*  
 ファイルの ID です。 *file_id*は**int**、既定値はありません。 NULL 値は許容されません。  
  
## <a name="table-returned"></a>返されるテーブル  
  
||||  
|-|-|-|  
|**列**|**データ型**|**[説明]**|  
|**database_id**|**int**|データベースの ID です。 null にすることはできません。|  
|**file_id**|**int**|ファイルの ID です。 null にすることはできません。|  
|**volume_mount_point**|**nvarchar(512)**|ボリュームがルートとするマウント ポイント。 空の文字列を返すことができます。|  
|**volume_id**|**nvarchar(512)**|オペレーティング システム ボリュームの id。 空の文字列を返すことができます。|  
|**logical_volume_name**|**nvarchar(512)**|論理ボリュームの名前。 空の文字列を返すことができます。|  
|**file_system_type**|**nvarchar(512)**|ファイル システム ボリューム (NTFS、FAT、RAW など) の型。 空の文字列を返すことができます。|  
|**total_bytes**|**bigint**|ボリュームのバイトの合計サイズ。 null にすることはできません。|  
|**available_bytes**|**bigint**|ボリューム上の使用可能な空き領域。 null にすることはできません。|  
|**supports_compression**|**bit**|ボリュームがオペレーティング システムによる圧縮をサポートするかどうかを示します。 null にすることはできません。|  
|**supports_alternate_streams**|**bit**|ボリュームが代替ストリームをサポートするかどうかを示します。 null にすることはできません。|  
|**supports_sparse_files**|**bit**|ボリュームがスパース ファイルをサポートしているかどうかを示します。  null にすることはできません。|  
|**is_read_only**|**bit**|ボリュームが現在読み取り専用としてマークされているかどうかを示します。 null にすることはできません。|  
|**is_compressed**|**bit**|このボリュームが現在圧縮されているかどうかを示します。 null にすることはできません。|  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 `VIEW SERVER STATE` 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-return-total-space-and-available-space-for-all-database-files"></a>A. 合計領域とすべてのデータベース ファイルの空き領域を返す  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにあるすべてのデータベース ファイルの合計領域と使用可能な領域 (バイト単位) を返します。  
  
```sql  
SELECT f.database_id, f.file_id, volume_mount_point, total_bytes, available_bytes  
FROM sys.master_files AS f  
CROSS APPLY sys.dm_os_volume_stats(f.database_id, f.file_id);  
```  
  
### <a name="b-return-total-space-and-available-space-for-the-current-database"></a>B. 現在のデータベースの合計領域と使用可能な領域を返す  
 次の例では、現在のデータベースに合計領域とデータベース ファイルのバイト単位で使用可能な領域を返します。  
  
```sql  
SELECT database_id, f.file_id, volume_mount_point, total_bytes, available_bytes  
FROM sys.database_files AS f  
CROSS APPLY sys.dm_os_volume_stats(DB_ID(f.name), f.file_id);  
```  
  
## <a name="see-also"></a>関連項目  
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
  
  
