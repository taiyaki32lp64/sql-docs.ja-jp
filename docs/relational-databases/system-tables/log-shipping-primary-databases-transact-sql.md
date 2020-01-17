---
title: log_shipping_primary_databases (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_primary_databases
- log_shipping_primary_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_primary_databases system table
ms.assetid: 56888756-a798-42be-9b5e-0f9aa05a2cc6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9c1dfefbc309e9ccc0f170461795c00a117247e2
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304987"
---
# <a name="log_shipping_primary_databases-transact-sql"></a>log_shipping_primary_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  では、プライマリデータベースの1つのレコードがログ配布構成に格納されます。 このテーブルは、 **msdb**データベースに格納されます。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|ログ配布構成のプライマリデータベースの ID。|  
|**primary_database**|**sysname**|ログ配布構成のプライマリデータベースの名前。|  
|**backup_directory**|**nvarchar(500)**|プライマリサーバーからのトランザクションログバックアップファイルが格納されているディレクトリ。|  
|**backup_share**|**nvarchar(500)**|バックアップディレクトリへのネットワークまたは UNC パス。|  
|**backup_retention_period**|**int**|バックアップ ディレクトリでログ バックアップ ファイルが保持される時間 (分単位)。この時間を過ぎるとファイルは削除されます。|  
|**backup_job_id**|**uniqueidentifier**|プライマリサーバー上のバックアップジョブに関連付けられている [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントジョブ ID。|  
|**monitor_server**|**sysname**|ログ配布構成で監視サーバーとして使用されて [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] のインスタンスの名前です。|  
|**monitor_server_security_mode**|**bit**|監視サーバーへの接続に使用されるセキュリティモード。<br /><br /> 1 = Windows 認証。<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証。|  
|**last_backup_file**|**nvarchar(500)**|最新のトランザクションログバックアップの絶対パス。|  
|**last_backup_date**|**datetime**|最後のログ バックアップ操作の日時。|  
|**user_specified_monitor**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **sp_help_log_shipping_primary_database**および**sp_help_log_shipping_secondary_primary**この列を使用して [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のモニター設定の表示を制御します。<br /><br /> 0 = この2つのストアドプロシージャのいずれかを呼び出すときに、ユーザーは **\@monitor_server**パラメーターに明示的な値を指定しませんでした。<br /><br /> 1 = ユーザーが明示的な値を指定しました。|  
|**backup_compression**|**tinyint**|ログ配布構成がサーバーレベルのバックアップ圧縮動作を上書きするかどうかを示します。<br /><br /> 0 = 無効です。 サーバーで構成されたバックアップ圧縮設定に関係なく、ログバックアップは圧縮されません。<br /><br /> 1 = 有効。 サーバーで構成されたバックアップ圧縮設定に関係なく、ログバックアップは常に圧縮されます。<br /><br /> 2 = サーバー構成を使用して、[ビューまたは、backup compression Default サーバー構成オプション](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)のサーバー構成オプションを構成します。 これが既定値です。<br /><br /> バックアップの圧縮は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の Enterprise エディションでのみサポートされています。|  
  
## <a name="see-also"></a>参照  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [transact-sql &#40;  の&#41; sp_add_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_delete_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)  
 [sp_help_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [システム テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
