---
title: SQLSetPos による行セットの行を更新しています |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating rows
ms.assetid: d83a8c2a-5aa8-4f19-947c-79a817167ee1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0575c7ef7e380b1157640f9927e41192838c1ac0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091597"
---
# <a name="updating-rows-in-the-rowset-with-sqlsetpos"></a>SQLSetPos による行セットの行の更新
更新操作**SQLSetPos**データ ソースのデータを使用してアプリケーションのバッファーでバインドされた各列 (長さ/インジケーター バッファーの値が、SQL_COLUMN_IGNORE) 限り、テーブルの 1 つまたは複数の選択した行を更新します。 バインドされていない列は更新されません。  
  
 行を更新する**SQLSetPos**アプリケーションは、次を実行します。  
  
1.  行セットのバッファーでは、新しいデータ値を配置します。 長い形式のデータを送信する方法については**SQLSetPos**を参照してください[長い形式のデータ、SQLSetPos および SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)します。  
  
2.  必要に応じて、各列の長さ/インジケーター バッファーの値を設定します。 これは、SQL_NTS またはデータのバイト長のバイナリのバッファーを NULL に設定する列の SQL_NULL_DATA バインドされている列のデータのバイト長の文字列のバッファーにバインドされている列です。  
  
3.  SQL_COLUMN_IGNORE を更新する列の長さ/インジケーター バッファーの値を設定します。 アプリケーションは、この手順をスキップし、既存のデータを再送信、これは非効率的とが切り詰められました。 読み取られたときにデータ ソースに値を送信するリスクがあります。  
  
4.  呼び出し**SQLSetPos**で*操作*SQL_UPDATE に設定し、 *RowNumber*を更新する行の番号に設定します。 場合*RowNumber*が 0 の行セット内のすべての行が更新されます場合、。  
  
 後**SQLSetPos** 、更新された行に設定されている現在の行を返します。  
  
 行セットのすべての行を更新するときに (*RowNumber*が 0)、アプリケーションは、(、SQL_ATTR_ROW_OPERATION_PTR によって指さ行操作配列の対応する要素を設定して特定の行の更新を無効にできますステートメント属性) SQL_ROW_IGNORE にします。 行操作配列 (し、SQL_ATTR_ROW_STATUS_PTR ステートメント属性によって示される)、行の状態の配列に要素のサイズと数に対応しています。 アプリケーションを正常にフェッチされた行セットから削除されていない結果セットの行のみを更新する行操作配列として行セットをフェッチする関数から行の状態配列を使用して**SQLSetPos**.  
  
 更新プログラムとして、データ ソースに送信されるすべての行をアプリケーション バッファーは有効な行のデータが必要です。 アプリケーション バッファーをフェッチすることによって入力された場合、および行の状態配列が維持されている場合が SQL_ROW_DELETED、SQL_ROW_ERROR、または sql_row_norow であっても、それらの行位置の各値はできません。  
  
 たとえば、次のコードは、Customers テーブルをスクロールし、更新、削除、または新しい行を追加するユーザーを許可します。 呼び出しの前に行セットのバッファーに新しいデータを配置**SQLSetPos**を更新または新しい行を追加します。 新しい行を保持するために、行セットのバッファーの最後に割り当てられている行を追加これは既存のデータが上書きバッファーに新しい行のデータを配置することを防ぎます。  
  
```  
#define UPDATE_ROW   100  
#define DELETE_ROW   101  
#define ADD_ROW      102  
  
SQLUINTEGER    CustIDArray[11];  
SQLCHAR        NameArray[11][51], AddressArray[11][51],   
               PhoneArray[11][11];  
SQLINTEGER     CustIDIndArray[11], NameLenOrIndArray[11],   
               AddressLenOrIndArray[11],  
               PhoneLenOrIndArray[11];  
SQLUSMALLINT   RowStatusArray[10], Action, RowNum;  
SQLRETURN      rc;  
SQLHSTMT       hstmt;  
  
// Set the SQL_ATTR_ROW_BIND_TYPE statement attribute to use column-wise   
// binding. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE   
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement   
// attribute to point to the row status array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_KEYSET_DRIVEN, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, SQL_BIND_BY_COLUMN, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, 10, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
  
// Bind arrays to the CustID, Name, Address, and Phone columns.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, CustIDArray, 0, CustIDIndArray);  
SQLBindCol(hstmt, 2, SQL_C_CHAR, NameArray, sizeof(NameArray[0]), NameLenOrIndArray);  
SQLBindCol(hstmt, 3, SQL_C_CHAR, AddressArray, sizeof(AddressArray[0]),  
            AddressLenOrIndArray);  
SQLBindCol(hstmt, 4, SQL_C_CHAR, PhoneArray, sizeof(PhoneArray[0]),  
            PhoneLenOrIndArray);  
  
// Execute a statement to retrieve rows from the Customers table.  
SQLExecDirect(hstmt, "SELECT CustID, Name, Address, Phone FROM Customers", SQL_NTS);  
  
// Fetch and display the first 10 rows.  
rc = SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
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
         SQLFetchScroll(hstmt, Action, RowNum);  
         DisplayData(CustIDArray, CustIDIndArray,  
                     NameArray, NameLenOrIndArray,  
                     AddressArray, AddressLenOrIndArray,  
                     PhoneArray, PhoneLenOrIndArray, RowStatusArray);  
         break;  
  
      case UPDATE_ROW:  
         // Place the new data in the rowset buffers and update the   
         // specified row.  
         GetNewData(&CustIDArray[RowNum - 1], &CustIDIndArray[RowNum - 1],  
                  NameArray[RowNum - 1], &NameLenOrIndArray[RowNum - 1],  
                  AddressArray[RowNum - 1], &AddressLenOrIndArray[RowNum - 1],  
                  PhoneArray[RowNum - 1], &PhoneLenOrIndArray[RowNum - 1]);  
         SQLSetPos(hstmt, RowNum, SQL_UPDATE, SQL_LOCK_NO_CHANGE);  
         break;  
  
      case DELETE_ROW:  
         // Delete the specified row.  
         SQLSetPos(hstmt, RowNum, SQL_DELETE, SQL_LOCK_NO_CHANGE);  
         break;  
  
      case ADD_ROW:  
         // Place the new data in the rowset buffers at index 10.   
         // This is an extra element for new rows so rowset data is   
         // not overwritten. Insert the new row. Row 11 corresponds   
         // to index 10.  
         GetNewData(&CustIDArray[10], &CustIDIndArray[10],  
                     NameArray[10], &NameLenOrIndArray[10],  
                     AddressArray[10], &AddressLenOrIndArray[10],  
                     PhoneArray[10], &PhoneLenOrIndArray[10]);  
         SQLSetPos(hstmt, 11, SQL_ADD, SQL_LOCK_NO_CHANGE);  
         break;  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
