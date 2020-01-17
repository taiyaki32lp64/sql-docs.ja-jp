---
title: ConfigDSN 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDSN
helpviewer_keywords:
- ConfigDSN [ODBC]
ms.assetid: 01ced74e-c575-4a25-83f5-bd7d918123f8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 21a02107359b26c0dc30aa87acbf46c1ab1a172d
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892849"
---
# <a name="configdsn-function"></a>ConfigDSN 関数
**互換性**  
 導入されたバージョン:ODBC 1.0  
  
 **概要**  
 **Configdsn**システム情報のデータソースを追加、変更、または削除します。 ユーザーに接続情報の入力を求めることがあります。 ドライバー DLL または別のセットアップ DLL に配置できます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL ConfigDSN(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>引数  
 *hwndParent*  
 代入親ウィンドウハンドル。 ハンドルが null の場合、この関数はダイアログボックスを表示しません。  
  
 *fRequest*  
 代入要求の種類。 *Frequest*引数には、次のいずれかの値が含まれている必要があります。  
  
 ODBC_ADD_DSN:新しいデータソースを追加します。  
  
 ODBC_CONFIG_DSN:既存のデータソースを構成 (変更) します。  
  
 ODBC_REMOVE_DSN:既存のデータソースを削除します。  
  
 *lpszDriver*  
 代入物理ドライバー名の代わりにユーザーに提示されるドライバーの説明 (通常は、関連付けられている DBMS の名前)。  
  
 *lpszAttributes*  
 代入キーワードと値のペアの形式の、二重の null で終わる属性のリスト。 詳細については、「コメント」を参照してください。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合は TRUE、失敗した場合は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **Configdsn**が FALSE を返す場合、関連 *\*する pferrorcode*値は、 **sqlpostインストーラエラー**の呼び出しによってインストーラーエラーバッファーにポストされ、 **sqlインストーラエラー**を呼び出すことによって取得できます。 次の表は、 **sqlインストーラエラー**によって返される可能性がある *\*pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|ウィンドウハンドルが無効です|*HwndParent*引数が無効でした。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無効なキーワードと値のペア|*Lpszattributes*引数に構文エラーが含まれています。|  
|ODBC_ERROR_INVALID_NAME|ドライバーまたは翻訳者名が無効です|*Lpszdriver*引数が無効でした。 レジストリに見つかりませんでした。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求の種類が無効です|*Frequest*引数は、次のいずれかではありませんでした:<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN|  
|ODBC_ERROR_REQUEST_FAILED|失敗した*要求*|*Frequest*引数によって要求された操作を実行できませんでした。|  
|ODBC_ERROR_DRIVER_SPECIFIC|ドライバーまたはトランスレーター固有のエラー|ODBC インストーラーエラーが定義されていないドライバー固有のエラー。 **Sqlpostインストーラ error**関数の呼び出しの*szerror*引数には、ドライバー固有のエラーメッセージが含まれている必要があります。|  
  
## <a name="comments"></a>コメント  
 **Configdsn**は、インストーラー DLL からの接続情報を、キーワードと値のペアの形式の属性のリストとして受け取ります。 各ペアは null バイトで終了し、リスト全体は null バイトで終了します。 (つまり、2つの null バイトはリストの末尾をマークします)。キーワードと値のペアの等号を囲むスペースは使用できません。 **Configdsn**では、 **SQLBrowseConnect**および**SQLDriverConnect**に対して有効なキーワードではないキーワードを受け入れることができます。 **Configdsn**では、 **SQLBrowseConnect**および**SQLDriverConnect**に有効なキーワードであるすべてのキーワードがサポートされるとは限りません。 (**Configdsn**は**DRIVER**キーワードを受け入れません)。**Configdsn**関数で使用されるキーワードは、インストーラーの自動セットアップ機能を使用してデータソースを再作成するために必要なすべてのオプションをサポートしている必要があります。 **Configdsn**値と接続文字列値を使用する場合は、同じキーワードを使用する必要があります。  
  
 **SQLBrowseConnect**と**SQLDriverConnect**の場合と同様に、キーワードとその値に **[]{}()、;? を含めることはできません。=\*! @** 文字、 **DSN**キーワードの値は空白だけで構成することはできません。 レジストリの文法により、キーワードとデータソース名に円記号 (\\) を含めることはできません。  
  
 **Configdsn**は**sqlvaliddsn**を呼び出して、データソース名の長さを確認し、無効な文字が名前に含まれていないことを確認する必要があります。 データソース名が SQL_MAX_DSN_LENGTH より長い場合、または無効な文字が含まれている場合、 **Sqlvaliddsn**はエラーを返し、 **configdsn**はエラーを返します。 データソース名の長さも**Sqlwritedsntoini**によって確認されます。  
  
 たとえば、ユーザー ID、パスワード、およびデータベース名を必要とするデータソースを構成するために、セットアップアプリケーションは次のようなキーワードと値のペアを渡す場合があります。  
  
```  
DSN=Personnel Data\0UID=Smith\0PWD=Sesame\0DATABASE=Personnel\0\0  
```  
  
 これらのキーワードの詳細については、「 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) and each driver's documentation」を参照してください。  
  
 ダイアログボックスを表示するには、 *hwndParent*を null にすることはできません。  
  
