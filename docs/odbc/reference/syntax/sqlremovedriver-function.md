---
title: SQLRemoveDriver 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDriver
helpviewer_keywords:
- SQLRemoveDriver function [ODBC]
ms.assetid: 9a3b4f8b-982b-44b9-ade6-754ff026dc90
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a86d958114a0755d8aead4470936115902f9c57a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024554"
---
# <a name="sqlremovedriver-function"></a>SQLRemoveDriver 関数
**準拠**  
 バージョンが導入されました。ODBC 3.0  
  
 **概要**  
 **SQLRemoveDriver**変更やシステム情報の Odbcinst.ini のエントリから、ドライバーに関する情報を削除します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引数  
 *lpszDriver*  
 [入力]システム情報の Odbcinst.ini のキーに登録されているドライバーの名前。  
  
 *fRemoveDSN*  
 [入力]有効な値は次のとおりです。  
  
 TRUE:Dsn に指定されたドライバーに関連付けられている削除*lpszDriver*します。 FALSE:Dsn に指定されたドライバーに関連付けられているを削除しないでください*lpszDriver*します。  
  
 *lpdwUsageCount*  
 [出力]この関数が呼び出された後、ドライバーの使用率カウントします。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合、FALSE が失敗した場合に TRUE を返します。 エントリが存在しない場合、システムの情報でこの関数が呼び出されたときに、関数は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLRemoveDriver** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーのエラー|エラーが発生する特定のインストーラーのエラーがなかった。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|コンポーネントがレジストリに見つかりません|インストーラーは、レジストリに存在しないか、レジストリで見つかりませんでした、ドライバーの情報を削除できませんでした。|  
|ODBC_ERROR_INVALID_NAME|無効なドライバーまたは翻訳者名|*LpszDriver*引数が無効です。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|インクリメントまたはコンポーネントの使用率カウントは減少できませんでした。|ドライバーの使用率カウントをデクリメントするインストーラーが失敗しました。|  
|ODBC_ERROR_REQUEST_FAILED|要求が失敗しました|*FRemoveDSN*引数が TRUE。 ただし、1 つまたは複数の Dsn を削除できませんでした。 呼び出し**SQLConfigDriver** ODBC_REMOVE_DRIVER 要求に失敗しました。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|インストーラーは、メモリ不足のため、関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **SQLRemoveDriver**補完、 [SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)関数と更新コンポーネントの使用法のシステム情報の数します。 この関数は、セットアップ アプリケーションからのみ呼び出す必要があります。  
  
 **SQLRemoveDriver**コンポーネントの使用状況カウントの値は 1 減ります。 コンポーネントの使用率カウントを 0 にした場合、次が発生します。  
  
1.  **SQLConfigDriver** ODBC_REMOVE_DRIVER オプションを使用して関数が呼び出されます。 場合、 *fRemoveDSN*オプションが TRUE に設定、 **ConfigDSN**関数呼び出し**SQLRemoveDSNFromIni**で指定されたドライバーに関連付けられているすべてのデータ ソースを削除するには*lpszDriver します。* 場合、 *fRemoveDSN*オプションが FALSE に設定されて、データ ソースは削除されません。  
  
2.  システム情報では driver エントリは削除されます。 Driver エントリは、ドライバーの名前で、次のシステム情報場所には。  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **SQLRemoveDriver**すべてのファイルを実際に削除されません。 呼び出し元のプログラムは、ファイルを削除して、ファイルの使用率カウントを維持します。 コンポーネントの使用率カウントと使用状況ファイルの数に達した後にのみ、0 は、物理的に削除ファイルになります。 コンポーネントの一部のファイルを削除して他のユーザー削除されません、ファイルの使用率カウントをインクリメントが他のアプリケーションでファイルを使用するかどうかによって異なります。  
  
 **SQLRemoveDriver**アップグレード プロセスの一部としても呼ばれます。 アプリケーションは、アップグレードを実行する必要があることと、ドライバーが既にインストールを検出した場合、ドライバーを削除して再インストールする必要があります。 **SQLRemoveDriver**コンポーネントの使用率カウントをデクリメントを呼び出す必要がありますまずし**SQLInstallDriverEx**コンポーネントの使用率カウントをインクリメントする呼び出す必要があります。 アプリケーションのセットアップ プログラムは、古いファイルを新しいファイルに置き換える必要があります。 ファイルの使用率カウントは同じですが、引き続き、以前のバージョンのファイルを使用する他のアプリケーションは、新しいバージョンを使用してようになりました。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|追加、変更、またはドライバーを削除します。|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md) (で DLL のセットアップ)|  
|追加、変更、またはドライバーを削除します。|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|ドライバーをインストールします。|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
