---
title: アプリ - ODBC の互換性のためのマッピング置換関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping replacement functions [ODBC]
- upgrading applications [ODBC], mapping replacement functions
- compatibility [ODBC], mapping replacement functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], mapping replacement functions
- application upgrades [ODBC], mapping replacement functions
- backward compatibility [ODBC], mapping replacement functions
ms.assetid: f5e6d9da-76ef-42cb-b3f5-f640857df732
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 45cec32e818eab1ec5586196eadef998b8f988ef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036392"
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>アプリケーションの旧バージョンとの互換性のためのマッピング置換関数
ODBC *3.x*作業を通じて、ODBC アプリケーション*3.x*ドライバー マネージャーは ODBC に対して動作*2.x*の新機能が使用されない限りドライバー。 両方の複製機能と動作の変更には、ただし、方法に影響する、ODBC *3.x*に ODBC アプリケーションが動作*2.x*ドライバー。 ODBC を使用する場合*2.x*ドライバー、ドライバー マネージャーは、マップの次の ODBC *3.x*関数で、1 つまたは複数の ODBC に置き換えられている*2.x*関数の場合に、対応する ODBC *2.x*関数。  
  
|ODBC *3.x*関数|ODBC *2.x*関数|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**SQLAllocEnv**、 **SQLAllocConnect**、または**SQLAllocStmt**|  
|**SQLBulkOperations**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLColAttributes**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**SQLExtendedFetch**|  
|**SQLFetchScroll**|**SQLExtendedFetch**|  
|**SQLFreeHandle**|**SQLFreeEnv**、 **SQLFreeConnect**、または**SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGetConnectOption**|  
|**SQLGetDiagRec**|**Sqlerror 関数**|  
|**SQLGetStmtAttr**|**SQLGetStmtOption**[1]|  
|**SQLSetConnectAttr**|**SQLSetConnectOption**|  
|**SQLSetStmtAttr**|**SQLSetStmtOption**[1]|  
  
 [要求されている属性によっては、1] その他のアクションが実行されますも可能性があります。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 ドライバー マネージャーをマップする**SQLAllocEnv**、 **SQLAllocConnect**、または**SQLAllocStmt**必要に応じて、します。 次の呼び出しに**SQLAllocHandle**:  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 ドライバー マネージャーでは、次を実行すると、(概念、エラー チェックなし) のマッピング。  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
 ドライバー マネージャーをマップする**SQLSetPos**します。 次の呼び出しに**SQLBulkOperations**:  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 次の一連の手順で決定されます。  
  
1.  ドライバー マネージャーを呼び出す場合は、演算の引数は、SQL_ADD、 **SQLSetPos**次のようにします。  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  演算の引数が SQL_ADD でない場合は、ドライバーは SQLSTATE HY092 を返します (無効な属性またはオプション識別子)。  
  
3.  アプリケーションが呼び出しの間で、し、SQL_ATTR_ROW_STATUS_PTR を変更しようとしたかどうかは**SQLFetch**または**SQLFetchScroll**と**SQLBulkOperations**、ドライバー マネージャーは、返す SQLSTATE HY011 (属性はここで設定することはできません)。  
  
4.  演算の引数が SQL_ADD の場合は、アプリケーションを呼び出す必要があります**SQLBindCol**を挿入するデータをバインドします。 呼び出すことができない**SQLSetDescField**または**SQLSetDescRec**を挿入するデータをバインドします。  
  
5.  演算の引数は、SQL_ADD いて、挿入される行の数が現在の行セット サイズと同じ**SQLSetStmtAttr** SQL_ATTR_ROW_ARRAY_SIZE のステートメント属性を行の数を設定して、呼び出す必要があります呼び出しの前に挿入された**SQLBulkOperations**します。 前の行セットのサイズに戻すには、アプリケーションがする前に、SQL_ATTR_ROW_ARRAY_SIZE ステートメント属性を設定する必要があります**SQLFetch**、 **SQLFetchScroll**、または**SQLSetPos**が呼び出されます。  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 ドライバー マネージャーをマップする**SQLColAttributes**します。 次の呼び出しに**SQLColAttribute**:  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 次の一連の手順で決定されます。  
  
