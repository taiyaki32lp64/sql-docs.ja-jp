---
title: ステートメントの遷移 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transitioning states [ODBC], statement
- state transitions [ODBC], statement
- statement transitions [ODBC]
ms.assetid: 3d70e0e3-fe83-4b4d-beac-42c82495a05b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b0d46bad2e0b37c5e6751a4895cdf1899aee4b01
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070106"
---
# <a name="statement-transitions"></a>ステートメントの遷移
ODBC ステートメントでは、次の状態があります。  
  
|状態|説明|  
|-----------|-----------------|  
|S0|未割り当てのステートメント。 (接続の状態は、C4、C5、C6 にある必要があります。 詳細については、次を参照してください[接続の遷移](../../../odbc/reference/appendixes/connection-transitions.md)。)。|  
|S1|割り当てられたステートメント。|  
|S2|準備されたステートメント。 結果セットは作成されません。|  
|S3|準備されたステートメント。 (場合によっては空) の結果セットが作成されます。|  
|S4|実行ステートメントおよびが結果セットが作成されました。|  
|S5|ステートメントが実行されると (場合によっては空) の結果セットが作成されました。 カーソルを開き、結果セットの最初の行の前に配置されているです。|  
|S6|配置されているカーソル**SQLFetch**または**SQLFetchScroll**します。|  
|S7|配置されているカーソル**SQLExtendedFetch**します。|  
|S8|関数には、データが必要があります。 **SQLParamData**呼び出されていません。|  
|S9|関数には、データが必要があります。 **SQLPutData**呼び出されていません。|  
|S10|関数には、データが必要があります。 **SQLPutData**が呼び出されました。|  
|S11|まだ実行しています。 ステートメントは、非同期的に実行される関数に SQL_STILL_EXECUTING が返された後に、この状態に残されます。 ステートメントは、ステートメント ハンドルの実行が受け取るすべての関数の中にこの状態が一時的に。 S11 が以外の状態テーブルの状態テーブルに表示されていない状態の一時的な居住地**SQLCancel**します。 関数を呼び出すことによってキャンセルできるステートメントは S11 の状態が一時的に、 **SQLCancel**別のスレッドから。|  
|S12|非同期実行が取り消されました。 S12、メンバー SQL_STILL_EXECUTING 以外の値が返されるまでに、アプリケーションで取り消された関数を呼び出す必要があります。 SQL_ERROR と SQLSTATE HY008 関数が返す場合にのみ、関数が正常に取り消されました (操作が取り消されました)。 場合は、キャンセル操作に失敗しました、通常実行される関数は SQL_SUCCESS などその他の値を返します。|  
  
 カーソルの状態、S10 を通じて S8 を示す必要があるデータの状態として、非同期の遷移の状態の S11 と S12 S7 を通じて S5 を示す状態 S2 および S3 は準備済みの状態と呼ばれます。 グループ内の各状態用に異なる場合にのみに、遷移は個別に表示する各グループほとんどの場合、各遷移状態で各グループは、同じです。  
  
 次の表では、各 ODBC 関数がステートメントの状態に与える影響を示します。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1], [5], [6]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[2], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|S1[3]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[4], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
  
 [1] この行は、移行を示しています。 ときに*HandleType* sql_handle_env としてでした。  
  
 [2] この行は、移行を示しています。 ときに*HandleType* sql_handle_dbc としてでした。  
  
 [3] この行は、移行を示しています。 ときに*HandleType* sql_handle_stmt としてでした。  
  
 [4] この行は、移行を示しています。 ときに*HandleType* SQL_HANDLE_DESC でした。  
  
 [5] 呼び出し**SQLAllocHandle**で*OutputHandlePtr*に以前の内容の処理し、ODBC ドライバーの問題が発生する可能性がありますに関係なく、そのハンドルを上書きする有効なハンドルを指します。 呼び出す ODBC アプリケーション プログラミングを正しくないが**SQLAllocHandle**に対して定義されている同じアプリケーション変数と 2 回 *\*OutputHandlePtr*呼び出さず**SQLFreeHandle**に再割り当てする前に、ハンドルを解放します。 一貫性のない動作やエラーの ODBC ドライバーの方に ODBC を上書きするようにハンドルを生じる可能性があります。  
  
