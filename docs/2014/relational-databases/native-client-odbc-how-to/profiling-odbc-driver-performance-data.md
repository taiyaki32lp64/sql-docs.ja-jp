---
title: (ODBC) ドライバーのパフォーマンス データをプロファイル |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- driver performance data [ODBC]
ms.assetid: b997790a-8cc6-4800-8867-74c1bef07be3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7de38f3c91814dbd364caee84b34dacdfbdf475
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200306"
---
# <a name="profile-driver-performance-data-odbc"></a>ドライバーのパフォーマンス データのプロファイル (ODBC)
  このサンプルでは、パフォーマンス統計を記録するための [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC ドライバー固有のオプションを示します。 サンプルは、1 つのファイルを作成します: odbcperf.log.This サンプル (SQLPERF 構造体は Odbcss.h で定義されます). SQLPERF データ構造体から直接パフォーマンス データの表示、パフォーマンス データのログ ファイルの作成を示しています。 このサンプルは、ODBC 3.0 以降のバージョン用に開発されました。  
  
> [!IMPORTANT]  
>  可能な場合は、Windows 認証を使用します。 Windows 認証が使用できない場合は、実行時に資格情報を入力するようユーザーに求めます。 資格情報をファイルに保存するのは避けてください。 資格情報を保持する必要がある場合は、[Win32 Crypto API](https://go.microsoft.com/fwlink/?LinkId=64532) を使用して暗号化してください。  
  
### <a name="to-log-driver-performance-data-using-odbc-administrator"></a>ODBC アドミニストレーターを使用してドライバーのパフォーマンス データをログに記録するには  
  
1.  **コントロール パネルの [** 、] をダブルクリックします**管理ツール**し、ダブルクリック**データ ソース (ODBC)** します。 または、odbcad32.exe を呼び出すことができます。  
  
2.  をクリックして、**ユーザー DSN**、**システム DSN**、または**ファイル DSN**タブ。  
  
3.  パフォーマンスのログを記録するデータ ソースをクリックします。  
  
4.  をクリックして**構成**です。  
  
5.  Microsoft SQL Server を構成する DSN ウィザードで、ページに移動します。**ログ ODBC ドライバーの統計情報、ログ ファイルに**します。  
  
6.  選択**ログ ODBC ドライバーの統計情報、ログ ファイルに**します。 ボックスに、統計をログに記録するファイルの名前を入力します。 必要に応じてクリックして**参照**ファイル システムの統計ログを参照します。  
  
### <a name="to-log-driver-performance-data-programmatically"></a>ドライバーのパフォーマンス データをプログラムを使用してログに記録するには  
  
1.  呼び出す[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) SQL_COPT_SS_PERF_DATA_LOG およびパフォーマンス データのログ ファイルの完全なパスとファイル名にします。 例 :  
  
    ```  
    "C:\\Odbcperf.log"  
    ```  
  
2.  呼び出す[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md)パフォーマンス データのログ記録を開始するには、SQL_COPT_SS_PERF_DATA および SQL_PERF_START を使用します。  
  
3.  必要に応じて、呼び出す[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) SQL_COPT_SS_LOG_NOW および NULL パフォーマンス データのログ ファイルにパフォーマンス データをタブ区切りのレコードを書き込めません。 これは、アプリケーションの実行時に複数回実行できます。  
  
4.  呼び出す[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) SQL_COPT_SS_PERF_DATA および SQL_PERF_STOP をパフォーマンス データのログ記録を停止するとします。  
  
### <a name="to-pull-driver-performance-data-into-an-application"></a>ドライバーのパフォーマンス データをアプリケーションにプルするには  
  
1.  呼び出す[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md)パフォーマンス データのプロファイリングを開始するには、SQL_COPT_SS_PERF_DATA および SQL_PERF_START を使用します。  
  
2.  呼び出す[SQLGetConnectAttr](../native-client-odbc-api/sqlgetconnectattr.md) SQL_COPT_SS_PERF_DATA および SQLPERF 構造体へのポインターのアドレスを使用します。 最初の呼び出しでは、現在のパフォーマンス データを含む有効な SQLPERF 構造体のアドレスを指すポインターが設定されます。 ドライバーは、パフォーマンス構造体内のデータを継続的に更新しません。 アプリケーションへの呼び出しを繰り返す必要があります[SQLGetConnectAttr](../native-client-odbc-api/sqlgetconnectattr.md)より現在のパフォーマンス データの構造体を更新する必要がある任意の時間。  
  
3.  呼び出す[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) SQL_COPT_SS_PERF_DATA および SQL_PERF_STOP をパフォーマンス データのログ記録を停止するとします。  
  
## <a name="example"></a>例  
 AdventureWorks と呼ばれる ODBC データ ソース (既定のデータベースは AdventureWorks サンプル データベース) が必要です (AdventureWorks サンプル データベースは、[Microsoft SQL Server のサンプルとコミュニティのプロジェクト](https://go.microsoft.com/fwlink/?LinkID=85384)のホーム ページからダウンロードできます)。このデータ ソースには、オペレーティング システムに用意されている ODBC ドライバーが使用されている必要があります (ドライバー名は "SQL Server")。 このサンプルを 64 ビット オペレーティング システムで 32 ビット アプリケーションとしてビルドし、実行する場合、%windir%\SysWOW64\odbcad32.exe の ODBC アドミニストレーターを使用して ODBC データ ソースを作成する必要があります。  
  
 このサンプルでは、コンピューターの既定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続します。 名前付きインスタンスに接続するには、ODBC データ ソースの定義を変更し、server\namedinstance 形式でそのインスタンスを指定します。 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] は、既定で名前付きインスタンスとしてインストールされます。  
  
 odbc32.lib を使用してコンパイルします。  
  
```  
// compile with: odbc32.lib  
#include <stdio.h>  
#include <string.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
SQLHENV henv = SQL_NULL_HENV;  
SQLHDBC hdbc1 = SQL_NULL_HDBC;       
SQLHSTMT hstmt1 = SQL_NULL_HSTMT;  
  
void Cleanup() {  
   if (hstmt1 != SQL_NULL_HSTMT)  
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
  
   // Pointer to the ODBC driver performance structure.  
   SQLPERF *PerfPtr;  
   SQLINTEGER cbPerfPtr;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // This sample use Integrated Security. Please create the SQL Server   
   // DSN by using the Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Set options to log performance statistics.  Specify file to use for the log.  
   retcode = SQLSetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA_LOG, &"odbcperf.log", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLSetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Start the performance statistics log.  
   retcode =   
      SQLSetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA, (SQLPOINTER)SQL_PERF_START, SQL_IS_UINTEGER);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLSetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate statement handle, then execute command.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLAllocHandle() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"SELECT * FROM Purchasing.Vendor", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA ) {  
      if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLMoreResults() Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"SELECT * FROM Sales.Store", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA ) {  
      if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLMoreResults() Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   // Generate a long-running query.  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"waitfor delay '00:00:04' ", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA ) {  
      if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLMoreResults() Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   // Write current statistics to the performance log.  
   retcode =   
      SQLSetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA_LOG_NOW, (SQLPOINTER)NULL, SQL_IS_UINTEGER);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLSetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Get pointer to current SQLPerf structure.  
   // Print a couple of statistics.  
   retcode =   
      SQLGetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA, (SQLPOINTER)&PerfPtr, SQL_IS_POINTER, &cbPerfPtr);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLGetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   printf("SQLSelects = %d, SQLSelectRows = %d\n", PerfPtr->SQLSelects, PerfPtr->SQLSelectRows);  
  
   // Cleanup  
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="see-also"></a>参照  
 [ODBC ドライバーのパフォーマンスに関するトピックをプロファイリング&#40;ODBC&#41;](profiling-odbc-driver-performance-odbc.md)   
 [ODBC ドライバー パフォーマンスのプロファイル](../native-client/odbc/profiling-odbc-driver-performance.md)  
  
  