1.  場合*FieldIdentifier*は、次の 1 つです。  
  
     SQL_DESC_PRECISION、SQL_DESC_SCALE、SQL_DESC_LENGTH、SQL_DESC_OCTET_LENGTH、SQL_DESC_UNNAMED、SQL_DESC_BASE_COLUMN_NAME、SQL_DESC_LITERAL_PREFIX、SQL_DESC_LITERAL_SUFFIX、または SQL_DESC_LOCAL_TYPE_NAME  
  
     ドライバー マネージャーは、SQLSTATE HY091 SQL_ERROR を返します (無効な記述子フィールド識別子)。 このセクションのそれ以降のルールは適用されません。  
  
2.  ドライバー マネージャー SQL_COLUMN_COUNT、SQL_COLUMN_NAME、またはマップ SQL_COLUMN_NULLABLE SQL_DESC_COUNT、SQL_DESC_NAME、または SQL_DESC_NULLABLE、それぞれします。 (ODBC *2.x*ドライバー必要がありますのみ SQL_COLUMN_COUNT、SQL_COLUMN_NAME と SQL_COLUMN_NULLABLE、いない SQL_DESC_COUNT、SQL_DESC_NAME、およびサポート SQL_DESC_NULLABLE)。SQLColAttribute への呼び出しにマップされます。  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  他のすべての*FieldIdentifier*とドライバーの値をを通じて渡される**SQLColAttribute**にマップされている**SQLColAttributes**前述のようにします。  
  
4.  場合*BufferLength*が 0 の場合、ドライバー マネージャーは、SQLSTATE HY090 の SQL_ERROR を返します。 より小さい (無効な文字列長またはバッファー長)。 このセクションのそれ以降のルールは適用されません。  
  
5.  場合*FieldIdentifier* SQL_DESC_CONCISE_TYPE は、戻り値の型は、簡潔な datetime データ型、戻り値は、日付、時刻、およびタイムスタンプのコードのドライバー マネージャー マップします。  
  
6.  ドライバー マネージャーは、表示するために必要なチェックを実行するかどうか SQLSTATE HY010 (関数のシーケンス エラー) のニーズが発生します。 ドライバー マネージャーが SQL_ERROR と SQLSTATE HY010 を返すため場合、(関数のシーケンス エラーです)。 このセクションのそれ以降のルールは適用されません。  
  
## <a name="sqlendtran"></a>SQLEndTran  
 ドライバー マネージャーをマップする**SQLTransact**します。 次の呼び出しに**SQLEndTran**:  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 ドライバー マネージャーでは、次を実行すると、(概念、エラー チェックなし) のマッピング。  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 ドライバー マネージャーをマップする**SQLExtendedFetch**で、 *FetchOrientation* SQL_FETCH_NEXT の引数。 次の呼び出しに**SQLFetch**:  
  
```  
SQLFetch (StatementHandle);  
```  
  
 ドライバー マネージャーの呼び出し元になります**SQLExtendedFetch**、次のようにします。  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 この呼び出しで、 *pcRow*引数が、アプリケーション設定への呼び出しを通じて SQL_ATTR_ROWS_FETCHED_PTR ステートメント属性を値に設定されている**SQLSetStmtAttr**します。  
  
> [!NOTE]  
>  アプリケーションを呼び出すと**SQLSetStmtAttr**状態配列を指すようにし、SQL_ATTR_ROW_STATUS_PTR を設定するドライバー マネージャーは、ポインターをキャッシュします。 *RowStatusArray* null ポインターは等しくならないことができます。  
  
 ドライバーがサポートされていない場合**SQLExtendedFetch**カーソル ライブラリが読み込まれるとは、ドライバー マネージャーは、カーソル ライブラリの**SQLExtendedFetch**にマップする**SQLFetch**に**SQLExtendedFetch**します。 ドライバーがサポートされていない場合**SQLExtendedFetch**およびカーソル ライブラリが読み込まれていない、ドライバー マネージャーへの呼び出しに渡します**SQLFetch**からドライバーにします。 アプリケーションを呼び出す場合**SQLSetStmtAttr**をし、SQL_ATTR_ROW_STATUS_PTR を設定するには、ドライバー マネージャーにより、配列を作成します。 アプリケーションを呼び出す場合**SQLSetStmtAttr** SQL_ATTR_ROWS_FETCHED_PTR を設定するには、ドライバー マネージャーでは、1 にこのフィールドを設定します。  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 ドライバー マネージャーをマップする**SQLExtendedFetch**します。 次の呼び出しに**SQLFetchScroll**:  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 次の一連の手順で決定されます。  
  
