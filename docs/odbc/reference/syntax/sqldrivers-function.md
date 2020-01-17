---
title: SQLDrivers 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDrivers
helpviewer_keywords:
- SQLDrivers function [ODBC]
ms.assetid: 6b5b7514-e9cb-4cfd-8b7a-ab51dfab9efa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f54be3d11f4870533513f464c1afdae13e04f367
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104663"
---
# <a name="sqldrivers-function"></a>SQLDrivers 関数
**準拠**  
 バージョンが導入されました。ODBC 2.0 の規格に準拠します。ODBC  
  
 **まとめ**  
 **SQLDrivers**ドライバーの説明とドライバー属性のキーワードを示します。 この関数は、ドライバー マネージャーによってのみ実装されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLDrivers(  
     SQLHENV         EnvironmentHandle,  
     SQLUSMALLINT    Direction,  
     SQLCHAR *       DriverDescription,  
     SQLSMALLINT     BufferLength1,  
     SQLSMALLINT *   DescriptionLengthPtr,  
     SQLCHAR *       DriverAttributes,  
     SQLSMALLINT     BufferLength2,  
     SQLSMALLINT *   AttributesLengthPtr);  
```  
  
## <a name="arguments"></a>引数  
 *EnvironmentHandle*  
 [入力]環境ハンドル。  
  
 *[方向]*  
 [入力]ドライバー マネージャーが次のドライバー記述リスト (SQL_FETCH_NEXT) または (SQL_FETCH_FIRST) リストの先頭から検索を開始するかどうかをフェッチするかどうかを判断します。  
  
 *DriverDescription*  
 [出力]ドライバーの説明を返すバッファーへのポインター。  
  
 場合*DriverDescription*が null の場合、 *DescriptionLengthPtr*はまだ文字 (文字データの null 終端文字を除く) の合計数を返しますで返される使用可能なによって示されるバッファー *DriverDescription*します。  
  
 *BufferLength1*  
 [入力]長さ、**DriverDescription*文字のバッファー。  
  
 *DescriptionLengthPtr*  
 [出力]文字 (null 終了文字を除く) の合計数を返すバッファーへのポインターで返される使用可能な\* *DriverDescription*します。 返すに使用できる文字数がより大きいかに等しい場合*BufferLength1*、ドライバーの説明で\* *DriverDescription*に切り捨てられます*BufferLength1* null 終了文字の長さマイナスです。  
  
 *DriverAttributes*  
 [出力]ドライバー (「コメント」を参照してください) 属性値のペアの一覧を返すバッファーへのポインター。  
  
 場合*DriverAttributes*が null の場合、 *AttributesLengthPtr*はバイト (文字データの null 終端文字を除く) の合計数を返しますが、バッファーに返される使用可能な指す*DriverAttributes*します。  
  
 *BufferLength2*  
 [入力]長さ、 \* *DriverAttributes*文字のバッファー。 場合、  *\*DriverDescription*値は、Unicode 文字列 (呼び出し時に**SQLDriversW**)、 *BufferLength*引数は偶数である必要があります。  
  
 *AttributesLengthPtr*  
 [出力] (Null 終了バイトを除く) バイトの合計数を返すバッファーへのポインターで返される使用可能な\* *DriverAttributes*します。 返される使用可能なバイト数がより大きいかに等しい場合*BufferLength2*、属性値のペアの一覧\* *DriverAttributes*に切り捨てられます*BufferLength2* null 終了文字の長さマイナスです。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLDrivers** SQL_ERROR または SQL_SUCCESS_WITH_INFO のいずれかを返します呼び出すことによって、関連付けられた SQLSTATE 値を取得できる**SQLGetDiagRec**で、 *HandleType*のSql_handle_env として、*処理*の*EnvironmentHandle*します。 次の表に、によって返される通常の SQLSTATE 値**SQLDrivers** ; この関数のコンテキストでそれぞれについて説明しますと表記"(DM)"の前にドライバー マネージャーによって返されるについての説明。 SQLSTATE 値ごとに関連付けられているリターン コードは明記しない限り、SQL_ERROR です。  
  
|SQLSTATE|[エラー]|説明|  
|--------------|-----------|-----------------|  
|01000|一般的な警告|(DM) ドライバー マネージャーに固有の情報メッセージ。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|01004|文字列データで、右側が切り捨てられました|(DM) バッファー \* *DriverDescription*を完全なドライバーの説明を返すのに十分な大きさがありません。 そのため、説明が切り捨てられました。 完全なドライバーの説明の長さが返される\* *DescriptionLengthPtr*します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。<br /><br /> (DM) バッファー \* *DriverAttributes*属性値のペアの完全な一覧を返すのに十分な大きさがありません。 そのため、一覧が切り捨てられました。 属性値のペアの切り詰められていない一覧の長さが返される **AttributesLengthPtr*します。 (関数は、SQL_SUCCESS_WITH_INFO を返します)。|  
|HY000|一般的なエラー|これがなかった固有の SQLSTATE とする実装に固有の SQLSTATE が定義されていない、エラーが発生しました。 によって返されるエラー メッセージ**SQLGetDiagRec**で、  *\*MessageText*バッファーは、エラーとその原因について説明します。|  
|HY001|メモリの割り当てエラー|(DM)、ドライバー マネージャーは、実行または関数の完了をサポートするために必要なメモリを割り当てることができませんでした。|  
|HY010|関数のシーケンス エラー|(DM) **SQLExecute**、 **SQLExecDirect**、または**SQLMoreResults**に対して呼び出された、 *StatementHandle* SQL_PARAM_DATA_ を返されます。ご利用いただけます。 ストリームのすべてのパラメーターのデータが取得される前に、この関数が呼び出されました。|  
|HY013|メモリ管理エラー|基になるメモリ オブジェクトにアクセスできませんでした、場合によってメモリ不足が原因であるために、関数呼び出しを処理できませんでした。|  
|HY090|文字列またはバッファーの長さが無効です。|引数に指定された (DM) 値*BufferLength1*が 0 未満でした。<br /><br /> 引数に指定された (DM) 値*BufferLength2*が 0 未満か、1 にします。|  
|HY103|無効な取得コード|引数に指定された値 (DM)*方向*SQL_FETCH_FIRST または SQL_FETCH_NEXT でした。|  
|HY117|不明なトランザクションの状態のため、接続が中断されます。 のみを切断して、読み取り専用の関数が許可されます。|(DM) 中断状態の詳細については、次を参照してください。 [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)します。|  
  
## <a name="comments"></a>コメント  
 **SQLDrivers**でドライバーの説明を返します、 \* *DriverDescription*バッファー。 ドライバーに関する追加情報が返されます、 \* *DriverAttributes*キーワードと値のペアのリストとしてのバッファー。 すべてのキーワードに一覧されたシステム情報を除き、すべてのドライバーのドライバーが返される**CreateDSN**、データ ソースの作成が要求するために使用してはそのため、省略可能です。 各ペアは、null バイトで終了し、完全な一覧が null のバイトで終了しました (つまり、2 つの null バイトがリストの末尾をマークする)。 たとえば、C# の構文を使用して、ファイル ベースのドライバーでは、次の属性 (「\0」は、null 文字を表します) の一覧を返す可能性があります。  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 場合\* *DriverAttributes*が十分に大きくないリスト全体を保持するために、リストが切り詰め、 **SQLDrivers** SQLSTATE 01004 (データは切り捨てられます)、およびリストの長さを返します (を除く、最後の null 終端バイト) が返される **AttributesLengthPtr*します。  
  
 ドライバーがインストールされている場合、システムの情報からドライバー属性のキーワードが追加されます。 詳細については、次を参照してください。 [ODBC コンポーネントをインストール](../../../odbc/reference/install/installing-odbc-components.md)します。  
  
 アプリケーションが呼び出すことができます**SQLDrivers**すべてのドライバーの説明の取得を複数回です。 ドライバー マネージャーは、システム情報からこの情報を取得します。 ない複数のドライバーの説明がある場合に**SQLDrivers** sql_no_data が返されます。 場合**SQLDrivers**は、最初のドライバーの説明を返します SQL_NO_DATA が返された後すぐに SQL_FETCH_NEXT で呼び出されます。 アプリケーションがによって返される情報を使用する方法については**SQLDrivers**を参照してください[データ ソースまたはドライバーを選択する](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)します。  
  
 SQL_FETCH_NEXT が渡された場合**SQLDrivers**呼び出されると、非常に最初に**SQLDrivers**最初のデータ ソース名を取得します。  
  
 **SQLDrivers**は実装されてドライバー マネージャーでの特定のドライバーの標準への準拠に関係なくすべてのドライバーでサポートされています。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|検出とデータ ソースに接続するために必要な値を一覧表示します。|[SQLBrowseConnect 関数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|データ ソースへの接続|[SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|データ ソース名を返す|[SQLDataSources 関数](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|接続文字列またはダイアログ ボックスを使用してデータ ソースへの接続|[SQLDriverConnect 関数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
