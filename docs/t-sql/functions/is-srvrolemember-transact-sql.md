---
title: IS_SRVROLEMEMBER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IS_SRVROLEMEMBER_TSQL
- IS_SRVROLEMEMBER
dev_langs:
- TSQL
helpviewer_keywords:
- roles [SQL Server], members
- IS_SRVROLEMEMBER function
- members [SQL Server], verifying
ms.assetid: 3241a44a-6958-415b-b8b7-2a1207c36ab3
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 478641bed0931fc78db3c7df166b860374034f90
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983260"
---
# <a name="is_srvrolemember-transact-sql"></a>IS_SRVROLEMEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインが、指定したサーバー ロールのメンバーであるかどうかを示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
IS_SRVROLEMEMBER ( 'role' [ , 'login' ] )  
```  
  
## <a name="arguments"></a>引数  
 **'** *role* **'**  
 確認するサーバー ロールの名前です。 *role* は **sysname**です。  
  
 *role* の有効な値は、ユーザー定義サーバー ロールと、次の固定サーバー ロールです。  
  
|||  
|-|-|  
|sysadmin|serveradmin|  
|dbcreator|setupadmin|  
|bulkadmin|securityadmin|  
|diskadmin|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> public|  
|processadmin||  
  
 **'** *login* **'**  
 確認する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの名前です。 *login* のデータ型は **sysname** で、既定値は NULL です。 値を指定しない場合、結果は現在の実行コンテキストに基づきます。 パラメーターに "NULL" という語が含まれていると、NULL が返されます。  
  
## <a name="return-types"></a>戻り値の型  
 **int**  
  
|戻り値|[説明]|  
|------------------|-----------------|  
|0|*login* は *role* のメンバーではありません。<br /><br /> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、このステートメントは常に 0 を返します。|  
|1|*login* は *role* のメンバーです。|  
|NULL|*role* または *login* が有効でないか、ロールのメンバーシップを表示する権限がありません。|  
  
## <a name="remarks"></a>Remarks  
 現在のユーザーがサーバー ロールの権限を必要とするアクションを実行できるかどうかを判断するには IS_SRVROLEMEMBER を使用します。  
  
 Contoso\Mary5 などの Windows ログインを *login* に指定した場合、**IS_SRVROLEMEMBER** は、そのログインに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への直接アクセスが許可または拒否されている場合を除き、**NULL** を返します。  
  
 省略可能な *login* パラメーターを指定しない場合、*login* が Windows ドメインのログインであると、そのログインは、Windows グループのメンバーシップを通じて、固定サーバー ロールのメンバーになっている可能性があります。 そのような間接的なメンバーシップを解決するために、IS_SRVROLEMEMBER は、Windows グループのメンバーシップ情報をドメイン コントローラーに要求します。 ドメイン コントローラーにアクセスできないか、またはドメイン コントローラーが応答しない場合、**IS_SRVROLEMEMBER** はユーザーとそのローカル グループのみを考慮したロール メンバーシップ情報を返します。 指定されたユーザーが現在のユーザーでない場合、IS_SRVROLEMEMBER が返す値は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に対する認証システム (Active Directory など) の最後のデータ更新と異なることがあります。  
  
 省略可能な login パラメーターを指定する場合は、クエリの対象となる Windows ログインが sys.server_principals に存在する必要があります。存在しない場合、IS_SRVROLEMEMBER は NULL を返します。 これは、そのログインが無効であることを示します。  
  
 login パラメーターがドメイン ログインか、Windows グループに基づくログインである場合、ドメイン コントローラーにアクセスできないと、IS_SRVROLEMEMBER の呼び出しが失敗し、不正確なデータや不完全なデータが返される可能性があります。  
  
 ドメイン コントローラーを利用できなくても、Windows プリンシパルをローカルで認証できる場合 (ローカル Windows アカウントや [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの場合など) は、IS_SRVROLEMEMBER の呼び出しで正確な情報が返されます。  
  
 Windows グループがログイン引数として使用されていて、この Windows グループが別の Windows グループのメンバーであり、さらにそのグループが指定されたサーバー ロールのメンバーである場合、**IS_SRVROLEMEMBER** は常に 0 を返します。  
  
 ユーザー アカウント制御 (UAC) の設定では、異なる結果が返されることもあります。 これは、ユーザーがサーバーに Windows グループのメンバーとしてアクセスしたか、特定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーとしてアクセスしたかによります。  
  
 この関数で評価されるのはロールのメンバーシップであって、基になる権限ではありません。 たとえば、**sysadmin** 固定サーバー ロールには **CONTROL SERVER** 権限があります。 **CONTROL SERVER** 権限を持っていても、**sysadmin** ロールに所属していなければ、そのユーザーはロールのメンバーではないと、この関数によって正確に報告されます。そのロールと同じ権限をユーザーが持っているとしても結果は変わりません。  
  
## <a name="related-functions"></a>関連する関数  
 現在のユーザーが指定された Windows グループまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ロールのメンバーであるかどうかを判断するには、[IS_MEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-member-transact-sql.md) を使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインがデータベース ロールのメンバーであるかどうかを判断するには、[IS_ROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-rolemember-transact-sql.md) を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 サーバー ロールに対する VIEW DEFINITION 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、現在のユーザーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインが固定サーバー ロール `sysadmin` のメンバーであるかどうかを示しています。  
  
```  
IF IS_SRVROLEMEMBER ('sysadmin') = 1  
   print 'Current user''s login is a member of the sysadmin role'  
ELSE IF IS_SRVROLEMEMBER ('sysadmin') = 0  
   print 'Current user''s login is NOT a member of the sysadmin role'  
ELSE IF IS_SRVROLEMEMBER ('sysadmin') IS NULL  
   print 'ERROR: The server role specified is not valid.';  
```  
  
 次の例では、ドメイン ログイン Pat が固定サーバー ロール **diskadmin** のメンバーであるかどうかを示します。  
  
```  
SELECT IS_SRVROLEMEMBER('diskadmin', 'Contoso\Pat');  
```  
  
## <a name="see-also"></a>参照  
 [IS_MEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [セキュリティ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
