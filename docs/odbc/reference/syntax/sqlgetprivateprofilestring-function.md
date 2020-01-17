---
title: SQLGetPrivateProfileString 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetPrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetPrivateProfileString
helpviewer_keywords:
- SQLGetPrivateProfileString function [ODBC]
ms.assetid: b72ca065-4d67-48df-baac-e18379a8320a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d58fe69e487b4f61384f9bd146b17c6d9ada9ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061472"
---
# <a name="sqlgetprivateprofilestring-function"></a>SQLGetPrivateProfileString 関数
**準拠**  
 バージョンが導入されました。ODBC 2.0  
  
 **概要**  
 **SQLGetPrivateProfileString**値やシステム情報の値に対応するデータの名前の一覧を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
int SQLGetPrivateProfileString(  
     LPCSTR   lpszSection,  
     LPCSTR   lpszEntry,  
     LPCSTR   lpszDefault,  
     LPCSTR   RetBuffer,  
     INT      cbRetBuffer,  
     LPCSTR   lpszFilename);  
```  
  
## <a name="arguments"></a>引数  
 *大文字、小文字*  
 [入力]キー名を格納しているセクションを指定する null で終わる文字列へのポインター。 この引数が NULL の場合、関数では、ファイルのすべてのセクション名を指定されたバッファーにコピーします。  
  
 *lpszEntry*  
 [入力]関連付けられている文字列を取得するが、キー名を含む null で終わる文字列へのポインター。 この引数が NULL の場合、すべてのキー名で指定されたセクションでは、*大文字、小文字*引数で指定したバッファーにコピー、 *RetBuffer*引数。  
  
 *から*  
 [入力]初期化ファイルにキーが見つからない場合は、指定されたキーの既定値を指定する null で終わる文字列へのポインター。 この引数は、NULL にすることはできません。  
  
 *RetBuffer*  
 [出力]取得した文字列を受け取るバッファーへのポインター。  
  
 *cbRetBuffer*  
 [入力]指し示されるバッファーの文字のサイズを指定します、 *RetBuffer*引数。  
  
 *場合*  
 [入力]初期化ファイルの名前を示す null で終わる文字列へのポインター。 この引数に、ファイルへの完全パスが含まれていない場合、既定のディレクトリが検索されます。  
  
## <a name="returns"></a>戻り値  
 **SQLGetPrivateProfileString**読み取られた文字の数を示す整数値を返します。  
  
## <a name="diagnostics"></a>診断  
 呼び出し時に**SQLGetPrivateProfileString**失敗すると、関連付けられている *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーのエラー|エラーが発生する特定のインストーラーのエラーがなかった。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|インストーラーは、メモリ不足のため、関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **SQLGetPrivateProfileString**に Microsoft Windows と Windows 2000 から Microsoft® Windows® ポート ドライバーとドライバーのセットアップ Dll に簡単な方法で提供されます。 呼び出す**GetPrivateProfileString** Odbc.ini ファイルからのプロファイルの文字列に置き換える必要があります取得する呼び出し**SQLGetPrivateProfileString**します。 **SQLGetPrivateProfileString**値やシステム情報の Odbc.ini サブキーの値に対応するデータの要求された名前を取得、Win32® api 関数を呼び出します。  
  
 構成モード (設定して**SQLSetConfigMode**) DSN の値を一覧表示した Odbc.ini エントリが、システム情報の場所を示します。 DSN がユーザー DSN (構成モードでは USERDSN_ONLY) の場合は、関数は、HKEY_CURRENT_USER 内の Odbc.ini エントリから読み取ります。 DSN がシステム DSN (SYSTEMDSN_ONLY) の場合は、関数は、HKEY_LOCAL_MACHINE 内の Odbc.ini エントリから読み取ります。 BOTHDSN 構成モードの場合、HKEY_CURRENT_USER 試行すると失敗した場合、HKEY_LOCAL_MACHINE が使用されます。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|システム情報の値を書き込む|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