1.  アプリケーションを呼び出すと**SQLSetStmtAttr**状態配列を指すようにし、SQL_ATTR_ROW_STATUS_PTR (これは、IRD の SQL_DESC_ARRAY_STATUS_PTR フィールドを設定する) を設定するドライバー マネージャーはこのポインターをキャッシュします。 このポインターができるように*RowStatusArray*しない場合は、let *RowStatusArray* null ポインターになります。 場合、 *RowStatusArray*引数が null ポインターに設定されている、ドライバー マネージャー、行状態配列が生成されます。  
  
2.  場合*FetchOrientation*は SQL_FETCH_NEXT、SQL_FETCH_PRIOR、SQL_FETCH_ABSOLUTE、SQL_FETCH_RELATIVE、SQL_FETCH_FIRST、SQL_FETCH_LAST、SQL_FETCH_BOOKMARK のいずれか SQL_ERROR と SQLSTATE ドライバー マネージャーを返しますHY106 (フェッチの範囲外の型)。 このセクションのそれ以降のルールは適用されません。  
  
3.  ケース:  
  
-   場合*FetchOrientation* SQL_FETCH_BOOKMARK、等しくになります。  
  
    -   場合**SQLSetStmtAttr** SQL_ATTR_FETCH_BOOKMARK_PTR の値を設定し、使用するために以前に呼び出された*bmk ファイルを削除*SQL_DESC_FETCH_BOOKMARK_PTR ポインターの逆参照で取得した値を指定します。  
  
    -   それ以外の場合、SQLSTATE HY111 SQL_ERROR を返します (無効なブックマーク値)。 このセクションのそれ以降のルールは適用されません。  
  
     ドライバー マネージャーを呼び出す**SQLExtendedFetch**、次のようにします。  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   ドライバー マネージャーは、それ以外の場合、 **SQLExtendedFetch**、次のようにします。  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     これらの呼び出しで、 *pcRow*引数が、アプリケーション設定への呼び出しを通じて SQL_ATTR_ROWS_FETCHED_PTR ステートメント属性を値に設定されている**SQLSetStmtAttr**します。  
  
-   SQL_ATTR_ROW_ARRAY_SIZE は SQL_ROWSET_SIZE にマップされます。  
  
-   場合*rc*が SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、またはと等しい場合に*FetchOrientation* SQL_FETCH_BOOKMARK と*FetchOffset*等しくを 0 にし、ドライバーは、警告、SQLSTATE 01S10 にポストされます (しようとすると、ブックマークのオフセットによってフェッチ、オフセット値は無視されます)、および、SQL_SUCCESS_WITH_INFO が返されます。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 ドライバー マネージャーをマップする**SQLFreeEnv**、 **SQLFreeConnect**、または**SQLFreeStmt**に応じて。 次の呼び出しに**SQLFreeHandle**:  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 ドライバー マネージャーでは、次を実行すると、(概念、エラー チェックなし) のマッピング。  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 ドライバー マネージャーをマップする**SQLGetConnectOption**します。 次の呼び出しに**SQLGetConnectAttr**:  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 次の一連の手順で決定されます。  
  
1.  場合*属性*ドライバーの定義済みの接続やステートメント属性ではないと、ODBC で定義されている属性のない*2.x*、ドライバー マネージャーは、SQLSTATE HY092 SQL_ERROR を返します (無効な属性/オプションの識別子)。 このセクションではそれ以降のルールは適用されません。  
  
2.  場合*属性*は SQL_ATTR_AUTO_IPD または SQL_ATTR_METADATA_ID、ドライバー マネージャーが SQLSTATE HY092 SQL_ERROR を返します (無効な属性またはオプション識別子)。  
  
