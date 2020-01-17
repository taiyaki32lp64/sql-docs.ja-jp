---
title: CREATE TABLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILESTREAM_TSQL
- TABLE
- CREATE_TABLE_TSQL
- CREATE TABLE
- FILESTREAM
- TABLE_TSQL
- FILESTREAM_ON
- FILESTREAM_ON_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHECK constraints
- global temporary tables [SQL Server]
- local temporary tables [SQL Server]
- size [SQL Server], tables
- UNIQUE constraints [SQL Server], creating
- constraints [SQL Server], columns
- maximum number of indexes per table
- number of tables per database
- number of indexes per table
- table creation [SQL Server], CREATE TABLE
- temporary tables [SQL Server], creating
- table size [SQL Server]
- nullability [SQL Server]
- partitioned tables [SQL Server], creating
- DEFAULT definition
- null values [SQL Server], columns
- number of rows per table
- maximum number of columns per table
- FOREIGN KEY constraints, creating
- PRIMARY KEY constraints
- number of bytes per row
- CREATE TABLE statement
- number of columns per table
- maximum number of bytes per row
ms.assetid: 1e068443-b9ea-486a-804f-ce7b6e048e8b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a4730cf8487b244502e339b5ea820e7ad9d160b6
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982740"
---
# <a name="create-table-transact-sql"></a>CREATE TABLE (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] で新しいテーブルを作成します。

> [!NOTE]
> [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 構文については、「[CREATE TABLE (Azure SQL Data Warehouse)](../../t-sql/statements/create-table-azure-sql-data-warehouse.md)」をご覧ください。

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="simple-syntax"></a>簡単な構文

```
-- Simple CREATE TABLE Syntax (common if not using options)
CREATE TABLE
    { database_name.schema_name.table_name. | schema_name.table_name | table_name }
    ( { <column_definition> } [ ,...n ] )
[ ; ]
```

## <a name="full-syntax"></a>完全な構文

```
-- Disk-Based CREATE TABLE Syntax
CREATE TABLE
    { database_name.schema_name.table_name | schema_name.table_name | table_name }
    [ AS FileTable ]
    ( {   <column_definition>
        | <computed_column_definition>
        | <column_set_definition>
        | [ <table_constraint> ] [ ,... n ]
        | [ <table_index> ] }
          [ ,...n ]
          [ PERIOD FOR SYSTEM_TIME ( system_start_time_column_name
             , system_end_time_column_name ) ]
      )
    [ ON { partition_scheme_name ( partition_column_name )
           | filegroup
           | "default" } ]
    [ TEXTIMAGE_ON { filegroup | "default" } ]
    [ FILESTREAM_ON { partition_scheme_name
           | filegroup
           | "default" } ]
    [ WITH ( <table_option> [ ,...n ] ) ]
[ ; ]
  
<column_definition> ::=
column_name <data_type>
    [ FILESTREAM ]
    [ COLLATE collation_name ]
    [ SPARSE ]
    [ MASKED WITH ( FUNCTION = ' mask_function ') ]
    [ CONSTRAINT constraint_name [ DEFAULT constant_expression ] ]
    [ IDENTITY [ ( seed,increment ) ]
    [ NOT FOR REPLICATION ]
    [ GENERATED ALWAYS AS ROW { START | END } [ HIDDEN ] ]
    [ NULL | NOT NULL ]
    [ ROWGUIDCOL ]
    [ ENCRYPTED WITH
        ( COLUMN_ENCRYPTION_KEY = key_name ,
          ENCRYPTION_TYPE = { DETERMINISTIC | RANDOMIZED } ,
          ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'
        ) ]
    [ <column_constraint> [, ...n ] ]
    [ <column_index> ]
  
<data_type> ::=
[ type_schema_name . ] type_name
    [ ( precision [ , scale ] | max |
        [ { CONTENT | DOCUMENT } ] xml_schema_collection ) ]
  
<column_constraint> ::=
[ CONSTRAINT constraint_name ]
{     { PRIMARY KEY | UNIQUE }
        [ CLUSTERED | NONCLUSTERED ]
        [
            WITH FILLFACTOR = fillfactor
          | WITH ( < index_option > [ , ...n ] )
        ]
        [ ON { partition_scheme_name ( partition_column_name )
            | filegroup | "default" } ]
  
  | [ FOREIGN KEY ]
        REFERENCES [ schema_name . ] referenced_table_name [ ( ref_column ) ]
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ NOT FOR REPLICATION ]
  
  | CHECK [ NOT FOR REPLICATION ] ( logical_expression )
}
  
<column_index> ::=
 INDEX index_name [ CLUSTERED | NONCLUSTERED ]
    [ WITH ( <index_option> [ ,... n ] ) ]
    [ ON { partition_scheme_name (column_name )
         | filegroup_name
         | default
         }
    ]
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]
  
<computed_column_definition> ::=
column_name AS computed_column_expression
[ PERSISTED [ NOT NULL ] ]
[
    [ CONSTRAINT constraint_name ]
    { PRIMARY KEY | UNIQUE }
        [ CLUSTERED | NONCLUSTERED ]
        [
            WITH FILLFACTOR = fillfactor
          | WITH ( <index_option> [ , ...n ] )
        ]
        [ ON { partition_scheme_name ( partition_column_name )
        | filegroup | "default" } ]
  
    | [ FOREIGN KEY ]
        REFERENCES referenced_table_name [ ( ref_column ) ]
        [ ON DELETE { NO ACTION | CASCADE } ]
        [ ON UPDATE { NO ACTION } ]
        [ NOT FOR REPLICATION ]
  
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )
]
  
<column_set_definition> ::=
column_set_name XML COLUMN_SET FOR ALL_SPARSE_COLUMNS
  
< table_constraint > ::=
[ CONSTRAINT constraint_name ]
{
    { PRIMARY KEY | UNIQUE }
        [ CLUSTERED | NONCLUSTERED ]
        (column [ ASC | DESC ] [ ,...n ] )
        [
            WITH FILLFACTOR = fillfactor
           |WITH ( <index_option> [ , ...n ] )
        ]
        [ ON { partition_scheme_name (partition_column_name)
            | filegroup | "default" } ]
    | FOREIGN KEY
        ( column [ ,...n ] )
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ NOT FOR REPLICATION ]
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )

< table_index > ::=
{  
    {  
      INDEX index_name [ CLUSTERED | NONCLUSTERED ]
         (column_name [ ASC | DESC ] [ ,... n ] )
    | INDEX index_name CLUSTERED COLUMNSTORE
    | INDEX index_name [ NONCLUSTERED ] COLUMNSTORE (column_name [ ,... n ] )
    }
    [ WITH ( <index_option> [ ,... n ] ) ]
    [ ON { partition_scheme_name (column_name )
         | filegroup_name
         | default
         }
    ]
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]
  
}

<table_option> ::=
{  
    [DATA_COMPRESSION = { NONE | ROW | PAGE }
      [ ON PARTITIONS ( { <partition_number_expression> | <range> }
      [ , ...n ] ) ]]
    [ FILETABLE_DIRECTORY = <directory_name> ]
    [ FILETABLE_COLLATE_FILENAME = { <collation_name> | database_default } ]
    [ FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME = <constraint_name> ]
    [ FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME = <constraint_name> ]
    [ FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME = <constraint_name> ]
    [ SYSTEM_VERSIONING = ON [ ( HISTORY_TABLE = schema_name . history_table_name
        [, DATA_CONSISTENCY_CHECK = { ON | OFF } ] ) ] ]
    [ REMOTE_DATA_ARCHIVE =
      {
          ON [ ( <table_stretch_options> [,...n] ) ]
        | OFF ( MIGRATION_STATE = PAUSED )
      }
    ]
}
  
<table_stretch_options> ::=
{  
    [ FILTER_PREDICATE = { null | table_predicate_function } , ]
      MIGRATION_STATE = { OUTBOUND | INBOUND | PAUSED }
 }
  
<index_option> ::=
{
    PAD_INDEX = { ON | OFF }
  | FILLFACTOR = fillfactor
  | IGNORE_DUP_KEY = { ON | OFF }
  | STATISTICS_NORECOMPUTE = { ON | OFF }
  | STATISTICS_INCREMENTAL = { ON | OFF }
  | ALLOW_ROW_LOCKS = { ON | OFF }
  | ALLOW_PAGE_LOCKS = { ON | OFF }
  | OPTIMIZE_FOR_SEQUENTIAL_KEY = { ON | OFF }
  | COMPRESSION_DELAY= {0 | delay [Minutes]}
  | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }
       [ ON PARTITIONS ( { <partition_number_expression> | <range> }
       [ , ...n ] ) ]
}
<range> ::=
<partition_number_expression> TO <partition_number_expression>
```

```
-- Memory optimized CREATE TABLE Syntax
CREATE TABLE
    { database_name.schema_name.table_name | schema_name.table_name | table_name }
    ( { <column_definition>
    | [ <table_constraint> ] [ ,... n ]
    | [ <table_index> ]
      [ ,... n ] }
      [ PERIOD FOR SYSTEM_TIME ( system_start_time_column_name
        , system_end_time_column_name ) ]
)
    [ WITH ( <table_option> [ ,... n ] ) ]
 [ ; ]

<column_definition> ::=
column_name <data_type>
    [ COLLATE collation_name ]
    [ GENERATED ALWAYS AS ROW { START | END } [ HIDDEN ] ]
    [ NULL | NOT NULL ]
[
    [ CONSTRAINT constraint_name ] DEFAULT memory_optimized_constant_expression ]
    | [ IDENTITY [ ( 1, 1 ) ]
]
    [ <column_constraint> ]
    [ <column_index> ]
  
<data_type> ::=
 [type_schema_name . ] type_name [ (precision [ , scale ]) ]

<column_constraint> ::=
 [ CONSTRAINT constraint_name ]
{
  { PRIMARY KEY | UNIQUE }
      {   NONCLUSTERED
        | NONCLUSTERED HASH WITH (BUCKET_COUNT = bucket_count)
      }
  | [ FOREIGN KEY ]
        REFERENCES [ schema_name . ] referenced_table_name [ ( ref_column ) ]
  | CHECK ( logical_expression )
}
  
< table_constraint > ::=
 [ CONSTRAINT constraint_name ]
{
   { PRIMARY KEY | UNIQUE }
     {
       NONCLUSTERED (column [ ASC | DESC ] [ ,... n ])
       | NONCLUSTERED HASH (column [ ,... n ] ) WITH ( BUCKET_COUNT = bucket_count )
                    }
    | FOREIGN KEY
        ( column [ ,...n ] )
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]
    | CHECK ( logical_expression )
}

<column_index> ::=
  INDEX index_name
{ [ NONCLUSTERED ] | [ NONCLUSTERED ] HASH WITH (BUCKET_COUNT = bucket_count)}

<table_index> ::=
  INDEX index_name
{   [ NONCLUSTERED ] HASH (column [ ,... n ] ) WITH (BUCKET_COUNT = bucket_count)
  | [ NONCLUSTERED ] (column [ ASC | DESC ] [ ,... n ] )
      [ ON filegroup_name | default ]
  | CLUSTERED COLUMNSTORE [WITH ( COMPRESSION_DELAY = {0 | delay [Minutes]})]
      [ ON filegroup_name | default ]
  
}
  
<table_option> ::=
{  
    MEMORY_OPTIMIZED = ON
  | DURABILITY = {SCHEMA_ONLY | SCHEMA_AND_DATA}
  | SYSTEM_VERSIONING = ON [ ( HISTORY_TABLE = schema_name . history_table_name
        [, DATA_CONSISTENCY_CHECK = { ON | OFF } ] ) ]
  
}
```

## <a name="arguments"></a>引数

*database_name*: テーブルが作成されるデータベースの名前です。 *database_name* には、既存のデータベース名を指定する必要があります。 指定しない場合、*database_name* は現在のデータベースに設定されます。 現在の接続に対するログインには、*database_name* で指定されたデータベース内の既存のユーザー ID を関連付け、そのユーザー ID に CREATE TABLE 権限を許可しておく必要があります。

*schema_name*: 新しいテーブルが所属するスキーマの名前です。

*table_name*: 新しいテーブルの名前です。 テーブル名は[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従っている必要があります。 116 文字までしか使用できないローカル一時テーブル名 (名前の先頭に 1 つの番号記号 (#) が付加されます) を除き、*table_name* には、最大 128 文字を使用できます。

AS FileTable **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降)。

新しいテーブルを FileTable として作成します。 FileTable には固定スキーマがあるため、列は指定しません。 詳細については、「[FileTables](../../relational-databases/blob/filetables-sql-server.md)」を参照してください。

*column_name*
*computed_column_expression*: 計算列の値を定義する式です。 計算列は、PERSISTED とマークされていない限り、テーブルに物理的に保存されない仮想列です。 この列は、同じテーブルの他の列を使用する式から計算されます。 たとえば、計算列は **cost** AS **price** \* **qty** として定義されます。式には、非計算列の名前、定数、関数、変数、および 1 つ以上の演算子によってこれらを結合した組み合わせを使用できます。 式をサブクエリにすることはできません。また、別名データ型を含めることはできません。

計算列は、選択リスト、WHERE 句、ORDER BY 句、その他標準式が使用できる任意の位置で使用できます。ただし、次の場合は除きます。

- FOREIGN KEY 制約または CHECK 制約で使用される計算列は、PERSISTED に設定する必要があります。
- 計算列の値が決定的な式によって定義され、その結果のデータ型がインデックス列で許可される場合、計算列は、インデックスのキー列として、または任意の PRIMARY KEY 制約や UNIQUE 制約の一部として使用できます。

   たとえば、テーブルに整数型の列 **a** と **b** がある場合、計算列 **a+b** にはインデックスを作成できますが、計算列 **a+DATEPART(dd, GETDATE())** にインデックスを作成することはできません。これは、この計算列の値が次の呼び出しで変更される可能性があるためです。

- 計算列を INSERT ステートメントまたは UPDATE ステートメントの対象にすることはできません。

> [!NOTE]
> テーブル内の各行は、計算列に関係する列に対して異なる値を持つ場合があります。そのため、計算列が各行について同じ値を持たない場合があります。

計算列で NULL 値を許容するかどうかは、使用されている式に基づいて[!INCLUDE[ssDE](../../includes/ssde-md.md)]によって自動的に決定されます。 null 値を許容しない列しかない場合でも、ほとんどの式の結果は null 値を許容すると見なされます。これは、アンダーフローやオーバーフローによって結果が null 値になる場合があるためです。 テーブルの任意の計算列で NULL 値が許容されるかどうかを調べるには、`COLUMNPROPERTY` 関数で **AllowsNull** プロパティを使用します。 NULL 値が許容される式を、NULL 値を許容しない式に変換するには、`ISNULL` に *check_expression* 定数を指定します。この定数は、NULL 値の結果の代わりに使用される NULL 以外の値です。 共通言語ランタイム (CLR) のユーザー定義型の式に基づく計算列では、その型に対する REFERENCES 権限が必要です。

PERSISTED: [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] により計算値が物理的にテーブルに格納され、計算列が依存している他の列のいずれかが更新されるとその値が更新されることを指定します。 計算列を `PERSISTED` とマークすることで、計算列に対して決定論的なインデックスを作成することができますが、正確ではありません。 詳細については、「 [計算列のインデックス](../../relational-databases/indexes/indexes-on-computed-columns.md)」を参照してください。 パーティション テーブルのパーティション分割列として使用される計算列は、明示的に `PERSISTED` に設定する必要があります。 `PERSISTED` が指定されている場合、*computed_column_expression* は決定論的である必要があります。

ON { *partition_scheme* | *filegroup* |  **"default"** } テーブルが格納されるパーティション構成またはファイル グループを指定します。 *partition_scheme* を指定すると、テーブルはパーティション テーブルとなり、各パーティションは *partition_scheme* で指定した 1 つ以上のファイル グループに格納されます。 *filegroup* を指定すると、テーブルは指定されたファイル グループに格納されます。 ファイル グループがデータベース内に存在している必要があります。 **"default"** を指定するか、ON をまったく指定しないと、テーブルは既定のファイル グループに格納されます。 CREATE TABLE で指定したテーブルの格納方法を後から変更することはできません。

ON {*partition_scheme* | *filegroup* |  **"default"** } は、PRIMARY KEY 制約または UNIQUE 制約で指定することもできます。 これらの制約はインデックスを作成します。 *filegroup* を指定すると、インデックスは指定されたファイル グループに格納されます。 **"default"** を指定するか、ON を指定しなかった場合、インデックスはテーブルと同じファイル グループに格納されます。 `PRIMARY KEY` または `UNIQUE` 制約によりクラスター化インデックスが作成される場合、テーブルのデータ ページはインデックスと同じファイル グループに格納されます。 `CLUSTERED` を指定するか、制約によりクラスター化インデックスを作成し、テーブル定義の *partition_scheme* または *filegroup* とは異なる *partition_scheme* (またはその逆) を指定すると、制約定義だけが優先され、それ以外は無視されます。

> [!NOTE]
> このコンテキストでは、*default* はキーワードではありません。 これは、既定ファイル グループの識別子なので、ON **"default"** または ON **[** default **]** のように区切る必要があります。 **"default"** を指定する場合は、現在のセッションに対して `QUOTED_IDENTIFIER` オプションが ON である必要があります。 これが既定の設定です。 詳しくは、「[SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md)」をご覧ください。
>
> パーティション テーブルを作成した後、テーブルの `LOCK_ESCALATION` オプションを `AUTO` に設定することを検討してください。 これにより、テーブルではなくパーティション (HoBT) レベルにロックをエスカレートできるようにすることで、コンカレンシーを向上させることができます。 詳細については、「[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)」を参照してください。

TEXTIMAGE_ON { *filegroup*|  **"default"** } **text**、**ntext**、**image**、**xml**、**varchar(max)** 、**nvarchar(max)** 、**varbinary(max)** 、および CLR ユーザー定義型の列 (geometry や geography など) が、指定したファイル グループに格納されることを示します。

テーブル内に値の大きな列がない場合は、`TEXTIMAGE_ON` は指定できません。 *partition_scheme* を指定した場合は、`TEXTIMAGE_ON` を指定できません。 **"default"** を指定するか、`TEXTIMAGE_ON` をまったく指定しないと、値の大きな列は既定のファイル グループに格納されます。 `CREATE TABLE` で指定した値の大きな列のデータのストレージを、後から変更することはできません。

> [!NOTE]
> Varchar(max)、nvarchar(max)、varbinary(max)、xml および大きな UDT 値は、データ行に直接格納されます。レコードのサイズまで値を格納できますが、サイズの上限は 8,000 バイトです。 値がレコードに収まらない場合には、ポインターが行内に格納され、残りは行外の LOB ストレージ領域に格納されます。 0 は、すべての値がデータ行に直接格納されていることを示す既定値です。
>
> `TEXTIMAGE_ON` では、"LOB ストレージ領域" の場所のみが変更され、データが行内に格納されている場合は影響しません。 sp_tableoption の large value types out of row オプションを使用すると、LOB 値全体が行外に格納されます。
>
> このコンテキストでは、default はキーワードではありません。 これは、既定ファイル グループの識別子なので、`TEXTIMAGE_ON "default"` または `TEXTIMAGE_ON [default]` のように区切る必要があります。 **"default"** を指定する場合は、現在のセッションに対して `QUOTED_IDENTIFIER` オプションが ON である必要があります。 これが既定の設定です。 詳しくは、「[SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md)」をご覧ください。

FILESTREAM_ON { *partition_scheme_name* | filegroup | **"** default **"** }     
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] 以降)。 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、`FILESTREAM` はサポートされていません。

FILESTREAM データのファイル グループを指定します。

テーブルが FILESTREAM データを含んでおり、テーブルがパーティション分割されている場合、FILESTREAM_ON 句を使用して、FILESTREAM ファイル グループのパーティション構成を指定する必要があります。 このパーティション構成では、テーブルのパーティション構成と同じパーティション関数とパーティション列を使用する必要があります。それ以外の場合は、エラーが発生します。

テーブルがパーティション分割されていない場合、FILESTREAM 列をパーティション分割することはできません。 テーブルの FILESTREAM データは、単一のファイル グループに格納する必要があります。 このファイル グループは、FILESTREAM_ON 句で指定します。

テーブルがパーティション分割されておらず、`FILESTREAM_ON` 句も指定されていない場合、`DEFAULT` プロパティ セットが使用されている FILESTREAM ファイル グループが使用されます。 FILESTREAM ファイル グループがない場合は、エラーが発生します。

ON や `TEXTIMAGE_ON` と同様に、`FILESTREAM_ON` の `CREATE TABLE` を使用して設定された値は、次の場合を除いて変更できません。

- [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) ステートメントでヒープをクラスター化インデックスに変換する。 この場合は、異なる FILESTREAM ファイル グループ、パーティション構成、または NULL を指定できます。
- [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md) ステートメントでクラスター化インデックスをヒープに変換する。 この場合は、異なる FILESTREAM ファイル グループ、パーティション構成、または **"default"** を指定できます。

`FILESTREAM_ON <filegroup>` 句のファイル グループ、またはパーティション構成で指定されている各 FILESTREAM ファイル グループには、ファイルが 1 つ定義されている必要があります。 このファイルは、[CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017) ステートメントまたは [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) ステートメントを使用して定義する必要があります。それ以外の場合は、エラーが発生します。

FILESTREAM の関連トピックについては、[バイナリ ラージ オブジェクト - BLOB データ](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)に関するページをご覧ください。

[ _type\_schema\_name_ **.** ] *type_name*     
列のデータ型と、そのデータ型が所属するスキーマを指定します。 ディスク ベース テーブルの場合、データ型は次のいずれかです。

- システム データ型
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のシステム データ型に基づく別名型。 別名データ型は、`CREATE TYPE` ステートメントを使って作成した後、テーブル定義で使用できます。 別名データ型用の NULL/NOT NULL 割り当ては、`CREATE TABLE` ステートメントの中でオーバーライドできます。 ただし、長さ指定は変更できません。`CREATE TABLE` ステートメント中の別名データ型の長さは指定できません。
- CLR ユーザー定義型。 CLR ユーザー定義型をテーブル定義の中で使用するには、まず、`CREATE TYPE` ステートメントで CLR ユーザー定義型を作成する必要があります。 CLR ユーザー定義型の列を作成するには、その型に対する REFERENCES 権限が必要です。

*type_schema_name* を指定しない場合、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]は次の順序で *type_name* を参照します。

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のシステム データ型
- 現在のデータベースにおける現在のユーザーの既定のスキーマ。
- 現在のデータベースの **dbo** スキーマ。