## <a name="sqlbindcol"></a>SQLBindCol  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbindparameter"></a>SQLBindParameter  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbrowseconnect-sqlconnect-and-sqldriverconnect"></a>SQLBrowseConnect、SQLConnect、および SQLDriverConnect  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|08002|08002|08002|08002|08002|08002|08002|  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|HY010|HY010|24000|次の表を参照してください。|HY010|NS [c] HY010 o|  
  
## <a name="sqlbulkoperations-cursor-states"></a>SQLBulkOperations (カーソルの状態)  
  
|S5<br /><br /> 開く|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|-- [s] S8 [d] S11 [x]|-- [s] S8 [d] S11 [x]|HY010|  
  
## <a name="sqlcancel"></a>SQLCancel  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|--|--|--|--|S1 S2 の [1] [nr] S3 [2] [r] と [2] S5 [3] と [5] S6 ([3] または [4]) と [6] S7 [4] と [7]|次の表を参照してください。|  
  
 [1] **SQLExecDirect** SQL_NEED_DATA が返されます。  
  
 [2] **SQLExecute** SQL_NEED_DATA が返されます。  
  
 [3] **SQLBulkOperations** SQL_NEED_DATA が返されます。  
  
 [4] **SQLSetPos** SQL_NEED_DATA が返されます。  
  
 [5] **SQLFetch**、 **SQLFetchScroll**、または**SQLExtendedFetch**呼び出されていない必要があります。  
  
 [6] **SQLFetch**または**SQLFetchScroll**が呼び出されました。  
  
 [7] **SQLExtendedFetch**が呼び出されました。  
  
## <a name="sqlcancel-asynchronous-states"></a>SQLCancel (非同期の状態)  
  
