---
title: 位置指定更新 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- SQLSetPos function
- SQLSetCursorName function
- ODBC applications, cursors
- cursors [ODBC], positioned updates
- positioned updates [ODBC]
- ODBC cursors, positioned updates
ms.assetid: ff404e02-630f-474d-b5d4-06442b756991
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2336944b583b6077d75bd5155bb4b52c66d9a852
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200527"
---
# <a name="positioned-updates-odbc"></a>位置指定更新 (ODBC)
  ODBC では、カーソルで位置指定更新を実行するために、次の 2 とおりの方法をサポートします。  
  
-   **SQLSetPos**  
  
-   WHERE CURRENT OF 句  
  
 一般的な方法は、使用する**SQLSetPos**します。 次のオプションがあります。  
  
 SQL_POSITION  
 現在の行セットの特定行にカーソルを位置付けます。  
  
 SQL_REFRESH  
 カーソルが現在位置付けられている行から取り出した値で、結果セット列にバインドされているプログラム変数を更新します。  
  
 SQL_UPDATE  
 結果セット列にバインドされているプログラム変数に格納されている値で、カーソルの現在行を更新します。  
  
 SQL_DELETE  
 カーソルの現在行を削除します。  
  
 **SQLSetPos**設定、サーバー カーソルを使用して、ステートメント ハンドル カーソル属性が設定されている場合、ステートメントの結果で使用できます。 結果セットの列を、プログラム変数にバインドする必要があります。 アプリケーションは行のフェッチとすぐに呼び出して**SQLSetPos**(SQL_POSTION) を行にカーソルを位置付けます。 その後、アプリケーションは SQLSetPos(SQL_DELETE) を呼び出して現在行を削除するか、新しいデータ値をバインドされているプログラム変数に移動し、SQLSetPos(SQL_UPDATE) を呼び出して現在行を更新します。  
  
 アプリケーションの更新または削除を含む行セットの任意の行**SQLSetPos**します。 呼び出す**SQLSetPos**を構築して、SQL ステートメントの実行に代わる便利な方法です。 **SQLSetPos**は現在の行セットを操作しへの呼び出し後にのみ使用することができます[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)します。  
  
 呼び出して行セットのサイズが設定されて[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)属性引数 sql_attr_row_array_size を指定します。 **SQLSetPos**への呼び出し後にのみ、新しい行セットのサイズを使用して**SQLFetch**または**SQLFetchScroll**します。 たとえば、次の行セットのサイズを変更すると、 **SQLSetPos**が呼び出され、 **SQLFetch**または**SQLFetchScroll**が呼び出されます。 呼び出し**SQLSetPos**古いの行セット サイズが使用されますが、 **SQLFetch**または**SQLFetchScroll**新しい行セット サイズが使用されます。  
  
 行セット内の先頭行の行番号は 1 です。 引数には、RowNumber **SQLSetPos**行セット内の行を識別する必要がありますは、その値が 1 から最後にフェッチされた行の数の範囲である必要があります。 この値には、行セット サイズよりも小さい値を指定できます。 RowNumber が 0 の場合、操作は行セット内のすべての行に適用されます。  
  
 削除操作の**SQLSetPos**データ ソースのテーブルの 1 つまたは複数の選択した行を削除します。 行を削除する**SQLSetPos**、アプリケーション呼び出し**SQLSetPos** Operation に SQL_DELETE、RowNumber は、行の数を設定を削除するとします。 RowNumber が 0 の場合は、行セット内のすべての行が削除されます。  
  
 後**SQLSetPos**削除された行は、現在の行とその状態は SQL_ROW_DELETED を返します。 呼び出しなど、追加の位置指定操作で、行は使用できません[SQLGetData](../native-client-odbc-api/sqlgetdata.md)または**SQLSetPos**します。  
  
 アプリケーションがからの更新操作と同じように、行操作配列を使用して、特定の行を削除するドライバーを防ぐことができます (RowNumber が 0 に等しい)、行セットのすべての行を削除すると**SQLSetPos**します。  
  
 削除対象の各行は、行セット内に存在する行でなければなりません。 フェッチによってアプリケーション バッファーが設定され、行の状態配列が維持されている場合は、これら各行位置の行の状態値が SQL_ROW_DELETED、SQL_ROW_ERROR、または SQL_ROW_NOROW であってはなりません。  
  
 位置指定更新は、UPDATE、DELETE、および INSERT の各ステートメントに WHERE CURRENT OF 句を使用することによっても実行できます。 ときに生成、現在のカーソル名 ODBC が必要です、 [SQLGetCursorName](../native-client-odbc-api/sqlgetcursorname.md)関数が呼び出されると、または呼び出すことで指定できる**SQLSetCursorName**します。 次に、ODBC アプリケーションで WHERE CURRENT OF 更新の実行に使用する一般的な手順を示します。  
  
-   呼び出す**SQLSetCursorName**ステートメント ハンドルのカーソル名を確立するためにします。  
  
-   FOR UPDATE OF 句を指定した SELECT ステートメントを作成し、実行します。  
  
-   呼び出す**SQLFetchScroll**行セットを取得するまたは**SQLFetch**行を取得します。  
  
-   呼び出す**SQLSetPos** (sql_position) を呼び出して、行にカーソルを位置付けます。  
  
-   ビルドおよび設定でカーソル名を使用して WHERE CURRENT OF 句を使用した UPDATE ステートメントを実行**SQLSetCursorName**します。  
  
 代わりに、呼び出すことができます**SQLGetCursorName**呼び出す代わりに、SELECT ステートメントの実行後**SQLSetCursorName** SELECT ステートメントを実行する前にします。 **SQLGetCursorName**を使用してカーソル名を設定しない場合は、ODBC によって割り当てられた既定のカーソル名を返します**SQLSetCursorName**します。  
  
 **SQLSetPos**をお勧め WHERE CURRENT OF 経由でサーバー カーソルを使用しているときにします。 ODBC カーソル ライブラリで静的で更新可能なカーソルを使用している場合、カーソル ライブラリは、基になるテーブルのキー値を指定した WHERE 句を追加することで、WHERE CURRENT OF 更新を実装します。 テーブル内のキーが一意でない場合、意図しない更新が行われることがあります。  
  
## <a name="see-also"></a>参照  
 [カーソルを使用して&#40;ODBC&#41;](using-cursors-odbc.md)  
  
  
