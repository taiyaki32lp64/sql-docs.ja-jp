---
title: ドライバーの機能 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: 75dcdea6-ff6b-4ac8-aa11-a1f9edbeb8e6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5f27efed55a2ae63b8c3726263077441bdacc49b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135717"
---
# <a name="what-the-driver-does"></a>ドライバーの機能
次の表に、どのような機能とステートメント属性 ODBC *3.x*ブロックおよびスクロール可能なカーソルのドライバーを実装する必要があります。  
  
|関数または<br /><br /> ステートメント属性|コメント|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|行の状態配列のアドレスが入力セット**SQLFetch**と**SQLFetchScroll**します。 この配列はで塗りつぶされますも**SQLSetPos**場合**SQLSetPos** S6 ステートメントの状態で呼び出されます。 場合**SQLSetPos**呼びます S7 状態でこの配列は記入されていませんが、によって示される、配列、 *RowStatusArray*の引数**SQLExtendedFetch**が入力されます。 詳細については、次を参照してください[ステートメントの遷移](../../../odbc/reference/appendixes/statement-transitions.md)で付録 b:。ODBC の状態遷移のテーブル。|  
|SQL_ATTR_ROWS_FETCHED_PTR|バッファーのアドレスを設定**SQLFetch**と**SQLFetchScroll**フェッチされた行の数を返します。 場合**SQLExtendedFetch**が呼び出されると、このバッファーは記入されていませんが、 *RowCountPtr*引数がフェッチされた行の数を指します。|  
|SQL_ATTR_ROW_ARRAY_SIZE|使用される行セットのサイズを設定**SQLFetch**と**SQLFetchScroll**します。|  
|SQL_ROWSET_SIZE|使用される行セットのサイズを設定**SQLExtendedFetch**します。 ODBC *3.x*ドライバーではこれが実装される場合は ODBC を使用する*2.x*を呼び出すアプリケーション**SQLExtendedFetch**または**SQLSetPos**します。|  
|**SQLBulkOperations**|場合、ODBC *3.x*ドライバーは ODBC を使用する必要があります*2.x*を使用するアプリケーション**SQLSetPos**で、*操作*SQL_ADD、ドライバーが必要がありますサポート**SQLSetPos**で、*操作*に加えて SQL_ADD の**SQLBulkOperations**で、*操作*SQL の追加 (_A)。|  
|**SQLExtendedFetch**|指定した行セットを返します。 ODBC *3.x*ドライバーではこれが実装される場合は ODBC を使用する*2.x*を呼び出すアプリケーション**SQLExtendedFetch**または**SQLSetPos**します。 次に、実装の詳細を示します。<br /><br /> -ドライバーは、SQL_ROWSET_SIZE ステートメント属性の値から行セットのサイズを取得します。<br />-ドライバーは、行の状態配列からのアドレスを取得、 *RowStatusArray*引数、し、SQL_ATTR_ROW_STATUS_PTR ステートメント属性ではありません。 *RowStatusArray*への呼び出しで引数**SQLExtendedFetch** null ポインターをすることはできません。 (ODBC で*3.x*、し、SQL_ATTR_ROW_STATUS_PTR ステートメント属性は null ポインターであることができます)。<br />-ドライバーからフェッチされた行のバッファーのアドレスを取得する、 *RowCountPtr*引数、SQL_ATTR_ROWS_FETCHED_PTR ステートメント属性ではありません。<br />-ドライバーは SQLSTATE 01S01 を返します (行内のエラー) への呼び出しによって行がフェッチされたときにエラーが発生したことを示す**SQLExtendedFetch**します。 ODBC *3.x*ドライバーは SQLSTATE 01S01 を返す必要があります (エラー行の) 場合にのみ**SQLExtendedFetch**が呼び出されると、いないときに**SQLFetch**または**SQLFetchScroll**が呼び出されます。 旧バージョンとの互換性を維持するときに SQLSTATE 01S01 (行内のエラー) がによって返される**SQLExtendedFetch**、ドライバー マネージャーが、"シーケンスの状態で説明したルールに従って、エラー キュー内状態レコードを注文できませんレコード数"のセクション[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)します。|  
|**SQLFetch**|次の行セットを返します。 次に、実装の詳細を示します。<br /><br /> -ドライバーは、SQL_ATTR_ROW_ARRAY_SIZE ステートメント属性の値から行セットのサイズを取得します。<br />-ドライバーは、し、SQL_ATTR_ROW_STATUS_PTR ステートメント属性からの行の状態配列のアドレスを取得します。<br />-ドライバーは、SQL_ATTR_ROWS_FETCHED_PTR ステートメント属性からバッファーをフェッチされた行のアドレスを取得します。<br />-アプリケーションは、間の呼び出しを混在させることが**SQLFetchScroll**と**SQLFetch**します。<br />-   **SQLFetch**列 0 がバインドされている場合は、ブックマークを返します。<br />-   **SQLFetch**呼び出す 1 つ以上の行を返すことができます。<br />-ドライバーは SQLSTATE 01S01 を返しません (行内のエラー) への呼び出しによって行がフェッチされたときにエラーが発生したことを示す**SQLFetch**します。|  
|**SQLFetchScroll**|指定した行セットを返します。 次に、実装の詳細を示します。<br /><br /> -ドライバーは、SQL_ATTR_ROW_ARRAY_SIZE ステートメント属性から行セットのサイズを取得します。<br />-ドライバーは、し、SQL_ATTR_ROW_STATUS_PTR ステートメント属性からの行の状態配列のアドレスを取得します。<br />-ドライバーは、SQL_ATTR_ROWS_FETCHED_PTR ステートメント属性からバッファーをフェッチされた行のアドレスを取得します。<br />-アプリケーションは、間の呼び出しを混在させることが**SQLFetchScroll**と**SQLFetch**します。<br />-ドライバーは SQLSTATE 01S01 を返しません (行内のエラー) への呼び出しによって行がフェッチされたときにエラーが発生したことを示す**SQLFetchScroll**します。|  
|**SQLSetPos**|さまざまな位置指定操作を実行します。 次に、実装の詳細を示します。<br /><br /> -これは、S6、S7 またはステートメントの状態で呼び出すことができます。 詳細については、次を参照してください[ステートメントの遷移](../../../odbc/reference/appendixes/statement-transitions.md)で付録 b:。ODBC の状態遷移のテーブル。<br />場合、これは、S5 または S6 ステートメントの状態で呼び出されると、ドライバー、SQL_ATTR_ROWS_FETCHED_PTR ステートメント属性とし、SQL_ATTR_ROW_STATUS_PTR ステートメント属性からの行の状態配列のアドレスから行セットのサイズを取得します。<br />場合、これは、ステートメント状態 S7 で呼び出されると、ドライバーが SQL_ROWSET_SIZE ステートメント属性と、行の状態配列からのアドレスから行セットのサイズを取得、 *RowStatusArray*の引数**SQLExtendedFetch**します。<br />-ドライバーは SQLSTATE 01S01 を返します (行内のエラー) への呼び出しによって行がフェッチされたときにエラーが発生したことを示すためにのみ**SQLSetPos** S7 の状態で、関数が呼び出されると、一括操作を実行します。 場合は、旧バージョンとの互換性を保持するために SQLSTATE 01S01 (行内のエラー) がによって返される**SQLSetPos**、ドライバー マネージャーは「シーケンスの状態レコード」に記載されている規則に従って、エラー キュー内の状態レコードを注文できませんセクションの[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)します。<br />場合は、ドライバーは ODBC を使用する必要があります*2.x*を呼び出すアプリケーション**SQLSetPos**で、*操作*SQL_ADD の引数は、ドライバーをサポートする必要があります**SQLSetPos**で、*操作*SQL_ADD の引数。|
