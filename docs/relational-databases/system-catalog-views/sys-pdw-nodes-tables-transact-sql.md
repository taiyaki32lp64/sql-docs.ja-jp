---
title: sys.pdw_nodes_tables (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 473b5d14-171b-4a16-9195-acf36d3f786c
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 5fa2412e61e30852497ffa00493ea6dbe244989a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001114"
---
# <a name="syspdwnodestables-transact-sql"></a>sys.pdw_nodes_tables (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  プリンシパルが所有しているか、またはをプリンシパルが権限を許可されて、テーブル オブジェクトごとの行が含まれています。  
  
|列名|データ型|説明|範囲|  
|-----------------|---------------|-----------------|-----------|  
|\<列を継承 >||このビューが継承する列の一覧は、次を参照してください。 [sys.objects](../system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)します。||  
|lob_data_space_id|**int**||常に 0 です。|  
|filestream_data_space_id|**int**|データ領域の FILESTREAM ファイル グループの ID または [!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|NULL|  
|max_column_id_used|**int**|このテーブルで使用される列の最大の ID。||  
|lock_on_bulk_load|**bit**|テーブルは、一括読み込みにロックされます。|TBD|  
|uses_ansi_nulls|**bit**|テーブルは、SET ANSI_NULLS データベース オプションが ON の場合に作成されます。|1|  
|is_replicated|**bit**|1 = テーブルはレプリケーションを使用してパブリッシュします。|0 になります。レプリケーションがサポートされていません。|  
|has_replication_filter|**bit**|1 = テーブルにはレプリケーション フィルターがあります。|0|  
|is_merge_published|**bit**|1 = テーブルは、マージ レプリケーションを使用してパブリッシュされます。|0 になります。サポートされていません。|  
|is_sync_tran_subscribed|**bit**|1 = テーブルは、即時更新サブスクリプションを使用してサブスクライブされます。|0 になります。サポートされていません。|  
|has_unchecked_assembly_data|**bit**|1 = テーブルに、前回の ALTER ASSEMBLY で定義が変更されたアセンブリに依存する、持続データが含まれています。 次の成功した DBCC CHECKDB または DBCC CHECKTABLE の後に 0 にリセットされます。|0 になります。CLR はサポートされません。|  
|text_in_row_limit|**int**|0 = text in row オプションは設定されていません。|常に 0 です。|  
|large_value_types_out_of_row|**bit**|1 = 大きい値の型は行外に格納されます。|常に 0 です。|  
|is_tracked_by_cdc|**bit**|1 = 変更データ キャプチャのテーブルが有効になっています。|常に 0 です。CDC はサポートされません。|  
|lock_escalation|**tinyint**|テーブルの LOCK_ESCALATION オプションの値です。2 = AUTO|常に 2 です。|  
|lock_escalation_desc|**nvarchar(60)**|Lock_escalation オプションの説明テキスト。|常に ꞌ auto ꞌ とです。|  
|pdw_node_id|**int**|一意の識別子、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]ノード。|NOT NULL|  
  
## <a name="see-also"></a>参照  
 [SQL Data Warehouse と Parallel Data Warehouse カタログ ビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
