---
title: SQL Server の例を参照 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBrowseConnect function [ODBC], example
- connecting to data source [ODBC], SqlBrowseConnect
- connecting to driver [ODBC], SQLBrowseConnect
ms.assetid: 6e0d5fd1-ec93-4348-a77a-08f5ba738bc6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3f3a7568c0849844526ef5f172bcecc0a5857268
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114327"
---
# <a name="sql-server-browsing-example"></a>SQL Server の参照の例
次の例はどのように**SQLBrowseConnect** for SQL Server ドライバーで使用可能な接続を参照する場合に使用します。 最初に、アプリケーションは、接続ハンドルを要求します。  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 次に、アプリケーション呼び出し**SQLBrowseConnect**によって返されるドライバーの名前を使用して、SQL Server ドライバーを指定します、 **SQLDrivers**:  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 これは、最初の呼び出しなので**SQLBrowseConnect**、ドライバー マネージャーが、SQL Server ドライバーを読み込むし、ドライバーの呼び出し**SQLBrowseConnect**から受け取った同じ引数で関数をアプリケーション。  
  
> [!NOTE]  
>  指定する必要があります Windows 認証をサポートするデータ ソース プロバイダーに接続するかどうか、`Trusted_Connection=yes`接続文字列でユーザー ID とパスワードの情報の代わりにします。  
  
 ドライバーでは、最初の呼び出しであるかを決定します。 **SQLBrowseConnect**し、接続属性の 2 番目のレベルを返します: サーバー、ユーザー名、パスワード、アプリケーション名、およびワークステーションの id。 サーバーの属性の有効なサーバー名の一覧を返します。 リターン コード**SQLBrowseConnect** SQL_NEED_DATA です。 参照結果の文字列を次に示します。  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 参照結果の文字列内の各キーワードは、コロンと等号 (=) の前に 1 つまたは複数の単語続きます。 これらの単語は、アプリケーションがビルド ダイアログ ボックスを使用できるわかりやすい名前です。 **アプリ**と**WSID**キーワードの意味は必須では、アスタリスクが付きます。 **SERVER**、 **UID**、および**PWD**キーワードのプレフィックスは、アスタリスクは、[次へ] の参照要求の文字列でそれらの値を指定する必要があります。 値、 **SERVER**によって返されるサーバーのいずれかのキーワードがあります**SQLBrowseConnect**またはユーザーが指定した名前。  
  
 アプリケーション呼び出し**SQLBrowseConnect**もう一度、緑色のサーバーを指定して、省略すると、**アプリ**と**WSID**キーワードと各キーワードの後に、わかりやすい名前。  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 ドライバーは、緑色のサーバーに接続しようとします。 不足しているキーワードと値のペアなどの致命的でないエラーがある場合**SQLBrowseConnect** SQL_NEED_DATA が返され、エラーが起こる前と同じ状態のままです。 アプリケーションを呼び出して**SQLGetDiagField**または**SQLGetDiagRec**エラーを確認します。 接続が成功した場合、ドライバーが SQL_NEED_DATA を返し、参照の結果文字列を返します。  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 この文字列内の属性は省略可能であるために、アプリケーションは、これらを省略できます。 ただし、アプリケーションを呼び出す必要があります**SQLBrowseConnect**もう一度です。 アプリケーションの言語とデータベースの名前を省略する場合、空の参照要求文字列を指定します。 Pubs データベースおよび呼び出し、この例では、アプリケーションを選択**SQLBrowseConnect**最後に、省略すると、**言語**キーワードとアスタリスクの前に、**データベース**キーワード。  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 **データベース**属性は、ドライバーで必要な最後の接続属性、参照の処理が完了したら、アプリケーションがデータ ソースに接続されていると**SQLBrowseConnect**SQL_SUCCESS を返します。 **SQLBrowseConnect**も参照結果の文字列として完全な接続文字列を返します。  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 ドライバーによって返される最終的な接続文字列は、それぞれのキーワードの後にわかりやすい名前を含まないも、アプリケーションで指定されていない省略可能なキーワードを含んでいるか。 アプリケーションでは、この文字列を使用します。 **SQLDriverConnect** (切断) 後の現在の接続ハンドル上のデータ ソースに再接続するか、異なる接続ハンドルのデータ ソースに接続します。 例:  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
