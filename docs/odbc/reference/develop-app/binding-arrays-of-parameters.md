---
title: パラメーターのバインディング配列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binding parameter arrays [ODBC]
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 037afe23-052d-4f3a-8aa7-45302b199ad0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 597142d41ed8d3cff26891dfdcc89398543dab43
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103824"
---
# <a name="binding-arrays-of-parameters"></a>パラメーターのバインディング配列
パラメーターの配列を使用するアプリケーションは、SQL ステートメントのパラメーターに、配列をバインドします。 これには 2 つの結合スタイルがあります。  
  
-   配列は、各パラメーターにバインドします。 各データ構造 (配列) には、1 つのパラメーターのすべてのデータが含まれています。 これは呼び出されます*列方向のバインド*1 つのパラメーターの値の列がバインドされています。  
  
-   パラメーターのセット全体のパラメーターのデータを保持し、これらの構造体の配列をバインドする構造体を定義します。 各データ構造体には、SQL ステートメントが 1 つのデータが含まれています。 これは呼び出されます*行方向のバインド*パラメーターの行バインドされています。  
  
 アプリケーションは、1 つの変数をパラメーターにバインドしたときに呼び出されます**SQLBindParameter**パラメーター配列にバインドします。 唯一の違いは、渡されたアドレスは、配列のアドレス、1 つの変数ではなくアドレスであります。 アプリケーションでは、列方向 (既定値) を使用するか行方向のバインドかどうかを指定するため、SQL_ATTR_PARAM_BIND_TYPE ステートメント属性を設定します。 列方向または行方向のバインドを使用するかどうかは、ほぼアプリケーションの基本設定の問題です。 プロセッサがメモリをアクセスする方法によっては、行方向のバインドを高速にあります。 ただし、違いは、非常に多くのパラメーターの行を除くごくわずかである可能性があります。  
  
## <a name="column-wise-binding"></a>列方向のバインド  
 列方向のバインドを使用する場合、アプリケーションは、各パラメーターのデータが提供するのに 1 つまたは 2 つの配列をバインドします。 最初の配列は、データの値を保持し、2 番目の配列は、長さ/インジケーター バッファーを保持します。 各配列には、パラメーターの値と同じ数の要素が含まれています。  
  
 既定値は、列方向のバインドします。 アプリケーション変更することも行方向のバインドから列方向のバインドに SQL_ATTR_PARAM_BIND_TYPE ステートメント属性を設定します。 次の図は、列方向のバインドの動作を示します。  
  
 ![表示方法列&#45;ごとの連結の動作が](../../../odbc/reference/develop-app/media/pr31.gif "pr31")  
  
 たとえば、次のコードでは、10 要素の配列を PartID、説明、および Price 列のパラメーターにバインドし、10 行を挿入するステートメントを実行します。 列方向のバインドを使用します。  
  
```  
#define DESC_LEN 51  
#define ARRAY_SIZE 10  
  
SQLCHAR *      Statement = "INSERT INTO Parts (PartID, Description,  Price) "  
                                                "VALUES (?, ?, ?)";  
SQLUINTEGER    PartIDArray[ARRAY_SIZE];  
SQLCHAR        DescArray[ARRAY_SIZE][DESC_LEN];  
SQLREAL        PriceArray[ARRAY_SIZE];  
SQLINTEGER     PartIDIndArray[ARRAY_SIZE], DescLenOrIndArray[ARRAY_SIZE],  
               PriceIndArray[ARRAY_SIZE];  
SQLUSMALLINT   i, ParamStatusArray[ARRAY_SIZE];  
SQLULEN ParamsProcessed;  
  
memset(DescLenOrIndArray, 0, sizeof(DescLenOrIndArray));  
memset(PartIDIndArray, 0, sizeof(PartIDIndArray));  
memset(PriceIndArray, 0, sizeof(PriceIndArray));  
  
// Set the SQL_ATTR_PARAM_BIND_TYPE statement attribute to use  
// column-wise binding.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_BIND_TYPE, SQL_PARAM_BIND_BY_COLUMN, 0);  
  
// Specify the number of elements in each parameter array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, ARRAY_SIZE, 0);  
  
// Specify an array in which to return the status of each set of  
// parameters.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_STATUS_PTR, ParamStatusArray, 0);  
  
// Specify an SQLUINTEGER value in which to return the number of sets of  
// parameters processed.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, &ParamsProcessed, 0);  
  
// Bind the parameters in column-wise fashion.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  PartIDArray, 0, PartIDIndArray);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  DescArray, DESC_LEN, DescLenOrIndArray);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  PriceArray, 0, PriceIndArray);  
  
// Set part ID, description, and price.  
for (i = 0; i < ARRAY_SIZE; i++) {  
   GetNewValues(&PartIDArray[i], DescArray[i], &PriceArray[i]);  
   PartIDIndArray[i] = 0;  
   DescLenOrIndArray[i] = SQL_NTS;  
   PriceIndArray[i] = 0;  
}  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Check to see which sets of parameters were processed successfully.  
for (i = 0; i < ParamsProcessed; i++) {  
   printf("Parameter Set  Status\n");  
   printf("-------------  -------------\n");  
   switch (ParamStatusArray[i]) {  
      case SQL_PARAM_SUCCESS:  
      case SQL_PARAM_SUCCESS_WITH_INFO:  
         printf("%13d  Success\n", i);  
         break;  
  
      case SQL_PARAM_ERROR:  
         printf("%13d  Error\n", i);  
         break;  
  
      case SQL_PARAM_UNUSED:  
         printf("%13d  Not processed\n", i);  
         break;  
  
      case SQL_PARAM_DIAG_UNAVAILABLE:  
         printf("%13d  Unknown\n", i);  
         break;  
  
   }  
}  
```  
  
## <a name="row-wise-binding"></a>行方向のバインド  
 行方向のバインドを使用する場合、アプリケーションは、各パラメーターのセットの構造を定義します。 構造体には、各パラメーターの 1 つまたは 2 つの要素が含まれています。 最初の要素は、パラメーターの値を保持し、2 番目の要素が長さ/インジケーター バッファーを保持します。 その後、アプリケーションでは、各パラメーターの値と同じ数の要素を含むこれらの構造体の配列を割り当てます。  
  
 アプリケーションは、SQL_ATTR_PARAM_BIND_TYPE ステートメント属性を持つドライバーに構造体のサイズを宣言します。 アプリケーションでは、配列の最初の構造体で、パラメーターのアドレスをバインドします。 そのため、ドライバーが特定の行と列のデータのアドレスを計算できます。  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size) + Offset  
