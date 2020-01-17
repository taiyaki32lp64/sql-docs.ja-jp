---
title: 長さとインジケーターの値を使用して |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- length/indicator buffers [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 849792f1-cb1e-4bc2-b568-c0aff0b66199
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b3a0b54617d55033addabc729adbd078680022fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902469"
---
# <a name="using-length-and-indicator-values"></a>長さとインジケーターの値の使用
長さ/インジケーター バッファーを使用して、データ バッファーまたは SQL_NULL_DATA、データが NULL であることを示すなどの特殊なインジケーター内のデータのバイトの長さを渡します。 によって使用されている関数は、長さ/インジケーター バッファーは、SQLINTEGER または、SQLSMALLINT に定義されます。 そのため、1 つの引数は、説明に必要です。 データ バッファーが使用中として入力バッファーの場合は、この引数には、データ自体のバイトの長さまたはインジケーターの値が含まれます。 という名前が多くの場合、 *StrLen_or_Ind*または類似する名前。 たとえば、次のコード呼び出し**SQLPutData**バッファーを渡すデータの完全な; バイトの長さ (*ValueLen*) ため、直接渡されるデータ バッファー (*ValuePtr*) は、入力バッファー。  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLen;  
  
// Call local function to place data in ValuePtr. In ValueLen, return the  
// number of bytes of data placed in ValuePtr. If there is not enough  
// data, this will be less than 50.  
FillBuffer(ValuePtr, sizeof(ValuePtr), &ValueLen);  
  
// Call SQLPutData to send the data to the driver.  
SQLPutData(hstmt, ValuePtr, ValueLen);  
```  
  
 データ バッファーが遅延の入力バッファー、遅延の出力バッファーまたは出力バッファーの場合は、引数には、長さ/インジケーター バッファーのアドレスが含まれています。 という名前が多くの場合、 *StrLen_or_IndPtr*または類似する名前。 たとえば、次のコード呼び出し**SQLGetData**データの完全なバッファーを取得するバイトの長さが長さ/インジケーター バッファー内のアプリケーションに返されます (*ValueLenOrInd*)、住所が渡される**SQLGetData**ため、対応するデータ バッファー (*ValuePtr*) は、使用中として出力バッファー。  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 具体的には禁止されている場合を除き、長さ/インジケーター バッファーの引数は 0 を指定できます (場合遅延の入力) または null ポインター (場合や遅延の入力と出力)。 入力バッファーの場合、これによりデータのバイトの長さを無視するドライバーです。 これは、可変長データを渡すときにエラーが返されますが、ので一般的では、null 以外の固定長のデータを渡すときに、長さもインジケーターの値が必要です。 出力バッファーの場合、これにより、データまたはインジケーターの値のバイトの長さは返されないドライバーです。 これは、ドライバーによって返されるデータは NULL ですので一般的では、null 非許容の固定長のデータを取得するときに、長さもインジケーターの値が必要な場合のエラーです。  
  
 遅延のデータ バッファーのアドレスがドライバーに渡された場合、としては、バッファーのバインドが解除されるまでに遅延の長さ/インジケーター バッファーのアドレスが有効する必要がありますあります。  
  
 次の長さは長さまたはインジケーターの値として有効です。  
  
-   *n*ここで、 *n* > 0。  
  
-   0.  
  
-   SQL_NTS します。 対応するデータ バッファー内のドライバーに送信された文字列が null で終わるこれは、そのバイトの長さを計算することがなく文字列を渡す C プログラマのための便利な方法です。 この値は、アプリケーション、ドライバーにデータを送信する場合にのみです。 ドライバーでは、アプリケーションにデータが返される、ときに常に、データの実際のバイトの長さを返します。  
  
 次の値の長さまたはインジケーターの値として有効です。 SQL_NULL_DATA が SQL_DESC_INDICATOR_PTR 記述子フィールドに格納されています。その他のすべての値は、SQL_DESC_OCTET_LENGTH_PTR 記述子 フィールドに格納されます。  
  
-   SQL_NULL_DATA します。 データは、NULL データ値、および対応するデータ バッファー内の値は無視されます。 この値は、SQL データを送信、またはドライバーから取得に対してのみ有効です。  
  
-   SQL_DATA_AT_EXEC です。 データ バッファーにデータが含まれていません。 データを送信する代わりに、 **SQLPutData** 、ステートメントが実行されるとき、または**SQLBulkOperations**または**SQLSetPos**が呼び出されます。 この値は、ドライバーに送信される SQL データに対してのみ有効です。 詳細については、次を参照してください。 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)、 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)、および[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)します。  
  
-   結果の SQL_LEN_DATA_AT_EXEC (*長さ*) マクロです。 この値は、SQL_DATA_AT_EXEC に似ています。 詳細については、次を参照してください。[長い形式のデータを送信する](../../../odbc/reference/develop-app/sending-long-data.md)します。  
  
-   SQL_NO_TOTAL します。 ドライバーは、まだ、出力バッファーに返される長い形式のデータのバイト数を判断できません。 この値は、ドライバーから取得した SQL データに対してのみ有効です。  
  
-   SQL_DEFAULT_PARAM します。 プロシージャでは、対応するデータ バッファー内の値ではなくプロシージャの入力パラメーターの既定値を使用します。  
  
-   SQL_COLUMN_IGNORE します。 **SQLBulkOperations**または**SQLSetPos**データ バッファー内の値を無視します。 呼び出しによってデータの行を更新するときに**SQLBulkOperations**または**SQLSetPos、** 列の値は変更されません。 呼び出しによって新しいデータの行を挿入するときに**SQLBulkOperations**列の値がその既定値に設定または、列には、null、既定値はありません。
