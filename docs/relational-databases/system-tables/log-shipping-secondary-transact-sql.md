---
title: log_shipping_secondary (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_secondary
- log_shipping_secondary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_secondary system table
ms.assetid: 69723419-4544-49c6-a517-adb30ffa5741
author: stevestein
ms.author: sstein
ms.openlocfilehash: 687f9f7441b7d77ea191047ef22491728ba81047
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095824"
---
# <a name="logshippingsecondary-transact-sql"></a>log_shipping_secondary (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  セカンダリ ID ごとの 1 つのレコードを格納します。 このテーブルに格納されます、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**secondary_id**|**uniqueidentifier**|ログ配布構成におけるセカンダリ サーバーの ID。|  
|**primary_server**|**sysname**|プライマリ ログ配布構成では、SQL Server データベース エンジンのインスタンスの名前。|  
|**primary_database**|**sysname**|ログ配布構成におけるプライマリ データベースの名前。|  
|**backup_source_directory**|**nvarchar(500)**|プライマリ サーバーからのトランザクション ログ バックアップ ファイルの保存先ディレクトリ。|  
|**backup_destination_directory**|**nvarchar(500)**|バックアップ ファイルがコピー先のセカンダリ サーバー上のディレクトリ。|  
|**file_retention_period**|**int**|バックアップ ファイルが削除されるまで、セカンダリ サーバーで保持される分単位の時間の長さ。|  
|**copy_job_id**|**uniqueidentifier**|セカンダリ サーバーでのコピー ジョブに関連付けられた ID。|  
|**restore_job_id**|**uniqueidentifier**|セカンダリ サーバー上の復元ジョブに関連付けられている ID です。|  
|**monitor_server**|**sysname**|インスタンスの名前、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ログ配布構成で監視サーバーとして使用されています。|  
|**monitor_server_security_mode**|**bit**|監視サーバーへの接続に使用されるセキュリティ モード。<br /><br /> 1 = Windows 認証。<br /><br /> 0 =[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。|  
|**last_copied_file**|**nvarchar(500)**|セカンダリ サーバーにコピーされた最後のバックアップ ファイルの名前。|  
|**last_copied_date**|**datetime**|セカンダリ サーバーに最後にコピー操作の日付と時刻。|  
  
## <a name="remarks"></a>コメント  
 指定されたプライマリ データベースと同じセカンダリ サーバー上の複数のセカンダリ データベースは、いくつかの設定を共有、 **log_shipping_secondary**テーブル。 いずれかのデータベースに対して共有設定が変更された場合、変更はすべてのデータベースに適用されます。  
  
## <a name="see-also"></a>関連項目  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_secondary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [sp_change_log_shipping_secondary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [システム テーブル &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
