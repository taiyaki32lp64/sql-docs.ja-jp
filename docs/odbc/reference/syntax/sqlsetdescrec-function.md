---
title: SQLSetDescRec 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetDescRec
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescRec
helpviewer_keywords:
- SQLSetDescRec function [ODBC]
ms.assetid: bf55256c-7eb7-4e3f-97ef-b0fee09ba829
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b9940d55ca10292d6c90a241f47479a2178eff3
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343059"
---
# <a name="sqlsetdescrec-function"></a>SQLSetDescRec 関数
**互換性**  
 導入されたバージョン:ODBC 3.0 標準準拠:ISO 92  
  
 **概要**  
 **SQLSetDescRec**関数は、列またはパラメーターデータにバインドされたデータ型とバッファーに影響を与える複数の記述子フィールドを設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLSetDescRec(  
      SQLHDESC      DescriptorHandle,  
      SQLSMALLINT   RecNumber,  
      SQLSMALLINT   Type,  
      SQLSMALLINT   SubType,  
      SQLLEN        Length,  
      SQLSMALLINT   Precision,  
      SQLSMALLINT   Scale,  
      SQLPOINTER    DataPtr,  
      SQLLEN *      StringLengthPtr,  
      SQLLEN *      IndicatorPtr);  
```  
  
## <a name="arguments"></a>引数  
 *記述子ハンドル*  
 代入記述子ハンドル。 IRD ハンドルを指定することはできません。  
  
 *RecNumber*  
 代入設定するフィールドを含む記述子レコードを示します。 記述子レコードは0から番号が付けられ、レコード番号0はブックマークレコードになります。 この引数は、0以上である必要があります。 *Recnumber*が SQL_DESC_COUNT の値よりも大きい場合、SQL_DESC_COUNTis は*recnumber*の値に変更されました。  
  
 *型*  
 代入記述子レコードの SQL_DESC_TYPE フィールドを設定する値。  
  
 *SubType*  
 代入種類が SQL_DATETIME または SQL_INTERVAL のレコードの場合、これが SQL_DESC_DATETIME_INTERVAL_CODE フィールドを設定する値になります。  
  
 *Length*  
 代入記述子レコードの SQL_DESC_OCTET_LENGTH フィールドを設定する値。  
  
 *Precision*  
 代入記述子レコードの SQL_DESC_PRECISION フィールドを設定する値。  
  
 *Scale*  
 代入記述子レコードの SQL_DESC_SCALE フィールドを設定する値。  
  
 *DataPtr*  
 [遅延入力または出力]記述子レコードの SQL_DESC_DATA_PTR フィールドを設定する値。 *DataPtr*は null ポインターに設定できます。  
  
 *DataPtr*引数を null ポインターに設定すると、SQL_DESC_DATA_PTR フィールドを null ポインターに設定できます。 *記述子ハンドル*引数のハンドルがに関連付けられている場合、その列はバインド解除されます。  
  
 *StringLengthPtr*  
 [遅延入力または出力]記述子レコードの SQL_DESC_OCTET_LENGTH_PTR フィールドを設定する値。 *Stringlength PTR*を null ポインターに設定すると、SQL_DESC_OCTET_LENGTH_PTR フィールドを null ポインターに設定できます。  
  
 *IndicatorPtr*  
 [遅延入力または出力]記述子レコードの SQL_DESC_INDICATOR_PTR フィールドを設定する値。 *IndicatorPtr*を null ポインターに設定すると、SQL_DESC_INDICATOR_PTR フィールドを null ポインターに設定できます。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLSetDescRec**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連付けられた SQLSTATE 値を取得するには、 *Handletype* SQL_HANDLE_DESC と*記述子ハンドル*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出します。 次の表に、 **SQLSetDescRec**によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|07009|無効な記述子のインデックス|*Recnumber*引数は0に設定され、*記述子ハンドル*は IPD ハンドルを参照しています。<br /><br /> *Recnumber*引数が0未満でした。<br /><br /> *Recnumber*引数が、データソースがサポートできる列またはパラメーターの最大数を超えています。また、*記述子ハンドル*引数は APD、IPD、またはでした。<br /><br /> *Recnumber*引数が0で、*記述子ハンドル*引数が暗黙的に割り当てられた APD を参照しています。 (明示的に割り当てられたアプリケーション記述子が APD であるか、または実行時までに適用されるかが不明であるため、明示的に割り当てられたアプリケーション記述子では、このエラーは発生しません)。|  
|08S01|通信リンクの失敗|関数が処理を完了する前に、ドライバーと、ドライバーが接続されていたデータソースとの間の通信リンクが失敗しました。|  
|HY000|一般エラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 Messagetext バッファーの**SQLGetDiagRec によっ**て返されるエラーメッセージには、エラーとその原因が記述されています。  *\**|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンスエラー|(DM)*記述子ハンドル*は*StatementHandle*に関連付けられていました。このハンドルは非同期に実行される関数 (この関数ではありません) が呼び出され、この関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、 **sqlbulkoperations**、または**SQLSetPos**が、*記述子ハンドル*が関連付けられて SQL_NEED_DATA を返した*StatementHandle*に対して呼び出されました。 この関数は、実行時データのすべてのパラメーターまたは列に対してデータが送信される前に呼び出されました。<br /><br /> (DM) 実行中の非同期関数が、*記述子ハンドル*に関連付けられている接続ハンドルに対して呼び出されました。 この aynchronous 関数は、 **SQLSetDescRec**関数が呼び出されたときにまだ実行されていました。<br /><br /> (DM) **Sqlexecute**、 **SQLExecDirect**、または**Sqlmoreresults**が、*記述子ハンドル*に関連付けられたステートメントハンドルの1つに対して呼び出され、SQL_PARAM_DATA_AVAILABLE が返されました。 この関数は、ストリーミングされたすべてのパラメーターのデータが取得される前に呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY016|実装行記述子を変更できません|*記述子ハンドル*引数は IRD に関連付けられました。|  
|HY021|不整合な記述子情報|*型*フィールド、または記述子の SQL_DESC_TYPE フィールドに関連付けられているその他のフィールドが無効であるか、整合性がありませんでした。<br /><br /> 整合性チェック中にチェックされた記述子情報が一致しませんでした。 (このセクションで後述する「整合性チェック」を参照してください)。|  
|HY090|文字列またはバッファーの長さが無効です|(DM) ドライバー*は ODBC 2.x*ドライバーでしたが、記述子は、その*columnnumber*引数が0に設定されており、引数*bufferlength*に指定された値が4ではありませんでした。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM)*記述子ハンドル*に関連付けられているドライバーでは、関数はサポートされていません。|  
  
## <a name="comments"></a>コメント  
 アプリケーションで**SQLSetDescRec**を呼び出して、1つの列またはパラメーターに次のフィールドを設定できます。  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (型が SQL_DATETIME または SQL_INTERVAL であるレコードの場合)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  **SQLSetDescRec**の呼び出しが失敗した場合、 *recnumber*引数によって識別される記述子レコードの内容は未定義になります。  
  
 列またはパラメーターをバインドする場合、 **SQLSetDescRec**では、 **SQLBindCol**または**SQLBindParameter**を呼び出したり、 **SQLSetDescField**に対して複数の呼び出しを行ったりすることなく、バインドに影響を与える複数のフィールドを変更できます。 **SQLSetDescRec**は、現在ステートメントに関連付けられていない記述子にフィールドを設定できます。 **SQLBindParameter**は**SQLSetDescRec**より多くのフィールドを設定し、1回の呼び出しで APD と IPD の両方にフィールドを設定できます。また、記述子ハンドルは必要ありません。  
  
> [!NOTE]  
>  Statement 属性 SQL_ATTR_USE_BOOKMARKS は常に、 *Recnumber*引数を0に設定**してブックマーク**フィールドを設定する前に設定する必要があります。 必須ではありませんが、強くお勧めします。  
  
## <a name="consistency-checks"></a>整合性チェック  
 アプリケーションが APD、IPD、またはの SQL_DESC_DATA_PTR フィールドを設定するたびに、ドライバーによって整合性チェックが自動的に実行されます。 いずれかのフィールドが他のフィールドと矛盾している場合、 **SQLSetDescRec**は SQLSTATE HY021 (矛盾した記述子情報) を返します。  
  
 アプリケーションが APD、SQL_DESC_DATA_PTR、または IPD の [] フィールドを設定するたびに、ドライバーは SQL_DESC_TYPE フィールドの値とその SQL_DESC_TYPE フィールドに適用できる値が有効で一貫性があることを確認します。 このチェックは、SQLBindParameter または**SQLBindCol**が呼び出されたとき、または APD、  、または IPD に対して**SQLSetDescRec**が呼び出されたときに常に実行されます。 この整合性チェックには、記述子フィールドに対する次のチェックが含まれています。  
  
-   SQL_DESC_TYPE フィールドは、有効な ODBC C または SQL 型、またはドライバー固有の SQL 型のいずれかである必要があります。 SQL_DESC_CONCISE_TYPE フィールドは、有効な ODBC C または SQL の型、またはドライバー固有の C または SQL の型のいずれかである必要があります。これには、簡潔な datetime 型と interval 型が含まれます。  
  
-   SQL_DESC_TYPE レコードフィールドが SQL_DATETIME または SQL_INTERVAL の場合、SQL_DESC_DATETIME_INTERVAL_CODE フィールドは有効な DATETIME または INTERVAL コードのいずれかである必要があります。 ( [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)の SQL_DESC_DATETIME_INTERVAL_CODE フィールドの説明を参照してください。)  
  
-   SQL_DESC_TYPE フィールドが数値型を示している場合は、SQL_DESC_PRECISION フィールドと SQL_DESC_SCALE フィールドが有効であることが検証されます。  
  
-   SQL_DESC_CONCISE_TYPE フィールドが time または timestamp データ型である場合、間隔の種類が秒のコンポーネントの場合、または期間のデータ型のいずれかの場合、SQL_DESC_PRECISION フィールドは有効な秒の有効桁数であることが検証されます。  
  
-   SQL_DESC_CONCISE_TYPE が interval データ型の場合、SQL_DESC_DATETIME_INTERVAL_PRECISION フィールドは有効な間隔の有効桁数の値であることが確認されます。  
  
 IPD の SQL_DESC_DATA_PTR フィールドは通常は設定されません。ただし、アプリケーションでは、IPD フィールドの整合性チェックを強制的に行うことができます。 IRD に対して整合性チェックを実行することはできません。 IPD の SQL_DESC_DATA_PTR フィールドがに設定されている値は、実際に格納されていないため、 **SQLGetDescField**または**Sqlgetdescrec**の呼び出しで取得することはできません。この設定は、整合性チェックを強制するためにのみ行われます。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|列のバインド|[SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|パラメーターのバインド|[SQLBindParameter 関数](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|単一の記述子フィールドを取得する|[SQLGetDescField 関数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|複数の記述子フィールドの取得|[SQLGetDescRec 関数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|1つの記述子フィールドの設定|[SQLSetDescField 関数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
