---
title: BULK INSERT または OPENROWSET(BULK...) を使用して SQL Server にデータをインポートする
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- BULK INSERT statement, importing data from a remote data file
- bulk importing [SQL Server], methods
- bulk exporting [SQL Server], methods
- OPENROWSET function, BULK INSERT
- bulk importing [SQL Server], security
- bulk rowset providers [SQL Server]
- bulk exporting [SQL Server], BULK INSERT statement
- remote data access [SQL Server], bulk importing
- bulk importing [SQL Server], BULK INSERT statement
- Transact-SQL bulk export/import operations
ms.assetid: 18a64236-0285-46ea-8929-6ee9bcc020b9
author: markingmyname
ms.author: maghan
manager: jroth
ms.custom: seo-lt-2019
ms.date: 09/25/2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: deaaa783f465c5cfecb940df4b9dd56e10590bc5
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056389"
---
# <a name="use-bulk-insert-or-openrowsetbulk-to-import-data-to-sql-server"></a>BULK INSERT または OPENROWSET(BULK...) を使用して SQL Server にデータをインポートする

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

この記事では、[!INCLUDE[tsql](../../includes/tsql-md.md)] の BULK INSERT ステートメントと INSERT...SELECT * FROM OPENROWSET(BULK...) ステートメントを使用して、データ ファイルから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database のテーブルにデータを一括インポートする方法の概要を説明します。 また、BULK INSERT および OPENROWSET(BULK...) を使用する場合のセキュリティの注意点や、リモート データ ソースから一括インポートする方法についても説明します。

> [!NOTE]
> BULK INSERT または OPENROWSET(BULK...) を使用する場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョンで権限の借用がどのように処理されるかを理解しておくことが重要です。 詳細については、後の「セキュリティの注意点」を参照してください。

## <a name="bulk-insert-statement"></a>BULK INSERT ステートメント

BULK INSERT では、データ ファイルからテーブルにデータが読み込まれます。 この機能は、 **bcp** コマンドの **in** オプションと似ていますが、データ ファイルが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスによって読み取られる点が異なります。 BULK INSERT の構文の説明については、「 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)」を参照してください。

## <a name="bulk-insert-examples"></a>BULK INSERT の例

- [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)
- [XML ドキュメントの一括インポートと一括エクスポートの例 &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)
- [データの一括インポート時の ID 値の保持 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)
- [一括インポート中の NULL の保持または既定値の使用 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)
- [フィールド ターミネータと行ターミネータの指定 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)
- [データの一括インポートでのフォーマット ファイルの使用 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)
- [文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)
- [ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)
- [Unicode 文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)
- [Unicode ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)
- [フォーマット ファイルを使用したテーブル列のスキップ &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)
- [フォーマット ファイルを使用したテーブル列とデータ ファイル フィールドのマッピング &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)

## <a name="openrowsetbulk-function"></a>OPENROWSET(BULK...)機能

OPENROWSET 一括行セット プロバイダーには、BULK オプションを指定して OPENROWSET 関数を呼び出すことによってアクセスします。 OPENROWSET(BULK...) 関数では、OLE DB プロバイダー経由でデータ ファイルなどのリモート データ ソースに接続することで、リモート データにアクセスできます。

データを一括インポートするには、INSERT ステートメントの SELECT...FROM 句から OPENROWSET(BULK...) を呼び出します。 データの一括インポートの基本構文は次のとおりです。

INSERT ...SELECT * FROM OPENROWSET(BULK...)

OPENROWSET(BULK...) を INSERT ステートメント内で使用する場合は、テーブル ヒントがサポートされます。 TABLOCK などの通常のテーブル ヒントに加えて、BULK 句では、次の特殊なテーブル ヒントを使用できます:IGNORE_CONSTRAINTS (CHECK 制約のみ無視します)、IGNORE_TRIGGERS、KEEPDEFAULTS、KEEPIDENTITY。 詳細については、「[テーブル ヒント &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)」を参照してください。

BULK オプションの上記以外の使い方の詳細については、「 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)」を参照してください。