3.  ドライバー マネージャーがかどうかを必要なチェックを実行 SQLSTATE 08003 (接続は開いていません) または SQLSTATE HY010 (関数のシーケンス エラー) が発生する必要があります。 そうである場合、ドライバー マネージャーは SQL_ERROR を返し、該当するエラー メッセージを投稿します。 このセクションのそれ以降のルールは適用されません。  
  
4.  ドライバー マネージャー呼び出し**SQLGetConnectOption**次のようにします。  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     なお、 *BufferLength*と*StringLengthPtr*は無視されます。  
  
## <a name="sqlgetdata"></a>SQLGetData  
 ときに、ODBC *3.x* odbc 作業アプリケーション*2.x*ドライバー呼び出し**SQLGetData**で、 *ColumnNumber*引数が 0 で、ODBC *3.x*ドライバー マネージャーでは、これをマップへの呼び出しに**SQLGetStmtOption**で、*オプション*属性 SQL_GET_BOOKMARK に設定します。  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 ドライバー マネージャーをマップする**SQLGetStmtOption**します。 次の呼び出しに**SQLGetStmtAttr**:  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 次の一連の手順で決定されます。  
  
1.  場合*属性*ドライバーの定義済みの接続やステートメント属性ではないと、ODBC で定義されている属性のない*2.x*、ドライバー マネージャーは、SQLSTATE HY092 SQL_ERROR を返します (無効な属性/オプションの識別子)。 このセクションではそれ以降のルールは適用されません。  
  
2.  場合*属性*は、次の 1 つです。  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     ドライバー マネージャーは、SQLSTATE HY092 SQL_ERROR を返します (無効な属性またはオプション識別子)。 このセクションのそれ以降のルールは適用されません。  
  
3.  ドライバー マネージャーは、表示するために必要なチェックを実行するかどうか SQLSTATE HY010 (関数のシーケンス エラー) のニーズが発生します。 ドライバー マネージャーが SQL_ERROR と SQLSTATE HY010 を返すため場合、(関数のシーケンス エラーです)。 このセクションのそれ以降のルールは適用されません。  
  
4.  場合*属性*と等しい SQL_ATTR_ROWS_FETCHED_PTR、内部のドライバー マネージャーの変数へのポインターをドライバー マネージャー返す*cRow*が使用またはへの呼び出しで使用することが**SQLExtendedFetch**します。 このセクションのそれ以降のルールは適用されません。  
  
5.  場合*属性*と等しい SQL_DESC_FETCH_BOOKMARK_PTR には、ドライバー マネージャーはへの呼び出し中に、キャッシュした適切なへのポインターを返します。 **SQLSetStmtAttr**します。  
  
6.  場合*属性*と等しい、し、SQL_ATTR_ROW_STATUS_PTR をドライバー マネージャーの呼び出し中にキャッシュしたことを適切なポインターを返します**SQLSetStmtAttr**します。  
  
7.  ドライバー マネージャー呼び出し**SQLGetStmtOption**次のようにします。  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     場所*hstmt*、 *fOption*、および*pvParam*の値に設定されます*StatementHandle*、*属性*、および*ValuePtr*、それぞれします。 *BufferLength*と*StringLengthPtr*は無視されます。  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 ドライバー マネージャーをマップする**SQLSetConnectOption**します。 次の呼び出しに**SQLSetConnectAttr**:  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 次の一連の手順で決定されます。  
  
1.  場合*属性*ドライバーの定義済みの接続やステートメント属性ではないと、ODBC で定義されている属性のない*2.x*、ドライバー マネージャーは、SQLSTATE HY092 SQL_ERROR を返します (無効な属性/オプションの識別子)。 このセクションではそれ以降のルールは適用されません。  
  
2.  場合*属性*と等しい SQL_ATTR_AUTO_IPD、ドライバー マネージャーが SQLSTATE HY092 SQL_ERROR を返します (無効な属性またはオプション識別子)。  
  
