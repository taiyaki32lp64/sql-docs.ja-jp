---
title: ハンドルの割り当て (ODBC) の SQL Server に接続および |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- handles [ODBC]
- handles [ODBC], connection
- handles [ODBC], about handles
ms.assetid: 6172cd52-9c9a-467d-992f-def07f3f3bb1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 322120624c612371b56029c2cf29c9ab457c81b5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63225499"
---
# <a name="allocate-handles-and-connect-to-sql-server-odbc"></a>ハンドルの割り当てと SQL Server への接続 (ODBC)
    
### <a name="to-allocate-handles-and-connect-to-sql-server"></a>ハンドルを割り当てて SQL Server に接続するには  
  
1.  ODBC ヘッダー ファイル Sql.h、Sqlext.h、Sqltypes.h を含めます。  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ドライバー固有のヘッダー ファイル Odbcss.h を含めます。  
  
3.  呼び出す[SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396)で、`HandleType`を ODBC を初期化して環境ハンドルを割り当てる sql_handle_env としての。  
  
4.  呼び出す[SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md)で`Attribute`SQL_ATTR_ODBC_VERSION に設定し、`ValuePtr`を ODBC 3.x 形式の関数呼び出しで使用するアプリケーションを示す SQL_OV_ODBC3 に設定します。  
  
5.  必要に応じて、呼び出す[SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md)他の環境を設定するオプション、または呼び出し[SQLGetEnvAttr](https://go.microsoft.com/fwlink/?LinkId=58403)環境オプションを取得します。  
  
6.  呼び出す[SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396)で、`HandleType`接続ハンドルの割り当てを sql_handle_dbc としての。  
  
7.  必要に応じて、呼び出す[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md)接続オプションの設定、または呼び出し[SQLGetConnectAttr](../native-client-odbc-api/sqlgetconnectattr.md)接続オプションを取得します。  
  
8.  接続する既存のデータ ソースを使用する SQLConnect を呼び出す[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
     または  
  
     呼び出す[SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md)に接続する接続文字列を使用する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
     最小の完全な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続文字列は、次の 2 つの形式のいずれかになります。  
  
    ```  
    DSN=dsn_name;Trusted_connection=yes;  
    DRIVER={SQL Server Native Client 10.0};SERVER=server;Trusted_connection=yes;  
    ```  
  
     接続文字列が完全でない場合は、`SQLDriverConnect` によって必要な情報の入力が要求される場合があります。 指定された値によって制御されます、 *DriverCompletion*パラメーター。  
  
     \- - または -  
  
     呼び出す[SQLBrowseConnect](../native-client-odbc-api/sqlbrowseconnect.md)接続文字列を作成しに接続する、反復的な方法で複数回[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
9. 必要に応じて、呼び出す[SQLGetInfo](../native-client-odbc-api/sqlgetinfo.md)ドライバーの属性と動作を取得する、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ ソース。  
  
10. ステートメントを割り当てて使用します。  
  
11. 呼び出しから切断する SQLDisconnect[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]接続ハンドルを新しい接続で使用できるようにします。  
  
12. 呼び出す[SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md)で、`HandleType`の sql_handle_dbc として接続ハンドルを解放します。  
  
13. `SQLFreeHandle` を SQL_HANDLE_ENV として `HandleType` を呼び出し、環境ハンドルを解放します。  
  
> [!IMPORTANT]  
>  可能な場合は、Windows 認証を使用します。 Windows 認証が使用できない場合は、実行時に資格情報を入力するようユーザーに求めます。 資格情報をファイルに保存するのは避けてください。 資格情報を保持する必要がある場合は、[Win32 Crypto API](https://go.microsoft.com/fwlink/?LinkId=64532) を使用して暗号化してください。  
  
## <a name="example"></a>例  
 次の例では、`SQLDriverConnect` を呼び出して、既存の ODBC データ ソースを要求せずに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続する方法を示しています。 不完全な接続文字列を `SQLDriverConnect` に渡すと、ODBC ドライバーから不足情報を入力するように要求されます。  
  
```  
#define MAXBUFLEN   255  
  
SQLHENV      henv = SQL_NULL_HENV;  
SQLHDBC      hdbc1 = SQL_NULL_HDBC;  
SQLHSTMT      hstmt1 = SQL_NULL_HSTMT;  
  
SQLCHAR      ConnStrIn[MAXBUFLEN] =  
         "DRIVER={SQL Server Native Client 10.0};SERVER=MyServer";  
  
SQLCHAR      ConnStrOut[MAXBUFLEN];  
SQLSMALLINT   cbConnStrOut = 0;  
  
// Make connection without data source. Ask that driver   
// prompt if insufficient information. Driver returns  
// SQL_ERROR and application prompts user  
// for missing information. Window handle not needed for  
// SQL_DRIVER_NOPROMPT.  
retcode = SQLDriverConnect(hdbc1,      // Connection handle  
                  NULL,         // Window handle  
                  ConnStrIn,      // Input connect string  
                  SQL_NTS,         // Null-terminated string  
                  ConnStrOut,      // Address of output buffer  
                  MAXBUFLEN,      // Size of output buffer  
                  &cbConnStrOut,   // Address of output length  
                  SQL_DRIVER_PROMPT);  
```  
  
  
