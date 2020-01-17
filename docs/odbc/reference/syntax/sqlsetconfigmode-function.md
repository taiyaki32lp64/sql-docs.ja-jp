---
title: SQLSetConfigMode 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConfigMode
helpviewer_keywords:
- SQLSetConfigMode function [ODBC]
ms.assetid: 09eb88ea-b6f6-4eca-b19d-0951cebc6c0a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e2f2bcd3fef2946e5b983c1bbdeee1efe4776512
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018919"
---
# <a name="sqlsetconfigmode-function"></a>SQLSetConfigMode 関数
**準拠**  
 バージョンが導入されました。ODBC 3.0  
  
 **概要**  
 **SQLSetConfigMode** DSN の値を一覧表示した Odbc.ini エントリが、システム情報の場所を示す構成モードを設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>引数  
 *wConfigMode*  
 [入力]インストーラーの構成モード (「コメント」を参照してください)。 値*wConfigMode*を指定できます。  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合、FALSE が失敗した場合に TRUE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLSetConfigMode** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|無効なパラメーターのシーケンス|*WConfigMode* ODBC_USER_DSN、ODBC_SYSTEM_DSN、または ODBC_BOTH_DSN が、引数に含まれていませんでした。|  
  
## <a name="comments"></a>コメント  
 この関数は、システム情報の DSN の値を一覧表示、Odbc.ini エントリの場所を設定に使用されます。 場合*wConfigMode*は ODBC_USER_DSN、DSN がユーザー DSN と関数は、HKEY_CURRENT_USER 内の Odbc.ini エントリから読み取ります。 ODBC_SYSTEM_DSN 場合は、DSN はシステム DSN と関数は、HKEY_LOCAL_MACHINE 内の Odbc.ini エントリから読み取ります。 ODBC_BOTH_DSN 場合は、HKEY_CURRENT_USER 試行すると、および失敗した場合は HKEY_LOCAL_MACHINE が使用されます。  
  
 この関数には影響しません**SQLCreateDataSource**と**SQLDriverConnect**します。 構成モードを呼び出すことによって、ドライバーがレジストリから読み取るときに設定する必要**SQLGetPrivateProfileString**または呼び出すことによって、レジストリに書き込む**SQLWritePrivateProfileString**します。 呼び出す**SQLGetPrivateProfileString**と**SQLWritePrivateProfileString**構成モードを使用して操作するレジストリのどの部分を理解します。  
  
> [!CAUTION]  
>  **SQLSetConfigMode**適切に機能する ODBC インストーラーが失敗するときに必要なモードが正しく設定されている場合のみ呼び出す必要があります。  
  
 **SQLSetConfigMode**構成モードのレジストリを直接変更します。 これは、プロセスへの呼び出しによって、構成モードを変更するのとは別に**SQLConfigDataSource**します。 呼び出し**SQLConfigDataSource** DSN を変更するときに、ユーザーとシステム Dsn を区別するために、構成モードを設定します。 を返す前に**SQLConfigDataSource** BOTHDSN 構成モードにリセットします。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|データ ソースの作成|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|接続文字列またはダイアログ ボックスを使用してデータ ソースへの接続|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|構成モードを取得します。|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
