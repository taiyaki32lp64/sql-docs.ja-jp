---
title: SQLConfigDataSource 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConfigDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDataSource
helpviewer_keywords:
- SQLConfigDataSource function [ODBC]
ms.assetid: f8d6e342-c010-434e-b1cd-f5371fb50a14
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e7706d3a7dd05273b4608d49211a6eaab8927f2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118605"
---
# <a name="sqlconfigdatasource-function"></a>SQLConfigDataSource 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0  
  
 **まとめ**  
 **SQLConfigDataSource**追加、変更、またはデータ ソースを削除します。  
  
 機能**SQLConfigDataSource**にアクセスすることも[ODBCCONF します。EXE](../../../odbc/odbcconf-exe.md)します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLConfigDataSource(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>引数  
 *hwndParent*  
 [入力]親ウィンドウ ハンドル。 関数では、ハンドルが null の場合、ダイアログ ボックスは表示されません。  
  
 *起こり*  
 [入力]要求の種類。 *起こり*引数は、次の値のいずれかを含める必要があります。  
  
 ODBC_ADD_DSN:新しいユーザー データ ソースを追加します。  
  
 ODBC_CONFIG_DSN:構成 (変更) 既存のユーザー データ ソース。  
  
 ODBC_REMOVE_DSN:既存のユーザー データ ソースを削除します。  
  
 ODBC_ADD_SYS_DSN:新しいシステム データ ソースを追加します。  
  
 ODBC_CONFIG_SYS_DSN:既存のシステム データ ソースを変更します。  
  
 ODBC_REMOVE_SYS_DSN:既存のシステム データ ソースを削除します。  
  
 ODBC_REMOVE_DEFAULT_DSN:システム情報の既定のデータ ソースの仕様 セクションを削除します。 (これからも削除されます既定ドライバーの仕様のセクション システム情報で Odbcinst.ini エントリ。 これは、*起こり*、非推奨と同じ機能を実行します**SQLRemoveDefaultDataSource**関数です。)。このオプションを指定すると、すべての呼び出しでその他のパラメーターの**SQLConfigDataSource** Null にする必要がありますは、それらは無視されますが NULL でない場合。  
  
 *lpszDriver*  
 [入力]ドライバーの名前 (通常は、関連付けられている DBMS の名前)、物理ドライバー名ではなくユーザーに表示されます。  
  
 *lpszAttributes*  
 [入力]二重の null で終わるキーワードと値のペアの形式で属性の一覧。 詳細については、次を参照してください。 [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)します。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合、FALSE が失敗した場合に TRUE を返します。 エントリが存在しない場合、システムの情報でこの関数が呼び出されたときに、関数は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLConfigDataSource** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーのエラー|エラーが発生する特定のインストーラーのエラーがなかった。|  
|ODBC_ERROR_INVALID_HWND|無効なウィンドウ ハンドル|*HwndParent*引数が無効または NULL。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求の型が無効です。|*起こり*引数が、次のいずれか。<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN ODBC_ADD_SYS_DSN ODBC_CONFIG_SYS_DSN ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DEFAULT_DSN|  
|ODBC_ERROR_INVALID_NAME|無効なドライバーまたは翻訳者名|*LpszDriver*引数が無効です。 レジストリに見つかりませんでした。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無効なキーワードと値のペア|*LpszAttributes*引数には、構文エラーが含まれています。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*できませんでした|インストーラーによって要求された操作を実行できませんでした、*起こり*引数。 呼び出し**ConfigDSN**できませんでした。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|ドライバーまたはトランスレーター セットアップ ライブラリを読み込むことができません。|ドライバーのセットアップのライブラリを読み込むことができませんでした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|インストーラーは、メモリ不足のため、関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **SQLConfigDataSource**の値を使用して*lpszDriver*システム情報から、ドライバーのセットアップ DLL の完全なパスを読み取れません。 DLL および呼び出しが読み込まれます**ConfigDSN**に渡された同じ引数を使用します。  
  
 **SQLConfigDataSource**を検索またはセットアップ DLL を読み込むことがない場合、またはユーザーがダイアログ ボックスをキャンセルした場合は FALSE を返します。 受け取ったステータスを返しますそれ以外の場合、 **ConfigDSN**します。  
  
 **SQLConfigDataSource**システム DSN のマップ*起こり*ユーザー DSN を*起こり*(ODBC_ADD_DSN に ODBC_ADD_SYS_DSN、ODBC_CONFIG_DSN、して ODBC_REMOVE_SYS_ ODBC_CONFIG_SYS_DSN sDSN ODBC_REMOVE_DSN)。 ユーザーとをシステム Dsn を区別するために**SQLConfigDataSource**インストーラーに次の表に従って構成モードを設定します。 を返す前に**SQLConfigDataSource** BOTHDSN 構成モードにリセットします。 **ConfigDSN** (ドライバーによって実装される) 呼び出す必要があります**SQLWriteDSNToIni**と**SQLWritePrivateProfileString**システム DSN をサポートします。 詳細については、次を参照してください。 [ConfigDSN 関数](../../../odbc/reference/syntax/configdsn-function.md)します。  
  
|*起こり*|構成モード|  
|----------------|------------------------|  
|ODBC_ADD_DSN|USERDSN_ONLY|  
|ODBC_CONFIG_DSN|USERDSN_ONLY|  
|ODBC_REMOVE_DSN|USERDSN_ONLY|  
|ODBC_ADD_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_CONFIG_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_REMOVE_SYS_DSN|SYSTEMDSN_ONLY|  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|追加、変更、またはデータ ソースを削除します。|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (で DLL のセットアップ)|  
|システム情報のデータ ソース名を削除します。|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|システム情報へのデータ ソース名の追加|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
