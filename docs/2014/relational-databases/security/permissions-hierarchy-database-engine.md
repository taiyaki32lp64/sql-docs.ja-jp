---
title: 権限の階層 (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.server.permissions.f1--May use common.permissions
helpviewer_keywords:
- security [SQL Server], denying access
- hierarchies [SQL Server], permissions
- securables [SQL Server]
- security [SQL Server], permissions
- permissions [SQL Server], hierarchy
- security [SQL Server], granting access
ms.assetid: f6d20a55-ef03-4e14-85f9-009902889866
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 05cc0d47053d8ddef0962c4aceee75e61b8b4b64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211954"
---
# <a name="permissions-hierarchy-database-engine"></a>権限の階層 (データベース エンジン)
  [!INCLUDE[ssDE](../../../includes/ssde-md.md)] では、権限を使用してセキュリティで保護できるエンティティの階層コレクションが管理されています。 これらのエンティティを、 *セキュリティ保護可能なリソース*と呼びます。 最も顕著なセキュリティ保護可能なリソースはサーバーとデータベースですが、さらに細かいレベルで個別の権限を設定できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 適切な権限が許可されていることを確認することにより、セキュリティ保護可能なリソースに対するプリンシパルによる操作を制御しています。  
  
 次の図は、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] の権限階層における関係を示します。  
  
 ![データベース エンジンの権限階層の図](../../database-engine/media/wj-security-layers.gif "データベース エンジンの権限階層の図")  
  
## <a name="chart-of-sql-server-permissions"></a>SQL Server 権限の一覧表  
 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] のすべてのアクセス許可を示した pdf 形式のポスター サイズの一覧表については、[https://go.microsoft.com/fwlink/?LinkId=229142](https://go.microsoft.com/fwlink/?LinkId=229142) を参照してください。  
  
## <a name="working-with-permissions"></a>権限を使用した作業  
 権限は、使い慣れた [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリ (RANT、DENY、REVOKE) で操作できます。 権限に関する情報は、 [sys.server_permissions](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) カタログ ビューおよび [sys.database_permissions](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) カタログ ビューに表示されます。 組み込み関数を使用して権限に関する情報をクエリすることもできます。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server の保護](securing-sql-server.md)   
 [アクセス許可 &#40;データベース エンジン&#41;](permissions-database-engine.md)   
 [Securables](securables.md)   
 [プリンシパル &#40;データベース エンジン&#41;](authentication-access/principals-database-engine.md)   
 [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)   
 [REVOKE &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql)   
 [DENY &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-transact-sql)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/has-perms-by-name-transact-sql)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql)   
 [sys.server_permissions &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql)   
 [sys.database_permissions &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql)  
  
  
