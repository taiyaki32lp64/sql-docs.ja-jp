---
title: sp_delete_backuphistory (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_backuphistory
- sp_delete_backuphistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_backuphistory
ms.assetid: bdb56834-616e-47e4-b942-e895d2325e97
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5c538a217c5d86f2b59f079f8629a6f4cbe9fea3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120063"
---
# <a name="spdeletebackuphistory-transact-sql"></a>sp_delete_backuphistory (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定した日付より古いバックアップ セットのエントリを削除することによって、バックアップと復元履歴テーブルのサイズを縮小します。 追加の行は、バックアップに追加され、各バックアップ復元履歴テーブルまたは復元操作が実行されます。定期的に実行こと勧めそのため、 **sp_delete_backuphistory**します。  
  
> [!NOTE]  
>  バックアップと復元履歴テーブルに存在、 **msdb**データベース。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_delete_backuphistory [ @oldest_date = ] 'oldest_date'   
```  
  
## <a name="arguments"></a>引数  
`[ @oldest_date = ] 'oldest\_date'` 最も古い日付は、バックアップと復元履歴テーブルに保持されます。 *oldest_date*は**datetime**、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 **sp_delete_backuphistory**から実行する必要があります、 **msdb**データベースし、次のテーブルに影響します。  
  
-   [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)  
  
-   [backupfilegroup](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)  
  
-   [backupmediafamily](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)  
  
-   [backupmediaset](../../relational-databases/system-tables/backupmediaset-transact-sql.md)  
  
-   [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
-   [restorefile](../../relational-databases/system-tables/restorefile-transact-sql.md)  
  
-   [restorefilegroup](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)  
  
-   [restorehistory](../../relational-databases/system-tables/restorehistory-transact-sql.md)  
  
 すべての履歴を削除しても、物理的なバックアップ ファイルは維持されます。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **sysadmin**他のユーザーには、固定サーバー ロールがアクセス許可を付与することができます。  
  
## <a name="examples"></a>使用例  
 次の例では、バックアップと復元の履歴テーブルから 2010 年 1 月 14 日の午前 12 時 より前のすべてのエントリを削除します。  
  
```  
USE msdb;  
GO  
EXEC sp_delete_backuphistory @oldest_date = '01/14/2010';  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_delete_database_backuphistory &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-backuphistory-transact-sql.md)   
 [バックアップの履歴とヘッダーの情報 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
