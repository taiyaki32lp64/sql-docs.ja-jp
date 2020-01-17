---
title: SQLGetData |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetData function
ms.assetid: 204848be-8787-45b4-816f-a60ac9d56fcf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 048ee2d27445bf64839c5331627a12e012cd4123
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193305"
---
# <a name="sqlgetdata"></a>SQLGetData
  **SQLGetData**列の値をバインドしないで結果セットのデータを取得するために使用します。 **SQLGetData**列から大量のデータを取得する同じ列に連続して呼び出すことができます、**テキスト**、 **ntext**、または**イメージ**データ型。  
  
 アプリケーションでは、変数をバインドして結果セット データをフェッチする必要はありません。 任意の列のデータを取得できる、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーを使用して**SQLGetData**します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、使用はサポートしません**SQLGetData**ランダムな列の順序でデータを取得します。 バインドされていないすべての列が処理される**SQLGetData**結果セットにバインドされた列数よりも高い列の序数を指定する必要があります。 アプリケーションでは、バインドされていない列の値を、列序数の小さい列から大きい列へと処理する必要があります。 前に処理した列よりも列序数が小さい列からデータを取得しようとすると、エラーが発生します。 アプリケーションで、結果セット行を報告するためにサーバー カーソルを使用している場合は、現在の行を再フェッチしてから列の値をフェッチできます。 既定の読み取り専用、順方向専用カーソルで、ステートメントを実行すると場合、は、バックアップするステートメントを再実行する必要があります**SQLGetData**します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーの長さを正確に報告する**テキスト**、 **ntext**、および**イメージ**データを使用して取得**SQLGetData**. アプリケーションの適切な使い方をすることができます、 *StrLen_or_IndPtr*長い形式のデータを迅速に取得するパラメーターを返します。  
  
> [!NOTE]  
>  大きな値型、 *StrLen_or_IndPtr*ケース データの切り捨ての SQL_NO_TOTAL が返されます。  
  
## <a name="sqlgetdata-support-for-enhanced-date-and-time-features"></a>SQLGetData による機能強化された日付と時刻のサポート  
 説明されているように、日付/時刻型の結果列の値が変換されます[SQL から C への変換](../native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)します。  
  
 詳細については、次を参照してください。[日付と時刻の強化&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)します。  
  
## <a name="sqlgetdata-support-for-large-clr-udts"></a>SQLGetData による大きな CLR UDT のサポート  
 **SQLGetData**大きなの CLR ユーザー定義型 (Udt) をサポートしています。 詳細については、次を参照してください。 [Large CLR User-Defined 型&#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md)します。  
  
## <a name="example"></a>例  
  
```  
SQLHDBC     hDbc = NULL;  
SQLHSTMT    hStmt = NULL;  
long        lEmpID;  
PBYTE       pPicture;  
SQLINTEGER  pIndicators[2];  
  
// Get an environment, connection, and so on.  
...  
  
// Get a statement handle and execute a command.  
SQLAllocHandle(SQL_HANDLE_STMT, hDbc, &hStmt);  
  
if (SQLExecDirect(hStmt,  
    (SQLCHAR*) "SELECT EmployeeID, Photo FROM Employees",  
    SQL_NTS) == SQL_ERROR)  
    {  
    // Handle error and return.  
    }  
  
// Retrieve data from row set.  
SQLBindCol(hStmt, 1, SQL_C_LONG, (SQLPOINTER) &lEmpID, sizeof(long),  
    &pIndicators[0]);  
  
while (SQLFetch(hStmt) == SQL_SUCCESS)  
    {  
    cout << "EmployeeID: " << lEmpID << "\n";  
  
    // Call SQLGetData to determine the amount of data that's waiting.  
    if (SQLGetData(hStmt, 2, SQL_C_BINARY, pPicture, 0, &pIndicators[1])  
        == SQL_SUCCESS_WITH_INFO)  
        {  
        cout << "Photo size: " pIndicators[1] << "\n\n";  
  
        // Get all the data at once.  
        pPicture = new BYTE[pIndicators[1]];  
        if (SQLGetData(hStmt, 2, SQL_C_DEFAULT, pPicture,  
            pIndicators[1], &pIndicators[1]) != SQL_SUCCESS)  
            {  
            // Handle error and continue.  
            }  
  
        delete [] pPicture;  
        }  
    else  
        {  
        // Handle error on attempt to get data length.  
        }  
    }  
```  
  
## <a name="see-also"></a>参照  
 [SQLGetData 関数](https://go.microsoft.com/fwlink/?LinkId=59350)   
 [ODBC API 実装の詳細](odbc-api-implementation-details.md)  
  
  
