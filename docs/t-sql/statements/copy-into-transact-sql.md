---
title: COPY INTO (Transact-SQL) (プレビュー)
titleSuffix: (SQL Data Warehouse) - SQL Server
description: Azure SQL Data Warehouse で COPY ステートメントを使用して、外部ストレージ アカウントからの読み込みを行います。
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COPY_TSQL
- COPY INTO
- COPY
- LOAD
dev_langs:
- TSQL
author: kevinvngo
ms.author: kevin
monikerRange: =sqlallproducts-allversions||=azure-sqldw-latest
ms.openlocfilehash: 4cdfba4070e8788687c453435b4a6d525aeb44fe
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321836"
---
# <a name="copy-transact-sql-preview"></a>COPY (Transact-SQL) (プレビュー)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

この記事では、Azure SQL Data Warehouse で COPY ステートメントを使用して、外部ストレージ アカウントからの読み込みを行う方法について説明します。 COPY ステートメントを使用すると、SQL Data Warehouse への高スループットのデータ インジェストで最大の柔軟性が確保されます。

> [!NOTE]  
> COPY ステートメントは、現在、パブリック プレビュー段階にあります。

## <a name="syntax"></a>構文  

```
COPY INTO [schema.]table_name
[(Column_list)] 
FROM ‘<external_location>’ [,...n]
WITH  
 ( 
 [FILE_TYPE = {'CSV' | 'PARQUET' | 'ORC'} ]
 [,FILE_FORMAT = EXTERNAL FILE FORMAT OBJECT ]  
 [,CREDENTIAL = (AZURE CREDENTIAL) ]
 [,ERRORFILE = '[http(s)://storageaccount/container]/errorfile_directory[/]] 
 [,ERRORFILE_CREDENTIAL = (AZURE CREDENTIAL) ]
 [,MAXERRORS = max_errors ] 
 [,COMPRESSION = { 'Gzip' | 'DefaultCodec'|’Snappy’}] 
 [,FIELDQUOTE = ‘string_delimiter’] 
 [,FIELDTERMINATOR =  ‘field_terminator’]  
 [,ROWTERMINATOR = ‘row_terminator’]
 [,FIRSTROW = first_row]
 [,DATEFORMAT = ‘date_format’] 
 [,ENCODING = {'UTF8'|'UTF16'}] 
 [,IDENTITY_INSERT = {‘ON’ | ‘OFF’}]
)
```

## <a name="arguments"></a>引数  

*schema_name*  
操作を実行するユーザーの既定のスキーマが、指定したテーブルのスキーマと同じ場合は省略可能です。 "*スキーマ*" を指定せず、さらに COPY 操作を実行するユーザーの既定のスキーマが、指定したテーブルのスキーマと異なる場合、COPY は取り消され、エラー メッセージが返されます。  

*table_name*  
データの COPY 先のテーブルの名前です。 ターゲット テーブルは、一時テーブルまたはパーマネント テーブルであり、データベースに既に存在している必要があります。 

*(column_list)*  
データ読み込み時のソース データ フィールドからターゲット テーブル列へのマッピングに使用される 1 つ以上の列のリストです。このリストは省略可能です。 *column_list* はかっこで囲み、コンマで区切る必要があります。 列リストの形式は次のとおりです。

[(Column_name [Default_value] [Field_number] [,...n])]

- *Column_name* - ターゲット テーブルの列の名前。
- *Default_value* - 入力ファイルの任意の NULL 値がこの既定値に置き換えられます。 既定値はすべてのファイル形式に適用されます。 COPY によって入力ファイルから NULL の読み込みが試行されるのは、列リストに省略されている列がある場合、または入力ファイルに空フィールドがある場合です。
- *Field_number* - ターゲット列の名前にマップされる入力ファイル フィールド番号。
- フィールドのインデックスは 1 から開始されます。

列リストが指定されていない場合、COPY では、ソースとターゲットの順序性に基づいて列がマップされます。入力フィールド 1 はターゲット列 1 に、フィールド 2 は列 2 に、以降同様にマップされます。

