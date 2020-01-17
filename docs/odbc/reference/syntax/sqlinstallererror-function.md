---
title: SQLInstallerError 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallerError
helpviewer_keywords:
- SQLInstallerError [ODBC]
ms.assetid: e6474b79-4d55-458f-81ce-abfafe357f83
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab9461d87a3df2efc98c38e4c72cee4c247fee7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138027"
---
# <a name="sqlinstallererror-function"></a>SQLInstallerError 関数
**準拠**  
 バージョンが導入されました。ODBC 3.0  
  
 **概要**  
 **SQLInstallerError** ODBC インストーラーの関数のエラーまたは状態の情報を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
RETCODE SQLInstallerError(  
     WORD      iError,  
     DWORD *   pfErrorCode,  
     LPSTR     lpszErrorMsg,  
     WORD      cbErrorMsgMax,  
     WORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>引数  
 *i エラー*  
 [入力]エラー レコードの数。 有効な数値は 1 ~ 8 です。  
  
 *pfErrorCode*  
 [出力]インストーラーのエラー コード。 (詳細については、「コメントです」を参照してください)  
  
 *lpszErrorMsg*  
 [出力]エラー メッセージのテキスト用のストレージへのポインター。  
  
 *cbErrorMsgMax*  
 [入力]最大長、*後*バッファー。 これ未満か、null 終端文字マイナス SQL_MAX_MESSAGE_LENGTH と等しい必要があります。  
  
 *cbErrorMsgMax*  
 [入力]最大長、*後*バッファー。 これ未満か、null 終端文字マイナス SQL_MAX_MESSAGE_LENGTH と等しい必要があります。  
  
 *pcbErrorMsg*  
 [出力]\(Null 終了文字を除く) バイトの総数へのポインターで返される使用可能な*lpszErrorMsg*です。 返される使用可能なバイト数がより大きいかに等しい場合*cbErrorMsgMax*、エラー メッセージ テキスト*lpszErrorMsg*に切り捨てられます*cbErrorMsgMax*マイナス、null 終端文字のバイト数。 *PcbErrorMsg*引数が null ポインターを指定できます。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、または SQL_ERROR します。  
  
## <a name="diagnostics"></a>診断  
 **SQLInstallerError**自体のエラー値は通知されません。 **SQLInstallerError** SQL_NO_DATA が返されるエラー情報を取得することができない場合 (この場合*pfErrorCode*が定義されていません)。 場合**SQLInstallerError**は通常、SQL_ERROR を返します何らかの理由でエラー値にアクセスできません**SQLInstallerError** SQL_ERROR が返されますが、エラー値は通知されません。 警告の文字列の長さがわからないかどうか (*lpszErrorMsg*) を設定することができます*lpszErrorMsg* NULL と呼び出しに**SQLInstallerError**します。 **SQLInstallerError**で警告の文字列の長さを戻り値には*cbErrorMsgMax*します。 エラー メッセージのバッファーが短すぎる場合**SQLInstallerError** SQL_SUCCESS_WITH_INFO を返します、正しい*pfErrorCode*値**SQLInstallerError**.  
  
 アプリケーション エラー メッセージで切り捨てが発生したかを判断する値と比較できます、 *cbErrorMsgMax*に書き込まれるメッセージのテキストの実際の長さへの引数、 *pcbErrorMsg*引数。 切り捨てが発生した場合、適切なバッファーの長さを割り当てる必要がある*lpszErrorMsg*と**SQLInstallerError**で対応するにはもう一度呼び出す必要がある*i エラー*レコード。  
  
## <a name="comments"></a>コメント  
 アプリケーションを呼び出す**SQLInstallerError**と以前の ODBC インストーラーの関数呼び出し、FALSE を返します。 ODBC インストーラーとドライバーまたはトランスレーター セットアップ関数が、関数が失敗した場合にのみ、0 個以上のエラーを投稿 (FALSE を返します)。そのため、アプリケーションが呼び出す**SQLInstallerError** ODBC インストーラー関数が失敗した後のみです。  
  
 ODBC インストーラーのエラー キューは、新しいインストーラー関数が呼び出されるたびにフラッシュされます。 そのため、アプリケーションは、インストーラーの最後の関数呼び出しからエラーを以外の関数を取得することはできません。  
  
 アプリケーションが呼び出す関数の呼び出しを複数のエラーを取得する**SQLInstallerError**複数回です。  
  
 追加の情報がない場合に**SQLInstallerError** 、SQL_NO_DATA が返される、 *pfErrorCode*引数が定義されて、 *pcbErrorMsg*引数が 0 の場合、*lpszErrorMsg*引数には、1 つの null 終端文字が含まれています (しない限り、 *cbErrorMsgMax*引数が 0)。
