---
title: SQLMoreResults 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLMoreResults
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLMoreResults
helpviewer_keywords:
- SQLMoreResults function [ODBC]
ms.assetid: bf169ed5-4d55-412c-b184-12065a726e89
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3ca7ed4f6bbcd31b8f67b95dc14a2c6c301b5a59
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138827"
---
# <a name="sqlmoreresults-function"></a>SQLMoreResults 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ODBC  
  
 **まとめ**  
 **SQLMoreResults**以上結果が含まれているステートメントで使用できるかどうかを判断します**SELECT**、 **UPDATE**、**INSERT**、または**DELETE**ステートメントと、それらの結果の初期化が処理そうである場合。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引数  
 *StatementHandle*  
 [入力]ステートメント ハンドルです。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_NO_DATA、SQL_ERROR、SQL_INVALID_HANDLE、または SQL_PARAM_DATA_AVAILABLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLMoreResults** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType* SQL の_HANDLE_STMT と*処理*の*StatementHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLMoreResults** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01S02|オプションの値が変更されました。|バッチとして変更ステートメント属性の値が処理されていた。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|40001|シリアル化エラー|トランザクションが別のトランザクションでリソース デッドロックによりロールバックされました。|  
|40003|不明なステートメント入力候補|この関数の実行中に、関連付けられた接続が失敗し、トランザクションの状態を特定できません。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *StatementHandle*します。 **SQLMoreResults**関数が呼び出された、前に、実行を完了**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*. 次に、 **SQLMoreResults**で関数が再度呼び出されました、 *StatementHandle*します。<br /><br /> **SQLMoreResults**関数が呼び出された、前に、実行を完了**SQLCancel**または**SQLCancelHandle**が呼び出されて、 *StatementHandle*マルチ スレッド アプリケーションで別のスレッドから。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された接続ハンドルに関連付けられているため、 *StatementHandle*します。 この非同期関数ではときに実行されている、 **SQLMoreResults**関数が呼び出されました。<br /><br /> (DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *StatementHandle*この関数が呼び出されたときに実行されているとします。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、または**SQLSetPos**に対して呼び出された、 *StatementHandle* SQL_NEED_DATA が返されます。 すべての実行時データ パラメーターまたは列のデータが送信される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *StatementHandle*関数をサポートしていません。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
  
## <a name="comments"></a>コメント  
 **SELECT**ステートメントの結果セットを返します。 **UPDATE**、**INSERT**、および**削除**ステートメントが影響を受ける行の数を返します。 これらのステートメントのいずれかがバッチ処理されて、プロシージャ、または (昇順にバッチ内で出現する順序で、パラメーターの順序番号付き) パラメーターの配列で送信された場合は、複数の結果セットを返すことまたは行をカウントします。 ステートメントのバッチおよびパラメーターの配列については、次を参照してください。 [SQL ステートメントのバッチ](../../../odbc/reference/develop-app/batches-of-sql-statements.md)と[パラメーター値の配列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)します。  
  
 バッチを実行した後、アプリケーションは最初の結果セットに配置されます。 アプリケーションを呼び出して**SQLBindCol**、 **SQLBulkOperations**、 **SQLFetch**、 **SQLGetData**、 **SQLFetchScroll**、 **SQLSetPos**、および最初またはそれ以降の結果セットでは、1 つの結果セットだけがあった場合と同様に、すべてのメタデータ関数。 完了すると、最初の結果セットで、アプリケーションを呼び出す**SQLMoreResults**次の結果セットに移動します。 もう 1 つの結果セットまたは count が使用可能な場合**SQLMoreResults** SQL_SUCCESS を返し、結果セットまたは追加の処理の数を初期化します。 結果セットを生成するステートメント間にあるすべての行の数を生成するステートメントが表示されない場合は、キーを呼び出す場所を空けるステップを実行できる**SQLMoreResults**します。呼び出した後**SQLMoreResults**の**UPDATE**、**INSERT**、または**DELETE**ステートメントでは、アプリケーションはを呼び出すことができます**SQLRowCount**します。  
  
 現在の結果が取り出されていない行は、セットがあった場合**SQLMoreResults**その結果セットを破棄し、次の結果セットまたは使用可能なカウントを使用します。 すべての結果が処理された場合**SQLMoreResults** sql_no_data が返されます。 一部のドライバーでは、出力パラメーターと戻り値は使用できませんすべての結果セットと行の数が処理されるまでです。 このようなドライバーは、出力パラメーターと戻り値のときに使用可能になる**SQLMoreResults** sql_no_data が返されます。  
  
 バインドが確立されているセットには、前の結果には、有効なままです。 列の構造体がこの結果セットのさまざまな場合は、呼び出して**SQLFetch**または**SQLFetchScroll**エラーまたは切り捨てが発生する可能性があります。 これを防ぐためには、アプリケーションが呼び出す**SQLBindCol**を明示的に適切な再バインド (または記述子フィールドを設定してください)。 また、アプリケーションを呼び出すことができます**SQLFreeStmt**で、*オプション*SQL_UNBIND 列のすべてのバッファーをバインド解除するのです。  
  
 呼び出しによって、batch を介して、アプリケーションが移動したときに、カーソルの種類、カーソルの同時実行、キーセットのサイズまたは長さが最大値などのステートメント属性の値を変更することがあります**SQLMoreResults**します。 この場合、 **SQLMoreResults**から SQL_SUCCESS_WITH_INFO と SQLSTATE 01S02 が返されます (オプションの値が変更されました)。  
  
 呼び出す**SQLCloseCursor**、または**SQLFreeStmt**で、*オプション*SQL_CLOSE のすべての結果セットとの実行の結果として使用可能になった行カウントを破棄します。バッチです。 ステートメント ハンドルを割り当てられたまたは準備された状態のいずれかを返します。 呼び出す**SQLCancel**されときにバッチが実行されたカーソル位置で実行された、ステートメント ハンドルは、または非同期状態がすべてのセットを結果行をカウントに非同期的に実行中の関数をキャンセルするにはキャンセル呼び出しが成功した場合に破棄されるバッチによって生成されます。 次のステートメントは、準備済みまたは割り当て済みの状態に戻ります。  
  
 ステートメントまたはプロシージャのバッチが他の SQL ステートメントとを混在かどうか**SELECT**、**UPDATE**、**INSERT**、および**DELETE**ステートメント、これらの他のステートメントには影響しません**SQLMoreResults**します。  
  
 詳細については、次を参照してください。[複数結果](../../../odbc/reference/develop-app/multiple-results.md)します。  
  
 ステートメントのバッチにデータ ソースで行が削除されない場合は、検索結果をupdate、insert、または delete ステートメントで**SQLMoreResults** SQL_SUCCESS を返します。 異なる検索のUPDATEの場合、INSERT、または delete ステートメントで実行される**SQLExecDirect**、 **SQLExecute**、または**SQLParamData**をデータ ソースの行には影響しない場合は、SQL_NO_DATA を返します。 アプリケーションを呼び出す場合**SQLRowCount**呼び出しの後に行の数を取得する**SQLMoreResults** 、どの行が影響を受けません**SQLRowCount** SQL_NO_DATA が返されます。  
  
 結果の処理関数の有効なシーケンス処理に関する詳細については、[付録 b:。ODBC の状態遷移テーブル](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)を参照してください。  
  
 SQL_PARAM_DATA_AVAILABLE とストリーミングされる出力パラメーターの詳細については、 [SQLGetData を使用して出力パラメーターを取得する](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)を参照してください。  
  
## <a name="availability-of-row-counts"></a>行の数の可用性  
 バッチに複数の連続する行の数を生成するステートメントが含まれている場合は、これらの行カウントが 1 つの行の数にロール アップすることができます。 たとえば、このバッチの場合は、特定のデータ ソースが 5 つの個別の行の数を返すことのできるステートメントの 5 つは挿入します。 その他の特定のデータ ソースは、5 つの個別の行の数の合計を表す 1 つだけの行の数を返します。  
  
 バッチに結果セットを生成して行の数を生成するステートメントの組み合わせが含まれている場合、行数は可能性があります。 またはできない場合がありますすべての。 行の数の可用性に関して、ドライバーの動作が呼び出しを通じて SQL_BATCH_ROW_COUNT 情報の種類に列挙された**SQLGetInfo**します。 たとえば、バッチが含まれている、**SELECT**、その後に 2 つ**INSERT**s、もう**SELECT**。 次のケースが考えられます。  
  
-   2 つに対応する行のカウント**INSERT**ステートメントは使用できませんに。 最初の呼び出し**SQLMoreResults** 、2 つ目の結果セットに位置する**SELECT**ステートメント。  
  
-   2 つに対応する行のカウント**INSERT**ステートメントは個別に使用できます。 (呼び出し**SQLGetInfo** SQL_BRC_ROLLED_UP ビット SQL_BATCH_ROW_COUNT 情報の種類には返されません)。最初の呼び出し**SQLMoreResults**最初の行の数に位置する**INSERT**、2 番目の呼び出しの位置で 2 番目の行の数と**INSERT**します。 3 番目の呼び出し**SQLMoreResults** 、2 つ目の結果セットに位置する**SELECT**ステートメント。  
  
-   2 つに対応する行のカウント**INSERT**使用できる 1 つの 1 つの行の数にロール アップされます。 (呼び出し**SQLGetInfo** SQL_BATCH_ROW_COUNT 情報の種類のビット SQL_BRC_ROLLED_UP を返します)。最初の呼び出し**SQLMoreResults**ロールアップされた行の数と、2 番目の呼び出しに位置する**SQLMoreResults** 、2 つ目の結果セットに位置する**SELECT**.  
  
 特定のドライバーは、ストアド プロシージャではないおよび明示的なバッチに対してのみ使用可能な行数を作成します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|ステートメントの処理をキャンセル|[SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|データのブロックをフェッチしています。 または、結果をスクロールの設定|[SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|1 つの行または順方向専用の方向にデータのブロックをフェッチしています|[SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|列のデータの一部またはすべてをフェッチしています|[SQLGetData 関数](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData を使用した出力パラメーターの取得](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
