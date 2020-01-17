---
title: ConfigDriver 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDriver
helpviewer_keywords:
- ConfigDriver [ODBC]
ms.assetid: 9473f48f-bcae-4784-89c1-7839bad4ed13
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9e6c7759cf63611da167bf54a2e88487abc7b1cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016747"
---
# <a name="configdriver-function"></a>ConfigDriver 関数
**準拠**  
 バージョンが導入されました。ODBC 2.5  
  
 **概要**  
 **ConfigDriver**により、セットアップ プログラムをインストールを実行し、関数を呼び出すプログラムを必要とせずアンインストール**ConfigDSN**します。 この関数では、ドライバー固有のシステム情報を作成し、インストール中に、DSN の変換を実行するだけでなくアンインストール中に、システム情報の変更をクリーンアップなどのドライバー固有の関数を実行します。 この関数は、ドライバーのセットアップ DLL または別のセットアップ DLL によって公開されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL ConfigDriver(  
      HWND    hwndParent,  
      WORD    fRequest,  
      LPCSTR  lpszDriver,  
      LPCSTR  lpszArgs,  
      LPSTR   lpszMsg,  
      WORD    cbMsgMax,  
      WORD *  pcbMsgOut);  
```  
  
## <a name="arguments"></a>引数  
 *hwndParent*  
 [入力]親ウィンドウ ハンドル。 関数では、ハンドルが null の場合、ダイアログ ボックスは表示されません。  
  
 *起こり*  
 [入力]要求の種類。 *起こり*引数は、次の値のいずれかを含める必要があります。  
  
 ODBC_INSTALL_DRIVER:新しいドライバーをインストールします。  
  
 ODBC_REMOVE_DRIVER:ドライバーを削除します。  
  
 このオプションは、ドライバー固有を場合にも、*起こり*ODBC_CONFIG_DRIVER_MAX + 1 から最初のオプションの引数を起動する必要があります。 *起こり*ODBC_CONFIG_DRIVER_MAX + 1 より大きい値から、追加のオプションの引数を開始する必要がありますもします。  
  
 *lpszDriver*  
 [入力]システム情報の Odbcinst.ini のキーに登録されているドライバーの名前。  
  
 *lpszArgs*  
 [入力]ドライバー固有の引数を含む null で終わる文字列*起こり*します。  
  
 *lpszMsg*  
 [出力]ドライバーのセットアップからの出力メッセージを含む null で終わる文字列。  
  
 *cbMsgMax*  
 [入力]長さ*lpszMsg*します。  
  
 *pcbMsgOut*  
 [出力]返される使用可能なバイトの合計数*lpszMsg*します。  
  
 返される使用可能なバイト数がより大きいかに等しい場合*cbMsgMax*、内の出力メッセージ*lpszMsg*に切り捨てられます*cbMsgMax* null 終了マイナス文字。 *PcbMsgOut*引数が null ポインターを指定できます。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合、FALSE が失敗した場合に TRUE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**ConfigDriver** 、関連付けられている FALSE が返されます *\*pfErrorCode*インストーラー エラー バッファーへの呼び出しで値が投稿された**SQLPostInstallerError**呼び出すことによって取得できる**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|無効なウィンドウ ハンドル|*HwndParent*引数が無効です。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求の型が無効です。|*起こり*引数が、次のいずれか。<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> ドライバー固有のオプションは、ODBC_CONFIG_DRIVER_MAX 以下でした。|  
|ODBC_ERROR_INVALID_NAME|無効なドライバーまたは翻訳者名|*LpszDriver*引数が無効です。 レジストリに見つかりませんでした。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*できませんでした|によって要求された操作を実行できませんでした、*起こり*引数。|  
|ODBC_ERROR_DRIVER_SPECIFIC|ドライバーに translator 固有のエラー|定義された ODBC インストーラーのエラーがないドライバー固有のエラーです。 *SzError*への呼び出しの引数、 **SQLPostInstallerError**関数は、ドライバー固有のエラー メッセージを含める必要があります。|  
  
## <a name="comments"></a>コメント  
  
### <a name="driver-specific-options"></a>ドライバー固有のオプション  
 アプリケーションを使用して、ドライバーによって公開されているドライバー固有の機能を要求できます、*起こり*引数。 *起こり*ODBC_CONFIG_DRIVER_MAX に 1 を加えた、最初のオプションは使用し、追加のオプションはその値から 1 ずつ増えます。 その関数が null で終わる文字列で指定する必要がありますのドライバーが必要な引数が渡された、 *lpszArgs*引数。 このような機能を提供するドライバーは、ドライバー固有のオプションのテーブルを維持する必要があります。 オプションは、ドライバーのマニュアルで完全に記述する必要があります。 ドライバー固有のオプションを使用しているアプリケーションの作成者は、これにより、アプリケーション小さい相互運用可能な対応にあります。  
  
### <a name="messages"></a>Messages  
 ドライバーのセットアップ ルーチンは null で終わる文字列としてアプリケーションにテキスト メッセージを送信することができます、 *lpszMsg*バッファー。 メッセージに切り捨てられます*cbMsgMax*によって null 終了文字マイナス、 **ConfigDriver**する以上の場合は機能*cbMsgMax*文字。
