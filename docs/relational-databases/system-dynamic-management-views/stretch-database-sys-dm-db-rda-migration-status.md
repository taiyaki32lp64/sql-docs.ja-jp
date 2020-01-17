---
title: sys.dm_db_rda_migration_status (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_migration_status
- sys.dm_db_rda_migration_status_TSQL
- dm_db_rda_migration_status
- dm_db_rda_migration_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_rda_migration_status dynamic management view
ms.assetid: faf3901c-a0e0-4e0c-8b1b-86d9f15f34dd
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 21e5230e4f3efd86fe90382202f0b21a0187a214
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937062"
---
# <a name="stretch-database---sysdmdbrdamigrationstatus"></a>Stretch Database - sys.dm_db_rda_migration_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  ローカル インスタンス上のそれぞれの Stretch 対応テーブルから移行されたデータのバッチごとの 1 つの行を含む[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 バッチは、開始時刻と終了時刻によって識別されます。  
  
 **sys.dm_db_rda_migration_status**スコープは現在のデータベース コンテキストに設定します。 移行の状態を表示するストレッチを有効にテーブルのデータベース コンテキストで確認するようにします。  
  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]の出力**sys.dm_db_rda_migration_status** 200 行に制限されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|行が移行されたテーブルの ID。|  
|**database_id**|**int**|行が移行されたデータベースの ID。|  
|**migrated_rows**|**bigint**|行の数は、このバッチで移行します。|  
|**start_time_utc**|**datetime**|バッチが開始された UTC 時刻。|  
|**end_time_utc**|**datetime**|バッチが完了した UTC 時刻。|  
|**error_number**|**int**|バッチが失敗した場合は、エラーが発生しました。 エラー数それ以外の場合は null です。|  
|**error_severity**|**int**|バッチが失敗した場合は、発生したエラーの重大度それ以外の場合は null です。|  
|**error_state**|**int**|バッチが失敗した場合は、発生したエラーの状態それ以外の場合は null です。<br /><br /> **Error_state**条件またはエラーが発生した場所を示します。|  
  
## <a name="see-also"></a>関連項目  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
