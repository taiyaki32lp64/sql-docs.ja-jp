---
title: BULK INSERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BULK_TSQL
- BULK INSERT
- BULK_INSERT_TSQL
- BULK
dev_langs:
- TSQL
helpviewer_keywords:
- tables [SQL Server], importing data into
- inserting files
- views [SQL Server], importing data into
- BULK INSERT statement
- views [SQL Server], exporting data from
- importing data, bulk import
- bulk importing [SQL Server], BULK INSERT statement
- file importing [SQL Server]
ms.assetid: be3984e1-5ab3-4226-a539-a9f58e1e01e2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6b6534e887f890700b69a11b4515d4cf1af4d86a
ms.sourcegitcommit: c98c6e33d04d4a1888db7dbe89cb0b1bb3a66418
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2019
ms.locfileid: "74249851"
---
# <a name="bulk-insert-transact-sql"></a>BULK INSERT (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、ユーザーが指定した形式で、データベース テーブルまたはビューにデータ ファイルをインポートします。

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>構文

```
BULK INSERT
   { database_name.schema_name.table_or_view_name | schema_name.table_or_view_name | table_or_view_name }
      FROM 'data_file'
     [ WITH
    (
   [ [ , ] BATCHSIZE = batch_size ]
   [ [ , ] CHECK_CONSTRAINTS ]
   [ [ , ] CODEPAGE = { 'ACP' | 'OEM' | 'RAW' | 'code_page' } ]
   [ [ , ] DATAFILETYPE =
      { 'char' | 'native'| 'widechar' | 'widenative' } ]
   [ [ , ] DATA_SOURCE = 'data_source_name' ]
   [ [ , ] ERRORFILE = 'file_name' ]
   [ [ , ] ERRORFILE_DATA_SOURCE = 'data_source_name' ]
   [ [ , ] FIRSTROW = first_row ]
   [ [ , ] FIRE_TRIGGERS ]
   [ [ , ] FORMATFILE_DATASOURCE = 'data_source_name' ]
   [ [ , ] KEEPIDENTITY ]
   [ [ , ] KEEPNULLS ]
   [ [ , ] KILOBYTES_PER_BATCH = kilobytes_per_batch ]
   [ [ , ] LASTROW = last_row ]
   [ [ , ] MAXERRORS = max_errors ]
   [ [ , ] ORDER ( { column [ ASC | DESC ] } [ ,...n ] ) ]
   [ [ , ] ROWS_PER_BATCH = rows_per_batch ]
   [ [ , ] ROWTERMINATOR = 'row_terminator' ]
   [ [ , ] TABLOCK ]

   -- input file format options
   [ [ , ] FORMAT = 'CSV' ]
   [ [ , ] FIELDQUOTE = 'quote_characters']
   [ [ , ] FORMATFILE = 'format_file_path' ]
   [ [ , ] FIELDTERMINATOR = 'field_terminator' ]
   [ [ , ] ROWTERMINATOR = 'row_terminator' ]
    )]
```

## <a name="arguments"></a>引数

*database_name* 指定のテーブルまたはビューが含まれているデータベース名を指定します。 指定しない場合、現在のデータベースが使用されます。

*schema_name* テーブルまたはビューのスキーマの名前を指定します。 一括インポート操作を実行するユーザーの既定のスキーマが、指定したテーブルまたはビューのスキーマと同じ場合、*schema_name* は省略可能です。 *スキーマ*を指定せず、さらに一括インポート操作を実行するユーザーの既定のスキーマが、指定したテーブルまたはビューのスキーマと異なる場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではエラー メッセージが返され、一括インポート操作は取り消されます。

*table_name* データの一括インポート先のテーブル名またはビュー名を指定します。 指定できるビューは、すべての列が同じベース テーブルを参照するビューだけです。 データをビューに読み込むときの制限の詳細については、「[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)」を参照してください。

**'** _data_file_ **'** 指定のテーブルまたはビューにインポートするデータが含まれているデータ ファイルの完全なパスを指定します。 BULK INSERT を使用して、ディスクまたは Azure Blob Storage (ネットワーク、フロッピー ディスク、ハード ディスクなど) からデータをインポートすることができます。

*data_file* には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行されているサーバーからの有効なパスを指定する必要があります。 *data_file* がリモート ファイルの場合は、UNC (汎用名前付け規則) 名を指定します。 UNC 名の形式は、\\\\*Systemname*\\*ShareName*\\*Path*\\*FileName*です。 次に例を示します。

