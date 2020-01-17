---
title: SQLCreateDataSource 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCreateDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCreateDataSource
helpviewer_keywords:
- SQLCreateDataSource function [ODBC]
ms.assetid: 76ee851a-dca9-40cc-8e9e-eb3f74e560ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0b3a6fced096c779b5ab91bf4e5b6a3f0a66e5f1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121385"
---
# <a name="sqlcreatedatasource-function"></a>SQLCreateDataSource 関数
**準拠**  
 バージョンが導入されました。ODBC 2.0  
  
 **まとめ**  
 **SQLCreateDataSource**ユーザーがデータ ソースを追加する ダイアログ ボックスが表示されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>引数  
 *hwnd*  
 [入力]親ウィンドウ ハンドル。  
  
 *lpszDS*  
 [入力]データ ソースの名前。 *lpszDS* null ポインターまたは空の文字列を指定できます。  
  
## <a name="returns"></a>戻り値  
 **SQLCreateDataSource**データ ソースを作成した場合は TRUE を返します。 それ以外の場合、FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLCreateDataSource** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーのエラー|エラーが発生する特定のインストーラーのエラーがなかった。|  
|ODBC_ERROR_INVALID_HWND|無効なウィンドウ ハンドル|*Hwnd*引数が無効または NULL。|  
|ODBC_ERROR_INVALID_DSN|無効な DSN|*LpszDS*引数には、DSN に無効な文字列が含まれています。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*できませんでした|呼び出し**ConfigDSN** ODBC_ADD_DSN オプションを使用できませんでした。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|ドライバーまたはトランスレーター セットアップ ライブラリを読み込むことができません。|ドライバーのセットアップのライブラリを読み込むことができませんでした。|  
|ODBC_ERROR_USER_CANCELED|操作のユーザーによって取り消されました|ユーザーには、新しいデータ ソースの作成が取り消されました。|  
|ODBC_ERROR_CREATE_DSN_FAILED|要求された DSN を作成できませんでした。|データベースに接続できませんでした。呼び出し**SQLDriverConnect**のファイル DSN 接続に成功が返されませんでした。<br /><br /> ファイルに書き込めませんでした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|インストーラーは、メモリ不足のため、関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 場合*hwnd*が null、 **SQLCreateDataSource** FALSE を返します。 それ以外の場合、表示、**データ ソースの新規作成** ダイアログ ボックスで次の図に示すように、設定、データ ソースの種類を選択するためのウィザード ページ。  
  
 ![新しいデータ ソース ダイアログ ボックスを作成します種類を選択します](../../../odbc/reference/syntax/media/ch23a.gif "CH23A。")  
  
 既定のオプションは**ファイル データ ソース**します。 データ ソースが選択されている場合と**次**クリックすると、インストールされたドライバーの一覧を含む次のウィザード ページが表示されます。  
  
 ![新しいデータ ソース ダイアログ ボックスを作成しますドライバーの選択](../../../odbc/reference/syntax/media/ch23b.gif "CH23B。")  
  
 場合**キャンセル**がクリックされた、ダイアログ ボックスは表示されなくなりますと**SQLCreateDataSource** ODBC_ERROR_USER_CANCELED のエラー コードでは FALSE を返します。 いずれか、**ユーザー データ ソース**または**システム データ ソース**オプションが選択された、**詳細**ボタンは使用できません。  
  
 ときに、**次**ボタンをクリックすると、次のいずれかが発生する、データの種類に応じて、ソースが選択されています。  
  
-   場合**ファイル データ ソース**がファイル名の入力をユーザーに選択すると、ウィザードのページを表示します。  
  
