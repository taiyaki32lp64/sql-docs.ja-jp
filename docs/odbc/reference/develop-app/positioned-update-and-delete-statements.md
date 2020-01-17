---
title: 位置指定更新と Delete ステートメント |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: 0eafba50-02c7-46ca-a439-ef3307b935dc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5b37bdfae5f97a453477768aca39b801c06c0701
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023296"
---
# <a name="positioned-update-and-delete-statements"></a>位置指定の UPDATE および DELETE ステートメント
アプリケーションの更新または位置指定更新と結果セットの現在の行を削除またはステートメントを削除します。 位置指定更新と delete ステートメントは、一部のデータ ソースが、それらのすべてでサポートします。 アプリケーションが配置されているデータ ソースのサポートが update および delete ステートメントであるかどうかを判断するを呼び出す**SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1、または SQL_STATIC_CURSOR_ATTRIBUTES1*情報の種類*(によって、カーソルの種類)。 ODBC カーソル ライブラリが位置指定更新をシミュレートし、ステートメントを削除することに注意してください。  
  
 位置指定更新を使用して、または delete ステートメントは、アプリケーションは結果セットを作成する必要があります、**選択更新**ステートメント。 このステートメントの構文です。  
  
 **SELECT** [**ALL** &#124; **DISTINCT**]*elect-list*  
  
 **FROM** *table-reference-list*  
  
 [**WHERE** *search-condition*]  
  
 **FOR UPDATE OF** [*column-name* [ **,** *column-name*]...]  
  
 次に、アプリケーションは、更新または削除する行にカーソルを位置付けます。 呼び出してそのこの**SQLFetchScroll**必要な行を格納していると、呼び出しの行セットを取得する**SQLSetPos**をその行に行セットのカーソルを配置します。 その後、アプリケーションは、結果セットで使用されているステートメントよりも別のステートメントで、位置指定の update または delete ステートメントを実行します。 これらのステートメントの構文です。  
  
 **UPDATE** *table-name*  
  
 **SET** *column-identifier* **=** {*expression* &#124; **NULL**}  
  
 [ **,** *column-identifier* **=** {*expression* &#124; **NULL**}]...  
  
 **WHERE CURRENT OF** *cursor-name*  
  
 **DELETE FROM** *table-name* **WHERE CURRENT OF** *table-name*  
  
 これらのステートメントでカーソル名が必要なことに注意してください。 アプリケーションはいずれかでカーソル名を指定できます**SQLSetCursorName**設定またはデータ ソースを自動的にさせることができます、結果を作成するステートメントを実行する前に、カーソルが作成されたときにカーソル名を生成します。 後者の場合、アプリケーションが呼び出すことで位置指定更新と delete ステートメントで使用するためには、このカーソル名を取得**SQLGetCursorName**します。  
  
 たとえば、次のコードは、Customers テーブルをスクロールし、顧客レコードを削除または、アドレスと電話番号を更新するユーザーを許可します。 呼び出す**SQLSetCursorName** 3 つのステートメント ハンドルを使用して顧客の結果セットを作成する前に、カーソル名を指定する: *hstmtCust* 、結果セットの*hstmtUpdate*位置指定の update ステートメント、および*hstmtDelete*位置指定の delete ステートメント。 コードでは、位置指定の update ステートメントのパラメーターに別個の変数をバインドすることが、行セットのバッファーを更新し、これらのバッファーの要素をバインドします。 これにより、更新されたデータと同期した行セットのバッファーが保持されます。  
  
```  
#define POSITIONED_UPDATE 100  
#define POSITIONED_DELETE 101  
  
SQLUINTEGER    CustIDArray[10];  
SQLCHAR        NameArray[10][51], AddressArray[10][51],   
               PhoneArray[10][11];  
SQLINTEGER     CustIDIndArray[10], NameLenOrIndArray[10],   
               AddressLenOrIndArray[10],  
               PhoneLenOrIndArray[10];  
SQLUSMALLINT   RowStatusArray[10], Action, RowNum;  
SQLHSTMT       hstmtCust, hstmtUpdate, hstmtDelete;  
  
// Set the SQL_ATTR_BIND_TYPE statement attribute to use column-wise   
// binding. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE   
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement   
// attribute to point to the row status array.  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_BIND_TYPE, SQL_BIND_BY_COLUMN, 0);  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_ARRAY_SIZE, 10, 0);  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
  
// Bind arrays to the CustID, Name, Address, and Phone columns.  
SQLBindCol(hstmtCust, 1, SQL_C_ULONG, CustIDArray, 0, CustIDIndArray);  
SQLBindCol(hstmtCust, 2, SQL_C_CHAR, NameArray, sizeof(NameArray[0]),  
            NameLenOrIndArray);  
SQLBindCol(hstmtCust, 3, SQL_C_CHAR, AddressArray, sizeof(AddressArray[0]),  
         AddressLenOrIndArray);  
SQLBindCol(hstmtCust, 4, SQL_C_CHAR, PhoneArray, sizeof(PhoneArray[0]),  
            PhoneLenOrIndArray);  
  
// Set the cursor name to Cust.  
SQLSetCursorName(hstmtCust, "Cust", SQL_NTS);  
  
// Prepare positioned update and delete statements.  
SQLPrepare(hstmtUpdate,  
   "UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust",  
   SQL_NTS);  
SQLPrepare(hstmtDelete, "DELETE FROM Customers WHERE CURRENT OF Cust", SQL_NTS);  
  
// Execute a statement to retrieve rows from the Customers table.  
SQLExecDirect(hstmtCust,  
   "SELECT CustID, Name, Address, Phone FROM Customers FOR UPDATE OF Address, Phone",  
   SQL_NTS);  
  
// Fetch and display the first 10 rows.  
SQLFetchScroll(hstmtCust, SQL_FETCH_NEXT, 0);  
DisplayData(CustIDArray, CustIDIndArray, NameArray, NameLenOrIndArray, AddressArray,  
            AddressLenOrIndArray, PhoneArray, PhoneLenOrIndArray, RowStatusArray);  
  
// Call GetAction to get an action and a row number from the user.  
while (GetAction(&Action, &RowNum)) {  
   switch (Action) {  
  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmtCust, Action, RowNum);  
         DisplayData(CustIDArray, CustIDIndArray, NameArray, NameLenOrIndArray,  
                     AddressArray, AddressLenOrIndArray, PhoneArray,  
                     PhoneLenOrIndArray, RowStatusArray);  
         break;  
  
      case POSITIONED_UPDATE:  
         // Get the new data and place it in the rowset buffers.  
         GetNewData(AddressArray[RowNum - 1], &AddressLenOrIndArray[RowNum - 1],  
                     PhoneArray[RowNum - 1], &PhoneLenOrIndArray[RowNum - 1]);  
  
         // Bind the elements of the arrays at position RowNum-1 to the   
         // parameters of the positioned update statement.  
         SQLBindParameter(hstmtUpdate, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                           50, 0, AddressArray[RowNum - 1], sizeof(AddressArray[0]),  
                           &AddressLenOrIndArray[RowNum - 1]);  
         SQLBindParameter(hstmtUpdate, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                           10, 0, PhoneArray[RowNum - 1], sizeof(PhoneArray[0]),  
                           &PhoneLenOrIndArray[RowNum - 1]);  
  
         // Position the rowset cursor. The rowset is 1-based.  
         SQLSetPos(hstmtCust, RowNum, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
  
         // Execute the positioned update statement to update the row.  
         SQLExecute(hstmtUpdate);  
         break;  
  
      case POSITIONED_DELETE:  
         // Position the rowset cursor. The rowset is 1-based.  
         SQLSetPos(hstmtCust, RowNum, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
  
         // Execute the positioned delete statement to delete the row.  
         SQLExecute(hstmtDelete);  
         break;  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmtCust);  
```
