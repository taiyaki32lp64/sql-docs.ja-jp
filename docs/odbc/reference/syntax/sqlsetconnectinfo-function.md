---
title: SQLSetConnectInfo 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectInfo function [ODBC]
ms.assetid: 0782a1c3-c5d1-499b-a8ba-134162db9990
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5d8087e7672dd331d0b078cea4930be7582a026
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093004"
---
# <a name="sqlsetconnectinfo-function"></a>SQLSetConnectInfo 関数
**準拠**  
 バージョンが導入されました。ODBC 3.81 規格に準拠します。ODBC  
  
 **まとめ**  
 **SQLSetConnectInfo**のアプリケーションの接続情報のトークンに、データ ソース、ユーザーの ID とパスワードを設定するため[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)呼び出します。  
  
## <a name="syntax"></a>構文  
  
```cpp
  
SQLRETURN  SQLSetConnectInfo(  
                SQLHDBC_INFO_TOKEN   TokenHandle,  
                WCHAR *              ServerName,  
                SQLSMALLINT          NameLength1,  
                WCHAR *              UserName,  
                SQLSMALLINT          NameLength2,  
                WCHAR *              Authentication,  
                SQLSMALLINT          NameLength3 );  
```  
  
## <a name="arguments"></a>引数  
 *TokenHandle*  
 [入力]トークンのハンドル。  
  
 *ServerName*  
 [入力]データ ソースの名前。 データをプログラムと同じコンピューター上またはネットワーク上のどこか別のコンピューター上にあることがあります。 アプリケーションがデータ ソースを選択する方法については、次を参照してください。[データ ソースまたはドライバーを選択する](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)します。  
  
 *NameLength1*  
 [入力]長さ **ServerName*文字数。  
  
 *UserName*  
 [入力]ユーザーの識別子です。  
  
 *NameLength2*  
 [入力]長さ **UserName*文字数。  
  
 *\[認証]*  
 [入力]認証の文字列 (通常はパスワード)。  
  
 *NameLength3*  
 [入力]長さ **認証*文字数。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 同じ[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)の検証のエラーを入力する点を除いて、ドライバー マネージャーを使用して、 **HandleType** SQL_HANDLE_DBC_INFO_TOKEN の**処理**の*hDbcInfoToken*します。  
  
## <a name="remarks"></a>コメント  
 ドライバー マネージャーが、アプリケーションにエラーを返します、ドライバーが SQL_ERROR または SQL_INVALID_HANDLE を返すたびに (で[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)または[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 ドライバー マネージャーがから診断情報を取得するたびに、ドライバーは SQL_SUCCESS_WITH_INFO を返します、 *hDbcInfoToken*でアプリケーションに SQL_SUCCESS_WITH_INFO を返すと[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)と[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)します。  
  
 アプリケーションでは、この関数を直接呼び出さないでください。 ドライバー対応接続プールをサポートする ODBC ドライバーでは、この関数を実装する必要があります。  
  
 ODBC ドライバーの開発の sqlspi.h が含まれます。  
  
## <a name="see-also"></a>参照  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC ドライバー対応接続プールの開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