メモリ最適化テーブルでサポートされるシステム型の一覧については、「[インメモリ OLTP に対してサポートされるデータ型](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md)」をご覧ください。

*有効桁数*      
指定されるデータ型の有効桁数です。 有効桁数の詳細については、「[有効桁数、小数点以下桁数、および長さ (Transact-SQL)](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)」を参照してください。

*小数点以下桁数*      
指定されるデータ型の小数点以下桁数です。 有効な小数点以下桁数の詳細については、「[有効桁数、小数点以下桁数、および長さ (Transact-SQL)](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)」を参照してください。

**最大**     
データ型 **varchar**、**nvarchar**、**varbinary** だけに適用され、2^31 バイトの文字データとバイナリ データ、および 2^30 バイトの Unicode データが格納されます。

CONTENT     
*column_name* 内の **xml** データ型の各インスタンスに、複数のトップレベル要素を含められることを指定します。 CONTENT は、**xml** データ型のみに適用され、*xml_schema_collection* も指定されている場合にだけ指定できます。 指定しない場合は、CONTENT が既定の動作となります。

DOCUMENT     
*column_name* 内の **xml** データ型の各インスタンスに、1 つのトップレベル要素のみを含められることを指定します。 DOCUMENT は、**xml** データ型のみに適用され、*xml_schema_collection* も指定されている場合にだけ指定できます。

*xml_schema_collection*     
**xml** データ型にのみ適用されます。XML スキーマ コレクションとこのデータ型を関連付けるためのものです。 スキーマで **xml** 列を使用するには、まず、[CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) を使用してデータベース内にスキーマを作成する必要があります。

DEFAULT    
挿入の際に明示的な値を指定しない場合に、列に入力される値を指定します。 DEFAULT 定義は、**timestamp** として定義された列または `IDENTITY` プロパティを持つ列以外のすべての列に適用できます。 ユーザー定義型の列に既定値を指定する場合は、その型で *constant_expression* 型からユーザー定義型への暗黙的な変換がサポートされている必要があります。 テーブルが削除されると、DEFAULT 定義は削除されます。 既定値として使用できるのは、文字列などの定数値、スカラー関数 (システム、ユーザー定義、CLR 関数のいずれか)、または NULL のみです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の旧バージョンとの互換性を保つため、DEFAULT に制約名を割り当てることができます。

*constant_expression*    
列の既定値として使用される定数、NULL またはシステム関数です。

*memory_optimized_constant_expression*     
列の既定値として使用できる定数、NULL、システム関数です。 ネイティブ コンパイル ストアド プロシージャでサポートされている必要があります。 ネイティブ コンパイル ストアド プロシージャの組み込み関数について詳しくは、「[ネイティブ コンパイル T-SQL モジュールでサポートされる機能](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)」をご覧ください。

IDENTITY    
新しい列が ID 列であることを指定します。 テーブルに行が新しく追加されると、[!INCLUDE[ssDE](../../includes/ssde-md.md)]は列に一意な増分の値を設定します。 ID 列は通常、PRIMARY KEY 制約と共に使用され、テーブルの一意な行識別子 (ROWID) の役割を果たします。 `IDENTITY` プロパティは、**tinyint**、**smallint**、**int**、**bigint**、**decimal(p,0)** 、**numeric(p,0)** のいずれかの列に割り当てることができます。 ID 列は 1 つのテーブルにつき 1 つだけ作成できます。 バインドされた既定値および DEFAULT 制約を ID 列と共に使用することはできません。 seed と increment の両方を指定するか、またはどちらも指定しません。 どちらも指定しないときの既定値は (1,1) です。

*seed*    
テーブルに読み込まれる最初の行に使用される値です。

*increment*    
読み込まれている前の行の ID 値に加算される増分値です。

NOT FOR REPLICATION    
`CREATE TABLE` ステートメントでは、IDENTITY プロパティ、FOREIGN KEY 制約、CHECK 制約で `NOT FOR REPLICATION` 句を指定できます。 `IDENTITY` プロパティでこの句を指定すると、レプリケーション エージェントが挿入を行うときに ID 列の値が増加されません。 制約でこの句を指定すると、レプリケーション エージェントが挿入、更新、削除操作を行う際に制約が適用されません。

GENERATED ALWAYS AS ROW { START | END } [ HIDDEN ] [ NOT NULL ]    
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。

