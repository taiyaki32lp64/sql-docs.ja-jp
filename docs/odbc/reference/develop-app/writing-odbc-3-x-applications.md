---
title: ODBC 3.x アプリケーションの作成 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], about upgrading
- ODBC drivers [ODBC], backward compatibility
- upgrading applications [ODBC]
- compatibility [ODBC], upgrading applications
- application upgrades [ODBC]
- upgrading applications [ODBC], about upgrading
- backward compatibility [ODBC], upgrading applications
ms.assetid: 19c54fc5-9dd6-49b6-8c9f-a38961b40a65
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9939d11e3a779cc25d7faeb4950783353947f140
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081454"
---
# <a name="writing-odbc-3x-applications"></a>ODBC 3.x アプリケーションの作成
ときに、ODBC *2.x*を ODBC アプリケーションはアップグレード*3.x*、ODBC の両方で機能するように書き込む*2.x*と*3.x*ドライバー. アプリケーションは、ODBC のフル活用するために条件付きのコードを組み込む必要があります*3.x*機能します。  
  
 SQL_OV_ODBC2 を SQL_ATTR_ODBC_VERSION 環境属性を設定する必要があります。 これにより、ドライバーは ODBC のように動作する*2.x*セクションで説明されている変更に関するドライバー[動作が変更される](../../../odbc/reference/develop-app/behavioral-changes.md)します。  
  
 アプリケーションが、セクションで説明されている機能のいずれか使うかどうか[の新機能](../../../odbc/reference/develop-app/new-features.md)、条件付きのコードを使用して、ドライバーが ODBC であるかどうかを判断する必要が*3.x*または ODBC *2.x*ドライバー。 アプリケーションを使用して**SQLGetDiagField**と**SQLGetDiagRec** ODBC を取得する*3.x* SQLSTATEs これらの条件付きのコード フラグメントの処理中にエラーを実行中にします。 新しい機能については、次の点を考慮する必要があります。  
  
-   行セット サイズの動作の変更によって影響を受けるアプリケーションを呼び出すしないように注意する必要があります**SQLFetch**配列のサイズが 1 より大きい場合。 これらのアプリケーションへの呼び出しを置き換える必要があります**SQLExtendedFetch**への呼び出しに**SQLSetStmtAttr** SQL_ATTR_ARRAY_STATUS_PTR ステートメント属性を設定して**SQLFetchScroll**ODBC の両方で動作する一般的なコードがあるため、 *3.x*および ODBC *2.x*ドライバー。 **SQLSetStmtAttr** SQL_ATTR_ROW_ARRAY_SIZE にマップされる**SQLSetStmtAttr** SQL_ROWSET_SIZE for ODBC を*2.x*ドライバー、アプリケーションは SQL を設定してできますのみその複数行のフェッチ操作 _ATTR_ROW_ARRAY_SIZE します。  
  
-   アップグレードするほとんどのアプリケーションは、SQLSTATE コードの変更によって実際には影響ありません。 影響を受けるアプリケーションには、機械的な検索を実行し、「SQLSTATE マッピング」のセクションではエラーの変換テーブルを使用して、ODBC を変換するほとんどの場合を指定して置換することができます*3.x* odbc エラー コード*2.x*コード。 以降、ODBC *3.x*ドライバー マネージャーは ODBC からマッピングを実行*2.x* odbc SQLSTATEs *3.x* SQLSTATEs、これらのアプリケーションの作成者にODBC用のチェックだけが必要があります*3.x* SQLSTATEs し、ODBC などについて心配ありません*2.x* SQLSTATEs で条件付きコード。  
  
-   アプリケーションが自身の ODBC を宣言できますアプリケーション日付、時刻、および timestamp データ型の場合は、 *2.x*コスト コードを使用する代わりに、既存のコードをアプリケーションおよび使用します。  
  
 アップグレードでは、次の手順を含める必要があります。  
  
-   呼び出す**SQLSetEnvAttr** SQL_OV_ODBC2 を SQL_ATTR_ODBC_VERSION 環境属性を設定する接続を割り当てる前にします。  
  
-   すべての呼び出しを置き換える**SQLAllocEnv**、 **SQLAllocConnect**、または**SQLAllocStmt**への呼び出しに**SQLAllocHandle**と適切な*HandleType* sql_handle_env として、sql_handle_dbc として、または sql_handle_stmt としての引数。  
  
-   すべての呼び出しを置き換える**SQLFreeEnv**または**SQLFreeConnect**への呼び出しに**SQLFreeHandle**と適切な*HandleType*引数sql_handle_dbc としてまたは sql_handle_stmt として。  
  
