---
title: SQLGetData を使用して出力パラメーターを取得する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], retrieving output parameters
- output parameters [ODBC]
- retrieving output parameters [ODBC]
ms.assetid: 7a8c298a-2160-491d-a300-d36f45568d9c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: eeb8fae9c563e675499dec47839acdd0a003765a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020513"
---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>SQLGetData を使用した出力パラメーターの取得
ODBC 3.8、前に、アプリケーションは、バインドされた出力バッファーを持つクエリの出力パラメーターを取得のみでした。 ただし、これはパラメーター値のサイズが (大きいイメージなど) の非常に大きい場合は、非常に大きなバッファーを割り当てることは困難です。 ODBC 3.8 には、部分の出力パラメーターを取得する新しい方法が導入されています。 アプリケーションで呼び出せるようになりました**SQLGetData**小さなバッファーを複数回に大きなパラメーター値を取得します。 これは、大きな列データの取得に似ています。  
  
 出力パラメーターまたはの部分で取得するには、入力/出力パラメーターをバインドするには、呼び出す**SQLBindParameter**で、 *InputOutputType*引数 SQL_PARAM_OUTPUT_STREAM または SQL_PARAM_INPUT_OUTPUT に設定_STREAM します。 SQL_PARAM_INPUT_OUTPUT_STREAM でアプリケーションを使用できます**SQLPutData**にデータをパラメーターを入力し、使用して**SQLGetData**出力パラメーターを取得します。 入力データは、実行時データ (DAE) である必要がありますを使用して、フォーム**SQLPutData**事前に割り当てられたバッファーへのバインドの代わりにします。  
  
 この機能は ODBC 3.8 アプリケーションで使用できるまたは ODBC を再コンパイル 3.x と ODBC 2.x アプリケーションでは、これらのアプリケーションに、ODBC 3.8 をサポートするドライバーを使用して出力パラメーターを取得する必要があります**SQLGetData**と ODBC 3.8 ドライバーマネージャー。 ODBC の新しい機能を使用する古いアプリケーションを有効にする方法については、次を参照してください。[の互換性対応表](../../../odbc/reference/develop-app/compatibility-matrix.md)します。  
  
## <a name="usage-example"></a>使用例  
 たとえば、ストアド プロシージャでは、実行する **{呼び出し sp_f(?,?)}** 、場所として SQL_PARAM_OUTPUT_STREAM、両方のパラメーターがバインドされているし、ストアド プロシージャが結果セットを返さない (このトピックの後半が見つかったらより複雑なシナリオ)。  
  
1.  パラメーターごとに、呼び出す**SQLBindParameter**で*InputOutputType* SQL_PARAM_OUTPUT_STREAM に設定し、 *ParameterValuePtr*パラメーター番号などのトークンに設定、、のデータへのポインターまたは入力パラメーターをバインドするアプリケーションが使用する構造体へのポインター。 この例では、パラメーターの序数をトークンとして使用します。  
  
2.  使用してクエリを実行**SQLExecDirect**または**SQLExecute**します。 取得するために使用可能なストリームの出力パラメーターがあることを示す、SQL_PARAM_DATA_AVAILABLE が返されます。  
  
3.  呼び出す**SQLParamData**の取得に使用されるパラメーターを取得します。 **SQLParamData**で設定された最初の使用可能なパラメーターのトークンを使用して SQL_PARAM_DATA_AVAILABLE を返す**SQLBindParameter** (ステップ 1)。 トークンがバッファーに返されますが、 *ValuePtrPtr*を指します。  
  
4.  呼び出す**SQLGetData**引数で*Col*_or\_*Param_Num*最初の使用可能なパラメーターのデータを取得する序数パラメーターに設定します。 場合**SQLGetData**から SQL_SUCCESS_WITH_INFO と SQLState 01004 (データは切り捨てられます)、戻り値と型が可変長クライアントとサーバーの両方で、使用可能な最初のパラメーターから取得する複数のデータがあります。 呼び出しを継続できます**SQLGetData**を変える SQL_SUCCESS または SQL_SUCCESS_WITH_INFO が返されるまで**SQLState**します。  
  