指定した `datetime2` 列が、システムによって、レコードの有効期限の開始時刻またはレコードの有効期限の終了時刻のいずれかを記録するために使用されることを指定します。 列を `NOT NULL` として定義する必要があります。 それらを `NULL` として指定しようとすると、システムによりエラーがスローされます。 期間列に対して明示的に NOT NULL を指定しない場合、システムにより既定で列が `NOT NULL` として定義されます。 `PERIOD FOR SYSTEM_TIME` および `WITH SYSTEM_VERSIONING = ON` 引数と組み合わせてこの引数を使い、テーブル上でシステムのバージョン管理を有効にします。 詳細については、「 [Temporal Tables](../../relational-databases/tables/temporal-tables.md)」を参照してください。

1 つまたは両方の期間列を **HIDDEN** フラグでマークしてこれらの列を暗黙的に非表示にし、**SELECT \* FROM** _`<table>`_ がこれらの列の値を返さないようにすることができます。 既定では、期間列は非表示ではありません。 非表示の列を使用するためには、テンポラル テーブルを直接参照するすべてのクエリで明示的に含める必要があります。 変更する、 **HIDDEN** を既存の**期間**列の属性 期間 削除し、別の非表示フラグを再作成する必要があります。

INDEX *index_name* [ CLUSTERED | NONCLUSTERED ] (*column_name* [ ASC | DESC ] [ ,... *n* ] )     
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。

テーブル上にインデックスを作成することを指定します。 これには、クラスター化インデックスまたは非クラスター化インデックスを指定できます。 インデックスには一覧表示される列が含まれ、昇順、降順のいずれかでデータが並べ替えられます。

INDEX *index_name* CLUSTERED COLUMNSTORE     
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。

テーブル全体を、列形式で、クラスター化列ストア インデックスを使って格納することを指定します。 これには常に、テーブル内のすべての列が含まれます。 列ストア圧縮のベネフィットを得るように列が構成されるため、データはアルファベットや数値順に並べ替えられません。

INDEX *index_name* [ NONCLUSTERED ] COLUMNSTORE (*column_name* [ ,... *n* ] )     
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。

テーブル上に非クラスター化列ストア インデックスを作成することを指定します。 基になるテーブルには、行ストア ヒープまたはクラスター化インデックスを指定するか、クラスター化列ストア インデックスを指定することができます。 すべての場合で、テーブルに非クラスター化列ストア インデックスを作成すると、列のデータの 2 番目のコピーがインデックスに格納されます。

非クラスター化列ストア インデックスは、クラスター化列ストア インデックスとして格納および管理されます。 これも非クラスター化列ストア インデックスと呼ばれます。列を制限することができ、テーブル上のセカンダリ インデックスとして存在するためです。

ON _partition\_scheme\_name_ **(** _column\_name_ **)**     
ファイル グループが定義されているパーティション構成を指定します。このファイル グループは、パーティション インデックスのパーティションのマップ先となります。 [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) または [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md) を実行して、パーティション構成がデータベース内に存在するようにする必要があります。 *column_name* には、パーティション インデックスがパーティション分割される対象の列を指定します。 この列は、*partition_scheme_name* で使用されているパーティション関数の引数のデータ型、長さ、および有効桁数に一致する必要があります。 *column_name* インデックス定義内の列に限定されません。 UNIQUE インデックスをパーティション分割する場合、*column_name* は一意のキーとして使用されている列から選択する必要がありますが、それ以外の場合はベース テーブルの任意の列を指定できます。 この制限により、[!INCLUDE[ssDE](../../includes/ssde-md.md)]では、単一のパーティション内だけでキー値の一意性を確認できます。

> [!NOTE]
> 一意でないクラスター化インデックスをパーティション分割するとき、[!INCLUDE[ssDE](../../includes/ssde-md.md)]では既定により、まだ指定されていない場合、パーティション分割列がクラスター化インデックス キーのリストに追加されます。 一意でない非クラスター化インデックスをパーティション分割するとき、[!INCLUDE[ssDE](../../includes/ssde-md.md)]では、まだ指定されていない場合、パーティション分割列がインデックスの非キー列 (付加列) として追加されます。

*partition_scheme_name* または *filegroup* が指定されないまま、テーブルがパーティション分割されると、インデックスは基になるテーブルと同じパーティション分割列を使用して、同じパーティション構造に配置されます。

> [!NOTE]
> XML インデックスにはパーティション構成を指定できません。 ベース テーブルがパーティション分割される場合、XML インデックスではテーブルと同じパーティション構造が使用されます。

パーティション分割の詳細については、「[パーティション テーブルとパーティション インデックス](../../relational-databases/partitions/partitioned-tables-and-indexes.md)」を参照してください。

ON *filegroup_name*    
指定したファイル グループに、指定したインデックスを作成します。 位置の指定がなく、テーブルまたはビューがパーティション分割されていない場合、インデックスには、基になるテーブルまたはビューと同じファイル グループが使用されます。 ファイル グループは既に存在している必要があります。

ON **"default"**     
既定のファイル グループに、指定したインデックスを作成します。

このコンテキストでの default という用語はキーワードではありません。 これは、既定ファイル グループの識別子なので、ON **"default"** または ON **[default]** のように区切る必要があります。 "default" を指定する場合は、現在のセッションに対して `QUOTED_IDENTIFIER` オプションが ON である必要があります。 これが既定の設定です。 詳しくは、「[SET QUOTED_IDENTIFIER](../../t-sql/statements/set-quoted-identifier-transact-sql.md)」をご覧ください。

[ FILESTREAM_ON { *filestream_filegroup_name* | *partition_scheme_name* | "NULL" } ]     
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] 以降)。

クラスター化インデックスの作成時に、テーブルの FILESTREAM データの配置を指定します。 FILESTREAM_ON 句を使用すると、異なる FILESTREAM ファイル グループやパーティション構成に FILESTREAM データを移動できます。

*filestream_filegroup_name* FILESTREAM ファイル グループの名前を指定します。 ファイル グループには、[CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md) ステートメントまたは [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) ステートメントを使用してファイルが 1 つ定義されている必要があります。それ以外の場合は、エラーが発生します。

テーブルがパーティション分割されている場合、`FILESTREAM_ON` 句を使用して、テーブルのパーティション構成と同じパーティション関数とパーティション列を使用するように、FILESTREAM ファイル グループのパーティション構成を指定する必要があります。 それ以外の場合は、エラーが発生します。

テーブルがパーティション分割されていない場合、FILESTREAM 列をパーティション分割することはできません。 テーブルの FILESTREAM データは、`FILESTREAM_ON` 句で指定した単一のファイル グループに格納する必要があります。

クラスター化インデックスの作成で、テーブルに FILESTREAM 列が含まれていないときは、`CREATE INDEX` ステートメントに `FILESTREAM_ON NULL` を指定できます。

詳細については、[FILESTREAM](../../relational-databases/blob/filestream-sql-server.md) に関するページをご覧ください。

ROWGUIDCOL     
新しい列が行の GUID 列であることを示します。 1 つのテーブルにつき、1 つの **uniqueidentifier** 列だけを ROWGUIDCOL 列に指定できます。 ROWGUIDCOL プロパティを適用すると、`$ROWGUID` を使用して列を参照できるようになります。 ROWGUIDCOL プロパティは **uniqueidentifier** 列にだけ割り当てることができます。 ユーザー定義データ型の列に ROWGUIDCOL を指定することはできません。

ROWGUIDCOL プロパティは、列に格納されている値の一意性を設定しません。 また、ROWGUIDCOL プロパティは、テーブルに挿入される新しい行の値を自動的に生成しません。 各列に対して一意な値を生成するには、[INSERT](../../t-sql/statements/insert-transact-sql.md) ステートメントで [NEWID](../../t-sql/functions/newid-transact-sql.md) 関数または [NEWSEQUENTIALID](../../t-sql/functions/newsequentialid-transact-sql.md) 関数を使用するか、これらの関数を列の既定値として使用します。

ENCRYPTED WITH    
[Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 機能を使って暗号化列を指定します。

COLUMN_ENCRYPTION_KEY = *key_name*     
列の暗号化キーを指定します。 詳細については、[CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) に関するページをご覧ください。

ENCRYPTION_TYPE = { DETERMINISTIC | RANDOMIZED }     
**確定的な暗号化** は常に任意のプレーン テキストを指定した値の場合は、同じ暗号化された値を生成するメソッドを使用します。 決定論的な暗号化を使うことにより、等価比較を使った検索や、グループ化、暗号化された値に基づく等価結合を使ったテーブルの結合が可能になりますが、承認されていないユーザーが、暗号化された列のパターンを調べることで暗号化された値に関する情報を推測することも可能になります。 決定論的に暗号化された列で 2 つのテーブルを結合することができるのは、両方の列が同じ列暗号化キーを使って暗号化されている場合のみです。 明確な暗号化では、バイナリ 2 文字型の列の並べ替え順序を持つ列の照合順序を使用する必要があります。

**暗号化をランダム化** は低い予測可能な方法でデータを暗号化するためのメソッドを使用します。 ランダム化された暗号化は、より安全ですが、SQL Server インスタンスでセキュア エンクレーブを使用する Always Encrypted がサポートされる場合を除き、暗号化された列に対する計算とインデックス作成はすべて阻止されます。 詳しくは、「[Always Encrypted with secure enclaves](../../relational-databases/security/encryption/always-encrypted-enclaves.md)」(セキュア エンクレーブを使用する Always Encrypted) をご覧ください。

Always Encrypted (セキュア エンクレーブなし) を使用している場合、政府の ID 番号などのパラメーターまたはグループ化パラメーターで検索される列には、決定論的な暗号化を使用します。 ランダム化された暗号化は、他のレコードとグループ化されたりテーブルの結合に使用されたりせず、関心のある暗号化された列を含む行の検索に他の列 (トランザクション番号など) を使用するため検索されない、クレジット カード番号などのデータに使用します。

セキュア エンクレーブを使用する Always Encrypted を使用する場合は、ランダム化された暗号化が推奨される暗号化の種類です。

列は、該当するデータ型である必要があります。

ALGORITHM    
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降)。

**'AEAD_AES_256_CBC_HMAC_SHA_256'** を指定する必要があります。

機能の制約などについて詳しくは、[Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) に関するページをご覧ください。

SPARSE    
列がスパース列であることを示します。 スパース列のストレージは NULL 値用に最適化されます。 スパース列を NOT NULL として指定することはできません。 スパース列のその他の制限事項と詳細については、「[スパース列の使用](../../relational-databases/tables/use-sparse-columns.md)」を参照してください。

MASKED WITH ( FUNCTION = ' *mask_function* ')     
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降)。

動的なデータ マスクを指定します。 *mask_function* マスキング関数は、適切なパラメーターの名前を指定します。 次の 4 つの関数を使用できます。

- default()
- email()
- partial()
- random()

関数のパラメーターについては、「[動的なデータ マスキング](../../relational-databases/security/dynamic-data-masking.md)」を参照してください。

FILESTREAM     
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] 以降)。

**varbinary(max)** 列に対してのみ有効です。 **varbinary (max)** BLOB データの FILESTREAM ストレージを指定します。

また、ROWGUIDCOL 属性を持つ **uniqueidentifier** データ型の列がテーブルに存在する必要があります。 この列では、null 値を許可してはならず、また UNIQUE、PRIMARY KEY のいずれかの単一列制約を持つ必要があります。 列の GUID 値は、データの挿入時にアプリケーションによって、または NEWID () 関数を使用する DEFAULT 制約によって、提供する必要があります。

テーブルに FILESTREAM 列が定義されている間は、ROWGUIDCOL 列を削除したり、関連する制約を変更したりすることはできません。 ROWGUIDCOL 列は、最後の FILESTREAM 列を削除した後にのみ削除できます。

列に対して FILESTREAM ストレージ属性を指定した場合、この列のすべての値がファイル システム上の FILESTREAM データ コンテナーに格納されます。

COLLATE *collation_name*     
列の照合順序を指定します。 照合順序名には、Windows 照合順序名または SQL 照合順序名を指定できます。 *collation_name* は、**char**、**varchar**、**text**、**nchar**、**nvarchar**、および **ntext** データ型の列に対してのみ適用可能です。 指定しない場合、ユーザー定義データ型の列である場合は列にユーザー定義データ型の照合順序が割り当てられ、それ以外の場合はデータベースの既定の照合順序が割り当てられます。

Windows の照合順序名および SQL の照合順序名の詳細については、「[Windows 照合順序名 (Transact-SQL)](../../t-sql/statements/windows-collation-name-transact-sql.md)」および「[SQL 照合順序名 (Transact-SQL)](../../t-sql/statements/sql-server-collation-name-transact-sql.md)」を参照してください。

詳しくは、「[COLLATE](~/t-sql/statements/collations.md)」をご覧ください。

CONSTRAINT     
PRIMARY KEY 制約、NOT NULL 制約、UNIQUE 制約、FOREIGN KEY 制約、または CHECK 制約の定義の開始を示す省略可能なキーワードです。

*constraint_name*     
制約の名前です。 制約名は、テーブルが所属するスキーマ内で一意である必要があります。

NULL | NOT NULL     
列で NULL 値を許容するかどうかを示します。 NULL は厳密には制約ではありませんが、NOT NULL と同じように指定することができます。 計算列で NOT NULL を指定できるのは、PERSISTED も指定した場合のみです。

PRIMARY KEY    
一意なインデックスによって、指定した 1 つ以上の列にエンティティの整合性を設定する制約です。 PRIMARY KEY 制約は、1 つのテーブルにつき 1 つだけ作成できます。

UNIQUE     
一意なインデックスによって、指定した 1 つ以上の列にエンティティの整合性を提供する制約です。 1 つのテーブルには複数の UNIQUE 制約を指定できます。