```sql
BULK INSERT Sales.Orders
FROM '\\SystemX\DiskZ\Sales\data\orders.dat';
```

**適用対象:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 および Azure SQL Database。
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP1.1 以降では、data_file は Azure Blob Storage に格納することができます。 その場合は、**data_source_name** オプションを指定する必要があります。 例については、「[Azure Blob Storage 内のファイルからデータをインポートする](#f-importing-data-from-a-file-in-azure-blob-storage)」を参照してください。

> [!IMPORTANT]
> Azure SQL Database でサポートされるのは、Azure Blob Storage からの読み取りのみです。

**'** _data_source_name_ **'** 
**適用対象:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 および Azure SQL Database。
インポートされるファイルの Azure Blob Storage の場所を指している名前付きの外部データ ソースです。 外部データ ソースは、[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 で追加された `TYPE = BLOB_STORAGE` オプションを使用して作成する必要があります。 詳しくは、「[CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)」をご覧ください。 例については、「[Azure Blob Storage 内のファイルからデータをインポートする](#f-importing-data-from-a-file-in-azure-blob-storage)」を参照してください。

BATCHSIZE **=** _batch_size_ バッチ内の行数を指定します。 それぞれのバッチは、1 回のトランザクションでサーバーにコピーされます。 コピーに失敗した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では各バッチのトランザクションがコミットまたはロールバックされます。 既定では、指定のデータ ファイル内にあるすべてのデータが 1 つのバッチになります。 パフォーマンスに関する考慮事項については、このトピックで後述する「解説」を参照してください。

CHECK_CONSTRAINTS 一括インポート操作中、対象テーブルまたはビューに対するすべての制約を検証します。 CHECK_CONSTRAINTS オプションを指定しない場合、CHECK 制約および FOREIGN KEY 制約は無視され、操作の後でテーブルの制約は信頼されていないものとしてマークされます。

> [!NOTE]
> UNIQUE および PRIMARY KEY 制約は常に適用されます。 NOT NULL 制約で定義された文字型列にインポートする場合、テキスト ファイルに値がなければ BULK INSERT は空白文字列を挿入します。

テーブル全体の制約は、任意の時点で必ず検証してください。 一括インポート操作の実行時にテーブルが空でなかった場合は、制約の再検証を行うと、追加データに CHECK 制約を適用するよりもコストがかかる可能性があります。

入力データに制約違反の行が含まれている場合などは、制約を無効 (既定の動作) にできます。 制約の CHECK を無効にした場合は、データをインポートした後 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用して無効なデータを削除できます。

> [!NOTE]
> MAXERRORS オプションは制約チェックには適用されません。

CODEPAGE **=** { **'** ACP **'**  |  **'** OEM **'**  |  **'** RAW **'**  |  **'** _code_page_ **'** } データ ファイル内のデータのコード ページを指定します。 CODEPAGE は、データに **char**、**varchar**、**text** 列 (文字値が **127** より大きいか、**32** 未満) が含まれている場合にのみ当てはまります。 例については、「[コード ページの指定](#d-specifying-a-code-page)」を参照してください。

> [!IMPORTANT]
> [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] の場合、CODEPAGE オプションは Linux 上ではサポートされていません。 [!INCLUDE[ssSQLv15_md](../../includes/sssqlv15-md.md)] の場合、CODEPAGE に対して使えるのは **'RAW'** オプションのみです。

> [!NOTE]
> [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、[フォーマット ファイル](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)の各列に対して照合順序名を指定することをお勧めします。

|CODEPAGE の値|[説明]|
|--------------------|-----------------|
|ACP|**char**、**varchar**、または **text** データ型の列は、[!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows コード ページ (ISO 1252) から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コード ページに変換されます。|
|OEM (既定値)|**char**、**varchar**、または **text** のデータ型の列は、システムの OEM コード ページから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コード ページに変換されます。|
|RAW|1 つのコード ページから別のコード ページへの変換は行われません。このオプションを使用すると、最も高速に操作を完了できます。|
|*code_page*|850 など、特定のコード ページ番号を指定します。<br /><br /> **&#42;&#42; 重要 &#42;&#42;** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] より前のバージョンはコード ページ 65001 (UTF-8 エンコード) をサポートしません。|
| &nbsp; | &nbsp; |

DATAFILETYPE **=** { **'char'**  |  **'native'**  |  **'widechar'**  |  **'widenative'** } BULK INSERT で、指定したデータ ファイルの型の値に基づいてインポート操作を実行します。

&nbsp;

|DATAFILETYPE の値|すべてのデータが示す形式|
|------------------------|------------------------------|
|**char** (既定値)|文字形式。<br /><br /> 詳細については、「[文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)」をご覧ください。|
|**native**|ネイティブ (データベース) データ型。 **bcp** ユーティリティを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からデータを一括インポートし、ネイティブ データ ファイルを作成します。<br /><br /> ネイティブ値を使用すると、char 型の値を使用するよりもパフォーマンスが向上します。 ネイティブ形式は、拡張文字や 2 バイト文字セット (DBCS) の文字を含まないデータ ファイルを使用して、SQL Server の複数のインスタンス間でデータを一括転送する場合に推奨します。<br /><br /> 詳細については、「[ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)」をご覧ください。|
|**widechar**|Unicode 文字。<br /><br /> 詳細については、「 [Unicode 文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)」をご覧ください。|
|**widenative**|ネイティブ (データベース) データ型。ただし、データが Unicode として格納される **char**、**varchar**、**text** 列は除きます。 **bcp** ユーティリティを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からデータを一括インポートし、**widenative** データ ファイルを作成します。<br /><br /> **widenative** 値を使用すると、**widechar** 値を使用するよりもパフォーマンスが向上します。 データ ファイルに [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)] 拡張文字が含まれている場合は、**widenative** を指定します。<br /><br /> 詳細については、「 [Unicode ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)」をご覧ください。|
| &nbsp; | &nbsp; |

ERRORFILE **='** _file_name_ **'** 形式エラーがあり、OLE DB 行セットに変換できない行を収集するときに使用するファイルを指定します。 該当する行は、データ ファイルからこのエラー ファイルに "そのまま" コピーされます。

このエラー ファイルは、コマンドが実行されたときに作成されます。 ファイルが既に存在する場合はエラーが発生し、 さらに、拡張子 .ERROR.txt の制御ファイルが作成されます。 このファイルにはエラー ファイルの各行の参照と、エラーの診断が含まれています。 エラーが修正されるとすぐ、データは読み込み可能になります。
**適用対象:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 以降では、`error_file_path` は Azure Blob Storage に格納することができます。

'errorfile_data_source_name' **以下に適用されます:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
名前付きの外部データ ソースで、インポート中に見つかったエラーを格納するエラー ファイルの Azure Blob Storage の場所を指しています。 外部データ ソースは、[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 で追加された `TYPE = BLOB_STORAGE` オプションを使用して作成する必要があります。 詳しくは、「[CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)」をご覧ください。

FIRSTROW **=** _first_row_ 最初に読み込む行の番号を指定します。 既定値は、指定されたデータ ファイルの先頭行です。 FIRSTROW は 1 から始まります。

> [!NOTE]
> FIRSTROW 属性は、列ヘッダーのスキップを目的としたものではありません。 ヘッダーのスキップは、BULK INSERT ステートメントではサポートされません。 行をスキップした場合、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ではフィールド ターミネータのみが調べられます。スキップした行のフィールドに含まれているデータの有効性は確認されません。

FIRE_TRIGGERS 一括読み込みの操作中に、インポート先のテーブルで定義されている挿入トリガーを実行します。 対象テーブルで INSERT 操作にトリガーが定義されている場合、そのトリガーは完了した各バッチに対して実行されます。

FIRE_TRIGGERS が指定されていない場合、挿入トリガーは実行されません。

FORMATFILE_DATASOURCE **=** 'data_source_name' **適用対象:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1.
インポートされるデータのスキーマを定義するフォーマット ファイルの Azure Blob Storage の場所を指している名前付きの外部データ ソースです。 外部データ ソースは、[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 で追加された `TYPE = BLOB_STORAGE` オプションを使用して作成する必要があります。 詳しくは、「[CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)」をご覧ください。

KEEPIDENTITY インポートしたデータ ファイルの ID 値 (複数可) を ID 列に使用することを指定します。 KEEPIDENTITY を指定しない場合、この列の ID 値は検証のみが行われ、インポートされません。この場合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、テーブルの作成時に指定された seed と増分値に基づいて、一意な値が自動的に割り当てられます。 データ ファイルにテーブルまたはビュー内の ID 列の値が含まれない場合は、フォーマット ファイルを使用して、データのインポート時にテーブルまたはビュー内の ID 列をスキップするよう指定します。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではこの列に一意な値が自動的に割り当てられます。 詳細については、「[DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)」をご覧ください。

ID 値の保持について詳しくは、「[データの一括インポート時の ID 値の保持 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)」をご覧ください。

KEEPNULLS 一括インポート操作時、空の列が挿入される場合は NULL 値が保持されます。その列の既定値は格納されません。 詳細については、「[一括インポート中の NULL の保持または既定値の使用 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)」をご覧ください。

KILOBYTES_PER_BATCH **=** _kilobytes_per_batch_ バッチあたりのデータの概算キロバイト数 (KB) を *kilobytes_per_batch* として指定します。 KILOBYTES_PER_BATCH の既定値はありません。 パフォーマンスに関する考慮事項については、このトピックで後述する「解説」を参照してください。

LASTROW **=** _last_row_ 最後に読み込む行の行番号を指定します。 既定値は 0 です。これは指定のデータ ファイルの最終行を表します。

MAXERRORS **=** _max_errors_ 一括インポート操作時に許容されるデータの構文エラーの最大数を指定します。この最大数に達すると、操作は取り消されます。 一括インポート操作でインポートできない行は無視され、それぞれ 1 つのエラーとしてカウントされます。 *max_errors* を指定しない場合の既定値は 10 です。

> [!NOTE]
> MAX_ERRORS オプションは、制約チェックや **money** および **bigint** のデータ型の変換には適用されません。

ORDER ( { *column* [ ASC | DESC ] } [ **,** ... *n* ] ) データ ファイル内のデータの並べ替え方法を指定する省略可能なヒントです。 インポートするデータをテーブル上のクラスター化インデックスに従って並べ替えると、一括インポートのパフォーマンスが向上します。 データ ファイルが異なる順序 (つまりクラスター化インデックス キーの順序以外の順) で並んでいる場合またはテーブルにクラスター化インデックスが存在しない場合、ORDER 句は無視されます。 指定する列の名前は、インポート先のテーブル内で有効な列の名前であることが必要です。 既定では、一括挿入操作はデータ ファイルが並べ替えられていないことを前提に実行されます。 最適な一括インポートのため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、インポートするデータが並べ替えられているかどうかも検証されます。

*n* 複数の列を指定できることを示すプレースホルダーです。

ROWS_PER_BATCH **=** _rows_per_batch_ データ ファイル内のデータ行の概算数を示します。

既定では、データ ファイル内のすべてのデータは単一のトランザクションとしてサーバーに送られ、バッチ内の行数はクエリ オプティマイザーには通知されません。 ROWS_PER_BATCH を値 > 0 で指定した場合、サーバーでは一括インポート操作の最適化にこの値が使用されます。 ROWS_PER_BATCH に指定する値は、実際の行数とほぼ同じにする必要があります。 パフォーマンスに関する考慮事項については、このトピックで後述する「解説」を参照してください。

TABLOCK 一括インポート操作中にテーブル レベルのロックを取得します。 テーブルにインデックスがなく、TABLOCK を指定した場合は、複数のクライアントで同時に 1 つのテーブルを読み込むことができます。 既定では、ロック動作はテーブル オプション **table lock on bulk load**によって決定されます。 一括インポート操作中にロックを維持すると、テーブル ロックの競合が少なくなるので、場合によってはパフォーマンスが大幅に向上します。 パフォーマンスに関する考慮事項については、このトピックで後述する「解説」を参照してください。

列ストア インデックスの場合。 複数の行セットに内部的に分かれているため、ロックの動作が異なります。各スレッドは、行セットに対して X ロックを取得して同時実行データ読み込みセッションによる並列データ読み込みを許可することで、それぞれの行セットにデータを排他的に読み込みます。 TABLOCK オプションを使用すると、スレッドは (従来の行セットの BU ロックとは異なり) テーブルに対して X ロックを取得し、他の同時実行スレッドが同時にデータを読み込むのを防ぎます。

### <a name="input-file-format-options"></a>入力ファイル フォーマットのオプション

FORMAT **=** 'CSV' **以下に適用されます:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
[RFC 4180](https://tools.ietf.org/html/rfc4180) 標準に準拠しているコンマ区切り値ファイルを指定します。

```sql
BULK INSERT Sales.Orders
FROM '\\SystemX\DiskZ\Sales\data\orders.csv'
WITH ( FORMAT='CSV');
```

FIELDQUOTE **=** 'field_quote' **以下に適用されます:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
CSV ファイルで引用符文字として使用される文字を指定します。 指定されていない場合は、[RFC 4180](https://tools.ietf.org/html/rfc4180) 標準の定義に従って引用符文字 (") が引用符文字として使用されます。

FORMATFILE **=** '_format_file_path_' フォーマット ファイルの完全なパスを指定します。 フォーマット ファイルには、格納済みの応答を含むデータ ファイルの内容が記述されています。これらの応答は同じテーブルまたはビューに対し **bcp** ユーティリティを実行して作成されたものです。 フォーマット ファイルは次の場合に使用します。

- データ ファイルに含まれる列の数が、テーブルまたはビューより多い、または少ない。
- 列の順序が異なる。
- 列の区切り記号が異なる。
- データ形式に他に変更点がある。 フォーマット ファイルは通常、**bcp** ユーティリティを使用して作成し、必要に応じてテキスト エディターで修正します。 詳細については、「[bcp ユーティリティ](../../tools/bcp-utility.md)」と「[フォーマット ファイルの作成](../../relational-databases/import-export/create-a-format-file-sql-server.md)」を参照してください。

**適用対象:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 および Azure SQL Database。
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 以降では、format_file_path は Azure Blob Storage に格納することができます。

FIELDTERMINATOR **='** _field_terminator_ **'** **char** および **widechar** 型のデータ ファイルに使用するフィールド ターミネータを指定します。 既定のフィールド ターミネータは \t (タブ文字) です。 詳細については、「 [フィールド ターミネータと行ターミネータの指定 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)」を参照してください。

ROWTERMINATOR **='** _row_terminator_ **'** **char** および **widechar** 型のデータ ファイルに使用する行ターミネータを指定します。 既定の行ターミネータは **\r\n** (改行文字) です。 詳細については、「 [フィールド ターミネータと行ターミネータの指定 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)」を参照してください。

## <a name="compatibility"></a>互換性

BULK INSERT によって、ファイルから読み込んだデータに対して厳密なデータ検証とデータ チェックが実行されるので、無効なデータを使用して既存のスクリプトを実行すると、スクリプトは失敗する可能性があります。 たとえば、BULK INSERT では次の検証が行われます。

- **float** データ型または **real** データ型のネイティブ表記が有効かどうか。
- Unicode データが偶数バイト長かどうか。

## <a name="data-types"></a>データ型

### <a name="string-to-decimal-data-type-conversions"></a>文字列から 10 進数へのデータ型変換

BULK INSERT で使用される文字列から 10 進数へのデータ型変換には、[!INCLUDE[tsql](../../includes/tsql-md.md)] の [CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) 関数と同じ規則が適用されるので、科学的表記法を使用した数値を表す文字列は拒否されます。 したがって、BULK INSERT では、そのような文字列は無効な値として処理され、変換エラーが報告されます。

この問題を回避するには、科学的表記法の **float** 型のデータを 10 進数の列に一括インポートするフォーマット ファイルを使用します。 フォーマット ファイルには、列のデータを明示的に **real** または **float** 型として記述します。 これらのデータ型の詳細については、[float 型と real 型 &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)を参照してください。

> [!NOTE]
> フォーマット ファイル **real** データとして、 **SQLFLT4** データ型と **float** データとして、 **SQLFLT8** データ型。 XML 以外のフォーマット ファイルについては、「[bcp を使用したファイル ストレージ型の指定 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)」をご覧ください。

#### <a name="example-of-importing-a-numeric-value-that-uses-scientific-notation"></a>科学的表記法を使用した数値をインポートする例

この例では、次のテーブルを使用します。

```sql
CREATE TABLE t_float(c1 float, c2 decimal (5,4));
```

 ここでの目的は、`t_float` テーブルにデータを一括インポートすることです。 データ ファイル C:\t_float-c.dat には、次のような科学的表記法の **float** 型のデータが含まれています。

```input
8.0000000000000002E-28.0000000000000002E-2
```

しかし、テーブルの 2 番目の列 `t_float` で `c2` データ型を使用しているので、このデータを BULK INSERT によって `decimal` に直接インポートすることはできません。 そのため、フォーマット ファイルが必要です。 フォーマット ファイルでは、科学的表記法の **float** 型のデータを列 `c2` の 10 進形式にマップする必要があります。

次のフォーマット ファイルでは、`SQLFLT8` データ型を使用して、2 番目のデータ フィールドを 2 番目の列にマップしています。

```xml
<?xml version="1.0"?>
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
<RECORD>
<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="30"/>
<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="30"/> </RECORD> <ROW>
<COLUMN SOURCE="1" NAME="c1" xsi:type="SQLFLT8"/>
<COLUMN SOURCE="2" NAME="c2" xsi:type="SQLFLT8"/> </ROW> </BCPFORMAT>
```

このフォーマット ファイル (ファイル名 `C:\t_floatformat-c-xml.xml`) を使用してテスト テーブルにテスト データをインポートするには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行します。

```sql
BULK INSERT bulktest..t_float
FROM 'C:\t_float-c.dat' WITH (FORMATFILE='C:\t_floatformat-c-xml.xml');
```

> [!IMPORTANT]
> Azure SQL Database でサポートされるのは、Azure Blob Storage からの読み取りのみです。

### <a name="data-types-for-bulk-exporting-or-importing-sqlxml-documents"></a>SQLXML ドキュメントの一括エクスポートまたは一括インポート用のデータ型

SQLXML データを一括エクスポートまたは一括インポートするには、フォーマット ファイルで次のいずれかのデータ型を使用します。

|データ型|結果|
|---------------|------------|
|SQLCHAR または SQLVARCHAR|データは、クライアント コード ページまたは照合順序で暗黙的に指定されるコード ページで送られます。 フォーマット ファイルを指定せずに DATAFILETYPE **='char'** を指定した場合と同じ結果が得られます。|
|SQLNCHAR または SQLNVARCHAR|データは Unicode として送られます。 フォーマット ファイルを指定せずに DATAFILETYPE **= 'widechar'** を指定した場合と同じ結果が得られます。|
|SQLBINARY または SQLVARBIN|データは変換なしで送られます。|
| &nbsp; | &nbsp; |

## <a name="general-remarks"></a>全般的な解説

BULK INSERT ステートメント、INSERT ... SELECT \* FROM OPENROWSET(BULK...) ステートメントおよび **bcp** コマンドについては、「[データの一括インポートと一括エクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)」をご覧ください。

データを一括インポート用に準備する方法については、「[一括エクスポートまたは一括インポートのデータの準備 &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)」をご覧ください。

BULK INSERT ステートメントは、テーブルまたはビューにデータをインポートするために、ユーザー定義のトランザクション内で実行できます。 必要に応じて、一括インポート データの複数の一致を使用するために、トランザクションでは BULK INSERT ステートメント内に BATCHSIZE 句を指定できます。 複数のバッチのトランザクションをロールバックする場合、トランザクションが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に送信したすべてのバッチがロールバックされます。

## <a name="interoperability"></a>相互運用性

### <a name="importing-data-from-a-csv-file"></a>CSV ファイルからのデータのインポート

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 以降では、Azure SQL Database と同じように、BULK INSERT で CSV 形式がサポートされます。
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 より前は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の一括インポート操作ではコンマ区切り値 (CSV) ファイルがサポートされていません。 ただし、場合によっては、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に対してデータを一括インポートする際、CSV ファイルをデータ ファイルとして使用できます。 CSV データ ファイルからデータをインポートするための要件については、「[一括エクスポートまたは一括インポートのデータの準備 &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)」をご覧ください。

## <a name="logging-behavior"></a>ログ記録の動作

 SQL Server への一括インポートによって実行される行挿入操作がトランザクション ログに記録される条件について詳しくは、「[一括インポートで最小ログ記録を行うための前提条件](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)」をご覧ください。 最小ログ記録は、Azure SQL Database ではサポートされていません。

## <a name="Limitations"></a> 制限

BULK INSERT でフォーマット ファイルを使用する場合、指定できるフィールド数は 1,024 個までです。 これは、テーブルに許容される最大列数と同じです。 フォーマット ファイルを使用して、1,024 個を超えるフィールドが含まれるデータ ファイルで BULK INSERT を使用すると、BULK INSERT によってエラー 4822 が生成されます。 [bcp ユーティリティ](../../tools/bcp-utility.md)にはこのような制限がないため、1,024 個を超えるフィールドを含むデータ ファイルには、フォーマット ファイルを使用せずに BULK INSERT を使用するか、**bcp** コマンドを使用してください。

## <a name="performance-considerations"></a>パフォーマンスに関する考慮事項

1 つのバッチでフラッシュされるページの数が内部しきい値を超えると、バッチのコミット時にフラッシュするページを特定するためにバッファー プールのフル スキャンが行われる可能性があります。 フル スキャンが行われると、一括インポートのパフォーマンスが低下します。 この内部しきい値の問題は、大きなバッファー プールと遅い I/O サブシステムの組み合わせでも発生します。 大規模なコンピューターでバッファー オーバーフローを防ぐには、TABLOCK ヒントを使用しないようにするか (一括インポートの最適化は行われなくなります)、バッチ サイズを小さくします (一括インポートの最適化は引き続き行われます)。

コンピューターはそれぞれ異なるため、実際のデータでさまざまなバッチ サイズを試して最適な値を見つけるようにすることをお勧めします。

Azure SQL Database では、大量のデータをインポートする場合、インポートの前にデータベースまたはインスタンスのパフォーマンス レベルを一時的に上げることを検討してください。

## <a name="security"></a>Security

### <a name="security-account-delegation-impersonation"></a>セキュリティ アカウントの委任 (権限借用)

ユーザーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを使用する場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス アカウントのセキュリティ プロファイルが使用されます。 SQL Server 認証を使用したログインは、データベース エンジン以外では認証できません。 そのため、SQL Server 認証を使用したログインによって BULK INSERT コマンドが開始されると、SQL Server プロセス アカウント (SQL Server データベース エンジン サービスで使用されるアカウント) のセキュリティ コンテキストを使用してデータへの接続が行われます。 ソース データを正しく読み取るには、SQL Server データベース エンジンで使用されるアカウントに対して、ソース データへのアクセス権を付与する必要があります。これに対して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーが Windows 認証を使用してログインした場合、そのユーザーは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスのセキュリティ プロファイルに関係なく、そのユーザー アカウントでアクセス可能なファイルのみを読み取ることができます。

あるコンピューターで **sqlcmd** または **osql** を使用して BULK INSERT ステートメントを実行し、2 台目のコンピューターの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にデータを挿入し、UNC パスを使用して 3 台目のコンピューターの *data_file* を指定した場合、エラー 4861 が返されることがあります。

この問題を解決するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス アカウントのセキュリティ プロファイルを使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定します。または、Windows の構成でセキュリティ アカウントの委任を有効にします。 ユーザー アカウントの信頼性を委任の対象として有効にする方法の詳細については、Windows ヘルプを参照してください。

BULK INSERT を使用する場合のこのセキュリティの考慮事項またはその他のセキュリティの考慮事項について詳しくは、「[BULK INSERT または OPENROWSET&#40;BULK...&#41; を使用した一括データのインポート &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)」をご覧ください。

Azure Blob Storage からパブリック (匿名アクセス) ではないデータをインポートするときは、[MASTER KEY](create-master-key-transact-sql.md) で暗号化された SAS キーに基づいて [DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md) を作成した後、BULK INSERT コマンドで使用する[外部データベース ソース](../../t-sql/statements/create-external-data-source-transact-sql.md)を作成します。 例については、「[Azure Blob Storage 内のファイルからデータをインポートする](#f-importing-data-from-a-file-in-azure-blob-storage)」を参照してください。

### <a name="permissions"></a>アクセス許可

INSERT 権限および ADMINISTER BULK OPERATIONS 権限が必要です。 Azure SQL Database では、INSERT および ADMINISTER DATABASE BULK OPERATIONS 権限が必要です。 ただし次のことが 1 つまたは複数当てはまる場合は、さらに ALTER TABLE 権限が必要になります。

- 制約が存在する場合に、CHECK_CONSTRAINTS オプションを指定しない。

   > [!NOTE]
   > 制約の無効化は既定の動作です。 制約を明示的に検証するには、CHECK_CONSTRAINTS オプションを使用します。

- トリガーが存在する場合に、FIRE_TRIGGER オプションを指定しない。

   > [!NOTE]
   > 既定では、トリガーは起動しません。 トリガーを明示的に起動するには、FIRE_TRIGGERS オプションを使用します。

- KEEPIDENTITY オプションを使用して、データ ファイルから ID 値をインポートする。

## <a name="examples"></a>例

### <a name="a-using-pipes-to-import-data-from-a-file"></a>A. ファイルからのデータのインポートにパイプを使用する

次の例では、パイプ (`|`) をフィールド ターミネータ、`|\n` を行ターミネータとして使用し、指定のデータ ファイルから `AdventureWorks2012.Sales.SalesOrderDetail` テーブルに、注文の詳細情報をインポートします。

```sql
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail
   FROM 'f:\orders\lineitem.tbl'
   WITH
      (  
         FIELDTERMINATOR =' |'
         , ROWTERMINATOR =' |\n'
      );
```

> [!IMPORTANT]
> Azure SQL Database でサポートされるのは、Azure Blob Storage からの読み取りのみです。

### <a name="b-using-the-fire_triggers-argument"></a>B. FIRE_TRIGGERS 引数を使用する

次の例では、`FIRE_TRIGGERS` 引数を指定します。

```sql
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail
   FROM 'f:\orders\lineitem.tbl'
   WITH
     (
         FIELDTERMINATOR =' |'
         , ROWTERMINATOR = ':\n'
         , FIRE_TRIGGERS
      );
```

> [!IMPORTANT]
> Azure SQL Database でサポートされるのは、Azure Blob Storage からの読み取りのみです。

### <a name="c-using-line-feed-as-a-row-terminator"></a>C. 行ターミネータとしてライン フィードを使用する

 次の例では、UNIX 出力などのように、ライン フィードを行ターミネータとして使用するファイルをインポートします。

```sql
DECLARE @bulk_cmd varchar(1000);
SET @bulk_cmd = 'BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail
FROM ''<drive>:\<path>\<filename>''
WITH (ROWTERMINATOR = '''+CHAR(10)+''')';
EXEC(@bulk_cmd);
```

> [!NOTE]
> Microsoft Windows によるテキスト ファイルの処理方法によって、 **(\n** は自動的に **\r\n)** に置き換えられます。

> [!IMPORTANT]
> Azure SQL Database でサポートされるのは、Azure Blob Storage からの読み取りのみです。

### <a name="d-specifying-a-code-page"></a>D. コード ページの指定

コード ページを指定する例を次に示します。

```sql
BULK INSERT MyTable
FROM 'D:\data.csv'
WITH
( CODEPAGE = '65001'
   , DATAFILETYPE = 'char'
   , FIELDTERMINATOR = ','
);
```

> [!IMPORTANT]
> Azure SQL Database でサポートされるのは、Azure Blob Storage からの読み取りのみです。

### <a name="e-importing-data-from-a-csv-file"></a>E. CSV ファイルからデータをインポートする

次の例は、`;` をフィールド ターミネータ、`0x0a` を行ターミネータとして使用して、ヘッダー (先頭行) をスキップして CSV ファイルを指定する方法を示しています。

```sql
BULK INSERT Sales.Invoices
FROM '\\share\invoices\inv-2016-07-25.csv'
WITH (FORMAT = 'CSV'
      , FIRSTROW=2
      , FIELDQUOTE = '\'
      , FIELDTERMINATOR = ';'
      , ROWTERMINATOR = '0x0a');
```

> [!IMPORTANT]
> Azure SQL Database でサポートされるのは、Azure Blob Storage からの読み取りのみです。

### <a name="f-importing-data-from-a-file-in-azure-blob-storage"></a>F. Azure Blob Storage 内のファイルからデータをインポートする

次の例では、SAS キーを作成した Azure Blob Storage の場所にある csv ファイルからデータを読み込む方法を示します。 Azure Blob Storage の場所は、外部データ ソースとして構成されます。 これには、ユーザー データベース内でマスター キーを使用して暗号化された共有アクセス署名を使用するデータベース スコープ資格情報が必要です。

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
> Azure SQL Database でサポートされるのは、Azure Blob Storage からの読み取りのみです。

### <a name="g-importing-data-from-a-file-in-azure-blob-storage-and-specifying-an-error-file"></a>G. Azure Blob Storage 内のファイルからデータをインポートし、エラー ファイルを指定する

次の例では、外部データ ソースとして構成されている Azure Blob Storage の場所に csv ファイルからデータを読み込み、エラー ファイルも指定する方法を示します。 これには、Shared Access Signature を使用したデータベース スコープ資格情報が必要です。 Azure SQL Database を実行している場合、ERRORFILE オプションと共に ERRORFILE_DATA_SOURCE も指定する必要があることに注意してください。指定しないと、アクセス許可エラーでインポートが失敗する可能性があります。 ERRORFILE で指定するファイルは、コンテナー内に存在していてはなりません。

```sql
BULK INSERT Sales.Invoices
FROM 'inv-2017-12-08.csv'
WITH (
         DATA_SOURCE = 'MyAzureInvoices'
         , FORMAT = 'CSV'
         , ERRORFILE = 'MyErrorFile'
         , ERRORFILE_DATA_SOURCE = 'MyAzureInvoices');
```

資格情報と外部データ ソースの構成などの `BULK INSERT` の詳細な例については、「[Azure BLOB ストレージのデータに一括アクセスする例](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)」をご覧ください。

### <a name="additional-examples"></a>その他の例

 `BULK INSERT` のその他の例については、次のトピックをご覧ください。

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

## <a name="see-also"></a>参照

- [データの一括インポートと一括エクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)
- [bcp ユーティリティ](../../tools/bcp-utility.md)
- [データのインポートまたはエクスポート用のフォーマット ファイル &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)
- [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)
- [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)
- [一括エクスポートまたは一括インポートのデータの準備 &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)
- [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)
