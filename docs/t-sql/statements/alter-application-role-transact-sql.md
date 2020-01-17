---
title: ALTER APPLICATION ROLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_APPLICATION_ROLE_TSQL
- ALTER APPLICATION ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- modifying application roles
- passwords [SQL Server], application roles
- ALTER APPLICATION ROLE statement
- application roles [SQL Server], modifying
ms.assetid: c6cd5d0f-18f4-49be-b161-64d9c5569086
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7d39f716717fe517fb3274e4c5519606916afb7b
ms.sourcegitcommit: e9c1527281f2f3c7c68981a1be94fe587ae49ee9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73064672"
---
# <a name="alter-application-role-transact-sql"></a>ALTER APPLICATION ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  アプリケーション ロールの名前、パスワード、または既定のスキーマを変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
ALTER APPLICATION ROLE application_role_name   
    WITH <set_item> [ ,...n ]  
  
<set_item> ::=   
    NAME = new_application_role_name   
    | PASSWORD = 'password'  
    | DEFAULT_SCHEMA = schema_name  
```  
  
## <a name="arguments"></a>引数  
 *application_role_name*  
 変更するアプリケーション ロールの名前です。  
  
 NAME =*new_application_role_name*  
 アプリケーション ロールの新しい名前を指定します。 この名前は、データベース内のどのプリンシパルへの参照にも使用されていない名前である必要があります。  
  
 PASSWORD ='*password*'  
 アプリケーション ロールのパスワードを指定します。 *password* は、Windows のパスワード ポリシーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを実行するコンピューターに要求する条件を満足する必要があります。 複雑なパスワードの使用をお勧めします。  
  
 DEFAULT_SCHEMA =*schema_name*  
 オブジェクトの名前を解決するときに、サーバーで最初に検索されるスキーマを指定します。 *schema_name* にはデータベースに存在しないスキーマを指定できます。  
  
## <a name="remarks"></a>Remarks  
 新しいアプリケーション ロールの名前が既にデータベースに存在する場合、このステートメントは失敗します。 アプリケーション ロールの名前、パスワード、または既定のスキーマが変更されても、そのロールに関連付けられている ID は変更されません。  
  
> [!IMPORTANT]  
>  パスワードの有効期限ポリシーは、アプリケーション ロールのパスワードには適用されません。 このため、複雑なパスワードを選択する際には十分注意してください。 アプリケーション ロールを呼び出すアプリケーションは、これらのパスワードを格納する必要があります。  
  
 アプリケーション ロールは、sys.database_principals カタログ ビューで参照できます。  
  
> [!CAUTION]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] でのスキーマの動作は、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から変更されました。 コードで、スキーマがデータベース ユーザーと同じであることが前提となっている場合、正しい結果が返されない場合があります。 以下の DDL ステートメントが使用されているデータベースでは、sysobjects などの古いカタログ ビューを使用してはいけません:CREATE SCHEMA、ALTER SCHEMA、DROP SCHEMA、CREATE USER、ALTER USER、DROP USER、CREATE ROLE、ALTER ROLE、DROP ROLE、CREATE APPROLE、ALTER APPROLE、DROP APPROLE、ALTER AUTHORIZATION。 これらのいずれかのステートメントが使用されたデータベースでは、新しいカタログ ビューを使用する必要があります。 新しいカタログ ビューでは、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] で導入されたプリンシパルとスキーマの分離が考慮されます。 カタログ ビューの詳細については、「[カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する ALTER ANY APPLICATION ROLE 権限が必要です。 既定のスキーマを変更するには、アプリケーション ロールに対する ALTER 権限も必要です。 アプリケーション ロールは、それ自体の既定のスキーマを変更できますが、名前とパスワードは変更できません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-changing-the-name-of-application-role"></a>A. アプリケーション ロールの名前を変更する  
 次の例では、アプリケーション ロール `weekly_receipts` の名前を `receipts_ledger` に変更します。  
  
```sql  
USE AdventureWorks2012;  
CREATE APPLICATION ROLE weekly_receipts   
    WITH PASSWORD = '987Gbv8$76sPYY5m23' ,   
    DEFAULT_SCHEMA = Sales;  
GO  
ALTER APPLICATION ROLE weekly_receipts   
    WITH NAME = receipts_ledger;  
GO  
```  
  
### <a name="b-changing-the-password-of-application-role"></a>B. アプリケーション ロールのパスワードを変更する  
 次の例では、アプリケーション ロール `receipts_ledger` のパスワードを変更します。  
  
```sql  
ALTER APPLICATION ROLE receipts_ledger   
    WITH PASSWORD = '897yUUbv867y$200nk2i';  
GO  
```  
  
### <a name="c-changing-the-name-password-and-default-schema"></a>C. 名前、パスワード、および既定のスキーマを変更する  
 次の例では、アプリケーション ロール `receipts_ledger` の名前、パスワード、および既定のスキーマをすべて同時に変更します。  
  
```sql  
ALTER APPLICATION ROLE receipts_ledger   
    WITH NAME = weekly_ledger,   
    PASSWORD = '897yUUbv77bsrEE00nk2i',   
    DEFAULT_SCHEMA = Production;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [アプリケーション ロール](../../relational-databases/security/authentication-access/application-roles.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