5.  手順 3 と 4 は現在のパラメーターを取得する手順を繰り返します。  
  
6.  呼び出す**SQLParamData**もう一度です。 SQL_PARAM_DATA_AVAILABLE 以外のすべてが返された場合は、以上ないストリームのパラメーター データを取得するがあるし、リターン コードが実行される次のステートメントのリターン コードになります。  
  
7.  呼び出す**SQLMoreResults** sql_no_data が返されるまでは、次のパラメーターのセットを処理します。 **SQLMoreResults**は SQL_ATTR_PARAMSET_SIZE ステートメント属性が 1 に設定された場合、この例では SQL_NO_DATA を返します。 それ以外の場合、 **SQLMoreResults**を次のセットを取得するパラメーターの使用可能なストリームの出力パラメーターがあることを示す SQL_PARAM_DATA_AVAILABLE が返されます。  
  
 引数で使用されるトークンの DAE 入力パラメーターと同様に、 *ParameterValuePtr*で**SQLBindParameter** (ステップ 1) を含むアプリケーションのデータ構造を指すポインターであることができます、パラメーターは、アプリケーション固有の詳細については、序数に必要な場合。  
  
 返されたストリーム出力または入力/出力パラメーターの順序は特定のドライバーと常にできないクエリで指定された順序と同じです。  
  
 アプリケーションが要求されていない場合**SQLGetData**手順 4 で、パラメーターの値は破棄されます。 同様に、アプリケーションを呼び出す場合**SQLParamData**で前にすべてのパラメーターの値が読み取られた**SQLGetData**残りの値が破棄され、アプリケーションは、[次へ] を処理できますパラメーター。  
  
 アプリケーションを呼び出す場合**SQLMoreResults**パラメーターを処理するすべてのストリーム出力する前に (**SQLParamData** SQL_PARAM_DATA_AVAILABLE を返すも)、残りのすべてのパラメーターは破棄されます。 同様に、アプリケーションから呼び出す場合**SQLMoreResults**で前にすべてのパラメーターの値が読み取られた**SQLGetData**、残りのすべてのパラメーターと値の剰余を破棄して、アプリケーションは、次のパラメーター セットを処理し続けることができます。  
  
 アプリケーションが両方の C データ型を指定できます**SQLBindParameter**と**SQLGetData**します。 指定された C データ型**SQLGetData**で指定された C データ型をオーバーライド**SQLBindParameter**の C データ型が指定されていない限り、 **SQLGetData** SQL_APD_TYPE が。  
  
 BLOB の出力パラメーターのデータ型がストリーミングされる出力パラメーターはさらに便利なこの機能は任意のデータ型にも使用できます。 ストリームの出力パラメーターでサポートされるデータ型は、ドライバーで指定されます。  
  
 処理する SQL_PARAM_INPUT_OUTPUT_STREAM パラメーターがある場合**SQLExecute**または**SQLExecDirect**最初 SQL_NEED_DATA を返します。 アプリケーションが呼び出すことができます**SQLParamData**と**SQLPutData** DAE パラメーターのデータを送信します。 すべての DAE 入力パラメーターが処理されるとき**SQLParamData**を示すストリーミング出力パラメーターは SQL_PARAM_DATA_AVAILABLE を返します。  
  
 出力パラメーターとバインドの出力パラメーターを処理してストリーミングは、ドライバーには、出力パラメーターを処理するための順序が決定します。 そのため、バッファーに出力パラメーターがバインドされている場合 (、 **SQLBindParameter**パラメーター *InputOutputType* SQL_PARAM_INPUT_OUTPUT または SQL_PARAM_OUTPUT に設定されている)、バッファーがまで設定されていない可能性があります**SQLParamData** SQL_SUCCESS、SQL_SUCCESS_WITH_INFO を返します。 アプリケーションは、バインドされたを読み込む必要がありますにした場合のみバッファー **SQLParamData** SQL_SUCCESS または SQL_SUCCESS_WITH_INFO をストリーム出力パラメーターでは、すべての処理を返します。  
  
 データ ソースは、さらに、ストリーミングされる出力パラメーターの警告と結果セットを返すことができます。 一般に、警告および結果セットが個別に処理ストリーミングされる出力パラメーターから呼び出すことによって**SQLMoreResults**します。 プロセスの警告と、結果をストリーム出力パラメーターを処理する前に設定します。  
  
 次の表では、サーバー、およびアプリケーションのしくみに送信される 1 つのコマンドのさまざまなシナリオについて説明します。  
  