## <a name="insertselect--from-openrowsetbulk-statements---examples"></a>INSERT...SELECT * FROM OPENROWSET(BULK...) ステートメント - 例:

- [XML ドキュメントの一括インポートと一括エクスポートの例 &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)
- [データの一括インポート時の ID 値の保持 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)
- [一括インポート中の NULL の保持または既定値の使用 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)
- [データの一括インポートでのフォーマット ファイルの使用 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)
- [文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)
- [フォーマット ファイルを使用したテーブル列のスキップ &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)
- [フォーマット ファイルを使用したデータ フィールドのスキップ &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)
- [フォーマット ファイルを使用したテーブル列とデータ ファイル フィールドのマッピング &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)

## <a name="security-considerations"></a>セキュリティに関する考慮事項

ユーザーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを使用する場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス アカウントのセキュリティ プロファイルが使用されます。 SQL Server 認証を使用したログインは、データベース エンジン以外では認証できません。 そのため、SQL Server 認証を使用したログインによって BULK INSERT コマンドが開始されると、SQL Server プロセス アカウント (SQL Server データベース エンジン サービスで使用されるアカウント) のセキュリティ コンテキストを使用してデータへの接続が行われます。 

ソース データを正しく読み取るには、SQL Server データベース エンジンで使用されるアカウントに対して、ソース データへのアクセス権を付与する必要があります。 これに対して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーが Windows 認証を使用してログインした場合、そのユーザーは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスのセキュリティ プロファイルに関係なく、そのユーザー アカウントでアクセス可能なファイルのみを読み取ることができます。

たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに Windows 認証を使用してログインしたユーザーを考えます。 ユーザーが BULK INSERT または OPENROWSET を使用してデータ ファイルから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルにデータをインポートするには、アカウントにデータ ファイルの読み取りアクセス許可が与えられていなければなりません。 データ ファイルへのアクセスで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスにそのファイルへのアクセス許可がなくても、ユーザーはそのファイルからテーブルにデータをインポートできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスにファイル アクセス許可を与える必要はありません。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows では、認証されている Windows ユーザーの資格情報を転送することで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスから別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスへ接続できるように構成することが可能です。 この設定を、" *権限借用* " または " *権限委譲*" といいます。 BULK INSERT または OPENROWSET を使用する場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョンによってユーザーの権限借用のセキュリティがどのように処理されるかを理解しておくことが重要です。 ユーザーの権限を借用することで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスまたはユーザーのいずれかが使用しているコンピューターとは異なるコンピューターにデータ ファイルを常駐させることができます。 たとえば、 **Computer_A** 上のユーザーが **Computer_B**上のデータ ファイルにアクセスでき、資格情報の委任が適切に設定されている場合、このユーザーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer_C **上で実行されている**のインスタンスに接続して、 **Computer_B**上のデータ ファイルにアクセスし、そのファイルから **Computer_C**上のテーブルにデータを一括インポートできます。

## <a name="bulk-importing-to-sql-server-from-a-remote-data-file"></a>リモート データ ファイルから SQL Server への一括インポート

BULK INSERT または INSERT...SELECT \* FROM OPENROWSET(BULK...) を使用して別のコンピューターからデータを一括インポートするには、データ ファイルを 2 台のコンピューター間で共有している必要があります。 共有データ ファイルを指定するには、UNC (汎用名前付け規則) 名を使用します。UNC 名の一般的な形式は、 **\\\\** _Servername_ **\\** _Sharename_ **\\** _Path_ **\\** _Filename_です。 また、データ ファイルへのアクセスに使用されるアカウントは、リモート ディスク上のファイルの読み取りに必要な権限を持っている必要があります。

たとえば、次の `BULK INSERT` ステートメントでは、 `SalesOrderDetail` というデータ ファイルから `AdventureWorks` データベースの `newdata.txt`テーブルにデータの一括インポートを行います。 このデータ ファイルは、`\dailyorders` というシステムの `salesforce` というネットワーク共有ディレクトリの `computer2` という共有フォルダーにあります。

```sql
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail
   FROM '\\computer2\salesforce\dailyorders\neworders.txt';
```

