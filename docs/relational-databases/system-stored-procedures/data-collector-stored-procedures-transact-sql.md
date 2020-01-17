---
title: データ コレクター ストアド プロシージャ (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- stored procedures [SQL Server], data collector
- system stored procedures [SQL Server], data collector
- data collector [SQL Server], stored procedures
ms.assetid: 9dd2824f-ea55-439b-8cd5-3a81fedb1432
author: stevestein
ms.author: sstein
ms.openlocfilehash: 522efa96e554a7b6eecb6e36c0771cbe95163a37
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942400"
---
# <a name="data-collector-stored-procedures-transact-sql"></a>データ コレクター ストアド プロシージャ (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  SQL Server データ コレクターと、次のコンポーネントを操作するために使用する次のシステム ストアド プロシージャをサポートしています。 コレクション セット、コレクション アイテム、およびコレクション型。  
  
> [!IMPORTANT]  
>  通常のストアド プロシージャとは異なり、データ コレクターで使用するストアド プロシージャではパラメーターのデータ型が厳密に定義されており、データ型の自動変換はサポートされていません。 これらのパラメーターが、引数の説明で指定されている正しいデータ型で呼び出されないと、このストアド プロシージャではエラーが返されます。  
  
|||  
|-|-|  
|[sp_syscollector_create_collection_item](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)|[sp_syscollector_set_cache_window](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)|  
|[sp_syscollector_create_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)|[sp_syscollector_set_warehouse_database_name](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql.md)|  
|[sp_syscollector_create_collector_type](../../relational-databases/system-stored-procedures/sp-syscollector-create-collector-type-transact-sql.md)|[sp_syscollector_set_warehouse_instance_name](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql.md)|  
|[sp_syscollector_delete_collection_item](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql.md)|[sp_syscollector_start_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-start-collection-set-transact-sql.md)|  
|[sp_syscollector_delete_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-set-transact-sql.md)|[sp_syscollector_stop_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md)|  
|[sp_syscollector_delete_collector_type](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collector-type-transact-sql.md)|[sp_syscollector_run_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql.md)|  
|[sp_syscollector_delete_execution_log_tree](../../relational-databases/system-stored-procedures/sp-syscollector-delete-execution-log-tree-transact-sql.md)|[sp_syscollector_update_collection_item](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql.md)|  
|[sp_syscollector_disable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)|[sp_syscollector_update_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-set-transact-sql.md)|  
|[sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)|[sp_syscollector_update_collector_type](../../relational-databases/system-stored-procedures/sp-syscollector-update-collector-type-transact-sql.md)|  
|[sp_syscollector_set_cache_directory](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql.md)|[sp_syscollector_upload_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-upload-collection-set-transact-sql.md)|  
  
 次のストアド プロシージャは内部でのみ使用されます。  
  
-   sp_syscollector_get_warehouse_connection_string  
  
-   sp_syscollector_set_warehouse_connection_password  
  
-   sp_syscollector_set_warehouse_connection_user  
  
-   sp_syscollector_event_oncollectionbegin  
  
-   sp_syscollector_event_oncollectionend  
  
-   sp_syscollector_event_onpackagebegin  
  
-   sp_syscollector_event_onpackageend  
  
-   sp_syscollector_event_onpackageupdate  
  
-   sp_syscollector_event_onerror  
  
-   sp_syscollector_event_onstatsupdate  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
