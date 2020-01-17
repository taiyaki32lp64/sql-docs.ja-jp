---
title: Azure BLOB ストレージのデータに一括アクセスする
ms.description: Transact-SQL examples that use BULK INSERT and OPENROWSET to access data in an Azure Blob storage account.
ms.date: 10/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], from Azure blob storage
- Azure blob storage, bulk import to SQL Server
- BULK INSERT, Azure blob storage
- OPENROWSET, Azure blob storage
ms.assetid: f7d85db3-7a93-400e-87af-f56247319ecd
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 08e81abbc21671881affc80fc9b7f0346cd490f7
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056003"
---
# <a name="examples-of-bulk-access-to-data-in-azure-blob-storage"></a>Azure BLOB ストレージのデータに一括アクセスする例

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

`BULK INSERT` ステートメントと `OPENROWSET` ステートメントは、Azure BLOB ストレージのファイルに直接アクセスできます。 次の例では、`inv-2017-01-19.csv` という名前の CSV (コンマ区切り値) ファイルのデータを使用します。このファイルは `newinvoices` という名前のストレージ アカウントで `Week3` という名前のコンテナーに格納されています。 ファイルの書式を設定するパスを使用できますが、以下の例には含まれていません。

SQL Server から Azure BLOB ストレージに一括アクセスする場合、[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 以上が必要になります。

> [!IMPORTANT]
> コンテナーと BLOB 上のファイルへのパスはすべて、`CASE SENSITIVE` です。 正しくない場合は、"一括読み込みできません。 ファイル "file.csv" が存在しないか、ファイルへのアクセス権がありません。" などのエラーが返される可能性があります。

## <a name="create-the-credential"></a>資格情報を作成する

下のすべての例で、Shared Access Signature を参照するデータベース スコープ資格情報が必要です。

> [!IMPORTANT]
> 外部データ ソースは、`SHARED ACCESS SIGNATURE` ID を使用するデータベース スコープ資格情報で作成する必要があります。 ストレージ アカウントの Shared Access Signature を作成するには、Azure ポータルのストレージ アカウント プロパティに関するページで **Shared Access Signature** プロパティを参照してください。 Shared Access Signature に関する詳細については、「[Shared Access Signature (SAS) を使用](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)」を参照してください。 資格情報の詳細については、「[CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)」 (データベース スコープ資格情報を作成する) を参照してください。

`IDENTITY` (`SHARED ACCESS SIGNATURE` に設定します) を利用してデータベース スコープ資格情報を作成します。 BLOB ストレージ アカウントに対して生成された SAS トークンを使用します。 SAS トークンの先頭に `?` がないこと、読み込む必要があるオブジェクトに対して少なくとも読み取りアクセス許可があること、有効期間が有効であることを確認します (すべての日付は UTC 時刻です)。

例:

```sql
CREATE DATABASE SCOPED CREDENTIAL UploadInvoices
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'sv=2018-03-28&ss=b&srt=sco&sp=rwdlac&se=2019-08-31T02:25:19Z&st=2019-07-30T18:25:19Z&spr=https&sig=KS51p%2BVnfUtLjMZtUTW1siyuyd2nlx294tL0mnmFsOk%3D';
```

## <a name="accessing-data-in-a-csv-file-referencing-an-azure-blob-storage-location"></a>Azure BLOB ストレージの場所を参照する CSV ファイルのデータにアクセスする

次の例では、`MyAzureInvoices` という名前の Azure ストレージ アカウントを指す外部データ ソースを使用します。

```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net',
        CREDENTIAL = UploadInvoices
    );
```

次に、`OPENROWSET` ステートメントがコンテナー名 (`week3`) をファイルの説明に追加します。 ファイルの名前は `inv-2017-01-19.csv` です。

```sql
SELECT * FROM OPENROWSET(
   BULK 'week3/inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   FORMAT = 'CSV',
   FORMATFILE='invoices.fmt',
   FORMATFILE_DATA_SOURCE = 'MyAzureInvoices'
   ) AS DataFile;   
```

`BULK INSERT` を利用し、コンテナーとファイルの説明を使用します。

```sql
BULK INSERT Colors2
FROM 'week3/inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoices',
      FORMAT = 'CSV');
```

## <a name="accessing-data-in-a-csv-file-referencing-a-container-in-an-azure-blob-storage-location"></a>Azure BLOB ストレージの場所にあるコンテナーを参照する CSV ファイルのデータにアクセスする

次の例では、Azure ストレージ アカウントにあるコンテナー (`week3` という名前) を指す外部データ ソースを使用します。

```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoicesContainer
    WITH (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = UploadInvoices
    );
```

`OPENROWSET` ステートメントはコンテナー名をファイルの説明に追加しません。

```sql
SELECT * FROM OPENROWSET(
   BULK 'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoicesContainer',
   FORMAT = 'CSV',
   FORMATFILE='invoices.fmt',
   FORMATFILE_DATA_SOURCE = 'MyAzureInvoices'
   ) AS DataFile;
```

`BULK INSERT` を利用し、ファイルの説明にコンテナー名を使用しません。

```sql
BULK INSERT Colors2
FROM 'inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoicesContainer',
      FORMAT = 'CSV');
```

## <a name="see-also"></a>参照

- [CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)
- [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)
- [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)
