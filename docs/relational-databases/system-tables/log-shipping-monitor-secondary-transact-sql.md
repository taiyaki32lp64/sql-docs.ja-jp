---
title: log_shipping_monitor_secondary (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_secondary_TSQL
- log_shipping_monitor_secondary
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_secondary system table
ms.assetid: afbe1bb7-89a7-4020-9408-0af64a043c2e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 838c810c28c03ae11237f449483789ed8dbbf740
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989958"
---
# <a name="logshippingmonitorsecondary-transact-sql"></a>log_shipping_monitor_secondary (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ログ配布構成におけるセカンダリ データベースごとに 1 つの監視レコードを格納します。 このテーブルに格納されます、 **msdb**データベース。  
  
 履歴や監視に関連するテーブルは、プライマリ サーバーとセカンダリ サーバーにも使用されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**secondary_server**|**sysname**|セカンダリ インスタンスの名前、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ログ配布構成にします。|  
|**secondary_database**|**sysname**|ログ配布構成におけるセカンダリ データベースの名前。|  
|**secondary_id**|**uniqueidentifier**|ログ配布構成におけるセカンダリ サーバーの ID。|  
|**primary_server**|**sysname**|ログ配布構成における [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のプライマリ インスタンスの名前。|  
|**primary_database**|**sysname**|ログ配布構成におけるプライマリ データベースの名前。|  
|**restore_threshold**|**int**|許容経過時間を分単位の数は、アラートを生成する前に、操作を復元します。|  
|**threshold_alert**|**int**|復元のしきい値を超えたときに発生する警告。|  
|**threshold_alert_enabled**|**bit**|復元のしきい値の警告を有効にするかどうか。 1 = 有効にします。<br /><br /> 0 = 無効になっています。|  
|**last_copied_file**|**nvarchar(500)**|セカンダリ サーバーにコピーされた最後のバックアップ ファイルの名前。|  
|**last_copied_date**|**datetime**|セカンダリ サーバーに最後にコピー操作の日付と時刻。|  
|**last_copied_date_utc**|**datetime**|世界協定時刻で表される、セカンダリ サーバーに最後にコピー操作の日付と時刻。|  
|**last_restored_file**|**nvarchar(500)**|セカンダリ データベースに復元される最後のバックアップ ファイルの名前。|  
|**last_restored_date**|**datetime**|最後の日付と時刻は、セカンダリ データベースに対する操作を復元します。|  
|**last_restored_date_utc**|**datetime**|最後の日付と時刻、世界協定時刻で表される、セカンダリ データベースに対する操作を復元します。|  
|**last_restored_latency**|**int**|プライマリ ログ バックアップの作成時に、セカンダリで復元された場合との間経過した時間 (分) の量。<br /><br /> 初期値には NULL です。|  
|**history_retention_period**|**int**|時間、分単位でログ配布履歴されるレコードは削除する前に特定のセカンダリ データベースに保持されます。|  
  
## <a name="remarks"></a>コメント  
 に加えて、リモート監視サーバーでは、格納されているし、セカンダリ サーバーでセカンダリ サーバーに関連する情報が格納されていることもその**log_shipping_monitor_secondary**テーブル。  
  
## <a name="see-also"></a>関連項目  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_refresh_log_shipping_monitor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [sp_add_log_shipping_secondary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [sp_change_log_shipping_secondary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_monitor_secondary &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [システム テーブル &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
