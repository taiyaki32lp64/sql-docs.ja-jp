---
title: SQLAllocHandle 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLAllocHandle
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLAllocHandle
helpviewer_keywords:
- SQLAllocHandle function [ODBC]
ms.assetid: 6e7fe420-8cf4-4e72-8dad-212affaff317
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2fcf08a4a55a7c65dbc94219ac908da83ea15bad
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344280"
---
# <a name="sqlallochandle-function"></a>SQLAllocHandle 関数
**互換性**  
 導入されたバージョン:ODBC 3.0 標準準拠:ISO 92  
  
 **まとめ**  
 **SQLAllocHandle**は、環境、接続、ステートメント、または記述子ハンドルを割り当てます。  
  
> [!NOTE]  
>  この関数は、ODBC 2.0 関数**Sqlallocconnect**、 **sqlallocconnect**、および**sqlallocconnect**を置き換えるハンドルを割り当てるためのジェネリック関数です。 **SQLAllocHandle**を呼び出しているアプリケーションが ODBC 2 で動作できるようにします。*x*ドライバーは、ドライバーマネージャーで**SQLAllocHandle**の呼び出しを、必要に応じて **sqlallocconnect**、 **sqlallocconnect**、または**sqlallocconnect**にマップします。 詳細については、「コメント」を参照してください。 ドライバーマネージャーが ODBC 3 でこの関数をマップする方法の詳細については、「」を参照してください。*x*アプリケーションは ODBC 2 で動作しています。*x*ドライバー、「[アプリケーションの旧バージョンとの互換性のための置換関数のマッピング](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>引数  
 *HandleType*  
 代入**SQLAllocHandle**によって割り当てられるハンドルの種類。 次のいずれかの値を指定する必要があります。  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN HANDLE は、ドライバーマネージャーとドライバーによってのみ使用されます。 アプリケーションでは、このハンドルの種類を使用しないでください。 SQL_HANDLE_DBC_INFO_TOKEN の詳細については、「 [ODBC ドライバーでの接続プールの認識の開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)」を参照してください。  
  
 *InputHandle*  
 代入新しいハンドルが割り当てられるコンテキストを持つの入力ハンドル。 *Handletype*が SQL_HANDLE_ENV の場合、これは SQL_NULL_HANDLE です。 *Handletype*が SQL_HANDLE_DBC の場合、これは環境ハンドルである必要があります。また、SQL_HANDLE_STMT または SQL_HANDLE_DESC の場合は、接続ハンドルである必要があります。  
  
 *OutputHandlePtr*  
 Output新しく割り当てられたデータ構造体にハンドルを返すバッファーへのポインター。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_INVALID_HANDLE、または SQL_ERROR。  
  
 環境ハンドル以外のハンドルを割り当てる場合、 **SQLAllocHandle**が SQL_ERROR を返すと、 *handletype*の値に応じて*OutputHandlePtr*が SQL_NULL_HDBC、SQL_NULL_HSTMT、または SQL_NULL_HDESC に設定されます (ただし、出力引数が null ポインターです。 その後、アプリケーションは、 *InputHandle*引数のハンドルに関連付けられている診断データ構造から追加情報を取得できます。  
  
## <a name="environment-handle-allocation-errors"></a>環境ハンドルの割り当てエラー  
 環境の割り当ては、ドライバーマネージャー内と各ドライバー内で行われます。 *Handletype*が SQL_HANDLE_ENV の**SQLAllocHandle**によって返されるエラーは、エラーが発生したレベルによって異なります。  
  
 *Handletype*が SQL_HANDLE_ENV の**SQLAllocHandle**が呼び出されたときに、ドライバーマネージャーが *\*OutputHandlePtr*にメモリを割り当てられない場合、またはアプリケーションが*OutputHandlePtr*に null ポインターを提供した場合は、 **SQLAllocHandle**は SQL_ERROR を返します。 ドライバーマネージャーは **OutputHandlePtr*を SQL_NULL_HENV に設定します (アプリケーションが SQL_ERROR を返す NULL ポインターを指定していない場合)。 追加の診断情報を関連付けるハンドルがありません。  
  
 ドライバーマネージャーは、アプリケーションが**SQLConnect**、 **SQLBrowseConnect**、または**SQLDriverConnect**を呼び出すまで、ドライバーレベルの環境ハンドル割り当て関数を呼び出しません。 ドライバーレベルの**SQLAllocHandle**関数でエラーが発生した場合、driver Manager レベルの**SQLConnect**、 **SQLBrowseConnect**、または**SQLDriverConnect**関数は SQL_ERROR を返します。 診断データ構造に SQLSTATE IM004 (ドライバーの**SQLAllocHandle** failed) が含まれています。 このエラーは、接続ハンドルで返されます。  
  
 ドライバーマネージャーとドライバー間の関数呼び出しのフローの詳細については、「 [SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)」を参照してください。  
  
## <a name="diagnostics"></a>診断  
 **SQLAllocHandle**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合、関連する SQLSTATE 値は、適切な*Handletype*と*Handle*を *InputHandle* の値に設定して**SQLGetDiagRec**を呼び出すことによって取得できます。 *OutputHandle*引数に対して SQL_SUCCESS_WITH_INFO (SQL_ERROR ではありません) を返すことができます。 次の表に、 **SQLAllocHandle**によって通常返される SQLSTATE 値と、この関数のコンテキストでのそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|08003|接続が開かれていません|(DM) *Handletype*引数が SQL_HANDLE_STMT または SQL_HANDLE_DESC でしたが、 *InputHandle*引数で指定された接続が開いていませんでした。 ドライバーがステートメントまたは記述子ハンドルを割り当てるには、接続プロセスが正常に完了し (接続が開いている必要があります) 必要があります。|  
|HY000|一般エラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 \* *Messagetext*バッファーの**SQLGetDiagRec**によって返されるエラーメッセージには、エラーとその原因が記述されています。|  
|HY001|メモリ割り当てエラー|(DM) ドライバーマネージャーは、指定されたハンドルにメモリを割り当てられませんでした。<br /><br /> ドライバーは、指定されたハンドルにメモリを割り当てられませんでした。|  
|HY009|Null ポインターの使い方が正しくありません|(DM) *OutputHandlePtr*引数が null ポインターでした。|  
|HY010|関数のシーケンスエラー|(DM) *Handletype*引数が SQL_HANDLE_DBC で、 **SQLSetEnvAttr**が呼び出されていないため、SQL_ODBC_VERSION 環境属性が設定されていません。<br /><br /> (DM) 非同期的に実行する関数が**InputHandle**に対して呼び出されましたが、 **HANDLETYPE**を SQL_HANDLE_STMT または SQL_HANDLE_DESC に設定して**SQLAllocHandle**関数が呼び出されたときに実行中でした。|  
|HY013|メモリ管理エラー|*Handletype*引数は SQL_HANDLE_DBC、SQL_HANDLE_STMT、または SQL_HANDLE_DESC です。また、基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY014|ハンドル数の上限を超えました|*Handletype*引数によって示されるハンドルの型に割り当てることができるハンドル数に対するドライバー定義の制限に達しました。|  
|HY092|属性またはオプションの識別子が無効です|(DM) *Handletype*引数が次のものではありませんでした:SQL_HANDLE_ENV、SQL_HANDLE_DBC、SQL_HANDLE_STMT、または SQL_HANDLE_DESC。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|*Handletype*引数が SQL_HANDLE_DESC で、ドライバーが ODBC 2 でした。*x*ドライバー。|  
|HYT01|接続タイムアウトの期限が切れました|データソースが要求に応答する前に、接続のタイムアウト期間が経過しました。 接続タイムアウト期間は、 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT によって設定されます。|  
|IM001|ドライバーはこの機能をサポートしていません|(DM) *Handletype*引数は SQL_HANDLE_STMT で、ドライバーは有効な ODBC ドライバーではありませんでした。<br /><br /> (DM) *Handletype*引数は SQL_HANDLE_DESC でしたが、ドライバーは記述子ハンドルの割り当てをサポートしていません。|  
  
## <a name="comments"></a>コメント  
 **SQLAllocHandle**は、次のセクションで説明するように、環境、接続、ステートメント、および記述子のハンドルを割り当てるために使用されます。 ハンドルに関する一般的な情報については、「[ハンドル](../../../odbc/reference/develop-app/handles.md)」を参照してください。  
  
 複数の割り当てがドライバーによってサポートされている場合は、一度に1つのアプリケーションで複数の環境、接続、またはステートメントハンドルを割り当てることができます。 ODBC では、一度に割り当てることができる環境、接続、ステートメント、または記述子ハンドルの数に制限は定義されていません。 ドライバーは、一度に割り当てることができる特定の種類のハンドルの数に制限を課すことがあります。詳細については、ドライバーのドキュメントを参照してください。  
  
 アプリケーションが、  *\*OutputHandlePtr*が既に存在する環境、接続、ステートメント、または記述子ハンドルに設定された**SQLAllocHandle**を呼び出す場合、ドライバーは*ハンドル*に関連付けられている情報を上書きします。アプリケーションで接続プールを使用している場合を除きます (このセクションで後述する「接続プールの環境属性の割り当て」を参照してください)。 ドライバーマネージャーでは、  *\*OutputHandlePtr*に入力された*ハンドル*が既に使用されているかどうかは確認されません。また、ハンドルの内容を上書きする前に、そのハンドルもチェックしません。  
  
> [!NOTE]  
>  *\*OutputHandlePtr*に対して定義されているものと同じアプリケーション変数を使用して**SQLAllocHandle**を2回呼び出すと、再割り当ての前にそのハンドルを解放するために**sqlfreehandle**を呼び出さなくても、ODBC アプリケーションプログラミングが正しく行われません. このような方法で ODBC ハンドルを上書きすると、ODBC ドライバーの一部で動作が不安定になったりエラーが発生したりする可能性があります。  
  
 複数のスレッドをサポートするオペレーティングシステムでは、アプリケーションは異なるスレッドで同じ環境、接続、ステートメント、または記述子ハンドルを使用できます。 このため、ドライバーは、この情報に対して安全でマルチスレッドアクセスをサポートする必要があります。これを実現する1つの方法は、たとえば、クリティカルセクションまたはセマフォを使用することです。 スレッド処理の詳細については、「[マルチスレッド](../../../odbc/reference/develop-app/multithreading.md)」を参照してください。  
  
 **SQLAllocHandle**は、環境ハンドルを割り当てるために呼び出されるときに SQL_ATTR_ODBC_VERSION environment 属性を設定しません。環境属性はアプリケーションによって設定される必要があります。接続ハンドルを割り当てるために**SQLAllocHandle**が呼び出されると、SQLSTATE HY010 (関数シーケンスエラー) が返されます。  
  
 標準に準拠しているアプリケーションの場合、 **SQLAllocHandle**はコンパイル時に**SQLAllocHandleStd**にマップされます。 これら2つの関数の違いは、SQL_HANDLE_ENV に設定されている*Handletype*引数を使用して呼び出された場合に、 **SQLAllocHandleStd**が SQL_ATTR_ODBC_VERSION 環境属性を SQL_OV_ODBC3 に設定することです。 標準に準拠しているアプリケーションは常に ODBC 3 であるため、この処理が行われます。*x*アプリケーション。 また、標準では、アプリケーションのバージョンを登録する必要がありません。 これは、次の2つの関数の唯一の違いです。それ以外の場合は同じです。 **SQLAllocHandleStd**は、ドライバーマネージャー内の**SQLAllocHandle**にマップされます。 そのため、サードパーティのドライバーでは、 **SQLAllocHandleStd**を実装する必要はありません。  
  
 ODBC 3.8 アプリケーションでは次のものを使用する必要があります。  
  
-   **SQLAllocHandle と Not SQLAllocHandleStd**は、環境ハンドルを割り当てます。  
  
-   **SQLSETENVATTR** SQL_ATTR_ODBC_VERSION environment 属性を SQL_OV_ODBC3_80 に設定します。  
  
## <a name="allocating-an-environment-handle"></a>環境ハンドルの割り当て  
 環境ハンドルは、有効な接続ハンドルやアクティブな接続ハンドルなどのグローバル情報へのアクセスを提供します。 環境ハンドルに関する一般的な情報については、「[環境ハンドル](../../../odbc/reference/develop-app/environment-handles.md)」を参照してください。  
  
 環境ハンドルを要求するには、アプリケーションは*Handletype*が SQL_HANDLE_ENV で*InputHandle*が SQL_NULL_HANDLE である**SQLAllocHandle**を呼び出します。 ドライバーは、環境情報にメモリを割り当て、関連付けられているハンドルの値を *\*OutputHandlePtr*引数に返します。 アプリケーションは、環境ハンドル引数を必要とする後続のすべての呼び出しで *\*OutputHandle*値を渡します。 詳細については、「[環境ハンドルの割り当て](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)」を参照してください。  
  
 ドライバーマネージャーの環境ハンドルで、ドライバーの環境ハンドルが既に存在する場合、接続が確立されたときに SQL_HANDLE_ENV の*Handletype*が**SQLAllocHandle**になっていると、そのドライバーでは呼び出されません。 **SQLAllocHandle**のみです。SQL_HANDLE_DBC の*Handletype*を使用します。 ドライバーマネージャーの環境ハンドルの下にドライバーの環境ハンドルが存在しない場合は、最初の接続時に SQL_HANDLE_ENV と SQLAllocHandle の HandleType を持つ SQLAllocHandle と HandleType SQL_HANDLE_DBC が両方ともドライバーで呼び出されます。環境のハンドルはドライバーに接続されています。  
  
 ドライバーマネージャーは、 *Handletype*が SQL_HANDLE_ENV の**SQLAllocHandle**関数を処理するときに、システム情報の [ODBC] セクションで**Trace**キーワードをチェックします。 1に設定されている場合、ドライバーマネージャーは現在のアプリケーションのトレースを有効にします。 トレースフラグが設定されている場合、最初の環境ハンドルが割り当てられた時点でトレースが開始され、最後の環境ハンドルが解放されると終了します。 詳細については、「[データソースの構成](../../../odbc/reference/install/configuring-data-sources.md)」を参照してください。  
  
 環境ハンドルを割り当てた後、アプリケーションは環境ハンドルで**SQLSetEnvAttr**を呼び出して、SQL_ATTR_ODBC_VERSION 環境属性を設定する必要があります。 環境で接続ハンドルを割り当てるために**SQLAllocHandle**が呼び出される前にこの属性が設定されていない場合、接続の割り当てを呼び出すと、SQLSTATE HY010 (関数シーケンスエラー) が返されます。 詳細については、「[アプリケーションの ODBC バージョンの宣言](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)」を参照してください。  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>接続プール用の共有環境の割り当て  
 環境は、1つのプロセスで複数のコンポーネント間で共有できます。 共有環境は、複数のコンポーネントで同時に使用することができます。 コンポーネントが共有環境を使用する場合は、プールされた接続を使用できます。これにより、接続を再作成することなく、既存の接続を割り当てて使用することができます。  
  
 接続プールに使用できる共有環境を割り当てる前に、アプリケーションで**SQLSetEnvAttr**を呼び出して、SQL_ATTR_CONNECTION_POOLING 環境属性を SQL_CP_ONE_PER_DRIVER または SQL_CP_ONE_PER_HENV に設定する必要があります。 この場合、 **SQLSetEnvAttr**は、 *EnvironmentHandle*を null に設定して呼び出されます。これにより、属性がプロセスレベルの属性になります。  
  
 接続プールが有効になると、アプリケーションは*Handletype*引数を SQL_HANDLE_ENV に設定して**SQLAllocHandle**を呼び出します。 この呼び出しで割り当てられた環境は、接続プールが有効になっているため、暗黙的な共有環境になります。  
  
 共有環境が割り当てられている場合、 *Handletype*が SQL_HANDLE_DBC の**SQLAllocHandle**が呼び出されるまで、使用される環境は決定されません。 その時点で、ドライバーマネージャーは、アプリケーションによって要求された環境属性に一致する既存の環境を見つけようとします。 このような環境が存在しない場合は、共有環境として作成されます。 ドライバーマネージャーは、各共有環境の参照カウントを保持します。環境が最初に作成されるときには、カウントは1に設定されます。 一致する環境が検出されると、その環境のハンドルがアプリケーションに返され、参照カウントがインクリメントされます。 この方法で割り当てられた環境ハンドルは、入力引数として環境ハンドルを受け入れる任意の ODBC 関数で使用できます。  
  
## <a name="allocating-a-connection-handle"></a>接続ハンドルの割り当て  
 接続ハンドルは、接続の有効なステートメントや記述子ハンドル、トランザクションが現在開いているかどうかなどの情報へのアクセスを提供します。 接続ハンドルに関する一般的な情報については、「[接続ハンドル](../../../odbc/reference/develop-app/connection-handles.md)」を参照してください。  
  
 接続ハンドルを要求するには、アプリケーションは*Handletype* SQL_HANDLE_DBC を使用して**SQLAllocHandle**を呼び出します。 *InputHandle*引数は、そのハンドルを割り当てた**SQLAllocHandle**への呼び出しによって返された環境ハンドルに設定されます。 ドライバーは接続情報にメモリを割り当て、関連付けられているハンドルの値を *\*OutputHandlePtr*に戻します。 アプリケーションは、接続ハンドルを必要とする後続のすべての呼び出しで *\*OutputHandlePtr*値を渡します。 詳細については、「[接続ハンドルの割り当て](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)」を参照してください。  
  
 ドライバーマネージャーは、 **SQLAllocHandle**関数を処理し、アプリケーションが**SQLConnect**、 **SQLBrowseConnect**、または**SQLDriverConnect**を呼び出したときに、ドライバーの**SQLAllocHandle**関数を呼び出します。 (詳細については、「 [SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)」を参照してください)。  
  
 環境で接続ハンドルを割り当てるために**SQLAllocHandle**が呼び出される前に SQL_ATTR_ODBC_VERSION environment 属性が設定されていない場合、接続の割り当てを呼び出すと、SQLSTATE HY010 (関数シーケンスエラー) が返されます。  
  
 アプリケーションが*InputHandle*引数を SQL_HANDLE_DBC に設定して**SQLAllocHandle**を呼び出し、さらに共有環境ハンドルに設定した場合、ドライバーマネージャーは環境属性に一致する既存の共有環境の検索を試みます。アプリケーションによって設定されます。 このような環境が存在しない場合は、参照カウント (ドライバーマネージャーによって管理されます) が1になるように作成されます。 一致する共有環境が見つかった場合、そのハンドルはアプリケーションに返され、その参照カウントがインクリメントされます。  
  
 **SQLConnect**または**SQLDriverConnect**が呼び出されるまで、使用される実際の接続はドライバーマネージャーによって決定されません。 ドライバーマネージャーは、 **SQLConnect** (または**SQLDriverConnect**の呼び出しの接続キーワード) の呼び出しで接続オプションを使用し、接続の割り当て後に設定された接続属性を使用して、プール内のどの接続を決定します。使用する必要があります。 詳細については、「 [SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)」を参照してください。  
  
## <a name="allocating-a-statement-handle"></a>ステートメント ハンドルの割り当て  
 ステートメントハンドルを使用すると、エラーメッセージ、カーソル名、SQL ステートメント処理の状態情報などのステートメント情報にアクセスできます。 ステートメントハンドルに関する一般的な情報については、「[ステートメントハンドル](../../../odbc/reference/develop-app/statement-handles.md)」を参照してください。  
  
 ステートメントハンドルを要求するために、アプリケーションはデータソースに接続し、SQL ステートメントを送信する前に**SQLAllocHandle**を呼び出します。 この呼び出しでは、 *Handletype*を SQL_HANDLE_STMT に設定し、 *InputHandle*を、そのハンドルを割り当てた**SQLAllocHandle**への呼び出しによって返された接続ハンドルに設定する必要があります。 ドライバーは、ステートメント情報にメモリを割り当て、指定された接続にステートメントハンドルを関連付け、関連付けられているハンドルの値を *\*OutputHandlePtr*に渡します。 アプリケーションは、ステートメントハンドルを必要とする後続のすべての呼び出しで *\*OutputHandlePtr*値を渡します。 詳細については、「[ステートメントハンドルの割り当て](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)」を参照してください。  
  
 ステートメントハンドルが割り当てられると、ドライバーによって自動的に4つの記述子のセットが割り当てられ、これらの記述子のハンドルが SQL_ATTR_APP_ROW_DESC、SQL_ATTR_APP_PARAM_DESC、SQL_ATTR_IMP_ROW_DESC、および SQL_ATTR_IMP_PARAM_DESC に割り当てられます。ステートメントの属性。 これらは、*暗黙的*に割り当てられた記述子と呼ばれます。 アプリケーション記述子を明示的に割り当てるには、次の「記述子ハンドルの割り当て」セクションを参照してください。  
  
## <a name="allocating-a-descriptor-handle"></a>記述子ハンドルの割り当て  
 アプリケーションが*Handletype*が SQL_HANDLE_DESC の**SQLAllocHandle**を呼び出すと、ドライバーはアプリケーション記述子を割り当てます。 これらは、*明示的*に割り当てられた記述子と呼ばれます。 アプリケーションは、SQL_ATTR_APP_ROW_DESC または SQL_ATTR_APP_ を使用して**SQLSetStmtAttr**関数を呼び出すことにより、特定のステートメントハンドルに対して自動的に割り当てられたアプリケーション記述子ではなく、明示的に割り当てられたアプリケーション記述子を使用するようにドライバーに指示します。PARAM_DESC 属性。 実装記述子を明示的に割り当てることはできません。また、 **SQLSetStmtAttr**関数呼び出しで実装記述子を指定することもできません。  
  
 明示的に割り当てられた記述子は、ステートメントハンドルではなく、接続ハンドルに関連付けられます (自動的に割り当てられた記述子はになります)。 記述子は、アプリケーションが実際にデータベースに接続されている場合にのみ割り当てられたままになります。 明示的に割り当てられた記述子は接続ハンドルに関連付けられるため、アプリケーションでは、明示的に割り当てられた記述子を接続内の複数のステートメントに関連付けることができます。 一方、暗黙的に割り当てられたアプリケーション記述子は、複数のステートメントハンドルに関連付けることはできません。 (割り当てられているものとは別のステートメントハンドルに関連付けることはできません)。明示的に割り当てられた記述子ハンドルは、アプリケーションによって明示的に解放するか、SQL_HANDLE_DESC の*Handletype*を使用して**sqlfreehandle**を呼び出すか、接続が閉じられたときに暗黙的に解放することができます。  
  
 明示的に割り当てられた記述子が解放されると、暗黙的に割り当てられた記述子がステートメントに再び関連付けられます。 (そのステートメントの SQL_ATTR_APP_ROW_DESC または SQL_ATTR_APP_PARAM_DESC 属性は、暗黙的に割り当てられた記述子ハンドルに設定されます)。これは、接続で明示的に割り当てられた記述子に関連付けられているすべてのステートメントに当てはまります。  
  
 記述子の詳細については、「[記述子](../../../odbc/reference/develop-app/descriptors.md)」を参照してください。  
  
## <a name="code-example"></a>コード例  
 「[サンプル ODBC プログラム](../../../odbc/reference/sample-odbc-program.md)」、「 [SQLBrowseConnect 関数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)」、「 [SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)」、および「 [SQLSetCursorName 関数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|SQL ステートメントの実行|[SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|準備された SQL ステートメントの実行|[SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|環境、接続、ステートメント、または記述子ハンドルの解放|[SQLFreeHandle 関数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|実行するステートメントの準備|[SQLPrepare 関数](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|接続属性の設定|[SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|記述子フィールドの設定|[SQLSetDescField 関数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|環境属性の設定|[SQLSetEnvAttr 関数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|ステートメント属性の設定|[SQLSetStmtAttr 関数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
