---
title: SQLInstallTranslatorEx 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallTranslatorEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslatorEx
helpviewer_keywords:
- SQLInstallTranslatorEx function [ODBC]
ms.assetid: a0630602-53c1-4db0-98ce-70d160aedf8d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43acc6708b5df71893c2c6b7658ca99bfb73f616
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018997"
---
# <a name="sqlinstalltranslatorex-function"></a>SQLInstallTranslatorEx 関数
**準拠**  
 バージョンが導入されました。ODBC 3.0  
  
 **まとめ**  
 **SQLInstallTranslatorEx**翻訳者に関する情報をシステム情報 (見つかりましたの Odbcinst.ini のセクションに追加されます。INI\ODBC トランスレーターのレジストリ キー)。  
  
 機能**SQLInstallTranslatorEx**にアクセスすることも[ODBCCONF します。EXE](../../../odbc/odbcconf-exe.md)します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLInstallTranslatorEx(  
     LPCSTR    lpszTranslator,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引数  
 *lpszTranslator*  
 [入力]これは、二重の null で終わる変換プログラムを記述するキーワードと値のペアの一覧を含める必要があります。 キーワードと値のペアの構文の詳細については、次を参照してください。[仕様のサブキー](../../../odbc/reference/install/translator-specification-subkeys.md)します。  
  
 **Translator**と**セットアップ**でキーワードを含める必要がある、 *lpszTranslator*文字列。 DLL が記載されている翻訳、 **Translator**キーワード、およびトランスレーター セットアップ DLL が記載されている、**セットアップ**キーワード。 各ペアは、NULL バイトで終了し、全体の一覧は NULL バイトで終了します。 (つまり、2 つの NULL バイトの末尾を示す一覧。)形式*lpszTranslator*のとおりです。  
  
 \0Translator=*translator-filename DLL*\0[Setup=*セットアップ-filename DLL*\0]\0  
  
 *lpszPathIn*  
 [入力]変換プログラムのインストールまたは null ポインターの完全パス。 場合*lpszPath* null ポインターの場合は、翻訳者は、システム ディレクトリにインストールされます。  
  
 *lpszPathOut*  
 [出力]変換プログラムのインストール先のターゲット ディレクトリのパス。 トランスレーターがインストールされていない場合*lpszPathOut*と同じ*lpszPathIn*します。 以前に、このトランスレータのインストールが存在する場合*lpszPathOut*は、以前のインストールのパスです。  
  
 *cbPathOutMax*  
 [入力]長さ*lpszPathOut します。*  
  
 *pcbPathOut*  
 [出力]返される使用可能なバイトの合計数*lpszPathOut*します。 返される使用可能なバイト数がより大きいかに等しい場合*cbPathOutMax*、出力パス*lpszPathOut*に切り捨てられます*pcbPathOutMax*マイナス、null 終了文字です。 *PcbPathOut*引数が null ポインターを指定できます。  
  
 *起こり*  
 [入力]要求の種類。 *起こり*値は次のいずれかを含める必要があります。  
  
 ODBC_INSTALL_INQUIRY:翻訳者をインストールできる場所について照会します。  
  
 ODBC_INSTALL_COMPLETE:インストール要求を完了します。  
  
 *lpdwUsageCount*  
 [出力]この関数が呼び出された後、変換プログラムの使用率カウントします。  
  
 アプリケーションでは、使用率カウントは設定しないでください。 ODBC では、この数を維持します。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合、FALSE が失敗した場合に TRUE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLInstallTranslatorEx** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーのエラー|エラーが発生する特定のインストーラーのエラーがなかった。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無効なバッファーの長さ|*LpszPathOut*引数が出力パスを格納するのに十分な大きさでした。 バッファーには、切り捨てられたパスが含まれています。<br /><br /> *CbPathOutMax*引数が 0 の場合、*起こり*引数が ODBC_INSTALL_COMPLETE します。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求の型が無効です。|*起こり*引数が、次のいずれか。<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無効なキーワードと値のペア|*LpszTranslator*引数には、構文エラーが含まれています。|  
|ODBC_ERROR_INVALID_PATH|無効なインストール パス|*LpszPathIn*引数に無効なパスが含まれています。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|無効なパラメーターのシーケンス|*LpszTranslator*引数には、キーワードと値のペアの一覧が含まれていませんでした。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|インクリメントまたはデクリメント、レジストリのコンポーネントの使用率カウントできませんでした。|Translator の使用状況のカウントをインクリメントするインストーラーが失敗しました。|  
  
## <a name="comments"></a>コメント  
 **SQLInstallTranslatorEx**変換プログラムをインストールするためのメカニズムを提供します。 この関数は、すべてのファイルを実際にはコピーしません。 呼び出し元のプログラムは、翻訳ファイルをコピーします。  
  
 **SQLInstallTranslatorEx**トランスレータをインストール済みコンポーネントの使用率カウントを 1 つインクリメントします。 変換プログラムのバージョンが既に存在する、変換プログラムのコンポーネントの使用カウントが存在しない場合は、新しいコンポーネントの使用状況カウント値が 2 に設定します。  
  
 アプリケーションのセットアップ プログラムは、物理的に翻訳ファイルをコピーし、ファイルの使用率カウントを維持します。 Translator ファイルが以前インストールされていない場合、アプリケーションのセットアップ プログラムがファイルまたはファイルをコピーし、ファイルまたはファイルの使用率カウントを作成する必要があります。 ファイルが既にインストールされている場合、セットアップ プログラムは単にファイルの使用率カウントをインクリメントします。  
  
 場合は、アプリケーションでは、変換プログラムの以前のバージョンがインストールされていた、translator がアンインストールされ、し再変換コンポーネントの使用率カウントは有効なようにする必要があります。 **SQLRemoveTranslator**コンポーネントの使用率カウントをデクリメントを呼び出す必要があり、 **SQLInstallTranslatorEx**コンポーネントの使用率カウントをインクリメントする呼び出す必要があります。 アプリケーションのセットアップ プログラムでは、新しいファイルを使用して、古いファイルまたはファイルを置き換える必要があります。 ファイルの使用率カウントは同じですが、引き続き、以前のバージョンのファイルを使用する他のアプリケーションは、新しいバージョンを使用してようになりました。  
  
 パスの長さ*lpszPathOut*で**SQLInstallTranslatorEx**により、2 フェーズのインストール プロセスでは、アプリケーションには、どのような判断できるように*cbPathOutMax*する必要があります呼び出してする**SQLInstallTranslatorEx**で、*起こり*ODBC_INSTALL_INQUIRY モードの。 使用できるバイトの合計数が返されます、 *pcbPathOut*バッファー。 **SQLInstallTranslatorEx**で呼び出すことができますし、*起こり*ODBC_INSTALL_COMPLETE の*cbPathOutMax*引数の値に設定、 *pcbPathOut*バッファーと、null 終了文字。  
  
 2 フェーズのモデルを使用しないように選択するかどうか**SQLInstallTranslatorEx**を設定する必要があります*cbPathOutMax*、として値 _MAX_PATH に、ターゲット ディレクトリのパスの記憶域のサイズを定義します。切り捨てを防ぐために、Stdlib.h で定義されます。  
  
 ときに*起こり*は ODBC_INSTALL_COMPLETE、 **SQLInstallTranslatorEx**により*lpszPathOut* NULL である (または*cbPathOutMax*0 になります)。 場合*起こり*ODBC_INSTALL_COMPLETE、返される使用可能なバイト数がより大きいまたは等しいときに、返される FALSE *cbPathOutMax*結果をその切り捨てが発生します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|翻訳の既定のオプションを返す|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|翻訳者を選択します。|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|翻訳者を削除します。|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
