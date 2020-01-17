---
title: SQLWritePrivateProfileString 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWritePrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWritePrivateProfileString
helpviewer_keywords:
- SQLWritePrivateProfileString [ODBC]
ms.assetid: 526f36a4-92ed-4874-9725-82d27c0b86f9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4b847576e503fbbbb511d2dda8f60675c298681c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039383"
---
# <a name="sqlwriteprivateprofilestring-function"></a>SQLWritePrivateProfileString 関数
**準拠**  
 バージョンが導入されました。ODBC 2.0  
  
 **概要**  
 **SQLWritePrivateProfileString**システム情報の Odbc.ini サブキーに値の名前とデータを書き込みます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLWritePrivateProfileString(  
     LPCSTR     lpszSection,  
     LPCSTR     lpszEntry,  
     LPCSTR     lpszString,  
     LPCSTR     lpszFilename);  
```  
  
## <a name="arguments"></a>引数  
 *大文字、小文字*  
 [入力]文字列のコピー先となるセクションの名前を含む null で終わる文字列へのポインター。 セクションが存在しない場合は作成されます。 セクションの名前がケースに依存しません。文字列は、任意の大文字と小文字を使用できます。  
  
 *lpszEntry*  
 [入力]文字列に関連付けられるキーの名前を含む null で終わる文字列へのポインター。 指定されたセクションにキーが存在しない場合は作成されます。 この引数が NULL の場合、セクション内のすべてのエントリを含むセクション全体が削除されます。  
  
 *lpszString*  
 [入力]ファイルに書き込まれる null で終わる文字列へのポインター。 この引数が NULL の場合、キーが指す、 *lpszEntry*引数を削除します。  
  
 *場合*  
 [出力]初期化ファイルの名前を示す null で終わる文字列へのポインター。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合、FALSE が失敗した場合に TRUE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLWritePrivateProfileString** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーのエラー|エラーが発生する特定のインストーラーのエラーがなかった。|  
|ODBC_ERROR_REQUEST_FAILED|要求が失敗しました|要求されたシステム情報を書き込めませんでした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|インストーラーは、メモリ不足のため、関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **SQLWritePrivateProfileString**に Microsoft Windows と Windows 2000 から Microsoft® Windows® ポート ドライバーとドライバーのセットアップ Dll に簡単な方法で提供されます。 呼び出す**WritePrivateProfileString** Odbc.ini ファイルにプロファイル文字列への呼び出しに置き換える必要がありますを記述する**SQLWritePrivateProfileString**します。 **SQLWritePrivateProfileString**システム情報の Odbc.ini サブキーに、指定された値の名前とデータを追加する Win32® API で関数を呼び出します。  
  
 構成モードでは、DSN の値を一覧表示、Odbc.ini エントリが、システム情報の場所を示します。 DSN がユーザー DSN (状態変数は USERDSN_ONLY) の場合は、この関数は、HKEY_CURRENT_USER 内の Odbc.ini エントリを書き込みます。 DSN がシステム DSN (SYSTEMDSN_ONLY) の場合は、この関数は、HKEY_LOCAL_MACHINE 内の Odbc.ini エントリを書き込みます。 状態変数が BOTHDSN の場合は、HKEY_CURRENT_USER 試行すると失敗した場合、HKEY_LOCAL_MACHINE が使用されます。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|システム情報の値を取得します。|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
