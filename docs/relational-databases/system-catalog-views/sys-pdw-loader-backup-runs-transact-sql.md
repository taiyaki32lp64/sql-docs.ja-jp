---
title: sys.pdw_loader_backup_runs (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2b72034c-6a11-46b9-a76c-7a88b2bea360
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c8e7826e4dcefdbed65fb0fa1f3368411a9ef12a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127471"
---
# <a name="syspdwloaderbackupruns-transact-sql"></a>sys.pdw_loader_backup_runs (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  進行中と完了したバックアップと復元操作に関する情報を格納[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]、および進行中と完了したバックアップ、復元、および読み込みの操作で[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]します。 情報は、システムの再起動の間で永続化します。  
  
|列名|データ型|説明|範囲|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|特定のバックアップ、復元、またはロードの実行の一意の識別子。<br /><br /> このビューのキー。||  
|NAME|**nvarchar (255)**|負荷の場合は null です。 バックアップまたは復元オプションの名前。||  
|submit_time|**datetime**|要求が送信された時刻。||  
|start_time|**datetime**|操作の開始時刻します。||  
|end_time|**datetime**|時間、操作の完了、失敗、またはが取り消されました。||  
|total_elapsed_time|**int**|時間の合計では、start_time と現在の時刻の間または start_time と end_time の間が経過した完了、キャンセル、または失敗した実行します。|Total_elapsed_time では、整数値 (ミリ秒単位で 24.8 日) の最大値を超えるをオーバーフローしました期日の実体化エラーが発生します。<br /><br /> 最大値をミリ秒単位は 24.8 日に相当します。|  
|operation_type|**nvarchar(16)**|負荷の種類。|' BACKUP'、'LOAD'、'RESTORE'|  
|mode|**nvarchar(16)**|実行の種類のモードです。|Operation_type =**バックアップ**<br />**DIFFERENTIAL**<br />**FULL**<br /><br /> Operation_type =**負荷**<br />**追加**<br />**RELOAD**<br />**UPSERT**<br /><br /> Operation_type =**復元**<br />**DATABASE**<br />**HEADER_ONLY**|  
|database_name|**nvarchar (255)**|この操作のコンテキストとなっているデータベースの名前||  
|table_name|**nvarchar (255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|Principal_id|**int**|操作を要求するユーザーの ID。||  
|session_id|**nvarchar(32)**|操作を実行するセッションの ID。|Session_id を参照してください。 [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)します。|  
|request_id|**nvarchar(32)**|操作を実行する要求の ID。 読み込み、これが、この負荷に関連付けられている現在または最近要求.|Request_id 内を参照してください。 [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)します。|  
|status|**nvarchar(16)**|実行の状態。|'が取り消されました'、' 完了 '、'失敗'、'QUEUED'、'実行中|  
|進行状況|**int**|完了率。|0 ~ 100|  
|command|**nvarchar (4000)**|ユーザーによって送信されたコマンドの完全なテキスト。|(スペースをカウントする)、4,000 文字より長い場合は切り捨てられます。|  
|rows_processed|**bigint**|この操作の一部として処理された行の数。||  
|rows_rejected|**bigint**|この操作の一部として拒否された行の数。||  
|rows_inserted|**bigint**|この操作の一環として、データベース テーブルに挿入された行の数。||  
  
## <a name="see-also"></a>関連項目  
 [SQL Data Warehouse と Parallel Data Warehouse カタログ ビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
