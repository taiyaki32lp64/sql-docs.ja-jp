---
title: sys.dm_tran_commit_table (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_commit_table
- dm_tran_commit_table_TSQL
- sys.dm_tran_commit_table
- sys.dm_tran_commit_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_commit_table dynamic management view
ms.assetid: 732d23c5-1f6c-4e96-bc85-8f29b520cf0e
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4bd5b497f1d96f813570282f785fe0cbfe73265d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017927"
---
# <a name="change-tracking---sysdmtrancommittable"></a>変更の追跡 - sys.dm_tran_commit_table
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  によって追跡されたテーブルに対してコミットされたトランザクションごとに 1 つの行を表示します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]変更の追跡。 サポート用に提供されている sys.dm_tran_commit_table 管理ビューには、トランザクション関連の情報が表示されます。この情報は、変更の追跡によって sys.syscommittab システム テーブルに格納されます。 sys.syscommittab テーブルは、データベース固有のトランザクション ID からトランザクションのコミット ログ シーケンス番号 (LSN) とコミット タイムスタンプへの、効率的かつ永続的なマッピングを提供します。 Sys.syscommittab テーブルに格納され、この管理ビューで公開されるデータは、保有期間に従ってクリーンアップ時に指定変更の追跡の構成します。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_tran_commit_table**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|commit_ts|**bigint**|各データベースに固有のタイムスタンプとして機能する単調に増加数では、トランザクションをコミットします。|  
|xdes_id|**bigint**|トランザクションの内部 ID をデータベースに固有です。|  
|commit_lbn|**bigint**|トランザクションのコミット ログ レコードを含むログ ブロックの数。|  
|commit_csn|**bigint**|トランザクションのコミットのインスタンスに固有のシーケンス番号。|  
|commit_time|**smalldatetime**|トランザクションがコミットされた時刻。|  
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [変更の追跡について &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)  
  
  


