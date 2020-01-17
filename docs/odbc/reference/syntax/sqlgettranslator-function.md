---
title: SQLGetTranslator 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTranslator
helpviewer_keywords:
- SQLGetTranslator function [ODBC]
ms.assetid: 33879db3-5ef9-4585-9be5-69376157e017
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f769d3c5b2dcfe5d2aa8a431695cb18a52893b91
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030650"
---
# <a name="sqlgettranslator-function"></a>SQLGetTranslator 関数
**準拠**  
 バージョンが導入されました。ODBC 2.0  
  
 **概要**  
 **SQLGetTranslator**ユーザーが翻訳者を選択できるダイアログ ボックスが表示されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLGetTranslator(  
     HWND      hwndParent,  
     LPSTR     lpszName,  
     WORD      cbNameMax,  
     WORD *    pcbNameOut,  
     LPSTR     lpszPath,  
     WORD      cbPathMax,  
     WORD *    pcbPathOut,  
     DWORD *   pvOption);  
```  
  
## <a name="arguments"></a>引数  
 *hwndParent*  
 [入力]親ウィンドウ ハンドル。  
  
 *lpszName*  
 [入力/出力]システム情報の変換プログラムの名前。  
  
 *cbNameMax*  
 [入力]最大長、 *lpszName*バッファー。  
  
 *pcbNameOut*  
 [入力/出力]\(Null 終了バイトを除く) バイトの合計数が指定値を渡したりで返される*lpszName*です。 返される使用可能なバイト数がより大きいかに等しい場合*cbNameMax*、翻訳者名*lpszName*に切り捨てられます*cbNameMax*マイナス、null 終了文字です。 *PcbNameOut*引数が null ポインターを指定できます。  
  
 *lpszPath*  
 [出力]トランスレーター DLL の完全パス。  
  
 *cbPathMax*  
 [入力]最大長、 *lpszPath*バッファー。  
  
 *pcbPathOut*  
 [出力]合計バイト数 (null 終了バイトを除く) で返される*lpszPath*します。 返される使用可能なバイト数がより大きいかに等しい場合*cbPathMax*、翻訳の DLL パス*lpszPath*に切り捨てられます*cbPathMax*マイナス、null 終了文字です。 *PcbPathOut*引数が null ポインターを指定できます。  
  
 *pvOption*  
 [出力] の 32 ビットの変換オプション。  
  
## <a name="returns"></a>戻り値  
 関数は、失敗した場合、またはユーザーがダイアログ ボックスをキャンセルした場合に FALSE である場合に TRUE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLGetTranslator** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーのエラー|エラーが発生する特定のインストーラーのエラーがなかった。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無効なバッファーの長さ|*CbNameMax*または*cbPathMax*引数が 0 未満でした。|  
|ODBC_ERROR_INVALID_HWND|無効なウィンドウ ハンドル|*HwndParent*引数が無効または NULL。|  
|ODBC_ERROR_INVALID_NAME|無効なドライバーまたは翻訳者名|*LpszName*引数が無効です。 レジストリに見つかりませんでした。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|ドライバーまたはトランスレーター セットアップ ライブラリを読み込むことができません。|Translator ライブラリを読み込むことができませんでした。|  
|ODBC_ERROR_INVALID_OPTION|無効なトランザクションのオプション|*PvOption*引数に無効な値が含まれています。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|インストーラーは、メモリ不足のため、関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 場合*hwndParent*が null 場合、または*lpszName*、 *lpszPath*、または*pvOption* null ポインターの場合は、 **SQLGetTranslator** FALSE を返します。 それ以外の場合、次のダイアログ ボックスでインストールされている翻訳者の一覧が表示されます。  
  
 ![翻訳者 ダイアログ ボックスをオン](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 場合*lpszName* translator の有効な名前が含まれていますが選択されています。 それ以外の場合、\<いいえ Translator > を選択します。  
  
 ユーザーが選択した場合\<いいえ Translator > の内容*lpszName*、 *lpszPath*、および*pvOption*に影響はないです。 **SQLGetTranslator**設定*pcbNameOut*と*pcbPathOut* 0 と、TRUE を返します。  
  
 ユーザーが、翻訳者が選択した場合**SQLGetTranslator**呼び出し**ConfigTranslator** translator のセットアップ DLL。 場合**ConfigTranslator** FALSE を返します**SQLGetTranslator**そのダイアログ ボックスに戻ります。 場合**ConfigTranslator** TRUE を返します**SQLGetTranslator**と共に選択した翻訳者名、パス、および変換オプションは、TRUE を返します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|変換を構成します。|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|翻訳の属性の取得|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|翻訳の属性を設定|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