3.  ドライバー マネージャーは、表示するために必要なチェックを実行するかどうかで SQLSTATE 08003 (接続は開いていません) または SQLSTATE HY010 が発生します。 (関数のシーケンス エラー) が必要です。 発生します。 これらのエラーのいずれかの場合は、ドライバー マネージャーは SQL_ERROR を返し、該当するエラー メッセージを投稿します。 このセクションのそれ以降のルールは適用されません。  
  
4.  ドライバー マネージャー呼び出し**SQLSetConnectOption**次のようにします。  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     場所*hdbc*、 *fOption*、および*vParam*の値に設定されます*ConnectionHandle*、*属性*、および*ValuePtr*、それぞれします。 *StringLengthPtr*は無視されます。  
  
> [!NOTE]  
>  接続レベルのステートメント属性を設定する機能は非推奨とされました。 ODBC でステートメント属性に、接続レベルで設定しないで*3.x*アプリケーション。  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 ドライバー マネージャーをマップする**SQLSetStmtOption**します。 次の呼び出しに**SQLSetStmtAttr**:  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 次の一連の手順で決定されます。  
  
1.  場合*属性*ドライバーの定義済みの接続やステートメント属性ではないと、ODBC で定義されている属性のない*2.x*、ドライバー マネージャーは、SQLSTATE HY092 SQL_ERROR を返します (無効な属性/オプションの識別子)。 このセクションではそれ以降のルールは適用されません。  
  
2.  場合*属性*は、次の 1 つです。  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     ドライバー マネージャーは、SQLSTATE HY092 SQL_ERROR を返します (無効な属性またはオプション識別子)。 このセクションのそれ以降のルールは適用されません。  
  
3.  ドライバー マネージャーは、表示するために必要なチェックが実行するかどうかが発生します。 SQLSTATE HY010 (関数のシーケンス エラー) が必要です。 ドライバー マネージャーが SQL_ERROR と SQLSTATE HY010 を返すため場合、(関数のシーケンス エラーです)。 このセクションのそれ以降のルールは適用されません。  
  
4.  場合*属性*このトピックの後半は、SQL_ATTR_PARAMSET_SIZE または SQL_ATTR_PARAMS_PROCESSED_PTR と等しく、「マッピングの処理、パラメーター配列」セクションを参照してください。 このセクションのそれ以降のルールは適用されません。  
  
5.  場合*属性*SQL_ATTR_ROWS_FETCHED_PTR、ポインターの値を後で使用できるドライバー マネージャーのキャッシュが**SQLFetchScroll**します。  
  
6.  場合*属性*はポインターの値を後で使用できるドライバー マネージャーのキャッシュ、し、SQL_ATTR_ROW_STATUS_PTR と等しく**SQLFetchScroll**または**SQLSetPos**します。 このセクションのそれ以降のルールは適用されません。  
  
7.  場合*属性*SQL_ATTR_FETCH_BOOKMARK_PTR、ドライバー マネージャーのキャッシュが*ValuePtr*への呼び出しの後で、キャッシュされた値を使用して**SQLFetchScroll**します。 このセクションのそれ以降のルールは適用されません。  
  
8.  ドライバー マネージャー呼び出し**SQLSetStmtOption**次のようにします。  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     場所*hstmt*、 *fOption*、および*vParam*の値に設定されます*StatementHandle*、*属性*、および*ValuePtr*、それぞれします。 *StringLength*引数は無視されます。  
  
     場合、ODBC *2.x*ドライバーは、文字の文字列、ドライバー固有のステートメントのオプション、ODBC をサポートしている*3.x*アプリケーションを呼び出す必要があります**SQLSetStmtOption**これらのオプションを設定します。  
  
