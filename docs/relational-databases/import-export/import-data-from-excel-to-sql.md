---
title: Excel から SQL にデータをインポートする | Microsoft Docs
ms.custom: sqlfreshmay19
ms.date: 09/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 77572a417836683e10ba3c7736fe4cdd0db4e129
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71708141"
---
# <a name="import-data-from-excel-to-sql-server-or-azure-sql-database"></a>Excel から SQL Server または Azure SQL Database にデータをインポートする

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Excel ファイルからSQL Server または Azure SQL Database に、データをインポートする方法はいくつかあります。 一部の方法では、Excel ファイルから直接 1 ステップでデータをインポートできます。他の方法では、先に Excel データをテキスト (CSV ファイル) としてエクスポートしてから、インポートする必要があります。 この記事では、よく使われる方法をまとめ、詳細な情報へのリンクを示します。

## <a name="list-of-methods"></a>方法の一覧

次のツールを使用して Excel からデータをインポートすることができます。

| 最初にテキストにエクスポートする (SQL Server および SQL Database) | Excel から直接 (SQL Server オンプレミスのみ) |
| :------------------------------------------------- |:------------------------------------------------- |
| [フラット ファイルのインポート ウィザード](#import-wiz)             |[SQL Server インポートおよびエクスポート ウィザード](#wiz)        |
| [BULK INSERT](#bulk-insert) ステートメント              |[SQL Server Integration Services (SSIS)](#ssis)    |
| [BCP](#bcp)                                        |[OPENROWSET](#openrowset) 関数 <br>            |
| [コピー ウィザード (Azure Data Factory)](#adf-wiz)       |                                                   |
| [Azure Data Factory](#adf)                         |                                                   |
| &nbsp; | &nbsp; |

Excel ブックから複数のワークシートをインポートする場合は、通常、シートごとに 1 回これらのツールをそれぞれ実行する必要があります。

SSIS や Azure Data Factory のような複雑なツールとサービスの詳細については、このリストの範囲外です。 興味のあるソリューションの詳細については、提供されているリンクを参照してください。

> [!IMPORTANT]
> Excel ファイルへの接続、および Excel から、または Excel へのデータの読み込みに関する制限事項と既知の問題については、「[Load data from or to Excel with SQL Server Integration Services (SSIS)](../../integration-services/load-data-to-from-excel-with-ssis.md)」 (SQL Server Integration Services (SSIS) を使用して Excel から、または Excel にデータを読み込む) を参照してください。

SQL Server をインストールしていない場合、あるいは SQL Server をインストールしているが、SQL Server Management Studio をインストールしていない場合、「 [SQL Server Management Studio (SSMS) のダウンロード](../../ssms/download-sql-server-management-studio-ssms.md)」を参照してください。

## <a name="wiz"></a> SQL Server インポートおよびエクスポート ウィザード

SQL Server インポートおよびエクスポート ウィザードのページをステップ実行して、Excel ファイルから直接データをインポートします。 必要に応じて、後でカスタマイズして再利用できる SQL Server Integration Services (SSIS) パッケージとして設定を保存します。

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。

2. **[データベース]** を展開します。
3. データベースを右クリックします。
4. **[タスク]** にカーソルを合わせます。
5. 以下のいずれかのオプションをクリックします。

  - **データのインポート**
  - **データのエクスポート**

    ![ウィザードの起動 (SSMS)](../../integration-services/import-export-data/media/start-wizard-ssms.jpg)

![Excel データ ソースに接続する](media/excel-connection.png)

ウィザードを使用して Excel から SQL Server にインポートする例については、「[Get started with this simple example of the Import and Export Wizard (インポートおよびエクスポート ウィザードのこの簡単な例から始める)](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)」を参照してください。

インポートとエクスポートのウィザードを起動するその他の方法については、「[SQL Server インポートおよびエクスポート ウィザードを起動する](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)」を参照してください。

## <a name="ssis"></a> SQL Server Integration Services (SSIS)

SSIS に精通していて、SQL Server インポートおよびエクスポート ウィザードを実行したくない場合は、Excel ソースおよびデータ フロー内の SQL Server 変換先を使用する SSIS パッケージを作成します。

これらの SSIS コンポーネントの詳細については、次のトピックを参照してください。

- [Excel ソース](../../integration-services/data-flow/excel-source.md)
- [SQL Server 変換先](../../integration-services/data-flow/sql-server-destination.md)

SSIS パッケージをビルドする方法の学習を開始するには、チュートリアル「[How to Create an ETL Package (ETL パッケージを作成する方法)](../../integration-services/ssis-how-to-create-an-etl-package.md)」を参照してください。

![データ フロー内のコンポーネント](media/excel-to-sql-data-flow.png)

## <a name="openrowset"></a>OPENROWSET およびリンク サーバー

> [!IMPORTANT]
> Azure SQL Database では、Excel から直接インポートすることはできません。 まず、データをテキスト (CSV) ファイルにエクスポートする必要があります。 例については、「[例](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)」を参照してください。

> [!NOTE]
> Excel データ ソースに接続する ACE プロバイダー (旧称 Jet プロバイダー) は、対話型のクライアント側での使用を対象としています。 特に自動化されたプロセスまたは並列で実行中のプロセスで、SQL Server 上の ACE プロバイダーを使用すると、予期しない結果になることがあります。

### <a name="distributed-queries"></a>分散クエリ

Transact-SQL `OPENROWSET` または `OPENDATASOURCE` 関数を使用して、Excel ファイルから直接データを SQL Server にインポートします。 このような使用方法は、 *"分散クエリ"* と呼ばれます。

> [!IMPORTANT]
> Azure SQL Database では、Excel から直接インポートすることはできません。 まず、データをテスト (CSV) ファイルにエクスポートする必要があります。 例については、「[例](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)」を参照してください。

分散クエリを実行する前に、次の例で示すように、`ad hoc distributed queries` サーバー構成オプションを有効にする必要があります。 詳しくは、「[ad hoc distributed queries サーバー構成オプション](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md)」を参照してください。

```sql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO
sp_configure 'Ad Hoc Distributed Queries', 1;
RECONFIGURE;
GO
```

次のコード サンプルでは、`OPENROWSET` を使用して、Excel `Sheet1` ワークシートから新しいデータベース テーブルにデータをインポートしています。

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENROWSET('Microsoft.ACE.OLEDB.12.0',
    'Excel 12.0; Database=C:\Temp\Data.xlsx', [Sheet1$]);
GO
```

`OPENDATASOURCE` と同じ例を次に示します。

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENDATASOURCE('Microsoft.ACE.OLEDB.12.0',
    'Data Source=C:\Temp\Data.xlsx;Extended Properties=Excel 12.0')...[Sheet1$];
GO
```

新しいテーブルを作成する代わりに、インポートされたデータを、 *"既存"* テーブルに *"追加"* するには、前の例で使用された `SELECT ... INTO ... FROM ...` 構文ではなく `INSERT INTO ... SELECT ... FROM ...` 構文を使用します。

Excel のデータをインポートせずに Excel のデータにクエリを実行するには、標準の `SELECT ... FROM ...` 構文を使用します。

分散クエリの詳細については、次のトピックを参照してください。

- [分散クエリ](https://msdn.microsoft.com/library/ms188721(v=sql.105).aspx) (分散クエリは SQL Server 2016 でもサポートされていますが、この機能のドキュメントは更新されていません。)
- [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)
- [OPENDATASOURCE](../../t-sql/functions/openquery-transact-sql.md)

### <a name="linked-servers"></a>リンク サーバー

SQL Server から Excel ファイルへの永続的な接続を *"リンク サーバー"* として構成することもできます。 次の例は、既存の Excel のリンク サーバー `EXCELLINK` の `Data` ワークシートからデータを、`Data_ls` という名前の新しい SQL Server データベース テーブルにインポートしています。

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_ls FROM EXCELLINK...[Data$];
GO
```

リンク サーバーは、SQL Server Management Studio から作成するか、次の例に示すように、システム ストアド プロシージャ `sp_addlinkedserver` を実行して作成できます。

```sql
DECLARE @RC int

DECLARE @server     nvarchar(128)
DECLARE @srvproduct nvarchar(128)
DECLARE @provider   nvarchar(128)
DECLARE @datasrc    nvarchar(4000)
DECLARE @location   nvarchar(4000)
DECLARE @provstr    nvarchar(4000)
DECLARE @catalog    nvarchar(128)

-- Set parameter values
SET @server =     'EXCELLINK'
SET @srvproduct = 'Excel'
SET @provider =   'Microsoft.ACE.OLEDB.12.0'
SET @datasrc =    'C:\Temp\Data.xlsx'
SET @provstr =    'Excel 12.0'

EXEC @RC = [master].[dbo].[sp_addlinkedserver] @server, @srvproduct, @provider,
@datasrc, @location, @provstr, @catalog
```

リンクサーバーの詳細については、次のトピックを参照してください。

- [リンク サーバーを作成する](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)
- [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md)

リンク サーバーと分散クエリに関する例および詳細な情報については、次のトピックを参照してください。

- [SQL Server のリンク サーバーおよび分散クエリで Excel を使用する方法](https://support.microsoft.com/help/306397/how-to-use-excel-with-sql-server-linked-servers-and-distributed-queries)
- [[HOWTO] DTS: Excel から SQL Server にデータをインポートする方法](https://support.microsoft.com/help/321686/how-to-import-data-from-excel-to-sql-server)

## <a name="prereq"></a> 前提条件 - Excel データをテキストとして保存する

このページの BULK INSERT ステートメント、BCP ツール、または Azure Data Factory に記載されているメソッドの残りの部分を使用するには、最初に Excel データをテキスト ファイルにエクスポートする必要があります。

Excel で **[ファイル] メニューから [名前をつけて保存]** を選択し、変換先ファイルの種類として **[テキスト (タブ区切り) (\*.txt)]** または **[CSV (コンマ区切り) (\*.csv)]** を選択します。

ブックから複数のワークシートをエクスポートする場合は、各シートを選択して、この手順を繰り返します。 **[名前をつけて保存]** コマンドでは、作業中のシートのみがエクスポートされます。

> [!TIP]
> データ インポート ツールで最適な結果を得るには、列ヘッダーとデータ行のみが含まれているシートを保存します。 保存したデータにページ タイトル、空白行、メモなどが含まれる場合は、後でデータをインポートするときに、予期しない結果になる可能性があります。

## <a name="import-wiz"></a>フラット ファイルのインポート ウィザード

フラット ファイルのインポート ウィザードのページをステップ実行して、テキストファイルとして保存したデータをインポートします。

前述の[前提条件](#prereq)のセクションで説明したとおり、Excel データをテキストとしてエクスポートしてからフラット ファイルのインポート ウィザードを使用してインポートする必要があります。

フラット ファイルのインポート ウィザードについて詳しくは、「[SQL のフラット ファイルのインポート ウィザード](import-flat-file-wizard.md)」をご覧ください。

## <a name="bulk-insert"></a>BULK INSERT コマンド

`BULK INSERT` は、SQL Server Management Studio から実行できる Transact-SQL コマンドです。 次の例では、`Data.csv` コンマ区切りファイルから既存のデータベース テーブルにデータを読み込みます。

前述の[前提条件](#prereq)のセクションで説明したとおり、Excel データをテキストとしてエクスポートしてから BULK INSERT を使用してインポートする必要があります。 BULK INSERT では、Excel ファイルを直接読み取ることはできません。 BULK INSERT コマンドを使用すると、ローカルまたは Azure Blob Storage に格納されている CSV ファイルをインポートできます。

```sql
USE ImportFromExcel;
GO
BULK INSERT Data_bi FROM 'C:\Temp\data.csv'
   WITH (
      FIELDTERMINATOR = ',',
      ROWTERMINATOR = '\n'
);
GO
```

SQL Server と SQL Database の詳細と例については、次のトピックを参照してください。

- [BULK INSERT または OPENROWSET(BULK...) を使用した一括データのインポート](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
- [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)

## <a name="bcp"></a>BCP ツール

BCP は、コマンド プロンプトから実行するプログラムです。 次の例では、`Data.csv` コンマ区切りファイルから既存の `Data_bcp` データベース テーブルにデータを読み込みます。

前述の[前提条件](#prereq)のセクションで説明したとおり、Excel データをテキストとしてエクスポートしてから BCP を使用してインポートする必要があります。 BCP では、Excel ファイルを直接読み取ることはできません。 ローカル ストレージに保存されているテスト (CSV) ファイルから SQL Server または SQL Database にインポートするために使用します。

> [!IMPORTANT]
> Azure Blob Storage に格納されているテキスト (CSV) ファイルの場合は、BULK INSERT または OPENROWSET を使用します。 例については、「[例](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)」を参照してください。

```console
bcp.exe ImportFromExcel..Data_bcp in "C:\Temp\data.csv" -T -c -t ,
```

BCP の詳細については、次のトピックを参照してください。

- [bcp ユーティリティを使用した一括データのインポートとエクスポート](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)
- [bcp ユーティリティ](../../tools/bcp-utility.md)
- [一括エクスポートまたは一括インポートのデータの準備](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)

## <a name="adf-wiz"></a>コピー ウィザード (Azure Data Factory)

Azure Data Factory のコピー ウィザードのページをステップ実行して、テキストファイルとして保存したデータをインポートします。

前述の[前提条件](#prereq)のセクションで説明したとおり、Excel データをテキストとしてエクスポートしてから Azure Data Factory を使用してインポートする必要があります。 Data Factory では、Excel ファイルを直接読み取ることはできません。

コピー ウィザードの詳細については、次のトピックを参照してください。

- [Data Factory コピー ウィザード](https://docs.microsoft.com/azure/data-factory/data-factory-azure-copy-wizard)
- [チュートリアル: コピー アクティビティがあるパイプラインを Data Factory コピー ウィザードで作成する](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-wizard-tutorial)。

## <a name="adf"></a> Azure Data Factory

Azure Data Factory に精通していて、コピー ウィザードを実行したくない場合は、テキスト ファイルから SQL Server または Azure SQL Database にコピーするコピー アクティビティでパイプラインを作成します。

前述の[前提条件](#prereq)のセクションで説明したとおり、Excel データをテキストとしてエクスポートしてから Azure Data Factory を使用してインポートする必要があります。 Data Factory では、Excel ファイルを直接読み取ることはできません。

これらの Data Factory のソースおよびシンクの使用に関する詳細については、次のトピックを参照してください。

- [ファイル システム](https://docs.microsoft.com/azure/data-factory/data-factory-onprem-file-system-connector)
- [SQL Server](https://docs.microsoft.com/azure/data-factory/data-factory-sqlserver-connector)
- [Azure SQL データベース](https://docs.microsoft.com/azure/data-factory/data-factory-azure-sql-connector)

Azure Data Factory でデータをコピーする方法の学習を開始するには、次のトピックを参照してください。

- [コピー アクティビティを使用したデータの移動](https://docs.microsoft.com/azure/data-factory/data-factory-data-movement-activities)
- [チュートリアル: コピー アクティビティがあるパイプラインを Azure portal で作成する](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database)

## <a name="common-errors"></a>一般的なエラー

### <a name="microsoftaceoledb120-has-not-been-registered"></a>"Microsoft.ACE.OLEDB.12.0" が登録されていません

このエラーは OLEDB プロバイダーがインストールされていない場合に発生します。 [Microsoft Access データベース エンジン 2010 再頒布可能パッケージ](https://www.microsoft.com/en-us/download/details.aspx?id=13255)からインストールします。 Windows と SQL Server が両方とも 64 ビットである場合は、64 ビット バージョンをインストールしてください。

エラーの全文は次のとおりです。

```
Msg 7403, Level 16, State 1, Line 3
The OLE DB provider "Microsoft.ACE.OLEDB.12.0" has not been registered.
```

## <a name="cannot-create-an-instance-of-ole-db-provider-microsoftaceoledb120-for-linked-server-null"></a>リンク サーバー "(null)" の OLE DB プロバイダー "Microsoft.ACE.OLEDB.12.0" のインスタンスを作成できません

これは Microsoft OLEDB が正しく構成されていないことを示しています。 これを解決するには、次の Transact-SQL コードを実行します。

```sql
EXEC sp_MSset_oledb_prop N'Microsoft.ACE.OLEDB.12.0', N'AllowInProcess', 1
EXEC sp_MSset_oledb_prop N'Microsoft.ACE.OLEDB.12.0', N'DynamicParameters', 1
```

エラーの全文は次のとおりです。

```
Msg 7302, Level 16, State 1, Line 3
Cannot create an instance of OLE DB provider "Microsoft.ACE.OLEDB.12.0" for linked server "(null)".
```

### <a name="the-32-bit-ole-db-provider-microsoftaceoledb120-cannot-be-loaded-in-process-on-a-64-bit-sql-server"></a>32 ビットの OLE DB プロバイダー "Microsoft.ACE.OLEDB.12.0" を 64 ビットの SQL Server のインプロセスで読み込むことができません

これは、32 ビット バージョンの OLE DB プロバイダーが 64 ビットの SQL Server でインストールされている場合に発生します。 この問題を解決するには、OLE DB プロバイダーの 32 ビット バージョンをアンインストールして、代わりに 64 ビット バージョンをインストールします。

エラーの全文は次のとおりです。

```
Msg 7438, Level 16, State 1, Line 3
The 32-bit OLE DB provider "Microsoft.ACE.OLEDB.12.0" cannot be loaded in-process on a 64-bit SQL Server.
```

### <a name="the-ole-db-provider-microsoftaceoledb120-for-linked-server-null-reported-an-error-the-provider-did-not-give-any-information-about-the-error"></a>リンク サーバー "(null)" の OLE DB プロバイダー "Microsoft.ACE.OLEDB.12.0" でエラーが報告されました。 プロバイダーからエラーに関する情報を取得できませんでした

### <a name="cannot-initialize-the-data-source-object-of-ole-db-provider-microsoftaceoledb120-for-linked-server-null"></a>リンク サーバー "(null)" の OLE DB プロバイダー "Microsoft.ACE.OLEDB.12.0" のデータ ソース オブジェクトを初期化できません

これらのエラーは通常、両方とも SQL Server プロセスとファイルの間のアクセス許可の問題を示しています。 SQL Server サービスを実行しているアカウントに、ファイルへのフル アクセス許可があることを確認してください。 デスクトップからファイルをインポートしてみてください。

エラーの全文は次のとおりです。

```
Msg 7399, Level 16, State 1, Line 3
The OLE DB provider "Microsoft.ACE.OLEDB.12.0" for linked server "(null)" reported an error. The provider did not give any information about the error.
```

```
Msg 7303, Level 16, State 1, Line 3
Cannot initialize the data source object of OLE DB provider "Microsoft.ACE.OLEDB.12.0" for linked server "(null)".
```

## <a name="see-also"></a>参照

[SQL Server Integration Services (SSIS) を使用して、Excel からデータをインポートする、または Excel にデータをエクスポートする](../../integration-services/load-data-to-from-excel-with-ssis.md)
