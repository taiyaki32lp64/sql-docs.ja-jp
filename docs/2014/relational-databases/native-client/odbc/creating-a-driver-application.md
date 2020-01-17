---
title: SQL Server ネイティブ クライアント ODBC ドライバー アプリケーションを作成します。マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: db71e2ca03cbefdccf0bdf879fdb43d775125064
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63205267"
---
# <a name="creating-a-sql-server-native-client-odbc-driver-application"></a>SQL Server Native Client ODBC ドライバー アプリケーションの作成
  ODBC アーキテクチャには、次の機能を実行する 4 つのコンポーネントがあります。  
  
|コンポーネント|関数|  
|---------------|--------------|  
|アプリケーション|ODBC 関数を呼び出して ODBC データ ソースと通信し、SQL ステートメントを送信して、結果セットを処理します。|  
|ドライバー マネージャー|アプリケーションと、そのアプリケーションで使用されるすべての ODBC ドライバー間の通信を管理します。|  
|Driver|アプリケーションからのすべての ODBC 関数呼び出しを処理し、データ ソースに接続して、SQL ステートメントをアプリケーションからデータ ソースに渡し、結果をアプリケーションに返します。 必要に応じて、アプリケーションの ODBC SQL をデータ ソースで使用されるネイティブ SQL に変換します。|  
|データ ソース|DBMS 内にあるデータの特定のインスタンスにアクセスするためにドライバーが必要とするすべての情報が含まれています。|  
  
 使用するアプリケーション、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスと通信するクライアントのネイティブの ODBC ドライバー[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]次のタスクを実行します。  
  
-   データ ソースとの接続  
  
-   データ ソースへの SQL ステートメントの送信  
  
-   データ ソースから返されたステートメント結果の処理  
  
-   プロセスのエラーとメッセージ  
  
-   データ ソースへの接続の終了  
  
 書かれてより複雑なアプリケーション、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ネイティブ クライアントの ODBC ドライバーは、次のタスクを実行も可能性があります。  
  
-   カーソルを使用した結果セット内の位置の制御  
  
-   トランザクション制御に関するコミット操作やロールバック操作の要求  
  
-   2 台以上のサーバーに関連する分散トランザクションの実行  
  
-   リモート サーバーでのストアド プロシージャの実行  
  
-   結果セットの属性に関する情報を取得するためのカタログ関数の呼び出し  
  
-   一括コピー操作を実行します。  
  
-   大規模なデータの管理 (**では**、 **nvarchar(max)** 、および**varbinary(max)** 列) の操作  
  
-   データベース ミラーリングが構成されているときにフェールオーバーを容易にするための再接続ロジックの使用  
  
-   パフォーマンス データや実行時間の長いクエリのログ記録  
  
 ODBC 関数を呼び出すには、C または C++ アプリケーションで sql.h ヘッダー ファイル、sqlext.h ヘッダー ファイル、および sqltypes.h ヘッダー ファイルをインクルードする必要があります。 ODBC インストーラーの API 関数を呼び出す場合は、アプリケーションで odbcinst.h ヘッダー ファイルをインクルードする必要があります。 Unicode ODBC アプリケーションでは、sqlucode.h ヘッダー ファイルをインクルードする必要があります。 ODBC アプリケーションは、odbc32.lib ファイルとリンクする必要があります。 ODBC インストーラーの API 関数を呼び出す ODBC アプリケーションは、odbccp32.lib ファイルとリンクする必要があります。 これらのファイルは、Windows プラットフォーム SDK に含まれています。  
  
 など、多くの ODBC ドライバー、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ネイティブ クライアントの ODBC ドライバーでは、ドライバー固有の ODBC 拡張機能を提供します。 利用する[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ネイティブ クライアントの ODBC ドライバーに固有の拡張機能、アプリケーションは、sqlncli.h のヘッダー ファイルを含める必要があります。 このヘッダー ファイルには、次の要素が含まれています。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ネイティブ クライアントの ODBC ドライバーに固有の接続の属性です。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ネイティブ クライアントの ODBC ドライバーに固有のステートメントの属性。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ネイティブ クライアントの ODBC ドライバーを指定する列の属性。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固有のデータ型  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固有のユーザー定義データ型  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ネイティブ クライアントの ODBC ドライバーに対応した[SQLGetInfo](../../native-client-odbc-api/sqlgetinfo.md)型です。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ネイティブ クライアントの ODBC ドライバーの診断フィールドです。  
  
-   診断に役立つ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固有の動的関数コード  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固有のネイティブ C データ型に関する C 型定義や C++ 型定義 (列が C データ型の SQL_C_BINARY にバインドされるときに返される)  
  
-   SQLPERF データ構造体の型定義  
  
-   ODBC 接続経由の一括コピー API の使用をサポートするための一括コピー用のマクロとプロトタイプ  
  
-   リンク サーバーとリンク サーバーのカタログ一覧を取得するための分散クエリ メタデータ API 関数呼び出し  
  
 一括コピー機能を使用する C または C++ の ODBC アプリケーションの[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ネイティブ クライアントの ODBC ドライバーは、sqlncli11.lib ファイルにリンクする必要があります。 分散クエリ メタデータ API 関数を呼び出すアプリケーションも、sqlncli11.lib とリンクする必要があります。 Sqlncli.h と sqlncli11.lib ファイルは、の一部として配布、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]開発者向けのツールです。 次のように、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の Include ディレクトリはコンパイラの INCLUDE パスに、Lib ディレクトリは LIB パスに含める必要があります。  
  
```  
LIB=c:\Program Files\Microsoft Data Access SDK 2.8\Libs\x86\lib;C:\Program Files\Microsoft SQL Server\100\Tools\SDK\Lib;  
INCLUDE=c:\Program Files\Microsoft Data Access SDK 2.8\inc;C:\Program Files\Microsoft SQL Server\100\Tools\SDK\Include;  
```  
  
 アプリケーションで複数の ODBC 呼び出しが同時に未処理状態になる必要があるかどうかというデザイン上の決定を、アプリケーションのビルド処理の初期段階で行います。 複数の同時実行 ODBC 呼び出しをサポートするには 2 つの方法があり、このセクションの残りのトピックで説明されています。 詳細についてを参照してください、 [ODBC プログラマーズ リファレンス](https://go.microsoft.com/fwlink/?LinkId=45250)。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [非同期モードと SQLCancel](../../native-client-odbc-api/sqlcancel.md)  
  
-   [マルチスレッド アプリケーション](creating-a-driver-application-multithreaded-applications.md)  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  
