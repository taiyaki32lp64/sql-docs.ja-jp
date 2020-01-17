---
title: 複数のアクティブな結果セット (MARS) を使用する |Microsoft Docs
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, MARS
- SQLNCLI, MARS
- data access [SQL Server Native Client], MARS
- Multiple Active Result Sets
- SQL Server Native Client, MARS
- MARS [SQL Server]
- SQL Server Native Client ODBC driver, MARS
ms.assetid: ecfd9c6b-7d29-41d8-af2e-89d7fb9a1d83
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2b72f93aa979c504c0f6eeb6a3b867cc8360728f
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761313"
---
# <a name="using-multiple-active-result-sets-mars"></a>複数のアクティブな結果セット (MARS) の使用

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] では、[!INCLUDE[ssDE](../../../includes/ssde-md.md)] にアクセスするアプリケーションで複数のアクティブな結果セット (MARS) がサポートされるようになりました。 以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、データベース アプリケーションは 1 つの接続で複数のアクティブなステートメントを保持できませんでした。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の既定の結果セットを使用しているときは、アプリケーションはその接続で他のバッチを実行する前に、1 つのバッチのすべての結果セットを処理するか、取り消す必要がありました。 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] では新しい接続属性が導入され、アプリケーションは接続ごとに複数の要求を保留中にできるだけでなく、接続ごとに複数のアクティブな既定の結果セットを保持できるようになりました。  
  
 MARS によって、次の新しい機能を使用したアプリケーションのデザインが簡素化されます。  
  
-   アプリケーションは、既定の結果セットを複数開くことができ、複数の既定の結果セットからの読み取りをインターリーブすることができます。  
  
-   アプリケーションは既定の結果セットを開いたまま、他のステートメント (INSERT、UPDATE、DELETE、ストアド プロシージャ呼び出しなど) を実行できます。  
  
 MARS を使用するアプリケーションについては、次のガイドラインを参照してください。  
  
-   1 つの SQL ステートメント (SELECT、OUTPUT を伴う DML、RECEIVE、READ TEXT など) で生成される結果セットが短期間しか有効でない場合や結果セットが小さい場合は、既定の結果セットを使用します。  
  
-   1 つの SQL ステートメントで生成される結果セットが長期間有効な場合や結果セットが大きくなる場合は、サーバー カーソルを使用します。  
  
-   結果を返すかどうかにかかわらず手続き型の要求の場合、および複数の結果を返すバッチの場合、常に、結果の最後まで読み取ります。  
  
