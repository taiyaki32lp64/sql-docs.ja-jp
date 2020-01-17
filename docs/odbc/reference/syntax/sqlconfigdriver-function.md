---
title: SQLConfigDriver 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDriver
helpviewer_keywords:
- SQLConfigDriver function [ODBC]
ms.assetid: 4f681961-ac9f-4d88-b065-5258ba112642
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e324b1f49bd6f8d0cad15ac2bcde73f558220330
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121446"
---
# <a name="sqlconfigdriver-function"></a>SQLConfigDriver 関数
**準拠**  
 バージョンが導入されました。ODBC 2.5  
  
 **概要**  
 **SQLConfigDriver**適切なドライバーのセットアップ DLL と呼び出しを読み込み、 **ConfigDriver**関数。  
  
 機能**SQLConfigDriver**にアクセスすることも[ODBCCONF します。EXE](../../../odbc/odbcconf-exe.md)します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLConfigDriver(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszArgs,  
     LPSTR    lpszMsg,  
     WORD     cbMsgMax,  
     WORD *   pcbMsgOut);  
```  
  
## <a name="arguments"></a>引数  
 *hwndParent*  
 [入力]親ウィンドウ ハンドル。 関数では、ハンドルが null の場合、ダイアログ ボックスは表示されません。  
  
 *起こり*  
 [入力]要求の種類。 *起こり*値は次のいずれかを含める必要があります。  
  
 ODBC_CONFIG_DRIVER:接続プール、ドライバーによって使用されるタイムアウトを変更します。  
  
 ODBC_INSTALL_DRIVER:新しいドライバーをインストールします。  
  
 ODBC_REMOVE_DRIVER:既存のドライバーを削除します。  
  
 このオプションは、ドライバー固有を場合にも、*起こり*最初のオプションが ODBC_CONFIG_DRIVER_MAX + 1 から開始する必要があります。 *起こり*追加のオプションは ODBC_CONFIG_DRIVER_MAX + 1 より大きい値から開始もする必要があります。  
  
 *lpszDriver*  
 [入力]システム情報に登録されているドライバーの名前。  
  
 *lpszArgs*  
 [入力]ドライバー固有の引数を含む null で終わる文字列*起こり*します。  
  
 *lpszMsg*  
 [出力]ドライバーのセットアップから、出力メッセージを含む null で終わる文字列。  
  
 *cbMsgMax*  
 [入力]長さ*lpszMsg します。*  
  
 *pcbMsgOut*  
 [出力]返される使用可能なバイトの合計数*lpszMsg*します。 返される使用可能なバイト数がより大きいかに等しい場合*cbMsgMax*、内の出力メッセージ*lpszMsg*に切り捨てられます*cbMsgMax* null 終了マイナス文字。 *PcbMsgOut*引数が null ポインターを指定できます。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合、FALSE が失敗した場合に TRUE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLConfigDriver** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーのエラー|エラーが発生する特定のインストーラーのエラーがなかった。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無効なバッファーの長さ|*LpszMsg*引数が無効です。|  
|ODBC_ERROR_INVALID_HWND|無効なウィンドウ ハンドル|*HwndParent*引数が無効です。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求の型が無効です。|*起こり*引数が、次のいずれか。<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> *起こり*引数があった ODBC_CONFIG_DRIVER_MAX 小さいドライバー固有のオプション。|  
|ODBC_ERROR_INVALID_NAME|無効なドライバーまたは翻訳者名|*LpszDriver*引数が無効です。 レジストリに見つかりませんでした。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無効なキーワードと値のペア|*LpszArgs*引数には、構文エラーが含まれています。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*できませんでした|インストーラーによって要求された操作を実行できませんでした、*起こり*引数。 呼び出し**ConfigDriver**できませんでした。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|ドライバーまたはトランスレーター セットアップ ライブラリを読み込むことができません。|ドライバーのセットアップのライブラリを読み込むことができませんでした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|インストーラーは、メモリ不足のため、関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **SQLConfigDriver**により、アプリケーションを呼び出してドライバーの**ConfigDriver**ルーチンに名前を知っているし、ドライバー固有のセットアップ DLL を読み込む必要はありません。 セットアップ プログラムは、DLL がインストールされているドライバーのセットアップ後に、この関数を呼び出します。 呼び出し元のプログラムはこの関数が使用できないことのすべてのドライバーが認識することはあります。 このような場合は、呼び出し元のプログラムは、エラーなく続行する必要があります。  
  
## <a name="driver-specific-options"></a>ドライバー固有のオプション  
 アプリケーションを使用して、ドライバーによって公開されているドライバー固有の機能を要求できます、*起こり*引数。 *起こり*ODBC_CONFIG_DRIVER_MAX + 1、最初のオプションとなり、追加のオプションはその値から 1 ずつ増えます。 その関数が null で終わる文字列で指定する必要がありますのドライバーが必要な引数が渡された、 *lpszArgs*引数。 このような機能を提供するドライバーは、ドライバー固有のオプションのテーブルを維持する必要があります。 オプションは、ドライバーのマニュアルで完全に記述する必要があります。 ドライバー固有のオプションを使用しているアプリケーションの作成者は、このような使用、アプリケーションは小さい相互運用可能な対応にあります。  
  
## <a name="setting-connection-pooling-timeout"></a>接続プーリングのタイムアウトの設定  
 ドライバーの構成を設定すると、接続プール タイムアウト プロパティを設定できます。 **SQLConfigDriver**を呼び出すと、*起こり*ODBC_CONFIG_DRIVER のおよび*lpszArgs*に設定**CPTimeout**します。 **CPTimeout**使用しなくても、接続プール内の接続が保持できる時間の期間を決定します。 タイムアウトの期限が切れるは、接続の終了し、プールから削除します。 既定のタイムアウトは、60 秒です。  
  
 ときに**SQLConfigDriver**を使用して呼び出した*起こり*ODBC_INSTALL_DRIVER または ODBC_REMOVE_DRIVER に設定すると、ドライバー マネージャー、適切なドライバーのセットアップ DLL と読み込みの呼び出し、 **ConfigDriver**関数。 ときに**SQLConfigDriver**を呼び出すと、*起こり*ODBC_CONFIG_DRIVER のすべての処理が、ODBC インストーラーの実行、ドライバーのセットアップ DLL が読み込まれる必要があるないようにします。  
  
## <a name="messages"></a>Messages  
 ドライバーのセットアップ ルーチンは、アプリケーション内の null で終わる文字列としてテキスト メッセージを送信することができます、 *lpszMsg*バッファー。 メッセージに切り捨てられます*cbMsgMax*によって null 終了文字マイナス、 **ConfigDriver**する以上の場合は機能*cbMsgMax*文字。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|追加、変更、またはドライバーを削除します。|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)(で DLL のセットアップ)|  
|既定のデータ ソースを削除します。|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
