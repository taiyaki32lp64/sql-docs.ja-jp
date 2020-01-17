---
title: SQLGetInstalledDrivers 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetInstalledDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInstalledDrivers
helpviewer_keywords:
- SQLGetInstalledDrivers function [ODBC]
ms.assetid: a1983a2e-0edf-422e-bd1b-ec5db40a34bc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9e7b079e2b66f4e1ba7b3233a6aaa20cd9908a67
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061522"
---
# <a name="sqlgetinstalleddrivers-function"></a>SQLGetInstalledDrivers 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0  
  
 **概要**  
 **SQLGetInstalledDrivers**のシステム情報 [ODBC Drivers] セクションを読み取って、インストールされたドライバーの説明の一覧を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>引数  
 *lpszBuf*  
 [出力]インストールされているドライバーの説明の一覧。 リスト構造については、「コメントです。」を参照してください。  
  
 *cbBufMax*  
 [入力]長さ*lpszBuf*します。  
  
 *pcbBufOut*  
 [出力]合計バイト数 (null 終了バイトを除く) で返される*lpszBuf*します。 返される使用可能なバイト数がより大きいかに等しい場合*cbBufMax*、ドライバーの説明の一覧*lpszBuf*に切り捨てられます*cbBufMax*マイナス、null 終了文字です。 *PcbBufOut*引数が null ポインターを指定できます。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合、FALSE が失敗した場合に TRUE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLGetInstalledDrivers** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーのエラー|エラーが発生する特定のインストーラーのエラーがなかった。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無効なバッファーの長さ|*LpszBuf*引数が NULL または無効、または*cbBufMax*引数が 0 未満でした。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|コンポーネントがレジストリに見つかりません|インストーラーは、レジストリで、[ODBC Drivers] セクションを見つけられませんでした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|インストーラーは、メモリ不足のため、関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 各ドライバーの説明は null のバイトで終了し、全体の一覧は null バイトで終了します。 (つまり、2 つの null バイトの末尾を示す一覧。)割り当てられたバッファー全体の一覧を保持するのに十分な大きさでない場合は、エラーなし、一覧は切り捨てられます。 Null ポインターとして渡される場合、エラーが返されます*lpszBuf*します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|ドライバーの説明と属性を返す|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