-   接続プロパティの変更やトランザクションの管理には、できるだけ [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントではなく API 呼び出しを優先して使用します。  
  
-   MARS では、複数のバッチが同時に実行されている間、セッション スコープの権限の借用が禁止されます。  

> [!NOTE]
> 既定では、MARS 機能はドライバーによって有効になっていません。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続するときに MARS を使用するには、接続文字列内で MARS を明示的に有効にする必要があります。 ただし、アプリケーションが MARS をサポートしていることをアプリケーションが検出した場合、既定では MARS が有効になることがあります。 これらのアプリケーションでは、必要に応じて接続文字列の MARS を無効にすることができます。 詳細については、この後の「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー」と「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバー」を参照してください。

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、接続でのアクティブなステートメントの数は制限されません。  
  
 複数ステートメントのバッチまたはストアドプロシージャを同時に実行する必要がない一般的なアプリケーションでは、mars の実装方法を理解しなくても、MARS の利点が得られます。 ただし、より複雑な要件のアプリケーションでは、MARS の実装方法を考慮する必要があります。  
  
 MARS では、1 つの接続内で複数の要求の実行をインターリーブできます。 つまり、1 つのバッチを実行し、その実行内で他の要求を実行できます。 ただし、MARS では並列実行が行われるのではなく、複数の実行がインターリーブされることに注意してください。  
  
 MARS のインフラストラクチャでは、複数のバッチがインターリーブ方式で実行されますが、実行の切り替えは明確に定義された時点でしか行われません。 また、ほとんどのステートメントはバッチ内で自動的に実行される必要があります。 クライアントに行を返すステートメント ( *yield ポイント*と呼ばれることもあります) は、次の例のように、行がクライアントに送信されている間、完了前に実行をインターリーブすることができます。  
  
-   SELECT  
  
-   FETCH  
  
-   RECEIVE  
  
 ストアド プロシージャまたはバッチの一部として実行されるその他のステートメントはいずれも、他の MARS 要求に切り替えられる前に実行を完了する必要があります。  
  
 バッチがどのようにインターリーブ実行されるかは、さまざまな要因の影響を受けます。そのため、呼び出しポイントを含む複数のバッチからのコマンドが実行されるときに、正確なシーケンスを予測することは困難です。 このような複雑なバッチをインターリーブ実行したときに、好ましくない影響が発生しないように注意してください。  
  
 このような問題を回避するために、接続状態 (SET、USE) やトランザクション (BEGIN TRAN、COMMIT、ROLLBACK) を管理する場合は、[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントではなく API 呼び出しを使用します。このとき、複数のステートメントで構成されるバッチに呼び出しポイントも含まれている場合、接続状態やトランザクションを管理するステートメントを含めないようにします。さらに、このようなバッチでは、すべての結果を処理するか、残りを取り消すことによって、実行を順番に行います。  
  
> [!NOTE]  
>  MARS が有効なときにトランザクションを手動または暗黙に開始するバッチやストアド プロシージャでは、バッチが終了する前にトランザクションを完了する必要があります。 トランザクションを完了しないと、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] はバッチの終了時にトランザクションによって行われたすべての変更をロールバックします。 このようなトランザクションは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によってバッチスコープのトランザクションとして管理されます。 これは [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] で導入された新しい形式のトランザクションで、MARS が有効なときに、既存の適切に動作するストアド プロシージャを使用できるようになります。 バッチスコープのトランザクションの詳細については、「[トランザクションステートメント&#40;transact-sql&#41;](~/t-sql/statements/statements.md)」を参照してください。  
  
 ADO から MARS を使用する例については、「 [USING ado with SQL Server Native Client](../../../relational-databases/native-client/applications/using-ado-with-sql-server-native-client.md)」を参照してください。  
  
## <a name="in-memory-oltp"></a>インメモリ OLTP  
 インメモリ OLTP では、クエリとネイティブコンパイルストアドプロシージャを使用した MARS がサポートされます。 MARS を使用すると、新しい結果セットから行をフェッチする要求を送信する前に、各結果セットを完全に取得しなくても、複数のクエリからデータを要求することができます。 複数の開いている結果セットから正常に読み取るには、MARS が有効な接続を使用する必要があります。  
  
 MARS は既定で無効になっているため、接続文字列に `MultipleActiveResultSets=True` を追加して明示的に有効にする必要があります。 次の例は、SQL Server のインスタンスに接続し、MARS が有効になっていることを指定する方法を示しています。  
  
```  
Data Source=MSSQL; Initial Catalog=AdventureWorks; Integrated Security=SSPI; MultipleActiveResultSets=True  
```  
  
 インメモリ OLTP を使用する MARS は、SQL エンジンの残りの部分では基本的に MARS と同じです。 次に、メモリ最適化テーブルとネイティブコンパイルストアドプロシージャで MARS を使用する場合の相違点を示します。  
  
 **MARS とメモリ最適化テーブル**  
  
 MARS が有効になっている接続を使用する場合、ディスクベーステーブルとメモリ最適化テーブルの違いは次のとおりです。  
  
-   2つのステートメントで同じ対象オブジェクト内のデータを変更できますが、両方が同じレコードを変更しようとすると、書き込み/書き込みの競合によって新しい操作が失敗します。 ただし、両方の操作で異なるレコードが変更された場合、操作は成功します。  
  
-   各ステートメントはスナップショット分離で実行されるため、新しい操作では既存のステートメントによって行われた変更を表示できません。 同時実行ステートメントが同じトランザクションで実行される場合でも、SQL エンジンは、相互に分離されたステートメントごとにバッチスコープトランザクションを作成します。 ただし、バッチスコープのトランザクションは同時にバインドされるため、1つのバッチスコープトランザクションのロールバックは、同じバッチ内の他のトランザクションに影響を及ぼします。  
  
-   DDL 操作はユーザートランザクションでは許可されないため、すぐに失敗します。  
  
 **MARS およびネイティブ コンパイル ストアド プロシージャ**  
  
 ネイティブコンパイルストアドプロシージャは、MARS が有効になっている接続で実行でき、yield ポイントが検出された場合にのみ実行を別のステートメントにすることができます。 Yield ポイントには SELECT ステートメントが必要です。これは、ネイティブコンパイルストアドプロシージャ内のステートメントであり、別のステートメントを実行することができます。 SELECT ステートメントが生成されないプロシージャ内に存在しない場合は、他のステートメントが開始される前に、そのステートメントが完了するまで実行されます。  
  
 **MARS とインメモリ OLTP のトランザクション**  
  
 インターリーブされたステートメントおよびアトミックブロックによって行われた変更は、相互に分離されます。 たとえば、1つのステートメントまたは atomic ブロックでいくつかの変更が行われた後、別のステートメントに対して実行が生成された場合、新しいステートメントでは、最初のステートメントによって行われた変更は表示されません。 また、最初のステートメントの実行が再開されても、他のステートメントによって行われた変更は表示されません。 ステートメントでは、ステートメントが開始される前に完了してコミットされた変更のみが表示されます。  
  
 BEGIN TRANSACTION ステートメントを使用して、現在のユーザートランザクション内で新しいユーザートランザクションを開始できます。これは相互運用モードでのみサポートされているので、BEGIN TRANSACTION は T-sql ステートメントからのみ呼び出すことができ、ネイティブにコンパイルされたストアドからは呼び出せません。作業.Save TRANSACTION またはトランザクションへの API 呼び出しを使用して、トランザクションにセーブポイントを作成できます。セーブポイントにロールバックするには、(save_point_name) を保存します。 この機能は、ネイティブコンパイルストアドプロシージャ内ではなく、T-sql ステートメントからのみ有効です。  
  
 **MARS インデックスと列ストアインデックス**  
  
 SQL Server (2016 以降) では、列ストアインデックスを持つ MARS がサポートされます。 SQL Server 2014 では、列ストア インデックスに読み取り専用で接続するために MARS が使用されます。    ただし、SQL Server 2014 では、列ストア インデックスを含むテーブルで DML (データ操作言語) を同時操作するとき、MARS を利用できません。 その場合、SQL Server は接続を強制終了し、トランザクションを中止します。   SQL Server 2012 には読み取り専用の列ストアインデックスがあり、MARS は適用されません。  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB プロバイダー  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、DBPROPSET_SQLSERVERDBINIT プロパティセットに実装されている SSPROP_INIT_MARSCONNECTION データソース初期化プロパティを追加することによって、MARS をサポートしています。 また、新しい接続文字列のキーワードとして **MarsConn** が追加されました。 **True**または**false**の値を受け取ります。既定値は**false**です。  
  
 データ ソース プロパティ DBPROP_MULTIPLECONNECTIONS の既定値は VARIANT_TRUE です。 これは、複数の同時実行コマンドや行セット オブジェクトをサポートするために、プロバイダーが複数の接続を起動することを意味しています。 MARS を有効にすると [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は、1つの接続で複数のコマンドと行セットオブジェクトをサポートできるため、MULTIPLE_CONNECTIONS は既定で VARIANT_FALSE に設定されます。  
  
 DBPROPSET_SQLSERVERDBINIT プロパティセットに対する拡張機能の詳細については、「[初期化プロパティと承認プロパティ](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)」を参照してください。  
  
### <a name="sql-server-native-client-ole-db-provider-example"></a>SQL Server Native Client OLE DB プロバイダーの例  
 この例では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のネイティブ OLE DB プロバイダーを使用してデータソースオブジェクトを作成し、セッションオブジェクトを作成する前に DBPROPSET_SQLSERVERDBINIT プロパティセットを使用して MARS を有効にします。  
  
```cpp
#include <sqlncli.h>  
  
IDBInitialize *pIDBInitialize = NULL;  
IDBCreateSession *pIDBCreateSession = NULL;  
IDBProperties *pIDBProperties = NULL;  
  
// Create the data source object.  
hr = CoCreateInstance(CLSID_SQLNCLI10, NULL,  
   CLSCTX_INPROC_SERVER,  
   IID_IDBInitialize,   
    (void**)&pIDBInitialize);  
  
hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void**)&pIDBProperties);  
  
// Set the MARS property.  
DBPROP rgPropMARS;  
  
// The following is necessary since MARS is off by default.  
rgPropMARS.dwPropertyID = SSPROP_INIT_MARSCONNECTION;  
rgPropMARS.dwOptions = DBPROPOPTIONS_REQUIRED;  
rgPropMARS.dwStatus = DBPROPSTATUS_OK;  
rgPropMARS.colid = DB_NULLID;  
V_VT(&(rgPropMARS.vValue)) = VT_BOOL;  
V_BOOL(&(rgPropMARS.vValue)) = VARIANT_TRUE;  
  
// Create the structure containing the properties.  
DBPROPSET PropSet;  
PropSet.rgProperties = &rgPropMARS;  
PropSet.cProperties = 1;  
PropSet.guidPropertySet = DBPROPSET_SQLSERVERDBINIT;  
  
// Get an IDBProperties pointer and set the initialization properties.  
pIDBProperties->SetProperties(1, &PropSet);  
pIDBProperties->Release();  
  
// Initialize the data source object.  
hr = pIDBInitialize->Initialize();  
  
//Create a session object from a data source object.  
IOpenRowset * pIOpenRowset = NULL;  
hr = IDBInitialize->QueryInterface(IID_IDBCreateSession, (void**)&pIDBCreateSession));  
hr = pIDBCreateSession->CreateSession(  
   NULL,             // pUnkOuter  
   IID_IOpenRowset,  // riid  
  &pIOpenRowset ));  // ppSession  
  
// Create a rowset with a firehose mode cursor.  
IRowset *pIRowset = NULL;  
DBPROP rgRowsetProperties[2];  
  
// To get a firehose mode cursor request a   
// forward only read only rowset.  
rgRowsetProperties[0].dwPropertyID = DBPROP_IRowsetLocate;  
rgRowsetProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
rgRowsetProperties[0].dwStatus = DBPROPSTATUS_OK;  
rgRowsetProperties[0].colid = DB_NULLID;  
VariantInit(&(rgRowsetProperties[0].vValue));  
rgRowsetProperties[0].vValue.vt = VARIANT_BOOL;  
rgRowsetProperties[0].vValue.boolVal = VARIANT_FALSE;  
  
rgRowsetProperties[1].dwPropertyID = DBPROP_IRowsetChange;  
rgRowsetProperties[1].dwOptions = DBPROPOPTIONS_REQUIRED;  
rgRowsetProperties[1].dwStatus = DBPROPSTATUS_OK;  
rgRowsetProperties[1].colid = DB_NULLID;  
VariantInit(&(rgRowsetProperties[1].vValue));  
rgRowsetProperties[1].vValue.vt = VARIANT_BOOL;  
rgRowsetProperties[1].vValue.boolVal = VARIANT_FALSE;  
  
DBPROPSET rgRowsetPropSet[1];  
rgRowsetPropSet[0].rgProperties = rgRowsetProperties  
rgRowsetPropSet[0].cProperties = 2  
rgRowsetPropSet[0].guidPropertySet = DBPROPSET_ROWSET;  
  
hr = pIOpenRowset->OpenRowset (NULL,  
   &TableID,  
   NULL,  
   IID_IRowset,  
   1,  
   rgRowsetPropSet  
   (IUnknown**)&pIRowset);  
```  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC ドライバー  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)および[Sqlgetconnectattr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)関数への追加によって MARS がサポートされています。 SQL_COPT_SS_MARS_ENABLED が追加され、SQL_MARS_ENABLED_YES または SQL_MARS_ENABLED_NO を受け取ります。既定値は SQL_MARS_ENABLED_NO です。 さらに、新しい接続文字列キーワード**Mars_Connection**が追加されました。 このキーワードは、"yes" と "no" を値として受け取ります。既定値は "no" です。  
  
### <a name="sql-server-native-client-odbc-driver-example"></a>SQL Server Native Client ODBC ドライバーの例  
 この例では、 **SQLSetConnectAttr**関数を使用して、 **SQLDriverConnect**関数を呼び出してデータベースに接続する前に、MARS を有効にします。 接続が確立されると、2つの**SQLExecDirect**関数が呼び出され、同じ接続に2つの異なる結果セットが作成されます。  
  
```cpp
#include <sqlncli.h>  
  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_MARS_ENABLED, SQL_MARS_ENABLED_YES, SQL_IS_UINTEGER);  
SQLDriverConnect(hdbc, hwnd,   
   "DRIVER=SQL Server Native Client 10.0;  
   SERVER=(local);trusted_connection=yes;", SQL_NTS, szOutConn,   
   MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt1);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt2);  
  
// The 2nd execute would have failed with connection busy error if  
// MARS were not enabled.  
SQLExecDirect(hstmt1, L"SELECT * FROM Authors", SQL_NTS);  
SQLExecDirect(hstmt2, L"SELECT * FROM Titles", SQL_NTS);  
  
// Result set processing can interleave.  
SQLFetch(hstmt1);  
SQLFetch(hstmt2);  
```  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client の機能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [SQL Server の既定の結果セットの使用](../../../relational-databases/native-client-odbc-cursors/implementation/using-sql-server-default-result-sets.md)  
  
  
