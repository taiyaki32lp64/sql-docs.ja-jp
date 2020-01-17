---
title: sys.dm_db_rda_schema_update_status (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_schema_update_status
- sys.dm_db_rda_schema_update_status_TSQL
- dm_db_rda_schema_update_status
- dm_db_rda_schema_update_status_TSQL
helpviewer_keywords:
- sys.dm_db_rda_schema_update_status dynamic management view
ms.assetid: 364e3caa-a7c6-4be5-a029-0b19da34de3e
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 611fe9d5bea47204b655f2defe5072d2dd17be92
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937014"
---
# <a name="stretch-database---sysdmdbrdaschemaupdatestatus"></a>Stretch Database - sys.dm_db_rda_schema_update_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  現在のデータベースで Stretch 対応テーブルごとのリモート データ アーカイブの各スキーマの更新タスクの 1 つの行が含まれています。 タスクは、そのタスク id によって識別されます。  
  
 **dm_db_rda_schema_update_status**スコープは現在のデータベース コンテキストに設定します。 スキーマの更新プログラムの状態を表示する、Stretch 対応テーブルのデータベース コンテキスト内にいることを確認します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|リモート データ アーカイブ スキーマ ローカルの Stretch 対応テーブルの ID を更新しています。|  
|**database_id**|**int**|ローカルの Stretch 対応テーブルを含むデータベースの ID。|  
|**task_id**|**bigint**|リモート データ アーカイブのスキーマの更新タスクの ID。|  
|**task_type**|**int**|リモート データ アーカイブのスキーマの更新タスクの型。|  
|**task_type_desc**|**nvarchar**|リモート データ アーカイブのスキーマの更新タスクの種類の説明です。|  
|**task_state**|**int**|リモート データ アーカイブのスキーマの更新タスクの状態。|  
|**task_state_des**|**nvarchar**|リモート データ アーカイブのスキーマの更新タスクの状態の説明。|  
|**start_time_utc**|**datetime**|リモート データのアーカイブ スキーマの更新を開始する UTC 時刻。|  
|**end_time_utc**|**datetime**|リモートのデータがスキーマの更新をアーカイブする UTC 時刻が完了しました。|  
|**error_number**|**int**|リモート データ アーカイブのスキーマの更新が失敗した場合は、エラーが発生しました。 エラー数それ以外の場合は null です。|  
|**error_severity**|**int**|リモート データ アーカイブのスキーマの更新が失敗した場合は、発生したエラーの重大度それ以外の場合は null です。|  
|**error_state**|**int**|リモート データ アーカイブのスキーマの更新が失敗した場合は、発生したエラーの状態それ以外の場合は null です。 Error_state は、条件またはエラーが発生した場所を示します。|  
  
## <a name="see-also"></a>関連項目  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
