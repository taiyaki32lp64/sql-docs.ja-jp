---
title: backupfile (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupfile
- backupfile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- file backups [SQL Server], backupfile system table
- backupfile system table
ms.assetid: f1a7fc0a-f4b4-47eb-9138-eebf930dc9ac
author: stevestein
ms.author: sstein
ms.openlocfilehash: c12575ae2eb07b5984d1e4a383830ff6fb44573a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091863"
---
# <a name="backupfile-transact-sql"></a>backupfile (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベースの各データまたは各ログ ファイルに対して 1 行のデータを格納します。 各列では、バックアップ作成時のファイル構成の詳細が示されます。 ファイルがバックアップに含まれているかどうかによって決まりますが、 **is_present**列。 このテーブルに格納されます、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|バックアップ セットを格納するファイルの一意な識別番号。 参照**backupset (backup_set_id)** します。|  
|**first_family_number**|**tinyint**|最初にこのバックアップ ファイルを格納しているメディアのファミリ番号。 NULL にすることができます。|  
|**first_media_number**|**smallint**|バックアップ ファイルが保存されている先頭のメディアのメディア番号。 NULL にすることができます。|  
|**filegroup_name**|**nvarchar(128)**|バックアップされたデータベース ファイルを含むファイル グループの名前です。 NULL にすることができます。|  
|**page_size**|**int**|(バイト単位)、ページのサイズ。|  
|**file_number**|**numeric(10,0)**|データベース内で一意の識別番号をファイル (対応する**sys.database_files**.**file_id**)。|  
|**backed_up_page_count**|**numeric(10,0)**|バックアップされたページ数。 NULL にすることができます。|  
|**file_type**|**char(1)**|バックアップされたファイル。次のいずれかです。<br /><br /> D = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ ファイル<br /><br /> L =[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログ ファイル。<br /><br /> F = フルテキスト カタログ<br /><br /> NULL にすることができます。|  
|**source_file_block_size**|**numeric(10,0)**|バックアップされたときに、元のデータまたはログ ファイルが存在するデバイスです。 NULL にすることができます。|  
|**file_size**|**numeric(20,0)**|バックアップされたファイルの長さ (バイト単位)。 NULL にすることができます。|  
|**logical_name**|**nvarchar(128)**|バックアップされたファイルの論理名。 NULL にすることができます。|  
|**physical_drive**|**nvarchar(260)**|物理ドライブまたはパーティションの名前。 NULL にすることができます。|  
|**physical_name**|**nvarchar(260)**|残りの物理 (オペレーティング システム) ファイルの名前。 NULL にすることができます。|  
|**state**|**tinyint**|ファイルのいずれかの状態:<br /><br /> 0 = ONLINE<br /><br /> 1 = を復元します。<br /><br /> 2 = 回復<br /><br /> 3 = RECOVERY PENDING<br /><br /> 4 = 問題あり<br /><br /> 6 = OFFLINE<br /><br /> 7 = DEFUNCT<br /><br /> 8 = 削除<br /><br /> 注:これらの値がデータベースの状態の値に対応するように、値 5 はスキップされます。|  
|**state_desc**|**nvarchar(64)**|ファイルの状態のいずれかの説明です。<br /><br /> ONLINE RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT OFFLINE DEFUNCT|  
|**create_lsn**|**numeric(25,0)**|ファイルが作成されたときのログ シーケンス番号。|  
|**drop_lsn**|**numeric(25,0)**|ファイルが削除されたときのログ シーケンス番号。 NULL にすることができます。<br /><br /> ファイルが削除されていない場合、この値は NULL です。|  
|**file_guid**|**uniqueidentifier**|ファイルの一意の識別子。|  
|**read_only_lsn**|**numeric(25,0)**|このファイルを含むファイル グループが、前回読み書き可能から読み取り専用に変更されたときのログ シーケンス番号。 NULL にすることができます。|  
|**read_write_lsn**|**numeric(25,0)**|このファイルを含むファイル グループが、前回読み取り専用から読み書き可能に変更されたときのログ シーケンス番号。 NULL にすることができます。|  
|**differential_base_lsn**|**numeric(25,0)**|差分バックアップのベース ログ シーケンス番号。 差分バックアップには、データ エクステントをログ シーケンス番号以上になるだけが含まれます。 **differential_base_lsn**します。<br /><br /> その他の種類のバックアップの場合、この値は NULL です。|  
|**differential_base_guid**|**uniqueidentifier**|差分バックアップの場合、ファイルの差分ベースとなる最新のデータ バックアップの一意識別子。この値が NULL の場合、ファイルは差分バックアップに含まれますが、ベースの作成後に追加されています。<br /><br /> その他の種類のバックアップの場合、この値は NULL です。|  
|**backup_size**|**numeric(20,0)**|このファイルのバックアップ サイズ (バイト単位)。|  
|**filegroup_guid**|**uniqueidentifier**|ファイル グループの ID。 Backupfilegroup テーブルでのファイル グループ情報を見つけるには使用**filegroup_guid**で**backup_set_id**します。|  
|**is_readonly**|**bit**|1 = ファイルは読み取り専用です。|  
|**is_present**|**bit**|1 = ファイルはバックアップ セットに含まれる。|  
  
## <a name="remarks"></a>コメント  
 RESTORE VERIFYONLY FROM *backup_device* WITH LOADHISTORY の列に設定、 **backupmediaset**メディア セット ヘッダーから適切な値を持つテーブル。  
  
 このテーブルおよびその他のバックアップと履歴テーブルの行の数を減らすためには、実行、 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)ストアド プロシージャ。  
  
## <a name="see-also"></a>参照  
 [バックアップし、復元テーブル&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [システム テーブル &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