## <a name="mappings-for-handling-parameter-arrays"></a>パラメーター配列を処理するためのマッピング  
 アプリケーションを呼び出すとします。  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 ドライバー マネージャーを呼び出します。  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 ドライバー マネージャーは、アプリケーションを呼び出すときにポインターをこの変数後で返します**SQLGetStmtAttr** SQL_ATTR_PARAMS_PROCESSED_PTR を取得します。 ドライバー マネージャーは、準備済みまたは割り当て済みの状態に、ステートメント ハンドルが返されるまで、この内部変数を変更できません。  
  
 ODBC *3.x*アプリケーションが呼び出すことができます**SQLGetStmtAttr** APD の SQL_DESC_ARRAY_SIZE フィールドを明示的に設定しない場合でも、SQL_ATTR_PARAMS_PROCESSED_PTR の値を取得します。 このような状況に発生する可能性、たとえば、アプリケーションが現在の「行」のパラメーターをチェックする汎用ルーチンと処理されている**SQLExecute** SQL_NEED_DATA を返します。 このルーチンが呼び出されるは、SQL_DESC_ARRAY_SIZE が 1 かどうかが 1 より大きいか。 アプリケーションが呼び出されているかどうかを示す、この内部変数を定義する必要がありますドライバー マネージャーは、このアカウントに**SQLSetStmtAttr** APD の SQL_DESC_ARRAY_SIZE フィールドを設定します。 ドライバー マネージャーがこの変数にはから戻る前に、値 1 が含まれているかどうかを確認する必要があります SQL_DESC_ARRAY_SIZE が設定されていない場合**SQLExecDirect**または**SQLExecute**します。  
  
## <a name="error-handling"></a>エラー処理  
 ODBC で*3.x*を呼び出すと、 **SQLFetch**または**SQLFetchScroll** IRD と特定の診断の SQL_DIAG_ROW_NUMBER フィールド SQL_DESC_ARRAY_STATUS_PTR を設定します。レコードには、このレコードに関連する行セットの行の数が含まれています。 これを使用して、アプリケーションは特定の行位置と、エラー メッセージを関連付けることができます。  
  
 ODBC *2.x*ドライバーはこの機能を提供することはできません。 ただし、SQLSTATE 01S01 とエラーの境界が提供されます (行内のエラー)。 ODBC *3.x*を使用しているアプリケーション**SQLFetch**または**SQLFetchScroll** ODBC に対してするときに*2.x*ドライバーを意識する必要がありますこの事実です。 このようなアプリケーションが呼び出すことができるなることにも注意してください**SQLGetDiagField**を実際にとにかく SQL_DIAG_ROW_NUMBER フィールドを取得します。 ODBC *3.x* odbc 作業アプリケーション*2.x*を呼び出すことがドライバー **SQLGetDiagField**でのみ、 *DiagIdentifier*SQL_DIAG_MESSAGE_TEXT、SQL_DIAG_NATIVE、SQL_DIAG_RETURNCODE、または SQL_DIAG_SQLSTATE の引数です。 ODBC *3.x*ドライバー マネージャーは ODBC を使用する場合に診断データ構造を維持*2.x*ドライバーが、ODBC *2.x*ドライバーはこれら 4 つのフィールドのみを返します。  
  
 ときに、ODBC *2.x* odbc アプリケーションが動作*2.x*ドライバーを操作できますが、ドライバー マネージャーによって返されますの複数のエラーが発生する場合は、さまざまなエラーによって返される ODBC *3.x*よりも、ODBC でのドライバー マネージャー *2.x*ドライバー マネージャー。  
  
## <a name="mappings-for-bookmark-operations"></a>ブックマークの操作のマッピング  
 ODBC *3.x*ドライバー マネージャーは、ODBC の場合は、次のマッピングを実行します。 *3.x* odbc 作業アプリケーション*2.x*ドライバーは、ブックマークの操作を実行します。  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 ときに、ODBC *3.x* odbc 作業アプリケーション*2.x*ドライバー呼び出し**SQLBindCol** 0 列にバインドする*fCType* SQL_C_ に等しいVARBOOKMARK、ODBC *3.x*ドライバー マネージャーがどうかをチェックするかどうか、 *BufferLength*引数を 4 より小さいか、4 よりも、そうである場合は、SQLSTATE HY090 を返します (無効な文字列またはバッファー長さ)。 場合、 *BufferLength*引数が 4 に等しい、ドライバー マネージャーは、 **SQLBindCol**を交換した後、ドライバーで*fCType* SQL_C_BOOKMARK とします。  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 ときに、ODBC *3.x* odbc 作業アプリケーション*2.x*ドライバー呼び出し**SQLColAttribute**で、 *ColumnNumber*引数が 0 に設定します。ドライバー マネージャーを返します、 *FieldIdentifier*値は、次の表に一覧表示します。  
  
