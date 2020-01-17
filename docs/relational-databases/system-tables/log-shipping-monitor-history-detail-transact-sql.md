---
title: log_shipping_monitor_history_detail (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_history_detail_TSQL
- log_shipping_monitor_history_detail
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_history_detail system table
ms.assetid: 7080c888-323b-4206-a1ab-e6c51f9e2579
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0f0a304020b972b29d521bd32da3f98b8d3fdfc9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989998"
---
# <a name="logshippingmonitorhistorydetail-transact-sql"></a>log_shipping_monitor_history_detail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ログ配布ジョブの履歴の詳細を格納します。 このテーブルに格納されます、 **msdb**データベース。  
  
 履歴や監視に関連するテーブルは、プライマリ サーバーとセカンダリ サーバーにも使用されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**agent_id**|**uniqueidentifier**|バックアップ用のプライマリ ID、またはコピーまたは復元用のセカンダリ ID。|  
|**agent_type**|**tinyint**|ログ配布ジョブの種類。<br /><br /> 0 = バックアップ。<br /><br /> 1 = コピーします。<br /><br /> 2 = 復元です。|  
|**session_id**|**int**|バックアップ、コピー、復元のセッション ID/ジョブします。|  
|**database_name**|**sysname**|このレコードに関連付けられているデータベースの名前。 復元では、バックアップ、セカンダリ データベースのコピーの場合は空白のプライマリ データベースです。|  
|**session_status**|**tinyint**|セッションの状態です。<br /><br /> 0 = 開始<br /><br /> 1 = 実行中です。<br /><br /> 2 = 成功。<br /><br /> 3 = エラー。<br /><br /> 4 = 警告|  
|**log_time**|**datetime**|レコードが作成された日時。|  
|**log_time_utc**|**datetime**|日付と位置、レコードが作成された時刻、世界協定時刻で表されます。|  
|**message**|**nvarchar(max)**|メッセージ テキスト。|  
  
## <a name="remarks"></a>コメント  
 このテーブルには、ログ配布エージェントの履歴の詳細が含まれています。 エージェント セッションを識別するために列を使用して、 **agent_id**、 **agent_type**、および**session_id**します。 エージェント セッションの履歴詳細を表示、並べ替え**log_time**します。  
  
 内のプライマリ サーバーでリモート監視サーバーに格納されるだけでなく、プライマリ サーバーに関連する情報が格納されているその**log_shipping_monitor_history_detail**テーブル、およびセカンダリに関連する情報サーバーがセカンダリ サーバーでも格納されているその**log_shipping_monitor_history_detail**テーブル。  
  
## <a name="see-also"></a>関連項目  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_delete_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_cleanup_log_shipping_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [システム テーブル&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [log_shipping_monitor_error_detail &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql.md)  
  
  