CLUSTERED | NONCLUSTERED    
PRIMARY KEY または UNIQUE 制約に対して、クラスター化インデックスまたは非クラスター化インデックスを作成することを示します。 PRIMARY KEY 制約の既定値は CLUSTERED で、UNIQUE 制約の既定値は NONCLUSTERED です。

`CREATE TABLE` ステートメントでは、1 つの制約に対してのみ CLUSTERED を指定することができます。 UNIQUE 制約で CLUSTERED が指定され、PRIMARY KEY 制約も指定した場合には、PRIMARY KEY の既定値は NONCLUSTERED になります。

FOREIGN KEY REFERENCES       
1 つ以上の列内のデータに参照整合性を持たせる制約です。 FOREIGN KEY 制約では、列内の各値が、参照されるテーブル内の対応する参照される列 (1 つまたは複数) に存在している必要があります。 FOREIGN KEY 制約は、参照されるテーブル内の PRIMARY KEY 制約または UNIQUE 制約である列、または参照されるテーブルの UNIQUE INDEX で参照される列のみを参照できます。 計算列上の外部キーも、PERSISTED とマークする必要があります。

[ _schema\_name_ **.** ] *referenced_table_name*]      
FOREIGN KEY 制約で参照されるテーブル名と、そのテーブルが所属するスキーマ名です。

**(** *ref_column* [ **,** ... *n* ] **)** : FOREIGN KEY 制約によって参照されるテーブルの、列または列の一覧です。

ON DELETE { **NO ACTION** | CASCADE | SET NULL | SET DEFAULT }         
作成されたテーブルの行が参照関係を持ち、参照される行が親テーブルから削除された場合に、その行に対して実行される操作を指定します。 既定値は NO ACTION です。

NO ACTION      
[!INCLUDE[ssDE](../../includes/ssde-md.md)] がエラーを生成し、親テーブルでの行の削除操作がロールバックされます。

CASCADE    
親テーブルから行が削除された場合に、参照元テーブルからもその行が削除されます。

SET NULL     
親テーブル内の対応する行が削除されると、外部キーを構成するすべての値に NULL が設定されます。 この制約を実行するには、外部キー列が NULL 値を使用できる必要があります。

SET DEFAULT    
親テーブル内の対応する行が削除されると、外部キーを構成するすべての値に既定値が設定されます。 この制約を実行するには、すべての外部キー列に既定値が定義されている必要があります。 列が NULL 値を許容し、明示的な既定値が設定されていない場合は、列の既定値として NULL が暗黙的に使用されます。

論理レコードを使用するマージ パブリケーションにテーブルを含める場合、CASCADE は使用しないでください。 論理レコードの詳細については、「[論理レコードによる関連行への変更をグループ化](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)」を参照してください。

`INSTEAD OF` トリガーの `ON DELETE` が既にテーブルに存在する場合は、`ON DELETE CASCADE` を定義できません。

たとえば、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースで、**ProductVendor** テーブルに **Vendor** テーブルとの参照関係があるとします。 ここで、**ProductVendor.BusinessEntityID** 外部キーは **Vendor.BusinessEntityID** 主キーを参照します。

`DELETE` ステートメントを **Vendor** テーブルの行で実行した場合、`ON DELETE CASCADE` アクションが **ProductVendor.BusinessEntityID** に対して指定されていると、[!INCLUDE[ssDE](../../includes/ssde-md.md)] では **ProductVendor** テーブルに 1 つ以上の従属行があるかどうかが確認されます。 従属行がある場合、**ProductVendor** テーブルの従属行が、**Vendor** テーブルで参照される行と共に削除されます。

これに対し、`NO ACTION` が指定されている場合、**ProductVendor** テーブルに **Vendor** テーブルの行を参照する行が 1 つでもあると、[!INCLUDE[ssDE](../../includes/ssde-md.md)] でエラーが発生し、Vendor 行の削除操作をロールバックします。

ON UPDATE { **NO ACTION** | CASCADE | SET NULL | SET DEFAULT }     
変更対象のテーブル内の行が参照関係を持ち、親テーブルで参照先の行が更新された場合、変更対象のテーブル内の行に対して発生する操作を指定します。 既定値は NO ACTION です。

NO ACTION    
NO ACTION を指定すると、[!INCLUDE[ssDE](../../includes/ssde-md.md)]でエラーが発生し、親テーブルの行の更新操作はロールバックされます。

CASCADE      
親テーブルで行が更新された場合に、参照元のテーブルでも対応する行が更新されます。

SET NULL     
親テーブルの対応する行が更新された場合、外部キーを形成するすべての値が NULL に設定されます。 この制約を実行するには、外部キー列が NULL 値を使用できる必要があります。

SET DEFAULT     
親テーブルの対応する行が更新された場合、外部キーを形成するすべての値が既定値に設定されます。 この制約を実行するには、すべての外部キー列に既定値が定義されている必要があります。 列が NULL 値を許容し、明示的な既定値が設定されていない場合は、列の既定値として NULL が暗黙的に使用されます。

論理レコードを使用するマージ パブリケーションにテーブルを含める場合、`CASCADE` は使用しないでください。 論理レコードの詳細については、「[論理レコードによる関連行への変更をグループ化](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)」を参照してください。

`INSTEAD OF` トリガーの `ON UPDATE` が変更するテーブルに既に存在する場合は、`ON UPDATE CASCADE`、`SET NULL`、または `SET DEFAULT` を定義できません。

たとえば、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースで、**ProductVendor** テーブルに **Vendor** テーブルとの参照関係があるとします。**ProductVendor.BusinessEntity** 外部キーは **Vendor.BusinessEntityID** 主キーを参照します。

UPDATE ステートメントを **Vendor** テーブルの行で実行した場合、ON UPDATE CASCADE アクションが **ProductVendor.BusinessEntityID** に対して指定されていると、[!INCLUDE[ssDE](../../includes/ssde-md.md)]では **ProductVendor** テーブルに 1 つ以上の従属行があるかどうかが確認されます。 従属行がある場合、**ProductVendor** テーブルの従属行が、**Vendor** テーブルで参照される行と共に更新されます。

これに対し、NO ACTION が指定されている場合、**ProductVendor** テーブルに **Vendor** テーブルの行を参照する行が 1 つでもあると、[!INCLUDE[ssDE](../../includes/ssde-md.md)]でエラーが発生し、Vendor 行の更新操作をロールバックします。

CHECK     
1 つ以上の列に入力できる値を制限することによってドメインの整合性を設定する制約です。 計算列の CHECK 制約も、PERSISTED とマークする必要があります。

*logical_expression*     
TRUE または FALSE を返す論理式です。 別名データ型を式に含めることはできません。

*column*     
テーブル制約で使われる、かっこで囲まれた 1 つの列または列リストです。制約定義で使われている列を示します。

[ **ASC** | DESC ]     
テーブル制約に参加している 1 つ以上の列が並べ替えられる順序を指定します。 既定値は ASC です。

*partition_scheme_name*     
パーティション テーブルの各パーティションがマップされるファイル グループを定義するパーティション構成の名前です。 パーティション構成はデータベース内に存在している必要があります。

[ _partition\_column\_name_ **.** ]      
パーティション テーブルに対して、パーティション分割する列を指定します。 ここで指定する列は、*partition_scheme_name* が使用しているパーティション関数で指定した列と、データ型、長さ、有効桁数が同じであることが必要です。 パーティション関数に関与する計算列は、明示的に PERSISTED とマークされている必要があります。

> [!IMPORTANT]
> パーティション テーブルに加え、ALTER TABLE...SWITCH 操作のソースまたはターゲットとなっているパーティション分割されていないテーブルのパーティション分割列にも、NOT NULL を指定することをお勧めします。 こうすることで、パーティション分割列上のすべての CHECK 制約で null 値のチェックを行う必要がなくなります。

WITH FILLFACTOR **=** _fillfactor_     
インデックス データの格納に使用される個々のインデックス ページを[!INCLUDE[ssDE](../../includes/ssde-md.md)]がどの程度埋めるかを指定します。 ユーザーが指定できる *fillfactor* の値は、1 ～ 100 です。 値を指定しない場合の既定値は 0 です。 FILL FACTOR 値 0 と 100 の機能は、まったく同じです。

> [!IMPORTANT]
> マニュアルには、WITH FILLFACTOR = *fillfactor* が PRIMARY KEY 制約または UNIQUE 制約に適用される唯一のインデックス オプションとして記述されていますが、これは旧バージョンとの互換性を維持するために記載されており、将来のリリースではこのような記述はなくなります。

*column_set_name* XML COLUMN_SET FOR ALL_SPARSE_COLUMNS     
列セットの名前です。 列セットは、型指定されていない XML 表記であり、テーブルのすべてのスパース列を 1 つにまとめて構造化した出力です。 列セットの詳細については、「 [列セットの使用](../../relational-databases/tables/use-column-sets.md)」を参照してください。

PERIOD FOR SYSTEM_TIME (*system_start_time_column_name* , *system_end_time_column_name* )        
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。

レコードの有効期間を記録するためにシステムで使われる列の名前を指定します。 GENERATED ALWAYS AS ROW { START | END } および WITH SYSTEM_VERSIONING = ON 引数と組み合わせてこの引数を使い、テーブル上でシステムのバージョン管理を有効にします。 詳細については、「 [Temporal Tables](../../relational-databases/tables/temporal-tables.md)」を参照してください。

COMPRESSION_DELAY     
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。

メモリ最適化のために、行が変更されないままテーブル内に留まる必要のある最小時間 (分) を遅延によって指定します。その後、それは列ストア インデックスへの圧縮対象となります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、圧縮する特定の行がその最終更新時刻に従って選択されます。 たとえば、行が 2 時間の期間に頻繁に変更されている場合は、SQL Server が行を圧縮する前に更新が確実に完了するように `COMPRESSION_DELAY = 120 Minutes` に設定できます。

ディスク ベースのテーブルの場合は、CLOSED 状態のデルタ行グループがそのデルタ行グループに留まる必要がある最低限の分数が遅延によって指定され、その時間が経過すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は行グループを、圧縮された行グループに圧縮できるようになります。 ディスク ベース テーブルでは個々の行において挿入時間と更新時間が追跡されないため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は CLOSED 状態のデルタ行グループに遅延を適用します。

既定値は、0 分です。

`COMPRESSION_DELAY` を使用する場合の推奨事項については、「[列ストアを使用したリアルタイム運用分析の概要](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)」を参照してください

\< table_option> ::=    
1 つ以上のテーブル オプションを指定します。

DATA_COMPRESSION     
指定したテーブル、パーティション番号、またはパーティション範囲に、データ圧縮オプションを指定します。 次のオプションがあります。

NONE     
テーブルまたは指定したパーティションが圧縮されません。

ROW    
行の圧縮を使用して、テーブルまたは指定したパーティションが圧縮されます。

PAGE     
ページの圧縮を使用して、テーブルまたは指定したパーティションが圧縮されます。

COLUMNSTORE    

**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。

非クラスター化列ストアとクラスター化列ストア インデックスの両方を含む列ストア インデックスにのみ適用されます。 COLUMNSTORE では、最も高パフォーマンスの列ストア圧縮で圧縮することを指定します。 これは、一般的な選択です。

COLUMNSTORE_ARCHIVE     
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。

非クラスター化列ストアとクラスター化列ストア インデックスの両方を含む列ストア インデックスにのみ適用されます。 COLUMNSTORE_ARCHIVE では、テーブルまたはパーティションをより小さなサイズにさらに圧縮します。 これは、アーカイブ用や、ストレージのサイズを減らす必要があり、かつ保存と取得に時間をかける余裕があるその他の状況で使用できます。

詳細については、「 [Data Compression](../../relational-databases/data-compression/data-compression.md)」を参照してください。

