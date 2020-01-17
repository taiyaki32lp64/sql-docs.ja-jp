---
title: SQLRemoveTranslator 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveTranslator
helpviewer_keywords:
- SQLRemoveTranslator function [ODBC]
ms.assetid: c6feda49-0359-4224-8de9-77125cf2397b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8a577a868f7b56a6677da3cb12cfb29057ea66f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024524"
---
# <a name="sqlremovetranslator-function"></a>SQLRemoveTranslator 関数
**準拠**  
 バージョンが導入されました。ODBC 3.0  
  
 **概要**  
 **SQLRemoveTranslator**情報を削除しますトランスレーターのシステム情報とデクリメント Odbcinst.ini セクションから、変換プログラムのコンポーネントの使用率カウントを 1 つ。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引数  
 *lpszTranslator*  
 [入力]システム情報の Odbcinst.ini のキーに登録されている変換プログラムの名前。  
  
 *lpdwUsageCount*  
 [出力]この関数が呼び出された後、変換プログラムの使用率カウントします。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合、FALSE が失敗した場合に TRUE を返します。 エントリが存在しない場合、システムの情報でこの関数が呼び出されたときに、関数は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLRemoveTranslator** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーのエラー|エラーが発生する特定のインストーラーのエラーがなかった。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|コンポーネントがレジストリに見つかりません|レジストリに存在しないか、レジストリで見つかりませんでした、インストーラーは変換プログラムの情報を削除できませんでした。|  
|ODBC_ERROR_INVALID_NAME|無効なドライバーまたは翻訳者名|*LpszTranslator*引数が無効です。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|インクリメントまたはコンポーネントの使用率カウントは減少できませんでした。|ドライバーの使用率カウントをデクリメントするインストーラーが失敗しました。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|インストーラーは、メモリ不足のため、関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **SQLRemoveTranslator**補完、 [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)関数と更新コンポーネントの使用法のシステム情報の数します。 この関数は、セットアップ アプリケーションからのみ呼び出す必要があります。  
  
 **SQLRemoveTranslator**を 1 つのコンポーネントの使用率カウントをデクリメントします。 コンポーネントの使用率カウントを 0 にした場合は、システム情報の変換プログラムのエントリが削除されます。 Translator エントリは、システムについては、翻訳者名の下に次の場所には。  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator**すべてのファイルを実際に削除されません。 呼び出し元のプログラムは、ファイルを削除して、ファイルの使用率カウントを保守を担当します。 コンポーネントの使用率カウントと使用状況ファイルの数に達した後にのみ、0 は、物理的に削除ファイルになります。 コンポーネントの一部のファイルを削除して他のユーザー削除されません、ファイルの使用率カウントをインクリメントが他のアプリケーションでファイルを使用するかどうかによって異なります。  
  
 **SQLRemoveTranslator**アップグレード プロセスの一部としても呼ばれます。 アプリケーションは、アップグレードを実行する必要があることと、ドライバーが既にインストールを検出した場合、ドライバーを削除して再インストールする必要があります。 **SQLRemoveTranslator**コンポーネントの使用率カウントをデクリメントを呼び出す必要がありますまずし**SQLInstallTranslatorEx**コンポーネントの使用率カウントをインクリメントする呼び出す必要があります。 アプリケーションのセットアップ プログラムでは、新しいファイルに古いファイルを置き換える必要がありますに物理的にします。 ファイルの使用率カウントは同じですが、引き続き、以前のバージョンのファイルを使用する他のアプリケーションは、新しいバージョンを使用してようになりました。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|変換プログラムをインストールします。|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
