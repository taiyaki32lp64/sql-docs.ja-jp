---
title: FETCH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FETCH
- FETCH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FETCH statement
- cursors [SQL Server], fetching
- Transact-SQL cursors, fetching and scrolling
- retrieving rows
- fetching [SQL Server]
- SCROLL option
- row fetching [SQL Server]
ms.assetid: 5d68dac2-f91b-4342-bb4e-209ee132665f
author: rothja
ms.author: jroth
ms.openlocfilehash: 8fd770d8f1af098d4328df12a11cdcff609f2328
ms.sourcegitcommit: f6bfe4a0647ce7efebaca11d95412d6a9a92cd98
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2019
ms.locfileid: "71974398"
---
# <a name="fetch-transact-sql"></a>FETCH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] サーバー カーソルから特定の行を取得します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
FETCH   
          [ [ NEXT | PRIOR | FIRST | LAST   
                    | ABSOLUTE { n | @nvar }   
                    | RELATIVE { n | @nvar }   
               ]   
               FROM   
          ]   
{ { [ GLOBAL ] cursor_name } | @cursor_variable_name }   
[ INTO @variable_name [ ,...n ] ]   
```  
  
## <a name="arguments"></a>引数  
 NEXT  
 現在の行の直後にある行を結果行として返し、この返した行に現在の行を加えます。 カーソルに対する最初のフェッチが `FETCH NEXT` の場合、結果セットの先頭の行が返ります。 `NEXT` は、カーソル フェッチの既定のオプションです。  
  
 PRIOR  
 現在の行の直前にある行を結果行として返し、現在の行を減らして、この返した行にします。 カーソルに対する最初のフェッチが `FETCH PRIOR` の場合、行は返されません。カーソルは先頭行の前に位置したままです。  
  
 FIRST  
 カーソル内の先頭行を返し、これを現在の行にします。  
  
 LAST  
 カーソル内の最終行を返し、これを現在の行にします。  
  
 ABSOLUTE { *n*| \@*nvar*}  
 *n* または \@*nvar* が正の値の場合は、カーソルの先頭から *n* 行目の行を返し、返した行を新しい現在の行にします。 *n* または \@*nvar* が負の値の場合は、カーソルの終端から *n* 行前の行を返し、返した行を新しい現在の行にします。 *n* または \@*nvar* が 0 の場合は、行を返しません。 *n* は整数の定数である必要があります。また、\@*nvar* は **smallint**、**tinyint**、または **int** である必要があります。  
  
 RELATIVE { *n*| \@*nvar*}  
 *n* または \@*nvar* が正の値の場合は、現在の行を先頭に *n* 行目の行を返し、返した行を新しい現在の行にします。 *n* または \@*nvar* が負の値の場合は、現在の行から *n* 行前の行を返し、返した行を新しい現在の行にします。 *n* または \@*nvar* が 0 の場合は、現在の行を返します。 カーソルに対して実行する最初のフェッチで、*n* または \@*nvar* を負の値または 0 に設定して `FETCH RELATIVE` を指定した場合は、行を返しません。 *n* は整数の定数である必要があります。また、\@*nvar* は **smallint**、**tinyint**、または **int** である必要があります。  
  
 GLOBAL  
 *cursor_name* でグローバル カーソルを参照することを指定します。  
  
 *cursor_name*  
 フェッチが行われる、開いているカーソルの名前です。 *cursor_name* という名前のグローバル カーソルとローカル カーソルの両方がある場合、GLOBAL が指定されると *cursor_name* はグローバル カーソルを参照します。GLOBAL が指定されない場合は、ローカル カーソルを参照します。  
  
 \@*cursor_variable_name*  
 フェッチが行われる、開いているカーソルを参照するカーソル変数の名前です。  
  
 INTO \@*variable_name*[ ,...*n*]  
 フェッチの列で得られたデータを、ローカル変数に設定します。 リスト内の各変数は、左から右に向かって、カーソル結果セット内の対応する列に関連付けられます。 各変数のデータ型は、対応する結果セット列のデータ型に一致するか、または暗黙的な型変換がサポートされていなければなりません。 変数の個数は、カーソル選択リスト内の列の個数と一致している必要があります。  
  
## <a name="remarks"></a>Remarks  
 `SCROLL` オプションが ISO 形式の`DECLARE CURSOR` ステートメントで指定されていない場合、サポートされる `FETCH` オプションは `NEXT` のみです。 ISO 形式の `DECLARE CURSOR` で `SCROLL` が指定されている場合、すべての `FETCH` オプションがサポートされます。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] DECLARE カーソル拡張が使用されると、次のルールが適用されます。  
  
-   `FORWARD_ONLY` または `FAST_FORWARD` のいずれかが指定されている場合、サポートされる `FETCH` オプションは `NEXT` のみです。  
  
-   `DYNAMIC`、`FORWARD_ONLY`、または `FAST_FORWARD` が指定されていない場合、`KEYSET`、`STATIC`、または `SCROLL` を指定すると、すべての `FETCH` オプションがサポートされます。  
  
-   `DYNAMIC SCROLL` カーソルは、`ABSOLUTE` を除くすべての `FETCH` オプションをサポートします。  
  
 `@@FETCH_STATUS` 関数は、最後に実行された `FETCH` ステートメントのステータスを返します。 sp_describe_cursor で返されるカーソル内の fetch_status 列に、同じ情報が記録されます。 `FETCH` ステートメントで返されたデータに対して操作を行う前に、このステータス情報を使用してデータの妥当性を判断する必要があります。 詳細については、「[@@FETCH_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/fetch-status-transact-sql.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 `FETCH` のアクセス許可は、既定ですべての有効なユーザーに与えられます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-fetch-in-a-simple-cursor"></a>A. 単純カーソル内での FETCH を使用する  
 この例では、`Person.Person` テーブル内の姓が `B` で始まる行に対して単純カーソルを宣言し、`FETCH NEXT` を使用して行を順番に移動します。 `FETCH` ステートメントは、`DECLARE CURSOR` の中で指定された列の値を、単一行の結果セットとして返します。  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE contact_cursor CURSOR FOR  
SELECT LastName FROM Person.Person  
WHERE LastName LIKE 'B%'  
ORDER BY LastName;  
  
OPEN contact_cursor;  
  
-- Perform the first fetch.  
FETCH NEXT FROM contact_cursor;  
  
-- Check @@FETCH_STATUS to see if there are any more rows to fetch.  
WHILE @@FETCH_STATUS = 0  
BEGIN  
   -- This is executed as long as the previous fetch succeeds.  
   FETCH NEXT FROM contact_cursor;  
END  
  
CLOSE contact_cursor;  
DEALLOCATE contact_cursor;  
GO  
```  
  