*External locations(s)*</br>
データを含むファイルがステージングされる場所です。 現在、Azure Data Lake Storage (ADLS) Gen2 と Azure Blob Storage がサポートされています。

- Blob Storage の *External location*: https://<account>.blob.core.windows.net/<container>/<path>
- ADLS Gen2 の *External location*: https://<account>. dfs.core.windows.net/<container>/<path>

> [!NOTE]  
> BLOB エンドポイントは ADLS Gen2 で使用できます。これは下位互換性のためにのみ用意されています。 最適なパフォーマンスを得るには、ADLS Gen2 に対して **dfs** エンドポイントを使用してください。

- *Account* - ストレージ アカウント名

- *Container* - BLOB コンテナー名

- *Path* - データのフォルダーまたはファイルのパス。 場所はコンテナーから始まります。 フォルダーが指定されている場合は、そのフォルダーとそのサブフォルダーにあるすべてのファイルが、COPY によって取得されます。 隠しフォルダーは無視され、アンダースコア (_) またはピリオド (.) で始まるファイルは返されません (パスで明示的に指定されている場合を除く)。 この動作は、ワイルドカードを使ってパスを指定した場合も同じです。

パスにはワイルドカードを含めることができます

- ワイルドカード パス名の一致では、大文字と小文字が区別されます
- ワイルドカードをエスケープするには、円記号 (\\) を使用します
- ワイルドカードの展開は再帰的に適用されます。 たとえば、次のようにパスを指定すると、Customer1 (Customer1 のサブディレクトリを含む) の下にある CSV ファイルすべてが読み込まれます: Account/Container/Customer1/*.csv

> [!NOTE]  
> 最適なパフォーマンスを得るには、多くのファイルに展開されるワイルドカードは指定しないでください。 可能な場合は、ワイルドカードではなく、複数のファイルの場所をリストを使って指定します。

複数のファイルの場所を指定するには、次のようなコンマ区切りのリストを使用して、同じストレージ アカウントおよびコンテナーから指定する必要があります。

- https://<account>.blob.core.windows.net/<container>/<path>、 https://<account>.blob.core.windows.net/<container>/<path> など

*FILE_TYPE = { ‘CSV’ | ‘PARQUET’ | ‘ORC’ }*</br>
*FILE_TYPE* により、外部データの形式が指定されます。

- CSV: [RFC 4180](https://tools.ietf.org/html/rfc4180) 標準に準拠しているコンマ区切り値ファイルを指定します。
- PARQUET: Parquet 形式を指定します。
- ORC: 最適化行多桁式 (ORC) 形式を指定します。

>[!NOTE]  
> Polybase のファイルの種類である "区切りテキスト" は "CSV" ファイル形式に置き換えられています。このファイル形式で既定のコンマ区切り記号を構成するには、FIELDTERMINATOR パラメーターを使用します。 

*FILE_FORMAT = external_file_format_name*</br>
*FILE_FORMAT* は Parquet ファイルおよび ORC ファイルにのみ適用され、外部データのファイルの種類と圧縮方法を格納する外部ファイル形式オブジェクトの名前を指定します。 外部ファイル形式を作成するには、[CREATE EXTERNAL FILE FORMAT](create-external-file-format-transact-sql.md?view=azure-sqldw-latest) を使用します。

*CREDENTIAL (IDENTITY = ‘’, SECRET = ‘’)*</br>
*CREDENTIAL* は、外部ストレージ アカウントにアクセスするための認証メカニズムを指定します。 認証方法を次に示します。

|                          |                CSV                |              Parquet              |                ORC                |
| :----------------------: | :-------------------------------: | :-------------------------------: | :-------------------------------: |
|  **Azure Blob Storage**  | SAS/MSI/サービス プリンシパル/キー/AAD |              SAS/キー              |              SAS/キー              |
| **Azure Data Lake Gen2** | SAS/MSI/サービス プリンシパル/キー/AAD | SAS/MSI/サービス プリンシパル/キー/AAD | SAS/MSI/サービス プリンシパル/キー/AAD |

AAD またはパブリック ストレージ アカウントを使用して認証する場合は、CREDENTIAL を指定する必要はありません。 

- Shared Access Signatures (SAS) を使用した認証 *IDENTITY: *"Shared Access Signature" の値が含まれている定数 
  *SECRET: *[*Shared Access Signature*](/azure/storage/common/storage-sas-overview) "*を使用すると、ストレージ アカウント内のリソースへの委任アクセスが可能になります。* "
  最低限必要な権限: READ および LIST

- [*サービス プリンシパル*](/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store#create-a-credential)を使用した認証

  *IDENTITY: <ClientID>@<OAuth_2.0_Token_EndPoint> *
  *SECRET: *AAD アプリケーション サービス プリンシパルキー。最低限必要な RBAC ロール: ストレージ BLOB データ共同作成者、ストレージ BLOB データ所有者、またはストレージ BLOB データ閲覧者

  > [!NOTE]  
  > OAuth 2.0 トークン エンドポイント **V1** を使用してください

- ストレージ アカウント キーを使用した認証 *IDENTITY: *"ストレージ アカウント キー" の値が含まれている定数 
  *SECRET: *ストレージ アカウント キー
  
- [マネージド ID ](/azure/sql-data-warehouse/load-data-from-azure-blob-storage-using-polybase#authenticate-using-managed-identities-to-load-optional) (VNet サービス エンドポイント) を使用した認証 *IDENTITY:* "マネージド ID" の値が含まれている定数。最低限必要な RBAC ロール: AAD 登録済み SQL Database サーバーに対するストレージ BLOB データ共同作成者、ストレージ BLOB データ所有者、またはストレージ BLOB データ閲覧者 
  
- AAD ユーザーを使用した認証 *CREDENTIAL は必須ではありません*。最低限必要な RBAC ロール: AAD ユーザーに対するストレージ BLOB データ共同作成者、ストレージ BLOB データ所有者、またはストレージ BLOB データ閲覧者

*ERRORFILE = Directory Location*</br>
*ERRORFILE* は CSV にのみ適用されます。 COPY ステートメント内でディレクトリを指定します。拒否された行と該当するエラー ファイルがそこに書き込まれます。 ストレージ アカウントからの完全なパスを指定することも、コンテナーを基準とした相対パスを指定することもできます。 指定したパスが存在しない場合は、自動的に作成されます。 "_rejectedrows" という名前で子ディレクトリが作成されます。"_ " 文字があることで、場所パラメーターで明示的に指定されない限り、他のデータ処理ではこのディレクトリがエスケープされます。 

このディレクトリ内には、YearMonthDay -HourMinuteSecond (例: 20180330-173205) のロード サブミッション時間に基づいて作成されたフォルダーがあります。 このフォルダーには、理由 (エラー) ファイルとデータ (行) ファイルの 2 種類のファイルが書き込まれ、それぞれ queryID、distributionID、ファイル GUID が事前に追加されています。 データと理由が別々のファイル内にあり、対応するファイルはプレフィックスが一致しています。

ERRORFILE でストレージ アカウントの完全なパスが定義されている場合、そのストレージへの接続には ERRORFILE_CREDENTIAL が使用されます。 それ以外の場合は、CREDENTIAL に指定された値が使用されます。

*ERRORFILE_CREDENTIAL = (IDENTITY= ‘’, SECRET = ‘’)*</br>
*ERRORFILE_CREDENTIAL* は、CSV ファイルにのみ適用されます。 サポートされているデータ ソースと認証方法は次のとおりです。

- Azure Blob Storage - SAS/サービス プリンシパル/キー/AAD
- Azure Data Lake Gen2 - SAS/MSI/サービス プリンシパル/キー/AAD
  
- Shared Access Signatures (SAS) を使用した認証
  - *IDENTITY:* "Shared Access Signature" の値が含まれている定数
  - *SECRET:* [*Shared Access Signature*](/azure/storage/common/storage-sas-overview) "*を使用すると、ストレージ アカウント内のリソースへの委任アクセスが可能になります。* "
  - 最低限必要な権限: READ、LIST、WRITE、CREATE、DELETE
  
- [*サービス プリンシパル*](/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store#create-a-credential)を使用した認証
  - *IDENTITY: <ClientID>@<OAuth_2.0_Token_EndPoint>*
  - *SECRET:* AAD サービス プリンシパル アプリケーション キー
  - 最低限必要な RBAC ロール: ストレージ BLOB データ共同作成者またはストレージ BLOB データ所有者
  
> [!NOTE]  
> OAuth 2.0 トークン エンドポイント **V1** を使用してください

- ストレージ アカウント キーを使用した認証
  - *IDENTITY:* "ストレージ アカウント キー" の値が含まれている定数
  - *SECRET:* ストレージ アカウント キー
  
- [マネージド ID](/azure/sql-data-warehouse/load-data-from-azure-blob-storage-using-polybase#authenticate-using-managed-identities-to-load-optional) (VNet サービス エンドポイント) を使用した認証
  - *IDENTITY:* "マネージド ID" の値が含まれている定数
  - 最低限必要な RBAC ロール: AAD 登録済み SQL Database サーバーに対するストレージ BLOB データ共同作成者またはストレージ BLOB データ所有者
  
- AAD ユーザーを使用した認証
  - *CREDENTIAL は必須ではありません*
  - 最低限必要な RBAC ロール: AAD ユーザーに対するストレージ BLOB データ共同作成者またはストレージ BLOB データ所有者

> [!NOTE]  
> ご自身の ERRORFILE に同じストレージ アカウントを使用し、コンテナーのルートを基準とした ERRORFILE パスを指定している場合は、ERROR_CREDENTIAL を指定する必要はありません。

*MAXERRORS = max_errors*</br>
*MAXERRORS* では、読み込みで拒否できる行の最大数を指定します。この最大数に達すると、COPY 操作は取り消されます。 COPY 操作でインポートできない行は無視され、それぞれ 1 つのエラーとしてカウントされます。 max_errors が指定されていない場合、既定値は 0 です。

*COMPRESSION = { 'DefaultCodec '| ’Snappy’ | ‘GZIP’ | ‘NONE’}*</br>
*COMPRESSION* は省略可能で、外部データのデータ圧縮方法を指定します。

- CSV は GZIP をサポートしています
- Parquet は GZIP および Snappy をサポートしています
- ORC は DefaultCodec および Snappy をサポートしています。
- Zlib は ORC の既定の圧縮です

このパラメーターが指定されていない場合、COPY コマンドでは、ファイル名拡張子に基づいて圧縮の種類が自動検出されます。

- .gz - **GZIP**
- .snappy - **Snappy**
- .deflate - **DefaultCodec**

 *FIELDQUOTE = 'field_quote'*</br>
*FIELDQUOTE* は CSV に適用され、CSV ファイルで引用符文字 (文字列の区切り記号) として使用される 1 バイト文字を指定します。 指定されていない場合は、RFC 4180 標準の定義に従って引用符文字 (") が引用符文字として使用されます。 拡張 ASCII 文字は、FIELDQUOTE の UTF-8 ではサポートされていません。

> [!NOTE]  
> FIELDQUOTE 文字は、2 バイト FIELDQUOTE (区切り記号) が存在する文字列型の列ではエスケープされます。 

*FIELDTERMINATOR = 'field_terminator’*</br>
*FIELDTERMINATOR* は CSV にのみ適用されます。 CSV ファイルで使用されるフィールド ターミネータを指定します。 フィールド ターミネータは、16 進数表記を使用して指定できます。 フィールド ターミネータにはマルチ文字を使用できます。 既定のフィールド ターミネータは (,) です。
詳細については、「[フィールド ターミネータと行ターミネータの指定 (SQL Server)](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md?view=sql-server-2017)」を参照してください。

ROW TERMINATOR = 'row_terminator'</br>
*ROW TERMINATOR* は CSV にのみ適用されます。 CSV ファイルで使用される行ターミネータを指定します。 行ターミネータは、16 進数表記を使用して指定できます。 行ターミネータにはマルチ文字を使用できます。 既定では、行ターミネータは \r\n です。 

COPY コマンドでは、\n (改行) を指定すると、その前に \r 文字が付けられ、\r\n になります。 \n 文字のみを指定するには、16 進数表記 (0x0A) を使用します。 マルチ文字の行ターミネータを 16 進数で指定する場合は、各文字の間で 0x を指定しないでください。

行ターミネータの指定に関する追加のガイダンスについては、次の[ドキュメント](https://docs.microsoft.com/sql/relational-databases/import-export/specify-field-and-row-terminators-sql-server?view=sql-server-2017#using-row-terminators)を参照してください。

*FIRSTROW  = First_row_int*</br>
*FIRSTROW* は CSV に適用され、COPY コマンドに対して、すべてのファイルで最初に読み取られる行番号を指定します。 値は 1 から始まり、これが既定値です。 2 に設定すると、データが読み込まれるときに、すべてのファイルの最初の行 (ヘッダー行) がスキップされます。 行は、行ターミネータの存在に基づいてスキップされます。

*DATEFORMAT = { ‘mdy’ | ‘dmy’ | ‘ymd’ | ‘ydm’ | ‘myd’ | ‘dym’ }*</br>
DATEFORMAT は CSV にのみ適用され、SQL Server 日付形式に対する日付の日付形式のマッピングを指定します。 Transact-SQL の日付と時刻のデータ型および関数の概要については、「[日付と時刻のデータ型および関数 (Transact-SQL)](../functions/date-and-time-data-types-and-functions-transact-sql.md?view=sql-server-ver15)」を参照してください。 COPY コマンド内の DATEFORMAT は、[セッション レベルで構成された DATEFORMAT](set-dateformat-transact-sql.md?view=sql-server-ver15) よりも優先されます。

*ENCODING = ‘UTF8’ | ‘UTF16’*</br>
*ENCODING* は CSV にのみ適用されます。 既定値は UTF8 です。 COPY コマンドによって読み込まれたファイルのデータ エンコード標準を指定します。 

*IDENTITY_INSERT = ‘ON’ | ‘OFF’*</br>
IDENTITY_INSERT は、インポートしたデータ ファイルの ID 値 (複数可) を ID 列に使用するかどうかを指定します。 IDENTITY_INSERT が OFF (既定値) の場合、この列の ID 値は検証されますが、インポートされません。 テーブル作成時に指定されたシード値と増分値に基づいて、固有の値が SQL DW によって自動的に割り当てられます。 COPY コマンドによる次の動作に注意してください。

- IDENTITY_INSERT が OFF で、テーブルに ID 列がある場合
  - 入力フィールドを ID 列にマップしない列リストを指定する必要があります。
- IDENTITY_INSERT が ON で、テーブルに ID 列がある場合
  - 列リストが渡された場合、入力フィールドを ID 列にマップする必要があります。
- 列リストの IDENTITY COLUMN に対して既定値がサポートされない。
- IDENTITY_INSERT は一度に 1 つのテーブルに対してのみ設定できる。

### <a name="permissions"></a>アクセス許可  

コピー コマンドを実行するユーザーには次の権限が必要です。 

- [ADMINISTER DATABASE BULK OPERATIONS](grant-database-permissions-transact-sql.md?view=azure-sqldw-latest#remarks)
- [INSERT ](grant-database-permissions-transact-sql.md?view=azure-sqldw-latest#remarks)

INSERT 権限および ADMINISTER BULK OPERATIONS 権限が必要です。 Azure SQL Data Warehouse では、INSERT 権限と ADMINISTER DATABASE BULK OPERATIONS 権限が必要です。

## <a name="examples"></a>例  

### <a name="a-load-from-a-public-storage-account"></a>A. パブリック ストレージ アカウントから読み込む

次の例は COPY コマンドの最も単純な形式で、パブリック ストレージ アカウントからデータを読み込みます。 この例では、COPY ステートメントの既定値は、行項目 csv ファイルの形式と一致しています。

```sql
COPY INTO dbo.[lineitem] FROM 'https://unsecureaccount.blob.core.windows.net/customerdatasets/folder1/lineitem.csv'
```

COPY コマンドの既定値を次に示します。

- DATEFORMAT = Session DATEFORMAT 

- MAXERRORS = 0

- COMPRESSION の既定値は圧縮解除です

- FIELDQUOTE = “” 

- FIELDTERMINATOR = “,” 

- ROWTERMINATOR = ‘\n'

> [!IMPORTANT]
> 内部的には COPY では ' \n ' が ' \r\n ' として処理されます。 詳細については、ROWTERMINATOR セクションを参照してください。

- FIRSTROW = 1

- ENCODING = ‘UTF8’

- FILE_TYPE = ‘CSV’

- IDENTITY_INSERT = ‘OFF’

### <a name="b-load-authenticating-via-share-access-signature-sas"></a>B. Shared Access Signature (SAS) を介して認証を読み込む

次の例では、UNIX 出力などのように、改行を行ターミネータとして使用するファイルを読み込みます。 また、SAS キーを使用して Azure Blob Storage に対して認証を行います。

```sql
COPY INTO test_1
FROM 'https://myaccount.blob.core.windows.net/myblobcontainer/folder1/'
WITH (
    FILE_TYPE = 'CSV',
    CREDENTIAL=(IDENTITY= 'Shared Access Signature', SECRET='<Your_SAS_Token>'),
    --CREDENTIAL should look something like this:
    --CREDENTIAL=(IDENTITY= 'Shared Access Signature', SECRET='?sv=2018-03-28&ss=bfqt&srt=sco&sp=rl&st=2016-10-17T20%3A14%3A55Z&se=2021-10-18T20%3A19%3A00Z&sig=IEoOdmeYnE9%2FKiJDSHFSYsz4AkNa%2F%2BTx61FuQ%2FfKHefqoBE%3D'),
    FIELDQUOTE = '"',
    FIELDTERMINATOR=';',
    ROWTERMINATOR='0X0A',
    ENCODING = 'UTF8',
    DATEFORMAT = 'ymd',
    MAXERRORS = 10,
    ERRORFILE = '/errorsfolder/',--path starting from the storage container
    IDENTITY_INSERT = 'ON'
)
```

### <a name="c-load-with-a-column-list-with-default-values-authenticating-via-storage-account-key"></a>C. ストレージ アカウント キーを介して認証を行い、既定値が含まれる列リストを使用して読み込む

この例では、既定値が含まれる列リストを指定してファイルを読み込みます。 

```sql
--Note when specifying the column list, input field numbers start from 1
COPY INTO test_1 (Col_one default 'myStringDefault' 1, Col_two default 1 3)
FROM 'https://myaccount.blob.core.windows.net/myblobcontainer/folder1/'
WITH (
    FILE_TYPE = 'CSV',
    CREDENTIAL=(IDENTITY= 'Storage Account Key', SECRET='<Your_Account_Key>'),
    --CREDENTIAL should look something like this:
    --CREDENTIAL=(IDENTITY= 'Storage Account Key', SECRET='x6RWv4It5F2msnjelv3H4DA80n0PQW0daPdw43jM0nyetx4c6CpDkdj3986DX5AHFMIf/YN4y6kkCnU8lb+Wx0Pj+6MDw=='),
    FIELDQUOTE = '"',
    FIELDTERMINATOR=',',
    ROWTERMINATOR='0x0A',
    ENCODING = 'UTF8',
    FIRSTROW = 2
)
```

### <a name="d-load-parquet-or-orc-using-existing-file-format-object"></a>D. 既存のファイル形式オブジェクトを使用して Parquet または ORC を読み込む

 この例では、ワイルドカードを使用して、フォルダーにあるすべての parquet ファイルを読み込みます。 

```sql
COPY INTO test_parquet
FROM 'https://myaccount.blob.core.windows.net/myblobcontainer/folder1/*.parquet'
WITH (
    FILE_FORMAT = myFileFormat
    CREDENTIAL=(IDENTITY= 'Shared Access Signature', SECRET='<Your_SAS_Token>')
)
```

### <a name="e-load-specifying-wild-cards-and-multiple-files"></a>E. ワイルドカードと複数のファイルを指定して読み込む

```sql
COPY INTO t1
FROM 
'https://myaccount.blob.core.windows.net/myblobcontainer/folder0/*.txt', 
    'https://myaccount.blob.core.windows.net/myblobcontainer/folder1'
WITH ( 
    FILE_TYPE = 'CSV'
    CREDENTIAL=(IDENTITY= '<client_id>@<OAuth_2.0_Token_EndPoint>',SECRET='<key>'),
    FIELDTERMINATOR = '|'
)
```

## <a name="faq"></a>よく寄せられる質問

### <a name="what-is-the-performance-of-the-copy-command-compared-to-polybase"></a>PolyBase と比較した場合の COPY コマンドのパフォーマンスについて教えてください。
COPY コマンドを使用すると、機能が一般公開される時点までにはパフォーマンスが向上します。 パブリック プレビュー中に最適な読み込みパフォーマンスを得るには、CSV の読み込み時に複数のファイルに入力を分割することを検討してください。 現在、INSERT SELECT を使用する場合のパフォーマンスは、PolyBase と同等です。 

### <a name="what-is-the-file-splitting-guidance-for-the-copy-command-loading-csv-files"></a>CSV ファイルを読み込む COPY コマンドに関するファイルの分割ガイダンスについて教えてください。
ファイル数に関するガイダンスを、次の表で説明します。 推奨されるファイル数に到達すると、大きいファイル程パフォーマンスが向上します。 COPY コマンドが一般公開されている場合、圧縮されていないファイルを分割する必要はありません。 

| **DWU** | **#Files** |
| :-----: | :--------: |
|   100   |     60     |
|   200   |     60     |
|   300   |     60     |
|   400   |     60     |
|   500   |     60     |
|  1,000  |    120     |
|  1,500  |    180     |
|  2,000  |    240     |
|  2,500  |    300     |
|  3,000  |    360     |
|  5,000  |    600     |
|  6,000  |    720     |
|  7,500  |    900     |
| 10,000  |    1200    |
| 15,000  |    1800    |
| 30,000  |    3600    |


### <a name="what-is-the-file-splitting-guidance-for-the-copy-command-loading-parquet-or-orc-files"></a>Parquet ファイルまたは ORC ファイルを読み込む COPY コマンドに関するファイルの分割ガイダンスについて教えてください。
COPY コマンドによって自動的にファイルが分割されるため、Parquet ファイルと ORC ファイルを分割する必要はありません。 最適なパフォーマンスを得るには、Azure ストレージ アカウントの Parquet ファイルと ORC ファイルが 256MB 以上である必要があります。 

### <a name="when-will-the-copy-command-be-generally-available"></a>COPY コマンドはいつ一般公開されますか?
COPY コマンドは、通常、次の暦年 (2020 年) の初めに一般公開されます。 

### <a name="are-there-any-known-issues-with-the-copy-command"></a>COPY コマンドに既知の問題はありますか?

- (n)varchar(max) などの LOB サポートは、COPY ステートメントでは使用できません。 これは、来年使用できるようになります。

フィードバックや問題は、配布リストの sqldwcopypreview@service.microsoft.com までお寄せください。

## <a name="see-also"></a>参照  

 [SQL Data Warehouse を使用した読み込みの概要](/azure/sql-data-warehouse/design-elt-data-loading)
