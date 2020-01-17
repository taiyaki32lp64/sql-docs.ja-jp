---
title: restorefile (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- restorefile
- restorefile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restorefile system table
- restoring files [SQL Server], restorefile system table
- file restores [SQL Server], restorefile system table
ms.assetid: 8e40145a-8559-4abe-8e2a-39b818928009
author: stevestein
ms.author: sstein
ms.openlocfilehash: 788d0296087ee8980be0b0ecf56c43f09fb3780c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910189"
---
# <a name="restorefile-transact-sql"></a>restorefile (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  復元されたファイルごとに 1 行のデータを格納します。復元されたファイルには、ファイル グループ名から間接的に復元されたものも含まれます。 このテーブルに格納されます、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|対応する復元操作を特定するための一意な識別番号。 参照**restorehistory (restore_history_id)** します。|  
|**file_number**|**numeric(10,0)**|復元されたファイルのファイル識別番号。 この数は、各データベース内で一意である必要があります。 NULL にすることができます。<br /><br /> データベースは、データベース スナップショットに戻す、この値は、完全な復元と同じ方法で指定されます。|  
|**destination_phys_drive**|**nvarchar(260)**|ドライブまたはパーティションのファイルの復元します。 NULL にすることができます。<br /><br /> データベースは、データベース スナップショットに戻す、この値は、完全な復元と同じ方法で指定されます。|  
|**destination_phys_name**|**nvarchar(260)**|ファイルの復元先のファイル名。ドライブやパーティション情報は含みません。 NULL にすることができます。<br /><br /> データベースは、データベース スナップショットに戻す、この値は、完全な復元と同じ方法で指定されます。|  
  
## <a name="remarks"></a>コメント  
 このテーブルおよびその他のバックアップと履歴テーブルの行の数を減らすためには、実行、 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)ストアド プロシージャ。  
  
## <a name="see-also"></a>参照  
 [バックアップし、復元テーブル&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restorefilegroup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)   
 [restorehistory &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/restorehistory-transact-sql.md)   
 [システム テーブル &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
