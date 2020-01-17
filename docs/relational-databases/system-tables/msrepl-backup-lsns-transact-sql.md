---
title: MSrepl_backup_lsns (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_backup_lsns_TSQL
- MSrepl_backup_lsns
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_backup_Isns system table
ms.assetid: de06c349-82a8-48c6-b602-b5d6938514f6
author: stevestein
ms.author: sstein
ms.openlocfilehash: a1f22edf81e5e5e8ac7e2d9b44ce26e6b1f8bad2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032515"
---
# <a name="msrepl_backup_lsns-transact-sql"></a>MSrepl_backup_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSrepl_backup_lsns**テーブルには、ディストリビューション データベースの"sync with backup"オプションをサポートするためのトランザクション ログ シーケンス番号 (LSN) が含まれています。 このテーブルは、ディストリビューション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|パブリッシャー データベースの ID。|  
|**valid_xact_id**|**varbinary(16)**|ログの切り捨てをマークする、パブリッシャーに送信されるトランザクションの ID をポイントします。 ディストリビューション データベースは、"sync with backup"モードである場合にのみを使用します。 バックアップされたディストリビューション データベースで最新のレプリケートされたトランザクションの ID が含まれています。 パブリッシャーに送信する、ログの切り捨てポイントをマークする、ログ リーダーによって。|  
|**valid_xact_seqno**|**varbinary(16)**|ポイントのログの切り捨てをマークする、パブリッシャーに送信されるトランザクションのシーケンス番号。 ディストリビューション データベースが "sync with backup" モードの場合にのみ使用されます。 バックアップされたディストリビューション データベース内の、最新のレプリケートされたトランザクションのログ シーケンス番号に相当します。 パブリッシャーに送信する、ログの切り捨てポイントをマークする、ログ リーダーによって。|  
|**next_xact_id**|**varbinary(16)**|バックアップ操作で使用する一時的なログ シーケンス番号。|  
|**nextx_xact_seqno**|**varbinary(16)**|バックアップ操作で使用する一時的なログ シーケンス番号。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
