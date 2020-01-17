---
title: Database Suspect Data Page イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- suspect_pages system table
- database mirroring [SQL Server], event notifications
- Database Suspect Data Page event class
ms.assetid: 098e1443-a8a0-425c-9311-0a479b1370ed
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 10caa7bd8270cdc73d1d5f9addd2b0ef55b89073
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68009540"
---
# <a name="database-suspect-data-page-event-class"></a>Database Suspect Data Page イベント クラス
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **Database Suspect Data Page** イベント クラスは、 [msdb](../../relational-databases/system-tables/suspect-pages-transact-sql.md) の [suspect_pages](../../relational-databases/databases/msdb-database.md)テーブルにページがいつ追加されたかを示します。 このイベント クラスは、問題があると思われるページの発生を監視するトレースに含めます。  
  
> [!NOTE]  
>  このイベントは、 **suspect_pages** テーブルへの対応する行の挿入とは非同期に発行されます。 したがって、このイベントを受信待ちするジョブでは、対応する **suspect_pages** エントリを直ちに見つけることができない場合があります。  
  
 **Database Suspect Data Page** イベント クラスをトレースに含めても、相対的なオーバーヘッドは低くなります。 問題があると思われるページ数が増えた場合 (ディスク ドライブで問題が発生した場合など) はオーバーヘッドが大きくなる可能性があります。  
  
## <a name="database-suspect-data-page-event-class-data-columns"></a>Database Suspect Data Page イベント クラスのデータ列  
  
|データ列名|データ型|[説明]|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|問題があると思われるページのイベントが発生したデータベースの ID。 これは **suspect_pages** テーブルの **database_id** 列と同じです。|3|はい|  
|**EventClass**|**int**|イベントの種類は 213 です。|27|いいえ|  
|**EventSequence**|**int**|バッチ内のイベント クラスのシーケンス。|51|いいえ|  
|**SPID**|**int**|問題があると思われるページが発生した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] タスクの ID。|12|はい|  
|**StartTime**|**datetime**|イベントが発生した時刻。|14|はい|  
|**Exchange Spill**|**int**|問題があると思われるページを格納しているデータベース ファイルの ID。 これは **suspect_pages** テーブルの **file_id** 列と同じです。|22|はい|  
|**ObjectID2**|**int**|ファイル内の問題があると思われるページの ID。 これは **suspect_pages** テーブルの **page_id** 列と同じです。|56|はい|  
|**Error**|**int**|発生したエラーの種類。 この値は、 **suspect_pages** テーブルのページの **event_type** 値と同じです。|31|はい|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [suspect_pages テーブルの管理 &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