ON PARTITIONS **(** { `<partition_number_expression>` | [ **,** ...*n* ] **)**       
DATA_COMPRESSION 設定を適用するパーティションを指定します。 テーブルがパーティション分割されていない場合に `ON PARTITIONS` 引数を使用すると、エラーが発生します。 `ON PARTITIONS` 句を指定しないと、パーティション テーブルのすべてのパーティションに対して `DATA_COMPRESSION` オプションが適用されます。

*partition_number_expression* は以下の方法で指定できます。

- 1 つのパーティションのパーティション番号を提供します。たとえば、`ON PARTITIONS (2)` のようになります。
- コンマで区切った複数の個別のパーティションのパーティション番号を提供します。たとえば次のとおりです: `ON PARTITIONS (1, 5)`
- 範囲と個別のパーティションの両方を提供します。たとえば次のとおりです: `ON PARTITIONS (2, 4, 6 TO 8)`

`<range>` はパーティション番号として、TO で区切って指定できます。たとえば、`ON PARTITIONS (6 TO 8)` のようになります。

さまざまなパーティションにさまざまな種類のデータ圧縮を設定するには、`DATA_COMPRESSION` オプションを複数回指定します。例:

```sql
WITH
(
    DATA_COMPRESSION = NONE ON PARTITIONS (1),
    DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),
    DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)
)
```

\<index_option> ::=      
1 つ以上のインデックス オプションを指定します。 これらのオプションの詳細な説明については、[CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) に関するページをご覧ください。

PAD_INDEX = { ON | **OFF** }     
ON の場合、FILLFACTOR で指定された空き領域の割合が、インデックスの中間レベル ページに適用されます。 OFF の場合や、FILLFACTOR 値を指定しない場合、中間レベル ページは、中間ページの一連のキーを考慮しつつ、インデックスが持つことのできる最大サイズの行を少なくとも 1 つ格納できる領域を残して、ほぼ容量いっぱいに使用されます。 既定値は OFF です。

FILLFACTOR **=** _fillfactor_     
インデックスの作成時または変更時に、[!INCLUDE[ssDE](../../includes/ssde-md.md)] が各インデックス ページのリーフ レベルをどの程度まで埋めるかを、パーセント値で指定します。 *fillfactor* 値には、1 ～ 100 の整数値を指定してください。 既定値は 0 です。 FILL FACTOR 値 0 と 100 の機能は、まったく同じです。

IGNORE_DUP_KEY = { ON | **OFF** }    
挿入操作で、一意のインデックスに重複するキー値を挿入しようとした場合のエラー応答を指定します。 IGNORE_DUP_KEY オプションは、インデックスが作成または再構築された後の挿入操作のみに適用されます。 [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)、[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)、または [UPDATE](../../t-sql/queries/update-transact-sql.md) を実行した場合、このオプションは無効です。 既定値は OFF です。

ON    
重複したキー値が一意のインデックスに挿入されると、警告メッセージが表示されます。 一意性制約に違反する行のみが失敗します。

OFF    
重複したキー値が一意のインデックスに挿入されると、エラー メッセージが表示されます。 INSERT 操作全体がロールバックされます。

ビューに作成されたインデックス、一意でないインデックス、XML インデックス、空間インデックス、およびフィルター処理されたインデックスについては、`IGNORE_DUP_KEY` を ON に設定することはできません。

`IGNORE_DUP_KEY` を表示するには、[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) を使用します。

下位互換性のある構文では、`WITH IGNORE_DUP_KEY` は `WITH IGNORE_DUP_KEY = ON` と等価です。

STATISTICS_NORECOMPUTE **=** { ON | **OFF** }     
ON の場合、古いインデックス統計値は自動的には再計算されません。 OFF の場合、統計値の自動的な更新が有効になります。 既定値は OFF です。

ALLOW_ROW_LOCKS **=** { **ON** | OFF }      
ON の場合、インデックスにアクセスするときに行ロックが許可されます。 いつ行ロックを使用するかは、[!INCLUDE[ssDE](../../includes/ssde-md.md)]によって決定されます。 OFF の場合、行のロックは使用されません。 既定値は ON です。

ALLOW_PAGE_LOCKS **=** { **ON** | OFF }       
ON の場合、インデックスにアクセスするときにページ ロックが許可されます。 いつページ ロックを使用するかは、[!INCLUDE[ssDE](../../includes/ssde-md.md)] によって決定されます。 OFF の場合、ページ ロックは使用されません。 既定値は ON です。

OPTIMIZE_FOR_SEQUENTIAL_KEY = { ON | **OFF** } **適用対象**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降。 <BR>
最終ページ挿入競合に対して最適化するかどうかを指定します。 既定値は OFF です。 詳細については、CREATE INDEX のページの「[シーケンシャル キー](./create-index-transact-sql.md#sequential-keys)」セクションを参照してください。

FILETABLE_DIRECTORY = *directory_name*      

**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降)。

Windows と互換性のある FileTable ディレクトリ名を指定します。 この名前は、データベース内のすべての FileTable ディレクトリ名の中で一意である必要があります。 一意性の比較では、照合順序の設定とは関係なく、大文字と小文字は区別されません。 この値を指定しない場合、FileTable の名前が使用されます。

FILETABLE_COLLATE_FILENAME = { *collation_name* | database_default }

**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降)。 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、`FILETABLE` はサポートされていません。

FileTable の **Name** 列に適用される照合順序の名前を指定します。 照合順序は、Windows のファイル名のセマンティクスに準拠するために、大文字と小文字を区別しない設定にする必要があります。 この値が指定されていない場合、データベースの既定の照合順序が使用されます。 データベースの既定の照合順序で大文字と小文字が区別される場合は、エラーが発生し、CREATE TABLE 操作は失敗します。

*collation_name*     
大文字と小文字を区別しない照合順序の名前です。

database_default        
データベースの既定の照合順序を使用するように指定します。 この照合順序は、大文字と小文字を区別しないものである必要があります。

FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME = *constraint_name*          
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降)。

FileTable に対して自動的に作成される主キー制約で使用する名前を指定します。 この値を指定しない場合、システムによって制約の名前が生成されます。

FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME = *constraint_name*        
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降)。

FileTable の **stream_id** 列に対して自動的に作成される一意制約で使用する名前を指定します。 この値を指定しない場合、システムによって制約の名前が生成されます。

FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME = *constraint_name*       
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降)。

FileTable の **parent_path_locator** 列と **name** 列に対して自動的に作成される一意制約で使用する名前を指定します。 この値を指定しない場合、システムによって制約の名前が生成されます。

SYSTEM_VERSIONING **=** ON [ ( HISTORY_TABLE **=** *schema_name* .*history_table_name* [, DATA_CONSISTENCY_CHECK **=** { **ON** | OFF } ] ) ]         
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)])。

データ型、NULL 値の許容制約、および主キー制約の要件が満たされている場合は、テーブルのシステムのバージョン管理を有効にします。 `HISTORY_TABLE` 引数を使用しない場合、システムは現在のテーブルと同じファイル グループ内の現在のテーブルのスキーマに一致する新しい履歴テーブルを生成し、これによって 2 つのテーブルの間にリンクが作成され、履歴テーブルに現在のテーブル内の各レコードの履歴が記録されるようになります。 この履歴テーブルの名前は `MSSQL_TemporalHistoryFor<primary_table_object_id>` になります。 履歴テーブルには既定では、 **PAGE** 圧縮します。 `HISTORY_TABLE` 引数を使ってリンクを作成し、既存の履歴テーブルを使用する場合、現在のテーブルと指定したテーブルの間のリンクが作成されます。 現在のテーブルがパーティション分割する場合、履歴テーブルは、パーティション分割構成がレプリケートされていないために自動的に現在のテーブルから履歴テーブルに既定のファイル グループに作成されます。 履歴テーブルの作成時に履歴テーブルの名前を指定すると場合、は、スキーマとテーブルの名前を指定する必要があります。 既存の履歴テーブルへのリンクを作成する場合は、データの整合性チェックを実行することもできます。 このデータの整合性チェックでは、既存のレコードが重複しないことを確認します。 データを実行する一貫性チェックが、既定値です。 `PERIOD FOR SYSTEM_TIME` および `GENERATED ALWAYS AS ROW { START | END }` 引数と組み合わせてこの引数を使い、テーブル上でシステムのバージョン管理を有効にします。 詳細については、「 [Temporal Tables](../../relational-databases/tables/temporal-tables.md)」を参照してください。

REMOTE_DATA_ARCHIVE = { ON [ ( *table_stretch_options* [,...n] ) ] | OFF ( MIGRATION_STATE = PAUSED ) }          
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降)。

Stretch Database が有効または無効になっている新しいテーブルを作成します。 詳細については、「 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)」を参照してください。

**テーブルに対して Stretch Database を有効にする**

`ON` を指定してテーブルに対して Stretch を有効にする場合は、必要に応じて、`MIGRATION_STATE = OUTBOUND` を指定してデータの移行をすぐに開始するか、`MIGRATION_STATE = PAUSED` を指定してデータの移行を延期することができます。 既定値は `MIGRATION_STATE = OUTBOUND` です。 テーブルに対して Stretch を有効にする方法については、「[データベースに対して Stretch Database を有効にする](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)」を参照してください。

**前提条件**。 テーブルに対して Stretch を有効にする前に、サーバーおよびデータベースで Stretch を有効にする必要があります。 詳細については、「 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)」を参照してください。

**権限**: データベースまたはテーブルの Stretch を有効にするには、db_owner アクセス許可が必要です。 テーブルの Stretch を有効にする場合、テーブルに対する ALTER 権限も必要です。

[ FILTER_PREDICATE = { null | *predicate* } ]       
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降)。

必要に応じて、履歴データと現在のデータの両方を含むテーブルから移行する行を選択するフィルター述語を指定します。 この述語で決定論的インライン テーブル値関数を呼び出す必要があります。 詳しくは、「[Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)」および「[フィルター関数を使用して移行する行を選択する](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)」をご覧ください。

> [!IMPORTANT]
> 指定したフィルター述語のパフォーマンスが低いと、データ移行のパフォーマンスも低くなります。 Stretch Database では、CROSS APPLY 演算子を使用してテーブルにフィルター述語を適用します。

フィルター述語を指定しない場合、テーブル全体が移行されます。

フィルター述語を指定する場合は、*MIGRATION_STATE* も指定する必要があります。

MIGRATION_STATE = { OUTBOUND | INBOUND | PAUSED }         
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。

-  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] にデータを移行するには `OUTBOUND` を指定します。
-  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にテーブルのリモート データをコピーして戻し、テーブルに対する Stretch を無効にするには、`INBOUND` を指定します。 詳細については、「 [Stretch Database を無効にして、リモート データを戻す](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md)」を参照してください。

   この操作によりデータ転送コストが発生し、取り消すことはできません。

-  データの移行を一時停止または延期するには `PAUSED` を指定します。 詳細については、[データ移行の一時停止と再開 - Stretch Database](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md) に関するページをご覧ください。

MEMORY_OPTIMIZED       
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)])。 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] マネージド インスタンスでは、メモリ最適化テーブルはサポートされません。

値が ON の場合は、テーブルがメモリ最適化されていることを示します。 メモリ最適化テーブルは、トランザクション処理のパフォーマンスの最適化に使用されるインメモリ OLTP 機能の一部です。 インメモリ OLTP の使用を開始する方法については、「[クイック スタート 1:Transact-SQL のパフォーマンスを向上させるインメモリ OLTP テクノロジ](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)」を参照してください。 メモリ最適化テーブルについて詳しくは、「[メモリ最適化テーブル](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)」をご覧ください。

既定値の OFF は、テーブルがディスク ベースであることを示します。

DURABILITY        
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。

値 `SCHEMA_AND_DATA` は、テーブルに持続性があり、変更がディスクに保存され、再起動またはフェールオーバー後も存続することを示します。 SCHEMA_AND_DATA が既定値です。

値 `SCHEMA_ONLY` は、テーブルに持続性がないことを示します。 データベースを再起動またはフェールオーバーした場合、テーブル スキーマは保存されますが、データの更新内容は保存されません。 `DURABILITY = SCHEMA_ONLY` は `MEMORY_OPTIMIZED = ON` でのみ使用することができます。

> [!WARNING]
> **DURABILITY = SCHEMA_ONLY** でテーブルが作成される場合、**READ_COMMITTED_SNAPSHOT** がその後 **ALTER DATABASE** を使用して変更されると、テーブル内のデータは失われます。

BUCKET_COUNT       
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)])。

ハッシュ インデックスに作成されるバケットの数を示します。 ハッシュ インデックスの BUCKET_COUNT の最大値は 1,073,741,824 です。 バケット数について詳しくは、「[メモリ最適化テーブルのインデックス](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)」をご覧ください。

BUCKET_COUNT は必須の引数です。

**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。

列インデックスとテーブル インデックスは、CREATE TABLE ステートメントの一部として指定できます。 メモリ最適化テーブルのインデックスの追加と削除の詳細については、次のページを参照してください。[メモリ最適化テーブルの変更](../../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md)

HASH      
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。

ハッシュ インデックスを作成することを示します。

ハッシュ インデックスは、メモリ最適化テーブルでのみサポートされます。

## <a name="remarks"></a>Remarks

許容されるテーブル、列、制約、およびインデックスの数については、「[SQL Server の最大容量仕様](../../sql-server/maximum-capacity-specifications-for-sql-server.md)」を参照してください。

一般的にテーブルとインデックスには、一度に 1 エクステントの増分で領域が割り当てられます。 `ALTER DATABASE` の `SET MIXED_PAGE_ALLOCATION` オプションが TRUE に設定されている場合、または常に [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] より前である場合は、テーブルまたはインデックスの作成時に、ページが単一エクステントを埋めるのに十分な量になるまで混合エクステントからページが割り当てられます。 ページが単一エクステントを埋めるのに十分な量になった後は、現在割り当てられているエクステントが埋まるたびに新しいエクステントが割り当てられます。 テーブルに割り当てられて使用されている領域の大きさに関するレポートを表示するには、`sp_spaceused` を実行します。

[!INCLUDE[ssDE](../../includes/ssde-md.md)]では、列定義の中で、DEFAULT、IDENTITY、ROWGUIDCOL または列制約を指定する順序は設定されていません。

テーブルを作成するときに、QUOTED IDENTIFIER オプションが OFF に設定されている場合でも、ON としてテーブルのメタデータ内に格納されます。

## <a name="temporary-tables"></a>一時テーブル
ローカルおよびグローバル一時テーブルを作成できます。 ローカル一時テーブルは現在のセッション内でしか使えず、グローバル一時テーブルはすべてのセッションで使えます。 一時テーブルをパーティション分割することはできません。

ローカル一時テーブル名の前には 1 つの番号記号 (#) を付加し (#*table_name*)、グローバル一時テーブル名の前には 2 つの番号記号を付加します (##*table_name*)。

[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは、`CREATE TABLE` ステートメントの *table_name* に指定された値を使用して、一時テーブルを参照します。以下に例を示します。

```sql
CREATE TABLE #MyTempTable (
    col1 INT PRIMARY KEY
);

INSERT INTO #MyTempTable
VALUES (1);
```

1 つのストアド プロシージャまたはバッチ内で複数の一時テーブルを作成する場合は、それぞれ違う名前で作成する必要があります。

一時テーブルを作成またはアクセスするときに *schema_name* を含めると、無視されます。 すべての一時テーブルは、dbo スキーマで作成されます。

ローカル一時テーブルが、複数ユーザーが同時に実行できるストアド プロシージャまたはアプリケーションで作成される場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)]は、異なるユーザーが作成する個々のテーブルを区別できなければなりません。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]は、各ローカル一時テーブル名の末尾に数値サフィックスを内部的に追加することによって、テーブルを区別します。 **tempdb** の **sysobjects** テーブルに格納される一時テーブルのフル ネームは、CREATE TABLE ステートメントで指定されたテーブル名とシステムが生成する数値サフィックスから構成されます。 サフィックスを許可する *table_name* 指定は、ローカルの一時テーブル名は、116 文字を超えることはできません。

