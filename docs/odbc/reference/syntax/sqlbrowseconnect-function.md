---
title: SQLBrowseConnect 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBrowseConnect
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBrowseConnect
helpviewer_keywords:
- SQLBrowseConnect function [ODBC]
ms.assetid: b7f1be66-e6c7-4790-88ec-62b7662103c0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2960c42690a9528763321bc882bb788b437cb66a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036201"
---
# <a name="sqlbrowseconnect-function"></a>SQLBrowseConnect 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ODBC  
  
 **概要**  
 **SQLBrowseConnect**反復的なメソッドを検出して、属性とデータ ソースに接続するために必要な属性の値を列挙するをサポートしています。 呼び出しごとに**SQLBrowseConnect**連続するレベルの属性と属性値を返します。 すべてのレベルが列挙された、データ ソースへの接続が完了し完全な接続文字列が返されます**SQLBrowseConnect**します。 SQL_SUCCESS または SQL_SUCCESS_WITH_INFO リターン コードは、すべての接続情報が指定されており、アプリケーションがデータ ソースに接続されているようになりましたことを示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLBrowseConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr);  
```  
  
## <a name="arguments"></a>引数  
 *ConnectionHandle*  
 [入力] 接続ハンドル。  
  
 *InConnectionString*  
 [入力]要求の接続文字列の参照 (を参照してください"*InConnectionString*引数"「コメント」)。  
  
 *StringLength1*  
 [入力]長さ **InConnectionString*文字数。  
  
 *OutConnectionString*  
 [出力]参照の結果の接続文字列を返す文字バッファーへのポインター (を参照してください"*OutConnectionString*引数"「コメント」内)。  
  
 場合*OutConnectionString*が null の場合、 *StringLength2Ptr*は文字 (文字データの null 終端文字を除く) の合計数を返しますが、バッファーに返される使用可能な指す*OutConnectionString*します。  
  
 *BufferLength*  
 [入力]文字の長さの **OutConnectionString*バッファー。  
  
 *StringLength2Ptr*  
 [出力]返される使用可能な文字 (除外 null 終了) の合計数\* *OutConnectionString*します。 返すに使用できる文字数がより大きいかに等しい場合*BufferLength*、内の接続文字列\* *OutConnectionString*に切り捨てられます*BufferLength* null 終了文字の長さマイナスです。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_ERROR、SQL_INVALID_HANDLE、または SQL_STILL_EXECUTING します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLBrowseConnect** SQL_ERROR、SQL_SUCCESS_WITH_INFO、または SQL_NEED_DATA、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType。* sql_handle_stmt としての*ConnectionHandle のハンドル*します。 次の表に、一般的にによって返される SQLSTATE 値**SQLBrowseConnect** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データで、右側が切り捨てられました|バッファー \* *OutConnectionString*が足りません全体の参照の結果の接続文字列を返すため、文字列が切り捨てられました。 バッファー **StringLength2Ptr*切り詰められていない参照結果の接続文字列の長さが含まれています。 (関数は、SQL_NEED_DATA を返します)。|  
|01S00|無効な接続文字列の属性|無効な属性のキーワードが参照要求の接続文字列で指定された (*InConnectionString*)。 (関数は、SQL_NEED_DATA を返します)。<br /><br /> 属性のキーワードが参照要求の接続文字列で指定された (*InConnectionString*) を現在の接続レベルには適用されません。 (関数は、SQL_NEED_DATA を返します)。|  
|01S02|値が変更されました|ドライバーでは、指定した値はサポートされていませんでした、 *ValuePtr*引数**SQLSetConnectAttr**のような値を置き換えるとします。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|08001|クライアント接続を確立できません。|ドライバーは、データ ソースとの接続を確立できませんでした。|  
|08002|使用されている接続名|(DM)、指定された接続は、データ ソースとの接続を確立するために既に使用されていたし、の接続が開かれていた。|  
|08004|サーバー接続を拒否しました|データ ソースには、実装定義上の理由から、接続の確立が拒否されます。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとの接続に、ドライバーをしようとしましたデータ ソース間の通信リンクに失敗しました。|  
|28000|無効な認証指定|ユーザー id 承認文字列またはその両方の参照で指定された要求の接続文字列 (*InConnectionString*)、データ ソースで定義されている制約に違反します。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|(DM)、ドライバー マネージャーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。<br /><br /> ドライバーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|呼び出して非同期操作が取り消されました[SQLCancelHandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)します。 後、元の関数でもう一度呼び出されますが、 *ConnectionHandle*します。<br /><br /> 呼び出して、操作が取り消されました**SQLCancelHandle**上、 *ConnectionHandle*マルチ スレッド アプリケーションで別のスレッドから。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *ConnectionHandle*この関数が呼び出されたときに実行されているとします。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|引数に指定された (DM) 値*StringLength1*が 0 未満、SQL_NTS に等しいでした。<br /><br /> 引数に指定された (DM) 値*BufferLength*が 0 未満でした。|  
|HY114|ドライバーは接続レベルの非同期関数の実行をサポートしていません|(DM)、アプリケーションでは、接続を確立する前に、接続ハンドルでの非同期操作を有効になります。 ただし、ドライバーは接続ハンドルでの非同期操作をサポートしていません。|  
|HYT00|タイムアウトが発生しました|完了したデータ ソースに接続する前に、ログイン タイムアウト期間が終了しました。 によって、タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_LOGIN_TIMEOUT します。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM)、指定されたデータ ソース名に対応するドライバーは、関数をサポートしていません。|  
|IM002|データ ソースが見つかりませんと指定された既定のドライバー|(DM)、データ ソースの参照要求の接続文字列で指定された名前 (*InConnectionString*)、システム情報に見つからなかったも既定ドライバーの仕様がありました。<br /><br /> (DM) システム情報 ODBC データ ソースと既定のドライバー情報が見つかりませんでした。|  
|IM003|指定されたドライバーを読み込むことができませんでした。|(DM)、ドライバーは、システムの情報でデータ ソースの仕様に記載またはで指定された、**ドライバー**キーワードが見つからなかったか、何らかの理由でアンロードできませんでした。|  
|IM004|ドライバーの**SQLAllocHandle**の SQL_HANDLE _ENV が失敗しました|(DM) 中に**SQLBrowseConnect**、ドライバー マネージャーという、ドライバーの**SQLAllocHandle**関数と、 *HandleType* sql_handle_env としてとドライバーの次のように返されます、。エラーがあります。|  
|IM005|ドライバーの**SQLAllocHandle**を sql_handle_dbc としてできませんでした|(DM) 中に**SQLBrowseConnect**、ドライバー マネージャーという、ドライバーの**SQLAllocHandle**関数と、 *HandleType*ドライバー sql_handle_dbc としての次のように返されます、。エラーがあります。|  
|IM006|ドライバーの**SQLSetConnectAttr**できませんでした|(DM) 中に**SQLBrowseConnect**、ドライバー マネージャーという、ドライバーの**SQLSetConnectAttr**関数と、ドライバーにエラーが返されます。|  
|IM009|トランスレーター DLL を読み込むことができません。|ドライバーは、翻訳または接続のデータ ソースの指定された DLL を読み込めませんでした。|  
|IM010|データ ソース名が長すぎます|(DM) DSN キーワードの属性の値は、SQL_MAX_DSN_LENGTH 文字を超えていました。|  
|IM011|ドライバー名が長すぎます|(DM)、DRIVER キーワードの属性の値が 255 文字より長かった。|  
|IM012|DRIVER キーワードの構文エラー|(DM)、DRIVER キーワードのキーワードと値のペアに構文エラーが含まれています。|  
|IM014|指定された DSN には、ドライバーとアプリケーション間のアーキテクチャの不一致が含まれています。|64 ビット ドライバー; に接続する DSN を使用する (DM) 32 ビット アプリケーションまたはその逆です。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
|S1118|ドライバーが非同期通知をサポートしていません|ドライバーが非同期通知をサポートしていない場合、SQL_ATTR_ASYNC_DBC_EVENT または SQL_ATTR_ASYNC_DBC_RETCODE_PTR を設定することはできません。|  
  
## <a name="inconnectionstring-argument"></a>InConnectionString 引数  
 参照要求の接続文字列では、次の構文があります。  
  
 *接続文字列*:: =*属性*[`;`] &#124; *属性* `;` *接続文字列*;<br>
 *属性*:: =*属性キーワード*`=`*属性値* &#124; `DRIVER=`[`{`]*属性と値の*[`}`]<br>
 *属性キーワード*:: = `DSN` &#124; `UID` &#124; `PWD` &#124; *ドライバー-定義の属性-キーワード*<br>
 *属性値*:: =*文字の文字列*<br>
 *ドライバーの定義の属性-キーワード*:: =*識別子*<br>
  
 場所*文字列*0 個以上の文字。*識別子*が 1 つ以上の文字。*属性キーワード*; 大文字小文字を区別することはありません*属性値*可能性があります。 大文字小文字を区別しの値、 **DSN**キーワードは空白ののみで構成されていません。 接続文字列と初期化ファイルの文法、キーワード、および属性の値の文字が含まれているため **:operator[]{}()、;?\*=! @** 避ける必要があります。 システム情報の文法、ため、キーワードおよびデータ ソース名が円記号を含めることはできません (\\) 文字。 ODBC 2 の場合。*x*ドライバー、DRIVER キーワードの属性値を囲む中かっこが必要です。  
  
 参照要求の接続文字列では、一切のキーワードが繰り返される、ドライバーは、最初に見つかったキーワードの関連付けられた値を使用します。 場合、 **DSN**と**ドライバー**で同じ参照要求の接続文字列キーワードが含まれている、ドライバー マネージャーとドライバーを使用して最初にどちらのキーワードが表示されます。  
  
 アプリケーションがデータ ソースまたはドライバーを選択する方法については、次を参照してください。[データ ソースまたはドライバーを選択する](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)します。  
  
## <a name="outconnectionstring-argument"></a>OutConnectionString 引数  
 参照結果の接続文字列は、接続属性の一覧です。 接続属性は、属性のキーワードと対応する属性値で構成されます。 参照結果の接続文字列では、次の構文があります。  
  
 *接続文字列*:: =*属性*[`;`] &#124; *属性* `;` *接続文字列*<br>
 *属性*:: = [`*`]*属性キーワード*`=`*属性値*<br>
 *属性キーワード*:: = *ODBC 属性-キーワード* &#124; *ドライバー-定義の属性-キーワード*<br>
 *ODBC 属性-キーワード*= {`UID` &#124; `PWD`} [`:`*ローカライズ識別子*]*ドライバー-定義の属性-キーワード*:: = *識別子*[`:`*ローカライズ識別子*]*属性値*:: = `{` *属性値リスト* `}` &#124; `?` (中かっこはリテラルは、ドライバーによって返される)。<br>
 *属性値リスト*:: =*文字列*[`:`*ローカライズされた文字の文字列*] &#124; *文字列*[`:`*ローカライズされた文字の文字列*] `,` *属性値リスト*<br>
  
 場所*文字列*と*ローカライズされた文字の文字列*0 個以上の文字。*識別子*と*ローカライズ識別子*1 つまたは複数の文字。*属性キーワード*小文字は区別; されず*属性値*小文字が区別されます。 接続により文字列および初期化ファイルの文法、キーワード、ローカライズされた識別子は、および属性値の文字が含まれている **:operator[]{}()、;?\*=! @** 避ける必要があります。 システム情報の文法、ため、キーワードおよびデータ ソース名が円記号を含めることはできません (\\) 文字。  
  
 参照結果の接続文字列の構文は、次のセマンティックの規則に従って使用されます。  
  
-   場合、アスタリスク (\*) の前に、*属性キーワード*、*属性*は省略可能で、次の呼び出しで省略できます**SQLBrowseConnect**します。  
  
-   属性のキーワード**UID**と**PWD**で定義されている同じ意味を持ちます**SQLDriverConnect**します。  
  
-   A*ドライバー-定義の属性-キーワード*属性値が指定する属性の種類の名前します。 たとえばである可能性があります**サーバー**、**データベース**、**ホスト**、または**DBMS**します。  
  
-   *ODBC 属性-キーワード*と*ドライバー-定義の属性-キーワード*キーワードのローカライズされたまたはユーザー フレンドリなバージョンが含まれます。 これは、アプリケーションでダイアログ ボックスのラベルとして使用可能性があります。 ただし、 **UID**、 **PWD**、または*識別子*単独で使用する必要が、ドライバーを 参照の要求文字列を渡すときにします。  
  
-   {*属性値リスト*} は実際の値の列挙体を対応する有効な*属性キーワード*します。 なお、中かっこ ({}) は選択肢の一覧を示していません。 ドライバーによって返されます。 たとえば、一連のサーバー名またはデータベース名の一覧があります。  
  
-   場合、*属性値*は 1 つの疑問符 (?) に対応する 1 つの値、*属性キーワード*します。 たとえば、UID ジョンズ; を =PWD Sesame を = です。  
  
-   呼び出しごとに**SQLBrowseConnect**接続プロセスの次のレベルを満たすために必要な情報のみを返します。 ドライバーは、コンテキストは呼び出しのたびに常に確認できるように、接続ハンドルの状態情報を関連付けます。  
  
## <a name="using-sqlbrowseconnect"></a>SQLBrowseConnect の使用  
 **SQLBrowseConnect**割り当て済みの接続が必要です。 ドライバー マネージャーに指定されているか、初期の参照要求の接続文字列で指定されたデータ ソース名に対応するドライバーを読み込みこれが発生すると詳細については、[コメント] セクションを参照してください。 [SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)します。 ドライバーは、参照の処理中に、データ ソースとの接続を設定できます。 場合**SQLBrowseConnect**未処理の接続が終了して、接続が接続されていない状態に返される、SQL_ERROR を返します。  
  
> [!NOTE]  
>  **SQLBrowseConnect**接続プールをサポートしていません。 場合**SQLBrowseConnect**接続プールを有効にすると、中に呼び出されます SQLSTATE HY000 (一般的なエラー) が返されます。  
  
 ときに**SQLBrowseConnect**呼びます接続で初めて参照要求の接続文字列を含める必要があります、 **DSN**キーワードまたは**ドライバー**キーワード。 参照要求の接続文字列が含まれている場合、 **DSN**キーワード、ドライバー マネージャーは、システム情報に対応するデータ ソースの指定を検索します。  
  
-   ドライバー マネージャーでは、対応するデータ ソースの指定が見つかると、関連付けられているドライバ DLL; を読み込むドライバーは、システム情報のデータ ソースに関する情報を取得できます。  
  
-   ドライバー マネージャーでは、対応するデータ ソースの指定を見つけられない場合、既定のデータ ソースの仕様を検索し、関連するドライバー DLL を読み込むドライバーは、システム情報の既定のデータ ソースに関する情報を取得できます。 "DEFAULT"は、DSN のドライバーに渡されます。  
  
-   ドライバー マネージャーは、対応するデータ ソースの指定を見つけることができません、既定のデータ ソースの指定がない場合は、SQLSTATE IM002 SQL_ERROR を返します (見つからないデータのソースおよび指定された既定のドライバー)。  
  
 参照要求の接続文字列が含まれている場合、**ドライバー**キーワード、ドライバー マネージャーは、指定されたドライバーを読み込みます。 システム情報内でデータ ソースを検索する試行しません。 **ドライバー**キーワードは、システム情報の情報を使用していない、ドライバーはドライバーは、参照要求の接続文字列の情報のみを使用してデータ ソースに接続できるように十分なキーワードを定義する必要があります。  
  
 呼び出すたびに**SQLBrowseConnect**アプリケーションが参照要求の接続文字列で、接続属性の値を指定します。 参照結果の接続文字列で、ドライバーが連続するレベルの属性と属性値を返します参照要求の接続文字列で列挙されていない接続属性がある限り、SQL_NEED_DATA が返されます。 アプリケーションでは、参照の結果の接続文字列の内容を使用して、次回の呼び出しの参照要求の接続文字列を構築**SQLBrowseConnect**します。 すべての必須属性 (にアスタリスクが付いていないもの、 *OutConnectionString*引数) に次の呼び出しに含める必要がある**SQLBrowseConnect**します。 現在参照要求接続文字列を構築するときに、アプリケーションが以前の参照の結果の接続文字列の内容を使用できないことに注意してください。つまり、前のレベルで設定の属性に別の値を指定できません。  
  
 接続と関連付けられている属性のすべてのレベルが列挙されたときに、ドライバーは SQL_SUCCESS を返し、データ ソースへの接続が完了すると、アプリケーションに完全な接続文字列が返されます。 接続文字列と組み合わせての使用に適した**SQLDriverConnect**、別の接続を確立するために SQL_DRIVER_NOPROMPT オプションを使用します。 完全な接続文字列は、別の呼び出しでは使用できません**SQLBrowseConnect**、ただし; 場合**SQLBrowseConnect**全体、もう一度呼び出された呼び出しのシーケンスが繰り返される必要があります。  
  
 **SQLBrowseConnect**参照プロセス; など、無効なパスワードまたはアプリケーションによって提供される属性のキーワードの中に回復可能な致命的でないエラーがある場合にも SQL_NEED_DATA を返します。 SQL_NEED_DATA が返されますと参照の結果の接続文字列は、エラーが発生した変更されずと、アプリケーションが呼び出すことができます**SQLGetDiagRec**参照時エラーの SQLSTATE を返す。 これにより、アプリケーションを属性を修正し、参照を続行できます。  
  
 アプリケーションは呼び出すことで、いつでも参照プロセスを終了することができます**SQLDisconnect**します。 ドライバーがすべて未処理の接続を終了し、接続されていない状態に戻されます。  
  
 非同期操作が、接続ハンドルの有効な場合**SQLBrowseConnect** SQL_STILL_EXECUTING が返すも可能性があります。 SQL_NEED_DATA が返されると、アプリケーションを使用する必要があります**SQLDisconnect**参照プロセスをキャンセルします。 場合**SQLBrowseConnect**返します SQL_STILL_EXECUTING、アプリケーションを使用する必要があります**SQLCancelHandle**進行中の操作をキャンセルします。 呼び出す**SQLCancelHandle**後、影響を与えません SQL_NEED_DATA を返します。  
  
 詳細については、次を参照してください。 [SQLBrowseConnect による接続](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)します。  
  
 ドライバーをサポートしている場合**SQLBrowseConnect**、キーワード」のドライバー、ドライバーのシステム情報を含める必要があります、 **ConnectFunctions**キーワードと 3 番目の文字"Y"に設定。  
  
## <a name="code-example"></a>コード例  
  
> [!NOTE]  
>  指定する必要があります Windows 認証をサポートするデータ ソース プロバイダーに接続するかどうか、`Trusted_Connection=yes`接続文字列でユーザー ID とパスワードの情報の代わりにします。  
  
 次の例では、アプリケーションが呼び出す**SQLBrowseConnect**繰り返し。 毎回**SQLBrowseConnect** 、SQL_NEED_DATA が返さで必要なデータに関する情報を渡す\* *OutConnectionString*します。 アプリケーション パス*OutConnectionString* 、ルーチンに**GetUserInput** (示されていません)。 **GetUserInput**情報を解析、ビルドし、ダイアログ ボックスを表示およびでユーザーが入力した情報を返します\* *InConnectionString*します。 アプリケーションでは、ユーザーの情報を渡すには、次の呼び出しにドライバー **SQLBrowseConnect**します。 アプリケーションには、ドライバーのデータ ソースへの接続をすべての必要な情報が提供された後に**SQLBrowseConnect** SQL_SUCCESS を返し、アプリケーションが続行されます。  
  
 呼び出すことによって、SQL Server ドライバーへの接続の詳細な例については**SQLBrowseConnect**を参照してください[SQL Server の参照例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)します。  
  
 たとえば、Sales のソースをデータに接続するに次の操作があります。 最初に、アプリケーションに渡す次の文字列を**SQLBrowseConnect**:  
  
```  
"DSN=Sales"  
```  
  
 ドライバー マネージャーは、Sales データ ソースに関連付けられているドライバーを読み込みます。 これを呼び出してドライバーの**SQLBrowseConnect**アプリケーションから受信したのと同じ引数を持つ関数です。 ドライバーでは、次の文字列を返します **OutConnectionString*:  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 アプリケーションがこの文字列を渡す、 **GetUserInput** 、日常的なダイアログ ボックスをビルドする赤、青、または緑のサーバーを選択して、ユーザー ID とパスワードを入力するユーザーに確認します。 日常的なパスで、次のユーザーが指定した情報がバックアップ\* *InConnectionString*、アプリケーションに渡します**SQLBrowseConnect**:  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect** Sesame、パスワードを使用して、Smith と赤のサーバーに接続するこの情報を使用して、次の文字列を返します **OutConnectionString*:  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 アプリケーションがこの文字列を渡す、 **GetUserInput** 、日常的なダイアログ ボックスをビルドするデータベースを選択するユーザーに確認します。 ユーザーの選択 empdata とアプリケーション呼び出し**SQLBrowseConnect**この文字列で最後の時刻。  
  
```  
"DATABASE=SalesOrders"  
```  
  
 これは、ドライバーは、データ ソースへの接続が必要な情報の最後の部分**SQLBrowseConnect** SQL_SUCCESS を返します、**OutConnectionString*完全な接続文字列が含まれています。  
  
```cpp  
// SQLBrowseConnect_Function.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define BRWS_LEN 100  
SQLHENV henv;  
SQLHDBC hdbc;  
SQLHSTMT hstmt;  
SQLRETURN retcode;  
SQLCHAR szConnStrIn[BRWS_LEN], szConnStrOut[BRWS_LEN];  
SQLSMALLINT cbConnStrOut;  
  
