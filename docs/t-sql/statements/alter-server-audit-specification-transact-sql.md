---
title: ALTER SERVER AUDIT SPECIFICATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER SERVER AUDIT SPECIFICATION
- ALTER_SERVER_AUDIT_SPECIFICATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server audit [SQL Server]
- audits [SQL Server], specification
- ALTER SERVER AUDIT SPECIFICATION statement
ms.assetid: 9cac288b-940e-4c16-88d6-de06aeed2b47
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7bc8d1e1a84ddacbffe5b830e1b5931eb94a5f14
ms.sourcegitcommit: a97d551b252b76a33606348082068ebd6f2c4c8c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70745330"
---
# <a name="alter-server-audit-specification-transact-sql"></a>ALTER SERVER AUDIT SPECIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit 機能を使用して、サーバー監査仕様オブジェクトを変更します。 詳しくは、「[SQL Server Audit &#40;データベース エンジン&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
ALTER SERVER AUDIT SPECIFICATION audit_specification_name  
{  
    [ FOR SERVER AUDIT audit_name ]  
    [ { { ADD | DROP } ( audit_action_group_name )  
      } [, ...n] ]  
    [ WITH ( STATE = { ON | OFF } ) ]  
}  
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *audit_specification_name*  
 監査仕様の名前。  
  
 *audit_name*  
 この仕様が適用される監査の名前。  
  
 *audit_action_group_name*  
 サーバーレベルの監査可能なアクションのグループの名前。 監査アクション グループの一覧については、「[SQL Server 監査のアクション グループとアクション](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)」をご覧ください。  
  
 WITH **(** STATE **=** { ON | OFF } **)**  
 監査による、この監査仕様についてのレコードの収集を有効または無効にします。  
  
## <a name="remarks"></a>Remarks  
 監査仕様を変更する場合は、監査仕様の状態のオプションを OFF に設定する必要があります。 STATE=OFF 以外のオプションを使用して監査仕様を有効にしているときに ALTER SERVER AUDIT SPECIFICATION を実行すると、エラー メッセージが表示されます。  
  
## <a name="permissions"></a>アクセス許可  
 ALTER ANY SERVER AUDIT 権限を持つユーザーは、サーバー監査仕様を変更し、任意の監査にバインドできます。  
  
 サーバー監査仕様の作成後は、CONTROL SERVER または ALTER ANY SERVER AUDIT 権限を持つプリンシパル、sysadmin アカウント、またはその監査への明示的なアクセス権を持つプリンシパルによってその仕様を表示できます。  
  
## <a name="examples"></a>使用例  
 次の例では、`HIPAA_Audit_Specification` というサーバー監査仕様を作成します。 `HIPAA_Audit` という [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 監査に対して、失敗したログインの監査アクション グループを削除し、データベース オブジェクト アクセスの監査アクション グループを追加します。  
  
```  
ALTER SERVER AUDIT SPECIFICATION HIPAA_Audit_Specification  
FOR SERVER AUDIT HIPAA_Audit  
    DROP (FAILED_LOGIN_GROUP)  
    ADD (DATABASE_OBJECT_ACCESS_GROUP);  
GO  
```  
  
 監査を作成する方法の完全な例については、「[SQL Server Audit &#40;データベース エンジン&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)」をご覧ください。  
  

## <a name="see-also"></a>参照  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
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
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [サーバー監査およびサーバー監査の仕様を作成する](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
