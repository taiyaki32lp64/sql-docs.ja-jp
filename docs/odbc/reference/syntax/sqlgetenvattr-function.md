---
title: SQLGetEnvAttr 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetEnvAttr
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLGetEnvAttr
helpviewer_keywords:
- SQLGetEnvAttr function [ODBC]
ms.assetid: 01f4590f-427a-4280-a1c3-18de9f7d86c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0940a5a2c70a7b670ca6a81521759fd08e60461e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345629"
---
# <a name="sqlgetenvattr-function"></a>SQLGetEnvAttr 関数
**互換性**  
 導入されたバージョン:ODBC 3.0 標準準拠:ISO 92  
  
 **まとめ**  
 **SQLGetEnvAttr**は、環境属性の現在の設定を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLGetEnvAttr(  
     SQLHENV        EnvironmentHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>引数  
 *EnvironmentHandle*  
 代入環境ハンドル。  
  
 *属性*  
 代入取得する属性。  
  
 *ValuePtr*  
 Output*属性*によって指定された属性の現在の値を返すバッファーへのポインター。  
  
 *Valueptr*が NULL の場合でも、 *stringlength Ptr*は、 *valueptr*が指すバッファー内で返されるバイトの合計数 (文字データの NULL 終端文字を除く) を返します。  
  
 *BufferLength*  
 代入*Valueptr*が文字列を指している場合、この引数は*valueptr*の\*長さである必要があります。 \**Valueptr*が整数の場合、 *bufferlength*は無視されます。 *\*Valueptr*が Unicode 文字列の場合 ( **SQLGetEnvAttrW**を呼び出す場合)、 *bufferlength*引数は偶数である必要があります。 属性値が文字列でない場合、 *Bufferlength*は使用されません。  
  
 *StringLengthPtr*  
 [出力] (Null 終了文字を除く) バイトの合計数を返すバッファーへのポインターで返される使用可能な *\*ValuePtr*します。 *Valueptr*が null ポインターの場合、長さは返されません。 属性値が文字列であり、返されるバイト数が*bufferlength*以上の場合、 \* *valueptr*内のデータは*bufferlength*に切り捨てられ、null 終了の長さを引いたものになります。文字とはドライバーによって null で終了します。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLGetEnvAttr**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合は、 *handletype* SQL_HANDLE_ENV と*EnvironmentHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって、関連付けられた SQLSTATE 値を取得できます。 次の表に、 **SQLGetEnvAttr**によって一般的に返される SQLSTATE 値と、この関数のコンテキストにおけるそれぞれの説明を示します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データ、右側が切り捨てられました|\* *Valueptr*に返されたデータは、 *bufferlength*から null 終了文字を引いた値に切り詰められました。 切り捨てられていない文字列値の長さは、**Stringlength ptr*で返されます。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|HY000|一般エラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 Messagetext バッファーの**SQLGetDiagRec によっ**て返されるエラーメッセージには、エラーとその原因が記述されています。  *\**|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンスエラー|(DM) **SQL_ATTR_ODBC_VERSION**は、 **SQLSetEnvAttr**によってまだ設定されていません。 **SQLAllocHandleStd**を使用している場合は、 **SQL_ATTR_ODBC_VERSION**を明示的に設定する必要はありません。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY092|属性またはオプションの識別子が無効です|引数*属性*に指定された値は、ドライバーでサポートされている ODBC のバージョンに対して有効ではありませんでした。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|引数*属性*に指定された値は、ドライバーでサポートされている odbc のバージョンに対して有効な odbc 環境属性でしたが、ドライバーではサポートされていませんでした。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *EnvironmentHandle*に対応するドライバーでは、関数はサポートされていません。|  
  
## <a name="comments"></a>コメント  
 属性の一覧については、「 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)」を参照してください。 ドライバー固有の環境属性はありません。 *属性*が文字列を返す属性を指定する場合、 *valueptr*は文字列を返すバッファーへのポインターである必要があります。 文字列の最大長 (null 終了バイトを含む) は、 *Bufferlength*バイトになります。  
  
 **SQLGetEnvAttr**は、環境ハンドルの割り当てと解放の間でいつでも呼び出すことができます。 アプリケーションによって環境に対して正常に設定されたすべての環境属性は、SQL_HANDLE_ENV の*Handletype*を使用して*EnvironmentHandle*で**sqlfreehandle**が呼び出されるまで保持されます。 ODBC 3.x では、複数の環境ハンドルを同時に割り当てることができます。 環境属性は、別の環境が割り当てられている場合、影響を受けません。  
  
> [!NOTE]
>  SQL_ATTR_OUTPUT_NTS 環境属性は、標準に準拠しているアプリケーションでサポートされています。 **SQLGetEnvAttr**が呼び出されると、ODBC 3 *. x*ドライバーマネージャーは常にこの属性の SQL_TRUE を返します。 **SQLSetEnvAttr**を呼び出すことによってのみ、SQL_ATTR_OUTPUT_NTS を SQL_TRUE に設定できます。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|接続属性の設定を返す|[SQLGetConnectAttr 関数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|ステートメント属性の設定を返す|[SQLGetStmtAttr 関数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|接続属性の設定|[SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|環境属性の設定|[SQLSetEnvAttr 関数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|ステートメント属性の設定|[SQLSetStmtAttr 関数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
