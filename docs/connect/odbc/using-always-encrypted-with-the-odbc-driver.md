---
title: SQL Server 用 ODBC ドライバーと共に Always Encrypted を使用する | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2018
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02e306b8-9dde-4846-8d64-c528e2ffe479
ms.author: v-chojas
author: MightyPen
ms.openlocfilehash: bf15831517ebaa8646c1d6f3c080033c3a41405d
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594379"
---
# <a name="using-always-encrypted-with-the-odbc-driver-for-sql-server"></a>SQL Server 用 ODBC ドライバーと共に Always Encrypted を使用する
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

### <a name="applicable-to"></a>適用対象

- ODBC Driver 13.1 for SQL Server
- ODBC Driver 17 for SQL Server

### <a name="introduction"></a>はじめに

この記事では、[Always Encrypted (データベース エンジン)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) または[セキュリティで保護されたエンクレーブが設定された Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md) と [ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md) を使用して ODBC アプリケーションを開発する方法について説明します。

Always Encrypted を使用すると、クライアント アプリケーションは SQL Server または Azure SQL データベースにデータまたは暗号化キーを開示することなく、機密データを暗号化することができます。 ODBC Driver for SQL Server など、Always Encrypted が有効なドライバーは、クライアント アプリケーション内の機密データを透過的に暗号化および暗号化解除することで、この処理を実行します。 ドライバーは、どのクエリ パラメーターが機密データベース列 (Always Encrypted を使用して保護される) に対応するかを自動的に決定し、SQL Server または Azure SQL データベースにデータを渡す前にこれらのパラメーターの値を暗号化します。 同様に、ドライバーは、クエリ結果内の暗号化されたデータベース列から取得されたデータを透過的に暗号化解除します。 "*セキュリティで保護されたエンクレーブが設定された*" Always Encrypted では、この機能を拡張して、データの機密性を保ちながら機密データに対してより豊富な機能を使えるようになります。

