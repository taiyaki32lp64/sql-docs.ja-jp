---
title: suspect_pages (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- suspect_page_table
- suspect_page_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- suspect_pages system table
- suspect pages [SQL Server]
ms.assetid: 119c8d62-eea8-44fb-bf72-de469c838c50
author: stevestein
ms.author: sstein
ms.openlocfilehash: 70dffcbf2ac3eac13f7ef42e901c4fcd99dce769
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130552"
---
# <a name="suspectpages-transact-sql"></a>suspect_pages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  マイナー 823 エラーまたは 824 エラーで失敗したページごとに 1 行が含まれています。 ページは、ため、それらが疑われるが、問題が実際にあります。 このテーブルに表示されます。 未確認のページを修復するでその状態が更新、 **event_type**列。  
  
 次の表は、最大 1,000 行には、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|このページを適用するデータベースの ID。|  
|**file_id**|**int**|データベース内のファイルの ID。|  
|**page_id**|**bigint**|問題があると考えられるページの ID。 すべてのページでは、データベース内のページの場所を識別する 32 ビット値であるページ ID を持ちます。 **Page_id**は 8 KB ページのデータ ファイルへのオフセット。 各ページ ID はファイル内で一意です。|  
|**event_type**|**int**|エラーの種類いずれか:<br /><br /> 1 = 問題があると考えられるページ (ディスク エラーなど) の原因となった 823 エラー、または、不正なチェックサムまたは破損ページ (不適切なページ ID) 以外の 824 エラー。<br /><br /> 2 = 不適切なチェックサム。<br /><br /> 3 = 破損ページ。<br /><br /> 4 = 復元済み (不正とマークされた後、ページが復元された)。<br /><br /> 5 = 修復済み (DBCC で修復されたページ)。<br /><br /> 7 = DBCC により割り当て解除。|  
|**error_count**|**int**|エラーが発生した回数。|  
|**last_update_date**|**datetime**|最終更新日時のタイムスタンプ。|  
  
## <a name="permissions"></a>アクセス許可  
 **msdb** に対するアクセスを持つユーザー は、 **suspect_pages** テーブルのデータを読み取ることができます。 suspect_pages テーブルに対する UPDATE 権限を持つすべてのユーザーは、そのレコードを更新できます。 **msdb** の **db_owner** 固定データベース ロールのメンバーまたは **sysadmin** 固定サーバー ロールのメンバーは、レコードの挿入、更新、および削除を行うことができます。  
  
## <a name="see-also"></a>関連項目  
 [ページ復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [Database Suspect Data Page イベント クラス](../../relational-databases/event-classes/database-suspect-data-page-event-class.md)   
 [システム テーブル&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [suspect_pages テーブルの管理 &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
