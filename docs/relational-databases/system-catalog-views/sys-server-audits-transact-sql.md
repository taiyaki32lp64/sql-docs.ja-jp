---
title: sys.server_audits (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 04/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_audits_TSQL
- sys.server_audits_TSQL
- sys.server_audits
- server_audits
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_audits catalog view
ms.assetid: c2c4a000-1127-46a8-b1e9-947fd1136e1e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0a00f6843a0ef379c12aa1d1d00df9380efbd139
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125003"
---
# <a name="sysserveraudits-transact-sql"></a>sys.server_audits (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  サーバー インスタンス内の各 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 監査について行を 1 つずつ含みます。 詳しくは、「[SQL Server Audit &#40;データベース エンジン&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**audit_id**|**int**|監査の ID。|  
|**name**|**sysname**|監査の名前。|  
|**audit_guid**|**uniqueidentifier**|メンバー サーバーで監査を列挙するために使用される監査の GUID&#124;アタッチ操作の中にサーバーの開始とデータベースのデータベース監査の仕様。|  
|**create_date**|**datetime**|監査が作成された UTC 日付。|  
|**modify_date**|**datetime**|監査が最後に変更された UTC 日付。|  
|**principal_id**|**int**|サーバーに登録されている、監査の所有者の ID。|  
|**type**|**char(2)**|監査の種類。<br /><br /> SL - NT セキュリティ イベント ログ<br /><br /> AL - NT アプリケーション イベント ログ<br /><br /> FL - ファイル システム上のファイル|  
|**type_desc**|**nvarchar(60)**|SECURITY LOG<br /><br /> アプリケーション ログ<br /><br /> FILE|  
|**on_failure**|**tinyint**|アクション エントリの書き込みに失敗します。<br /><br /> 0 - 続行します。<br /><br /> 1 - サーバー インスタンスのシャット ダウン<br /><br /> 2 - 操作に失敗します。|  
|**on_failure_desc**|**nvarchar(60)**|アクション エントリの書き込みに失敗します。<br /><br /> CONTINUE<br /><br /> サーバー インスタンスのシャット ダウン<br /><br /> FAIL_OPERATION|  
|**is_state_enabled**|**tinyint**|0 - 無効<br /><br /> 1 - 有効|  
|**queue_delay**|**int**|ディスクに書き込む前に待機するミリ秒単位で最大時間。 0 の場合、監査は、イベントが続行する前に書き込みを保証します。|  
|**述語**|**nvarchar(3000)**|イベントに適用される述語式。|  
  
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
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [サーバー監査およびサーバー監査の仕様を作成する](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