|シナリオ|SQLExecute、SQLExecDirect またはからの戻り値|次に行うこと|  
|--------------|---------------------------------------------------|---------------------|  
|データには、ストリーミングされる出力パラメーターにはのみが含まれます。|SQL_PARAM_DATA_AVAILABLE|使用**SQLParamData**と**SQLGetData**ストリーミングされる出力パラメーターを取得します。|  
|データが結果セットが含まれていますとストリーム出力パラメーター|SQL_SUCCESS|使用して結果セットを取得**SQLBindCol**と**SQLGetData**します。<br /><br /> 呼び出す**SQLMoreResults**にストリーミングされる出力パラメーターの処理を開始します。 SQL_PARAM_DATA_AVAILABLE が返されます。<br /><br /> 使用**SQLParamData**と**SQLGetData**ストリーミングされる出力パラメーターを取得します。|  
|データ警告メッセージが含まれ、ストリーム出力パラメーター|SQL_SUCCESS_WITH_INFO|使用**SQLGetDiagRec**と**SQLGetDiagField**に警告メッセージを処理します。<br /><br /> 呼び出す**SQLMoreResults**にストリーミングされる出力パラメーターの処理を開始します。 SQL_PARAM_DATA_AVAILABLE が返されます。<br /><br /> 使用**SQLParamData**と**SQLGetData**ストリーミングされる出力パラメーターを取得します。|  
|データには警告メッセージが含まれています、結果の設定し出力パラメーターのストリーミング|SQL_SUCCESS_WITH_INFO|使用**SQLGetDiagRec**と**SQLGetDiagField**に警告メッセージを処理します。 呼び出して**SQLMoreResults**結果の処理を開始するには設定します。<br /><br /> 結果のセットを取得**SQLBindCol**と**SQLGetData**します。<br /><br /> 呼び出す**SQLMoreResults**にストリーミングされる出力パラメーターの処理を開始します。 **SQLMoreResults** SQL_PARAM_DATA_AVAILABLE を返す必要があります。<br /><br /> 使用**SQLParamData**と**SQLGetData**ストリーミングされる出力パラメーターを取得します。|  
|たとえば、ストリームの入力/出力 (DAE) パラメーター DAE の入力パラメーターを持つクエリします。|SQL NEED_DATA|呼び出す**SQLParamData**と**SQLPutData** DAE を送信するには、パラメーターのデータを入力します。<br /><br /> すべての DAE 入力パラメーターが処理された後**SQLParamData**リターン コードを返すことができます**SQLExecute**と**SQLExecDirect**返すことができます。 このテーブル内のケースを適用できます。<br /><br /> SQL_PARAM_DATA_AVAILABLE をリターン コードには、ストリーミングされる出力パラメーターを使用できます。 アプリケーションを呼び出す必要があります**SQLParamData**でこのテーブルの最初の行の説明に従って、ストリームの出力パラメーターのトークンを取得するには、もう一度です。<br /><br /> リターン コードが SQL_SUCCESS の場合は、処理の結果セットがあるか、処理が完了。<br /><br /> リターン コードが SQL_SUCCESS_WITH_INFO の場合は、警告メッセージを処理します。|  
  
 後**SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**アプリケーションを呼び出す返します SQL_PARAM_DATA_AVAILABLE、関数のシーケンス エラーが発生します。次の一覧にない機能:  
  
-   **SQLAllocHandle** / **SQLAllocHandleStd**  
  
-   **SQLDataSources** / **SQLDrivers**  
  
