---
title: managed_backup.fn_available_backups (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- smart_admin.fn_available_backups
- smart_admin.fn_available_backups_TSQL
- fn_available_backups_TSQL
- fn_available_backups
dev_langs:
- TSQL
helpviewer_keywords:
- fn_available_backups
- smart_admin.fn_available_backups
ms.assetid: 7aa84474-16e5-49bd-a703-c8d1408ef107
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1c7bb6e33dfd2ee6640e9588011d3686a72a0188
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140669"
---
# <a name="managedbackupfnavailablebackups-transact-sql"></a>managed_backup.fn_available_backups (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  指定されたデータベースに使用可能なバックアップ ファイルの 0 行、1 行、または複数の行から成るテーブルを返します。 返されるバックアップ ファイルがによって作成されたバックアップ[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
managed_backup.fn_available_backups ([@database_name = ] 'database name')  
```  
  
##  <a name="Arguments"></a> 引数  
 @database_name  
 データベースの名前。 @database_nameは nvarchar (512)。  
  
## <a name="table-returned"></a>返されるテーブル  
 テーブルが一意のクラスター化制約 (database_guid、backup_start_date、および first_lsn, backup_type) にあります。   
データベースを削除してから再作成すると、すべてのデータベースのバックアップ セットが返されます。 出力は、各データベースを一意に識別する database_guid に従って並べ替えられます。   
LSN は、ログ チェーンの中断があることを意味の矛盾点がある場合は、テーブルには不足している各 LSN セグメントに対して特別な行が含まれます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|Backup_path|NVARCHAR(260) COLLATE Latin1_General_CI_AS_KS_WS|バックアップ ファイルの URL。|  
|backup_type|NVARCHAR (6)|'DB' データベースのバックアップのログ バックアップには、"LOG"。|  
|expiration_date|DATETIME|このファイルが削除される予定日。 これは、指定された保有期間内の特定の時点にデータベースを復旧する機能に基づいて設定されます。|  
|database_guid|一意識別子|指定したデータベースの GUID 値。  GUID はデータベースを一意に識別します。|  
|first_lsn|NUMERIC (25, 0)|バックアップ セット内の先頭または最も古いログ レコードのログ シーケンス番号。 NULL にすることができます。|  
|last_lsn|NUMERIC (25, 0)|バックアップ セットの次のログ レコードのログ シーケンス番号。 NULL にすることができます。|  
|backup_start_date|DATETIME|バックアップ操作が開始された日付と時刻。|  
|backup_finish_date|NVARCHAR (128)|バックアップ操作が終了した日付と時刻。|  
|machine_name|NVARCHAR (128)|SQL Server インスタンスがインストールされ実行されているコンピューターの名前[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]します。|  
|last_recovery_fork_id|一意識別子|終了の復旧分岐の id 番号。|  
|first_recovery_fork_id|一意識別子|最初の復旧分岐の ID。 データのバックアップ、first_recovery_fork_guid は last_recovery_fork_guid と同じです。|  
|fork_point_lsn|NUMERIC (25, 0)|first_recovery_fork_id が last_recovery_fork_id に等しくない場合は、分岐ポイントのログ シーケンス番号。 これらが同じである場合、この値は NULL になります。|  
|availability_group_guid|一意識別子|データベースが Alwayson データベースの場合は、これは、可用性グループの GUID です。 それ以外の場合、この値は NULL です。|  
  
## <a name="return-code-value"></a>リターン コード値  
 0 (成功) または 1 (失敗)。  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 必要があります**選択**この関数に対する権限。  
  
## <a name="examples"></a>使用例  
 次の例では、すべての利用可能なバックアップを使用してバックアップを表示する[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]データベース"MyDB"の  
  
```  
SELECT *   
FROM managed_backup.fn_available_backups ('MyDB')  
  
```  
  
## <a name="see-also"></a>関連項目  
 [Microsoft Azure への SQL Server マネージ バックアップ](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)   
 [Microsoft Azure に格納されたバックアップからの復元](../../relational-databases/backup-restore/restoring-from-backups-stored-in-microsoft-azure.md)  
  
  
