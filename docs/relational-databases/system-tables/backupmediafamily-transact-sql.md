---
title: backupmediafamily (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupmediafamily
- backupmediafamily_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backupmediafamily system table
- backup media [SQL Server], backupmediafamily system table
ms.assetid: ee16de24-3d95-4b2e-a094-78df2514d18a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6ea3fd7937447ba3ed0f3ad89965301dead772cf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122878"
---
# <a name="backupmediafamily-transact-sql"></a>backupmediafamily (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  メディア ファミリごとに 1 行のデータを格納します。 メディア ファミリがミラー化されたメディア セット内にある場合は、メディア セット内のミラーごとに個別の行が格納されます。 このテーブルに格納されます、 **msdb**データベース。  
    
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|このファミリがメンバーであるメディア セットを識別する一意な識別番号。 参照**backupmediaset(media_set_id)**|  
|**family_sequence_number**|**tinyint**|メディア セット内のこのメディア ファミリの位置。|  
|**media_family_id**|**uniqueidentifier**|メディア ファミリを識別する一意の識別番号。 NULL にすることができます。|  
|**media_count**|**int**|メディア ファミリ内のメディアの数。 NULL にすることができます。|  
|**logical_device_name**|**nvarchar(128)**|バックアップ デバイスの名前**sys.backup_devices.name**します。 これが一時的なバックアップ デバイスの場合 (永続的なバックアップ デバイスに存在するのではなく**sys.backup_devices**) の値**logical_device_name**は NULL です。|  
|**physical_device_name**|**nvarchar(260)**|バックアップ デバイスの物理名。 NULL にすることができます。 このフィールドは、バックアップおよび復元プロセスで共有されます。 これには、元のバックアップ先のパスまたは復元の元のソース パスを含めることができます。 によって、かどうかのバックアップまたは復元最初に発生したデータベースのサーバーにします。 同じバックアップ ファイルからの連続する復元が、復元時にその場所に関係なく、パスを更新できないことに注意してください。 このため、 **physical_device_name**使用復元パスを表示するフィールドを使用できません。|  
|**device_type**|**tinyint**|バックアップ デバイスの種類。<br /><br /> 2 = ディスク<br /><br /> 5 = テープ<br /><br /> 7 = 仮想デバイス<br /><br /> 9 = azure Storage<br /><br /> 105 = パーマネントなバックアップ デバイス。<br /><br /> NULL にすることができます。<br /><br /> すべての永続的なデバイス名とデバイス番号で見つかる**sys.backup_devices**します。|  
|**physical_block_size**|**int**|メディア ファミリを記述するために使用する物理ブロック サイズ。 NULL にすることができます。|  
|**mirror**|**tinyint**|ミラー数 (0 ～ 3)。|  
  
## <a name="remarks"></a>コメント  
 RESTORE VERIFYONLY FROM *backup_device* WITH LOADHISTORY の列に設定、 **backupmediaset**メディア セット ヘッダーから適切な値を持つテーブル。  
  
 このテーブルおよびその他のバックアップと履歴テーブルの行の数を減らすためには、実行、 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)ストアド プロシージャ。  
  
## <a name="see-also"></a>参照  
 [バックアップし、復元テーブル&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [システム テーブル &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
