---
title: コア レベル API 関数 (ODBC Driver for Oracle) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- core level API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 8596eed7-bda6-4cac-ae1f-efde1aab785f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cc95ec17dc221cb77bd94fc3378af483aeee92dd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081969"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>コア レベルの API 関数 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用します。  
  
 このレベルでの関数は、ODBC ドライバーのインターフェイスの適合性の最小レベルを構成します。  
  
|API 関数|メモ|  
|------------------|-----------|  
|**SQLAllocConnect**|接続ハンドル用にメモリを割り当てます*hdbc*で識別される環境内で*henv*します。 ドライバー マネージャーは、この呼び出しを処理し、ドライバーの呼び出し**SQLAllocConnect**たびに関数**SQLConnect**、 **SQLBrowseConnect**、または**SQLDriverConnect**が呼び出されます。|  
|**SQLAllocEnv**|Oracle クライアント ソフトウェアの要件を指定するダイアログ ボックスを表示し、SQL_NULL_HANDLE を返します。 この関数が、環境ハンドルのメモリを割り当て、Oracle クライアント ソフトウェアがインストールされていない場合*henv*、し、アプリケーションで使用するための ODBC 呼び出しレベルのインターフェイスを初期化します。|  
|**SQLAllocStmt**|ステートメント ハンドルのメモリを割り当てし、ステートメント ハンドルを hdbc によって指定された接続に関連付けます。 ドライバー マネージャーは、hstmt 構造体のメモリを割り当てて、ドライバーには、この呼び出しを渡します。|  
|**SQLBindCol**|結果列の記憶域スペースを割り当てるし、結果の型を指定します。|  
|**SQLCancel**|Hstmt、ステートメント ハンドルでの処理をキャンセルします。 場合によっては、Oracle では実行中のステートメントの取り消しを使用することはできません。 これは、Oracle ODBC Driver for Oracle でどの時点で、ステートメントの結果が取り消された、プロセスを完了するまで実行中のステートメントを続行することを意味します。|  
|**SQLColAttributes**|結果セット内の列の記述子の情報を返します。 記述子の情報は、文字列、32 ビットの記述子に依存する値、または整数値として返されます。|  
|**SQLConnect**|データ ソースに接続します。 Oracle オペレーティング システムの認証を使用する指定として「/」、 *szUID*パラメーターと""として、 *szAuthStr*パラメーター。|  
|**SQLDescribeCol**|名前、型、有効桁数、スケール、および指定された結果の列の null 値を返します。 **注:SQLDescribeCol** SQL_VARCHAR として計算列をレポートします。|  
|**SQLDisconnect**|接続を閉じます。 共有環境の接続プールが有効になっているし、アプリケーションを呼び出すかどうか**SQLDisconnect**その環境で、接続で、接続が接続プールに返されを使用して他のコンポーネントを引き続き使用できます同じ共有環境です。|  
|**SQLError**|最後のエラーについてのエラーまたは状態情報を返します。 このドライバーは、スタックまたはに対して返されるエラーの一覧、 *hstmt*、 *hdbc*、および*henv*方法に応じて、引数への呼び出し**SQLError**されます。 エラー キューは、各ステートメントの後にフラッシュされます。 通常、Oracle のエラー メッセージを取得し、空ではそれ以外の場合。|  
|**SQLExecDirect**|新しい、準備されていない SQL ステートメントを実行します。 ドライバーでは、ステートメントにパラメーターが存在しない場合、パラメーター マーカーの変数の現在の値が使用されます。 テーブル、ビュー、またはフィールド名にスペースが含まれる場合の名前で囲みます引用符の背面にマークします。 たとえば、データベースには、という名前のテーブルが含まれている場合*My Table*とフィールド*My Field*、次のように、識別子の各要素を囲みます。<br /><br /> SELECT \`My Table\`. \`My Field1\`,; \`My Table\`.\`My Field2\` FROM \`My Table\`|  
|**SQLExecute**|準備された SQL ステートメントを実行します (既にによって準備ステートメント**SQLPrepare**)。 ドライバーでは、ステートメントにパラメーターが存在しない場合、パラメーター マーカーの変数の現在の値が使用されます。|  
|**SQLFetch**|前の呼び出しで指定された場所に結果セットから 1 つの行を取得します。 **SQLBindCol**します。 呼び出すのため、ドライバーを準備します**SQLGetData**バインドされていない列にします。|  
|**SQLFreeConnect**|接続ハンドルを解放し、ハンドルに割り当てられたすべてのメモリを解放します。|  
|**SQLFreeEnv**|ODBC Driver for Oracle を終了し、ドライバーに関連付けられているすべてのメモリを解放します。|  
|**SQLFreeStmt**|特定 hstmt に関連付けられている処理を停止、hstmt に関連付けられている開いているカーソルを閉じ、保留中の結果を破棄および必要に応じて、ステートメント ハンドルに関連付けられているすべてのリソースを解放します。|  
|**SQLGetCursorName**|指定された hstmt に関連付けられているカーソルの名前を返します。|  
|**SQLNumResultCols**|結果セットのカーソルでは、列の数を返します。|  
|**SQLPrepare**|最適化し、ステートメントを実行する方法を計画することにより、SQL ステートメントを準備します。 実行するため、SQL ステートメントがコンパイルされる**SQLExecDirect**します。<br /><br /> テーブル、ビュー、またはフィールド名にスペースが含まれる場合の名前で囲みます引用符の背面にマークします。 たとえば、データベースには、という名前のテーブルが含まれている場合*My Table*とフィールド*My Field*、次のように、識別子の各要素を囲みます。<br /><br /> SELECT \`My Table\`.\`My Field\` FROM \`My Table\`<br /><br /> 仮パラメーターとして配列を含む結果セットの使用方法の詳細については、次を参照してください。[ストアド プロシージャから配列パラメーターを返す](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)します。|  
|**SQLRowCount**|Oracle では、結果セットの最後の行をフェッチした後、返します-1 までの行の数を決定する方法は提供されません。|  
|**SQLSetCursorName**|カーソル名をアクティブなステートメント ハンドルに関連付けます*hstmt*します。|  
|**SQLSetParam**|Odbc 2 SQLBindParameter で置き換えられます。*x*します。|  
|**SQLTransact**|コミットまたはロールバック操作のすべてのステートメント ハンドル (hstmts)、接続に関連付けられているすべてのアクティブな操作や、環境ハンドルに関連付けられているすべての接続を要求*henv*します。 トランザクションはアクティブなまま手動モードの場合、コミットに失敗した場合トランザクションをロールバックまたはコミット操作を再試行することができます。 自動トランザクション モードのときに、コミット操作が失敗した場合、トランザクションは自動的にロールバックします。トランザクションを非アクティブにすることはできません。|