-   すべての呼び出しを置き換える**SQLSetConnectOption**への呼び出しに**SQLSetConnectAttr**します。 属性の値の設定が文字列の場合、設定、 *StringLength*引数適切にします。 変更*属性*SQL_ATTR_XXXX SQL_XXXX から引数。  
  
-   すべての呼び出しを置き換える**SQLGetConnectOption**への呼び出しに**SQLGetConnectAttr**します。 文字列またはバイナリ属性を取得する場合は、設定*BufferLength*に適切な値を渡します、 *StringLength*引数。 変更*属性*SQL_ATTR_XXXX SQL_XXXX から引数。  
  
-   すべての呼び出しを置き換える**SQLSetStmtOption**への呼び出しに**SQLSetStmtAttr**します。 属性の値の設定が文字列の場合、設定、 *StringLength*引数適切にします。 変更*属性*SQL_ATTR_XXXX SQL_XXXX から引数。  
  
-   すべての呼び出しを置き換える**SQLGetStmtOption**への呼び出しに**SQLGetStmtAttr**します。 文字列またはバイナリ属性を取得する場合は、設定*BufferLength*に適切な値を渡します、 *StringLength*引数。 変更*属性*SQL_ATTR_XXXX SQL_XXXX から引数。  
  
-   すべての呼び出しを置き換える**SQLTransact**への呼び出しに**SQLEndTran**します。 場合の最も右にある有効なハンドル、 **SQLTransact**呼び出しは、環境ハンドルを*HandleType* sql_handle_env としての引数を使用する必要があります、 **SQLEndTran**を呼び出す適切な*処理*引数。 場合の最も右にある有効なハンドル、 **SQLTransact**呼び出しは、接続ハンドルを*HandleType* sql_handle_dbc としての引数を使用する必要があります、 **SQLEndTran**を呼び出す適切な*処理*引数。  
  
-   すべての呼び出しを置き換える**SQLColAttributes**への呼び出しに**SQLColAttribute**します。 場合、 *FieldIdentifier* SQL_COLUMN_PRECISION、SQL_COLUMN_SCALE、または SQL_COLUMN_LENGTH のいずれかに引数がある関数の名前以外にも変更しないでください場合、。 そうでない場合は、変更*FieldIdentifier* SQL_COLUMN_XXXX SQL_DESC_XXXX するからです。 場合*FieldIdentifier* SQL_DESC_CONCISE_TYPE データ型が datetime データ型であり、対応する ODBC に変更*3.x*データ型。  
  
-   ブロック カーソル、スクロール可能なカーソル、またはその両方を使用して、アプリケーションは次の。  
  
    -   行セットのサイズ、カーソルの種類、およびカーソルの同時実行制御を使用して設定**SQLSetStmtAttr**します。  
  
    -   呼び出し**SQLSetStmtAttr**状態レコードの配列を指すようにし、SQL_ATTR_ROW_STATUS_PTR を設定します。  
  
    -   呼び出し**SQLSetStmtAttr** SQLINTEGER を指す SQL_ATTR_ROWS_FETCHED_PTR を設定します。  
  
    -   必要なバインディングを実行し、SQL ステートメントを実行します。  
  
    -   呼び出し**SQLFetchScroll**で行をフェッチし、結果内を移動するループを設定します。  
  
    -   ブックマークによるをフェッチする必要がある場合、アプリケーションが呼び出す**SQLSetStmtAttr** SQL_ATTR_FETCH_BOOKMARK_PTR を呼び出し、フェッチする行のブックマークを含む変数を設定する**SQLFetchScroll**で、 *FetchOrientation* SQL_FETCH_BOOKMARK の引数。  
  
-   パラメーターの配列を使用する場合、アプリケーションは、次の。  
  
    -   呼び出し**SQLSetStmtAttr** SQL_ATTR_PARAMSET_SIZE 属性パラメーターの配列のサイズを設定します。  
  
    -   呼び出し**SQLSetStmtAttr**内部 UDWORD 変数を指す SQL_ATTR_ROWS_PROCESSED_PTR を設定します。  
  
    -   実行の準備、バインド、および適切な操作を実行します。  
  
    -   何らかの理由 (SQL_NEED_DATA) などの実行が停止し場合、は、SQL_ATTR_ROWS_PROCESSED_PTR によって示される場所を調べることによってパラメーターの「現在」の行を検索ができます。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [アプリケーションの旧バージョンとの互換性のためのマッピング置換関数](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [SQLCloseCursor の呼び出し](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [SQLGetDiagField の呼び出し](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [SQLSetPos の呼び出し](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [カーソル ライブラリの操作](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [Cursor Attributes1 の情報の種類のマッピング](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