-   いずれか**ユーザー データ ソース**または**システム データ ソース**が選択すると、データ ソースとドライバーの種類を表示するウィザード ページの表示については、いつ**完了**はクリックすると、データ ソースを設定します。  
  
 場合**詳細**がクリックされたドライバー固有の情報を入力するユーザーのデータ ソースの新規作成ウィザードのページからウィザード ページが表示されます。 このダイアログ ボックスのテキスト ボックスで、次の図に示すように、ドライバーと戻り値で区切られたキーワードを入力します。  
  
 ![事前作成用のファイル DSN 設定ダイアログ ボックス](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 追加のドライバー固有のキーワードの説明の下にあります**SQLDriverConnect**します。 除くすべて**DSN**許可されます。  
  
 既定値は、**この接続の確認**オプションが TRUE です。 この既定値には、このウィザード ページがアクティブ化されるかどうかが適用されます。 場合 **[ok]** がクリックされた、テキスト ボックスで指定した文字列と**この接続の確認**オプションの値がキャッシュされます。 (場合、**閉じる**ボタンまたは**キャンセル**がクリックすると、新たに入力した任意、テキスト ボックスに、文字列が指定されているために、ドライバー固有の情報が失われたと**の接続の確認**オプションの値はキャッシュされません)。  
  
 場合**ファイル データ ソース**ユーザーがファイル名を入力するように求め、ドライバーが選択されているし、キーワードの値は、詳細ウィザードのページに入力されている、その後、ウィザードの最初のページで選択しました。 クリックして**参照**場合の既定のディレクトリ、ファイル名を検索する、**参照**ボックスは、HKEY_LOCAL_MACHINE で CommonFileDir によって指定されたパスの組み合わせで指定されました。Microsoft\Windows\CurrentVersion と"ODBC\DataSources"。 (CommonFileDir"C:\Program files \common files Files"だった場合は、既定のディレクトリは"C:\Program files \common files 場合 Sources"が)。  
  
 ファイル名が入力されている場合と **[次へ]** がクリックされた、ファイル名の入力に対して、オペレーティング システムの標準のファイルの名前付け規則の有効性がチェックします。 ファイル名が有効でない場合、エラー メッセージ ボックスは、無効なファイル名を入力したユーザーを通知します。 ユーザーが承認されると、メッセージ ボックス、ファイル名が入力されるウィザード ページにフォーカスが返されます。 ファイル名が有効な場合は、次の図に示すように、審査のため、選択したキーワードと値のペアを表示するウィザード ページが表示されます。  
  
 ![新しいデータ ソース ダイアログ ボックスを作成します確認](../../../odbc/reference/syntax/media/ch23d.gif "CH23D。")  
  
 場合**完了**がクリックされたと**ファイル データ ソース**データ ソースの種類として選択されている場合に、**この接続の確認**オプションが TRUE、 **SQLDriverConnect**を呼び出すと、 **SAVEFILE**と**ドライバー**キーワード。 *DriverCompletion*引数が SQL_DRIVER_COMPLETE に設定します。 ファイル名を**SAVEFILE**キーワードは、入力した名前を選択、やのドライバー名、**ドライバー**キーワードは、選択された名。 後にその文字列が追加されたドライバー固有の接続文字列は、詳細ウィザードのページで指定されている場合、**ドライバー**キーワード。  
  
 場合**SQLDriverConnect**返します SQL_SUCCESS、ドライバー マネージャーがファイル DSN を作成します。 **SQLCreateDataSource** TRUE を返します。 場合**SQLDriverConnect** SQL_SUCCESS、警告メッセージを返さないボックスは、接続をデータ ソースを確立できませんでしたを示します。 最低限の接続情報を含む DSN を作成もできます。 このメッセージ ボックスをキャンセルするか、ファイル DSN の作成を続行できます。  
  
 かどうか、ユーザーは、DSN を作成を続行するが、このプロセスは継続として、**この接続の確認**オプションが FALSE に設定されました。 FALSE が返されます場合は、ユーザーのキャンセルを選択**SQLCreateDataSource** ODBC_ERROR_CREATE_DSN_FAILED のエラー コードを使用します。  
  
 場合**ファイル データ ソース**データ ソースの種類として選択された、**この接続の確認**オプションが FALSE で、ファイル DSN がで作成された、**ドライバー**キーワードとユーザーが指定した文字列の詳細ウィザードのページから (ある場合) に接続します。 ファイルの作成が成功した場合の TRUE が返されます。 **SQLCreateDataSource**します。 ファイルの作成に失敗した場合、エラー メッセージ ボックスは、ユーザーにどのようなエラーがオペレーティング システムから返されたを通知します。 FALSE が返されます**SQLCreateDataSource** ODBC_ERROR_CREATE_DSN_FAILED のエラー コードを使用します。 ファイル データ ソースの詳細については、次を参照してください。[を使用してファイル データ ソースの接続](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)、を参照してくださいまたは[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)します。  
  
 場合**ユーザー**または**システム データ ソース**データ ソースの種類として選択された**ConfigDSN**ドライバーのセットアップでは、ライブラリ、ODBC_ADD_DSN で呼び出されます*起こり*します。 詳細については、次を参照してください。 [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|データ ソースの管理|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
