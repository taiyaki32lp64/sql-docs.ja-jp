---
title: 割り当てと解放バッファー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- buffers [ODBC], allocating and freeing
- allocating buffers [ODBC]
- freeing buffers [ODBC]
ms.assetid: 886bc9ed-39d4-43d2-82ff-aebc35b14d39
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b783c2fc6766f0e2d2685724169894160c15ffc9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077193"
---
# <a name="allocating-and-freeing-buffers"></a>バッファーの割り当てと解放
すべてのバッファーに割り当てられ、アプリケーションによって解放されます。 バッファーが遅延しない場合は必要があります関数の呼び出しの期間中のみ存在します。 たとえば、 **SQLGetInfo**によって指し示されるバッファー内の特定のオプションに関連付けられている値を返します、 *InfoValuePtr*引数。 呼び出し後すぐにこのバッファーを解放できる**SQLGetInfo**次のコード例のように。  
  
```  
SQLSMALLINT   InfoValueLen;  
SQLCHAR *     InfoValuePtr = malloc(50);   // Allocate InfoValuePtr.  
  
SQLGetInfo(hdbc, SQL_DBMS_NAME, (SQLPOINTER)InfoValuePtr, 50,  
            &InfoValueLen);  
  
free(InfoValuePtr);                        // OK to free InfoValuePtr.  
```  
  
 遅延バッファーは 1 つの関数で指定された、他で使用されるため、ドライバーがまだ期待したに存在するときに、遅延バッファーを解放するために、アプリケーション プログラミング エラーになります。 アドレスなど、 \* *ValuePtr*に渡されるバッファー **SQLBindCol**によって後で使用できる**SQLFetch**します。 列がへの呼び出しのようにバインドされた、まで、このバッファーを解放できません**SQLBindCol**または**SQLFreeStmt**次のコード例に示すようにします。  
  
```  
SQLRETURN    rc;  
SQLINTEGER   ValueLenOrInd;  
SQLHSTMT     hstmt;  
  
// Allocate ValuePtr  
SQLCHAR * ValuePtr = malloc(50);  
  
// Bind ValuePtr to column 1. It is an error to free ValuePtr here.  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, 50, &ValueLenOrInd);  
  
// Fetch each row of data and place the value for column 1 in *ValuePtr.  
// Code to check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO   
// not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   // It is an error to free ValuePtr here.  
}  
  
// Unbind ValuePtr from column 1.  It is now OK to free ValuePtr.  
SQLFreeStmt(hstmt, SQL_UNBIND);  
free(ValuePtr);  
```  
  
 このようなエラーが; 関数でローカルにバッファーを宣言することで簡単に行われました。バッファーは、アプリケーションが、関数を離れるときに解放されます。 たとえば、次のコードでは、ドライバーで未定義とおそらく致命的な動作がなります。  
  
```  
SQLRETURN   rc;  
SQLHSTMT    hstmt;  
  
BindAColumn(hstmt);  
  
// Fetch each row of data and try to place the value for column 1 in  
// *ValuePtr. Because ValuePtr has been freed, the behavior is undefined  
// and probably fatal. Code to check if rc equals SQL_ERROR or   
// SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {}  
  
   .  
   .  
   .  
  
void BindAColumn(SQLHSTMT hstmt)  // WARNING! This function won't work!  
{  
   // Declare ValuePtr locally.  
   SQLCHAR      ValuePtr[50];  
   SQLINTEGER   ValueLenOrInd;  
  
   // Bind rgbValue to column.  
   SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr),  
               &ValueLenOrInd);  
  
   // ValuePtr is freed when BindAColumn exits.  
}  
```
