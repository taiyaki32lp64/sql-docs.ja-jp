---
title: SQL の例の埋め込み |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- embedded SQL [ODBC]
ms.assetid: b8a26e05-3c82-4c5f-8f01-9de0edb645e9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 966962bdda79a57e83a0bce06b9254267efb474c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068657"
---
# <a name="embedded-sql-example"></a>埋め込み SQL の例
次のコードは c 言語で記述された単純な埋め込み SQL プログラムです。プログラムは、埋め込みのすべてではありませんが、ほとんどの SQL の方法を示しています。 プログラムは、注文番号のユーザーに求めます、顧客番号、別に販売員と注文の状態を取得し、画面に取得した情報を表示します。  
  
```cpp  
int main() {  
   EXEC SQL INCLUDE SQLCA;  
   EXEC SQL BEGIN DECLARE SECTION;  
      int OrderID;         /* Employee ID (from user)         */  
      int CustID;            /* Retrieved customer ID         */  
      char SalesPerson[10]   /* Retrieved salesperson name      */  
      char Status[6]         /* Retrieved order status        */  
   EXEC SQL END DECLARE SECTION;  
  
   /* Set up error processing */  
   EXEC SQL WHENEVER SQLERROR GOTO query_error;  
   EXEC SQL WHENEVER NOT FOUND GOTO bad_number;  
  
   /* Prompt the user for order number */  
   printf ("Enter order number: ");  
   scanf_s("%d", &OrderID);  
  
   /* Execute the SQL query */  
   EXEC SQL SELECT CustID, SalesPerson, Status  
      FROM Orders  
      WHERE OrderID = :OrderID  
      INTO :CustID, :SalesPerson, :Status;  
  
   /* Display the results */  
   printf ("Customer number:  %d\n", CustID);  
   printf ("Salesperson: %s\n", SalesPerson);  
   printf ("Status: %s\n", Status);  
   exit();  
  
query_error:  
   printf ("SQL error: %ld\n", sqlca->sqlcode);  
   exit();  
  
bad_number:  
   printf ("Invalid order number.\n");  
   exit();  
}  
```  
  
 このプログラムについては、次に注意してください。  
  
-   **ホスト変数**で囲まれたセクションでは、ホスト変数が宣言されている、**宣言セクションの開始**と**エンド宣言セクション**キーワード。 埋め込まれた SQL ステートメントに表示されるときに各ホストの変数名のコロン (:) が付きます。 コロンは、ホスト変数やテーブルと同じ名前を含む列などのデータベース オブジェクトを区別するプリコンパイラを使用できます。  
  
-   **データ型**DBMS とホスト言語でサポートされるデータ型をまったく異なることができます。 ホストの変数は、二重の役割を果たすため、これに影響します。 一方では、ホスト変数は、プログラム変数、宣言され、ホスト言語のステートメントによって操作です。 その一方で、データベースのデータを取得する組み込みの SQL ステートメントで、使用されます。 DBMS のデータ型に対応するホスト言語の型がない場合は、DBMS は、データを自動的に変換します。 ただし、各 DBMS は、独自のルールと変換プロセスに関連付けられている特異性があるために、慎重にホストの変数の型が選択する必要があります。  
  
-   **エラー処理**DBMS が、SQL 通信領域、または SQLCA によるアプリケーション プログラムを実行時エラーを報告します。 上記のコード例では、最初の埋め込まれた SQL ステートメントは、含める SQLCA は。 これは、プログラムに SQLCA 構造体を含めるプリコンパイラを指示します。 これは、機能は、プログラムは、DBMS によって返されるエラーを処理するたびに必要です。 WHENEVER.GOTO ステートメントは、分岐を特定のラベルを使用しているときにエラーが発生したエラー処理コードを生成するプリコンパイラを指示します。  
  
-   **単一選択**データを返すために使用するステートメントは単一の SELECT ステートメント。 つまり、1 行のデータのみを返します。 そのため、コード例を宣言したりしないカーソルを使用します。
