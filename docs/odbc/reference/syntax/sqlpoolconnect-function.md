---
title: SQLPoolConnect 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPoolConnect function [ODBC]
ms.assetid: 41322737-890d-4a81-aed2-06cc3d546962
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c390dacb5072c5d516e95b4fe6b789bfffbbd2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005800"
---
# <a name="sqlpoolconnect-function"></a>SQLPoolConnect 関数
**準拠**  
 バージョンが導入されました。ODBC 3.8 規格に準拠します。ODBC  
  
 **概要**  
 **SQLPoolConnect**プール内の接続を再利用できるない場合は、新しい接続を作成するために使用します。  
  
## <a name="syntax"></a>構文  
  
```cpp
  
SQLRETURN  SQLPoolConnect(  
                SQLHDBC              hDbc,  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              wszOutConnectString,  
                SQLSMALLINT          cchConnectStringBuffer,  
                SQLSMALLINT *        cchConnectStringLen );  
```  
  
## <a name="arguments"></a>引数  
 *hDbc*  
 [入力]接続ハンドルです。  
  
 *hDbcInfoToken*  
 [入力]新しいアプリケーションの接続要求のトークンのハンドル。  
  
 *wszOutConnectString*  
 [出力]完全な接続文字列を格納するバッファーへのポインター。 ターゲット データ ソースへの接続に成功は、このバッファーには、完全な接続文字列が含まれています。 アプリケーションは、このバッファーには少なくとも 1,024 文字を割り当てる必要があります。  
  
 場合*wszOutConnectString*が null の場合、 *cchConnectStringLen*はまだ文字 (文字データの null 終端文字を除く) の合計数を返しますで返される使用可能なによって示されるバッファー *wszOutConnectString*します。  
  
 *cchConnectStringBuffer*  
 [入力]長さ、**wszOutConnectString*文字のバッファー。  
  
 *cchConnectStringLen*  
 [出力]文字 (null 終了文字を除く) の合計数を返すバッファーへのポインターで返される使用可能な\* *wszOutConnectString*します。 返すに使用できる文字数がより大きいかに等しい場合*cchConnectStringBuffer*、内の接続文字列を完了した\* *wszOutConnectString* に切り捨てられます*cchConnectStringBuffer* null 終了文字の長さマイナスです。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ような[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)ドライバー マネージャーを使用する点を除いて、任意の入力検証のエラーを**HandleType** SQL_HANDLE_DBC_INFO_TOKEN の**処理**の*hDbcInfoToken*します。  
  
## <a name="remarks"></a>コメント  
 ドライバー マネージャーは、保証のハンドルを HENV 親*hDbc*と*hDbcInfoToken*は同じです。  
  
 異なり[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)、あるありません*DriverCompletion*接続情報の入力を求めるへの引数。 プロンプトを表示するダイアログは、プーリングのシナリオでは許可されていません。  
  
 アプリケーションでは、この関数を直接呼び出さないでください。 ドライバー対応接続プールをサポートする ODBC ドライバーでは、この関数を実装する必要があります。  
  
 ドライバー マネージャーが、アプリケーションにエラーを返します、ドライバーが SQL_ERROR または SQL_INVALID_HANDLE を返すたびに (で[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)または[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 ドライバー マネージャーがから診断情報を取得するたびに、ドライバーは SQL_SUCCESS_WITH_INFO を返します、 *hDbcInfoToken*でアプリケーションに SQL_SUCCESS_WITH_INFO を返すと[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)と[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)します。  
  
 アプリケーションが[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)、 *wszOutConnectString* (最後の 3 つのパラメーターすべてに設定されます NULL、0、NULL) バッファーは、NULL になります。 それ以外の場合、ドライバーは、アプリケーションに返される出力接続文字列を返す必要があります[SQLDriverConnect 関数](../../../odbc/reference/syntax/sqldriverconnect-function.md)呼び出します。  
  
 ODBC ドライバーの開発の sqlspi.h が含まれます。  
  
## <a name="see-also"></a>参照  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC ドライバー対応接続プールの開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
