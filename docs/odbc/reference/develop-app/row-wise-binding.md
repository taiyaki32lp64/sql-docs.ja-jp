---
title: 行方向のバインド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4f622cf4-0603-47a1-a48b-944c4ef46364
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aab33f8805741083fd42e9fbcb25d67a416be319
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061617"
---
# <a name="row-wise-binding"></a>行方向のバインド
行方向のバインドを使用する場合、アプリケーション 1 つまたは 2 を含む構造体を定義または場合によって 3 では、データが返される対象の各列の要素。 最初の要素は、データ値を保持し、2 番目の要素が長さ/インジケーター バッファーを保持します。 インジケーターと長さの値は SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR 記述子フィールドを別の値に設定しての別のバッファーに格納できます。これが完了している場合、構造体には、3 番目の要素が含まれています。 その後、アプリケーションでは、行セットの行がある多くの要素を含むこれらの構造体の配列を割り当てます。  
  
 アプリケーションでは、SQL_ATTR_ROW_BIND_TYPE ステートメント属性を持つドライバーに構造体のサイズを宣言し、配列の最初の要素内の各メンバーのアドレスにバインドします。 そのため、ドライバーが特定の行と列のデータのアドレスを計算できます。  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size)  
```  
  
 場所の行は 1 から行セットのサイズを数えます。 (いずれかから差し引かれます行番号配列を C でのインデックスは 0 から始まるためです。)次の図は、行方向のバインドの動作を示します。 一般に、構造にバインドされる列のみが含まれます。 構造体は、結果セット列に関連しないフィールドを含めることができます。 列は、任意の順序で構造内に配置することができますが、わかりやすくするための順番に表示されます。  
  
 ![表示行&#45;賢明バインド](../../../odbc/reference/develop-app/media/pr22.gif "pr22")  
  
 たとえば、次のコードでは、OrderID、営業担当者、および状態の列のデータと長さ/インジケーターの販売員と状態列に返される要素を持つ構造体を作成します。 これらの構造体の 10 を割り当てるし、OrderID、営業担当者、および状態列にバインドします。  
  
```  
#define ROW_ARRAY_SIZE 10  
  
// Define the ORDERINFO struct and allocate an array of 10 structs.  
typedef struct {  
   SQLUINTEGER   OrderID;  
   SQLINTEGER    OrderIDInd;  
   SQLCHAR       SalesPerson[11];  
   SQLINTEGER    SalesPersonLenOrInd;  
   SQLCHAR       Status[7];  
   SQLINTEGER    StatusLenOrInd;  
} ORDERINFO;  
ORDERINFO OrderInfoArray[ROW_ARRAY_SIZE];  
  
SQLULEN    NumRowsFetched;  
SQLUSMALLINT   RowStatusArray[ROW_ARRAY_SIZE], i;  
SQLRETURN      rc;  
SQLHSTMT       hstmt;  
  
// Specify the size of the structure with the SQL_ATTR_ROW_BIND_TYPE  
// statement attribute. This also declares that row-wise binding will  
// be used. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE  
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement  
// attribute to point to the row status array. Set the  
// SQL_ATTR_ROWS_FETCHED_PTR statement attribute to point to  
// NumRowsFetched.  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, sizeof(ORDERINFO), 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, ROW_ARRAY_SIZE, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROWS_FETCHED_PTR, &NumRowsFetched, 0);  
  
// Bind elements of the first structure in the array to the OrderID,  
// SalesPerson, and Status columns.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, &OrderInfoArray[0].OrderID, 0, &OrderInfoArray[0].OrderIDInd);  
SQLBindCol(hstmt, 2, SQL_C_CHAR, OrderInfoArray[0].SalesPerson,  
            sizeof(OrderInfoArray[0].SalesPerson),  
            &OrderInfoArray[0].SalesPersonLenOrInd);  
SQLBindCol(hstmt, 3, SQL_C_CHAR, OrderInfoArray[0].Status,  
            sizeof(OrderInfoArray[0].Status), &OrderInfoArray[0].StatusLenOrInd);  
  
// Execute a statement to retrieve rows from the Orders table.  
SQLExecDirect(hstmt, "SELECT OrderID, SalesPerson, Status FROM Orders", SQL_NTS);  
  
// Fetch up to the rowset size number of rows at a time. Print the actual  
// number of rows fetched; this number is returned in NumRowsFetched.  
// Check the row status array to print only those rows successfully  
// fetched. Code to check if rc equals SQL_SUCCESS_WITH_INFO or  
// SQL_ERRORnot shown.  
while ((rc = SQLFetchScroll(hstmt,SQL_FETCH_NEXT,0)) != SQL_NO_DATA) {  
   for (i = 0; i < NumRowsFetched; i++) {  
      if (RowStatusArray[i] == SQL_ROW_SUCCESS|| RowStatusArray[i] ==   
         SQL_ROW_SUCCESS_WITH_INFO) {  
         if (OrderInfoArray[i].OrderIDInd == SQL_NULL_DATA)  
            printf(" NULL      ");  
         else  
            printf("%d\t", OrderInfoArray[i].OrderID);  
         if (OrderInfoArray[i].SalesPersonLenOrInd == SQL_NULL_DATA)  
            printf(" NULL      ");  
         else  
            printf("%s\t", OrderInfoArray[i].SalesPerson);  
         if (OrderInfoArray[i].StatusLenOrInd == SQL_NULL_DATA)  
            printf(" NULL\n");  
         else  
            printf("%s\n", OrderInfoArray[i].Status);  
      }  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
