---
title: sys.dm_audit_actions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_audit_actions_TSQL
- sys.dm_audit_actions
- dm_audit_actions_TSQL
- dm_audit_actions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_audit_actions dynamic management view
ms.assetid: b987c2b9-998a-4a5f-a82d-280dc6963cbe
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5e6a6c91cb31c9c3036bc95239f0aff9c75fda7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936977"
---
# <a name="sysdmauditactions-transact-sql"></a>sys.dm_audit_actions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  監査ログで報告される可能性のあるすべての監査アクション、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit の一部として構成できるすべての監査アクション グループに対して 1 つの行を返します。 詳細については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]監査を参照してください[SQL Server Audit&#40;データベース エンジン&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**action_id**|**varchar (4)**|監査アクションの ID。 関連する、 **action_id**各監査レコードに書き込まれた値。 NULL 値が許可されます。 監査グループの場合は NULL です。|  
|**action_in_log**|**bit**|アクションを監査ログに書き込めるかどうかを示します。 値は次のとおりです。<br /><br /> 1 = はい<br /><br /> 0 = いいえ|  
|**name**|**sysname**|監査アクションまたはアクション グループの名前。 NULL 値は許可されません。|  
|**class_desc**|**nvarchar(120)**|監査アクションが適用されるオブジェクトのクラス名。 サーバー、データベース、またはスキーマ スコープのいずれかのオブジェクトがスキーマ オブジェクトは含まれませんを指定できます。 NULL 値は許可されません。|  
|**parent_class_desc**|**nvarchar(120)**|class_desc で記述されるオブジェクトの親クラスの名前。 Class_desc がサーバーである場合は NULL です。|  
|**covering_parent_action_name**|**nvarchar(120)**|この行で記述される監査アクションを含む、監査アクションまたは監査グループの名前。 これは、アクションと包含アクションの階層を作成に使用されます。 NULL 値が許可されます。|  
|**configuration_level**|**nvarchar(10)**|アクションまたはこの行で指定したアクション グループがグループまたはアクション レベルで構成可能でことを示します。 アクションは構成可能な場合は NULL です。|  
|**containing_group_name**|**nvarchar(120)**|指定したアクションを含む監査グループの名前。 名前の値がグループの場合は NULL です。|  
  
## <a name="permissions"></a>アクセス許可  
 プリンシパルが必要**選択**権限。 既定では、これは Public に付与されています。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
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
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [サーバー監査およびサーバー監査の仕様を作成する](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