```  
  
 パラメーターのサイズに行が 1 から番号を設定します。 オフセットを定義されている場合は、SQL_ATTR_PARAM_BIND_OFFSET_PTR ステートメント属性によって示される値です。 次の図は、行方向のバインドの動作を示します。 パラメーターは、任意の順序で構造内に配置することができますが、わかりやすくするための順番に表示されます。  
  
 ![表示行&#45;ごとの連結の動作が](../../../odbc/reference/develop-app/media/pr32.gif "pr32")  
  
 次のコードでは、PartID、説明、および価格の列に格納する値の要素を持つ構造体を作成します。 これらの構造体の 10 要素を配列し、行方向のバインドを使用して、PartID、説明、および Price 列のパラメーターにバインドされます。 10 個の行を挿入するステートメントを実行します。  
  
```  
#define DESC_LEN 51  
#define ARRAY_SIZE 10  
  
typedef tagPartStruct {  
   SQLREAL       Price;  
   SQLUINTEGER   PartID;  
   SQLCHAR       Desc[DESC_LEN];  
   SQLINTEGER    PriceInd;  
   SQLINTEGER    PartIDInd;  
   SQLINTEGER    DescLenOrInd;  
} PartStruct;  
  
PartStruct PartArray[ARRAY_SIZE];  
SQLCHAR *      Statement = "INSERT INTO Parts (PartID, Description,  
                Price) "  
               "VALUES (?, ?, ?)";  
SQLUSMALLINT   i, ParamStatusArray[ARRAY_SIZE];  
SQLULEN ParamsProcessed;  
  
// Set the SQL_ATTR_PARAM_BIND_TYPE statement attribute to use  
// column-wise binding.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_BIND_TYPE, sizeof(PartStruct), 0);  
  
// Specify the number of elements in each parameter array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, ARRAY_SIZE, 0);  
  
// Specify an array in which to return the status of each set of  
// parameters.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_STATUS_PTR, ParamStatusArray, 0);  
  
// Specify an SQLUINTEGER value in which to return the number of sets of  
// parameters processed.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, &ParamsProcessed, 0);  
  
// Bind the parameters in row-wise fashion.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartArray[0].PartID, 0, &PartArray[0].PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  PartArray[0].Desc, DESC_LEN, &PartArray[0].DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &PartArray[0].Price, 0, &PartArray[0].PriceInd);  
  
// Set part ID, description, and price.  
for (i = 0; i < ARRAY_SIZE; i++) {  
   GetNewValues(&PartArray[i].PartID, PartArray[i].Desc, &PartArray[i].Price);  
   PartArray[0].PartIDInd = 0;  
   PartArray[0].DescLenOrInd = SQL_NTS;  
   PartArray[0].PriceInd = 0;  
}  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Check to see which sets of parameters were processed successfully.  
for (i = 0; i < ParamsProcessed; i++) {  
   printf("Parameter Set  Status\n");  
   printf("-------------  -------------\n");  
   switch (ParamStatusArray[i]) {  
      case SQL_PARAM_SUCCESS:  
      case SQL_PARAM_SUCCESS_WITH_INFO:  
         printf("%13d  Success\n", i);  
         break;  
  
      case SQL_PARAM_ERROR:  
         printf("%13d  Error\n", i);  
         break;  
  
      case SQL_PARAM_UNUSED:  
         printf("%13d  Not processed\n", i);  
         break;  
  
      case SQL_PARAM_DIAG_UNAVAILABLE:  
         printf("%13d  Unknown\n", i);  
         break;  
  
   }  
```