|*FieldIdentifier*|値|  
|-----------------------|-----------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|  
|SQL_DESC_CATALOG_NAME|"" (空の文字列)|  
|SQL_DESC_CONCISE_TYPE|SQL_BINARY|  
|SQL_DESC_COUNT|によって返されるのと同じ値**SQLNumResultCols**|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|  
|SQL_DESC_DISPLAY_SIZE|8|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|  
|SQL_DESC_LABEL|"" (空の文字列)|  
|SQL_DESC_LENGTH|0|  
|SQL_DESC_LITERAL_PREFIX|"" (空の文字列)|  
|SQL_DESC_LITERAL_SUFFIX|"" (空の文字列)|  
|SQL_DESC_LOCAL_TYPE_NAME|"" (空の文字列)|  
|SQL_DESC_NAME|"" (空の文字列)|  
|SQL_DESC_NULLABLE|SQL_NO_NULLS|  
|SQL_DESC_OCTET_LENGTH|4|  
|SQL_DESC_PRECISION|4|  
|SQL_DESC_SCALE|0|  
|SQL_DESC_SCHEMA_NAME|"" (空の文字列)|  
|SQL_DESC_SEARCHABLE|SQL_PRED_NONE|  
|SQL_DESC_TABLE_NAME|"" (空の文字列)|  
|SQL_DESC_TYPE|SQL_BINARY|  
|SQL_DESC_TYPE_NAME|"" (空の文字列)|  
|SQL_DESC_UNNAMED|SQL_UNNAMED|  
|SQL_DESC_UNSIGNED|SQL_FALSE|  
|SQL_DESC_UPDATEABLE|SQL_ATTR_READ_ONLY|  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 ときに、ODBC *3.x* odbc 作業アプリケーション*2.x*ドライバー呼び出し**SQLDescribeCol**で、 *ColumnNumber*引数が 0 に設定します。ドライバー マネージャーは、次の表に記載した値を返します。  
  
|バッファー|値|  
|------------|-----------|  
|[ColumnName]|"" (空の文字列)|  
|\* NameLengthPtr|0|  
|\* DataTypePtr|SQL_BINARY|  
|\* ColumnSizePtr|4|  
|\* DecimalDigitsPtr|0|  
|\* NullablePtr|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 ときに、ODBC *3.x* odbc 作業アプリケーション*2.x*ドライバーは、次の呼び出しを**SQLGetData**ブックマークを取得します。  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 呼び出しにマップされて**SQLGetStmtOption**で、 *fOption*の次のように、SQL_GET_BOOKMARK:  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 場所*hstmt*と*pvParam*内の値に設定されて*StatementHandle*と*TargetValuePtr*、それぞれします。 指すバッファーにブックマークが返されます、 *pvParam* (*TargetValuePtr*) 引数。 バッファー内の値が指す、 *StrLen_or_IndPtr*への呼び出しで引数**SQLGetData** 4 に設定されます。  
  
 このマッピングを内のケースを考慮する必要があります**SQLFetch**を呼び出す前に呼び出された**SQLGetData**と ODBC *2.x*ドライバーがをサポートしていない**SQLExtendedFetch**します。 この場合、 **SQLFetch**を ODBC を通じて渡される*2.x*ドライバー、大文字と小文字のブックマークの取得はサポートされていません。  
  
 **SQLGetData** ODBC で複数回を呼び出すことができません*2.x*呼び出すので、パーツ内のブックマークを取得するドライバー **SQLGetData**で、 *BufferLength*引数が 4 未満の値に設定し、 *ColumnNumber*引数を 0 に設定するには、SQLSTATE HY090 が返されます (無効な文字列長またはバッファー長)。 **SQLGetData**ただし、同じブックマークを取得する複数回呼び出されます。  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 ときに、ODBC *3.x* odbc 作業アプリケーション*2.x*ドライバー呼び出し**SQLSetStmtAttr**を設定する、SQL_ATTR_USE_BOOKMARKS 属性を SQL_UB_VARIABLE ドライバーマネージャーは、基になる odbc SQL_UB_ON に属性を設定*2.x*ドライバー。
