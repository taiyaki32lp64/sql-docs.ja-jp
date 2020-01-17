---
title: sys.remote_data_archive_tables (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.remote_data_archive_tables
- sys.remote_data_archive_tables_TSQL
- remote_data_archive_tables
- remote_data_archive_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_data_archive_tables catalog view
ms.assetid: 765069b7-60fd-414c-875f-3455460b75cd
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 65e42e6303b467abd38ddadb6be0c0d0fece46e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018189"
---
# <a name="stretch-database-catalog-views---sysremotedataarchivetables"></a>カタログ ビューでの Stretch Database sys.remote_data_archive_tables
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Stretch が有効なローカル テーブルからデータを格納する各リモート テーブルの 1 つの行が含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Stretch が有効なローカル テーブルのオブジェクトの ID。|  
|**remote_database_id**|**int**|自動生成されたローカルの識別子、リモート データベース。|  
|**remote_table_name**|**sysname**|Stretch が有効なローカル テーブルに対応するリモートのデータベース内のテーブルの名前です。|  
|**filter_predicate**|**nvarchar(max)**|フィルター述語では、存在する場合、移行するテーブル内の行を識別します。 値が null の場合、テーブル全体が移行の対象になります。<br /><br /> 詳細については、次を参照してください。[テーブルに対して Stretch Database を有効にする](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)と[フィルター述語を使用して移行する行を選択します。](~/sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)します。|  
|**migration_direction**|**tinyint**|これでデータが現在移行中の方向。 使用可能な値、次に示します。<br/>1 (送信)<br/>2 (受信)|  
|**migration_direction_desc**|**nvarchar(60)**|これでデータが現在移行中の方向の説明です。 使用可能な値、次に示します。<br/>送信 (1)<br/>受信 (2)|  
|**is_migration_paused**|**bit**|移行が現在一時停止しているかどうかを示します。|  
|**is_reconciled**|**bit**| リモート SQL Server のテーブルとが同期するかどうかを示します。<br/><br/>ときに、値の**is_reconciled** 1 (true) には、リモート SQL Server のテーブルとは同期、およびリモートのデータを含むクエリを実行することができます。<br/><br/>ときに、値の**is_reconciled**は 0 (false)、リモート SQL Server のテーブルと同期されていません。最近移行済みの行は、もう一度移行する必要があります。 これは、リモート Azure データベースを復元するとき、またはリモート テーブルから行を手動で削除するときに発生します。 テーブルを調整するまで、リモート データを含むクエリを実行することはできません。 テーブルを調整するために実行[sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)します。 |  
  
## <a name="see-also"></a>参照  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  