void GetUserInput(SQLCHAR * szConnStrOut, SQLCHAR * szConnStrIn) {}  
  
int main() {  
   // Allocate the environment handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);        
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
      // Set the version environment attribute.  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
         // Allocate the connection handle.  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            // Call SQLBrowseConnect until it returns a value other than SQL_NEED_DATA   
            // (pass data source name the first time).  If SQL_NEED_DATA is returned, call GetUserInput   
            // (not shown) to build a dialog from the values in szConnStrOut.  The user-supplied values   
            // are returned in szConnStrIn, which is passed in the next call to SQLBrowseConnect.  
  
            strcpy_s((char*)szConnStrIn, _countof(szConnStrIn), "DSN=Sales");  
            do {  
               retcode = SQLBrowseConnect(hdbc, szConnStrIn, SQL_NTS,  
                  szConnStrOut, BRWS_LEN, &cbConnStrOut);  
               if (retcode == SQL_NEED_DATA)  
                  GetUserInput(szConnStrOut, szConnStrIn);  
            } while (retcode == SQL_NEED_DATA);  
  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
               // Allocate the statement handle.  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                  // Process data after successful connection  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               SQLDisconnect(hdbc);  
            }  
         }  
         SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
      }  
   }  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|解決方法|  
|---------------------------|---------|  
|接続ハンドルの割り当てください。|[SQLAllocHandle 関数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|データ ソースへの接続|[SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|データ ソースからの切断|[SQLDisconnect 関数](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|接続文字列またはダイアログ ボックスを使用してデータ ソースへの接続|[SQLDriverConnect 関数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|ドライバーの説明と属性を返す|[SQLDrivers 関数](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|接続ハンドルの解放|[SQLFreeHandle 関数](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