### <a name="b-using-fetch-to-store-values-in-variables"></a>B. FETCH を使用して変数に値を格納する  
 次の例は例 A に似ていますが、`FETCH` ステートメントの出力をクライアントに直接返すのではなく、ローカル変数に格納します。 `PRINT` ステートメントは変数を 1 つの文字列に結合し、これをクライアントに返します。  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Declare the variables to store the values returned by FETCH.  
DECLARE @LastName varchar(50), @FirstName varchar(50);  
  
DECLARE contact_cursor CURSOR FOR  
SELECT LastName, FirstName FROM Person.Person  
WHERE LastName LIKE 'B%'  
ORDER BY LastName, FirstName;  
  
OPEN contact_cursor;  
  
-- Perform the first fetch and store the values in variables.  
-- Note: The variables are in the same order as the columns  
-- in the SELECT statement.   
  
FETCH NEXT FROM contact_cursor  
INTO @LastName, @FirstName;  
  
-- Check @@FETCH_STATUS to see if there are any more rows to fetch.  
WHILE @@FETCH_STATUS = 0  
BEGIN  
  
   -- Concatenate and display the current values in the variables.  
   PRINT 'Contact Name: ' + @FirstName + ' ' +  @LastName  
  
   -- This is executed as long as the previous fetch succeeds.  
   FETCH NEXT FROM contact_cursor  
   INTO @LastName, @FirstName;  
END  
  
CLOSE contact_cursor;  
DEALLOCATE contact_cursor;  
GO  
```  
  
### <a name="c-declaring-a-scroll-cursor-and-using-the-other-fetch-options"></a>C. SCROLL カーソルを宣言し、他の FETCH オプションを使用する  
 次の例では、`SCROLL` カーソルを作成し、`LAST`、`PRIOR`、`RELATIVE`、および `ABSOLUTE` オプションを介してすべてのスクロール機能を使用します。  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Execute the SELECT statement alone to show the   
-- full result set that is used by the cursor.  
SELECT LastName, FirstName FROM Person.Person  
ORDER BY LastName, FirstName;  
  
-- Declare the cursor.  
DECLARE contact_cursor SCROLL CURSOR FOR  
SELECT LastName, FirstName FROM Person.Person  
ORDER BY LastName, FirstName;  
  
OPEN contact_cursor;  
  
-- Fetch the last row in the cursor.  
FETCH LAST FROM contact_cursor;  
  
-- Fetch the row immediately prior to the current row in the cursor.  
FETCH PRIOR FROM contact_cursor;  
  
-- Fetch the second row in the cursor.  
FETCH ABSOLUTE 2 FROM contact_cursor;  
  
-- Fetch the row that is three rows after the current row.  
FETCH RELATIVE 3 FROM contact_cursor;  
  
-- Fetch the row that is two rows prior to the current row.  
FETCH RELATIVE -2 FROM contact_cursor;  
  
CLOSE contact_cursor;  
DEALLOCATE contact_cursor;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
