---
title: 列方向のバインド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column-wise binding [ODBC]
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 86d37637-3a25-455d-9c82-a0d7bff8d70d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6f91dca1ac20173f9c10b4a52adf292e7abc45d0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083381"
---
# <a name="column-wise-binding"></a>列方向のバインド
列方向のバインドを使用する場合、アプリケーションは、データが返される対象の各列に 1 つまたは 2 つ、または場合によっては、次の 3 つの配列をバインドします。 最初の配列は、データの値を保持し、2 番目の配列は、長さ/インジケーター バッファーを保持します。 インジケーターと長さの値は SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR 記述子フィールドを別の値に設定しての別のバッファーに格納できます。これは、3 番目の配列はバインドされています。 各配列には、行セットの行がある多くの要素が含まれています。  
  
 SQL_ATTR_ROW_BIND_TYPE ステートメント属性を持つ列方向のバインドが使用されているアプリケーションの宣言のパラメーターではなくバッファーを行セットのバインドの種類を決定するバッファーを設定します。 ドライバーは、各配列の連続する要素の各行のデータを返します。 次の図は、列方向のバインドの動作を示します。  
  
 ![列&#45;3 つの列のバインドを賢明](../../../odbc/reference/develop-app/media/pr21.gif "pr21")  
  
 たとえば、次のコードでは、OrderID、営業担当者、および状態列に 10 要素の配列をバインドします。  
  
```  
#define ROW_ARRAY_SIZE 10  
  
SQLUINTEGER    OrderIDArray[ROW_ARRAY_SIZE], NumRowsFetched;  
SQLCHAR        SalesPersonArray[ROW_ARRAY_SIZE][11],  
               StatusArray[ROW_ARRAY_SIZE][7];  
SQLINTEGER     OrderIDIndArray[ROW_ARRAY_SIZE],  
               SalesPersonLenOrIndArray[ROW_ARRAY_SIZE],  
               StatusLenOrIndArray[ROW_ARRAY_SIZE];  
SQLUSMALLINT   RowStatusArray[ROW_ARRAY_SIZE], i;  
SQLRETURN      rc;  
SQLHSTMT       hstmt;  
  
// Set the SQL_ATTR_ROW_BIND_TYPE statement attribute to use  
// column-wise binding. Declare the rowset size with the  
// SQL_ATTR_ROW_ARRAY_SIZE statement attribute. Set the  
// SQL_ATTR_ROW_STATUS_PTR statement attribute to point to the  
// row status array. Set the SQL_ATTR_ROWS_FETCHED_PTR statement  
// attribute to point to cRowsFetched.  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, SQL_BIND_BY_COLUMN, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, ROW_ARRAY_SIZE, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROWS_FETCHED_PTR, &NumRowsFetched, 0);  
  
// Bind arrays to the OrderID, SalesPerson, and Status columns.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, OrderIDArray, 0, OrderIDIndArray);  
SQLBindCol(hstmt, 2, SQL_C_CHAR, SalesPersonArray, sizeof(SalesPersonArray[0]),  
            SalesPersonLenOrIndArray);  
SQLBindCol(hstmt, 3, SQL_C_CHAR, StatusArray, sizeof(StatusArray[0]),  
            StatusLenOrIndArray);  
  
// Execute a statement to retrieve rows from the Orders table.  
SQLExecDirect(hstmt, "SELECT OrderID, SalesPerson, Status FROM Orders", SQL_NTS);  
  
// Fetch up to the rowset size number of rows at a time. Print the actual  
// number of rows fetched; this number is returned in NumRowsFetched.  
// Check the row status array to print only those rows successfully  
// fetched. Code to check if rc equals SQL_SUCCESS_WITH_INFO or  
// SQL_ERROR not shown.  
while ((rc = SQLFetchScroll(hstmt,SQL_FETCH_NEXT,0)) != SQL_NO_DATA) {  
   for (i = 0; i < NumRowsFetched; i++) {  
      if ((RowStatusArray[i] == SQL_ROW_SUCCESS) ||  
            (RowStatusArray[i] == SQL_ROW_SUCCESS_WITH_INFO)) {  
         if (OrderIDIndArray[i] == SQL_NULL_DATA)  
            printf(" NULL      ");  
         else  
            printf("%d\t", OrderIDArray[i]);  
         if (SalesPersonLenOrIndArray[i] == SQL_NULL_DATA)  
            printf(" NULL      ");  
         else  
            printf("%s\t", SalesPersonArray[i]);  
         if (StatusLenOrIndArray[i] == SQL_NULL_DATA)  
            printf(" NULL\n");  
         else  
            printf("%s\n", StatusArray[i]);  
      }  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