## <a name="adding-a-data-source"></a>データ ソースの追加  
 *Lpszattributes*で**configdsn**にデータソース名が渡されると、 **configdsn**によって名前が有効であることがチェックされます。 データソース名が既存のデータソース名と一致し、 *hwndParent*が null の場合、 **configdsn**は既存の名前を上書きします。 既存の名前と一致し、 *hwndParent*が null でない場合、 **configdsn**はユーザーに対して既存の名前を上書きするように求めます。  
  
 *Lpszattributes*にデータソースへの接続に必要な情報が含まれている場合は、 **configdsn**を使用してデータソースを追加したり、ユーザーが接続情報を変更できるダイアログボックスを表示したりすることができます。 *Lpszattributes*にデータソースに接続するための十分な情報が含まれていない場合は、 **configdsn**によって必要な情報が決定される必要があります。*hwndParent*が null でない場合は、ユーザーから情報を取得するためのダイアログボックスが表示されます。  
  
 **Configdsn**によってダイアログボックスが表示される場合は、 *lpszattributes*で渡されたすべての接続情報を表示する必要があります。 特に、データソース名が渡された場合、その名前は**Configdsn**によって表示されますが、ユーザーが変更することはできません。 **Configdsn**では、 *lpszattributes*で渡されない接続情報の既定値を指定できます。  
  
 **Configdsn**がデータソースの完全な接続情報を取得できない場合は、FALSE を返します。  
  
 **Configdsn**がデータソースの完全な接続情報を取得できる場合、インストーラー DLL で**Sqlwritedsntoini**を呼び出して、新しいデータソースの仕様を Odbc .ini ファイル (またはレジストリ) に追加します。 **Sqlwritedsntoini**は、[ODBC データソース] セクションにデータソース名を追加し、[データソースの指定] セクションを作成して、ドライバーのキーワードを値としてドライバーの説明と共に追加します。 **Configdsn**はインストーラー DLL 内の**Sqlwriteprivateprofilestring**を呼び出して、ドライバーによって使用されるキーワードと値を追加します。  
  
## <a name="modifying-a-data-source"></a>データソースの変更  
 データソースを変更するには、 *Lpszattributes*の**configdsn**にデータソース名を渡す必要があります。 **Configdsn**は、データソース名が Odbc .ini ファイル (またはレジストリ) にあることを確認します。  
  
 *HwndParent*が null の場合、 **Configdsn**は*lpszattributes*の情報を使用して、Odbc .ini ファイル (またはレジストリ) の情報を変更します。 *HwndParent*が null でない場合、 **configdsn**では、 *lpszattributes*; の情報を使用してダイアログボックスが表示されます。*Lpszattributes*以外の情報については、システム情報の情報が使用されます。 ユーザーは、 **Configdsn**がシステム情報に格納する前に、情報を変更できます。  
  
 データソース名が変更された場合、 **Configdsn**はまずインストーラー DLL で**Sqlremovedsnfromini**を呼び出して、Odbc .ini ファイル (またはレジストリ) から既存のデータソースの仕様を削除します。 次に、前のセクションの手順に従って、新しいデータソースの仕様を追加します。 データソース名が変更されていない場合、 **Configdsn**はインストーラー DLL 内の**Sqlwriteprivateprofilestring**を呼び出して他の変更を行います。 **Configdsn**では、 **Driver**キーワードの値を削除または変更することはできません。  
  
## <a name="deleting-a-data-source"></a>データソースの削除  
 データソースを削除するには、 *Lpszattributes*の**configdsn**にデータソース名を渡す必要があります。 **Configdsn**は、データソース名が Odbc .ini ファイル (またはレジストリ) にあることを確認します。 次に、インストーラー DLL で**Sqlremovedsnfromini**を呼び出して、データソースを削除します。  
  
## <a name="note"></a>注
 このルーチンの Unicode バージョンを記述する場合は、LPCSTR ではなく LPCWSTR 引数を使用して、 **ConfigDSNW**を呼び出す必要があります。
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|データソースの追加、変更、または削除|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Odbc .ini ファイルまたはレジストリから値を取得する|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|  
|既定のデータソースの削除|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Odbc .ini (またはレジストリ) からのデータソース名の削除|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|Odbc .ini (またはレジストリ) へのデータソース名の追加|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|  
|Odbc .ini ファイルまたはレジストリへの値の書き込み|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
