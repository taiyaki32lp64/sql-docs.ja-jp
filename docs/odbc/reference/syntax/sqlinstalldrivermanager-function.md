---
title: SQLInstallDriverManager 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallDriverManager
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverManager
helpviewer_keywords:
- SQLInstallDriverManager function [ODBC]
ms.assetid: aebc439b-fffd-4d98-907a-0163f79aee8d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f1e3ac7f0a76c607fa07d6eb92d069d99ef5e0a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076209"
---
# <a name="sqlinstalldrivermanager-function"></a>SQLInstallDriverManager 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0:Windows XP Service Pack 2、Windows Server 2003 Service Pack 1 では、以降のオペレーティング システムで非推奨とされます。  
  
 **概要**  
 **SQLInstallDriverManager** ODBC コア コンポーネントのインストールのターゲット ディレクトリのパスを返します。 呼び出し元のプログラムは、ターゲット ディレクトリにドライバー マネージャーのファイルをコピー実際にする必要があります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>引数  
 *lpszPath*  
 [出力]インストールのターゲット ディレクトリのパス。  
  
 *cbPathMax*  
 [入力]長さ*lpszPath*します。 以上である必要がありますこれ _MAX_PATH バイト。  
  
 *pcbPathOut*  
 [出力]合計バイト数 (null 終了バイトを除く) で返される*lpszPath*します。 返される使用可能なバイト数がより大きいかに等しい場合*cbPathMax*、パス*lpszPath*に切り捨てられます*cbPathMax* null 終了マイナス文字。 *PcbPathOut*引数が null ポインターを指定できます。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合、FALSE が失敗した場合に TRUE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLInstallDriverManager** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーのエラー|エラーが発生する特定のインストーラーのエラーがなかった。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無効なバッファーの長さ|*LpszPath*引数が出力パスを格納するのに十分な大きさでした。 バッファーには、切り捨てられたパスが含まれています。<br /><br /> *CbPathMax*引数が _MAX_PATH より小さい。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|インクリメントまたはコンポーネントの使用率カウントは減少できませんでした。|ODBC コア コンポーネントの使用率カウントをインクリメントするインストーラーが失敗しました。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|インストーラーは、メモリ不足のため、関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **SQLInstallDriverManager**が呼び出され、パスの戻り値のシステム情報で ODBC コア コンポーネントとコンポーネントの使用状況の増分をカウントします。 ドライバー マネージャーのバージョンが既に存在するドライバーのコンポーネントの使用率カウントは存在しない場合は、新しいコンポーネントの使用状況カウント値が 2 に設定します。  
  
 アプリケーションのセットアップ プログラムはコア コンポーネントのファイルを物理的にコピー担当し、ファイルの使用状況の維持をカウントします。 コア コンポーネントのファイルが以前インストールされていない場合、アプリケーションのセットアップ プログラムはファイルのコピーし、ファイルの使用率カウントを作成する必要があります。 ファイルが既にインストールされている場合、セットアップ プログラムは単なるファイルの使用率カウントをインクリメントします。  
  
 場合は、アプリケーションのセットアップ プログラムによっては、以前のバージョンのドライバー マネージャーがインストールされていた、コア コンポーネントがアンインストールされ、再インストール、コア コンポーネントの使用率カウントは有効なようにする必要があります。 **SQLRemoveDriverManager**最初のコンポーネントの使用率カウントをデクリメントを呼び出す必要があります。 **SQLInstallDriverManager**し、コンポーネントの使用率カウントをインクリメントする呼び出す必要があります。 アプリケーションのセットアップ プログラムは、古いコア コンポーネント ファイルを新しいファイルに置き換える必要があります。 ファイル使用状況カウントが、同じままになります、および古いバージョンのコア コンポーネント ファイルを使用する他のアプリケーションがより新しいバージョンのファイルを使用するようになりました。  
  
 新規インストール ODBC コア コンポーネント、ドライバー、および翻訳者は、アプリケーションのセットアップ プログラムは、シーケンスで、次の関数を呼び出す必要があります。**SQLInstallDriverManager**、 **SQLInstallDriverEx**、 **SQLConfigDriver** (で、*起こり*ODBC_INSTALL_DRIVER の)、し**SQLInstallTranslatorEx**します。 コア コンポーネント、ドライバー、および変換プログラムのアンインストール、アプリケーションのセットアップ プログラムは、シーケンスで、次の関数を呼び出す必要があります。**SQLRemoveTranslator**、 **SQLRemoveDriver**、し**SQLRemoveDriverManager**します。 このシーケンスでは、これらの関数を呼び出す必要があります。 すべてのコンポーネントのアップグレードでは、シーケンスですべての削除関数を呼び出す必要があり、シーケンスで、すべてのインストール関数を呼び出す必要があります。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|追加、変更、またはドライバーを削除します。|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|ドライバーをインストールします。|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|変換プログラムをインストールします。|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|ドライバーを削除します。|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|ドライバー マネージャーを削除します。|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|翻訳者を削除します。|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
