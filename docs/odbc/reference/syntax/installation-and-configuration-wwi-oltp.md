---
title: SQLSetDriverConnectInfo 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetDriverConnectInfo function [ODBC]
ms.assetid: bfd4dfc2-fbca-4ef3-81e5-2706f2389256
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 54e37940062427008e9b90f6cda4cec825a721ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915283"
---
# <a name="sqlsetdriverconnectinfo-function"></a>SQLSetDriverConnectInfo 関数
**準拠**  
 バージョンが導入されました。ODBC 3.81 規格に準拠します。ODBC  
  
 **概要**  
 **SQLSetDriverConnectInfo**接続文字列をアプリケーションの接続情報のトークンに設定に使用される**SQLDriverConnect**呼び出します。  
  
## <a name="syntax"></a>構文  
  
```cpp
  
SQLRETURN SQLSetDriverConnectInfo(  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              InConnectionString,  
                SQLSMALLINT          StringLength1 );  
```  
  
## <a name="arguments"></a>引数  
 *TokenHandle*  
 [入力]トークンのハンドル。  
  
 *InConnectionString*  
 [入力]完全な接続文字列 (「コメント」内の構文を参照してください[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))、部分的な接続文字列、または空の文字列。  
  
 *StringLength1*  
 [入力]長さ **InConnectionString*、文字の場合、文字列は ANSI または DBCS 文字列が Unicode、またはバイトの場合。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 同じ[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)ドライバー マネージャーを使用する点を除いて、任意の入力の検証エラーに関連する、 **HandleType** SQL_HANDLE_DBC_INFO_TOKEN の**処理**の*hDbcInfoToken*します。  
  
## <a name="remarks"></a>コメント  
 ドライバー マネージャーが、アプリケーションにエラーを返します、ドライバーが SQL_ERROR または SQL_INVALID_HANDLE を返すたびに (で[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)または[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 ドライバー マネージャーがから診断情報を取得するたびに、ドライバーは SQL_SUCCESS_WITH_INFO を返します、 *hDbcInfoToken*でアプリケーションに SQL_SUCCESS_WITH_INFO を返すと[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)と[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)します。  
  
 アプリケーションでは、この関数を直接呼び出さないでください。 ドライバー対応接続プールをサポートする ODBC ドライバーでは、この関数を実装する必要があります。  
  
 ODBC ドライバーの開発の sqlspi.h が含まれます。  
  
## <a name="see-also"></a>参照  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC ドライバー対応接続プールの開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
