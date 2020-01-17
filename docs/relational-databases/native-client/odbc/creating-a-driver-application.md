---
title: SQL Native Client ODBC アプリの作成
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, architecture
- SQL Server Native Client ODBC driver, creating applications
- ODBC function calls
- ODBC, header files
- ODBC applications
- ODBC applications, creating
- SQL Server Native Client ODBC driver, extensions
- applications [SQL Server Native Client]
- SQL Server Native Client ODBC driver, ODBC architecture
- extensions [ODBC]
- ODBC, driver extensions
- function calls [ODBC]
ms.assetid: c83c36e2-734e-4960-bc7e-92235910bc6f
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0cf46cdf2fb658623a549f3eef160ae6293ab9c7
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247390"
---
# <a name="creating-a-driver-application"></a>ドライバー アプリケーションの作成
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC アーキテクチャには、次の機能を実行する 4 つのコンポーネントがあります。  
  
|コンポーネント|機能|  
|---------------|--------------|  
|アプリケーション|ODBC 関数を呼び出して ODBC データ ソースと通信し、SQL ステートメントを送信して、結果セットを処理します。|  
|ドライバー マネージャー|アプリケーションと、そのアプリケーションで使用されるすべての ODBC ドライバー間の通信を管理します。|  
|ドライバー|アプリケーションからのすべての ODBC 関数呼び出しを処理し、データ ソースに接続して、SQL ステートメントをアプリケーションからデータ ソースに渡し、結果をアプリケーションに返します。 必要に応じて、アプリケーションの ODBC SQL をデータ ソースで使用されるネイティブ SQL に変換します。|  
|データ ソース|DBMS 内にあるデータの特定のインスタンスにアクセスするためにドライバーが必要とするすべての情報が含まれています。|  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC ドライバーを使用しての[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンスと通信するアプリケーションは、次のタスクを実行します。  
  
-   データ ソースとの接続  
  
-   データ ソースへの SQL ステートメントの送信  
  
-   データ ソースから返されたステートメント結果の処理  
  
-   エラーとメッセージを処理します  
  
-   データ ソースへの接続の終了  
  
 Native Client ODBC ドライバー用に記述[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]されたより複雑なアプリケーションでも、次のタスクが実行される場合があります。  
  
-   カーソルを使用した結果セット内の位置の制御  
  
-   トランザクション制御に関するコミット操作やロールバック操作の要求  
  
-   2 台以上のサーバーに関連する分散トランザクションの実行  
  
-   リモート サーバーでのストアド プロシージャの実行  
  
-   結果セットの属性に関する情報を取得するためのカタログ関数の呼び出し  
  
-   一括コピー操作の実行  
  
-   大規模データ (**varchar (max)**、 **nvarchar (max)**、および**varbinary (max)** の各列) 操作の管理  
  
-   データベース ミラーリングが構成されているときにフェールオーバーを容易にするための再接続ロジックの使用  
  
-   パフォーマンス データや実行時間の長いクエリのログ記録  
  
 ODBC 関数を呼び出すには、C または C++ アプリケーションで sql.h ヘッダー ファイル、sqlext.h ヘッダー ファイル、および sqltypes.h ヘッダー ファイルをインクルードする必要があります。 ODBC インストーラーの API 関数を呼び出す場合は、アプリケーションで odbcinst.h ヘッダー ファイルをインクルードする必要があります。 Unicode ODBC アプリケーションでは、sqlucode.h ヘッダー ファイルをインクルードする必要があります。 ODBC アプリケーションは、odbc32.lib ファイルとリンクする必要があります。 ODBC インストーラーの API 関数を呼び出す ODBC アプリケーションは、odbccp32.lib ファイルとリンクする必要があります。 これらのファイルは、Windows プラットフォーム SDK に含まれています。  
  
 Native Client ODBC ドライバーを含む[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]多くの odbc ドライバーには、ドライバー固有の odbc 拡張機能が用意されています。 Native Client ODBC ドライバー [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]固有の拡張機能を利用するには、アプリケーションに sqlncli ヘッダーファイルを含める必要があります。 このヘッダー ファイルには、次の要素が含まれています。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC ドライバー固有の接続属性。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC ドライバー固有のステートメント属性。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC ドライバー固有の列属性。  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固有のデータ型  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固有のユーザー定義データ型  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC ドライバー固有の[SQLGetInfo](../../../relational-databases/native-client-odbc-api/sqlgetinfo.md)型。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC ドライバーの診断フィールド。  
  
-   診断に役立つ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固有の動的関数コード  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固有のネイティブ C データ型に関する C 型定義や C++ 型定義 (列が C データ型の SQL_C_BINARY にバインドされるときに返される)  
  
-   SQLPERF データ構造体の型定義  
  
-   ODBC 接続経由の一括コピー API の使用をサポートするための一括コピー用のマクロとプロトタイプ  
  
-   リンク サーバーとリンク サーバーのカタログ一覧を取得するための分散クエリ メタデータ API 関数呼び出し  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC ドライバーの一括コピー機能を使用する C または C++ ODBC アプリケーションは、sqlncli11 ファイルとリンクされている必要があります。 分散クエリ メタデータ API 関数を呼び出すアプリケーションも、sqlncli11.lib とリンクする必要があります。 Sqlncli ファイルと sqlncli11 ファイルは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]開発者ツールの一部として配布されます。 次のように、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の Include ディレクトリはコンパイラの INCLUDE パスに、Lib ディレクトリは LIB パスに含める必要があります。  
  
```  
LIB=c:\Program Files\Microsoft Data Access SDK 2.8\Libs\x86\lib;C:\Program Files\Microsoft SQL Server\100\Tools\SDK\Lib;  
INCLUDE=c:\Program Files\Microsoft Data Access SDK 2.8\inc;C:\Program Files\Microsoft SQL Server\100\Tools\SDK\Include;  
```  
  
 アプリケーションで複数の ODBC 呼び出しが同時に未処理状態になる必要があるかどうかというデザイン上の決定を、アプリケーションのビルド処理の初期段階で行います。 複数の同時実行 ODBC 呼び出しをサポートするには 2 つの方法があり、このセクションの残りのトピックで説明されています。 詳細については、 [ODBC プログラマーズリファレンス](https://go.microsoft.com/fwlink/?LinkId=45250)を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [非同期モードと SQLCancel](../../../relational-databases/native-client/odbc/creating-a-driver-application-asynchronous-mode-and-sqlcancel.md)  
  
-   [マルチスレッド アプリケーション](../../../relational-databases/native-client/odbc/creating-a-driver-application-multithreaded-applications.md)  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
