---
title: Database Suspect Data Page イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- suspect_pages system table
- database mirroring [SQL Server], event notifications
- Database Suspect Data Page event class
ms.assetid: 098e1443-a8a0-425c-9311-0a479b1370ed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 78e6a175ce7757a9e9808a5a993bec6a44a3db2a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62662994"
---
# <a name="database-suspect-data-page-event-class"></a>Database Suspect Data Page イベント クラス
  **Database Suspect Data Page** イベント クラスは、 [msdb](/sql/relational-databases/system-tables/suspect-pages-transact-sql) の [suspect_pages](../databases/msdb-database.md)テーブルにページがいつ追加されたかを示します。 このイベント クラスは、問題があると思われるページの発生を監視するトレースに含めます。  
  
> [!NOTE]  
>  このイベントは、 **suspect_pages** テーブルへの対応する行の挿入とは非同期に発行されます。 したがって、このイベントを受信待ちするジョブでは、対応する **suspect_pages** エントリを直ちに見つけることができない場合があります。  
  
 **Database Suspect Data Page** イベント クラスをトレースに含めても、相対的なオーバーヘッドは低くなります。 問題があると思われるページ数が増えた場合 (ディスク ドライブで問題が発生した場合など) はオーバーヘッドが大きくなる可能性があります。  
  
## <a name="database-suspect-data-page-event-class-data-columns"></a>Database Suspect Data Page イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|問題があると思われるページのイベントが発生したデータベースの ID。 これは **suspect_pages** テーブルの **database_id** 列と同じです。|3|はい|  
|**EventClass**|**int**|イベントの種類は 213 です。|27|いいえ|  
|**EventSequence**|**int**|バッチ内のイベント クラスのシーケンス。|51|いいえ|  
|**SPID**|**int**|問題があると思われるページが発生した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] タスクの ID。|12|はい|  
|**StartTime**|**datetime**|イベントが発生した時刻。|14|はい|  
|**Exchange Spill**|**int**|問題があると思われるページを格納しているデータベース ファイルの ID。 これは **suspect_pages** テーブルの **file_id** 列と同じです。|22|はい|  
|**ObjectID2**|**int**|ファイル内の問題があると思われるページの ID。 これは **suspect_pages** テーブルの **page_id** 列と同じです。|56|[はい]|  
|**Error**|**int**|発生したエラーの種類。 この値は、 **suspect_pages** テーブルのページの **event_type** 値と同じです。|31|はい|  
  
## <a name="see-also"></a>参照  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [suspect_pages テーブルの管理 &#40;SQL Server&#41;](../backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
