---
title: user_token (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.user_token
- user_token
- sys.user_token_TSQL
- user_token_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], security tokens
- sys.user_token catalog view
- user tokens [SQL Server]
- tokens [SQL Server]
- user_token catalog view
ms.assetid: be018103-5e57-43a4-9160-9bf420892aa7
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions|| = azure-sqldw-latest
ms.openlocfilehash: 9b3e389b97cee8a8a6d548eb93ad70b94d09ba40
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160739"
---
# <a name="sysuser_token-transact-sql"></a>user_token (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md.md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のユーザートークンの一部であるデータベースプリンシパルごとに1行のデータを返します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**principal_id**|**int**|プリンシパルの ID です。 値はデータベース内で一意です。|  
|**sid**|**varbinary(85)**|プリンシパルがデータベースの外部で定義されている場合のプリンシパルのセキュリティ識別子。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン、Windows ログイン、Windows グループ ログイン、証明書にマップされるログインなどです。それ以外の場合、この値は NULL になります。|  
|**name**|**nvarchar (128)**|プリンシパルの名前。 値はデータベース内で一意です。|  
|**型**|**nvarchar (128)**|プリンシパルの種類の説明。 すべての型が**sid**にマップされます。 値は次のいずれかになります。<br /><br /> SQL USER<br /><br /> WINDOWS ログイン<br /><br /> WINDOWS GROUP<br /><br /> ROLE<br /><br /> APPLICATION ROLE<br /><br /> DATABASE ROLE<br /><br /> USER MAPPED TO CERTIFICATE<br /><br /> 非対称キーにマップされたユーザー<br /><br /> CERTIFICATE<br /><br /> ASYMMETRIC KEY|  
|**ユーセジリンク**|**nvarchar (128)**|GRANT または DENY 権限の評価にプリンシパルが参加するかどうか、または認証子としての役割を果たすかどうかを示します。<br /><br /> この値には、次のいずれかを指定できます。<br /><br /> GRANT または DENY<br /><br /> 拒否のみ<br /><br /> アプリ|  
  
## <a name="see-also"></a>参照  
 [login_token &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-login-token-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
