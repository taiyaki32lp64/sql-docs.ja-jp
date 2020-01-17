---
title: SQLInstallDriverEx 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallDriverEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverEx
helpviewer_keywords:
- SQLInstallDriverEx function [ODBC]
ms.assetid: 1dd74544-f4e9-46e1-9b5f-c11d84fdab4c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 673e3e53468780ef261a22b00a2ec1bb9df0e184
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030605"
---
# <a name="sqlinstalldriverex-function"></a>SQLInstallDriverEx 関数
**準拠**  
 バージョンが導入されました。ODBC 3.0  
  
 **まとめ**  
 **SQLInstallDriverEx**システム情報の Odbcinst.ini のエントリに、ドライバーに関する情報を追加し、インクリメント、ドライバーの*UsageCount*を 1 つ。 ただし、バージョンのドライバー、既に存在する場合が、 *UsageCount*値のドライバーが存在しない新しい*UsageCount*値が 2 に設定します。  
  
 この関数は、すべてのファイルを実際にはコピーしません。 ドライバーのファイルを正しくターゲット ディレクトリにコピーする呼び出し元のプログラムの役目です。  
  
 機能**SQLInstallDriverEx**にアクセスすることも[ODBCCONF します。EXE](../../../odbc/odbcconf-exe.md)します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLInstallDriverEx(  
     LPCSTR    lpszDriver,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引数  
 *lpszDriver*  
 [入力]物理ドライバー名の代わりにユーザーに表示されるドライバーの名前 (通常は、関連付けられている DBMS の名前)。 *LpszDriver*引数は、二重の null で終わる、ドライバーを記述するキーワードと値のペアの一覧を含める必要があります。 キーワードと値のペアの詳細については、次を参照してください。[ドライバーの仕様のサブキー](../../../odbc/reference/install/driver-specification-subkeys.md)します。 二重の null で終わる文字列の詳細については、次を参照してください。 [ConfigDSN 関数](../../../odbc/reference/syntax/configdsn-function.md)します。  
  
 *lpszPathIn*  
 [入力]インストール、または null ポインターのターゲット ディレクトリの完全パス。 場合*lpszPathIn* null ポインターの場合は、ドライバーはシステム ディレクトリにインストールされます。  
  
 *lpszPathOut*  
 [出力]ドライバーのインストール先のターゲット ディレクトリのパス。 ドライバーが既にインストールされていない場合、 *lpszPathOut*と同じである必要があります*lpszPathIn*します。 ドライバーがインストールされていた場合*lpszPathOut*は、以前のインストール パスです。  
  
 *cbPathOutMax*  
 [入力]長さ*lpszPathOut*します。  
  
 *pcbPathOut*  
 [出力]\(Null 終了文字を除く) バイトの合計数で返される使用可能な*lpszPathOut*です。 返される使用可能なバイト数がより大きいかに等しい場合*cbPathOutMax*、出力パス*lpszPathOut*に切り捨てられます*cbPathOutMax*マイナス、null 終了文字です。 *PcbPathOut*引数が null ポインターを指定できます。  
  
 *起こり*  
 [入力]要求の種類。 *起こり*引数は、次の値のいずれかを含める必要があります。  
  
 ODBC_INSTALL_INQUIRY:ドライバーをインストールできる場所について照会します。  
  
 ODBC_INSTALL_COMPLETE:インストール要求を完了します。  
  
 *lpdwUsageCount*  
 [出力]この関数が呼び出された後、ドライバーの使用率カウントします。  
  
 アプリケーションでは、使用率カウントは設定しないでください。 ODBC では、この数を維持します。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合、FALSE が失敗した場合に TRUE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLInstallDriverEx** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーのエラー|エラーが発生する特定のインストーラーのエラーがなかった。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無効なバッファーの長さ|*LpszPathOut*引数が出力パスを格納するのに十分な大きさでした。 バッファーには、切り捨てられたパスが含まれています。<br /><br /> *CbPathOutMax*引数が 0 の場合と*起こり*ODBC_INSTALL_COMPLETE でした。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求の型が無効です。|*起こり*引数が、次のいずれか。<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無効なキーワードと値のペア|*LpszDriver*引数には、構文エラーが含まれています。|  
|ODBC_ERROR_INVALID_PATH|無効なインストール パス|*LpszPathIn*引数に無効なパスが含まれています。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|ドライバーまたはトランスレーター セットアップ ライブラリを読み込むことができません。|ドライバーのセットアップのライブラリを読み込むことができませんでした。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|無効なパラメーターのシーケンス|*LpszDriver*引数には、キーワードと値のペアの一覧が含まれていませんでした。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|インクリメントまたはコンポーネントの使用率カウントは減少できませんでした。|ドライバーの使用状況のカウントをインクリメントするインストーラーが失敗しました。|  
  
## <a name="comments"></a>コメント  
 *LpszDriver*引数は、キーワードと値のペアの形式で属性の一覧を示します。 各ペアは、null バイトで終了し、全体の一覧は null バイトで終了します。 (つまり、2 つの null バイトの末尾を示す一覧。)この一覧の形式は次のとおりです。  
  
 _ドライバー desc_ **\\** 0Driver **=** _ドライバー-filename DLL_ **\\** 0 [セットアップ **=** _セットアップ-filename DLL_<b>\\</b>0]  
  
 [_ドライバー-attr-keyword1_ **=** _value1_<b>\\</b>0] [_ドライバー-attr-keyword2_ **=** _value2_<b>\\</b>0].<b> \\ </b>0  
  
 \0 の null バイトがあると*ドライバー-attr-keywordn*ドライバー属性のいずれかのキーワードは、します。 キーワードは、指定した順序で表示する必要があります。 たとえば、書式設定されたテキスト ファイル用のドライバーが個別のドライバーと Dll のセットアップとし、.txt および .csv の拡張子を持つファイルを使用できます。 *LpszDriver*引数のこのドライバーで次のようにある可能性があります。  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 SQL Server 用のドライバーが別のセットアップ DLL ではありませんし、ドライバー属性キーワードはありませんとします。 *LpszDriver*引数のこのドライバーで次のようにある可能性があります。  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 後**SQLInstallDriverEx**からドライバーに関する情報を取得、 *lpszDriver*引数、システムの Odbcinst.ini のエントリの [ODBC Drivers] セクションに、ドライバーの説明を追加します情報。 ドライバーの説明を持つというセクションを作成し、ドライバ DLL の完全パスとセットアップ DLL を追加します。 最後に、インストールのターゲット ディレクトリのパスを返しますが、ドライバー ファイルをコピーはありません。 呼び出し元のプログラムは、ターゲット ディレクトリにドライバー ファイルをコピーする必要があります実際にします。  
  
 **SQLInstallDriverEx**を 1 つインストールされているドライバーのコンポーネントの使用率カウントをインクリメントします。 ドライバーのバージョンが既に存在するドライバーのコンポーネントの使用率カウントは存在しない場合は、新しいコンポーネントの使用状況カウント値が 2 に設定します。  
  
 アプリケーションのセットアップ プログラムは、物理的にドライバー ファイルをコピーし、ファイルの使用率カウントを維持します。 ドライバー ファイルが以前インストールされていない場合、アプリケーションのセットアップ プログラムがでファイルをコピーする必要があります、 *lpszPathIn*パスとファイルの使用率カウントを作成します。 セットアップ プログラムは、ファイルが既にインストールされている場合、単ファイルの使用率カウントをインクリメントし、以前のインストールでのパスを返します、 *lpszPathOut*引数。  
  
> [!NOTE]  
>  使用状況カウントがコンポーネントと使用状況カウントがファイルの詳細については、次を参照してください。[使用状況のカウント](../../../odbc/reference/install/usage-counting.md)します。  
  
 場合は、アプリケーションでは、以前のバージョンのドライバー ファイルがインストールされていた、ドライバーをアンインストールし、再インストール、ドライバー コンポーネントの使用率カウントは有効なようにする必要があります。 **SQLConfigDriver** (で、*起こり*ODBC_REMOVE_DRIVER の) 必要がありますまず呼び出され、し**SQLRemoveDriver**コンポーネントの使用率カウントをデクリメントを呼び出す必要があります。 **SQLInstallDriverEx**し、コンポーネントの使用率カウントをインクリメント、ドライバを再インストールを呼び出す必要があります。 アプリケーションのセットアップ プログラムは、古いファイルを新しいファイルに置き換える必要があります。 ファイルの使用率カウントは同じですが、引き続き、以前のバージョンのファイルを使用して、他のアプリケーションは、新しいバージョンを使用してようになりました。  
  
> [!NOTE]  
>  ドライバーがインストールされていた場合と**SQLInstallDriverEx**関数は TRUE、別のディレクトリにドライバーをインストールすると呼びますが、 *lpszPathOut*にディレクトリを含めるドライバーが既にインストールされています。 これで入力したディレクトリに含まれませんが、 *lpszDriver*引数。  
  
 パスの長さ*lpszPathOut*で**SQLInstallDriverEx**により、2 フェーズのインストール プロセスでは、アプリケーションには、どのような判断できるように*cbPathOutMax*である必要があります呼び出す**SQLInstallDriverEx**で、*起こり*ODBC_INSTALL_INQUIRY モード。 使用できるバイトの合計数が返されます、 *pcbPathOut*バッファー。 **SQLInstallDriverEx**で呼び出すことができますし、*起こり*ODBC_INSTALL_COMPLETE の*cbPathOutMax*引数の値に設定、 *pcbPathOut*バッファーと、null 終了文字。  
  
 2 フェーズのモデルを使用しないように選択するかどうか**SQLInstallDriverEx**を設定する必要があります*cbPathOutMax*、として値 _MAX_PATH に、ターゲット ディレクトリのパスの記憶域のサイズを定義します。切り捨てを防ぐために、Stdlib.h で定義されます。  
  
 ときに*起こり*ODBC_INSTALL_COMPLETE は、 **SQLInstallDriverEx**により*lpszPathOut* NULL である (または*cbPathOutMax*にする0 の場合)。 場合*起こり*ODBC_INSTALL_COMPLETE、返される使用可能なバイト数がより大きいまたは等しいときに、返される FALSE *cbPathOutMax*結果をその切り捨てが発生します。  
  
 後**SQLInstallDriverEx**が呼び出されたとアプリケーションのセットアップ プログラムは、必要に応じて、ドライバー ファイルがコピー、ドライバーのセットアップ DLL を呼び出す必要があります**SQLConfigDriver**構成を設定しますドライバー。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|ドライバー マネージャーのインストール|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