-   **SQLGetInfo** / **SQLGetFunctions**  
  
-   **SQLGetConnectAttr** / **SQLGetEnvAttr** / **SQLGetDescField** / **SQLGetDescRec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **SQLGetDiagField** / **SQLGetDiagRec**  
  
-   **SQLCancel**  
  
-   **SQLCancelHandle** (されたステートメント ハンドル)  
  
-   **SQLFreeStmt** (オプション = SQL_CLOSE、SQL_DROP または SQL_UNBIND)  
  
-   **SQLCloseCursor**  
  
-   **SQLDisconnect**  
  
-   **SQLFreeHandle** (HandleType = sql_handle_stmt として)  
  
-   **SQLGetStmtAttr**  
  
 アプリケーションは引き続き使用できます**SQLSetDescField**または**SQLSetDescRec**バインド情報を設定します。 フィールド マッピングは変更されません。 ただし、記述子内のフィールドは、新しい値を返す可能性があります。 たとえば、SQL_DESC_PARAMETER_TYPE には、SQL_PARAM_INPUT_OUTPUT_STREAM または SQL_PARAM_OUTPUT_STREAM を返す可能性があります。  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>使用シナリオ:結果セットからの部分でイメージを取得します。  
 **SQLGetData**ストアド プロシージャが 1 行のイメージに関するメタデータを含む結果セットを返すし、イメージが大規模な出力パラメーターで返されるときに、部分でデータを取得するために使用できます。  
  
```  
// CREATE PROCEDURE SP_TestOutputPara  
//      @ID_of_picture   as int,  
//      @Picture         as varbinary(max) out  
// AS  
//     output the image data through streamed output parameter  
// GO  
BOOL displayPicture(SQLUINTEGER idOfPicture, SQLHSTMT hstmt) {  
   SQLLEN      lengthOfPicture;    // The actual length of the picture.  
   BYTE        smallBuffer[100];   // A very small buffer.  
   SQLRETURN   retcode, retcode2;  
  
   // Bind the first parameter (input parameter)  
   SQLBindParameter(  
         hstmt,  
         1,                         // The first parameter.   
         SQL_PARAM_INPUT,           // Input parameter: The ID_of_picture.  
         SQL_C_ULONG,               // The C Data Type.  
         SQL_INTEGER,               // The SQL Data Type.  
         0,                         // ColumnSize is ignored for integer.  
         0,                         // DecimalDigits is ignored for integer.  
         &idOfPicture,              // The Address of the buffer for the input parameter.  
         0,                         // BufferLength is ignored for integer.  
         NULL);                     // This is ignored for integer.  
  
   // Bind the streamed output parameter.  
   SQLBindParameter(  
         hstmt,   
         2,                         // The second parameter.  
         SQL_PARAM_OUTPUT_STREAM,   // A streamed output parameter.   
         SQL_C_BINARY,              // The C Data Type.    
         SQL_VARBINARY,             // The SQL Data Type.  
         0,                         // ColumnSize: The maximum size of varbinary(max).  
         0,                         // DecimalDigits is ignored for binary type.  
         (SQLPOINTER)2,             // ParameterValuePtr: An application-defined  
                                    // token (this will be returned from SQLParamData).  
                                    // In this example, we used the ordinal   
                                    // of the parameter.  
         0,                         // BufferLength is ignored for streamed output parameters.  
         &lengthOfPicture);         // StrLen_or_IndPtr: The status variable returned.   
  
   retcode = SQLPrepare(hstmt, L"{call SP_TestOutputPara(?, ?)}", SQL_NTS);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   retcode = SQLExecute(hstmt);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   // Assume that the retrieved picture exists.  Use SQLBindCol or SQLGetData to retrieve the result-set.  
  
   // Process the result set and move to the streamed output parameters.  
   retcode = SQLMoreResults( hstmt );  
  
   // SQLGetData retrieves and displays the picture in parts.  
   // The streamed output parameter is available.  
   while (retcode == SQL_PARAM_DATA_AVAILABLE) {  
      SQLPOINTER token;   // Output by SQLParamData.  
      SQLLEN cbLeft;      // #bytes remained  
      retcode = SQLParamData(hstmt, &token);   // returned token is 2 (according to the binding)  
      if ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
         // A do-while loop retrieves the picture in parts.  
         do {  
            retcode2 = SQLGetData(   
               hstmt,   
               (UWORD) token,          // the value of the token is the ordinal.   
               SQL_C_BINARY,           // The C-type.  
               smallBuffer,            // A small buffer.   
               sizeof(smallBuffer),    // The size of the buffer.  
               &cbLeft);               // How much data we can get.  
         }  
         while ( retcode2 == SQL_SUCCESS_WITH_INFO );  
      }  
   }  
  
   return TRUE;  
}  
```  
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>使用シナリオ:ストリームの入力/出力パラメーターとしてのラージ オブジェクトの送受信  
 **SQLGetData**を取得し、ストアド プロシージャでは、ラージ オブジェクトを渡すと、データベースの間の値をストリーミング入力/出力パラメーターとしての部分でデータを送信するために使用できます。 メモリ内のすべてのデータを格納する必要はありません。  
  
