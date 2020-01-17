---
title: log_shipping_secondary_databases (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_secondary_databases_TSQL
- log_shipping_secondary_databases
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_secondary_databases system table
ms.assetid: ba2374af-86b8-480c-a10c-51e7c4e3ae23
author: stevestein
ms.author: sstein
ms.openlocfilehash: ad6d61f4267e30c6c0b3f6cede9085cad5d39006
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095786"
---
# <a name="logshippingsecondarydatabases-transact-sql"></a>log_shipping_secondary_databases (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ログ配布構成のセカンダリ データベースごとに 1 つのレコードを格納します。 このテーブルに格納されます、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**secondary_database**|**sysname**|ログ配布構成におけるセカンダリ データベースの名前。|  
|**secondary_id**|**uniqueidentifier**|ログ配布構成におけるセカンダリ サーバーの ID。|  
|**restore_delay**|**int**|指定されたバックアップ ファイルを復元する前に、セカンダリ サーバーが待機する分単位の時間数。 既定値は、0 分です。|  
|**restore_all**|**bit**|場合は、復元ジョブの実行時に、1、セカンダリ サーバーに設定はすべてのトランザクション ログ バックアップを復元します。 それ以外の場合、1 つのファイルを復元した後を停止します。|  
|**restore_mode**|**bit**|セカンダリ データベースの復元モード。<br /><br /> 0 = NORECOVERY でログを復元します。<br /><br /> 1 = STANDBY でログを復元します。|  
|**disconnect_users**|**bit**|かどうか 1 に設定、ユーザーが切断、セカンダリ データベースから復元操作を実行します。 既定値 = 0。|  
|**block_size**|**int**|サイズ (バイト単位) をバックアップ デバイスのブロック サイズとして使用されます。|  
|**buffer_count**|**int**|バックアップまたは復元操作で使用されるバッファーの合計数。|  
|**max_transfer_size**|**int**|サイズをバイト単位の最大入力または出力要求によって発行された[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]バックアップ デバイスにします。|  
|**last_restored_file**|**nvarchar(500)**|セカンダリ データベースに復元される最後のバックアップ ファイルの名前。|  
|**last_restored_date**|**datetime**|最後の日付と時刻は、セカンダリ データベースに対する操作を復元します。|  
  
## <a name="see-also"></a>関連項目  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_secondary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [log_shipping_secondary &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-secondary-transact-sql.md)   
 [システム テーブル &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
