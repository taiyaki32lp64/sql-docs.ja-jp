---
title: sp_delete_backup (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 808e50ae-ff6e-4520-9ce2-530591d3d59b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 49eb0906a9a5af1fec2abfeec3ef58845b605e69
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941820"
---
# <a name="spdeletebackup-transact-sql"></a>sp_delete_backup (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  すべてのスナップショットと、バックアップ ファイル スナップショット バックアップ セット、指定されたデータベースからの構成を削除します。 このシステム ストアド プロシージャは、スナップショット バックアップ セットを管理するためだけの推奨される方法です。 詳細については、「 [Azure でのデータベース ファイルのファイル スナップショット バックアップ](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_delete_backup   
    [ @backup_url = ] backup_metadata_file_url  
    ,[ [ @db_name = ] database_name | NULL ]  
```  
  
## <a name="arguments"></a>引数  
 *[ @backup_url =] backup_meta_file_url*  
 バックアップ ファイル自体を含む設定の指定されたバックアップを構成するすべてのスナップショットを削除する、削除するバックアップの URL。  
  
 *[ @db_name =] database_name*  
 削除するスナップショットを含むデータベースの名前。 データベース名が提供される、システムは、指定されたデータベースのバックアップの URL を使用して、バックアップの URL が提供されることを検証の場合[sp_delete_backup_file_snapshot &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)各スナップショットを削除します。 データベース名が指定されていない場合は、このデータベースのチェックは実行されません。  
  
## <a name="permissions"></a>アクセス許可  
 ALTER ANY DATABASE 権限または指定されたデータベースに対する ALTER 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [sys.fn_db_backup_file_snapshots &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup_file_snapshot (Transact-SQL)](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
