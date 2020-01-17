---
title: Windows ODBC ドライバーの接続の回復性 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 614fa0b4-e9fd-4c68-aab3-183f9b9df143
author: MightyPen
ms.author: genemi
ms.openlocfilehash: eecf4868791a9dcd963a31963f742f90a2cf3843
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008434"
---
# <a name="connection-resiliency-in-the-windows-odbc-driver"></a>Windows ODBC ドライバーの接続レジリエンシー
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  確実にアプリケーションを [!INCLUDE[ssAzure](../../../includes/ssazure_md.md)]に接続されたままにするため、Windows 上の ODBC ドライバーは、アイドル状態の接続を復元できます。  
  
> [!IMPORTANT]  
>  接続の復元機能は Microsoft Azure SQL データベースと SQL Server 2014 (以降) サーバー バージョンでご利用いただけます。  
  
 アイドル接続の回復性について詳しくは、「[Technical Article - Idle Connection Resiliency](https://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/Idle%20Connection%20Resiliency.docx)」 (技術記事 - アイドル接続の回復性) をご覧ください。
  
 Windows の場合、ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には再接続動作を変更する方法が 2 つあります。  
  
-   接続の再試行回数。  
  
     接続の再試行回数は、接続に障害が発生した場合の再接続試行回数を決定します。 有効な値の範囲は 0 ～ 255 です。 ゼロ (0) の場合、再接続は試行されません。 既定の再接続試行数は 1 です。  
  
     次の場合に接続再試行回数を変更できます。  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 接続の再試行回数 **制御で ODBC Driver for** を使用するデータ ソースを定義または変更する。  
  
    -   **ConnectRetryCount** 接続文字列キーワードを使用する。  
  
     接続の再試行回数を取得するには、**SQL_COPT_SS_CONNECT_RETRY_COUNT** (読み取り専用) 接続属性を使用します。 接続の回復性をサポートしていないサーバーにアプリケーションが接続する場合、**SQL_COPT_SS_CONNECT_RETRY_COUNT** は 0 を返します。  
  
-   接続の再試行間隔。  
  
     接続の再試行間隔では、接続再試行間の秒数が指定されます。 有効な値は 1 から 60 までです。 再接続の合計時間は接続タイムアウトを超過できません (SQLSetStmtAttr の SQL_ATTR_QUERY_TIMEOUT)。 既定値は 10 秒です。  
  
     次の場合に接続再試行間隔を変更できます。  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 接続の再試行間隔 **制御で ODBC Driver for** を使用するデータ ソースを定義または変更する。  
  
    -   **ConnectRetryInterval** 接続文字列キーワードを使用する。  
  
     接続の再試行間隔の長さを取得するには、**SQL_COPT_SS_CONNECT_RETRY_INTERVAL** (読み取り専用) 接続属性を使用します。  
  
 アプリケーションが SQL_DRIVER_COMPLETE_REQUIRED で接続を確立し、後で、途切れた接続でステートメントを実行しようとする場合、ODBC ドライバーはダイアログ ボックスを再度表示しません。 回復の進行中にもです。  
  
-   回復中は、**SQLGetConnectAttr(SQL_COPT_SS_CONNECTION_DEAD)** が呼び出されたとき、**SQL_CD_FALSE** が返されるようにします。  
  
-   回復できなかった場合、**SQLGetConnectAttr(SQL_COPT_SS_CONNECTION_DEAD)** が呼び出されたとき、**SQL_CD_TRUE** が返されるようにします。  
  
 次の状態コードは、サーバーでコマンドを実行する関数から返されます。  
  
|状態|メッセージ|  
|-----------|-------------|  
|IMC01|接続が切断され、復旧は不可能です。 クライアント ドライバーは接続の復旧を 1 回または複数回試行しましたが、すべて失敗しました。 復旧試行数を増やすには、ConnectRetryCount の値を増やします。|  
|IMC02|サーバーは復旧試行を認識しませんでした。接続復旧は不可能です。|  
|IMC03|サーバーは、復旧試行中、要求されたクライアント TDS バージョンを正確に保存しませんでした。接続復旧は不可能です。|  
|IMC04|サーバーは、復旧試行中、要求されたサーバー メジャー バージョンを正確に保存しませんでした。接続復旧は不可能です。|  
|IMC05|接続が切断され、復旧は不可能です。 サーバーは接続を復旧不可能としてマークしています。 接続復旧は試行されませんでした。|  
|IMC06|接続が切断され、復旧は不可能です。 クライアント ドライバーは接続を復旧不可能としてマークしています。 接続復旧は試行されませんでした。|  
  
## <a name="example"></a>例  
 次の例には、2 つの関数が含まれています。 **func1** は、Windows の場合に、ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を使用するデータ ソース名 (DSN) で接続する方法を示しています。 DSN は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証を使用し、ユーザー ID を指定します。 **func1**は、 **SQL_COPT_SS_CONNECT_RETRY_COUNT**による接続再試行の回数を取得します。  
  
 **func2** は **SQLDriverConnect**、 **ConnectRetryCount** 接続文字列キーワード、接続属性を使用し、接続再試行と再試行間隔の設定を取得します。  
  
```  
// Connection_resiliency.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
#include <sqlext.h>  
#include <msodbcsql.h>  
  
void func1() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
   SQLSMALLINT i = 21;  

   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLCHAR*) "MyDSN", SQL_NTS, (SQLCHAR*) "userID", SQL_NTS, (SQLCHAR*) "password_for_userID", SQL_NTS);  
            retcode = SQLGetConnectAttr(hdbc, SQL_COPT_SS_CONNECT_RETRY_COUNT, &i, SQL_IS_INTEGER, NULL);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}
  
void func2() {  
   SQLHENV henv;  
   SQLHDBC hdbc1;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
   SQLSMALLINT i = 21;  
  
#define MAXBUFLEN 255  
  
   SQLCHAR ConnStrIn[MAXBUFLEN] = "DRIVER={ODBC Driver 13 for SQL Server};SERVER=server_that_supports_connection_resiliency;UID=userID;PWD= password_for_userID;ConnectRetryCount=2";
   SQLCHAR ConnStrOut[MAXBUFLEN];

   SQLSMALLINT cbConnStrOut = 0;  
 
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3_80, SQL_IS_INTEGER);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            // SQLSetConnectAttr(hdbc1, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            retcode = SQLDriverConnect(hdbc1, NULL, ConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
         }  
         retcode = SQLGetConnectAttr(hdbc1, SQL_COPT_SS_CONNECT_RETRY_COUNT, &i, SQL_IS_INTEGER, NULL);  
         retcode = SQLGetConnectAttr(hdbc1, SQL_COPT_SS_CONNECT_RETRY_INTERVAL, &i, SQL_IS_INTEGER, NULL);  
      }  
   }  
}  
  
int main() {  
   func1();  
   func2();  
}  
```  
  
## <a name="see-also"></a>参照  
 [Microsoft ODBC Driver for SQL Server on Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