|S11<br /><br /> まだ実行中|S12<br /><br /> 非同期のキャンセル|  
|-----------------------------|-----------------------------|  
|S12 の NS [1] [2]|S12|  
  
 [1] で、ステートメントは、関数の実行中状態 S11 で一時的にしました。 **SQLCancel**が別のスレッドから呼び出されました。  
  
 [2] で、ステートメントは、非同期的に呼び出される関数に SQL_STILL_EXECUTING が返されるため、状態 S11 でした。  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|24000|24000|24000|S1 np 受信 S3 [p]|HY010|HY010|  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|HY010|次の表を参照してください。|24000|-[s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqlcolattribute-prepared-states"></a>SQLColAttribute (準備済みの状態)  
  
|S2<br /><br /> 結果がありません。|S3<br /><br /> [結果]|  
|-----------------------|--------------------|  
|--[1] 07005[2]|-[s] S11 x|  
  
 [1] *FieldIdentifier* SQL_DESC_COUNT でした。  
  
 [2] *FieldIdentifier* SQL_DESC_COUNT でした。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges、SQLColumns、SQLForeignKeys、SQLGetTypeInfo、SQLPrimaryKeys、SQLProcedureColumns、SQLProcedures、SQLSpecialColumns、SQLStatistics、SQLTablePrivileges、および SQLTables  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(組み込み)|S5 [s] S11 [x]|S1 [e] S5 [s] S11 [x]|S1 [e] [1] S5 [s] と [1] S11 [x] [1] と 24000 [2]|次の表を参照してください。|HY010|NS [c] HY010 o|  
  
 [1] で、現在の結果は、last、または結果だけ、または現在の結果はありません。 複数の結果の詳細については、次を参照してください。[複数結果](../../../odbc/reference/develop-app/multiple-results.md)します。  
  
 [2] の現在の結果は、最後の結果ではありません。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables-cursor-states"></a>SQLColumnPrivileges、SQLColumns、SQLForeignKeys、SQLGetTypeInfo、SQLPrimaryKeys、SQLProcedureColumns、SQLProcedures、SQLSpecialColumns、SQLStatistics、SQLTablePrivileges、および SQLTables (カーソルの状態)  
  
|S5<br /><br /> 開く|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000[1]|24000|  
  
 [1] このエラーが返されますドライバー マネージャーによって**SQLFetch**または**SQLFetchScroll** SQL_NO_DATA が返されなかったと場合、ドライバーによって返される**SQLFetch**または**SQLFetchScroll** SQL_NO_DATA が返されます。  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込みの [1]|--|--|--|--|HY010|NS [c] と [3] HY010 [o] または [4]|  
|組み込み [2]|HY010|次の表を参照してください。|24000|-[s] S11 x|HY010|NS [c] と [3] HY010 [o] または [4]|  
  
 [1] この行は、移行を示しています。 ときに、 *SourceDescHandle*引数が ARD、APD、または IPD します。  
  
 [2] この行は、移行を示しています。 ときに、 *SourceDescHandle*引数は、IRD します。  
  
 [3]、 *SourceDescHandle*と*TargetDescHandle*引数がの場合と同じ、 **SQLCopyDesc**が非同期的に実行されている関数。  
  
 [4] か、 *SourceDescHandle*引数または*TargetDescHandle*引数 (または両方) が異なっています、 **SQLCopyDesc**が実行されている関数非同期的にします。  
  
## <a name="sqlcopydesc-prepared-states"></a>SQLCopyDesc (準備済みの状態)  
  
|S2<br /><br /> 結果がありません。|S3<br /><br /> [結果]|  
|-----------------------|--------------------|  
|24000[1]|-[s] S11 [x]|  
  
 [1]この行は、移行を示しています。 ときに、 *SourceDescHandle*引数は、IRD します。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources と SQLDrivers  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqldescribecol"></a>SQLDescribeCol  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|HY010|次の表を参照してください。|24000|-[s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqldescribecol-prepared-states"></a>SQLDescribeCol (準備済みの状態)  
  
|S2<br /><br /> 結果がありません。|S3<br /><br /> [結果]|  
|-----------------------|--------------------|  
|07005|-[s] S11 [x]|  
  
## <a name="sqldescribeparam"></a>SQLDescribeParam  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|HY010|-[s] S11 [x]|HY010|HY010|HY010|NS [c] HY010 [o]|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|S0 [1]|S0 [1]|S0 [1]|S0 [1]|(HY010)|(HY010)|  
  
 [1] 呼び出し**SQLDisconnect**接続に関連付けられたすべてのステートメントを解放します。 接続状態が返されます。 C2 にさらに、接続状態は、ステートメントの状態は、S0 前に、C4 にすることがあります。  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|-[2] [3] S1 または [1]|-S1 [np] [3] と ([1] または [2]) S1 [p] と [1] S2 [p] と [2]|-S1 [np] [3] と ([1] または [2]) S1 [p] と [1] S3 [p] と [2]|(HY010)|(HY010)|  
  
 [1]、 *CompletionType*引数が指定して、 **SQLGetInfo** SQL_CB_DELETE SQL_CURSOR_COMMIT_BEHAVIOR 情報の種類を返しますまたは、 *CompletionType*引数が SQL_ROLLBACK と**SQLGetInfo** SQL_CB_DELETE SQL_CURSOR_ROLLBACK_BEHAVIOR 情報の種類を返します。  
  
 [2]、 *CompletionType*引数が指定して、 **SQLGetInfo** SQL_CB_CLOSE SQL_CURSOR_COMMIT_BEHAVIOR 情報の種類を返しますまたは、 *CompletionType*引数が SQL_ROLLBACK と**SQLGetInfo** SQL_CB_CLOSE SQL_CURSOR_ROLLBACK_BEHAVIOR 情報の種類を返します。  
  
 [3]、 *CompletionType*引数が指定して、 **SQLGetInfo** SQL_CB_PRESERVE SQL_CURSOR_COMMIT_BEHAVIOR 情報の種類を返しますまたは、 *CompletionType*引数が SQL_ROLLBACK と**SQLGetInfo** SQL_CB_PRESERVE SQL_CURSOR_ROLLBACK_BEHAVIOR 情報の種類を返します。  
  
## <a name="sqlexecdirect"></a>SQLExecDirect  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(組み込み)|S4 [s] と [nr] S5 [s]、[r] [d] S8 S11 [x]|-S1 [e] [1] と [2] S4 [s] および [nr] S5 の [e] と [s]、[r] [d] S8 S11 [x]|-[e]、[1] と [3] S1 [e] [2]、s4 [3] [s]、[nr] と [3] S5 [s]、[r] S8 [3] [d] と [3] S11 [x] と [3] 24000 [4]|次の表を参照してください。|HY010|NS [c] HY010 [o]|  
  
 [ドライバー マネージャーによっては、1]、エラーが返されました。  
  
 [2] のエラーには、ドライバー マネージャーによって返されませんでした。  
  
 [3] で、現在の結果は、last、または結果だけ、または現在の結果はありません。 複数の結果の詳細については、次を参照してください。[複数結果](../../../odbc/reference/develop-app/multiple-results.md)します。  
  
 [4] の現在の結果は、最後の結果ではありません。  
  
## <a name="sqlexecdirect-cursor-states"></a>SQLExecDirect (カーソルの状態)  
  
|S5<br /><br /> 開く|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [1] このエラーが返されますドライバー マネージャーによって**SQLFetch**または**SQLFetchScroll** 、SQL_NO_DATA が返されなかったと場合、ドライバーによって返される**SQLFetch**または**SQLFetchScroll** SQL_NO_DATA が返されます。  
  
## <a name="sqlexecute"></a>SQLExecute  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(組み込み)|(HY010)|次の表を参照してください。|S2 [e] p、および [1] S4 [s]、[p] [nr] と [1] S5 [s]、[p] [r] と [1] S8 [d] [p] と [1] S11 [x]、[p] [1] と 24000 [p] と [2] HY010 [np]|カーソルの状態テーブルを参照してください。|HY010|NS [c] HY010 [o]|  
  
 [1] で、現在の結果は、last、または結果だけ、または現在の結果はありません。 複数の結果の詳細については、次を参照してください。[複数結果](../../../odbc/reference/develop-app/multiple-results.md)します。  
  
 [2] の現在の結果は、最後の結果ではありません。  
  
## <a name="sqlexecute-prepared-states"></a>SQLExecute (準備済みの状態)  
  
|S2<br /><br /> 結果がありません。|S3<br /><br /> [結果]|  
|-----------------------|--------------------|  
|S4 [s] [d] S8 S11 [x]|S5 [s] [d] S8 S11 [x]|  
  
## <a name="sqlexecute-cursor-states"></a>SQLExecute (カーソルの状態)  
  
|S5<br /><br /> 開く|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000 [p] HY010 [np]|24000 [p]、[1] HY010 [np]|24000 [p] HY010 [np]|  
  
 [1] このエラーが返されますドライバー マネージャーによって**SQLFetch**または**SQLFetchScroll** 、SQL_NO_DATA が返されなかったと場合、ドライバーによって返される**SQLFetch**または**SQLFetchScroll** SQL_NO_DATA が返されます。  
  
## <a name="sqlextendedfetch"></a>SQLExtendedFetch  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|S1010|S1010|24000|次の表を参照してください。|S1010|NS [c] S1010 [o]|  
  
## <a name="sqlextendedfetch-cursor-states"></a>SQLExtendedFetch (カーソルの状態)  
  
|S5<br /><br /> 開く|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S7 [s] または [%nf] S11 [x]|S1010|-[s] または [%nf] S11 [x]|  
  
## <a name="sqlfetch-and-sqlfetchscroll"></a>SQLFetch と SQLFetchScroll  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|HY010|HY010|24000|次の表を参照してください。|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlfetch-and-sqlfetchscroll-cursor-states"></a>SQLFetch と SQLFetchScroll (カーソルの状態)  
  
|S5<br /><br /> 開く|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S6 [s] または [%nf] S11 [x]|-[s] または [%nf] S11 [x]|HY010|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|-- [1]|HY010|HY010|HY010|HY010|HY010|HY010|  
|組み込み [2]|S0|S0|S0|S0|HY010|HY010|  
|-- [3]|--|--|--|--|--|--|  
  
 [1] この行は、移行を示しています。 ときに*HandleType* sql_handle_env としてまたは sql_handle_dbc として。  
  
 [2] この行は、移行を示しています。 ときに*HandleType* sql_handle_stmt としてでした。  
  
 [3] この行は、移行を示しています。 ときに*HandleType* SQL_HANDLE_DESC、記述子が明示的に割り当てられます。  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込みの [1]|--|--|S1 np 受信 S2 [p]|S1 np 受信 S3 [p]|HY010|HY010|  
|組み込み [2]|--|--|--|--|HY010|HY010|  
  
 [1] この行は、移行を示しています。 ときに*オプション*SQL_CLOSE をでした。  
  
 [2] この行は、移行を示しています。 ときに*オプション*SQL_UNBIND または SQL_RESET_PARAMS でした。 場合、*オプション*引数が SQL_DROP と基になるドライバーは、ODBC 3 *.x*ドライバー、ドライバー マネージャーは、これにマップへの呼び出し**SQLFreeHandle**で*HandleType*を sql_handle_stmt として設定します。 詳細については、の遷移のテーブルを参照してください。 [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)します。  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetcursorname"></a>SQLGetCursorName  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|--|--|--|--|HY010|HY010|  
  
## <a name="sqlgetdata"></a>SQLGetData  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|HY010|HY010|24000|次の表を参照してください。|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlgetdata-cursor-states"></a>SQLGetData (カーソルの状態)  
  
|S5<br /><br /> 開く|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-[s] または [%nf] [x] [b] HY109 24000 S11 [i]|-[s] または [%nf] [x] [b] HY109 24000 S11 [i]|  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField および SQLGetDescRec  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|-[1] または HY010 [2] [3]|次の表を参照してください。|-[1] または 24000 [2] [3]|-[1] [2]、または S11 [3] [3] と [x]|HY010|NS [c] または [4] HY010 [o] と [5]|  
  
 [1]、 *DescriptorHandle*引数が APD または ARD します。  
  
 [2]、 *DescriptorHandle*引数は、IPD します。  
  
 [3]、 *DescriptorHandle*引数は、IRD します。  
  
 [4]、 *DescriptorHandle*引数が同じ、 *DescriptorHandle*引数、 **SQLGetDescField**または**SQLGetDescRec**非同期的に実行している関数。  
  
 [5]、 *DescriptorHandle*引数が異なる場合、 *DescriptorHandle*引数、 **SQLGetDescField**または**SQLGetDescRec**が非同期的に実行されている関数。  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec-prepared-states"></a>SQLGetDescField および SQLGetDescRec (準備済みの状態)  
  
|S2<br /><br /> 結果がありません。|S3<br /><br /> [結果]|  
|-----------------------|--------------------|  
|-[1] [2]、または S11 [2] [3] と [x]|-[1]、[2] または S11 [x] [3]|  
  
 [1]、 *DescriptorHandle*引数が APD または ARD します。  
  
 [2]、 *DescriptorHandle*引数は、IPD します。  
  
 [3]、 *DescriptorHandle*引数は、IRD します。 これらの関数は、状態 S2 SQL_NO_DATA を常に返すときに*DescriptorHandle* IRD のでした。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField と SQLGetDiagRec  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--|--|--|  
|組み込み [2]|--[3]|--[3]|--|--|--[3]|--[3]|  
  
 [1] この行は、移行を示しています。 ときに*HandleType* sql_handle_env として、sql_handle_dbc として、または SQL_HANDLE_DESC でした。  
  
 [2] この行は、移行を示しています。 ときに*HandleType* sql_handle_stmt としてでした。  
  
 [3] **SQLGetDiagField**常にこのエラーを返します状態*DiagIdentifier* SQL_DIAG_ROW_COUNT が。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|--[1] 24000[2]|--[1] 24000[2]|--[1] 24000[2]|次の表を参照してください。|HY010|HY010|  
  
 [1] で、ステートメント属性の SQL_ATTR_ROW_NUMBER でした。  
  
 [2] のステートメント属性は、SQL_ATTR_ROW_NUMBER でした。  
  
## <a name="sqlgetstmtattr-cursor-states"></a>SQLGetStmtAttr (カーソルの状態)  
  
|S5<br /><br /> 開く|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[1] 24000[2]|--または [1] ([v] と [2]) 24000 [b] と [2] HY109 [i] と [2]|--または [i] ([v] と [2]) 24000 [b] と [2] HY109 [1] と [2]|  
  
 [1]、*属性*引数 SQL_ATTR_ROW_NUMBER がありませんでした。  
  
 [2]、*属性*引数が SQL_ATTR_ROW_NUMBER します。  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(組み込み)|--[1]|--[1]|-[s] と [2] S1 [%nf] [np] と [4] S2 [%nf] [p] と [4] S5 [s] と [3] S11 [x]|S1 [%nf]、[np] と [4] S3 [%nf] [p] と [4] S4 [s] と [2] S5 [s] と [3] S11 [x]|HY010|NS [c] HY010 [o]|  
  
 [1]、関数は、この状態で SQL_NO_DATA を常に返します。  
  
 [2] で、次の結果は、行の数です。  
  
 [3] で、次の結果は、結果セットです。  
  
 [4] の現在の結果は、最後の結果です。  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlnumparams"></a>SQLNumParams  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|HY010|-[s] S11 [x]|-[s] S11 [x]|-[s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlnumresultcols"></a>SQLNumResultCols  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|HY010|-[s] S11 [x]|-[s] S11 [x]|-[s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata"></a>SQLParamData  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|HY010|HY010|HY010|HY010|次の表を参照してください。|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata-need-data-states"></a>SQLParamData (必要データの状態)  
  
|S8<br /><br /> データが必要|S9<br /><br /> 配置する必要があります。|S10<br /><br /> 配置することができます。|  
|----------------------|---------------------|---------------------|  
|S1 [e] と S2 [1] [e] [nr]、および S3 [2] [e] [r] と [2] S5 [e] と [4] S6 [e] と [5] S7 [e] と S9 [3] [d] S11 [x]|HY010|S1 [e] と S2 [1] [e] [nr] s3 [2] [e] [r] と [2] S4 [s]、[nr] と ([1] または [2]) S5 [s]、[r] と ([1] または [2]) S5 ([s] または [e]) と [4] S6 ([s] または [e]) と [5] S7 ([s] または [e]) と S9 [3] [d] S11 [x]|  
  
 [1] **SQLExecDirect** SQL_NEED_DATA が返されます。  
  
 [2] **SQLExecute** SQL_NEED_DATA が返されます。  
  
 [3] **SQLSetPos**状態 S7 から呼び出されるされ、SQL_NEED_DATA が返されます。  
  
 [4] **SQLBulkOperations**状態 S5 から呼び出されるされ、SQL_NEED_DATA が返されます。  
  
 [5] **SQLSetPos**または**SQLBulkOperations**状態 S6 から呼び出されるされ、SQL_NEED_DATA が返されます。  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(組み込み)|S2 [s] と [nr] S3 [s]、[r] S11 [x]|--または [s] ([e] と [1]) S1 [e] と S11 [x] [2]|S1 [e] と [3] S2 [s]、[nr] と [3] S3 [s]、[r] と [3] S11 [x] [3] と 24000 [4]|次の表を参照してください。|HY010|NS [c] HY010 [o]|  
  
 [1] で、準備は、ステートメントの検証以外の理由が失敗した (SQLSTATE が HY009 [無効な引数の値] HY090 または [無効な文字列長またはバッファー長])。  
  
 [2] の準備は、ステートメントの検証中に失敗した (SQLSTATE は HY009 でした。 [無効な引数の値] HY090 または [無効な文字列長またはバッファー長])。  
  
 [3] で、現在の結果は、last、または結果だけ、または現在の結果はありません。 複数の結果の詳細については、次を参照してください。[複数結果](../../../odbc/reference/develop-app/multiple-results.md)します。  
  
 [4] の現在の結果は、最後の結果ではありません。  
  
## <a name="sqlprepare-cursor-states"></a>SQLPrepare (カーソルの状態)  
  
|S5<br /><br /> 開く|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000|24000|  
  
## <a name="sqlputdata"></a>SQLPutData  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|HY010|HY010|HY010|HY010|次の表を参照してください。|NS [c] HY010 [o]|  
  
## <a name="sqlputdata-need-data-states"></a>SQLPutData (必要データの状態)  
  
|S8<br /><br /> データが必要|S9<br /><br /> 配置する必要があります。|S10<br /><br /> 配置することができます。|  
|----------------------|---------------------|---------------------|  
|HY010|S1 [e] と S2 [1] [e] [nr] s3 [2] [e] [r] と [2] S5 [e] と [4] S6 [e] と [5] S7 [e] と S10 [3] [s] S11 [x]|-S1 [s] [e] と S2 [1] [e] [nr] s3 [2] [e] [r] と [2] S5 [e] と [4] S6 [e] と [5] S7 [e] と S11 [x] [3] HY011 [6]|  
  
 [1] **SQLExecDirect** SQL_NEED_DATA が返されます。  
  
 [2] **SQLExecute** SQL_NEED_DATA が返されます。  
  
 [3] **SQLSetPos**状態 S7 から呼び出されるされ、SQL_NEED_DATA が返されます。  
  
 [4] **SQLBulkOperations**状態 S5 から呼び出されるされ、SQL_NEED_DATA が返されます。  
  
 [5] **SQLSetPos**または**SQLBulkOperations**状態 S6 から呼び出されるされ、SQL_NEED_DATA が返されます。  
  
 [6] 1 つまたは複数の呼び出し**SQLPutData** SQL_SUCCESS と後の呼び出しを 1 つのパラメーターが返される**SQLPutData**で同じパラメーター向けに作成された*StrLen_or_Ind*設定SQL_NULL_DATA します。  
  
## <a name="sqlrowcount"></a>SQLRowCount  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(組み込み)|(HY010)|(HY010)|--|--|(HY010)|(HY010)|  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--[2] 24000[3]|HY010|HY010|  
  
 [1] この行は、移行を示しています。 ときに*属性*接続属性されました。 場合に遷移*属性*ステートメントだった属性のステートメントの遷移のテーブルを参照してください**SQLSetStmtAttr**します。  
  
 [2]、*属性*引数 SQL_ATTR_CURRENT_CATALOG がありませんでした。  
  
 [3]、*属性*引数 SQL_ATTR_CURRENT_CATALOG のでした。  
  
## <a name="sqlsetcursorname"></a>SQLSetCursorName  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|--|--|24000|24000|HY010|HY010|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField および SQLSetDescRec  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込みの [1]|--|--|--|--|HY010|HY010|  
  
 [1] この行は、移行を示しています場所、 *DescriptorHandle*引数は、ARD、APD、IPD、または (の**SQLSetDescField**)、IRD ときに、 *FieldIdentifier*引数が sql _。DESC_ARRAY_STATUS_PTR または SQL_DESC_ROWS_PROCESSED_PTR します。 呼び出すとエラーが**SQLSetDescField** 、IRD のときに*FieldIdentifier*はその他の値。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|HY011|HY011|HY011|HY011|Y011|HY01|HY011|  
  
## <a name="sqlsetpos"></a>SQLSetPos  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|HY010|HY010|24000|次の表を参照してください。|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlsetpos-cursor-states"></a>SQLSetPos (カーソルの状態)  
  
|S5<br /><br /> 開く|S6<br /><br /> SQLFetch または SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-[s] S8 [d] [x] [b] HY109 24000 S11 [i]|-[s] S8 [d] [x] [b] HY109 24000 S11 [i]|  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
  
|S0<br /><br /> 未割り当て|S1<br /><br /> 割り当てられました。|S2、S3<br /><br /> Prepared|S4<br /><br /> 実行|S5 S7<br /><br /> カーソル|S8 S10<br /><br /> データが必要|S11 S12<br /><br /> 非同期|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|組み込み|--|--HY011 [1] [2]|--[1] 24000[2]|--[1] 24000[2]|HY010 [np] または [1] HY011 [p] と [2]|HY010 [np] または [1] HY011 [p] と [2]|  
  
 [1]、*属性*SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR、SQL_ATTR_USE_BOOKMARKS、SQL_ATTR_CURSOR_SCROLLABLE、または SQL_ATTR_CURSOR_SENSITIVITY 引数がありませんでした。  
  
 [2]、*属性*引数は、SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR、SQL_ATTR_USE_BOOKMARKS、SQL_ATTR_CURSOR_SCROLLABLE、または SQL_ATTR_CURSOR_SENSITIVITY がでした。
