---
title: log_shipping_monitor_error_detail (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_error_detail_TSQL
- log_shipping_monitor_error_detail
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_error_detail system table
ms.assetid: 0c38a625-60d2-4ee2-bcf3-2ba367914220
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5e441e5165262a4455e34cb9a0adb55b9679578f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990056"
---
# <a name="logshippingmonitorerrordetail-transact-sql"></a>log_shipping_monitor_error_detail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ログ配布ジョブのエラーの詳細を格納します。 このテーブルに格納されます、 **msdb**データベース。  
  
 履歴や監視に関連するテーブルは、プライマリ サーバーとセカンダリ サーバーにも使用されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**agent_id**|**uniqueidentifier**|バックアップ用のプライマリ ID、またはコピーまたは復元用のセカンダリ ID。|  
|**agent_type**|**tinyint**|ログ配布ジョブの種類。<br /><br /> 0 = バックアップ。<br /><br /> 1 = コピーします。<br /><br /> 2 = 復元です。|  
|**session_id**|**int**|バックアップ、コピー、復元のセッション ID/ジョブします。|  
|**database_name**|**sysname**|このエラー レコードに関連付けられているデータベースの名前。 復元では、バックアップ、セカンダリ データベースのコピーの場合は空白のプライマリ データベースです。|  
|**sequence_number**|**int**|複数のレコードにまたがるエラーに関する情報の適切な順序を示す増分の番号。|  
|**log_time**|**datetime**|レコードが作成された日時。|  
|**log_time_utc**|**datetime**|日付と位置、レコードが作成された時刻、世界協定時刻で表されます。|  
|**message**|**nvarchar**|メッセージ テキスト。|  
|**source**|**nvarchar**|エラー メッセージまたはイベントのソース。|  
|**help_url**|**nvarchar**|URL は、エラーの詳細についてはありますが使用可能な場合です。|  
  
## <a name="remarks"></a>コメント  
 このテーブルには、ログ配布エージェントに関するエラーの詳細が格納されます。 各エラーは一連の例外として記録され、 エージェントのセッションごとに複数のエラー (シーケンス) があります。  
  
 内のプライマリ サーバーでリモート監視サーバーに格納されるだけでなく、プライマリ サーバーに関連する情報が格納されているその**log_shipping_monitor_error_detail**テーブル、およびセカンダリ サーバーに関連する情報セカンダリ サーバーに格納されてもその**log_shipping_monitor_error_detail**テーブル。  
  
 エージェント セッションを識別するために列を使用して、 **agent_id**、 **agent_type**、および**session_id**します。 並べ替える**log_time**記録された順序でエラーを表示します。  
  
## <a name="see-also"></a>関連項目  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [log_shipping_monitor_history_detail &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql.md)   
 [sp_cleanup_log_shipping_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [システム テーブル &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
