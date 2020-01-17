---
title: log_shipping_monitor_primary (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_primary
- log_shipping_monitor_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_primary system table
ms.assetid: 5f629a29-1a62-40e6-ae33-6f6b7dd09a36
author: stevestein
ms.author: sstein
ms.openlocfilehash: d39ea859f1fd2cc3064d8d8c71c91ba6324f162c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989977"
---
# <a name="logshippingmonitorprimary-transact-sql"></a>log_shipping_monitor_primary (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  各ログ配布構成内のプライマリ データベースごとに、1 つの監視レコードを格納します。 このテーブルに格納されます、 **msdb**データベース。  
  
 履歴や監視に関連するテーブルは、プライマリ サーバーとセカンダリ サーバーにも使用されます。   
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|ログ配布構成におけるプライマリ データベースの ID。|  
|**primary_server**|**sysname**|プライマリ インスタンスの名前、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ログ配布構成にします。|  
|**primary_database**|**sysname**|ログ配布構成におけるプライマリ データベースの名前。|  
|**backup_threshold**|**int**|分単位の許容経過時間を通知する前にバックアップ操作の数が生成されます。|  
|**threshold_alert**|**int**|バックアップのしきい値を超えたときに発生する警告。|  
|**threshold_alert_enabled**|**bit**|バックアップのしきい値のアラートが有効になっているかどうかを決定します。 1 = 有効にします。<br /><br /> 0 = 無効になっています。|  
|**last_backup_file**|**nvarchar(500)**|最新のトランザクション ログ バックアップの絶対パス。|  
|**last_backup_date**|**datetime**|最後のトランザクションの日付と時刻は、プライマリ データベースでバックアップ操作にログインします。|  
|**last_backup_date_utc**|**datetime**|最後のトランザクションの日付と時刻は、世界協定時刻で表される、プライマリ データベースでバックアップ操作にログインします。|  
|**history_retention_period**|**int**|指定したプライマリ データベースでログ配布履歴レコードが保持される時間 (分単位)。この時間を過ぎるとレコードは削除されます。|  
  
## <a name="remarks"></a>コメント  
 内のプライマリ サーバーでリモート監視サーバーに格納されるだけでなく、プライマリ サーバーに関連する情報が格納されているその**log_shipping_monitor_primary**テーブル。  
  
## <a name="see-also"></a>関連項目  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)   
 [sp_change_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [sp_help_log_shipping_monitor_primary &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql.md)   
 [sp_delete_log_shipping_alert_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-alert-job-transact-sql.md)   
 [システム テーブル &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
