---
title: SQLManageDataSources |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLManageDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLManageDataSources
helpviewer_keywords:
- SQLManageDataSources [ODBC]
ms.assetid: ac6d186f-b394-406c-94c4-c6331d1ca468
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 819856a584c6133e28e222a704b720337f99cd9c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018964"
---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**準拠**  
 バージョンが導入されました。ODBC 2.0  
  
 **まとめ**  
 **SQLManageDataSources**ユーザーことができますを設定する、追加、およびシステム情報のデータ ソースを削除 ダイアログ ボックスを表示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>引数  
 *hwnd*  
 [入力]親ウィンドウ ハンドル。  
  
## <a name="returns"></a>戻り値  
 **SQLManageDataSources**場合は FALSE を返します*hwnd*有効なウィンドウ ハンドルではありません。 それ以外の場合、TRUE を返します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLManageDataSources** 、関連付けられている FALSE が返されます *\*pfErrorCode*を呼び出して値を取得する**SQLInstallerError**します。 次の表、  *\*pfErrorCode*によって返される値**SQLInstallerError**とこの関数のコンテキストでそれぞれについて説明します。  
  
|*\*pfErrorCode*|[エラー]|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーのエラー|エラーが発生する特定のインストーラーのエラーがなかった。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*できませんでした|呼び出し**ConfigDSN**できませんでした。|  
|ODBC_ERROR_INVALID__HWND|無効なウィンドウ ハンドル|*Hwnd*引数が無効または NULL。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|インストーラーは、メモリ不足のため、関数を実行できませんでした。|  
  
