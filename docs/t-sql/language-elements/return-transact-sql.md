---
title: RETURN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RETURN_TSQL
- RETURN
dev_langs:
- TSQL
helpviewer_keywords:
- unconditionally exiting program
- stored procedures [SQL Server], exiting
- batches [SQL Server], exiting
- statement blocks [SQL Server]
- queries [SQL Server], exiting
- exiting queries [SQL Server]
- exiting procedures [SQL Server]
- RETURN statement
ms.assetid: 1d9c8247-fd89-4544-be9c-01c95b745db0
author: rothja
ms.author: jroth
ms.openlocfilehash: 7e16193e0bf6a9596a17f767b157fc825ff3e0a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072371"
---
# <a name="return-transact-sql"></a>RETURN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  クエリまたはプロシージャを無条件で終了します。 RETURN は即時に実行され、完了します。また、プロシージャ、バッチ、またはステートメント ブロックを終了する任意の位置で使用できます。 RETURN の後に続くステートメントは実行されません。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
RETURN [ integer_expression ]   
```  
  
## <a name="arguments"></a>引数  
 *integer_expression*  
 返される整数値です。 ストアド プロシージャは、呼び出しプロシージャまたはアプリケーションに整数値を返すことができます。  
  
## <a name="return-types"></a>戻り値の型  
 必要に応じて **int** を返します。  
  
> [!NOTE]  
>  特に記述がない限り、すべてのシステム ストアド プロシージャでは値 0 が返されます。 これは成功を示し、0 以外の値は失敗を示します。  
  
## <a name="remarks"></a>Remarks  
 ストアド プロシージャと一緒に使用する場合、RETURN は NULL 値を返すことができません。 プロシージャが NULL 値を返そうとすると (たとえば、@status の値が NULL のときに RETURN @status を使用)、警告メッセージが生成されて値 0 が返されます。  
  
 現在のプロシージャを実行したバッチまたはプロシージャの中の後続の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントに、返されたステータス値を指定できます。この場合、`EXECUTE @return_status = <procedure_name>` の形式で入力する必要があります。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-from-a-procedure"></a>A. プロシージャを終了する  
 次の例では、`findjobs` を実行するときにユーザー名がパラメーターとして指定されていない場合、ユーザーの画面にメッセージを出力後、`RETURN` でプロシージャを終了します。 ユーザー名が指定された場合は、そのユーザーが現在のデータベースに作成したすべてのオブジェクトの名前が、適切なシステム テーブルから取得されます。  
  
```  
CREATE PROCEDURE findjobs @nm sysname = NULL  
AS   
IF @nm IS NULL  
    BEGIN  
        PRINT 'You must give a user name'  
        RETURN  
    END  
ELSE  
    BEGIN  
        SELECT o.name, o.id, o.uid  
        FROM sysobjects o INNER JOIN master..syslogins l  
            ON o.uid = l.sid  
        WHERE l.name = @nm  
    END;  
```  
  
### <a name="b-returning-status-codes"></a>B. ステータス コードを返す  
 次の例では、指定した連絡先の ID の状態をチェックします。 状態が Washington (`WA`) である場合は、`1` の状態が返されます。 `2` が `WA` 以外の値であったり、`StateProvince` が行に一致しないなど、それ以外のすべての場合は、`ContactID` を返します。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE PROCEDURE checkstate @param varchar(11)  
AS  
IF (SELECT StateProvince FROM Person.vAdditionalContactInfo WHERE ContactID = @param) = 'WA'  
    RETURN 1  
ELSE  
    RETURN 2;  
GO  
```  
  
 次の例では、`checkstate` を実行して得られる戻りステータスを示します。 最初は Washington の連絡先、2 つ目は Washington 以外の連絡先、3 つ目は有効でない連絡先を示しています。 `@return_status` ローカル変数は、これを宣言してからでないと使用できません。  
  
```  
DECLARE @return_status int;  
EXEC @return_status = checkstate '2';  
SELECT 'Return Status' = @return_status;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Return Status 
  
 ------------- 
  
 1
 ```  
  
 別の連絡先番号を指定して、クエリを再び実行します。  
  
```  
DECLARE @return_status int;  
EXEC @return_status = checkstate '6';  
SELECT 'Return Status' = @return_status;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Return Status  
 -------------  
  
 2
 ```  
  
 別の連絡先番号を指定して、クエリを再び実行します。  
  
```  
DECLARE @return_status int  
EXEC @return_status = checkstate '12345678901';  
SELECT 'Return Status' = @return_status;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Return Status  
 -------------  
  
 2
 ```  
  
## <a name="see-also"></a>参照  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)   
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)  
  
  
