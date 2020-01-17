---
title: dm_server_audit_status (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 04/19/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_server_audit_status_TSQL
- sys.dm_server_audit_status
- dm_server_audit_status
- sys.dm_server_audit_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_audit_status dynamic management view
ms.assetid: 4aa32d54-2ae1-437e-bbaa-7f1df1404b44
author: stevestein
ms.author: sstein
ms.openlocfilehash: c30cbd012bb1ccc7d379eadcfd29fee87a96dd85
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313685"
---
# <a name="sysdm_server_audit_status-transact-sql"></a>dm_server_audit_status (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  監査の現在の状態を示す、サーバー監査ごとに1行の値を返します。 詳細については、「[SQL Server Audit &#40;データベース エンジン&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)」を参照してください。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**audit_id**|**int**|監査の ID。 は、**システム**カタログビューの**audit_id**フィールドにマップされます。|  
|**name**|**sysname**|監査の名前。 **Server_audits**カタログビューの**name**フィールドと同じです。|  
|**ステータス**|**smallint**|サーバー監査の状態を表す数値。<br /><br /> 0 = 未開始<br /><br /> 1 =<br />        Started<br /><br /> 2 =<br />      実行時エラー<br /><br /> 3 = ターゲットの作成失敗<br /><br /> 4 = シャットダウン中|  
|**status_desc**|**nvarchar (256)**|サーバー監査の状態を示す文字列。<br /><br /> NOT_STARTED<br /><br /> STARTED<br /><br /> RUNTIME_FAIL<br /><br /> TARGET_CREATION_FAILED<br /><br /> SHUTTING_DOWN|  
|**status_time**|**datetime2**|監査の最後の状態変更の UTC のタイムスタンプ。|  
|**event_session_address**|**varbinary(8)**|監査に関連付けられている拡張イベントセッションのアドレス。 **Dm_xe_sessions**カタログビューに関連付けられています。|  
|**audit_file_path**|**nvarchar (256)**|現在使用されている監査ファイル ターゲットの完全なパスとファイル名。 ファイル監査にのみ設定されます。|  
|**audit_file_size**|**bigint**|監査ファイルのおおよそのサイズ (バイト)。 ファイル監査にのみ設定されます。|  
  
## <a name="permissions"></a>アクセス許可  
 プリンシパルには、 **VIEW SERVER STATE**と**SELECT**権限が必要です。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
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
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [サーバー監査およびサーバー監査の仕様を作成する方法](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
