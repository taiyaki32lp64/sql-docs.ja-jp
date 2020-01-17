---
title: システム ビュー、ストアド プロシージャ、Dmv の待機の種類、インメモリ OLTP の |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: efaa59e3-dbfa-407f-b1aa-cb0c6602ea17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d047cbc4fe3ba3f4945acd9da4f627a05992e779
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62842401"
---
# <a name="system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp"></a>インメモリ OLTP 向けのシステム ビュー、ストアド プロシージャ、DMV、待機の種類
  このトピックでは、簡単な説明を行い、インメモリ OLTP をサポートする多くのデータベース オブジェクトへのリンクを提供します。  
  
### <a name="system-views"></a>システム ビュー  
  
|システム ビュー|説明|インメモリ OLTP の機能|  
|-----------------|-----------------|-----------------------------|  
|[sys.data_spaces &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-data-spaces-transact-sql)|ファイル グループにメモリ最適化データが含まれているかどうか確認します。|次の列が追加の値を表示:**型**と**type_desc**します。|  
|[sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)|メモリ最適化テーブルにインデックスが付けられているか確認します。|次の列が追加の値を表示:**型**と**type_desc**します。|  
|[sys.parameters &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-parameters-transact-sql)|(ネイティブ コンパイル ストアド プロシージャのより効率的に実行) の not null の値を許容するパラメーターを確認します。|**によって is_nullable**列。|  
|[sys.all_sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-all-sql-modules-transact-sql)|ストアド プロシージャをネイティブにコンパイルされているかどうかを確認します。|**uses_native_compilation**列。|  
|[sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)|ストアド プロシージャをネイティブにコンパイルされているかどうかを確認します。|**uses_native_compilation**列。|  
|[sys.table_types &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-table-types-transact-sql)|テーブルがメモリ最適化されているか確認します。|**is_memory_optimized**列。|  
|[sys.tables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql)|テーブルがメモリ最適化テーブルの持続性の設定を確認する場合を確認します。|**持続性**、 **durability_desc**、および**is_memory_optimized**列。|  
|[sys.hash_indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-hash-indexes-transact-sql)|メモリ最適化テーブルのハッシュ インデックスを表示します。|インメモリ OLTP 固有|  
  
### <a name="metadata-functions"></a>メタデータ関数  
  
|メタデータ関数|説明|インメモリ OLTP の機能|  
|-----------------------|-----------------|-----------------------------|  
|[OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)|データベース オブジェクトがメモリ最適化されているか確認します。|**ExecIsWithNativeCompilation**と**TableIsMemoryOptimized**プロパティ。<br /><br /> **IsSchemaBound**プロパティ (NULL の代わりにプロシージャの場合は 0 を返します) プロシージャ オブジェクトの種類をサポートしています。|  
|[SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)|サーバーがインメモリ OLTP をサポートしているか確認します。|**IsXTPSupported**プロパティ。|  
  
### <a name="system-stored-procedures"></a>システム ストアド プロシージャ  
  
|ストアド プロシージャ|説明|  
|----------------------|-----------------|  
|[sys.sp_xtp_bind_db_resource_pool &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql)|インメモリ OLTP データベースをリソース プールにバインドします。|  
|[sys.sp_xtp_checkpoint_force_garbage_collection &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-checkpoint-force-garbage-collection-transact-sql)|インメモリ OLTP データベースのガベージ コレクションを開始します。|  
|[sys.sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql)|ネイティブ コンパイル ストアド プロシージャの統計コレクションを有効にします。|  
|[sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql)|ネイティブ コンパイル ストアド プロシージャのクエリ統計コレクションごとに有効にします。|  
|[sys.sp_xtp_merge_checkpoint_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql)|データとデルタ ファイルをマージします。|  
|[sys.sp_xtp_unbind_db_resource_pool &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql)|データベースとリソース プールの間のバインドを削除します。|  
  
## <a name="dynamic-management-views-dmvs"></a>動的管理ビュー (DMV)  
 メモリ最適化テーブルにはいくつかの DMV があります。  
  
 詳細については、次を参照してください。[メモリ最適化テーブルの動的管理ビュー &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql)します。  
  
## <a name="wait-types"></a>待機の種類  
 インメモリ OLTP をサポートする待機の種類がいくつかあります。  
  
 詳細については、次を参照してください。 待機の種類が付いている**WAIT_XTP**、および**XTPPROC**で、 [sys.dm_os_wait_stats &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql)トピック。  
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)   
 [Transact-SQL によるインメモリ OLTP のサポート](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  
  
