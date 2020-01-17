---
title: SQLGetConfigMode 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConfigMode
helpviewer_keywords:
- SQLGetConfigMode function [ODBC]
ms.assetid: b96ab3b8-08d5-4fea-9ffe-e03043efbf2d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14fb43015db9113262320f78f0bae53f8a168f95
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044555"
---
# <a name="sqlgetconfigmode-function"></a>SQLGetConfigMode 関数
**準拠**  
 バージョンが導入されました。ODBC 3.0  
  
 **概要**  
 **SQLGetConfigMode** DSN の値を一覧表示した Odbc.ini エントリが、システム情報の場所を示す構成モードを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>引数  
 *pwConfigMode*  
 [出力]構成モードを格納しているバッファーへのポインター。 (「コメントです」を参照してください)値 *\*pwConfigMode*を指定できます。  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合、FALSE が失敗した場合に TRUE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLGetConfigMode** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|インストーラーは、メモリ不足のため、関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 この関数を使用して、DSN の値を一覧表示した Odbc.ini エントリが、システム情報の場所を決定します。 場合 *\*pwConfigMode*は ODBC_USER_DSN、DSN がユーザー DSN と関数は、HKEY_CURRENT_USER 内の Odbc.ini エントリから読み取ります。 ODBC_SYSTEM_DSN 場合は、DSN はシステム DSN と関数は、HKEY_LOCAL_MACHINE 内の Odbc.ini エントリから読み取ります。 ODBC_BOTH_DSN 場合は、HKEY_CURRENT_USER 試行すると失敗した場合、HKEY_LOCAL_MACHINE が使用されます。  
  
 既定では、 **SQLGetConfigMode** ODBC_BOTH_DSN を返します。 呼び出してユーザー DSN またはシステム DSN を作成するときに**SQLConfigDataSource**関数が ODBC_USER_DSN または ODBC_SYSTEM_DSN DSN の変更中にユーザーとシステム Dsn を区別するために、構成モードを設定します。 を返す前に**SQLConfigDataSource** ODBC_BOTH_DSN 構成モードにリセットします。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|構成モードの設定|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
