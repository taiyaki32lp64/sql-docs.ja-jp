---
title: sys.server_principals (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_principals
- sys.server_principals_TSQL
- sys.server_principals
- server_principals_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_principals catalog view
ms.assetid: c5dbe0d8-a1c8-4dc4-b9b1-22af20effd37
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 408ad309ade858c800b79ee83993fda4fe78467a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133075"
---
# <a name="sysserverprincipals-transact-sql"></a>sys.server_principals (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  サーバー レベルのプリンシパルごとに 1 行のデータを格納します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|プリンシパルの名前。 サーバー内で一意です。|  
|**principal_id**|**int**|プリンシパルの ID 番号。 サーバー内で一意です。|  
|**sid**|**varbinary(85)**|プリンシパルの SID (セキュリティ識別子)。 Windows プリンシパルの場合、これは Windows SID に一致します。|  
|**type**|**char(1)**|プリンシパルの種類。<br /><br /> S = SQL ログイン<br /><br /> U = Windows ログイン<br /><br /> G = Windows グループ<br /><br /> R = サーバーの役割<br /><br /> C = 証明書にマップされるログイン<br /><br /> K = 非対称キーにマップされるログイン|  
|**type_desc**|**nvarchar(60)**|プリンシパルの種類の説明です。<br /><br /> SQL_LOGIN<br /><br /> WINDOWS_LOGIN<br /><br /> WINDOWS_GROUP<br /><br /> SERVER_ROLE<br /><br /> CERTIFICATE_MAPPED_LOGIN<br /><br /> ASYMMETRIC_KEY_MAPPED_LOGIN|  
|**is_disabled**|**int**|1 = ログインは無効です。|  
|**create_date**|**datetime**|プリンシパルが作成された日時。|  
|**modify_date**|**datetime**|プリンシパルの定義が最後に変更された時刻。|  
|**default_database_name**|**sysname**|プリンシパルの既定のデータベース。|  
|**default_language_name**|**sysname**|このプリンシパルの既定の言語。|  
|**credential_id**|**int**|このプリンシパルに関連付けられている資格情報の ID。 このプリンシパルに関連付けられている資格情報がない場合、credential_id は NULL になります。|  
|**owning_principal_id**|**int**|**Principal_id**サーバー ロールの所有者のです。 プリンシパル サーバーの役割でない場合は NULL です。|  
|**is_fixed_role**|**bit**|プリンシパルが固定のアクセス許可を持つ組み込みのサーバー ロールのいずれかの場合は、1 を返します。 詳細については、「 [サーバー レベルのロール](../../relational-databases/security/authentication-access/server-level-roles.md)」を参照してください。|  
  
## <a name="permissions"></a>アクセス許可  
 すべてのログインは自分のログイン名、システム ログイン、および固定サーバー ロールを参照できます。 他のログインを参照するには、ALTER ANY LOGIN、またはログインに対する権限が必要です。 ユーザー定義サーバー ロールを参照する ALTER ANY SERVER ROLE をまたはロールのメンバーシップが必要です。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次のクエリは、明示的に付与または拒否サーバー プリンシパル アクセス許可を一覧表示します。  
  
> [!IMPORTANT]  
>  (パブリック) 以外の固定サーバー ロールのアクセス許可は、sys.server_permissions には表示されません。 そのため、サーバー プリンシパルには、この一覧にない追加のアクセス許可があります。  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pe.state_desc, pe.permission_name   
FROM sys.server_principals AS pr   
JOIN sys.server_permissions AS pe   
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [権限の階層 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
  
  