詳細については、「 [Always Encrypted (データベースエンジン)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 」および「 [Secure Enclaves での Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)」を参照してください。

### <a name="prerequisites"></a>Prerequisites

データベースで Always Encrypted を構成します。 この処理には、Always Encrypted キーのプロビジョニング、および選択したデータベース列の暗号化の設定が含まれます。 Always Encrypted が構成されたデータベースがない場合は、「 [Always Encrypted の作業の開始](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)」の手順に従います。 特に、ご利用のデータベースには、列マスターキー (CMK) 用、列暗号化キー (CEK) 用、およびその CEK を使用して暗号化された 1 つまたは複数の列を含むテーブル用のメタデータ定義を含める必要があります。

### <a name="enabling-always-encrypted-in-an-odbc-application"></a>ODBC アプリケーションで Always Encrypted を有効にする

パラメーターの暗号化と、結果セットの暗号化された列の暗号化解除を有効にするには、`ColumnEncryption` 接続文字列キーワードの値を **[有効]** に設定するのが最も簡単な方法です。 Always Encrypted を有効にする接続文字列の例を次に示します。

```
SQLWCHAR *connString = L"Driver={ODBC Driver 13 for SQL Server};Server={myServer};Trusted_Connection=yes;ColumnEncryption=Enabled;";
```

Always Encrypted は、DSN 構成内で同じキーと値 (接続文字列設定が存在する場合は、それによってオーバーライドされる) を使用して有効にすることも、`SQL_COPT_SS_COLUMN_ENCRYPTION` 接続前属性を使用してプログラムで有効にすることもできます。 それを次のように設定すると、接続文字列または DSN に設定されている値はオーバーライドされます。

```
 SQLSetConnectAttr(hdbc, SQL_COPT_SS_COLUMN_ENCRYPTION, (SQLPOINTER)SQL_COLUMN_ENCRYPTION_ENABLE, 0);
```

接続に対して有効にすると、個々のクエリに合わせて Always Encrypted の動作を調整することができます。 詳細については、「[Always Encrypted のパフォーマンスの影響を制御する](#controlling-the-performance-impact-of-always-encrypted)」を参照してください。

暗号化または暗号化解除を正常に行うには、Always Encrypted を有効にするだけでは不十分です。さらに、次のようになっていることを確認する必要があります。

- アプリケーションが、データベース内の Always Encrypted キーに関するメタデータへのアクセスに必要な *VIEW ANY COLUMN MASTER KEY DEFINITION* および *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* データベース権限を持っている。 詳細については、「[データベース権限](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)」を参照してください。

- アプリケーションで、クエリ対象の暗号化された列の CEK を保護する CMK にアクセスできる。 このことは、CMK を格納するキーストア プロバイダーに依存します。 詳細については、「[列マスター キー ストアを操作する](#working-with-column-master-key-stores)」を参照してください。

### <a name="enabling-always-encrypted-with-secure-enclaves"></a>セキュリティで保護されたエンクレーブが設定された Always Encrypted を有効にする

バージョン 17.4 以降のドライバーでは、セキュリティで保護されたエンクレーブが設定された Always Encrypted がサポートされています。 SQL Server 2019 以降に接続するときにエンクレーブを使用できるようにするには、`ColumnEncryption` DSN、接続文字列、または接続属性を、エンクレーブの種類と構成証明プロトコルの名前、および関連する構成証明書のデータをコンマで区切って設定します。 バージョン17.4 では、`VBS-HGS`によって示される、[仮想化ベースの Security](https://www.microsoft.com/security/blog/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/)エンクレーブ Type と[Host Guardian Service](https://docs.microsoft.com/windows-server/security/set-up-hgs-for-always-encrypted-in-sql-server)構成証明プロトコルのみがサポートされています。これを使用するには、構成証明サーバーの URL を指定します。次に例を示します。

```
Driver=ODBC Driver 17 for SQL Server;Server=yourserver.yourdomain;Trusted_Connection=Yes;ColumnEncryption=VBS-HGS,http://attestationserver.yourdomain/Attestation
```

サーバーと構成証明サービスが正しく構成されていて、目的の列に対してエンクレーブ対応 CMKs と CEKs が適切に構成されている場合は、次のように、エンクレーブを使用するクエリを実行できるようになりました。Always Encrypted によって提供される既存の機能。 詳細については[、「Configure Always Encrypted with secure enclaves](../../relational-databases/security/encryption/configure-always-encrypted-enclaves.md) 」を参照してください。


### <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>暗号化された列のデータを取得および変更する

接続で Always Encrypted を有効にすると、標準の ODBC Api を使用できるようになります。 ODBC Api では、暗号化されたデータベース列のデータを取得または変更できます。 次のドキュメントは、このような場合に役立ちます。

- [ODBC サンプルコード](cpp-code-example-app-connect-access-sql-db.md)
- [ODBC プログラマー リファレンス](../../odbc/reference/odbc-programmer-s-reference.md)

アプリケーションには、必要なデータベース権限が必要であり、列マスターキーにアクセスできる必要があります。 次に、ドライバーは、暗号化された列を対象とするすべてのクエリパラメーターを暗号化します。 ドライバーは、暗号化された列から取得したデータの暗号化も解除します。 ドライバーは、ソースコードからの支援を受けずに、すべての暗号化と復号化を実行します。 プログラムに対しては、列が暗号化されていないかのようになります。

Always Encrypted が有効でない場合、暗号化された列をターゲットとするパラメーターを含むクエリは失敗します。 暗号化された列をターゲットとするパラメーターがクエリにない場合は、暗号化された列からデータを取得できます。 ただし、ドライバーによって暗号化の解除は試みられず、アプリケーションでは暗号化されたバイナリ データを (バイト配列として) 受け取ることになります。

次の表は、Always Encrypted が有効かどうかに応じたクエリの動作をまとめたものです。

|クエリの特性 | Always Encrypted が有効になっており、アプリケーションがキーとキー メタデータにアクセスできる|Always Encrypted が有効になっており、アプリケーションがキーまたはキー メタデータにアクセスできない | Always Encrypted が無効になっている|
|:---|:---|:---|:---|
| 暗号化された列をターゲットとするパラメーター。 | パラメーター値は透過的に暗号化されます。 | エラー | エラー|
| 暗号化された列をターゲットとするパラメーターを含まない、暗号化された列からのデータの取得。| 暗号化された列の結果は透過的に暗号化解除されます。 アプリケーションでは、プレーン テキスト列の値を受け取ります。 | エラー | 暗号化された列の結果は暗号化解除されません。 アプリケーションは、暗号化された値をバイト配列として受け取ります。

次の例は、暗号化された列のデータを取得および変更する方法を示しています。 この例では、次のスキーマを持つテーブルを想定しています。 SSN 列と BirthDate 列が暗号化されていることに注意してください。

```
CREATE TABLE [dbo].[Patients](
 [PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] )
 GO
```

#### <a name="data-insertion-example"></a>データ挿入の例

この例では、Patients テーブルに列を挿入します。 次のことを考慮してください。

- このサンプル コードの暗号化に固有のものは何もありません。 暗号化された列をターゲットとする SSN および日付パラメータの値が、ドライバーによって自動的に検出されて、暗号化されます。 これにより、アプリケーションに対して暗号化が透過的に実行されます。

- 暗号化された列を含め、データベース列に挿入された値は、バインドされたパラメーターとして渡されます (「[SQLBindParameter 関数](https://msdn.microsoft.com/library/ms710963(v=vs.85).aspx)」を参照してください)。 暗号化されていない列に値を送信する場合、パラメーターの使用は省略可能です (ただし、SQL インジェクションを防ぐのに役立つので、強くお勧めします) が、暗号化された列をターゲットとする値に対しては必須です。 SSN 列または BirthDate 列に挿入された値がクエリ ステートメントに埋め込まれたリテラルとして渡された場合、ドライバーではクエリ内のリテラルの暗号化または処理が試行されないため、クエリは失敗します。 その結果、サーバーはこれらの値を、暗号化された列と互換性がないと見なして拒否します。

- SSN 列に挿入されるパラメーターの SQL 型は SQL_CHAR (**char** SQL Server データ型にマップされる) に設定されます (`rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);`)。 パラメーターの型が SQL_WCHAR (**nchar** にマップされる) に設定された場合、クエリは失敗します。暗号化された nchar 値から、暗号化された char 値へのサーバー側変換が Always Encrypted でサポートされていないためです。 データ型のマッピングについては、「[ODBC プログラマー リファレンス - 付録 D: データ型](https://msdn.microsoft.com/library/ms713607.aspx)」を参照してください。

```
    SQL_DATE_STRUCT date;
    SQLLEN cbdate;   // size of date structure  

    SQLCHAR SSN[12];
    strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

    SQLWCHAR* firstName = L"Catherine";
    SQLWCHAR* lastName = L"Abel";
    SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

    // Initialize the date structure  
    date.day = 10;
    date.month = 9;
    date.year = 1996;

    // Size of structures   
    cbdate = sizeof(SQL_DATE_STRUCT);

    SQLRETURN rc = 0;

    string queryText = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?) ";

    rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

    //SSN
    rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);
    //FirstName
    rc = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)firstName, 0, &cbFirstName);
    //LastName
    rc = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)lastName, 0, &cbLastName);
    //BirthDate
    rc = SQLBindParameter(hstmt, 4, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 10, 0, (SQLPOINTER)&date, 0, &cbdate);

    rc = SQLExecute(hstmt);
```

#### <a name="plaintext-data-retrieval-example"></a>プレーンテキスト データの取得の例

次の例は、暗号化された値に基づいてデータをフィルター処理し、暗号化された列からプレーンテキスト データを取得する方法を示しています。 次のことを考慮してください。

- SQLBindParameter を使用して SSN 列に対してフィルター処理するために WHERE 句で使用される値は、サーバーに送信する前にドライバーが透過的に暗号化できるように、パラメーターとして渡す必要があります。

- ドライバーが SSN 列と BirthDate 列から取得されたデータを透過的に暗号化解除するので、プログラムで出力される値はすべてプレーンテキストになります。

> [!NOTE]
> 暗号化が決定的である場合、または secure エンクレーブが有効になっている場合にのみ、クエリは暗号化された列に対して等価比較を実行できます。 詳細については、「[明確な暗号化またはランダム化された暗号化の選択](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)」を参照してください。

```
SQLCHAR SSN[12];
strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

SQLWCHAR* firstName = L"Catherine";
SQLWCHAR* lastName = L"Abel";
SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

SQLRETURN rc = 0;
string empty = "";
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] " + empty +
    "FROM  [dbo].[Patients]" +
    "WHERE " +
    "[SSN] = ? ";

rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

//SSN
rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);

rc = SQLExecute(hstmt);
HandleDiagnosticRecord(hstmt, SQL_HANDLE_STMT, rc);

SQL_DATE_STRUCT dateVal;
SQLWCHAR firstNameVal[50];
SQLWCHAR lastNameVal[50];
SQLCHAR SSNVal[12];
SQLLEN cbdate;   // size of date structure  

int rowcount = 0;
while (SQL_SUCCEEDED(SQLFetch(hstmt)))
{
    rowcount++;
    SQLGetData(hstmt, 1, SQL_C_CHAR, &SSNVal, 11, &cbSSN);
    SQLGetData(hstmt, 2, SQL_C_WCHAR, &firstNameVal, 50, &cbFirstName);
    SQLGetData(hstmt, 3, SQL_C_WCHAR, &lastNameVal, 50, &cbLastName);
    SQLGetData(hstmt, 4, SQL_C_TYPE_DATE, &dateVal, 10, &cbdate);        
}
```

#### <a name="ciphertext-data-retrieval-example"></a>暗号化テキスト データの取得の例

Always Encrypted が有効になっていない場合でも、暗号化された列をターゲットとするパラメーターがクエリになければ、クエリでは、暗号化された列からデータを取得できます。

次の例は、暗号化された列から暗号化されたバイナリ データを取得する方法を示しています。 次のことを考慮してください。

- 接続文字列で Always Encrypted が有効になっていないので、クエリは、SSN と BirthDate の暗号化された値をバイト配列として返します (プログラムによって値が文字列に変換されます)。
- Always Encrypted が無効の状態で、暗号化された列からデータを取得するクエリは、暗号化された列をターゲットとするパラメーターがない場合に限り、パラメーターを含むことができます。 上記のクエリは、データベースで暗号化されない LastName によってフィルター処理を行います。 クエリが SSN または BirthDate によってフィルター処理を行った場合、クエリは失敗します。


```
SQLCHAR SSN[12];
strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

SQLWCHAR* firstName = L"Catherine";
SQLWCHAR* lastName = L"Abel";
SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

SQLRETURN rc = 0;
string empty = "";
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] " + empty +
    "FROM  [dbo].[Patients]" +
    "WHERE " +
    "[LastName] = ?";

rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

//LastName
rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)lastName, 0, &cbLastName);

rc = SQLExecute(hstmt);
HandleDiagnosticRecord(hstmt, SQL_HANDLE_STMT, rc);

SQL_DATE_STRUCT dateVal;
SQLWCHAR firstNameVal[50];
SQLWCHAR lastNameVal[50];
SQLCHAR SSNVal[12];
SQLLEN cbdate;   // size of date structure  

int rowcount = 0;
while (SQL_SUCCEEDED(SQLFetch(hstmt)))
{
    rowcount++;
    SQLGetData(hstmt, 1, SQL_C_CHAR, &SSNVal, 11, &cbSSN);
    SQLGetData(hstmt, 2, SQL_C_WCHAR, &firstNameVal, 50, &cbFirstName);
    SQLGetData(hstmt, 3, SQL_C_WCHAR, &lastNameVal, 50, &cbLastName);
    SQLGetData(hstmt, 4, SQL_C_TYPE_DATE, &dateVal, 10, &cbdate);        
}
```

#### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>暗号化された列をクエリする際の一般的な問題を回避する

ここでは、暗号化された列を ODBC アプリケーションからクエリする際のエラーの一般的なカテゴリと、その対処方法に関するいくつかのガイドラインを示します。

##### <a name="unsupported-data-type-conversion-errors"></a>サポートされていないデータ型の変換エラー

Always Encrypted では、暗号化されたデータ型に対するいくつかの変換がサポートされています。 サポートされている型の変換の詳細な一覧については、「[Always Encrypted (データベース エンジン)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)」を参照してください。 データ型変換のエラーを回避するには、暗号化された列をターゲットとするパラメーターで SQLBindParameter を使用する場合、必ず次の点に注意してください。

- パラメーターの SQL 型については、ターゲットとする列の型とまったく同じであるか、または SQL 型から列の型への変換がサポートされている。

- `decimal` と `numeric` の SQL Server データ型の列をターゲットとするパラメーターの有効桁数と小数点以下桁数が、ターゲット列に対して構成された有効桁数と小数点と同じである。

- ターゲット列を変更するクエリで、`datetime2`、`datetimeoffset`、または `time` の SQL Server データ型の列をターゲットとするパラメーターの有効桁数が、ターゲット列の有効桁数以下である。  

##### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>暗号化された値の代わりにプレーンテキストを渡すことによるエラー

暗号化された列をターゲットとする値はいずれも、サーバーに送信する前に暗号化する必要があります。 暗号化された列でプレーンテキスト値の挿入、変更、フィルター処理を行おうとすると、エラーになります。 このようなエラーを防ぐには、次のことを確認してください。

- Always Encrypted が有効にされていること (特定の接続の `SQL_COPT_SS_COLUMN_ENCRYPTION` 接続属性、または特定のステートメントの `SQL_SOPT_SS_COLUMN_ENCRYPTION` ステートメント属性を設定して接続する前に DSN の接続文字列で)。

- SQLBindParameter を使用して、暗号化された列をターゲットとするデータを送信すること。 次の例は、SQLBindParameter に引数としてリテラルを渡す代わりに、暗号化された列 (SSN) でリテラル/定数によって不正なフィルター処理を行うクエリを示しています。

```
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

### <a name="precautions-when-using-sqlsetpos-and-sqlmoreresults"></a>SQLSetPos および SQLMoreResults を使用する際の注意事項

#### <a name="sqlsetpos"></a>SQLSetPos

`SQLSetPos` API を使用すると、SQLBindCol にバインドされ、行データが事前に取り込まれているバッファーを使用して結果セット内の行をアプリケーションで更新することができます。 暗号化された固定長型の非対称の埋め込み動作が原因で、これらの列のデータは、行内の他の列に対して更新が行われている間に、予期せずに変更される可能性があります。 AE では、固定長文字の値は、バッファー サイズより小さい場合に埋め込まれます。

この動作を軽減するには、`SQLBulkOperations` の一環として更新されない列、およびカーソル ベースの更新に `SQLSetPos` を使用する場合に更新されない列を無視するために、`SQL_COLUMN_IGNORE`フラグを使用します。  アプリケーションによって直接変更されない列はすべて無視する必要があります。パフォーマンス上の理由と、実際の (DB) サイズより*小さい*バッファーにバインドされている列の切り捨てを回避するための両面からそのようにします。 詳細については、[SQLSetPos 関数のリファレンス](https://msdn.microsoft.com/library/ms713507(v=vs.85).aspx)を参照してください。

#### <a name="sqlmoreresults--sqldescribecol"></a>SQLMoreResults と SQLDescribeCol

アプリケーション プログラムでは、準備されたステートメント内の列のメタデータを返すために、[SQLDescribeCol](https://msdn.microsoft.com/library/ms716289(v=vs.85).aspx) を呼び出す場合があります。  Always Encrypted が有効にされているとき、`SQLDescribeCol` を呼び出す "*前に*" `SQLMoreResults` を呼び出すと、[sp_describe_first_result_set](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) が呼び出されるため、暗号化された列のプレーンテキスト メタデータは正しく返されません。 この問題を回避するには、`SQLMoreResults` を呼び出す "*前に*" 準備されたステートメント上で `SQLDescribeCol` を呼び出します。

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>Always Encrypted のパフォーマンスの影響を制御する

Always Encrypted はクライアント側暗号化テクノロジであるため、ほとんどのパフォーマンス オーバーヘッドは、データベースではなくクライアント側で発生します。 暗号化および暗号化解除の操作のコストとは別に、クライアント側のパフォーマンス オーバーヘッドのその他の原因を次に示します。

- クエリ パラメーターのメタデータを取得するためのデータベースへの追加のラウンド トリップ。

- 列マスター キーにアクセスするための列マスター キー ストアの呼び出し。

このセクションでは、ODBC Driver for SQL Server の組み込みのパフォーマンス最適化、および上記の 2 つの要因によるパフォーマンスへの影響を制御する方法について説明します。

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>クエリ パラメーターのメタデータを取得するためのラウンド トリップを制御する

既定では、接続に対して Always Encrypted が有効になっている場合、ドライバーは、各パラメーター化クエリに対して [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) を呼び出し、クエリ ステートメント (パラメーター値を除く) を SQL Server に渡します。 このストアド プロシージャでは、クエリ ステートメントを分析して、パラメーターを暗号化する必要があるかどうかが判断され、必要がある場合は、ドライバーでパラメーターを暗号化できるようにするため、パラメーターごとに暗号化関連の情報が返されます。 上記の動作により、クライアント アプリケーションに対する次のような高度な透明性が確保されます: 暗号化された列をターゲットとする値がパラメーターでドライバーに渡される限り、アプリケーション (およびアプリケーション開発者) は、暗号化された列にどのクエリがアクセスするかを認識する必要はありません。

### <a name="per-statement-always-encrypted-behavior"></a>ステートメントごとの Always Encrypted 動作

パラメーター化クエリに対して暗号化メタデータを取得することによるパフォーマンスへの影響を制御するには、接続に対して Always Encrypted 動作が有効にされている場合、個々のクエリに対する Always Encrypted 動作を変更することができます。 これにより、暗号化された列をターゲットとするパラメーターを含むことがわかっているクエリに対してのみ `sys.sp_describe_parameter_encryption` が確実に呼び出されるようにすることができます。 ただし、これにより、暗号化の透明度が損なわれることに注意してください。データベース内の別の列を暗号化する場合は、スキーマの変更に合わせてアプリケーション コードの変更が必要になる可能性があります。

ステートメントの Always Encrypted 動作を制御するには、SQLSetStmtAttr を呼び出して、`SQL_SOPT_SS_COLUMN_ENCRYPTION` ステートメント属性を次のいずれかの値に設定します。

|[値]|[説明]|
|-|-|
|`SQL_CE_DISABLED` (0)|ステートメントに対して Always Encrypted は無効にされます|
|`SQL_CE_RESULTSETONLY` (1)|暗号化解除のみです。 結果セットと戻り値は暗号化解除され、パラメーターは暗号化されません|
|`SQL_CE_ENABLED` (3) | Always Encrypted は有効にされ、パラメーターと結果の両方に使用されます。|

Always Encrypted を有効にした接続から作成された新しいステートメント ハンドルは、既定では SQL_CE_ENABLED になります。 Always Encrypted を無効にした接続から作成された新しいステートメント ハンドルは、既定では SQL_CE_DISABLED になります (そして、それらのハンドルに対して Always Encrypted を有効にすることはできません)。

クライアント アプリケーションのクエリのほとんどが暗号化された列にアクセスする場合は、次の操作をお勧めします。

- `ColumnEncryption` 接続文字列キーワードを `Enabled` に設定します。

- 暗号化されたどの列にもアクセスしないステートメント上で、`SQL_SOPT_SS_COLUMN_ENCRYPTION` 属性を `SQL_CE_DISABLED` に設定します。 これにより、`sys.sp_describe_parameter_encryption` の呼び出しと、結果セット内の値の暗号化解除の試みとが両方とも無効にされます。
    
- 暗号化を必要とするパラメーターは何も含まれていないものの、暗号化された列からデータを取得するステートメント上で、`SQL_SOPT_SS_COLUMN_ENCRYPTION` 属性を `SQL_CE_RESULTSETONLY` に設定します。 これにより、`sys.sp_describe_parameter_encryption` の呼び出しとパラメーターの暗号化が無効にされます。 暗号化された列を含む結果は、引き続き暗号化が解除されたままです。

## <a name="always-encrypted-security-settings"></a>Always Encrypted のセキュリティ設定

### <a name="force-column-encryption"></a>列の暗号化の強制

パラメーターの暗号化を強制するには、SQLSetDescField 関数を呼び出して、`SQL_CA_SS_FORCE_ENCRYPT` 実装パラメーター記述子 (IPD) フィールドを設定します。 0 以外の値を使用すると、関連付けられたパラメーターに対する暗号化メタデータが返されない場合にドライバーからはエラーが返されます。

```
SQLHDESC ipd;
SQLGetStmtAttr(hStmt, SQL_ATTR_IMP_PARAM_DESC, &ipd, 0, 0);
SQLSetDescField(ipd, paramNum, SQL_CA_SS_FORCE_ENCRYPT, (SQLPOINTER)TRUE, SQL_IS_SMALLINT);   
```

パラメーターの暗号化が不要であることが SQL Server からドライバーに通知された場合、このパラメーターを使用するクエリは失敗します。 攻撃を受けた SQL Server がクライアントに不正な暗号化メタデータを提供すると、データ漏えいが引き起こされる可能性がありますが、これにより、そのようなセキュリティ攻撃に対する保護を強化します。

### <a name="column-encryption-key-caching"></a>列暗号化キーのキャッシュ

列暗号化キーを暗号化解除するための列マスター キー ストアの呼び出し回数を減らすために、ドライバーではプレーンテキスト CEK がメモリにキャッシュされます。 CEK キャッシュはドライバに対してグローバルであり、どの接続にも関連付けられていません。 ECEK をデータベース メタデータから受け取った後、ドライバーでは、まず、キャッシュ内の暗号化されたキー値に対応するプレーンテキスト CEK の検索が試みられます。 ドライバーでは、キャッシュ内で対応するプレーンテキスト CEK が見つからない場合にのみ、CMK を含むキー ストアが呼び出されます。

> [!NOTE]
> ODBC Driver for SQL Server では、2 時間のタイムアウト後にキャッシュ内のエントリが削除されます。 つまり、ECEK が指定されている場合、ドライバーはアプリケーションの有効期間中または 2 時間間隔のうち、どちらか短い方の期間中に 1 回だけキー ストアと交信します。

ODBC Driver 17.1 for SQL Server 以降、CEK がキャッシュ内に保持される秒数を指定する `SQL_COPT_SS_CEKCACHETTL` 接続属性を使用して CEK キャッシュ タイムアウトを調整することができます。 キャッシュにはグローバルな性質があるため、この属性はドライバーに対して有効などの接続ハンドルからも調整できます。 キャッシュ TTL を小さくすると、既存の CEK も新しい TTL を超える場合は削除されます。 0 の場合、CEK はキャッシュされません。

### <a name="trusted-key-paths"></a>信頼されたキー パス

ODBC Driver 17.1 for SQL Server 以降では、`SQL_COPT_SS_TRUSTEDCMKPATHS` 接続属性を使用すると、指定された CMK リスト (キー パスで識別された) のみを Always Encrypted 操作で使用するようにアプリケーションから要求できるようになります。 既定では、この属性は NULL です。つまり、ドライバーでは任意のキー パスが受け入れられます。 この機能を使用するには、許可されたキー パスを一覧する null 区切り null 終了のワイド文字列を指すように `SQL_COPT_SS_TRUSTEDCMKPATHS` を設定します。 この属性が指すメモリは、それが設定されている接続ハンドルを使用した暗号化操作または暗号化解除操作中に、有効な状態に維持される必要があります。その上で、サーバー メタデータによって指定された CMK パスはこのリスト内で大文字と小文字が区別されているかどうかがドライバーによって確認されます。 CMK パスがリストにない場合、操作は失敗します。 アプリケーションでは、この属性が指すメモリの内容を変更することで、属性を再設定することなく、その信頼された CMK リストを変更することができます。

## <a name="working-with-column-master-key-stores"></a>列マスター キー ストアを操作する

データを暗号化または暗号化解除する場合、ターゲット列に対して構成された CEK がドライバーによって取得される必要があります。 CEK は、データベース メタデータ内に暗号化された形式 (ECEK) で格納されます。 各 CEK には、暗号化する際に使用された対応する CMK があります。 [データベース メタデータ](../../t-sql/statements/create-column-master-key-transact-sql.md)に CMK 自体は格納されません。これにはキーストアの名前と、キーストアが CMK を検索するために使用できる情報のみが含まれます。

ECEK のプレーンテキスト値を取得するために、ドライバーでは、まず、CEK とそれに対応する CMK の両方についてメタデータが取得されます。次に、この情報を使用して CMK を含むキーストアと交信し、ECEK の暗号化を解除するように要求が出されます。 ドライバーとキーストアの通信は、キーストア プロバイダーを使用して行われます。

### <a name="built-in-keystore-providers"></a>組み込みのキーストア プロバイダー

ODBC Driver for SQL Server には、次の組み込みのキーストア プロバイダーが付属しています。

| [オブジェクト名] | [説明] | プロバイダー (メタデータ) 名 |可用性|
|:---|:---|:---|:---|
|Azure Key Vault |Azure Key Vault に CMK を格納します | `AZURE_KEY_VAULT` |Windows、macOS、Linux|
|Windows 証明書ストア|Windows キーストアに CMK をローカルに保存します| `MSSQL_CERTIFICATE_STORE`|Windows|

- ユーザー (またはデータベース管理者) は、列マスター キーのメタデータで構成されているプロバイダー名が正しいこと、および列マスター キー パスが、特定のプロバイダーに対するキー パス形式に準拠していることを確認する必要があります。 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md) ステートメントを発行した際に有効なプロバイダー名とキー パスを自動的に生成する、SQL Server Management Studio などのツールを使用してキーを構成することをお勧めします。

- アプリケーションがキー ストア内のキーにアクセスできることを確認する必要があります。 これには、キーストアに応じてキーまたはキー ストアへのアクセスをアプリケーションに許可したり、その他のキー ストア固有の構成手順を行ったりするプロセスが含まれる場合があります。 たとえば、Azure Key Vault にアクセスするには、正しい資格情報をキーストアに提供する必要があります。

### <a name="using-the-azure-key-vault-provider"></a>Azure Key Vault プロバイダーを使用する

Azure Key Vault (AKV) は、Always Encrypted の列マスター キーを格納および管理するための便利なオプションです (特にアプリケーションが Azure でホストされている場合)。 Linux、macOS、および Windows 向けの ODBC Driver for SQL Server には、Azure Key Vault 用の組み込みの列マスター キーストア プロバイダーが含まれています。 Always Encrypted に対して Azure Key Vault を構成する方法の詳細については、[Azure Key Vault の操作手順](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/)、[Key Vault の概要](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)、および [Azure Key Vault での列マスター キーの作成](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2)に関するページを参照してください。

> [!NOTE]
> ODBC ドライバーは、AKV 認証の Active Directory フェデレーションサービス (AD FS) をサポートしていません。 AKV に対して Azure Active Directory 認証を使用していて、Active Directory 構成にフェデレーションサービスが含まれている場合、認証が失敗する可能性があります。
> Linux および macOS 用のドライバー バージョン 17.2 以降の場合、`libcurl` は、このプロバイダーを使用する上で必要ですが、明示的な依存関係にはありません。ドライバーを使用した他の操作ではそれを必要としないからです。 `libcurl` に関するエラーが発生する場合は、それがインストールされていることを確認してください。

ドライバーでは、次の資格情報の種類を使用して Azure Key Vault への認証がサポートされます。

- ユーザー名/パスワード - この方法では、資格情報は Azure Active Directory ユーザーの名前とそのパスワードです。

- クライアント ID /シークレット - この方法では、資格情報はアプリケーションクライアント ID とアプリケーション シークレットです。

ドライバーが AKV に格納されている CMK を列暗号化に使用できるようにするには、次の接続文字列限定のキーワードを使用します。

|[資格情報の種類]| `KeyStoreAuthentication` |`KeyStorePrincipalId`| `KeyStoreSecret` |
|-|-|-|-|
|ユーザー名/パスワード| `KeyVaultPassword`|ユーザー プリンシパル名|Password|
|クライアント ID/シークレット| `KeyVaultClientSecret`|クライアント ID|シークレット|

#### <a name="example-connection-strings"></a>接続文字列の例

次の接続文字列は、2 種類の資格情報を使用して Azure Key Vault に対して認証する方法を示しています。

**クライアント ID/シークレット**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultClientSecret;KeyStorePrincipalId=<clientId>;KeyStoreSecret=<secret>
```

**ユーザー名/パスワード**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultPassword;KeyStorePrincipalId=<username>;KeyStoreSecret=<password>
```

CMK ストレージで AKV を使用する場合、ODBC アプリケーションに他の変更を加える必要はありません。

### <a name="using-the-windows-certificate-store-provider"></a>Windows 証明書ストア プロバイダーの使用

Windows 用の ODBC Driver for SQL Server には、`MSSQL_CERTIFICATE_STORE` と呼ばれる Windows 証明書ストア用の組み込みの列マスター キー ストア プロバイダーが含まれています (このプロバイダーは macOS または Linux では使用できません)。このプロバイダーを使用すると、CMK はクライアント コンピューター上にローカルに格納され、ドライバーでそれを使用するためにアプリケーションで追加の構成を行う必要はありません。 ただし、アプリケーションには、ストア内の証明書とその秘密キーへのアクセス権が必要です。 詳しくは、「[列マスター キーを作成して保存する (Always Encrypted)](https://docs.microsoft.com/sql/relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted)」をご覧ください。

### <a name="using-custom-keystore-providers"></a>カスタム キーストア プロバイダーの使用

ODBC Driver for SQL Server では、CEKeystoreProvider インターフェイスを使用したカスタムのサードパーティ製キーストア プロバイダーもサポートされています。 これにより、ドライバーが暗号化された列にアクセスする場合にキーストア プロバイダーを使用できるように、アプリケーションでキーストア プロバイダーの読み込み、クエリ、および構成を行うことができます。 アプリケーションはまた、SQL Server に格納するための CEK を暗号化し、ODBC で暗号化された列にアクセスする以外のタスクを実行するために、キーストア プロバイダーと直接やりとりする場合もあります。詳細については、「[カスタム キーストア プロバイダー](../../connect/odbc/custom-keystore-providers.md)」を参照してください。

カスタム キーストア プロバイダーとのやりとりには、2 つの接続属性が使用されます。 これらは次のとおりです。

- `SQL_COPT_SS_CEKEYSTOREPROVIDER`

- `SQL_COPT_SS_CEKEYSTOREDATA`

前者はキーストア プロバイダーを読み込んで、読み込まれたものを列挙するために使用され、後者はアプリケーションとプロバイダー間の通信を有効するために使用されます。 アプリケーションとプロバイダー間のやりとりには SQL Server との通信が必要ないため、これらの接続属性は、接続を確立する前後にいつでも使用できます。 ただし、ドライバーはまだ読み込まれていないため、接続前にこれらの属性を設定および取得すると、それらはドライバー マネージャーによって処理され、期待した結果が得られない場合があります。

#### <a name="loading-a-keystore-provider"></a>キーストア プロバイダーの読み込み

`SQL_COPT_SS_CEKEYSTOREPROVIDER` 接続属性を設定すると、クライアント アプリケーションでプロバイダー ライブラリを読み込み、そこに含まれるキーストア プロバイダーを使用できるようになります。

```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```

| 引数 | [説明] |
|:---|:---|
|`ConnectionHandle`|[入力] 接続ハンドル。 有効な接続ハンドルである必要がありますが、1 つの接続ハンドルを介して読み込まれたプロバイダーは、同じプロセス内の他のいずれからもアクセス可能です。|
|`Attribute`|[入力] 設定する属性: `SQL_COPT_SS_CEKEYSTOREPROVIDER` 定数。|
|`ValuePtr`|[入力] プロバイダー ライブラリのファイル名を指定する null 終了文字列へのポインター。 SQLSetConnectAttrA の場合、これは ANSI (マルチバイト) 文字列です。 SQLSetConnectAttrW の場合、これは Unicode (wchar_t) 文字列です。|
|`StringLength`|[入力] ValuePtr 文字列の長さ、または SQL_NTS。|

ドライバーは、プラットフォーム定義の動的なライブラリー読み込みメカニズム (Linux および macOS の場合は `dlopen()`、Windows の場合は `LoadLibrary()`) を使用して ValuePtr パラメーターで識別されたライブラリーの読み込みを試み、そこで定義されているプロバイダーを自身が認識しているプロバイダーのリストに追加します。 次のエラーが発生することがあります。

| エラー | [説明] |
|:--|:--|
|`CE203`|動的なライブラリを読み込めませんでした。|
|`CE203`|"CEKeyStoreProvider" エクスポート シンボルがライブラリ内で見つかりませんでした。|
|`CE203`|ライブラリ内の 1 つまたは複数のプロバイダーが既に読み込まれています。|

`SQLSetConnectAttr` からは、通常、エラーまたは成功を示す値が返され、標準的な ODBC 診断メカニズムを介して発生したエラーについては追加の情報が提供されます。

> [!NOTE]
> アプリケーション プログラマーは、任意のカスタム プロバイダーを必要とする任意のクエリを任意の接続を介して送信する前に、そのカスタム プロバイダーを確実に読み込んでおく必要があります。 このようにしないと、エラーが発生します。

| エラー | [説明] |
|:--|:--|
|`CE200`|キーストア プロバイダー %1 が見つかりません。 適切なキーストア プロバイダー ライブラリが読み込まれていることを確認します。|

> [!NOTE]
> キーストア プロバイダーの実装者は、ご自分のカスタム プロバイダーの名前に `MSSQL` を使用することを避けてください。 この用語は Microsoft による使用のみを目的として予約されており、将来の組み込みプロバイダーと競合する可能性があります。 カスタム プロバイダーの名前にこの用語を使用すると、ODBC 警告が発生する可能性があります。

#### <a name="getting-the-list-of-loaded-providers"></a>読み込まれたプロバイダーの一覧を取得する

この接続属性を取得すると、クライアント アプリケーションが、ドライバーに現在読み込まれているキーストア プロバイダー (組み込まれているものも含まれる) を特定できるようになります。これは、接続した後でのみ実行できます。

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```

| 引数 | [説明] |
|:---|:---|
|`ConnectionHandle`|[入力] 接続ハンドル。 有効な接続ハンドルである必要がありますが、1 つの接続ハンドルを介して読み込まれたプロバイダーは、同じプロセス内の他のいずれからもアクセス可能です。|
|`Attribute`|[入力] 取得する属性: `SQL_COPT_SS_CEKEYSTOREPROVIDER` 定数。|
|`ValuePtr`|[出力] 次に読み込まれたプロバイダー名を返す先のメモリを指すポインター。|
|`BufferLength`|[入力] バッファー ValuePtr バッファーの長さ。|
|`StringLengthPtr`|[出力] (Null 終了文字を除く) バイトの合計数を返すバッファーへのポインターで返される使用可能な\*ValuePtr します。 ValuePtr が null ポインターである場合、長さは返されません。 属性値が文字列であり、返す対象のバイト数が BufferLength から null 終了文字の長さを差し引いた値より大きい場合、\* ValuePtr 内のデータは、BufferLength から null 終了文字の長さを差し引いた長さに切り捨てられ、ドライバーによって null で終了されます。|

リスト全体を取得できるようにするために、すべての Get 操作で、現在のプロバイダーの名前が返され、内部カウンターがインクリメントされ次へと進みます。 このカウンターがリストの末尾に達すると、空の文字列 ("") が返され、カウンターはリセットされます。後続の Get 操作は、リストの先頭から再び続行されます。

### <a name="communicating-with-keystore-providers"></a>キーストア プロバイダーとの通信

`SQL_COPT_SS_CEKEYSTOREDATA` 接続属性を使用すると、クライアント アプリケーションで、読み込まれたキーストア プロバイダーと通信して追加のパラメーターやキー生成情報を構成できるようになります。クライアント アプリケーションとプロバイダー間の通信は、この接続属性を使用した Get 要求および Set 要求に基づき、シンプルな要求 - 応答プロトコルに従って行われます。 通信はクライアント アプリケーションによってのみ開始されます。

> [!NOTE]
> CEKeyStoreProvider が応答する ODBC 呼び出し (SQLGet/SetConnectAttr) の性質上、ODBC インターフェイスでは接続コンテキストの解決方法でのデータの設定のみがサポートされます。

アプリケーションは、CEKeystoreData 構造体を介し、ドライバーを通してキーストアプロバイダーと通信します。

```
typedef struct CEKeystoreData {
wchar_t *name;
unsigned int dataSize;
char data[];
} CEKEYSTOREDATA;
```

| 引数 | [説明] |
|:---|:---|
|`name`|[入力] 設定時にデータが送信される先のプロバイダーの名前。 取得時には無視されます。 null で終了するワイド文字列。|
|`dataSize`|[入力] 構造体に続くデータ配列のサイズ。|
|`data`|[入出力] 設定時にプロバイダーに送信されるデータ。 これは任意のデータとなる場合があります。ドライバーでは、データの解釈は試みられません。 取得時に、プロバイダーから読み取られたデータを受信するバッファー。|

#### <a name="writing-data-to-a-provider"></a>プロバイダーへのデータの書き込み

`SQL_COPT_SS_CEKEYSTOREDATA` 属性を使用した `SQLSetConnectAttr` 呼び出しでは、指定されたキーストア プロバイダーにデータの "パケット" が書き込まれます。
```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```

| 引数 | [説明] |
|:---|:---|
|`ConnectionHandle`| [入力] 接続ハンドル。 有効な接続ハンドルである必要がありますが、1 つの接続ハンドルを介して読み込まれたプロバイダーは、同じプロセス内の他のいずれからもアクセス可能です。|
|`Attribute`|[入力] 設定する属性: `SQL_COPT_SS_CEKEYSTOREDATA` 定数。|
|`ValuePtr`|[入力] CEKeystoreData 構造体を指すポインター。 構造体の名前フィールドでは、データが対象とされているプロバイダーが識別されます。|
|`StringLength`|[入力] SQL_IS_POINTER 定数|

エラーに関する追加の詳細情報は、[SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx) を介して取得できます。

> [!NOTE]
> プロバイダーでは必要に応じて接続ハンドルを使用して、書き込まれたデータを特定の接続に関連付けることができます。 これは、接続ごとの構成を実装する場合に役立ちます。 また、データを送信するのに使用した接続に関係なく、接続コンテキストが無視され、データが同じように扱われる場合もあります。 詳細については、「[コンテキストの関連付け](../../connect/odbc/custom-keystore-providers.md#context-association)」を参照してください。

#### <a name="reading-data-from-a-provider"></a>プロバイダーからのデータの読み取り

`SQL_COPT_SS_CEKEYSTOREDATA` 属性を使用して `SQLGetConnectAttr` を呼び出すと、"*最後に書き込まれた*" プロバイダーからデータの "パケット" が読み取られます。 何もなければ、関数シーケンス エラーが発生します。 キーストア プロバイダーの実装者には、他の副作用を引き起こすことなく読み取り操作のためにプロバイダーを選択する方法として 0 バイトの "ダミー書き込み" をサポートすることが理にかなっている場合、それをお勧めします。

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```

| 引数 | [説明] |
|:---|:---|
|`ConnectionHandle`|[入力] 接続ハンドル。 有効な接続ハンドルである必要がありますが、1 つの接続ハンドルを介して読み込まれたプロバイダーは、同じプロセス内の他のいずれからもアクセス可能です。|
|`Attribute`|[入力] 取得する属性: `SQL_COPT_SS_CEKEYSTOREDATA` 定数。|
|`ValuePtr`|[出力] プロバイダーから読み取られたデータが配置される CEKeystoreData 構造体を指すポインター。|
|`BufferLength`|[入力] SQL_IS_POINTER 定数|
|`StringLengthPtr`|[出力] BufferLength を返す先のバッファーを指すポインター。 *ValuePtr が null ポインターである場合、長さは返されません。|

呼び出し元は、CEKEYSTOREDATA 構造体をたどるのに十分な長さのバッファーを、書き込み先のプロバイダーに確実に割り当てる必要があります。 戻ると、その dataSize フィールドは、プロバイダーから読み取られたデータの実際の長さで更新されます。 エラーに関する追加の詳細情報は、[SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx) を介して取得できます。

このインターフェイスでは、アプリケーションとキーストア プロバイダーの間で転送されるデータの形式に対して追加の要件は設定されていません。 各プロバイダーでは、必要に応じて独自のプロトコル/データ フォーマットを定義できます。

独自のキーストア プロバイダーを実装する例については、「[カスタム キーストア プロバイダー](../../connect/odbc/custom-keystore-providers.md)」を参照してください。

## <a name="limitations-of-the-odbc-driver-when-using-always-encrypted"></a>Always Encrypted を使用するときの ODBC ドライバーの制限事項

### <a name="asynchronous-operations"></a>非同期操作
ODBC ドライバーでは、Always Encrypted で[非同期操作](../../relational-databases/native-client/odbc/creating-a-driver-application-asynchronous-mode-and-sqlcancel.md)の使用が許可されますが、Always Encrypted を有効にすると、操作に対してパフォーマンスの影響があります。 ステートメントの暗号化メタデータを特定する `sys.sp_describe_parameter_encryption` の呼び出しはブロックされており、ドライバーはサーバーからメタデータが返されるのを待ってから `SQL_STILL_EXECUTING` を返します。

### <a name="retrieve-data-in-parts-with-sqlgetdata"></a>SQLGetData を使用してパーツ内のデータを取得する
ODBC Driver 17 for SQL Server より前では、SQLGetData を使用してパーツ内の暗号化された文字およびバイナリの列を取得することはできません。 列のデータ全体を入れるのに十分な長さのバッファーを使用して、SQLGetData を 1 回だけ呼び出すことができます。

### <a name="send-data-in-parts-with-sqlputdata"></a>SQLPutData を使用してパーツ内にデータを送信する
ODBC Driver 17.3 for SQL Server より前では、SQLPutData を使用してパーツ内に挿入または比較用のデータを送信することはできません。 データ全体を入れるバッファーを使用して、SQLPutData を 1 回だけ呼び出すことができます。 暗号化された列に長いデータを挿入するには、次のセクションで説明する一括コピー API を入力データ ファイルと一緒に使用します。

### <a name="encrypted-money-and-smallmoney"></a>暗号化された money および smallmoney
暗号化された **money** 列または **smallmoney** 列をパラメーターの対象にすることはできません。それらのデータ型にマップされる特定の ODBC データ型がなく、結果としてオペランド型の不整合エラーが発生するためです。

## <a name="bulk-copy-of-encrypted-columns"></a>暗号化された列の一括コピー

ODBC Driver 17 for SQL Server 以降、[SQL 一括コピー関数](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)および **bcp** ユーティリティーの使用は Always Encrypted でサポートされています。 プレーンテキスト (挿入時に暗号化され、取得時に暗号化解除される) と暗号化テキスト (逐語的に転送される) は両方とも、一括コピー (bcp_&#42;) API および **bcp** ユーティリティを使用して挿入および取得することができます。

- 暗号化テキストを varbinary(max) 形式で取得するには (たとえば、別のデータベースに一括で読み込む場合)、`ColumnEncryption` オプションを指定せずに (またはそれを `Disabled` に設定して) BCP OUT 操作を実行します。

- プレーン テキストを挿入および取得し、必要に応じてドライバーに暗号化と暗号化解除を透過的に実行させるには、`ColumnEncryption` を `Enabled` に設定するだけで十分です。 BCP API の機能は、それ以外では変更されていません。

- 暗号化テキストを varbinary(max) 形式 (上記で取得したような) で挿入するには、`BCPMODIFYENCRYPTED` オプションを TRUE に設定して BCP IN 操作を実行します。 結果として得られたデータを暗号化解除できるようにするには、変換先列の CEK を、暗号化テキストを最初に取得したときの CEK と確実に同じにしてください。

**bcp** ユーティリティーを使用する場合: `ColumnEncryption` 設定を制御するには、-D オプションを使用して、必要な値を含む DSN を指定します。 暗号テキストを挿入するには、ユーザーの `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` 設定を確実に有効にします。

次の表は、暗号化された列を操作するときのアクションの要約を示しています。

|`ColumnEncryption`|BCP の方向|[説明]|
|----------------|-------------|-----------|
|`Disabled`|OUT (クライアントへ)|暗号化テキストを取得します。 観察対象のデータ型は **varbinary(max)** です。|
|`Enabled`|OUT (クライアントへ)|プレーンテキストを取得します。 ドライバーでは、列データが暗号化解除されます。|
|`Disabled`|IN (サーバーへ)|暗号化テキストを挿入します。 これは、暗号化されたデータの暗号化解除を必要とすることなく、不透明に移動することを目的としています。 `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` オプションがユーザーに対して設定されていないか、接続ハンドルに対して BCPMODIFYENCRYPTED が設定されていない場合、操作は失敗します。 詳しくは以下をご覧ください。|
|`Enabled`|IN (サーバーへ)|プレーン テキストを挿入します。 ドライバーで列データが暗号化されます。|

### <a name="the-bcpmodifyencrypted-option"></a>BCPMODIFYENCRYPTED オプション

データの破損を防ぐために、サーバーでは、通常、暗号化された列に暗号化テキストを直接挿入することは許可されていません。したがって、それを試みても失敗します。ただし、暗号化されたデータ BCP API を使用して一括読み込みする場合は、`BCPMODIFYENCRYPTED` [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) オプションを TRUE に設定することで、暗号化テキストを直接挿入できるようになり、ユーザー アカウント上で `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` オプションを設定するより暗号化されたデータが破損する危険性が少なくなります。 とはいえ、キーはデータと一致する必要があるため、一括挿入の後、およびさらに使用する前に、挿入されたデータの読み取り専用チェックを実行することをお勧めします。

詳しくは、「[Always Encrypted で保護された機微なデータの移行](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)」をご覧ください。

## <a name="always-encrypted-api-summary"></a>Always Encrypted API の概要

### <a name="connection-string-keywords"></a>接続文字列キーワード

|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|`ColumnEncryption`|指定できる値は `Enabled`/`Disabled` です。<br>`Enabled` -- 接続の Always Encrypted 機能を有効にします。<br>`Disabled` -- 接続の Always Encrypted 機能を無効にします。<br>*type*、*data* --(バージョン17.4 以降) では、secure エンクレーブと構成証明プロトコルの*種類*、および関連する構成証明データ*データ*を使用して Always Encrypted を有効にします。 <br><br>既定値は `Disabled` です。|
|`KeyStoreAuthentication` | 有効な値: `KeyVaultPassword`、`KeyVaultClientSecret` |
|`KeyStorePrincipalId` | `KeyStoreAuthentication`  = `KeyVaultPassword` の場合は、この値を有効な Azure Active Directory ユーザー プリンシパル名に設定します。 <br>`KeyStoreAuthetication`  = `KeyVaultClientSecret` の場合は、この値を有効な Azure Active Directory アプリケーション クライアント ID に設定します。 |
|`KeyStoreSecret` | `KeyStoreAuthentication`  = `KeyVaultPassword` の場合は、この値を対応するユーザー名のパスワードに設定します。 <br>`KeyStoreAuthentication`  = `KeyVaultClientSecret` の場合は、この値を、有効な Azure Active Directory アプリケーション クライアント ID に関連付けられたアプリケーション シークレットに設定します。 |


### <a name="connection-attributes"></a>接続属性

|[オブジェクト名]|型|[説明]|  
|----------|-------|----------|  
|`SQL_COPT_SS_COLUMN_ENCRYPTION`|接続前|`SQL_COLUMN_ENCRYPTION_DISABLE` (0) -- Always Encrypted を無効にします <br>`SQL_COLUMN_ENCRYPTION_ENABLE` (1) -- Always Encrypted を有効にします<br> *型*へのポインター、*データ*文字列--(バージョン17.4 以降) で secure エンクレーブを有効にします。|
|`SQL_COPT_SS_CEKEYSTOREPROVIDER`|接続後|[設定] CEKeystoreProvider の読み込みを試みます<br>[取得] CEKeystoreProvider 名を返します|
|`SQL_COPT_SS_CEKEYSTOREDATA`|接続後|[設定] CEKeystoreProvider にデータを書き込みます<br>[取得] CEKeystoreProvider からデータを読み取ります|
|`SQL_COPT_SS_CEKCACHETTL`|接続後|[設定] CEK キャッシュ TTL を設定します<br>[取得] 現在の CEK キャッシュ TTL を取得します|
|`SQL_COPT_SS_TRUSTEDCMKPATHS`|接続後|[設定] 信頼された CMK パス ポインターを設定します<br>[取得] 現在の信頼された CMK パス ポインターを取得します|

### <a name="statement-attributes"></a>ステートメント属性

|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|`SQL_SOPT_SS_COLUMN_ENCRYPTION`|`SQL_CE_DISABLED` (0) -- ステートメントに対して Always Encrypted が無効にされます <br>`SQL_CE_RESULTSETONLY` (1) -- 暗号化解除のみ。 結果セットと戻り値は暗号化解除され、パラメーターは暗号化されません <br>`SQL_CE_ENABLED` (3) -- Always Encrypted は有効にされ、パラメーターと結果の両方に使用されます|

### <a name="descriptor-fields"></a>記述子フィールド

|IPD フィールド|サイズ/型|既定値|[説明]|
|-|-|-|-|  
|`SQL_CA_SS_FORCE_ENCRYPT` (1236)|WORD (2 バイト)|0|0 (既定値) の場合: このパラメーターを暗号化するかどうかは、暗号化メタデータの可用性によって決まります。<br><br>ゼロ以外の場合: このパラメーターで暗号化メタデータが使用可能な場合、それは暗号化されます。 それ以外の場合、要求は次のエラーで失敗します: [CE300] [Microsoft][ODBC Driver 13 for SQL Server]必須の暗号化がパラメーターに指定されましたが、サーバーから暗号化メタデータが提供されませんでした。|

### <a name="bcp_control-options"></a>bcp_control オプション

|オプション名|既定値|[説明]|
|-|-|-|
|`BCPMODIFYENCRYPTED` (21)|FALSE|TRUE の場合、varbinary (max) 値を暗号化された列に挿入できるようにします。 FALSE の場合、正しい型と暗号化メタデータが提供されていない限り、挿入を阻止します。|

## <a name="see-also"></a>参照

- [Always Encrypted (データベース エンジン)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)
- [Always Encrypted 関連のブログ](https://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)
