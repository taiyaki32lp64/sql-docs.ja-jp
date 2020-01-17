---
title: REVERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- REVERT_TSQL
- REVERT
dev_langs:
- TSQL
helpviewer_keywords:
- REVERT statement
- context switching [SQL Server], reverting
- reverting execution context
- REVERT WITH COOKIE statement
- execution context [SQL Server]
- COOKIE clause
ms.assetid: 4688b17a-dfd1-4f03-8db4-273a401f879f
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2105b03f64ecc2e0357e5a06f0d7cb2c18fb69b0
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252177"
---
# <a name="revert-transact-sql"></a>REVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  実行コンテキストを、最後の EXECUTE AS ステートメントの呼び出し元に戻します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
REVERT  
    [ WITH COOKIE = @varbinary_variable ]  
```  
  
## <a name="arguments"></a>引数  
 WITH COOKIE = @*varbinary_variable*  
 対応するスタンドアロンの [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md) ステートメントで作成されたクッキーを指定します。 *\@varbinary_variable* は **varbinary(100)** です。  
  
## <a name="remarks"></a>Remarks  
 REVERT は、ストアド プロシージャまたはユーザー定義関数などのモジュール内で、またはスタンドアロンのステートメントとして指定できます。 モジュール内で指定した場合、REVERT はモジュール内で定義された EXECUTE AS ステートメントにのみ適用されます。 たとえば、次のストアド プロシージャでは、`EXECUTE AS` ステートメントの後に `REVERT` ステートメントが実行されます。  
  
```  
CREATE PROCEDURE dbo.usp_myproc   
  WITH EXECUTE AS CALLER  
AS   
    SELECT SUSER_NAME(), USER_NAME();  
    EXECUTE AS USER = 'guest';  
    SELECT SUSER_NAME(), USER_NAME();  
    REVERT;  
    SELECT SUSER_NAME(), USER_NAME();  
GO  
```  
  
 次の例のように、ストアド プロシージャが実行されるセッションで、セッションの実行コンテキストが明示的に `login1` に変更されるとします。  
  
```  
  -- Sets the execution context of the session to 'login1'.  
EXECUTE AS LOGIN = 'login1';  
GO  
EXECUTE dbo.usp_myproc;   
```  
  
 この場合、`usp_myproc` 内で定義された `REVERT` ステートメントでは、モジュール内で設定されている実行コンテキストが切り替えられますが、モジュール外で設定されている実行コンテキストに影響はありません。 つまり、セッションの実行コンテキストは `login1` のままです。  
  
 スタンドアロンのステートメントとして指定した場合、REVERT はバッチまたはセッション内で定義された EXECUTE AS に適用されます。 対応する EXECUTE AS ステートメントに WITH NO REVERT 句が含まれている場合、REVERT は無効です。 この場合、実行コンテキストはセッションが削除されるまで有効です。  
  
## <a name="using-revert-with-cookie"></a>REVERT WITH COOKIE の使用  
 セッションの実行コンテキストの設定に使われる EXECUTE AS ステートメントには、WITH NO REVERT COOKIE = @*varbinary_variable* 句を指定できます。 このステートメントを実行すると、[!INCLUDE[ssDE](../../includes/ssde-md.md)]ではクッキーが @*varbinary_variable* に渡されます。 そのステートメントで設定された実行コンテキストを以前のコンテキストに戻すことができるのは、REVERT WITH COOKIE = @*varbinary_variable* ステートメントの呼び出し時に、適切な *\@varbinary_variable* 値が含まれている場合だけです。  
  
 このメカニズムは、接続プールが使用される環境で役立ちます。 接続プールには、複数のエンド ユーザーがアプリケーションで再利用するデータベース接続のグループが管理されています。 *\@varbinary_variable* に渡される値は、EXECUTE AS ステートメントの呼び出し元 (この場合はアプリケーション) だけが認識できるため、呼び出し元が確立した実行コンテキストは、アプリケーションを呼び出すエンド ユーザーによって変更されることはありません。 実行コンテキストが戻された後、アプリケーションではコンテキストを他のプリンシパルに切り替えることができます。  
  
## <a name="permissions"></a>アクセス許可  
 権限は必要ありません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-execute-as-and-revert-to-switch-context"></a>A. EXECUTE AS と REVERT を使用してコンテキストを切り替える  
 次の例では、複数のプリンシパルを使用してコンテキスト実行スタックを作成した後、 REVERT ステートメントを使用して実行コンテキストを以前のコンテキストに戻します。 REVERT ステートメントは、実行コンテキストが最初の呼び出し元に設定されるまで、スタックの上層に向かって複数回実行されます。  
  
```  
USE AdventureWorks2012;  
GO  
-- Create two temporary principals.  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE LOGIN login2 WITH PASSWORD = 'Uor80$23b';  
GO  
CREATE USER user1 FOR LOGIN login1;  
CREATE USER user2 FOR LOGIN login2;  
GO  
-- Give IMPERSONATE permissions on user2 to user1  
-- so that user1 can successfully set the execution context to user2.  
GRANT IMPERSONATE ON USER:: user2 TO user1;  
GO  
-- Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- Set the execution context to login1.   
EXECUTE AS LOGIN = 'login1';  
-- Verify that the execution context is now login1.  
SELECT SUSER_NAME(), USER_NAME();  
-- Login1 sets the execution context to login2.  
EXECUTE AS USER = 'user2';  
-- Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- The execution context stack now has three principals: the originating caller, login1, and login2.  
-- The following REVERT statements will reset the execution context to the previous context.  
REVERT;  
-- Display the current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
REVERT;  
-- Display the current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
  
-- Remove the temporary principals.  
DROP LOGIN login1;  
DROP LOGIN login2;  
DROP USER user1;  
DROP USER user2;  
GO  
```  
  
### <a name="b-using-the-with-cookie-clause"></a>B. WITH COOKIE 句を使用する  
 次の例では、セッションの実行コンテキストを、指定したユーザーに設定し、WITH NO REVERT COOKIE = @*varbinary_variable* 句を指定します。 コンテキストを正常に呼び出し元に戻すには、`REVERT` ステートメントで、`EXECUTE AS` ステートメントの `@cookie` 変数に渡される値を指定する必要があります。 この例を実行するには、例 A で作成したログイン `login1` とユーザー `user1` が存在している必要があります。  
  
```  
DECLARE @cookie varbinary(100);  
EXECUTE AS USER = 'user1' WITH COOKIE INTO @cookie;  
-- Store the cookie somewhere safe in your application.  
-- Verify the context switch.  
SELECT SUSER_NAME(), USER_NAME();  
--Display the cookie value.  
SELECT @cookie;  
GO  
-- Use the cookie in the REVERT statement.  
DECLARE @cookie varbinary(100);  
-- Set the cookie value to the one from the SELECT @cookie statement.  
SET @cookie = <value from the SELECT @cookie statement>;  
REVERT WITH COOKIE = @cookie;  
-- Verify the context switch reverted.  
SELECT SUSER_NAME(), USER_NAME();  
GO  
```  
  
## <a name="see-also"></a>参照  
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [EXECUTE AS 句 &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [SUSER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-name-transact-sql.md)   
 [USER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)  
  
  