## <a name="managing-data-sources"></a>データ ソースの管理  
 **SQLManageDataSources**最初に表示されます、 **ODBC データ ソース アドミニストレーター**  ダイアログ ボックスで、次の図に示すようにします。  
  
 ![ODBC データ ソース アドミニストレーター ダイアログ ボックス](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 ダイアログ ボックスでは、3 つのタブの下のシステム情報の一覧にあるデータ ソースが表示されます。**ユーザー DSN**、**システム DSN**、および**ファイル DSN**します。 ユーザーについて、データ ソースをダブルクリックまたはデータ ソースを選択およびクリックしてでかどうか**構成**、 **SQLManageDataSources**呼び出し**ConfigDSN** ODBC_CONFIG_ による DLL のセットアップDSN のオプションです。  
  
 ユーザーがクリックした場合**追加**、 **SQLManageDataSources**が表示されます、**データ ソースの新規作成** ダイアログ ボックスで、次の図に示すようにします。  
  
 ![新しいデータ ソース ダイアログ ボックスを作成する](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 ダイアログ ボックスには、インストールされているドライバーの一覧が表示されます。 ユーザーについて、ドライバーをダブルクリックするまたはドライバーを選択およびクリックしてでかどうか**OK**、 **SQLManageDataSources**呼び出し**ConfigDSN**セットアップ DLL を ODBC_ADD_DSN オプションを渡します。  
  
 ユーザーがデータ ソースを選択してクリックすると**削除**、 **SQLManageDataSources**ユーザーがデータ ソースを削除するかどうかを確認します。 ユーザーがクリックした場合**はい**、 **SQLManageDataSources**呼び出し**ConfigDSN** ODBC_REMOVE_DSN オプションを使用してセットアップ DLL でします。  
  
 **データ ソースの新規作成**ユーザーのデータ ソース、システム データ ソース、またはファイル データ ソースを追加または削除する ダイアログ ボックスを使用します。  
  
## <a name="user-dsns"></a>ユーザー Dsn  
 個々 のユーザー用に作成された Dsn はシステム Dsn と区別するためのユーザー Dsn と呼ばれます。 ユーザー Dsn は、システム情報に、次のように登録されます。  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>システム Dsn  
 **データ ソースの新規作成**ダイアログ ボックスで、ローカル コンピューターまたは削除に 1 つは、システム データ ソースを追加する、またはシステム データ ソースの構成を設定できます。  
  
 同じコンピューター上の 1 つ以上のユーザーによっては、データ ソースがシステム データ ソース名 (DSN) を使用して設定を使用できます。 これは、コンピューターにユーザーがログインしていない場合でも、データ ソースへのアクセスを取得し、システム全体のサービスで使用できます。  
  
 システム DSN は、HKEY_CURRENT_USER エントリではなく、システムの情報には、HKEY_LOCAL_MACHINE エントリに登録されます。 1 ユーザーに特定のユーザー名とパスワードを使用してログオンし、使用することがそのコンピューターのすべてのユーザーや、システム全体の自動サービスによっては関連付けられません。 システム DSN は、ただし、1 つのマシンに関連付けられています。 マシン間のリモートの Dsn を使用する機能はサポートしません。 システム Dsn は、システム情報に、次のように登録されます。  
  
 HKEY_LOCAL_MACHINE ソフトウェア ODBC Odbc.ini  
  
## <a name="file-dsns"></a>ファイル Dsn  
 ファイル データ ソースをは、コンピューターのデータ ソースを行い、任意の 1 人のユーザーまたはコンピューターに登録されていないと、データ ソース名がありません。 そのデータ ソースの接続情報は、任意のコンピューターにコピーできる .dsn ファイルに含まれます。 ファイル データ ソースをでき、共有可能 .dsn ファイルをネットワークに存在する場合は同時に使用する、ネットワーク上の複数のユーザーが、ユーザーがある、適切なドライバーがインストールされている限り。 ファイルのデータ ソースもできます共有可能、それを使用して単一のコンピューターにのみ場合。  
  
 ファイル データ ソースの詳細については、次を参照してください。[を使用してファイル データ ソースの接続](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)、を参照してくださいまたは[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)します。  
  
## <a name="managing-drivers"></a>ドライバーの管理  
 ユーザーがクリックした場合、**ドライバー**  タブで、 **ODBC データ ソース アドミニストレーター**ダイアログ ボックスで、 **SQLManageDataSources**システムにインストールされている ODBC ドライバーの一覧を表示します。ドライバーに関する情報。 表示される日付は、次の図に示すように、ドライバーの作成日です。  
  
 ![ODBC データ ソース アドミニストレーター [ドライバー] タブ](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>[トレース オプション]  
 ユーザーがクリックした場合、**トレース** タブで、 **ODBC データ ソース アドミニストレーター**ダイアログ ボックスで、 **SQLManageDataSources**次に示すように、トレースのオプションを表示します図。  
  
 ![ODBC データ ソース アドミニストレーターのトレース タブ](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 ユーザーがクリックした場合**トレースの開始**し、クリック **[ok]** 、 **SQLManageDataSources**マシンで現在実行されているすべてのアプリケーションを手動でトレースを有効にします。  
  
 ユーザーが内のトレース ファイルの名前を指定するかどうか、**ログ ファイルのパス**テキスト ボックスと、数回のクリック**OK**、 **SQLManageDataSources**設定、 **TraceFile**の指定した名前に、システム情報 [ODBC] セクションではキーワードです。  
  
> [!IMPORTANT]  
>  Visual Studio Analyzer のサポートは、以降 (Visual Studio Analyzer のみ含まれていた以前のバージョンの Visual Studio でします。) Windows 8 では削除されました。 トラブルシューティング メカニズムの代わりに、BID のトレースを使用します。  
  
 ユーザーがクリックした場合**Visual Studio Analyzer の開始**し、クリック **[ok]** 、Visual Studio Analyzer を有効にします。 これまでは有効のままに**Visual Studio Analyzer の停止**をクリックします。  
  
 トレースの詳細については、次を参照してください。[トレース](../../../odbc/reference/develop-app/tracing.md)します。 詳細については、**トレース**と**TraceFile**キーワードを参照してください[ODBC サブキー](../../../odbc/reference/install/odbc-subkey.md)します。  
  
## <a name="related-functions"></a>関連する関数  
  
|詳細|参照先|  
|---------------------------|---------|  
|データ ソースの作成|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|