```  
// CREATE PROCEDURE SP_TestInOut  
//       @picture as varbinary(max) out  
// AS  
//    output the image data through output parameter   
// go  
  
BOOL displaySimilarPicture(BYTE* image, ULONG lengthOfImage, SQLHSTMT hstmt) {  
   BYTE smallBuffer[100];   // A very small buffer.  
   SQLRETURN retcode, retcode2;  
   SQLLEN statusOfPicture;  
  
   // First bind the parameters, before preparing the statement that binds the output streamed parameter.  
   SQLBindParameter(  
      hstmt,   
      1,                                 // The first parameter.  
      SQL_PARAM_INPUT_OUTPUT_STREAM,     // I/O-streamed parameter: The Picture.  
      SQL_C_BINARY,                      // The C Data Type.  
      SQL_VARBINARY,                     // The SQL Data Type.  
      0,                                 // ColumnSize: The maximum size of varbinary(max).  
      0,                                 // DecimalDigits is ignored.   
      (SQLPOINTER)1,                     // An application defined token.   
      0,                                 // BufferLength is ignored for streamed I/O parameters.  
      &statusOfPicture);                 // The status variable.  
  
   statusOfPicture = SQL_DATA_AT_EXEC;   // Input data in parts (DAE parameter at input).  
  
   retcode = SQLPrepare(hstmt, L"{call SP_TestInOut(?) }", SQL_NTS);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   // Execute the statement.  
   retcode = SQLExecute(hstmt);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   if ( retcode == SQL_NEED_DATA ) {  
      // Use SQLParamData to loop through DAE input parameters.  For  
      // each, use SQLPutData to send the data to database in parts.  
  
      // This example uses an I/O parameter with streamed output.  
      // Therefore, the last call to SQLParamData should return  
      // SQL_PARAM_DATA_AVAILABLE to indicate the end of the input phrase   
      // and report that a streamed output parameter is available.  
  
      // Assume retcode is set to the return value of the last call to  
      // SQLParamData, which is equal to SQL_PARAM_DATA_AVAILABLE.  
   }  
  
   // Start processing the streamed output parameters.  
   while ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
      SQLPOINTER token;   // Output by SQLParamData.  
      SQLLEN cbLeft;     // #bytes remained  
      retcode = SQLParamData(hstmt, &token);  
      if ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
         do {  
            retcode2 = SQLGetData(   
               hstmt,   
               (UWORD) token,          // the value of the token is the ordinal.   
               SQL_C_BINARY,           // The C-type.  
               smallBuffer,            // A small buffer.   
               sizeof(smallBuffer),    // The size of the buffer.  
               &cbLeft);               // How much data we can get.  
         }  
         while ( retcode2 == SQL_SUCCESS_WITH_INFO );  
      }  
   }   
  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>参照  
 [ステートメント パラメーター](../../../odbc/reference/develop-app/statement-parameters.md)
