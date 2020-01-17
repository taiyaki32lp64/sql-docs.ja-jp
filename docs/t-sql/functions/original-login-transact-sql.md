---
title: ORIGINAL_LOGIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ORIGINAL_LOGIN_TSQL
- ORIGINAL_LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], context switches
- context switching [SQL Server], login names
- original login names [SQL Server]
- ORIGINAL_LOGIN function
- names [SQL Server], logins
ms.assetid: ddfb0991-cde3-4b97-a5b7-ee450133f160
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ff9f53c6dd3e0029f2627545c7654ded3219abbe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67914532"
---
# <a name="originallogin-transact-sql"></a>ORIGINAL_LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続しているログインの名前を返します。 この関数を使用すると、明示的または暗黙的にコンテキストが何度も切り替えられるセッションにおける、元のログインの ID を取得できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
ORIGINAL_LOGIN( )  
```  
  
## <a name="return-types"></a>戻り値の型  
 **sysname**  
  
## <a name="remarks"></a>Remarks  
 この関数は、元の接続コンテキストの ID を監査するときに便利です。 [SESSION_USER](../../t-sql/functions/session-user-transact-sql.md) や [CURRENT_USER](../../t-sql/functions/current-user-transact-sql.md) などの関数では、現在実行しているコンテキストが返されるのに対し、ORIGINAL_LOGIN では、そのセッションで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに最初に接続したログインの ID が返されます。  
 
  
## <a name="examples"></a>使用例  
 次の例では、現在のセッションの実行コンテキストを、ステートメントの呼び出し元のログインから `login1` に切り替えます。 関数 `SUSER_SNAME` および `ORIGINAL_LOGIN` を使用すると、現在のセッションのユーザー (コンテキストの切り替え先のユーザー) と、元のログイン アカウントが返されます。 
 
  >[!NOTE]
  > Azure SQL Database では ORIGINAL_LOGIN 関数がサポートされますが、*Execute as LOGIN* がサポートされないため、次のスクリプトは失敗します。 
  
```  
USE AdventureWorks2012;  
GO  
--Create a temporary login and user.  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE USER user1 FOR LOGIN login1;  
GO  
--Execute a context switch to the temporary login account.  
DECLARE @original_login sysname;  
DECLARE @current_context sysname;  
EXECUTE AS LOGIN = 'login1';  
SET @original_login = ORIGINAL_LOGIN();  
SET @current_context = SUSER_SNAME();  
SELECT 'The current executing context is: '+ @current_context;  
SELECT 'The original login in this session was: '+ @original_login  
GO  
-- Return to the original execution context  
-- and remove the temporary principal.  
REVERT;  
GO  
DROP LOGIN login1;  
DROP USER user1;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [REVERT &#40;Transact-SQL&#41;](../../t-sql/statements/revert-transact-sql.md)  
  
  
