---
title: SQLRemoveDSNFromIni 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDSNFromIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDSNFromIni
helpviewer_keywords:
- SQLRemoveDSNFromIni function [ODBC]
ms.assetid: bb2e8273-7b61-4113-bfc8-f7ccc607c811
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4cc83a8cafffc9b5d1166df76d91ce4c63f0b858
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024532"
---
# <a name="sqlremovedsnfromini-function"></a>SQLRemoveDSNFromIni 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0  
  
 **概要**  
 **SQLRemoveDSNFromIni**システム情報から、データ ソースを削除します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>引数  
 *lpszDSN*  
 [入力]削除するデータ ソースの名前です。  
  
## <a name="returns"></a>戻り値  
 関数は、データ ソースを削除または Odbc.ini ファイルで、データ ソースはなかった場合に TRUE を返します。 データ ソースの削除に失敗した場合は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLRemoveDSNFromIni** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーのエラー|エラーが発生する特定のインストーラーのエラーがなかった。|  
|ODBC_ERROR_INVALID_DSN|無効な DSN|*LpszDSN*引数が無効です。|  
|ODBC_ERROR_REQUEST_FAILED|要求が失敗しました|インストーラーは、レジストリから DSN 情報を削除できませんでした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|インストーラーは、メモリ不足のため、関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **SQLRemoveDSNFromIni**のシステム情報 [ODBC データ ソース] セクションから、データ ソース名を削除します。 データ ソースの仕様のセクションでは、システム情報からも削除されます。  
  
 この関数は、ドライバーのセットアップのライブラリからのみ呼び出す必要があります。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|追加、変更、またはデータ ソースを削除します。|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|追加、変更、またはデータ ソースを削除します。|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|既定のデータ ソースを削除します。|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|システム情報へのデータ ソース名の追加|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
