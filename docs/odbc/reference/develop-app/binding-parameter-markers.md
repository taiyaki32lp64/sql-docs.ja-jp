---
title: バインディング パラメーター マーカー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- parameter markers [ODBC]
- binding parameter markers [ODBC]
ms.assetid: fe88c1c2-4ee4-45e0-8500-b8c25c047815
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0e625e01b9bf4771f18dd8e9807ab09100ca580c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107649"
---
# <a name="binding-parameter-markers"></a>バインディング パラメーター マーカー
アプリケーションが呼び出すことによってパラメーターをバインド**SQLBindParameter**します。 **SQLBindParameter**一度に 1 つのパラメーターをバインドします。 アプリケーションは、次を指定します。  
  
-   パラメーターの数。 パラメーターは、増加のパラメーターの順序番号 1 以降、SQL ステートメント内で番号が付けられます。 以上であるパラメーターの数を指定することは、ステートメントが実行されたときに、SQL ステートメント内のパラメーター数よりも、パラメーター値は無視されます。  
  
-   パラメーターの型 (入力、入力/出力、または出力)。 プロシージャ呼び出しのパラメーターを除くすべてのパラメーターは入力パラメーターが。 詳細については、次を参照してください。[プロシージャ パラメーター](../../../odbc/reference/develop-app/procedure-parameters.md)、このセクションで後述します。  
  
-   変数の C データ型、アドレス、およびバイト長は、パラメーターにバインドします。 ドライバーは、データを C データ型から SQL データ型に変換できる必要があります。 またはエラーが返されます。 サポートされる変換の一覧は、次を参照してください[C から SQL データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)付録 d:。データ型。  
  
-   SQL データ型、有効桁数、およびパラメーター自体の小数点以下桁数。  
  
-   長さ/インジケーター バッファーのアドレス。 バイナリまたは文字のデータの長さをバイト、データが null の場合を指定します。 または、でのデータが送信されることを指定します**SQLPutData**します。 詳細については、次を参照してください。[長さ/インジケーターの値を使用して](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)します。  
  
 たとえば、次のコードのバインド*販売員*と*CustID*販売員と CustID 列のパラメーターにします。 *販売員*可変長である、文字データが含まれています、コードのバイト長の指定*販売員*(11) バインドと*SalesPersonLenOrInd*に内のデータのバイトの長さを含む*販売員*します。 この情報が必要ない*CustID*の固定長である整数データが含まれています。  
  
```  
SQLCHAR       SalesPerson[11];  
SQLINTEGER    SalesPersonLenOrInd, CustIDInd;  
SQLUINTEGER   CustID;  
  
// Bind SalesPerson to the parameter for the SalesPerson column and  
// CustID to the parameter for the CustID column.  
SQLBindParameter(hstmt1, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 10, 0,  
                  SalesPerson, sizeof(SalesPerson), &SalesPersonLenOrInd);  
SQLBindParameter(hstmt1, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &CustID, 0, &CustIDInd);  
  
// Set values of salesperson and customer ID and length/indicators.  
strcpy_s((char*)SalesPerson, _countof(SalesPerson), "Garcia");  
SalesPersonLenOrInd = SQL_NTS;  
CustID = 1331;  
CustIDInd = 0;  
  
// Execute a statement to get data for all orders made to the specified  
// customer by the specified salesperson.  
SQLExecDirect(hstmt1,"SELECT * FROM Orders WHERE SalesPerson=? AND CustID=?",SQL_NTS);  
```  
  
 ときに**SQLBindParameter**が呼び出されると、ドライバー情報を保存、ステートメントの構造体。 ステートメントが実行されたときに、パラメーター データを取得し、データ ソースに送信する情報を使用します。  
  
> [!NOTE]  
>  パラメーターのバインドされていたと ODBC 1.0 では、 **SQLSetParam**します。 ドライバー マネージャーの間の呼び出しをマップする**SQLSetParam**と**SQLBindParameter**アプリケーションおよびドライバーによって使用される ODBC のバージョンに応じて、します。
