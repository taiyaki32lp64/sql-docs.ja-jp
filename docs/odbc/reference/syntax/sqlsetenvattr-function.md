---
title: SQLSetEnvAttr 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetEnvAttr
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetEnvAttr
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC]
ms.assetid: 0343241c-4b15-4d4b-aa2b-2e8ab5215cd2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b69b08a5004252f9016fbc616e9198179db31fb1
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343082"
---
# <a name="sqlsetenvattr-function"></a>SQLSetEnvAttr 関数
**互換性**  
 導入されたバージョン:ODBC 3.0 標準準拠:ISO 92  
  
 **まとめ**  
 **SQLSetEnvAttr**は、環境の側面を管理する属性を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLSetEnvAttr(  
     SQLHENV      EnvironmentHandle,  
     SQLINTEGER   Attribute,  
     SQLPOINTER   ValuePtr,  
     SQLINTEGER   StringLength);  
```  
  
## <a name="arguments"></a>引数  
 *EnvironmentHandle*  
 代入環境ハンドル。  
  
 *属性*  
 代入設定する属性。 "Comments" に記載されています。  
  
 *ValuePtr*  
 代入*属性*に関連付けられる値へのポインター。 *属性*の値に応じて、 *valueptr*は32ビット整数値になるか、null で終わる文字列を指します。  
  
 *StringLength*  
 代入*Valueptr*が文字列またはバイナリバッファーを指している場合、この引数は **valueptr*の長さである必要があります。 文字列データの場合、この引数には文字列のバイト数を含める必要があります。  
  
 *Valueptr*が整数の場合、 *stringlength*は無視されます。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLSetEnvAttr**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返す場合は、 *handletype* SQL_HANDLE_ENV と*EnvironmentHandle*の*ハンドル*を指定して**SQLGetDiagRec**を呼び出すことによって、関連付けられた SQLSTATE 値を取得できます。 次の表に、 **SQLSetEnvAttr**によって通常返される SQLSTATE 値と、この関数のコンテキストでのそれぞれについて説明します。"(DM)" という表記は、ドライバーマネージャーによって返される SQLSTATEs の説明の前にあります。 特に記載がない限り、各 SQLSTATE 値に関連付けられているリターンコードは SQL_ERROR です。 ドライバーで環境属性がサポートされていない場合、接続時にのみエラーが返されることがあります。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般警告|ドライバー固有の情報メッセージ。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|01S02|オプションの値が変更されました|ドライバーは、 *Valueptr*に指定された値をサポートしておらず、同様の値に置き換えられました。 (関数は SQL_SUCCESS_WITH_INFO を返します)。|  
|HY000|一般エラー|特定の SQLSTATE がなく、実装固有の SQLSTATE が定義されていないエラーが発生しました。 Messagetext バッファーの**SQLGetDiagRec によっ**て返されるエラーメッセージには、エラーとその原因が記述されています。  *\**|  
|HY001|メモリ割り当てエラー|ドライバーは、関数の実行または完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY009|Null ポインターの使い方が正しくありません|属性引数が文字列値を必要とし、 *Valueptr*引数が null ポインターである環境属性を識別しました。|  
|HY010|関数のシーケンスエラー|(DM) *EnvironmentHandle*で接続ハンドルが割り当てられています。<br /><br /> (DM) **SQL_ATTR_ODBC_VERSION**が**SQLSetEnvAttr**で設定されておらず、*属性*が**SQL_ATTR_ODBC_VERSION**と等しくありません。 **SQLAllocHandleStd**を使用している場合は、 **SQL_ATTR_ODBC_VERSION**を明示的に設定する必要はありません。|  
|HY013|メモリ管理エラー|基になるメモリオブジェクトにアクセスできなかったため、関数呼び出しを処理できませんでした。メモリ不足の状態が原因である可能性があります。|  
|HY024|無効な属性値|指定された*属性*値が指定されている場合、 *valueptr*に無効な値が指定されています。|  
|HY090|文字列またはバッファーの長さが無効です|*Stringlength*引数が0未満ですが、SQL_NTS ませんでした。|  
|HY092|属性またはオプションの識別子が無効です|(DM) 引数*属性*に指定された値は、ドライバーでサポートされている ODBC のバージョンでは無効です。|  
|HY117|トランザクションの状態が不明なため、接続が中断されました。 切断と読み取り専用の機能のみが許可されます。|(DM) 中断状態の詳細については、「 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)」を参照してください。|  
|HYC00|省略可能な機能は実装されていません|引数*属性*に指定された値は、ドライバーでサポートされている odbc のバージョンの有効な odbc 環境属性でしたが、ドライバーではサポートされていませんでした。<br /><br /> (DM)*属性*引数が SQL_ATTR_OUTPUT_NTS、 *VALUEPTR*が SQL_FALSE でした。|  
  
## <a name="comments"></a>コメント  
 アプリケーションは、環境に接続ハンドルが割り当てられていない場合にのみ、 **SQLSetEnvAttr**を呼び出すことができます。 環境に対してアプリケーションによって正常に設定された環境属性はすべて、環境で**Sqlfreehandle**が呼び出されるまで保持されます。 *ODBC 3.x*では、複数の環境ハンドルを同時に割り当てることができます。  
  
 *Valueptr*によって設定される情報の形式は、指定した*属性*によって異なります。 **SQLSetEnvAttr**は、null で終わる文字列または32ビット整数値の2つの異なる形式のいずれかで属性情報を受け取ります。 各の形式は、属性の説明に記載されています。  
  
 ドライバー固有の環境属性はありません。  
  
 **SQLSetEnvAttr**を呼び出すことによって接続属性を設定することはできません。 これを実行しようとすると、SQLSTATE HY092 (無効な属性/オプション識別子) が返されます。  
  
|*属性*|*Valueptr*コンテンツ|  
|-----------------|-------------------------|  
|SQL_ATTR_CONNECTION_POOLING (ODBC 3.8)|環境レベルでの接続プールを有効または無効にする32ビット SQLUINTEGER 値。 次の値が使用されます。<br /><br /> SQL_CP_OFF = 接続プーリングはオフになっています。 既定値です。<br /><br /> SQL_CP_ONE_PER_DRIVER = 各ドライバーで1つの接続プールがサポートされています。 プール内のすべての接続は、1つのドライバーに関連付けられています。<br /><br /> SQL_CP_ONE_PER_HENV = 1 つの接続プールが各環境でサポートされています。 プール内のすべての接続は、1つの環境に関連付けられています。<br /><br /> SQL_CP_DRIVER_AWARE = ドライバーの接続プールの認識機能を使用できる場合は、それを使用します。 ドライバーで接続プールの認識がサポートされていない場合、SQL_CP_DRIVER_AWARE は無視され、SQL_CP_ONE_PER_HENV が使用されます。 詳細については、「[ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)」を参照してください。 一部のドライバーがサポートしていて、一部のドライバーで接続プールの認識がサポートされていない環境では、SQL_CP_DRIVER_AWARE はこれらのサポートドライバーで接続プールの認識機能を有効にすることができますが、これは SQL_CP_ONE_PER_HENV on に設定することと同じです。これらのドライバーは、接続プールの認識機能をサポートしていません。<br /><br /> 接続プールは、 **SQLSetEnvAttr**を呼び出して SQL_ATTR_CONNECTION_POOLING 属性を SQL_CP_ONE_PER_DRIVER または SQL_CP_ONE_PER_HENV に設定することによって有効になります。 この呼び出しは、アプリケーションが接続プールを有効にする共有環境を割り当てる前に行う必要があります。 **SQLSetEnvAttr**の呼び出しの環境ハンドルは null に設定されます。これにより、SQL_ATTR_CONNECTION_POOLING のプロセスレベルの属性が作成されます。 接続プールを有効にした後、アプリケーションは、 *InputHandle*引数を SQL_HANDLE_ENV に設定して**SQLAllocHandle**を呼び出すことによって、暗黙的な共有環境を割り当てます。<br /><br /> 接続プールが有効化され、アプリケーションの共有環境が選択されると、SQL_ATTR_CONNECTION_POOLING は、その環境に対してはリセットできません。これは、設定時に**SQLSetEnvAttr**が null 環境ハンドルで呼び出されるためです。この属性。 共有環境で接続プールが既に有効になっている間にこの属性が設定されている場合、属性は、後で割り当てられた共有環境にのみ影響します。<br /><br /> 環境で接続プールを有効にすることもできます。 環境接続プールについては、次の点に注意してください。<br /><br /> -NULL ハンドルでの接続プールの有効化は、プロセスレベルの属性です。 その後、割り当てられた環境は共有環境になり、プロセスレベルの接続プーリング設定が継承されます。<br />-環境が割り当てられた後も、アプリケーションは接続プールの設定を変更できます。<br />-環境接続プーリングが有効になっていて、接続のドライバーがドライバープーリングを使用している場合、環境プーリングが優先されます。<br /><br /> SQL_ATTR_CONNECTION_POOLING は、ドライバーマネージャー内で実装されます。 ドライバーは SQL_ATTR_CONNECTION_POOLING を実装する必要はありません。 ODBC 2.0 および3.0 アプリケーションでは、この環境属性を設定できます。<br /><br /> 詳細については、「 [ODBC Connection Pooling (ODBC 接続プール)](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)」を参照してください。|  
|SQL_ATTR_CP_MATCH (ODBC 3.0)|接続プールから接続を選択する方法を決定する32ビット SQLUINTEGER 値。 **SQLConnect**または**SQLDriverConnect**が呼び出されると、ドライバーマネージャーによって、プールから再利用される接続が決まります。 ドライバーマネージャーは、呼び出しの接続オプションと、アプリケーションによって設定された接続属性を、プール内の接続のキーワードと接続属性に一致させようとします。 この属性の値によって、一致条件の精度のレベルが決まります。<br /><br /> この属性の値を設定するには、次の値を使用します。<br /><br /> SQL_CP_STRICT_MATCH = 呼び出しの接続オプションと完全に一致する接続のみが、アプリケーションによって設定された接続属性を再利用します。 既定値です。<br /><br /> SQL_CP_RELAXED_MATCH = 一致する接続文字列キーワードを使用した接続を使用できます。 キーワードは一致している必要がありますが、すべての接続属性が一致している必要はありません。<br /><br /> プールされた接続への接続でドライバーマネージャーが照合を実行する方法の詳細については、「 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)」を参照してください。 接続プールの詳細については、「 [ODBC 接続プール](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)」を参照してください。|  
|SQL_ATTR_ODBC_VERSION (ODBC 3.0)|特定の機能*で odbc 2.x*動作また*は odbc 3.x*動作が動作するかどうかを決定する32ビット整数。 この属性の値を設定するには、次の値を使用します。<br /><br /> SQL_OV_ODBC3_80 = ドライバーマネージャーとドライバーは、次の ODBC 3.8 動作を示しています。<br /><br /> -ドライバーは、日付、時刻、およびタイムスタンプの ODBC *3. x*コードを返します。<br />- **SQLError**、 **SQLGetDiagField**、または**SQLGetDiagRec**が呼び出されると、ドライバーは ODBC 3.x コードを返します *。*<br />- **Sqltables**の呼び出しの*CatalogName*引数は、検索パターンを受け入れます。<br />-ドライバーマネージャーは、C データ型の拡張機能をサポートしています。 C データ型の拡張機能の詳細については、「 [ODBC の c データ型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)」を参照してください。<br /><br /> 詳細については、「 [ODBC 3.8 の新機能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)」を参照してください。<br /><br /> SQL_OV_ODBC3 = ドライバーマネージャーとドライバーは、次の ODBC *3. x*動作を示しています。<br /><br /> -ドライバーは、日付、時刻、およびタイムスタンプの ODBC *3. x*コードを返します。<br />- **SQLError**、 **SQLGetDiagField**、または**SQLGetDiagRec**が呼び出されると、ドライバーは ODBC 3.x コードを返します *。*<br />- **Sqltables**の呼び出しの*CatalogName*引数は、検索パターンを受け入れます。<br />-ドライバーマネージャーは、C データ型の拡張機能をサポートしていません。<br /><br /> SQL_OV_ODBC2 = ドライバーマネージャーとドライバーは、次の ODBC *2.x 動作を*示しています。 これは、odbc *2.x アプリケーションで*odbc *2.x ドライバーを*使用する場合に特に便利です。<br /><br /> -ドライバーはを返し、日付、時刻、およびタイムスタンプ*の ODBC 2.x*コードを想定します。<br />- **SQLError**、 **SQLGetDiagField**、または**SQLGetDiagRec**が呼び出されると、ドライバー*は ODBC 2.x*コードを返します。<br />- **Sqltables**の呼び出しの*CatalogName*引数は、検索パターンを受け入れません。<br />-ドライバーマネージャーは、C データ型の拡張機能をサポートしていません。<br /><br /> アプリケーションでは、SQLHENV 引数を持つ関数を呼び出す前に、この環境属性を設定する必要があります。そうしないと、呼び出しによって SQLSTATE HY010 (関数シーケンスエラー) が返されます。 これらの環境フラグに追加の動作が存在するかどうかは、ドライバーによって異なります。<br /><br /> -詳細については、「[アプリケーションの ODBC のバージョン](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)と[動作の変更](../../../odbc/reference/develop-app/behavioral-changes.md)の宣言」を参照してください。|  
|SQL_ATTR_OUTPUT_NTS (ODBC 3.0)|ドライバーが文字列データを返す方法を決定する32ビット整数。 SQL_TRUE の場合、ドライバーは null で終わる文字列データを返します。 SQL_FALSE の場合、ドライバーは null で終わる文字列データを返しません。<br /><br /> この属性の既定値は SQL_TRUE です。 **SQLSetEnvAttr**を呼び出して SQL_TRUE に設定すると、SQL_SUCCESS が返されます。 **SQLSetEnvAttr**を呼び出して SQL_FALSE に設定すると、SQL_ERROR と SQLSTATE HYC00 (省略可能な機能は実装されていません) が返されます。|  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|ハンドルの割り当て|[SQLAllocHandle 関数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|環境属性の設定を返す|[SQLGetEnvAttr 関数](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダーファイル](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 3.8 の新機能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
