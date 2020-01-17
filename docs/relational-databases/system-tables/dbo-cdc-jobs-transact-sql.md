---
title: dbo.cdc_jobs (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc_jobs
- cdc_jobs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dbo.cdc_jobs
ms.assetid: 85e2d580-1c54-4b81-b7e6-2e12997199fd
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0c9668c234728dc34952a7095889fe6ba5cfd06a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084701"
---
# <a name="dbocdc_jobs-transact-sql"></a>dbo.cdc_jobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  キャプチャ ジョブおよびクリーンアップ ジョブで使用される、変更データ キャプチャの構成パラメーターを格納します。 このテーブルに格納されます**msdb**します。  
  
 
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ジョブが実行されるデータベースの ID。|  
|**job_type**|**nvarchar(20)**|ジョブの種類 ('capture' または 'cleanup')。|  
|**job_id**|**uniqueidentifier**|ジョブに関連付けられた一意の ID。|  
|**maxtrans**|**int**|各スキャン サイクルで処理する最大トランザクション数。<br /><br /> **maxtrans** はキャプチャ ジョブでのみ有効です。|  
|**maxscans**|**int**|ログからすべての行を抽出するために実行する最大スキャン サイクル数。<br /><br /> **maxscans** はキャプチャ ジョブでのみ有効です。|  
|**continuous**|**bit**|キャプチャ ジョブを連続的に実行するか (1)、1 回だけ実行するか (0) を示すフラグ。 詳細については、次を参照してください。 [sys.sp_cdc_add_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)します。<br /><br /> **continuous** はキャプチャ ジョブでのみ有効です。|  
|**pollinginterval**|**bigint**|ログ スキャン サイクル間の秒数。<br /><br /> **pollinginterval** はキャプチャ ジョブでのみ有効です。|  
|**retention**|**bigint**|変更行が変更テーブルに保持される分数。<br /><br /> **retention** はクリーンアップ ジョブでのみ有効です。|  
|**threshold**|**bigint**|クリーンアップ時に 1 つのステートメントを使用して削除できる最大削除エントリ数。|  
  
## <a name="see-also"></a>参照  
 [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)   
 [sys.sp_cdc_change_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md)   
 [sys.sp_cdc_help_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)   
 [sys.sp_cdc_drop_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-drop-job-transact-sql.md)  
  
  
