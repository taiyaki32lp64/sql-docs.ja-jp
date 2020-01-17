---
title: SQLNativeSql 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLNativeSql
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLNativeSql
helpviewer_keywords:
- SQLNativeSql function [ODBC]
ms.assetid: b8efc247-27ab-4a00-92b6-1400785783fe
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 719b34eef3eb51af1e5eeabce3a88d453f005eff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138822"
---
# <a name="sqlnativesql-function"></a>SQLNativeSql 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ODBC  
  
 **まとめ**  
 **SQLNativeSql**ドライバーによって変更された SQL 文字列を返します。 **SQLNativeSql** SQL ステートメントは実行されません。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLNativeSql(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      InStatementText,  
     SQLINTEGER     TextLength1,  
     SQLCHAR *      OutStatementText,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   TextLength2Ptr);  
```  
  
## <a name="arguments"></a>引数  
 *ConnectionHandle*  
 [入力] 接続ハンドル。  
  
 *InStatementText*  
 [入力]SQL 翻訳されるテキストを指定する文字列。  
  
 *TextLength1*  
 [入力]文字の長さ **InStatementText*テキスト文字列。  
  
 *OutStatementText*  
 [出力]SQL の翻訳された文字列を返すバッファーへのポインター。  
  
 場合*OutStatementText*が null の場合、 *TextLength2Ptr*は文字 (文字データの null 終端文字を除く) の合計数を返しますが、バッファーに返される使用可能な指す*OutStatementText*します。  
  
 *BufferLength*  
 [入力]内の文字数、 \* *OutStatementText*バッファー。 値が返される場合 *\*InStatementText*は Unicode 文字列です (呼び出し時に**SQLNativeSqlW**)、 *BufferLength*引数は偶数である必要があります。  
  
 *TextLength2Ptr*  
 [出力]返される使用可能な文字 (除外 null 終了) の合計数を返すバッファーへのポインター \* *OutStatementText*します。 返すに使用できる文字数がより大きいかに等しい場合*BufferLength*での SQL 文字列を翻訳\* *OutStatementText*に切り捨てられます*BufferLength* null 終了文字の長さマイナスです。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLNativeSql** SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返します呼び出すことによって、関連付けられた SQLSTATE 値を取得できる**SQLGetDiagRec**で、 *HandleType*sql_handle_dbc としての*処理*の*ConnectionHandle*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLNativeSql** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データで、右側が切り捨てられました|バッファー \* *OutStatementText*容量が不足する SQL 文字列全体を返すため、SQL 文字列が切り捨てられました。 切り詰められていない SQL 文字列の長さが返される **TextLength2Ptr*します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|08003|接続は開いていません|*ConnectionHandle*接続状態ではありませんでした。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとドライバーが接続されているデータ ソース間の通信リンクに失敗しました。|  
|22007|無効な datetime 形式|**InStatementText* escape 句に無効な日付、時刻、またはタイムスタンプ値が含まれています。|  
|24000|カーソル状態が無効|または、結果セットの終了後に結果セットの開始前に、ステートメントで参照されるカーソルが配置されました。 このエラーをネイティブ DBMS カーソルの実装を持つドライバーによって返されないことができます。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY009|無効な null ポインターの使用|(DM) **InStatementText*が null ポインター。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数が呼び出された、 *ConnectionHandle*この関数が呼び出されたときに実行されているとします。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|(DM) 引数*TextLength1* SQL_NTS に等しくないが、0 より小さいをでした。|  
|||(DM) 引数*BufferLength*が 0 との引数よりも小さい*OutStatementText*が null ポインターではありません。|  
|HY109|無効なカーソルの位置|カーソルの現在の行に削除されたかがまだフェッチされていません。 このエラーをネイティブ DBMS カーソルの実装を持つドライバーによって返されないことができます。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) に、ドライバーが関連付けられている、 *ConnectionHandle*関数をサポートしていません。|  
  
## <a name="comments"></a>コメント  
 どのような例を次に**SQLNativeSql** CONVERT スカラー関数を含む次の入力 SQL 文字列を返す可能性があります。 データ ソースの整数型の列 empid があると仮定します。  
  
```sql  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Microsoft SQL Server 用のドライバーでは、次の変換された SQL 文字列を返す可能性があります。  
  
```sql  
SELECT convert (smallint, empid) FROM employee  
```  
  
 ORACLE サーバー用のドライバーでは、次の変換された SQL 文字列を返す可能性があります。  
  
```sql  
SELECT to_number (empid) FROM employee  
```  
  
 Ingres 用のドライバーでは、次の変換された SQL 文字列を返す可能性があります。  
  
```sql  
SELECT int2 (empid) FROM employee  
```  
  
 詳細については、次を参照してください。[を直接実行](../../../odbc/reference/develop-app/direct-execution-odbc.md)と[準備された実行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)します。  
  
## <a name="related-functions"></a>関連する関数  
 [なし] :  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
