---
title: SQLConnect 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConnect
helpviewer_keywords:
- SQLConnect function [ODBC]
ms.assetid: 59075e46-a0ca-47bf-972a-367b08bb518d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b1c0b20fed0e6c15fef76b1bcbebc98edd37cfbc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121459"
---
# <a name="sqlconnect-function"></a>SQLConnect 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。ISO 92  
  
 **まとめ**  
 **SQLConnect**ドライバーとデータ ソースへの接続を確立します。 接続ハンドルの状態、トランザクションの状態、およびエラー情報を含む、データ ソースへの接続に関するすべての情報のストレージを参照します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLConnect(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      ServerName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      UserName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      Authentication,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>引数  
 *ConnectionHandle*  
 [入力] 接続ハンドル。  
  
 *ServerName*  
 [入力]データ ソースの名前。 データをプログラムと同じコンピューター上またはネットワーク上のどこか別のコンピューター上にあることがあります。 アプリケーションがデータ ソースを選択する方法については、次を参照してください。[データ ソースまたはドライバーを選択する](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)します。  
  
 *NameLength1*  
 [入力]長さ **ServerName*文字数。  
  
 *UserName*  
 [入力]ユーザーの識別子です。  
  
 *NameLength2*  
 [入力]長さ **UserName*文字数。  
  
 *\[認証]*  
 [入力]認証の文字列 (通常はパスワード)。  
  
 *NameLength3*  
 [入力]長さ **認証*文字数。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE、または SQL_STILL_EXECUTING します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLConnect** SQL_ERROR または SQL_SUCCESS_WITH_INFO、関連付けられている SQLSTATE 値を返しますを呼び出すことによって取得できる**SQLGetDiagRec**で、 *HandleType* sql _ のHANDLE_DBC と*処理*の*ConnectionHandle*します。 次の表に、によって返される通常の SQLSTATE 値**SQLConnect** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|ドライバー固有の情報メッセージです。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01S02|オプション値が変更されました|ドライバーでは、指定した値はサポートされていませんでした、 *ValuePtr*引数**SQLSetConnectAttr**のような値を置き換えるとします。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|08001|クライアント接続を確立できません。|ドライバーは、データ ソースとの接続を確立できませんでした。|  
|08002|使用されている接続名|(DM)、指定した*ConnectionHandle*を確立、データ ソースとの接続と、接続がまだ開かれていたか、ユーザーの接続の参照が既に使用されている必要があります。|  
|08004|サーバー接続を拒否しました|データ ソースには、実装定義上の理由から、接続の確立が拒否されます。|  
|08S01|通信リンク エラー|関数が完了した処理の前に、ドライバーとの接続に、ドライバーにしようとしたが、データ ソース間の通信リンクに失敗しました。|  
|28000|無効な認証指定|引数が指定された値*UserName*または引数が指定された値*認証*データ ソースで定義されている制約に違反します。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|(DM)、ドライバー マネージャーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY008|操作が取り消されました|非同期処理が有効に、 *ConnectionHandle*します。 **SQLConnect**関数が呼び出され、実行を完了する前に[SQLCancelHandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)が呼び出されて、 *ConnectionHandle*、およびし**SQLConnect**で関数が再度呼び出されました、 *ConnectionHandle*します。<br /><br /> また、 **SQLConnect**関数が呼び出された、および前に、実行を完了**SQLCancelHandle**が呼び出されて、 *ConnectionHandle*から別のスレッドで、マルチ スレッド アプリケーションです。|  
|HY010|関数のシーケンス エラー|(DM) を非同期的に実行中の関数 (いないこの"1") が呼び出された、 *ConnectionHandle*この関数が呼び出されたときに実行されているとします。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|引数に指定された (DM) 値*NameLength1*、 *NameLength2*、または*NameLength3* SQL_NTS 等しくもありませんが、0 より小さいをでした。<br /><br /> 引数に指定された (DM) 値*NameLength1*データ ソース名の最大長を超えています。|  
|HYT00|タイムアウトが発生しました|クエリのタイムアウト期間は、完了したデータ ソースに接続する前に有効期限が切れました。 によって、タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_LOGIN_TIMEOUT します。|  
|HY114|ドライバーは接続レベルの非同期関数の実行をサポートしていません|(DM)、アプリケーションでは、接続を確立する前に、接続ハンドルでの非同期操作を有効になります。 ただし、ドライバーは接続ハンドルで非同期操作をサポートしていません。|  
|HYT01|接続がタイムアウトしました|データ ソースが要求に応答する前に、接続のタイムアウト期間が終了しました。 によって、接続タイムアウト期間が設定されます**SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT します。|  
|IM001|ドライバーでは、この関数はサポートされていません|(DM) データ ソース名で指定されたドライバーは、関数をサポートしていません。|  
|IM002|データ ソースが見つかりませんと指定された既定のドライバー|(DM)、データ ソース名が、引数で指定された*ServerName*システム情報 で見つからなかったも既定ドライバーの仕様がありました。|  
|IM003|指定されたドライバーに接続できませんでした。|(DM) データで、ドライバーが表示されているシステム情報のソースの仕様が見つからなかったか、でしたに接続されていないその他の何らかの理由。|  
|IM004|Sql_handle_env としてドライバーの SQLAllocHandle に失敗しました|(DM) 中に**SQLConnect**、ドライバー マネージャーという、ドライバーの**SQLAllocHandle**関数と、 *HandleType* sql_handle_env としてとドライバーのエラーが返されました。|  
|IM005|Sql_handle_dbc としてドライバーの SQLAllocHandle に失敗しました|(DM) 中に**SQLConnect**、ドライバー マネージャーという、ドライバーの**SQLAllocHandle**関数と、 *HandleType*ドライバー sql_handle_dbc としてのエラーが返されました。|  
|IM006|ドライバーの SQLSetConnectAttr できませんでした。|中に**SQLConnect**、ドライバー マネージャーという、ドライバーの**SQLSetConnectAttr**関数と、ドライバーにエラーが返されます。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|IM009|トランスレーター DLL に接続できません。|ドライバーは、変換、データ ソースの指定された DLL への接続にできませんでした。|  
|IM010|データ ソース名が長すぎます|(DM)  *\*ServerName* SQL_MAX_DSN_LENGTH 文字を超えていました。|  
|IM014|指定された DSN には、ドライバーとアプリケーション間のアーキテクチャの不一致が含まれています。|64 ビット ドライバー; に接続する DSN を使用する (DM) 32 ビット アプリケーションまたはその逆です。|  
|IM015|ドライバーの SQLConnect SQL_HANDLE_DBC_INFO_HANDLE に失敗しました|ドライバーでは、SQL_ERROR が返された場合は、ドライバー マネージャーは、アプリケーションに SQL_ERROR を返し、接続は失敗します。<br /><br /> SQL_HANDLE_DBC_INFO_TOKEN の詳細については、次を参照してください。 [ODBC ドライバーで接続プールの認識を開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)します。|  
|IM017|非同期通知モードでのポーリングは無効です。|通知のモデルを使用すると、常にポーリングは無効です。|  
|IM018|**SQLCompleteAsync**このハンドルに対する前の非同期操作を完了が呼び出されていません。|通知モードが有効になっている場合、ハンドルでは、前の関数呼び出しに SQL_STILL_EXECUTING が返された場合と**SQLCompleteAsync**後処理を行い、操作を完了するハンドルで呼び出す必要があります。|  
|S1118|ドライバーが非同期通知をサポートしていません|ドライバーが非同期通知をサポートしていない場合、SQL_ATTR_ASYNC_DBC_EVENT または SQL_ATTR_ASYNC_DBC_RETCODE_PTR を設定することはできません。|  
  
## <a name="comments"></a>コメント  
 アプリケーションを使用する理由について**SQLConnect**を参照してください[SQLConnect による接続](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)します。  
  
 ドライバー マネージャーでは、アプリケーションは、関数を呼び出すまで、ドライバーに接続しません (**SQLConnect**、 **SQLDriverConnect**、または**SQLBrowseConnect**) に接続するため、ドライバー。 その時点まで、ドライバー マネージャーは、独自の処理と連携し、接続情報を管理します。 指定したかどうかをドライバーに現在接続されているアプリケーションが接続関数を呼び出すと、ドライバー マネージャーを確認します*ConnectionHandle*:  
  
-   ドライバー マネージャーは、ドライバーと呼び出しに接続するドライバーが接続されていない場合**SQLAllocHandle**で、 *HandleType* sql_handle_env としての**SQLAllocHandle**で、*HandleType* sql_handle_dbc としての**SQLSetConnectAttr** (かどうか、アプリケーション指定された任意の接続属性)、およびドライバーの接続関数。 ドライバー マネージャーは、SQLSTATE IM006 を返します (ドライバーの**SQLSetConnectOption**に失敗しました) と接続関数の場合は、ドライバーのエラーを返しました SQL_SUCCESS_WITH_INFO **SQLSetConnectAttr**します。 詳細については、次を参照してください。[データ ソースまたはドライバーに接続する](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)します。  
  
-   指定されたドライバーをオンに既に接続されている場合、 *ConnectionHandle*、ドライバー マネージャーがドライバーの接続関数のみを呼び出します。 この場合、ドライバーがすべての接続の属性を確認してくださいに行う必要があります、 *ConnectionHandle*現在の設定を維持します。  
  
-   ドライバー マネージャーを呼び出す場合に、別のドライバーは接続されている、 **SQLFreeHandle**で、 *HandleType* sql_handle_dbc としての次に、その他のドライバーがその環境に接続されていない、呼び出しますと**SQLFreeHandle**で、 *HandleType* sql_handle_env として接続されているドライバーの後、そのドライバーを切断します。 ドライバーに接続されていない場合と同じ操作を実行します。  
  
 ドライバーは、ハンドルの割り当てし、自体を初期化します。  
  
 アプリケーションを呼び出すと**SQLDisconnect**、ドライバー マネージャー呼び出し**SQLDisconnect**ドライバー。 ただし、ドライバーは切断されません。 これにより、繰り返しに接続し、データ ソースから切断するアプリケーションのメモリのドライバーが維持されます。 アプリケーションを呼び出すと**SQLFreeHandle**で、 *HandleType*ドライバー マネージャーを呼び出し、sql_handle_dbc としての**SQLFreeHandle**で、 *HandleType* sql_handle_dbc としてのし**SQLFreeHandle**で、 *HandleType* driver では、sql_handle_env としての接続を切断し、ドライバーと。  
  
 ODBC アプリケーションでは、1 つ以上の接続を確立できます。  
  
## <a name="driver-manager-guidelines"></a>ドライバー マネージャーのガイドライン  
 内容 **ServerName*ドライバー マネージャーとドライバーがどのように連携してデータ ソースへの接続を確立するには影響します。  
  
-   場合\* *ServerName*有効なデータ ソース名を含むドライバー マネージャーのシステム情報に対応するデータ ソースの指定を検索して、関連するドライバーに接続します。 ドライバー マネージャーに渡す各**SQLConnect**ドライバーへの引数。  
  
-   データ ソース名が見つからない場合、または*ServerName* null ポインターの場合は、ドライバー マネージャーの既定のデータ ソースの仕様を検索して、関連するドライバーに接続します。 ドライバー マネージャーがドライバーに渡します、 *UserName*と*認証*未変更の状態で引数との"DEFAULT"、 *ServerName*引数。  
  
-   場合、 *ServerName*引数が"DEFAULT"、ドライバー マネージャーの既定のデータ ソースの仕様を検索して、関連するドライバーに接続します。 ドライバー マネージャーに渡す各**SQLConnect**ドライバーへの引数。  
  
-   データ ソース名が見つからない場合、または*ServerName*は null ポインターの場合、既定のデータ ソースの指定がない場合は、ドライバー マネージャーは、SQLSTATE IM002 SQL_ERROR を返します (データ ソースが見つかりません名前と既定値はありません。指定されたドライバー)。  
  
 接続されているドライバー マネージャーによって後、ドライバーはシステム情報内でその対応するデータ ソースの仕様を検索し、仕様からドライバー固有の情報を使用して、必要な接続情報のセットを完了します。  
  
 データ ソースのシステム情報の既定のライブラリは翻訳が指定されている場合、ドライバーは、それに接続します。 呼び出すことによって、別の翻訳ライブラリに接続できる**SQLSetConnectAttr** SQL_ATTR_TRANSLATE_LIB 属性を持つ。 呼び出して変換オプションを指定できます**SQLSetConnectAttr** SQL_ATTR_TRANSLATE_OPTION 属性を持つ。  
  
 ドライバーをサポートしている場合**SQLConnect**、システム情報、ドライバーのドライバー キーワード セクションを含める必要があります、 **ConnectFunctions**キーワードの最初の文字"Y"に設定。  
  
### <a name="connection-pooling"></a>接続のプール  
 接続プールでは既に作成されている接続を再利用するアプリケーション。 接続プールが有効にすると、 **SQLConnect**を呼び出すと、ドライバー マネージャーの接続プールが指定されている環境で接続プールの一部である接続を使用して接続を確立しよう。 この環境は、プール内の接続を使用するすべてのアプリケーションで使用される共有環境です。  
  
 接続プールが有効になって、環境が呼び出すことによって割り当てられた**SQLSetEnvAttr** SQL_CP_ONE_PER_DRIVER (元のドライバーごとに 1 つのプールの最大数を指定) または SQL_CP_ONE_PER_HENV SQL_ATTR_CONNECTION_POOLING に設定するには(環境ごとに 1 つのプールの最大数を指定します。) **SQLSetEnvAttr**ここで使用して呼び出した*EnvironmentHandle*属性は、プロセス レベルの属性が null に設定します。 SQL_ATTR_CONNECTION_POOLING を SQL_CP_OFF に設定すると、接続プールは無効になります。  
  
 接続プールが有効になったら、 **SQLAllocHandle**で、 *HandleType*環境を割り当てる sql_handle_env としてが呼び出されます。 この呼び出しによって割り当てられた環境は、接続プールが有効になっているために、共有環境です。 ただし、使用される環境はまで決まりません**SQLAllocHandle**で、 *HandleType* sql_handle_dbc としてが呼び出されます。  
  
 **SQLAllocHandle**で、 *HandleType* sql_handle_dbc としては、接続の割り当てに呼び出されます。 ドライバー マネージャーは、アプリケーションによって設定された環境属性に一致する既存の共有環境を見つけようとします。 このような環境が存在しない場合、暗黙の型として作成されます*共有環境*します。 一致する共有環境が見つかった場合は、環境ハンドルは、アプリケーションに返され、参照カウントがインクリメントされます。  
  
 ただし、使用される接続はまで決まりません**SQLConnect**が呼び出されます。 その時点では、ドライバー マネージャーは、アプリケーションによって要求された条件に一致する接続プール内の既存の接続を見つけようとします。 これらの基準への呼び出しで要求された接続オプションを含める**SQLConnect** (の値、 *ServerName*、 *UserName*、および*認証*キーワード) ため、任意の接続属性セットと**SQLAllocHandle**で、 *HandleType* sql_handle_dbc としてが呼び出されました。 ドライバー マネージャーは、対応する接続キーワードと、プール内の接続での属性に対してこれらの条件を確認します。 一致が見つかった場合は、プール内の接続が使用されます。 一致が検出されない場合は、新しい接続が作成されます。  
  
 SQL_ATTR_CP_MATCH 環境属性が SQL_CP_STRICT_MATCH に設定されている場合、一致が使用するプール内の接続の正確な場合があります。 SQL_ATTR_CP_MATCH 環境属性が SQL_CP_RELAXED_MATCH に設定されている場合、接続オプションへの呼び出し**SQLConnect**一致がないすべての接続属性する必要がありますに一致する必要があります。  
  
 次のルールが前に、アプリケーションによって設定されたときに、接続属性を適用は**SQLConnect**を呼び出すと、プール内の接続の接続属性と一致しません。  
  
-   場合は、接続が行われる前に、接続属性を設定する必要があります。  
  
     SQL_ATTR_CP_MATCH が SQL_CP_STRICT_MATCH の場合は、SQL_ATTR_PACKET_SIZE プールされた接続では、アプリケーションによって設定された属性と同じである必要があります。 別の SQL_CP_RELAXED_MATCH、SQL_ATTR_PACKET_SIZE の値を使用できます。 場合、  
  
     SQL_ATTR_LOGIN_VALUE の値は、一致には影響しません。  
  
-   接続の確立後または前に、接続属性を設定できます。 場合、  
  
     接続属性は、アプリケーションが設定されていませんが、プール内の接続が設定されている場合、既定値は、プールされた接続で接続の属性は、既定値に戻してし、一致するものは宣言されています。 既定値がない場合は、プールされた接続には一致するものはありません。  
  
     接続属性が、アプリケーションによって設定されている、プール内の接続に設定されていない場合は、プールの接続属性は、アプリケーションがそのセットに変更され、一致するものは宣言されています。  
  
     接続属性が、アプリケーションで設定されているし、プール内の接続に設定されても、値が異なる場合は、アプリケーションの接続属性の値を使用し、一致が宣言されています。  
  
-   ドライバー固有の接続属性の値が同一でない SQL_ATTR_CP_MATCH が SQL_CP_STRICT_MATCH に設定されている場合は、プール内の接続は使用されません。  
  
 アプリケーションを呼び出すと**SQLDisconnect**切断するには、接続が接続プールに返され、再利用できます。  
  
### <a name="optimizing-connection-pooling-performance"></a>接続プールのパフォーマンスを最適化します。  
 分散トランザクションが関与すると、接続を使用してプールのパフォーマンスを最適化することは**SQL_DTC_TRANSITION_COST**、SQLUINTEGER ビットマスクであります。 呼ばれる遷移は、接続属性に 0 以外の場合、値 0 から移動 SQL_ATTR_ENLIST_IN_DTC の遷移、またはその逆です。 これからの接続は、分散トランザクションに参加しているいませんは、分散トランザクションでは、その逆に参加しています。 どのドライバー (設定の接続属性 SQL_ATTR_ENLIST_IN_DTC) の参加の実装が、によってそれらの遷移は高価な場合があり、最適なパフォーマンスは避ける必要がありますので。  
  
 ドライバーによって返される値には、次のビットの任意の組み合わせが含まれています。  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**ときに、設定、0 以外の遷移にゼロが 0 以外の値から別の 0 以外の値 (次のトランザクションで以前に参加している接続の参加) への移行よりも大幅に高くことを意味します。  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**ときに、設定、SQL_ATTR_ENLIST_IN_DTC 属性を持つが、既に 0 に設定の接続を使用するよりも大幅に高く、0 個の遷移を 0 以外のことを意味します。  
  
 これは、接続の使用状況のトレードオフとパフォーマンスです。 ドライバーは、1 つ以上のこれらの遷移が高価なことを示している場合、ドライバー マネージャーの接続プーラーはプールにより多くの接続を維持することでこれに応答します。 接続プール内の一部に非トランザクションの使用に適しているし、トランザクションの使用に適したいくつか。 ただし場合は、ドライバーは、これらの遷移が高価ないないことを示します、接続数を使用できます、おそらくの非トランザクションとトランザクションの使用の間で切り替えます。  
  
 SQL_ATTR_ENLIST_IN_DTC をサポートしていないドライバーは、SQL_DTC_TRANSITION_COST をサポートする必要はありません。 SQL_ATTR_ENLIST_IN_DTC がない SQL_DTC_TRANSITION_COST をサポートするドライバー、遷移がドライバーにはこの値を 0 (ビットが設定されていない) が返される場合、高価ないないことを前提とします。  
  
 ただし、SQL_DTC_TRANSITION_COST は、ODBC 3.5 では、ODBC 2 で導入されました。*x*ドライバーもサポートできますが、ドライバー マネージャーがドライバーのバージョンに関係なく、この情報にクエリを実行しているためです。  
  
### <a name="code-example"></a>コード例  
 次の例では、アプリケーションを割り当てる環境と接続ハンドル。 ユーザー ID ジョンズ SalesOrders データ ソースとパスワード Sesame に接続し、データを処理します。 データの処理が完了したら、データ ソースから切断し、ハンドルを解放します。  
  
```cpp  
// SQLConnect_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR * OutConnStr = (SQLCHAR * )malloc(255);  
   SQLSMALLINT * OutConnStrLen = (SQLSMALLINT *)malloc(255);  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLCHAR*) "NorthWind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
### <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|ハンドルの割り当てください。|[SQLAllocHandle 関数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|検出およびデータ ソースに接続するために必要な値を列挙します。|[SQLBrowseConnect 関数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|データ ソースからの切断|[SQLDisconnect 関数](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|接続文字列またはダイアログ ボックスを使用してデータ ソースへの接続|[SQLDriverConnect 関数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|接続属性の設定を返す|[SQLGetConnectAttr 関数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|接続属性の設定|[SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