一時テーブルは、DROP TABLE を使用して明示的に削除される場合を除き、有効範囲外になったときに自動的に削除されます。

- ストアド プロシージャで作成されたローカル一時テーブルは、ストアド プロシージャが終了すると自動的に削除されます。 テーブルは、そのテーブルを作成したストアド プロシージャによって実行される任意の入れ子になったストアド プロシージャから参照できます。 テーブルを作成したストアド プロシージャの呼び出し元のプロセスから、そのテーブルを参照することはできません。
- その他すべてのローカル一時テーブルは、現在のセッションの終了時に自動的に削除されます。
- グローバル一時テーブルは、テーブルを作成したセッションが終了し、その他すべてのタスクがその参照をやめたときに、自動的に削除されます。 タスクとテーブルの間の関連付けは、1 つの [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが存続する間のみ維持されます。 したがって、グローバル一時テーブルは、テーブルを作成したセッションが終了したときに、テーブルを能動的に参照していた最後の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが完了したときに削除されます。

ストアド プロシージャまたはトリガーの内部で作成されたローカル一時テーブルは、ストアド プロシージャまたはトリガーが呼び出される前に作成された一時テーブルと同じ名前にすることができます。 ただし、クエリが一時テーブルを参照し、かつ同じ名前の一時テーブルが同時に 2 つ存在する場合、クエリがどちらのテーブルに対して解決されるかは定義されません。 入れ子になったストアド プロシージャも、そのプロシージャを呼び出したストアド プロシージャによって作成された一時テーブルと同じ名前を持つ一時テーブルを作成することができます。 ただし、入れ子になったプロシージャで作成したテーブルへの解決を変更するためには、呼び出し元プロシージャで作成されたテーブルと同じ構造、同じ列名である必要があります。 次の例を参照してください。

```sql
CREATE PROCEDURE dbo.Test2
AS
    CREATE TABLE #t (x INT PRIMARY KEY);
    INSERT INTO #t VALUES (2);
    SELECT Test2Col = x FROM #t;
GO

CREATE PROCEDURE dbo.Test1
AS
    CREATE TABLE #t (x INT PRIMARY KEY);
    INSERT INTO #t VALUES (1);
    SELECT Test1Col = x FROM #t;
    EXEC Test2;
GO

CREATE TABLE #t(x INT PRIMARY KEY);
INSERT INTO #t VALUES (99);
GO

EXEC Test1;
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
(1 row(s) affected)
Test1Col
-----------
1

(1 row(s) affected)
 Test2Col
 -----------
 2
 ```

ローカルまたはグローバル一時テーブルを作成する場合、`CREATE TABLE` 構文では、FOREIGN KEY 制約を除く制約定義がサポートされています。 一時テーブルで FOREIGN KEY 制約が指定されていると、ステートメントは、制約が省略されたことを示す警告メッセージを返します。 テーブルは FOREIGN KEY 制約なしのままで作成されます。 FOREIGN KEY 制約の中で一時テーブルを参照することはできません。

名前付き制約のある一時テーブルがユーザー定義トランザクションのスコープ内で作成される場合、一時テーブルを作成するステートメントを実行できるのは、一度に 1 ユーザーだけです。 たとえば、ストアド プロシージャで名前付き主キー制約のある一時テーブルが作成される場合、そのストアド プロシージャを複数のユーザーが同時に実行することはできません。

## <a name="database-scoped-global-temporary-tables-azure-sql-database"></a>データベース スコープ グローバル一時テーブル (Azure SQL Database)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のグローバル一時テーブル (テーブル名が ## で始まる) は、tempdb に格納され、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス全体のすべてのユーザーのセッション間で共有されます。 SQL テーブル型については、前述のテーブルの作成に関するセクションをご覧ください。

[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] は、tempdb にも保存されてスコープがデータベース レベルに設定されるグローバル一時テーブルをサポートしています。 これは、グローバル一時テーブルが同じ [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 内ですべてのユーザーのセッションで共有されることを意味します。 他のデータベースからのユーザー セッションは、グローバル一時テーブルにアクセスできません。

[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] のグローバル一時テーブルは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が一時テーブルに使用するのと同じ構文およびセマンティクスに従います。 同様に、グローバル一時ストアド プロシージャも、スコープが [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 内のデータベース レベルに設定されます。 ローカル一時テーブル (テーブル名が # で始まる) も [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] でサポートされ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用されるのと同じ構文およびセマンティクスに従います。 [一時テーブル](#temporary-tables)に関する上のセクションをご覧ください。  

> [!IMPORTANT]
> この機能は、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] で使用できます。

### <a name="troubleshooting-global-temporary-tables-for-azure-sql-database"></a>Azure SQL Database のグローバル一時テーブルのトラブルシューティング
tempdb のトラブルシューティングについては、「[tempdb の使用状況を監視する方法](../../relational-databases/databases/tempdb-database.md#how-to-monitor-tempdb-use)」を参照してください。

> [!NOTE]
> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] の DMV のトラブルシューティングにアクセスできるのは、サーバー管理者のみです。

### <a name="permissions"></a>アクセス許可
すべてのユーザーがグローバル一時オブジェクトを作成できます。 ユーザーは追加の権限を付与されない限り、自分で作成したオブジェクトにしかアクセスできません。

## <a name="partitioned-tables"></a>パーティション テーブル
CREATE TABLE を使用してパーティション テーブルを作成するには、まず、テーブルをパーティション分割する方法を指定するパーティション関数を作成する必要があります。 パーティション関数は、[CREATE PARTITION FUNCTION](../../t-sql/statements/create-partition-function-transact-sql.md) を使用して作成します。 次に、パーティション構成を作成する必要があります。パーティション構成では、パーティション関数が示すパーティションを保持するファイル グループを指定します。 パーティション構成は、[CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) を使用して作成します。 パーティション テーブルでは、PRIMARY KEY 制約または UNIQUE 制約を別のファイル グループに配置するよう指定できません。 詳細については、「 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)」を参照してください。

## <a name="primary-key-constraints"></a>PRIMARY KEY 制約
- テーブルに含めることができる PRIMARY KEY 制約は 1 つだけです。
- PRIMARY KEY 制約によって生成されたインデックスが含まれていても、テーブル上のインデックスの数を、非クラスター化インデックス 999 個、クラスター化インデックス 1 個より多くすることはできません。
- PRIMARY KEY 制約に対して CLUSTERED または NONCLUSTERED が指定されていない場合、UNIQUE 制約に対してクラスター化インデックスが指定されていない場合は CLUSTERED が使用されます。
- PRIMARY KEY 制約中で定義する列はすべて、NOT NULL として定義する必要があります。 NULL 値を許容するかどうかを指定しない場合、PRIMARY KEY 制約の影響を受けるすべての列は NOT NULL に設定されます。

    > [!NOTE]
    > メモリ最適化テーブルでは、null 許容型キー列が許可されます。

- CLR ユーザー定義型の列に対して主キーを定義する場合は、型の実装でバイナリ順がサポートされている必要があります。 詳細については、「 [CLR ユーザー定義型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)」を参照してください。

## <a name="unique-constraints"></a>UNIQUE 制約
- UNIQUE 制約に対して CLUSTERED または NONCLUSTERED が指定されていない場合は、特に指定がない限り、NONCLUSTERED が使用されます。
- 個々の UNIQUE 制約はインデックスを生成します。 UNIQUE 制約の数が原因で、テーブル上のインデックスの数が、非クラスター化インデックス 999 個、クラスター化インデックス 1 個を超えることはありません。
- CLR ユーザー定義型の列に対して一意の制約を定義する場合は、型の実装でバイナリまたは演算子ベースの順序をサポートする必要があります。 詳細については、「 [CLR ユーザー定義型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)」を参照してください。

## <a name="foreign-key-constraints"></a>FOREIGN KEY 制約
- FOREIGN KEY 制約の列に NULL 以外の値を入力するときは、その値が参照される列に存在している必要があります。存在していないと外部キー違反のエラー メッセージが返されます。
- FOREIGN KEY 制約は、変換元列が指定されている場合を除き、前の列に適用されます。
- FOREIGN KEY 制約は、同じサーバー上の同じデータベース内のテーブルのみを参照できます。 複数のデータベースにまたがる参照整合性は、トリガーを使って実装する必要があります。 詳細については、[CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md) に関するページをご覧ください。
- FOREIGN KEY 制約は、同じテーブル内の他の列を参照できます。 これは、自己参照と呼ばれます。
- 列レベルの FOREIGN KEY 制約の REFERENCES 句は、参照列を 1 つだけ表示できます。 この参照列は、制約が定義されている列と同じデータ型である必要があります。
- テーブルレベルの FOREIGN KEY 制約の REFERENCES 句は、制約列リスト内の列の数と同じ数の参照列を持っている必要があります。 また、各参照列のデータ型は、列リスト内の、参照列に対応する列と同じでなければなりません。
- **timestamp** 型の列が外部キーまたは参照されるキーの一部である場合、CASCADE、SET NULL、または SET DEFAULT を指定することはできません。
- CASCADE、SET NULL、SET DEFAULT および NO ACTION は、互いに参照関係にあるテーブルに対して組み合わせて使用することができます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] が NO ACTION を検出すると、関連する CASCADE、SET NULL および SET DEFAULT 操作が停止されロールバックされます。 DELETE ステートメントの実行によって、CASCADE、SET NULL、SET DEFAULT および NO ACTION 操作の組み合わせが適用される場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] が NO ACTION があるかどうかを調べる前にすべての CASCADE、SET NULL および SET DEFAULT 操作が適用されます。
- [!INCLUDE[ssDE](../../includes/ssde-md.md)] には、他のテーブルを参照するテーブルに含めることができる FOREIGN KEY 制約の数についても、特定のテーブルを参照する他のテーブルが持つ FOREIGN KEY 制約の数についても、事前定義済みの制限はありません。

  ただし、使用できる FOREIGN KEY 制約の実際の数は、ハードウェア構成やデータベースおよびアプリケーションのデザインにより制限されます。 1 つのテーブルに含める FOREIGN KEY 制約は 253 個までとし、253 個以内の FOREIGN KEY 制約から参照することをお勧めします。 効率的な制限は、アプリケーションとハードウェアにある程度依存します。 ご自分のデータベースやアプリケーションを設計するときは、FOREIGN KEY 制約を適用することのコストを検討します。

- FOREIGN KEY 制約は一時テーブルには設定されません。
- FOREIGN KEY 制約は、参照されているテーブルの PRIMARY KEY 制約または UNIQUE 制約の中の列だけを参照できます。
- CLR ユーザー定義型の列に対して外部キーを定義する場合は、型の実装でバイナリ順がサポートされている必要があります。 詳細については、「 [CLR ユーザー定義型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)」を参照してください。
- 外部キー リレーションシップに参加する列は、同じ長さと小数点以下桁数で定義する必要があります。

## <a name="default-definitions"></a>DEFAULT 定義
- 1 つの列は DEFAULT 定義を 1 つだけ持つことができます。
- DEFAULT 定義には、定数値、関数、SQL 標準ニラディック関数、または NULL を含めることができます。 次の表は、ニラディック関数と、それらが INSERT ステートメントの実行中に既定値として返す値を示しています。

    |SQL-92 ニラディック関数|返される値|
    |------------------------------|--------------------|
    |CURRENT_TIMESTAMP|現在の日付と時刻です。|
    |CURRENT_USER|挿入を実行しているユーザーの名前です。|
    |SESSION_USER|挿入を実行しているユーザーの名前です。|
    |SYSTEM_USER|挿入を実行しているユーザーの名前です。|
    |User|挿入を実行しているユーザーの名前です。|
- DEFAULT 定義内の *constant_expression* は、テーブル内の他の列、または、他のテーブル、ビュー、あるいはストアド プロシージャを参照できません。
- **timestamp** データ型を持つ列や IDENTITY プロパティを持つ列に DEFAULT 定義を作成することはできません。
- 別名データ型が既定のオブジェクトにバインドされている場合、別名データ型を持つ列に DEFAULT 定義を作成することはできません。

## <a name="check-constraints"></a>CHECK 制約
- 列は CHECK 制約をいくつでも持つことが可能です。また、条件には AND と OR を使って結合した複数の論理式を含めることができます。 列に対する複数の CHECK 制約は、それらが作成された順に検証されます。
- 検索条件はブール式によって評価する必要があり、他のテーブルを参照することはできません。
- 列レベルの CHECK 制約は、制約された列のみを参照でき、テーブルレベルの CHECK 制約は、同じテーブル内の列のみを参照できます。

  CHECK CONSTRAINTS とルールは、INSERT ステートメントと UPDATE ステートメントの実行中のデータの検証という同じ役割を果たします。

- 列に対して 1 つのルールおよび複数の CHECK 制約がある場合、すべての制限が評価されます。
- **text** 列、**ntext** 列、**image** 列に対しては CHECK 制約を定義できません。

