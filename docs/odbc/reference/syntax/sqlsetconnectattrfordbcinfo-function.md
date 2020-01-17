---
title: SQLSetConnectAttrForDbcInfo 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttrForDbcInfo function [ODBC]
ms.assetid: a28fadb9-b998-472a-b252-709507e92005
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f16cac6a715716dcef0a1c2b337716835c14b2b7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910368"
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>SQLSetConnectAttrForDbcInfo 関数
**準拠**  
 バージョンが導入されました。ODBC 3.81 規格に準拠します。ODBC  
  
 **概要**  
 **SQLSetConnectAttrForDbcInfo**と同じ**SQLSetConnectAttr**が接続ハンドルの代わりに、接続情報トークンの属性を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp
  
SQLRETURN  SQLSetConnectAttrForDbcInfo(  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                SQLINTEGER            Attribute,  
                SQLPOINTER            ValuePtr,  
                SQLINTEGER            StringLength );  
```  
  
## <a name="arguments"></a>引数  
 *hDbcInfoToken*  
 [入力]トークンのハンドル。  
  
 *属性*  
 [入力]設定する属性。 有効な属性の一覧は、特定のドライバーと同じである[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)します。  
  
 *ValuePtr*  
 [入力]関連付けられる値を指すポインター*属性*します。 値に応じて*属性*、 *ValuePtr*は 32 ビット符号なし整数値にまたは null で終わる文字列を指します。 されている場合、*属性*引数は、ドライバー固有の値、値*ValuePtr*符号付き整数である可能性があります。  
  
 *StringLength*  
 [入力]場合*属性*ODBC で定義された属性と*ValuePtr*文字の文字列またはバイナリのバッファーを指す、この引数の長さである必要があります **ValuePtr*します。 文字の文字列データでは、この引数は、文字列のバイト数を含める必要があります。  
  
 場合*属性*ODBC で定義された属性と*ValuePtr*整数*StringLength*は無視されます。  
  
 場合*属性*ドライバーの定義済みの属性では、アプリケーションを設定して属性をドライバー マネージャーの性質を示します、 *StringLength*引数。 *StringLength*次の値を持つことができます。  
  
-   場合*ValuePtr*文字の文字列へのポインターは*StringLength* SQL_NTS または文字列の長さです。  
  
-   場合*ValuePtr* 、SQL_LEN_BINARY_ATTR の結果を配置するアプリケーションが、バイナリ バッファーへのポインター (*長さ*) マクロで*StringLength*します。 これにより、負の値で*StringLength*します。  
  
-   場合*ValuePtr*文字の文字列またはバイナリ文字列以外の値へのポインターは*StringLength* SQL_IS_POINTER 値でなければなりません。  
  
-   場合*ValuePtr* 、固定長の値を含む*StringLength* SQL_IS_INTEGER または SQL_IS_UINTEGER のいずれかを適切なは。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 同じ[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)ドライバー マネージャーを使用する点を除いて、 **HandleType** SQL_HANDLE_DBC_INFO_TOKEN の**処理**の*hDbcInfoToken*.  
  
## <a name="remarks"></a>コメント  
 **SQLSetConnectAttrForDbcInfo**と同じ**SQLSetConnectAttr**が接続ハンドルの代わりに、接続情報トークンの属性を設定します。 たとえば場合、 **SQLSetConnectAttr** 、属性を認識しない**SQLSetConnectAttrForDbcInfo**もその属性の SQL_ERROR を返します。  
  
 ドライバーには、SQL_ERROR または SQL_INVALID_HANDLE が返されます、たびに、ドライバーはプール ID を計算するには、この属性を無視します。 ドライバー マネージャーがから診断情報を取得することも、 *hDbcInfoToken*でアプリケーションに SQL_SUCCESS_WITH_INFO を返すと[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)と[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md). そのため、アプリケーションでは、一部の属性を設定できない理由に関する詳細を取得できます。  
  
 アプリケーションでは、この関数を直接呼び出さないでください。 ドライバー対応接続プールをサポートする ODBC ドライバーでは、この関数を実装する必要があります。  
  
 ODBC ドライバーの開発の sqlspi.h が含まれます。  
  
## <a name="see-also"></a>参照  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC ドライバー対応接続プールの開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
