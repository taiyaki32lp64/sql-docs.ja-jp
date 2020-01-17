---
title: コア インターフェイスの適合性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- core-level interface conformance levels [ODBC]
ms.assetid: aaaa864a-6477-45ff-a50a-96d8db66a252
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02e8aabf808ebf11f2e241fc7d330f794dbb0112
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002109"
---
# <a name="core-interface-conformance"></a>コア インターフェイスの適合性
すべての ODBC ドライバーは、少なくともコア レベルを示す必要がありますインターフェイスの適合性。 コア レベルの機能は、最も一般的な相互運用可能なアプリケーションに必要なものであるために、ドライバーは、このようなアプリケーションを操作できます。 コア レベルの機能には、ISO CLI 仕様で定義されている機能と、開いているグループ CLI 仕様で定義されている nonoptional 機能にも対応しています。 コア レベルのインターフェイスに準拠 ODBC ドライバーは、次のすべてのアプリケーションを使用できます。  
  
-   割り当て、ハンドルのすべての種類を呼び出すことによって解放**SQLAllocHandle**と**SQLFreeHandle**します。  
  
-   すべての形式を使用して、 **SQLFreeStmt**関数。  
  
-   呼び出すことにより、結果セットの列をバインド**SQLBindCol**します。  
  
-   動的パラメーターを呼び出すことによってのみ、入力方向のパラメーターの配列を含む処理**SQLBindParameter**と**SQLNumParams**します。 (出力方向のパラメーターで 203 の機能は[レベル 2 インターフェイスの適合性](../../../odbc/reference/develop-app/level-2-interface-conformance.md))。  
  
-   バインドのオフセットを指定します。  
  
-   呼び出しに関連する実行時のデータのダイアログ ボックスを使用して、 **SQLParamData**と**SQLPutData**します。  
  
-   呼び出すことによって、カーソルやカーソル名を管理**SQLCloseCursor**、 **SQLGetCursorName**、および**SQLSetCursorName**します。  
  
-   呼び出すことによって、結果セットの説明 (メタデータ) へのアクセスを得る**SQLColAttribute**、 **SQLDescribeCol**、 **SQLNumResultCols**、および**SQLRowCount**. (ブックマークのメタデータを取得する列番号 0 のこれらの関数の使用は 204 で機能が[レベル 2 インターフェイスの適合性](../../../odbc/reference/develop-app/level-2-interface-conformance.md))。  
  
-   カタログ関数を呼び出すことによって、データ ディクショナリをクエリ**SQLColumns**、 **SQLGetTypeInfo**、 **SQLStatistics**、および**SQLTables**します。  
  
     ドライバーは、データベース テーブルとビューのマルチパート名をサポートする必要はありません。 (詳細については、101 の機能を参照してください[レベル 1 インターフェイスの適合性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)で 201 の機能と[レベル 2 インターフェイスの適合性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)。ただし、列名の修飾やインデックスの名前など、SQL 92 仕様の特定の機能は、マルチパートの名前付けに相当する構文。 ODBC の機能の存在の一覧は、SQL 92 のこれらの側面に新しいオプションを導入するものではありません。  
  
-   データ ソースとの接続を呼び出すことによって管理**SQLConnect**、 **SQLDataSources**、 **SQLDisconnect**、および**SQLDriverConnect**します。 ODBC に関係なくレベル、サポート、呼び出すことによって、ドライバーに関する情報を入手**SQLDrivers**します。  
  
-   準備して呼び出すことによって、SQL ステートメントを実行**SQLExecDirect**、 **SQLExecute**、および**SQLPrepare**します。  
  
-   呼び出すことによって結果セットの 1 つの行または順方向のみに、複数の行をフェッチ**SQLFetch**または呼び出すことによって**SQLFetchScroll**で、 *FetchOrientation*引数SQL_FETCH_NEXT に設定します。  
  
-   パートでは、非バインド列を呼び出すことによって取得**SQLGetData**します。  
  
-   呼び出すことによって、すべての属性の現在の値を取得**SQLGetConnectAttr**、 **SQLGetEnvAttr**、および**SQLGetStmtAttr**、し、既定値にすべての属性を設定し、既定以外の値に特定の属性を呼び出すことによって設定**SQLSetConnectAttr**、 **SQLSetEnvAttr**、および**SQLSetStmtAttr**します。  
  
-   記述子の特定のフィールドを呼び出すことによって操作**SQLCopyDesc**、 **SQLGetDescField**、 **SQLGetDescRec**、 **SQLSetDescField**、**SQLSetDescRec**します。  
  
-   呼び出すことによって、診断情報を取得**SQLGetDiagField**と**SQLGetDiagRec**します。  
  
-   ドライバーの機能を呼び出すことによって検出**SQLGetFunctions**と**SQLGetInfo**します。 また、テキストの置換が呼び出すことによって、データ ソースに送信される前に、SQL ステートメントに加えられたすべての結果を検出**SQLNativeSql**します。  
  
-   構文を使用して**SQLEndTran**トランザクションをコミットします。 コア レベルのドライバー必要がある場合は true。 トランザクションをサポートしていませんそのため、アプリケーションを指定できません SQL_ROLLBACK も SQL_AUTOCOMMIT_OFF SQL_ATTR_AUTOCOMMIT 接続属性。 (詳細については、109 の機能を参照してください[レベル 2 インターフェイスの適合性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)。  
  
-   呼び出す**SQLCancel**実行時のデータ ダイアログをキャンセルして、マルチ スレッド環境で、ODBC 関数を実行して別のスレッドをキャンセルします。 コア レベルのインターフェイスの適合性、機能の非同期実行もの使用のサポートを必要としません**SQLCancel**を非同期的に実行する ODBC 関数を取り消します。 プラットフォームでも ODBC ドライバーにドライバーが個々 のアクティビティを同時に実行するためのマルチ スレッドを使用する必要があります。 ただし、マルチ スレッド環境で、ODBC ドライバーではスレッド セーフである必要があります。 アプリケーションからの要求のシリアル化は、パフォーマンスに重大な問題が発生する可能性がありますが、この仕様を実装するために準拠する方法です。  
  
-   呼び出すことによって、テーブルの SQL_BEST_ROWID の行を識別する列を取得**SQLSpecialColumns**します。 (SQL_ROWVER のサポートは、機能の 208 で[レベル 2 インターフェイスの適合性](../../../odbc/reference/develop-app/level-2-interface-conformance.md))。  
  
    > [!IMPORTANT]  
    >  ODBC ドライバーでは、コア インターフェイスの適合性レベルで関数を実装する必要があります。
