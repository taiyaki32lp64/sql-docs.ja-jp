---
title: SQLWriteDSNToIni 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWriteDSNToIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteDSNToIni
helpviewer_keywords:
- SQLWriteDSNToIni [ODBC]
ms.assetid: dc7018b2-18d4-4657-96d0-086479a47474
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8eece6a1347aa7fba41577f66493e35f92a69d6f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039509"
---
# <a name="sqlwritedsntoini-function"></a>SQLWriteDSNToIni 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0  
  
 **概要**  
 **SQLWriteDSNToIni**システム情報をデータ ソースを追加します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLWriteDSNToIni(  
     LPCSTR   lpszDSN,  
     LPCSTR   lpszDriver);  
```  
  
## <a name="arguments"></a>引数  
 *lpszDSN*  
 [入力]追加するデータ ソースの名前です。  
  
 *lpszDriver*  
 [入力]ドライバーの名前 (通常は、関連付けられている DBMS の名前)、物理ドライバー名ではなくユーザーに表示されます。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合、FALSE が失敗した場合に TRUE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLWriteDSNToIni** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーのエラー|エラーが発生する特定のインストーラーのエラーがなかった。|  
|ODBC_ERROR_INVALID_DSN|無効な DSN|*LpszDSN*引数には、DSN に無効な文字列が含まれています。|  
|ODBC_ERROR_INVALID_NAME|無効なドライバーまたは翻訳者名|*LpszDriver*引数が無効です。|  
|ODBC_ERROR_REQUEST_FAILED|要求が失敗しました|インストーラーは、レジストリで、DSN を作成できませんでした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|インストーラーは、メモリ不足のため、関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **SQLWriteDSNToIni**のシステム情報 [ODBC データ ソース] セクションに、データ ソースを追加します。 データ ソースの仕様のセクションを作成し、1 つのキーワードを追加します (**ドライバー**) ドライバーの値として DLL の名前に置き換えます。 データ ソースの仕様のセクションが既に存在する場合**SQLWriteDSNToIni**新しいを作成する前に、古いセクションを削除します。  
  
 この関数の呼び出し元では、システム情報のデータ ソースの仕様のセクションに、ドライバー固有のキーワードと値を追加する必要があります。  
  
 データ ソースの名前が既定では場合、 **SQLWriteDSNToIni**システム情報の既定のドライバーの仕様のセクションも作成されます。  
  
 この関数は、DLL のセットアップからのみ呼び出す必要があります。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|追加、変更、またはデータ ソースを削除します。|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)(で DLL のセットアップ)|  
|追加、変更、またはデータ ソースを削除します。|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|システム情報のデータ ソース名を削除します。|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
