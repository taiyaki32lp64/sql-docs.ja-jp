---
title: sys.database_role_members (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_role_members_TSQL
- sys.database_role_members
- database_role_members_TSQL
- database_role_members
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_role_members catalog view
ms.assetid: ed1b019d-ca48-4db3-85df-cf6d2db591cf
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1bbbcf04cdb141cff25565360d82714eed1e98f1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079474"
---
# <a name="sysdatabaserolemembers-transact-sql"></a>sys.database_role_members (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  データベース ロールのメンバーごとに 1 行のデータを返します。  データベース ユーザー、アプリケーション ロール、およびその他のデータベース ロールは、データベース ロールのメンバーであることができます。 ロールにメンバーを追加するには、使用、 [ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md)ステートメントを`ADD MEMBER`オプション。 結合[sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)の名前を返す、`principal_id`値。
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**role_principal_id**|**int**|データベース ロールのプリンシパルの ID。|  
|**member_principal_id**|**int**|メンバーのデータベース プリンシパルの ID。|  
  
## <a name="permissions"></a>アクセス許可  
 すべてのユーザーは自分のロールのメンバーシップを参照できます。 メンバーシップを他のロールを表示するにはメンバーシップが必要です、`db_securityadmin`固定データベース ロールまたは`VIEW DEFINITION`データベースでします。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のクエリでは、データベース ロールのメンバーを返します。  
  
```  
SELECT DP1.name AS DatabaseRoleName,   
   isnull (DP2.name, 'No members') AS DatabaseUserName   
 FROM sys.database_role_members AS DRM  
 RIGHT OUTER JOIN sys.database_principals AS DP1  
   ON DRM.role_principal_id = DP1.principal_id  
 LEFT OUTER JOIN sys.database_principals AS DP2  
   ON DRM.member_principal_id = DP2.principal_id  
WHERE DP1.type = 'R'
ORDER BY DP1.name;  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
[ALTER ROLE (Transact SQLL)](../../t-sql/statements/alter-role-transact-sql.md)      
[sys.server_role_members (TRANSACT-SQL)](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)   
  


