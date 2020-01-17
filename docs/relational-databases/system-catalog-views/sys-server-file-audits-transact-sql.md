---
title: sys.server_file_audits (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 04/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_file_audits_TSQL
- sys.server_file_audits_TSQL
- sys.server_file_audits
- server_file_audits
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_file_audits catalog view
ms.assetid: 553288a0-be57-4d79-ae53-b7cbd065e127
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7b3ed8e08d333c4aed2576154c645a0050ebf4df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133130"
---
# <a name="sysserverfileaudits-transact-sql"></a>sys.server_file_audits (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ファイル監査タイプに関する拡張情報を含む、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サーバー インスタンス上の監査します。 詳しくは、「[SQL Server Audit &#40;データベース エンジン&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|audit_id|**int**|監査の ID。|  
|NAME|**sysname**|監査の名前。|  
|audit_guid|**uniqueidentifier**|監査の GUID です。|  
|create_date|**datetime**|ファイル監査が作成された UTC 日付。|  
|modify_date|**datatime**|ファイル監査が最後に変更された UTC 日付。|  
|principal_id|**int**|サーバーに登録されている監査の所有者の ID。|  
|type|**char(2)**|監査の種類。<br /><br /> 0 = NT セキュリティ イベント ログ<br /><br /> 1 = NT アプリケーション イベント ログ<br /><br /> 2 = ファイル システムのファイル|  
|type_desc|**nvarchar(60)**|監査の種類の説明。|  
|on_failure|**tinyint**|失敗した場合。<br /><br /> 0 = 続行<br /><br /> 1 = サーバー インスタンスのシャットダウン<br /><br /> 2 = 失敗の操作|  
|on_failure_desc|**nvarchar(60)**|アクション エントリの書き込みに失敗します。<br /><br /> CONTINUE<br /><br /> サーバー インスタンスのシャット ダウン<br /><br /> 操作に失敗します。|  
|is_state_enabled|**tinyint**|0 = 無効<br /><br /> 1 = 有効|  
|queue_delay|**int**|ディスクに書き込む前に待機するミリ秒単位で最大の時間をお勧めします。 0 の場合は、イベントが続行する前に必ず書き込みが行われます。|  
|述語|**nvarchar(8000)**|イベントに適用される述語式。|  
|max_file_size|**bigint**|監査の最大サイズ (MB):<br /><br /> 0 = 無制限/選択した監査タイプには適用されません。|  
|max_rollover_files|**int**|ロール オーバー オプションを使用するファイルの最大数。|  
|max_files|**int**|ロール オーバー オプションを指定せずに使用するファイルの最大数。|  
|reserved_disk_space|**int**|ファイルごとに予約するディスク領域の量。|  
|log_file_path|**nvarchar(260)**|監査が配置される場所のパス。 ファイル監査、アプリケーション ログ監査のためのアプリケーション ログのパスのファイル パス。|  
|log_file_name|**nvarchar(260)**|CREATE AUDIT DDL で提供されるログ ファイルの基本名。 base_log_name ファイルにサフィックスとして連番が付加されて、ログ ファイル名が作成されます。|  
  
## <a name="permissions"></a>アクセス許可  
 持つプリンシパル、 **ALTER ANY SERVER AUDIT**または**VIEW ANY DEFINITION**このカタログ ビューにアクセス許可にアクセスします。 さらに、プリンシパル必要があります拒否されていない**VIEW ANY DEFINITION**権限。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits (TRANSACT-SQL)](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [サーバー監査およびサーバー監査の仕様を作成する](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