> [!NOTE]
> クライアントが読み取るファイルは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] とは無関係であるため、**bcp** にはこの制限は適用されません。

## <a name="bulk-importing-from-azure-blob-storage"></a>Azure Blob Storage からの一括インポート

Azure Blob Storage からパブリック (匿名アクセス) ではないデータをインポートするときは、[MASTER KEY](../../t-sql/statements/create-master-key-transact-sql.md) で暗号化された SAS キーに基づいて [DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md) を作成した後、BULK INSERT コマンドで使用する[外部データベース ソース](../../t-sql/statements/create-external-data-source-transact-sql.md)を作成します。

### <a name="using-bulk-insert"></a>BULK INSERT の使用

次の例では、BULK INSERT コマンドを使用して、SAS キーを作成した Azure Blob Storage の場所にある csv ファイルからデータを読み込む方法を示します。 Azure Blob Storage の場所は、外部データ ソースとして構成されます。 これには、ユーザー データベース内でマスター キーを使用して暗号化された共有アクセス署名を使用するデータベース スコープ資格情報が必要です。

```sql
--> Optional - a MASTER KEY is not requred if a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'YourStrongPassword1';
GO
--> Optional - a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE DATABASE SCOPED CREDENTIAL MyAzureBlobStorageCredential
 WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
 SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************';

 -- NOTE: Make sure that you don't have a leading ? in SAS token, and
 -- that you have at least read permission on the object that should be loaded srt=o&sp=r, and
 -- that expiration period is valid (all dates are in UTC time)

CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
WITH ( TYPE = BLOB_STORAGE,
          LOCATION = 'https://****************.blob.core.windows.net/invoices'
          , CREDENTIAL= MyAzureBlobStorageCredential --> CREDENTIAL is not required if a blob is configured for public (anonymous) access!
);

BULK INSERT Sales.Invoices
FROM 'inv-2017-12-08.csv'
WITH (DATA_SOURCE = 'MyAzureBlobStorage');
```

> [!IMPORTANT]
> Azure SQL Database では、Windows ファイルからの読み取りはサポートされません。

### <a name="using-openrowset"></a>OPENROWSET の使用

次の例では、OPENROWSET コマンドを使用して、SAS キーを作成した Azure Blob Storage の場所にある csv ファイルからデータを読み込む方法を示します。 Azure Blob Storage の場所は、外部データ ソースとして構成されます。 これには、ユーザー データベース内でマスター キーを使用して暗号化された共有アクセス署名を使用するデータベース スコープ資格情報が必要です。

```sql
--> Optional - a MASTER KEY is not requred if a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'YourStrongPassword1';
GO
--> Optional - a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE DATABASE SCOPED CREDENTIAL MyAzureBlobStorageCredential
 WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
 SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************';

 -- NOTE: Make sure that you don't have a leading ? in SAS token, and
 -- that you have at least read permission on the object that should be loaded srt=o&sp=r, and
 -- that expiration period is valid (all dates are in UTC time)

CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
WITH ( TYPE = BLOB_STORAGE,
          LOCATION = 'https://****************.blob.core.windows.net/invoices'
          , CREDENTIAL= MyAzureBlobStorageCredential --> CREDENTIAL is not required if a blob is configured for public (anonymous) access!
);

INSERT INTO achievements with (TABLOCK) (id, description)
SELECT * FROM OPENROWSET(
   BULK  'csv/achievements.csv',
   DATA_SOURCE = 'MyAzureBlobStorage',
   FORMAT ='CSV',
   FORMATFILE='csv/achievements-c.xml',
   FORMATFILE_DATA_SOURCE = 'MyAzureBlobStorage'
    ) AS DataFile;
```

> [!IMPORTANT]
> Azure SQL Database では、Windows ファイルからの読み取りはサポートされません。

## <a name="see-also"></a>参照

- [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)
- [SELECT 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-clause-transact-sql.md)
- [データの一括インポートと一括エクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)
- [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)
- [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)
- [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)
- [bcp ユーティリティ](../../tools/bcp-utility.md)
- [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)  