## <a name="additional-constraint-information"></a>制約に関する追加情報
- 制約に対して作成されたインデックスは、`DROP INDEX` でドロップすることはできません。`ALTER TABLE` を使用して制約をドロップする必要があります。 制約に対して作成され、制約によって使用されるインデックスは、`ALTER INDEX ... REBUILD` を使用して再構築できます。 詳細については、「 [インデックスの再編成と再構築](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)」を参照してください。
- 制約名は[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従う必要があります。ただし、番号記号 (#) で始めることはできません。 *constraint_name* を指定しない場合、この制約にはシステムによって生成された名前が割り当てられます。 制約の違反に関するすべてのエラー メッセージには、制約名が表示されます。
- `INSERT` ステートメント、`UPDATE` ステートメントまたは `DELETE` ステートメントで制約の違反があった場合は、ステートメントが終了します。 ただし、`SET XACT_ABORT` が OFF に設定されている場合は、トランザクション (ステートメントが明示的なトランザクションの一部である場合) の処理は続行されます。 `SET XACT_ABORT` が ON に設定されている場合は、トランザクション全体がロールバックされます。 `@@ERROR` システム関数を調べることにより、トランザクション定義付きの `ROLLBACK TRANSACTION` ステートメントを使用することもできます。
- `ALLOW_ROW_LOCKS = ON` と `ALLOW_PAGE_LOCK = ON` の場合、インデックスにアクセスするとき、行レベル、ページ レベル、テーブル レベルのロックが許可されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]は適切なロックを選択し、行ロックまたはページ ロックをテーブル ロックにエスカレートすることができます。 `ALLOW_ROW_LOCKS = OFF` と `ALLOW_PAGE_LOCK = OFF` の場合、インデックスにアクセスするとき、テーブル レベルのロックのみが許可されます。
- テーブルが FOREIGN KEY または CHECK CONSTRAINTS とトリガーを持っている場合、制約条件は、トリガーが実行される前に評価されます。

テーブルとテーブルの列に関するレポートを表示するには、`sp_help` または `sp_helpconstraint` を使用します。 テーブル名を変更するには、`sp_rename` を使用します。 テーブルに依存するビューとストアド プロシージャに関するレポートを表示するには、[sys.dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md) および [sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md) を使用します。

## <a name="nullability-rules-within-a-table-definition"></a>テーブル定義内での NULL 値許容の規則
列の NULL 値の許容により、その列でその列内のデータとして null 値 (NULL) が許可されるかどうかが決定されます。 NULL は 0 でも空白でもありません。NULL は、何も入力されなかった、または明示的な NULL が設定されたことを意味し、通常、値が未知である、または使用できないことを示します。

`CREATE TABLE` または `ALTER TABLE` を使用してテーブルを作成または変更すると、データベースとセッションの設定は、列定義で使われているデータ型に NULL 値を許すかどうかの設定に影響を及ぼし、場合によっては、NULL 値を許すかどうかの設定をオーバーライドします。 計算列でない場合は、常に明示的に NULL または NOT NULL として列を定義することをお勧めします。または、ユーザー定義データ型を使用する場合は、データ型の規定の NULL 値の許容を列が使用できるようにすることをお勧めします。 スパース列では常に NULL を許容する必要があります。

列の NULL 値の許容を明示的に指定しない場合、列の NULL 値の許容は次の表に示す規則に従います。

|[列データ型]|Rule|
|----------------------|----------|
|別名データ型|[!INCLUDE[ssDE](../../includes/ssde-md.md)]は、データ型が作成されたときに指定された NULL 値を許容するかどうかの設定を使用します。 データ型に NULL 値を許容するかどうかの既定の設定を調べるには、**sp_help** を使用します。|
|CLR ユーザー定義型 (CLR user-defined type)|NULL 値を許容するかどうかは列の定義によって決まります。|
|システムから提供されているデータ型|システムから提供されているデータ型にオプションが 1 つしかない場合は、それが優先されます。 **timestamp** データ型は NOT NULL である必要があります。 いずれかのセッション設定が SET を使って ON に設定されている場合:<br />**ANSI_NULL_DFLT_ON** が ON になっていれば、NULL が割り当てられます。 <br />**ANSI_NULL_DFLT_OFF** が ON になっていれば、NOT NULL が割り当てられます。<br /><br /> いずれかのデータベース設定が ALTER DATABASE を使って構成されている場合:<br />**ANSI_NULL_DEFAULT_ON** が ON になっていれば、NULL が割り当てられます。 <br />**ANSI_NULL_DEFAULT_OFF** が ON になっていれば、NOT NULL が割り当てられます。<br /><br /> ANSI_NULL_DEFAULT のデータベース設定を表示するには、カタログ ビュー **sys.databases** を使用します|

どちらの ANSI_NULL_DFLT オプションもセッションに設定されていない状態で、データベースが既定値 (ANSI_NULL_DEFAULT が OFF) に設定されていると、既定値である NOT NULL が割り当てられます。

列が計算列の場合、その列に NULL 値を許容するかどうかは、常に[!INCLUDE[ssDE](../../includes/ssde-md.md)]によって自動的に決定されます。 このような列が NULL 値を許容するかどうかを確認するには、`COLUMNPROPERTY` 関数で **AllowsNull** プロパティを使用します。

> [!NOTE]
> SQL Server ODBC ドライバーでも SQL Server OLE DB ドライバーでも、特に指定のない限り ANSI_NULL_DFLT_ON が ON に設定されます。 ODBC と OLE DB ユーザーは、ODBC データ ソースで、またはアプリケーションで設定される接続の属性またはプロパティを使って、これを構成することができます。

## <a name="data-compression"></a>Data Compression

システム テーブルで圧縮を有効にすることはできません。 テーブルを作成しているとき、特に指定しない限り、データ圧縮は NONE に設定されます。 範囲外の一連のパーティションまたは単独のパーティションを指定すると、エラーが生成されます。 データ圧縮の詳細については、「 [データの圧縮](../../relational-databases/data-compression/data-compression.md)」を参照してください。

圧縮状態の変更による、テーブル、インデックス、またはパーティションへの影響を評価するには、 [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) ストアド プロシージャを使用します。

## <a name="permissions"></a>アクセス許可

データベースの `CREATE TABLE` 権限と、テーブルを作成するスキーマの `ALTER` 権限が必要です。

`CREATE TABLE` ステートメント内の列をユーザー定義型として定義する場合は、そのユーザー定義型に対する `REFERENCES` 権限が必要です。

`CREATE TABLE` ステートメント内の列を CLR ユーザー定義型として定義する場合は、その型の所有権か、その型に対する `REFERENCES` 権限が必要です。

`CREATE TABLE` ステートメント内の列に XML スキーマ コレクションが関連付けられている場合は、その XML スキーマ コレクションの所有権か、そのスキーマ コレクションに対する `REFERENCES` 権限が必要です。

すべてのユーザーが tempdb 内に一時テーブルを作成できます。

## <a name="examples"></a>使用例
### <a name="a-create-a-primary-key-constraint-on-a-column"></a>A. 列に PRIMARY KEY 制約を作成する
次の例では、`Employee` テーブルの `EmployeeID` 列にクラスター化インデックスを持つ PRIMARY KEY 制約の列定義を示しています。 制約名を指定していないため、制約名はシステムによって提供されます。

```sql
CREATE TABLE dbo.Employee (
    EmployeeID INT PRIMARY KEY CLUSTERED
);
```

### <a name="b-using-foreign-key-constraints"></a>B. FOREIGN KEY 制約の使用
FOREIGN KEY 制約は、他のテーブルを参照するために使用します。 外部キーは単一列キーの場合も複数列キーの場合もあります。 次の例では、`SalesPerson` テーブルを参照する `SalesOrderHeader` テーブルに対する単一列 FOREIGN KEY 制約を示しています。 単一列 FOREIGN KEY 制約では、REFERENCES 句のみが必要とされます。

```sql
SalesPersonID INT NULL REFERENCES SalesPerson(SalesPersonID)
```

FOREIGN KEY 句を明示的に使用して、列属性を書き換えることもできます。 列名が両方のテーブルで同じである必要はないことに注意してください。

```sql
FOREIGN KEY (SalesPersonID) REFERENCES SalesPerson(SalesPersonID)
```

複数列キー制約はテーブル制約として作成されます。 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース内の `SpecialOfferProduct` テーブルには、複数列 PRIMARY KEY が含まれています。 次の例は、このキーを他のテーブルから参照する方法を示しています。明示的な制約名は省略可能です。

```sql
CONSTRAINT FK_SpecialOfferProduct_SalesOrderDetail
    FOREIGN KEY (ProductID, SpecialOfferID)
    REFERENCES SpecialOfferProduct (ProductID, SpecialOfferID)
```

### <a name="c-using-unique-constraints"></a>C. UNIQUE 制約の使用
UNIQUE 制約は、非主キー列に一意性を設定するために使用します。 次の例では、`Name` テーブルの `Product` 列が一意でなくてはならないという制限を課しています。

```sql
Name NVARCHAR(100) NOT NULL
UNIQUE NONCLUSTERED
```

### <a name="d-using-default-definitions"></a>D. DEFAULT 定義の使用
既定値により、値が指定されない場合に (INSERT および UPDATE ステートメントで) 値が指定されます。 たとえば、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースは、会社内で従業員が行うさまざまな職務を列挙する参照テーブルを含むことができます。 各職務について説明する列では、文字列の規定値によって、実際の説明が明示的に入力されなかったときの説明を指定できます。

```sql
DEFAULT 'New Position - title not formalized yet'
```

DEFAULT 定義には、定数だけでなく関数を含めることができます。 エントリの現在の日付を取得するには、次の例を使います。

```sql
DEFAULT (GETDATE())
```

ニラディック関数のスキャンによってデータ整合性を向上させることもできます。 行を挿入したユーザーを追跡するには、USER 用ニラディック関数を使用します。 ニラディック関数をかっこで囲まないでください。

```sql
DEFAULT USER
```

### <a name="e-using-check-constraints"></a>E. CHECK 制約を使用する
次の例は、`Vendor` テーブルの `CreditRating` 列に入力する値に対する制限を示しています。 制約には名前がありません。

```sql
CHECK (CreditRating >= 1 and CreditRating <= 5)
```

この例は、テーブルの列に入力される文字データのパターンを制限する名前付き制約を示しています。

```sql
CONSTRAINT CK_emp_id CHECK (
    emp_id LIKE '[A-Z][A-Z][A-Z][1-9][0-9][0-9][0-9][0-9][FM]'
    OR emp_id LIKE '[A-Z]-[A-Z][1-9][0-9][0-9][0-9][0-9][FM]'
)
```

この例では、値が特定のリスト内にあるか、指定したパターンに従う必要があることを指定しています。

```sql
CHECK (
    emp_id IN ('1389', '0736', '0877', '1622', '1756')
    OR emp_id LIKE '99[0-9][0-9]'
)
```

### <a name="f-showing-the-complete-table-definition"></a>F. 完全なテーブル定義の表示
次の例は、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース内に作成された `PurchaseOrderDetail` テーブルの完全なテーブル定義とすべての制約定義を示します。 例を実行するときには、テーブル スキーマを `dbo` に変更することに注意してください。

```sql
CREATE TABLE dbo.PurchaseOrderDetail
(
    PurchaseOrderID int NOT NULL
        REFERENCES Purchasing.PurchaseOrderHeader(PurchaseOrderID),
    LineNumber smallint NOT NULL,
    ProductID int NULL
        REFERENCES Production.Product(ProductID),
    UnitPrice money NULL,
    OrderQty smallint NULL,
    ReceivedQty float NULL,
    RejectedQty float NULL,
    DueDate datetime NULL,
    rowguid uniqueidentifier ROWGUIDCOL NOT NULL
        CONSTRAINT DF_PurchaseOrderDetail_rowguid DEFAULT (NEWID()),
    ModifiedDate datetime NOT NULL
        CONSTRAINT DF_PurchaseOrderDetail_ModifiedDate DEFAULT (GETDATE()),
    LineTotal AS ((UnitPrice*OrderQty)),
    StockedQty AS ((ReceivedQty-RejectedQty)),
    CONSTRAINT PK_PurchaseOrderDetail_PurchaseOrderID_LineNumber
               PRIMARY KEY CLUSTERED (PurchaseOrderID, LineNumber)
               WITH (IGNORE_DUP_KEY = OFF)
)
ON PRIMARY;
```

### <a name="g-creating-a-table-with-an-xml-column-typed-to-an-xml-schema-collection"></a>G. XML スキーマ コレクションに型指定された xml 列を含むテーブルの作成
次の例では、XML スキーマ コレクション `xml` 型の `HRResumeSchemaCollection` 列を持つテーブルを作成します。 `DOCUMENT` キーワードは、*column_name* 内の `xml` データ型の各インスタンスに、トップレベル要素を 1 つだけ含むことができるように指定します。

```sql
CREATE TABLE HumanResources.EmployeeResumes
(
    LName nvarchar(25),
    FName nvarchar(25),
    Resume xml(DOCUMENT HumanResources.HRResumeSchemaCollection)
);
```

### <a name="h-creating-a-partitioned-table"></a>H. パーティション テーブルの作成
次の例では、テーブルまたはインデックスを 4 つのパーティションに分割するパーティション関数を作成します。 次に、例では、4 つのパーティションをそれぞれ保持するファイル グループを指定するパーティション構成を作成します。 最後に、そのパーティション構成を使用するテーブルを作成します。 この例では、ファイル グループが既にデータベースに存在していると仮定しています。

```sql
CREATE PARTITION FUNCTION myRangePF1 (int)
    AS RANGE LEFT FOR VALUES (1, 100, 1000);
GO

CREATE PARTITION SCHEME myRangePS1
    AS PARTITION myRangePF1
    TO (test1fg, test2fg, test3fg, test4fg);
GO  
  
CREATE TABLE PartitionTable (col1 int, col2 char(10))
    ON myRangePS1 (col1);
GO
```

`PartitionTable` の列 `col1` の値に基づき、各パーティションは次のように割り当てられます。

|[ファイル グループ]|test1fg|test2fg|test3fg|test4fg|
|---------------|-------------|-------------|-------------|-------------|
|**パーティション**|1|2|3|4|
|**値**|col 1 \<= 1|col1 > 1 AND col1 \<= 100|col1 > 100 AND col1 \<= 1,000|col1 > 1000|

### <a name="i-using-the-uniqueidentifier-data-type-in-a-column"></a>I. 列での uniqueidentifier データ型の使用
次の例では、`uniqueidentifier` 列を含むテーブルを作成します。 この例では、PRIMARY KEY 制約を使って、重複値を挿入するユーザーからテーブルを保護し、`DEFAULT` 制約で `NEWSEQUENTIALID()` 関数を使って、新しい行の値を指定します。 また、$ROWGUID キーワードを使用して参照できるように、この `uniqueidentifier` 列に ROWGUIDCOL プロパティを適用します。

```sql
CREATE TABLE dbo.Globally_Unique_Data
(
    GUID UNIQUEIDENTIFIER
        CONSTRAINT Guid_Default DEFAULT
        NEWSEQUENTIALID() ROWGUIDCOL,
    Employee_Name VARCHAR(60)
    CONSTRAINT Guid_PK PRIMARY KEY (GUID)
);
```

### <a name="j-using-an-expression-for-a-computed-column"></a>J. 計算列に式を使用する
次の例は、式 (`(low + high)/2`) を使用して `myavg` 計算列を計算する方法を示しています。

```sql
CREATE TABLE dbo.mytable
(
    low INT,
    high INT,
    myavg AS (low + high)/2
);
```

### <a name="k-creating-a-computed-column-based-on-a-user-defined-type-column"></a>K. ユーザー定義型の列に基づく計算列の作成
次の例では、ユーザー定義型 `utf8string` として定義された 1 つの列を持つテーブルを作成します。型のアセンブリと型自体が現在のデータベース中に既に作成されていることを前提としています。 2 番目の列は `utf8string` に基づいて定義され、**type(class)** `utf8string` のメソッド `ToString()` を使用して列の値が計算されます。

```sql
CREATE TABLE UDTypeTable
(
    u UTF8STRING,
    ustr AS u.ToString() PERSISTED
);
```

### <a name="l-using-the-user_name-function-for-a-computed-column"></a>L. 計算列に対する USER_NAME 関数の使用
次の例では、`myuser_name` 列で `USER_NAME()` 関数を使用します。

```sql
CREATE TABLE dbo.mylogintable
(
    date_in DATETIME,
    user_id INT,
    myuser_name AS USER_NAME()
);
```

### <a name="m-creating-a-table-that-has-a-filestream-column"></a>M. FILESTREAM 列を含むテーブルを作成する
次の例では、`Photo` という `FILESTREAM` 列を含むテーブルを作成します。 テーブルに 1 つ以上の `FILESTREAM` 列が含まれる場合、テーブルには `ROWGUIDCOL` 列が 1 つ存在する必要があります。

```sql
CREATE TABLE dbo.EmployeePhoto
(
    EmployeeId INT NOT NULL PRIMARY KEY,
    Photo VARBINARY(MAX) FILESTREAM NULL,
    MyRowGuidColumn UNIQUEIDENTIFIER NOT NULL ROWGUIDCOL UNIQUE DEFAULT NEWID()
);
```

### <a name="n-creating-a-table-that-uses-row-compression"></a>N. 行の圧縮を使用するテーブルの作成
次の例では、行の圧縮を使用するテーブルを作成します。

```sql
CREATE TABLE dbo.T1
(
    c1 INT,
    c2 NVARCHAR(200)
)
WITH (DATA_COMPRESSION = ROW);
```

その他のデータ圧縮の例については、「[データ圧縮](../../relational-databases/data-compression/data-compression.md)」を参照してください。

### <a name="o-creating-a-table-that-has-sparse-columns-and-a-column-set"></a>O. スパース列と列セットを含むテーブルの作成
次の例では、1 つのスパース列を含むテーブルと、2 つのスパース列と 1 つの列セットを含むテーブルを作成する方法を示します。 これらの例では基本構文を使用します。 さらに複雑な例については、「[スパース列の使用](../../relational-databases/tables/use-sparse-columns.md)」と「[列セットの使用](../../relational-databases/tables/use-column-sets.md)」をご覧ください。

この例では、1 つのスパース列を含むテーブルを作成します。

```sql
CREATE TABLE dbo.T1
(
    c1 INT PRIMARY KEY,
    c2 VARCHAR(50) SPARSE NULL
);
```

次の例では、2 つのスパース列と `CSet` という 1 つの列セットを含むテーブルを作成します。

```sql
CREATE TABLE T1
(
    c1 INT PRIMARY KEY,
    c2 VARCHAR(50) SPARSE NULL,
    c3 INT SPARSE NULL,
    CSet XML COLUMN_SET FOR ALL_SPARSE_COLUMNS
);
```

### <a name="p-creating-a-system-versioned-disk-based-temporal-table"></a>P. システム バージョン管理されたディスク ベースのテンポラル テーブルの作成
**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。

次の例では、新しい履歴テーブルにリンクされたテンポラル テーブルを作成する方法と、既存の履歴テーブルにリンクされたテンポラル テーブルを作成する方法を示します。 テンポラル テーブルでは、システムのバージョン管理を有効にするテーブルに対して有効になるように定義された主キーを含める必要があることに注意してください。 既存のテーブルのシステムのバージョン管理の追加または削除方法を示す例については、「[使用例](../../t-sql/statements/alter-table-transact-sql.md#Example_Top)」でシステムのバージョン管理の例をご覧ください。 ユース ケースについては、「[テンポラル テーブル](../../relational-databases/tables/temporal-tables.md)」をご覧ください。

この例では、新しい履歴テーブルにリンクされた新しいテンポラル テーブルを作成します。

```sql
CREATE TABLE Department
(
    DepartmentNumber CHAR(10) NOT NULL PRIMARY KEY CLUSTERED,
    DepartmentName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDepartmentNumber CHAR(10) NULL,
    SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
    SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
    PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)
)
WITH (SYSTEM_VERSIONING = ON);
```

この例では、既存の履歴テーブルにリンクされた新しいテンポラル テーブルを作成します。

```sql
-- Existing table
CREATE TABLE Department_History
(
    DepartmentNumber CHAR(10) NOT NULL,
    DepartmentName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDepartmentNumber CHAR(10) NULL,
    SysStartTime DATETIME2 NOT NULL,
    SysEndTime DATETIME2 NOT NULL
);

-- Temporal table
CREATE TABLE Department
(
    DepartmentNumber CHAR(10) NOT NULL PRIMARY KEY CLUSTERED,
    DepartmentName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDepartmentNumber CHAR(10) NULL,
    SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
    SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
    PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)
)
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.Department_History, DATA_CONSISTENCY_CHECK = ON));
```

### <a name="q-creating-a-system-versioned-memory-optimized-temporal-table"></a>Q. システム バージョン管理されたメモリ最適化テンポラル テーブルの作成
**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。

次の例では、ディスク ベースの新しい履歴テーブルにリンクされた、システム バージョン管理されたメモリ最適化テンポラル テーブルを作成する方法を示します。

この例では、新しい履歴テーブルにリンクされた新しいテンポラル テーブルを作成します。

```sql
CREATE SCHEMA History;
GO

CREATE TABLE dbo.Department
(
    DepartmentNumber CHAR(10) NOT NULL PRIMARY KEY NONCLUSTERED,
    DepartmentName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDepartmentNumber CHAR(10) NULL,
    SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
    SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
    PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)
)
WITH
(
    MEMORY_OPTIMIZED = ON,
    DURABILITY = SCHEMA_AND_DATA,
    SYSTEM_VERSIONING = ON (HISTORY_TABLE = History.DepartmentHistory)
);
```

この例では、既存の履歴テーブルにリンクされた新しいテンポラル テーブルを作成します。

```sql
-- Existing table
CREATE TABLE Department_History
(
    DepartmentNumber CHAR(10) NOT NULL,
    DepartmentName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDepartmentNumber CHAR(10) NULL,
    SysStartTime DATETIME2 NOT NULL,
    SysEndTime DATETIME2 NOT NULL
);

-- Temporal table
CREATE TABLE Department
(
    DepartmentNumber CHAR(10) NOT NULL PRIMARY KEY CLUSTERED,
    DepartmentName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDepartmentNumber CHAR(10) NULL,
    SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
    SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
    PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)
)
WITH
(
    SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.Department_History, DATA_CONSISTENCY_CHECK = ON)
);
```

### <a name="r-creating-a-table-with-encrypted-columns"></a>R. 暗号化された列を含むテーブルの作成
次の例では、2 つの暗号化された列を含むテーブルを作成します。 詳細については、「 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)」を参照してください。

```sql
CREATE TABLE Customers (
    CustName NVARCHAR(60)
        ENCRYPTED WITH (
            COLUMN_ENCRYPTION_KEY = MyCEK,
            ENCRYPTION_TYPE = RANDOMIZED,
            ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'
        ),
    SSN VARCHAR(11) COLLATE Latin1_General_BIN2
        ENCRYPTED WITH (
            COLUMN_ENCRYPTION_KEY = MyCEK,
            ENCRYPTION_TYPE = DETERMINISTIC ,
            ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'
        ),
    Age INT NULL
);
```

### <a name="s-create-an-inline-filtered-index"></a>S. インライン フィルターが適用されたインデックスを作成します
インライン フィルターが適用されたインデックスを持つテーブルを作成します。

```sql
CREATE TABLE t1
(
    c1 INT,
    index IX1 (c1) WHERE c1 > 0
);
```

### <a name="t-create-an-inline-index"></a>T. インライン インデックスの作成
ディスク ベース テーブルで NONCLUSTERED インラインを使用する方法を次に示します。

```sql
CREATE TABLE t1
(
    c1 INT,
    INDEX ix_1 NONCLUSTERED (c1)
);

CREATE TABLE t2
(
    c1 INT,
    c2 INT INDEX ix_1 NONCLUSTERED
);

CREATE TABLE t3
(
    c1 INT,
    c2 INT,
    INDEX ix_1 NONCLUSTERED (c1,c2)
);
```

### <a name="u-create-a-temporary-table-with-an-anonymously-named-compound-primary-key"></a>U. 匿名で名前付けされた複合主キーを持つ一時テーブルを作成します
匿名で名前付けされた複合主キーを持つテーブルを作成します。 これは、(それぞれが別のセッションにある) 2 つのセッション スコープの一時テーブルが、同じ制約の名前を使用している場合に、実行時の競合を回避するのに役立ちます。

```sql
CREATE TABLE #tmp
(
    c1 INT,
    c2 INT,
    PRIMARY KEY CLUSTERED ([c1], [c2])
);
GO
```

制約を明示的に名付ける場合は、2 つ目のセッションで次のようなエラーが発生します。

```
Msg 2714, Level 16, State 5, Line 1
There is already an object named 'PK_#tmp' in the database.
Msg 1750, Level 16, State 1, Line 1
Could not create constraint or index. See previous errors.
```

一時テーブルの名前が一意であるのに対して、制約の名前が一意ではないことが原因で、問題が発生しています。

### <a name="v-using-global-temporary-tables-in-azure-sql-database"></a>V. Azure SQL Database でのグローバル一時テーブルの使用
セッション A は、グローバル一時テーブル ##test を [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] testdb1 に作成し、1 行を追加します

```sql
CREATE TABLE ##test (
    a INT,
    b INT
);

INSERT INTO ##test
VALUES (1, 1);

-- Obtain object ID for temp table ##test
SELECT OBJECT_ID('tempdb.dbo.##test') AS 'Object ID';
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
1253579504
```

tempdb (2) で指定されたオブジェクト ID 1253579504 のグローバル一時テーブル名を取得します

```sql
SELECT name FROM tempdb.sys.objects WHERE object_id = 1253579504;
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```sql
##test
```

セッション B は、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] testdb1 に接続し、セッション A によって作成されたテーブル ##test にアクセスできます

```sql
SELECT * FROM ##test;
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```sql
1, 1
```

セッション C は、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] testdb2 内の別のデータベースに接続し、testdb1 で作成された ##test にアクセスしようとします。 この選択は、グローバル一時テーブルのデータベース スコープが原因で失敗します

```sql
SELECT * FROM ##test
```

これにより、次のエラーが生成されます。

```
Msg 208, Level 16, State 0, Line 1
Invalid object name '##test'
```

現在のユーザー データベース testdb1 からの [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] tempdb 内のシステム オブジェクトのアドレス指定

```sql
SELECT * FROM tempdb.sys.objects;
SELECT * FROM tempdb.sys.columns;
SELECT * FROM tempdb.sys.database_files;
```

## <a name="see-also"></a>参照
[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)
[COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md)
[CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)
[CREATE VIEW](../../t-sql/statements/create-view-transact-sql.md)
[Data Types](../../t-sql/data-types/data-types-transact-sql.md)
[DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md)
[sys.dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)
[sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)
[DROP TABLE](../../t-sql/statements/drop-table-transact-sql.md)
[CREATE PARTITION FUNCTION](../../t-sql/statements/create-partition-function-transact-sql.md)
[CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)
[CREATE TYPE](../../t-sql/statements/create-type-transact-sql.md)
[EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
[sp_help](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)
[sp_helpconstraint](../../relational-databases/system-stored-procedures/sp-helpconstraint-transact-sql.md)
[sp_rename](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)
[sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
