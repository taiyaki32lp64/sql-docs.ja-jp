---
title: DEALLOCATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DEALLOCATE
- DEALLOCATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], cursors
- DEALLOCATE statement
- deallocations [SQL Server]
- deleting cursor references
- removing cursor references
ms.assetid: c75cf73d-0268-4c57-973d-b8a84ff801fa
author: rothja
ms.author: jroth
ms.openlocfilehash: 92153155be5761e804c6d62cece4d392b40a1412
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67894898"
---
# <a name="deallocate-transact-sql"></a>DEALLOCATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  カーソル参照を削除します。 最後のカーソル参照の割り当てが解除されると、カーソルを構成するデータ構造は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって解放されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
DEALLOCATE { { [ GLOBAL ] cursor_name } | @cursor_variable_name }  
```  
  
## <a name="arguments"></a>引数  
 *cursor_name*  
 宣言済みのカーソル名を指定します。 *cursor_name* という名前のカーソルとして、グローバル カーソルとローカル カーソルの両方がある場合は、`GLOBAL` を指定すると *cursor_name* ではグローバル カーソルが参照され、`GLOBAL` を指定しないとローカル カーソルが参照されます。  
  
 @*cursor_variable_name*  
 **cursor** 変数の名前を指定します。 @*cursor_variable_name* は **cursor** 型である必要があります。  
  
## <a name="remarks"></a>Remarks  
カーソルを操作するステートメントでは、カーソル名またはカーソル変数を使用してカーソルを参照します。 `DEALLOCATE` を実行すると、カーソルと、カーソル名またはカーソル変数との間の関係が削除されます。 名前または変数がカーソルを参照する最後のものである場合は、カーソルの割り当てが解除され、カーソルが使用しているリソースが解放されます。 フェッチの孤立を防ぐために使用するスクロール ロックは、`DEALLOCATE` で解放されます。 カーソルを介して行われる位置指定更新を含め、更新を保護するために使用するトランザクション ロックは、トランザクションの終了時まで保持されます。  
  
`DECLARE CURSOR` ステートメントでは、カーソルを割り当て、カーソル名と関連付けます。  
  
```sql  
DECLARE abc SCROLL CURSOR FOR  
SELECT * FROM Person.Person;  
```  
  
カーソルにカーソル名が割り当てられると、このカーソルの割り当てが解除されるまで、その名前を同じ範囲 (グローバルまたはローカル) の別のカーソルに対して使用することはできません。  
  
 カーソル変数は、次のいずれかの方法でカーソルに関連付けられます。  
  
-   カーソルをカーソル変数に設定する `SET` ステートメントを使用して、名前を指定する。  
  
    ```sql  
    DECLARE @MyCrsrRef CURSOR;  
    SET @MyCrsrRef = abc;  
    ```  
  
-   カーソル名を定義せずにカーソルを作成し、変数に関連付ける。  
  
    ```sql  
    DECLARE @MyCursor CURSOR;  
    SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Person.Person;  
    ```  
  
 `DEALLOCATE <@cursor_variable_name>` ステートメントでは、カーソルに対し、指定した変数の参照だけを削除します。 変数の割り当ては、バッチ、ストアド プロシージャ、またはトリガーの終了時にその有効範囲が失われるまで、解除されることはありません。 `DEALLOCATE <@cursor_variable_name>` ステートメントの後で SET ステートメントを使用して、変数を別のカーソルに関連付けることもできます。  
  
```sql  
USE AdventureWorks2012;  
GO  
  
DECLARE @MyCursor CURSOR;  
SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Sales.SalesPerson;  
  
DEALLOCATE @MyCursor;  
  
SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Sales.SalesTerritory;  
GO  
```  
  
カーソル変数は、明示的に割り当てを解除する必要はありません。 変数は、有効範囲を失うと暗黙的に割り当てが解除されます。  
  
## <a name="permissions"></a>アクセス許可  
 `DEALLOCATE` のアクセス許可は、既定ですべての有効なユーザーに与えられます。  
  
## <a name="examples"></a>使用例  
 次の例では、最後の名前まで、またはカーソルを参照している変数の割り当てが解除されるまで、カーソルが保持されます。  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Create and open a global named cursor that  
-- is visible outside the batch.  
DECLARE abc CURSOR GLOBAL SCROLL FOR  
    SELECT * FROM Sales.SalesPerson;  
OPEN abc;  
GO  
-- Reference the named cursor with a cursor variable.  
DECLARE @MyCrsrRef1 CURSOR;  
SET @MyCrsrRef1 = abc;  
-- Now deallocate the cursor reference.  
DEALLOCATE @MyCrsrRef1;  
-- Cursor abc still exists.  
FETCH NEXT FROM abc;  
GO  
-- Reference the named cursor again.  
DECLARE @MyCrsrRef2 CURSOR;  
SET @MyCrsrRef2 = abc;  
-- Now deallocate cursor name abc.  
DEALLOCATE abc;  
-- Cursor still exists, referenced by @MyCrsrRef2.  
FETCH NEXT FROM @MyCrsrRef2;  
-- Cursor finally is deallocated when last referencing  
-- variable goes out of scope at the end of the batch.  
GO  
-- Create an unnamed cursor.  
DECLARE @MyCursor CURSOR;  
SET @MyCursor = CURSOR LOCAL SCROLL FOR  
SELECT * FROM Sales.SalesTerritory;  
-- The following statement deallocates the cursor  
-- because no other variables reference it.  
DEALLOCATE @MyCursor;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [カーソル](../../relational-databases/cursors.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
