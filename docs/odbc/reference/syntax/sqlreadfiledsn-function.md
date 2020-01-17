---
title: SQLReadFileDSN 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLReadFileDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLReadFileDSN
helpviewer_keywords:
- SQLReadFileDSN function [ODBC]
ms.assetid: ead464aa-cdc3-47dd-a0c0-997711205d31
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ad1e3dc4901fc7251528e6040b9250469f8fef6c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053658"
---
# <a name="sqlreadfiledsn-function"></a>SQLReadFileDSN 関数
**準拠**  
 バージョンが導入されました。ODBC 3.0  
  
 **概要**  
 **SQLReadFileDSN**ファイル DSN から情報を読み取ります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLReadFileDSN(  
     LPCSTR   lpszFileName,  
     LPCSTR   lpszAppName,  
     LPCSTR   lpszKeyName,  
     LPSTR    lpszString,  
     WORD     cbString,  
     WORD *   pcbString);  
```  
  
## <a name="arguments"></a>引数  
 *lpszFileName*  
 [入力].Dsn ファイルの名前を含むデータ バッファーへのポインター。 .Dsn 拡張子は .dsn 拡張機能がまだないすべてのファイル名に追加されます。 値 *\*場合*null で終わる文字列にする必要があります。  
  
 *lpszAppName*  
 [入力]アプリケーションの名前を含むデータ バッファーへのポインター。 これは、ODBC のセクションの"ODBC"です。 値 *\*lpszAppName* null で終わる文字列にする必要があります。  
  
 *lpszKeyName*  
 [入力]読み取るキーの名前を含むデータ バッファーへのポインター。 予約済みキーワードは、「コメント」を参照してください。 値 *\*lpszAppName* null で終わる文字列にする必要があります。  
  
 *lpszString*  
 [出力]読み取るキーに関連付けられた文字列を含むデータ バッファーへのポインター。  
  
 場合 *\*場合*有効 .dsn ファイルの名前ですが、 *lpszAppName*引数が null ポインター、 *lpszKeyName*引数が null ポインターの場合は、 *\*lpszString*有効なアプリケーションの一覧が含まれています。 場合 *\*場合*有効 .dsn ファイルの名前を指定し、  *\*lpszAppName*は有効なアプリケーションの名前ですが、 *lpszKeyName*引数が nullポインターの場合、  *\*lpszString*セミコロンで区切られた、DSN ファイルの適切なセクションでは有効の予約済みキーワードの一覧が含まれています。 場合 *\*場合*は有効な .dsn ファイル名が *\*lpszAppName* null ポインター、 *lpszKeyName*引数が null ポインターの場合は、 *\*lpszString* DSN ファイルで、セミコロンで区切られたセクションの一覧が含まれています。  
  
 *cbString*  
 [入力]長さ、  *\*lpszString*バッファー。  
  
 *pcbString*  
 [出力]返される使用可能なバイトの合計数 *\*lpszString*します。 返される使用可能なバイト数がより大きいかに等しい場合*cbString*、出力文字列 *\*lpszString*に切り捨てられます*cbString*マイナスnull 終了文字です。 *PcbString*引数が null ポインターを指定できます。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合、FALSE が失敗した場合に TRUE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLReadFileDSN** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーのエラー|エラーが発生する特定のインストーラーのエラーがなかった。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無効なバッファーの長さ|*LpszString*引数が NULL でした。<br /><br /> *CbString*引数が 0 未満でした。|  
|ODBC_ERROR_INVALID_PATH|無効なインストール パス|指定されたファイル名のパス、*場合*引数が無効です。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求の型が無効です。|*LpszAppName*引数が null の場合中、 *lpszKeyName*引数が無効です。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|インストーラーは、メモリ不足のため、関数を実行できませんでした。|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|出力文字列の切り捨て|返される文字列 *\*lpszString*ために切り捨てられました値*cbString*の値以下 *\*pcbString*.|  
|ODBC_ERROR_REQUEST_FAILED|要求が失敗しました|キーワードは、ファイル DSN では存在しませんでした。|  
  
## <a name="comments"></a>コメント  
 ODBC では、接続情報を格納するための [ODBC] セクションの名前を予約します。 このセクションの予約済みキーワードは、内の接続文字列用に予約したのと同じ**SQLDriverConnect**します。 (詳細については、次を参照してください、 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)関数の説明です。)。  
  
 アプリケーションでは、ファイル DSN に情報を読み取るため、これらの予約済みキーワードを使用できます。 アプリケーションを呼び出すことができますに関連付けられたファイル DSN では、DSN を使用しない接続文字列を確認する必要がある場合**SQLReadFileDSN** [ODBC] セクションでは、予約済みの接続文字列キーワードのいずれか。 DSN を使用しない接続で渡される完全な接続文字列は、[ODBC] セクションでは、キーワード (予約済みおよびドライバー固有) のすべての組み合わせです。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|ファイル DSN に情報を書き込む|[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
