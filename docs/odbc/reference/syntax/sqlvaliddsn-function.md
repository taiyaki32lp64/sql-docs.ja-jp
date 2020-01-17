---
title: SQLValidDSN 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLValidDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLValidDSN
helpviewer_keywords:
- SQLValidDSN [ODBC]
ms.assetid: 930d1d89-337a-4429-85a2-84ee10555ac9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bbd8df72bcb0e76c8abcc3d738c2ff8da61a7bfe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039485"
---
# <a name="sqlvaliddsn-function"></a>SQLValidDSN 関数
**準拠**  
 バージョンが導入されました。ODBC 2.0  
  
 **概要**  
 **SQLValidDSN**名前は、システムの情報を追加する前に、長さとデータ ソース名の有効性を確認します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>引数  
 *lpszDSN*  
 [入力]データ ソースの名前を確認します。  
  
## <a name="returns"></a>戻り値  
 関数は、データ ソース名が有効な場合に TRUE を返します。 データ ソース名が無効であるか、関数呼び出しに失敗した場合は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLValidDSN** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 A  *\*pfErrorCode*が返されるだけ、関数呼び出しが失敗したかどうか、データ ソース名が無効なために、FALSE が返された場合にありません。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーのエラー|エラーが発生する特定のインストーラーのエラーがなかった。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|インストーラーは、メモリ不足のため、関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **SQLValidDSN**ドライバーのによって呼び出される[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)をデータ ソース名の長さと、データ ソースの個別の文字の有効性を確認します。 Sqlext.h で定義されている名前の長さが SQL_MAX_DSN_LENGTH より大きいかどうかを確認します。 (データ ソース名の長さがによってチェックも[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md))。**SQLValidDSN**の次の無効な文字がデータ ソース名に含めるかどうかを確認します。  
  
 [ ] { } ( ) , ; ? * = ! \@ \  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|追加、変更、またはデータ ソースを削除します。|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (で DLL のセットアップ)|  
|追加、変更、またはデータ ソースを削除します。|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|システム情報へのデータ ソース名の書き込み|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
