---
title: OPENROWSET (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OPENROWSET_TSQL
- OPENROWSET
dev_langs:
- TSQL
helpviewer_keywords:
- data sources [SQL Server]
- OPENROWSET function
- remote data access [SQL Server], OPENROWSET
- ad hoc distributed queries
- OPENROWSET function, Transact-SQL
- OPENROWSET statement
- OLE DB data sources [SQL Server]
- ad hoc connection information
ms.assetid: f47eda43-33aa-454d-840a-bb15a031ca17
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: d50c8c83ebba970a847c5a2db70ca0268637d3e8
ms.sourcegitcommit: 02449abde606892c060ec9e9e9a85a3f49c47c6c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74542285"
---
# <a name="openrowset-transact-sql"></a>OPENROWSET (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

OLE DB データ ソースからリモート データへのアクセスに必要な、すべての接続情報をインクルードします。 このメソッドは、リンク サーバー内のテーブルにアクセスする代わりに、OLE DB を使用してリモート データに接続しアクセスするアドホック メソッドです。 OLE DB データ ソースをより頻繁に参照する場合は、代わりにリンク サーバーを使用してください。 詳しくは、「 [リンク サーバー &#40;データベース エンジン&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)」を参照してください。 `OPENROWSET` 関数は、テーブル名と同じように、クエリの FROM 句で参照できます。 `OPENROWSET` 関数は、`INSERT`、`UPDATE`、または `DELETE` ステートメントのターゲット テーブルとしても参照できます。ただしこれは OLE DB プロバイダーの機能により制限されます。 クエリでは複数の結果セットが返される場合がありますが、`OPENROWSET` では最初の 1 つだけが返されます。

`OPENROWSET` では、組み込みの BULK プロバイダーによる一括操作もサポートされ、ファイルのデータを行セットとして読み取り、返すことができます。

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>構文

```
OPENROWSET
( { 'provider_name' , { 'datasource' ; 'user_id' ; 'password'
   | 'provider_string' }
   , {   [ catalog. ] [ schema. ] object
       | 'query'
     }
   | BULK 'data_file' ,
       { FORMATFILE = 'format_file_path' [ <bulk_options> ]
       | SINGLE_BLOB | SINGLE_CLOB | SINGLE_NCLOB }
} )

<bulk_options> ::=
   [ , CODEPAGE = { 'ACP' | 'OEM' | 'RAW' | 'code_page' } ]
   [ , DATASOURCE = 'data_source_name' ]
   [ , ERRORFILE = 'file_name' ]
   [ , ERRORFILE_DATASOURCE = 'data_source_name' ]
   [ , FIRSTROW = first_row ]
   [ , LASTROW = last_row ]
   [ , MAXERRORS = maximum_errors ]
   [ , ROWS_PER_BATCH = rows_per_batch ]
   [ , ORDER ( { column [ ASC | DESC ] } [ ,...n ] ) [ UNIQUE ] ]
  
   -- bulk_options related to input file format
   [ , FORMAT = 'CSV' ]
   [ , FIELDQUOTE = 'quote_characters']
   [ , FORMATFILE = 'format_file_path' ]
```

## <a name="arguments"></a>引数

'*provider_name*' レジストリで指定された OLE DB プロバイダーのフレンドリ名 (または PROGID) を表す文字列です。 *provider_name* 既定値はありません。

'*datasource*' 特定の OLE DB データ ソースに対応する文字列定数です。 *datasource* は DBPROP_INIT_DATASOURCE のプロパティで、プロバイダーの IDBProperties インターフェイスに渡され、プロバイダーの初期化に使用されます。 一般的に、この文字列にはデータベース ファイルの名前、データベース サーバーの名前、プロバイダーがデータベースを検索する際に認識する名前のいずれかを指定します。

'*user_id*' 指定された OLE DB プロバイダーに渡されるユーザー名を表す文字列定数です。 *user_id* は接続のセキュリティ コンテキストを示し、DBPROP_AUTH_USERID プロパティとして渡され、プロバイダーの初期化に使用されます。 *user_id* Microsoft Windows のログイン名にすることはできません。

'*password*' OLE DB プロバイダーに渡されるユーザー パスワードを表す文字列定数です。 *password* は DBPROP_AUTH_PASSWORD プロパティとして引き渡され、プロバイダーの初期化に使用されます。 *password* を Microsoft Windows のパスワードとすることはできません。

'*provider_string*' プロバイダー固有の接続文字列です。これは、DBPROP_INIT_PROVIDERSTRING プロパティとして渡され、OLE DB の初期化に使用されます。 *provider_string* 通常、プロバイダーの初期化に必要なすべての接続情報をカプセル化します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーで認識されるキーワードの一覧については、「[初期化プロパティと承認プロパティ](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)」を参照してください。

*catalog* 指定したオブジェクトが存在するカタログまたはデータベースの名前です。

*schema* 指定したオブジェクトのスキーマまたはオブジェクト所有者の名前です。

*object* 操作するオブジェクトを一意に識別するオブジェクト名です。

'*query*' プロバイダーに送られ、プロバイダーによって実行される文字列定数です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のローカル インスタンスでは、このクエリは処理されず、プロバイダーから返されたクエリ結果が処理されます (パススルー クエリ)。 パススルー クエリは、表形式のデータをテーブル名ではなくコマンド言語のみで公開するプロバイダーで使用すると便利です。 パススルー クエリは、クエリ プロバイダーが OLE DB をサポートしていれば、リモート サーバーでサポートされてコマンド オブジェクトとその必須インターフェイス。 詳細については、[SQL Server Native Client &#40;OLE DB&#41; のリファレンス](../../relational-databases/native-client-ole-db-interfaces/sql-server-native-client-ole-db-interfaces.md)をご覧ください。

BULK ファイルからのデータ読み取りに OPENROWSET の BULK 行セット プロバイダーを使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、OPENROWSET を使用すると、データを対象テーブルに読み込むことなくデータ ファイルからの読み取りができます。 このため、OPENROWSET は簡単な SELECT ステートメントで使用できます。

> [!IMPORTANT]
> Azure SQL Database でサポートされるのは、Azure Blob Storage からの読み取りのみです。

BULK オプションの引数を使用すると、データの読み取りを開始および終了する場所や、エラーの取り扱い、データの解釈方法について、細かく制御することができます。 たとえば、データ ファイルを **varbinary**、**varchar**、**nvarchar** 型の単一行、単一列の行セットとして読み取るように指定できます。 既定の動作については、後の引数の説明を参照してください。

 BULK オプションの使用方法の詳細については、後の「解説」を参照してください。 BULK オプションに必要な権限については、このトピックで後述する「アクセス許可」を参照してください。

> [!NOTE]
> OPENROWSET (BULK ...) を完全復旧モデルでデータのインポートに使用する場合、ログ記録は最適化されません。

データを一括インポート用に準備する方法については、「[一括エクスポートまたは一括インポートのデータの準備 &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)」をご覧ください。

'*data_file*' データをターゲット テーブルにコピーするデータ ファイルの完全なパスです。
**適用対象:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 以降では、data_file は Azure Blob Storage に格納することができます。 例については、「[Azure BLOB ストレージのデータに一括アクセスする例](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)」をご覧ください。

> [!IMPORTANT]
> Azure SQL Database でサポートされるのは、Azure Blob Storage からの読み取りのみです。

\<bulk_options> BULK オプションの引数を 1 つまたは複数指定します。

CODEPAGE = { 'ACP'| 'OEM'| 'RAW'| '*code_page*' } データ ファイル内のデータのコード ページを指定します。 CODEPAGE は、データに **char**、**varchar**、**text** 列 (文字値が 127 より大きいか、32 未満) が含まれている場合にのみ当てはまります。

> [!IMPORTANT]
> CODEPAGE は、Linux ではサポートされていないオプションです。

> [!NOTE]
> フォーマット ファイルの各列に対して照合順序名を指定することをお勧めします (65001 オプションを照合順序/コード ページ仕様よりも優先する場合を除く)。

|CODEPAGE の値|[説明]|
|--------------------|-----------------|
|ACP|**char**、**varchar**、または **text** データ型の列を、ANSI/[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows コード ページ (ISO 1252) から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コード ページに変換します。|
|OEM (既定値)|**char**、**varchar**、または **text** データ型の列を、システムの OEM コード ページから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コード ページに変換します。|
|RAW|コード ページの変換は行われません。 これは最も高速なオプションです。|
|*code_page*|データ ファイルの文字データのエンコードに使用されているソースのコード ページを示します (例 : 850)。<br /><br /> **重要**[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] より前のバージョンではコード ページ 65001 (UTF-8 エンコード) がサポートされません。|

ERRORFILE ='*file_name*' 形式エラーがあり、OLE DB 行セットに変換できない行を収集するときに使用するファイルを指定します。 該当する行は、データ ファイルからこのエラー ファイルに "そのまま" コピーされます。

エラー ファイルはコマンドの実行開始時に作成されます。 存在するファイルの場合にはエラーが発生し、 さらに、拡張子 .ERROR.txt の制御ファイルが作成されます。 このファイルにはエラー ファイルの各行の参照と、エラーの診断が含まれています。 エラーが修正されると、データは読み込み可能になります。
**適用対象:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 以降では、`error_file_path` は Azure Blob Storage に格納することができます。

'errorfile_data_source_name' **以下に適用されます:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
名前付きの外部データ ソースで、インポート中に見つかったエラーを格納するエラー ファイルの Azure Blob Storage の場所を指しています。 外部データ ソースは、[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 で追加された `TYPE = BLOB_STORAGE` オプションを使用して作成する必要があります。 詳しくは、「[CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)」をご覧ください。

FIRSTROW =*first_row* 最初に読み込む行の番号を指定します。 既定値は 1 です。 指定したデータ ファイルの最初の行を示します。 行番号は行ターミネータの数をカウントして決定されます。 FIRSTROW は 1 から始まります。

LASTROW =*last_row* 最後に読み込む行の行番号を指定します。 既定値は 0 です。 指定したデータ ファイルの最後の行を示します。

MAXERRORS =*maximum_errors* フォーマット ファイルで定義されている、構文エラーまたは違反行の許容最大数を指定します。この数を超えると、OPENROWSET で例外が発生することがあります。 OPENROWSET は、MAXERRORS に達するまで、違反行を読み込まずに無視し、違反行はエラーとしてカウントされます。

既定の *maximum_errors* は 10 です。

> [!NOTE]
> MAX_ERRORS は CHECK 制約、または変換には適用されません **money** と **bigint** データ型。

ROWS_PER_BATCH =*rows_per_batch* データ ファイル内のデータ行の概算数を指定します。 この値は実際の行数と同じ次数にする必要があります。

OPENROWSET では、常にデータ ファイルが単一のバッチとしてインポートされますが、 *rows_per_batch* に 0 より大きい値 (> 0) を指定した場合、クエリ プロセッサでは、クエリ プランのリソース割り当てのヒントとして *rows_per_batch* の値が使用されます。

ROWS_PER_BATCH の既定値はありません。 ROWS_PER_BATCH = 0 の指定は、ROWS_PER_BATCH を省略した場合と同じになります。

ORDER ( { *column* [ ASC | DESC ] } [ ,... *n* ] [ UNIQUE ] ) データ ファイル内のデータの並べ替え方法を指定する省略可能なヒントです。 既定では、一括操作はデータ ファイルが並べ替えられていないことを前提に実行されます。 指定された順序を利用してクエリ オプティマイザーでより効率的なクエリ プランを生成することができる場合、パフォーマンスが向上する可能性があります。 並べ替えの指定は、次の場合に役立ちます。

- クラスター化インデックスを持ち、クラスター化インデックス キーで行セット データが並べ替えられているテーブルに行を挿入する場合。
- 行セットを別のテーブルに結合するとき、並べ替え列と結合列が一致する場合。
- 並べ替え列で行セット データを集約する場合。
- クエリの FROM 句で行セットをソース テーブルとして使用するとき、並べ替え列と結合列が一致する場合。

UNIQUE は、データ ファイルに重複したエントリがないことを指定します。

データ ファイル内の実際の行が指定の順序で並べ替えられていない場合、または UNIQUE ヒントが指定された一方で重複したキーが存在する場合は、エラーが返されます。

ORDER を使用する場合は列の別名が必要です。 列の別名リストは、BULK 句によってアクセスされる派生テーブルを参照する必要があります。 ORDER 句に指定された列名は、この列の別名リストを参照します。 大きな値の型 (**varchar (max)** , 、**nvarchar (max)** , 、**varbinary (max)** , 、および **xml**) およびラージ オブジェクト (LOB) 型 (**text**, 、**ntext**, 、および **image**) 列を指定することはできません。

SINGLE_BLOB *data_file* の内容を、**varbinary(max)** 型の単一行、単一列の行セットとして返します。

> [!IMPORTANT]
> すべての Windows エンコード変換がサポートされるのは SINGLE_BLOB オプションだけなので、SINGLE_CLOB オプションや SINGLE_NCLOB オプションではなく、SINGLE_BLOB オプションだけを使用して XML データをインポートすることをお勧めします。

SINGLE_CLOB

*data_file* を ASCII として読み取り、現在のデータベースの照合順序に従い、内容を **varchar(max)** 型の単一行、単一列の行セットとして返します。

SINGLE_NCLOB *data_file* を UNICODE として読み取り、現在のデータベースの照合順序に従い、内容を **nvarchar(max)** 型の単一行、単一列の行セットとして返します。

### <a name="input-file-format-options"></a>入力ファイル フォーマットのオプション

FORMAT **=** 'CSV' **以下に適用されます:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
[RFC 4180](https://tools.ietf.org/html/rfc4180) 標準に準拠しているコンマ区切り値ファイルを指定します。

FORMATFILE ='*format_file_path*' フォーマット ファイルの完全なパスを指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、次の 2 種類のフォーマット ファイルがサポートされます: XML と非 XML。

フォーマット ファイルは、結果セットの列の型を定義する場合に必要となります。 ただし SINGLE_CLOB、SINGLE_BLOB、または SINGLE_NCLOB を指定した場合は例外で、この場合はフォーマット ファイルは必要ありません。

フォーマット ファイルについては、「[データの一括インポートでのフォーマット ファイルの使用 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)」をご覧ください。

**適用対象:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 以降では、format_file_path は Azure Blob Storage に格納することができます。 例については、「[Azure BLOB ストレージのデータに一括アクセスする例](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)」をご覧ください。

FIELDQUOTE **=** 'field_quote' **以下に適用されます:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
CSV ファイルで引用符文字として使用される文字を指定します。 指定されていない場合は、[RFC 4180](https://tools.ietf.org/html/rfc4180) 標準の定義に従って引用符文字 (") が引用符文字として使用されます。

## <a name="remarks"></a>解説

`OPENROWSET` は、OLE DB データ ソースからリモート データにアクセスするときに使用できます。ただしこの場合、指定したプロバイダーに対して **DisallowAdhocAccess** レジストリ オプションが明示的に 0 に設定されており、Ad Hoc Distributed Queries 詳細構成オプションが有効になっている必要があります。 これらのオプションが設定されていない場合は、既定でアドホック アクセスは許可されません。

リモートの OLE DB データ ソースにアクセスするとき、信頼関係接続のログイン ID は、クライアントの接続先サーバーからクエリの対象サーバーに自動的に委任されるわけではありません。 したがって、認証の委任を構成する必要があります。

指定したデータ ソースにおいて、OLE DB プロバイダーが複数のカタログとスキーマをサポートする場合は、カタログ名とスキーマ名を指定する必要があります。 _カタログ_と_スキーマ_の値は、OLE DB プロバイダーではサポートしていない場合は省略できます。 プロバイダーがスキーマ名しかサポートしていない場合は、_スキーマ_ **.** _オブジェクト_ という形式の 2 部構成の名前を指定する必要があります。 プロバイダーがカタログ名しかサポートしていない場合は、_カタログ_ **.** _スキーマ_ **.** _オブジェクト_ という形式の 3 部構成の名前を指定する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーを使用するパススルー クエリには、3 つの部分で構成される名前を指定する必要があります。 詳しくは、「[Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)」をご覧ください。

`OPENROWSET` の引数に変数は指定できません。

`FROM` 句での `OPENDATASOURCE`、`OPENQUERY`、または `OPENROWSET` の呼び出しは、更新のターゲットとして使用されるこれらの関数の呼び出しとは別に評価されます。これは、両方の呼び出しに同じ引数が指定されている場合にも当てはまります。 特に、いずれか一方の呼び出しの結果に適用されるフィルター条件または結合条件は、もう一方の結果に影響しません。

## <a name="using-openrowset-with-the-bulk-option"></a>OPENROWSET を BULK オプションと共に使用する

次に示す [!INCLUDE[tsql](../../includes/tsql-md.md)] の機能拡張では、OPENROWSET(BULK...) 関数がサポートされます。

- `SELECT` と共に使用される FROM 句では、テーブル名の代わりに `OPENROWSET(BULK...)` を呼び出すことができます。このとき `SELECT` の機能に制限はありません。

   `OPENROWSET` で `BULK` オプションを使用するには、`FROM` 句に相関名を指定する必要があります。これは範囲変数または別名とも呼ばれます。 列には別名を指定できます。 列の別名のリストを指定しない場合は、フォーマット ファイルに列名が必要です。 次のように、列の別名を指定した場合は、フォーマット ファイルの列名をオーバーライドして使用されます。

  - `FROM OPENROWSET(BULK...) AS table_alias`
  - `FROM OPENROWSET(BULK...) AS table_alias(column_alias,...n)`

  > [!IMPORTANT]
  > `AS <table_alias>` への追加に失敗すると次のエラーが発生します:Msg 491, Level 16, State 1, Line 20 FROM 句の一括行セットには相関名を指定してください。

- `SELECT...FROM OPENROWSET(BULK...)` ステートメントは、データをテーブルにインポートせずに、ファイル内のデータに対してクエリを直接実行します。 また、`SELECT...FROM OPENROWSET(BULK...)` ステートメントでフォーマット ファイルを使用して列名やデータ型を指定すると、一括列の別名を列挙することもできます。
- `INSERT` ステートメントまたは `MERGE` ステートメント内でソース テーブルとして `OPENROWSET(BULK...)` を使用すると、データ ファイルから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルにデータが一括インポートされます。 詳細については、「[BULK INSERT または OPENROWSET&#40;BULK...&#41; を使用した一括データのインポート &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)」をご覧ください。
- `INSERT` ステートメントと共に使用する `OPENROWSET BULK` オプションでは、BULK 句でテーブル ヒントがサポートされます。 `TABLOCK` などの通常のテーブル ヒントに加えて、`BULK` 句では、次の特殊なテーブル ヒントを使用できます: `IGNORE_CONSTRAINTS` (`CHECK` および `FOREIGN KEY` 制約のみ無視します)、`IGNORE_TRIGGERS`、`KEEPDEFAULTS`、`KEEPIDENTITY`。 詳細については、「[テーブル ヒント &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)」を参照してください。

  `INSERT...SELECT * FROM OPENROWSET(BULK...)` ステートメントの使用方法については、「[データの一括インポートと一括エクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)」をご覧ください。 一括インポートによって実行される行挿入操作がトランザクション ログに記録される条件について詳しくは、「 [一括インポートで最小ログ記録を行うための前提条件](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)」をご覧ください。

> [!NOTE]
> `OPENROWSET` を使用するにあたっては、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で権限借用がどのように処理されるかを理解しておくことが重要です。 セキュリティの考慮事項については、「[BULK INSERT または OPENROWSET&#40;BULK...&#41; を使用した一括データのインポート &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)」をご覧ください。

### <a name="bulk-importing-sqlchar-sqlnchar-or-sqlbinary-data"></a>SQLCHAR、SQLNCHAR、または SQLBINARY データの一括インポート

OPENROWSET(BULK...) では、指定がない場合、SQLCHAR、SQLNCHAR、および SQLBINARY データの最大の長さが 8000 バイトを超えないものと想定されます。 インポートされるデータが 8000 バイトを超える **varchar(max)** 、**nvarchar(max)** 、または **varbinary(max)** オブジェクトを含む LOB データ フィールドにある場合、XML フォーマット ファイルを使用してそのデータ フィールドの最大の長さを定義する必要があります。 最大の長さを指定するには、フォーマット ファイルを編集して MAX_LENGTH 属性を宣言します。

> [!NOTE]
> 自動生成されたフォーマット ファイルには、LOB フィールドの長さまたは最大長の指定がありません。 ただし、手作業でフォーマット ファイルを編集して長さまたは最大の長さを指定できます。

### <a name="bulk-exporting-or-importing-sqlxml-documents"></a>SQLXML ドキュメントの一括エクスポートまたは一括インポート

SQLXML データを一括エクスポートまたは一括インポートする場合、フォーマット ファイルのデータ型には次のいずれかを使用します。

|データ型|結果|
|---------------|------------|
|SQLCHAR または SQLVARYCHAR|データは、クライアント コード ページまたは照合順序で暗黙的に指定されるコード ページで送られます。|
|SQLNCHAR または SQLNVARCHAR|データは Unicode として送られます。|
|SQLBINARY または SQLVARYBIN|データは変換なしで送られます。|

## <a name="permissions"></a>アクセス許可

`OPENROWSET` 権限は、OLE DB プロバイダーに渡されるユーザー名の権限によって決まります。 `BULK` オプションを使用するには、`ADMINISTER BULK OPERATIONS` 権限が必要です。

## <a name="examples"></a>例

### <a name="a-using-openrowset-with-select-and-the-sql-server-native-client-ole-db-provider"></a>A. OPENROWSET を SELECT および SQL Server Native Client OLE DB プロバイダーと共に使用する

次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーを使用して、リモート サーバー `HumanResources.Department` のデータベース [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] のテーブル `Seattle1` にアクセスします (SQLNCLI を使用すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により最新バージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーにリダイレクトされます)。`SELECT` ステートメントは、返す行セットの定義に使用します。 プロバイダーの文字列には、`Server` と `Trusted_Connection` キーワードが含まれます。 これらのキーワードは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーによって認識されます。

```sql
SELECT a.*
FROM OPENROWSET('SQLNCLI', 'Server=Seattle1;Trusted_Connection=yes;',
     'SELECT GroupName, Name, DepartmentID
      FROM AdventureWorks2012.HumanResources.Department
      ORDER BY GroupName, Name') AS a;
```

### <a name="b-using-the-microsoft-ole-db-provider-for-jet"></a>B. Microsoft OLE DB Provider for Jet を使用する

次の例では、[!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet を介して、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Access `Northwind` データベース内のテーブル `Customers` にアクセスします。

> [!NOTE]
> この例では、Access がインストールされていることを前提としています。 この例を実行するには、Northwind データベースをインストールする必要があります。

```sql
SELECT CustomerID, CompanyName
   FROM OPENROWSET('Microsoft.Jet.OLEDB.4.0',
      'C:\Program Files\Microsoft Office\OFFICE11\SAMPLES\Northwind.mdb';
      'admin';'',Customers);
```

> [!IMPORTANT]
> Azure SQL Database でサポートされるのは、Azure Blob Storage からの読み取りのみです。

### <a name="c-using-openrowset-and-another-table-in-an-inner-join"></a>C. OPENROWSET と INNER JOIN 内の別のテーブルを使用する

次の例では、ローカル インスタンスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `Northwind` データベース内の `Customers` テーブル、および同じコンピューター上に格納されている Access `Northwind` データベースの `Orders` テーブルから、すべてのデータを選択します。

> [!NOTE]
> この例では、Access がインストールされていることを前提としています。 この例を実行するには、Northwind データベースをインストールする必要があります。

```sql
USE Northwind;
GO
SELECT c.*, o.*
FROM Northwind.dbo.Customers AS c
   INNER JOIN OPENROWSET('Microsoft.Jet.OLEDB.4.0',
   'C:\Program Files\Microsoft Office\OFFICE11\SAMPLES\Northwind.mdb';'admin';'', Orders)
   AS o
   ON c.CustomerID = o.CustomerID ;
```

> [!IMPORTANT]
> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] でサポートされるのは、Azure Blob Storage からの読み取りのみです。

### <a name="d-using-openrowset-to-bulk-insert-file-data-into-a-varbinarymax-column"></a>D. OPENROWSET を使用して、ファイル データを varbinary(max) 列に一括挿入する

 次の例では、小さなテーブルを作成し、ルート ディレクトリ `C:` にあるファイル `Text1.txt` から `varbinary(max)` 列にファイル データを挿入します。

```sql
CREATE TABLE myTable(FileName nvarchar(60),
  FileType nvarchar(60), Document varbinary(max));
GO

INSERT INTO myTable(FileName, FileType, Document)
   SELECT
      'Text1.txt' AS FileName
      , '.txt' AS FileType
      , *
   FROM OPENROWSET(BULK N'C:\Text1.txt', SINGLE_BLOB) AS Document;
GO
```

> [!IMPORTANT]
> Azure SQL Database でサポートされるのは、Azure Blob Storage からの読み取りのみです。

### <a name="e-using-the-openrowset-bulk-provider-with-a-format-file-to-retrieve-rows-from-a-text-file"></a>E. OPENROWSET BULK プロバイダーをフォーマット ファイルと共に使用して、テキスト ファイルから行を取得する

次の例では、フォーマット ファイルを使用して、タブ区切りのテキスト ファイル `values.txt` から行を取得します。このテキスト ファイルには次のデータが含まれます。

```sql
1     Data Item 1
2     Data Item 2
3     Data Item 3
```

フォーマット ファイル `values.fmt` では、`values.txt` の列が次のように表されています。

```sql
9.0
2  
1  SQLCHAR  0  10 "\t"        1  ID                      SQL_Latin1_General_Cp437_BIN
2  SQLCHAR  0  40 "\r\n"      2  Description        SQL_Latin1_General_Cp437_BIN
```

データを取得するクエリは次のようになります。

```sql
SELECT a.* FROM OPENROWSET( BULK 'c:\test\values.txt',
   FORMATFILE = 'c:\test\values.fmt') AS a;
```

> [!IMPORTANT]
> Azure SQL Database でサポートされるのは、Azure Blob Storage からの読み取りのみです。

### <a name="f-specifying-a-format-file-and-code-page"></a>F. フォーマット ファイルとコード ページを指定する

次の例では、フォーマット ファイルとコード ページの両方のオプションを同時に使用する方法を示します。

```sql
INSERT INTO MyTable SELECT a.* FROM
OPENROWSET (BULK N'D:\data.csv', FORMATFILE =
    'D:\format_no_collation.txt', CODEPAGE = '65001') AS a;
```

### <a name="g-accessing-data-from-a-csv-file-with-a-format-file"></a>G. フォーマット ファイルを使用して CSV ファイルのデータにアクセスする

**適用対象:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.

```sql
SELECT *
FROM OPENROWSET(BULK N'D:\XChange\test-csv.csv',
    FORMATFILE = N'D:\XChange\test-csv.fmt',
    FIRSTROW=2,
    FORMAT='CSV') AS cars;
```

> [!IMPORTANT]
> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] でサポートされるのは、Azure Blob Storage からの読み取りのみです。

### <a name="h-accessing-data-from-a-csv-file-without-a-format-file"></a>H. フォーマット ファイルなしで CSV ファイルのデータにアクセスする

```sql
SELECT * FROM OPENROWSET(
   BULK 'C:\Program Files\Microsoft SQL Server\MSSQL14.CTP1_1\MSSQL\DATA\inv-2017-01-19.csv',
   SINGLE_CLOB) AS DATA;
```

```sql
select *
from openrowset
   (  'MSDASQL'
     ,'Driver={Microsoft Access Text Driver (*.txt, *.csv)}'
     ,'select * from E:\Tlog\TerritoryData.csv')
;
```

> [!IMPORTANT]
>
> - ODBC ドライバーは 64 ビットである必要があります。 このことを確認するには、Windows で [OBDC データ ソース](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md) アプリケーションの **[ドライバー]** タブを開きます。 64 ビット バージョンの sqlservr.exe では機能しない、32 ビットの `Microsoft Text Driver (*.txt, *.csv)` があります。
> - Azure SQL Database でサポートされるのは、Azure Blob Storage からの読み取りのみです。

### <a name="i-accessing-data-from-a-file-stored-on-azure-blob-storage"></a>I. Azure Blob Storage に格納されているファイルのデータにアクセスする

**適用対象:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
次の例では、Shared Access Signature に対して作成された Azure ストレージ アカウントとデータベース スコープ資格情報のコンテナーを指している外部データ ソースを使用します。

```sql
SELECT * FROM OPENROWSET(
   BULK 'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   SINGLE_CLOB) AS DataFile;
```

資格情報と外部データ ソースの構成などの `OPENROWSET` の詳細な例については、「[Azure BLOB ストレージのデータに一括アクセスする例](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)」をご覧ください。

### <a name="j-importing-into-a-table-from-a-file-stored-on-azure-blob-storage"></a>J. Azure Blob Storage に格納されているファイルからテーブルへのインポート

次の例は、OPENROWSET コマンドを使用して、SAS キーを作成した Azure Blob Storage の場所にある csv ファイルからデータを読み込む方法を示しています。 Azure Blob Storage の場所は、外部データ ソースとして構成されます。 これには、ユーザー データベース内でマスター キーを使用して暗号化された共有アクセス署名を使用するデータベース スコープ資格情報が必要です。

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
          LOCATION = 'https://****************.blob.core.windows.net/curriculum'
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
> Azure SQL Database でサポートされるのは、Azure Blob Storage からの読み取りのみです。

### <a name="additional-examples"></a>その他の例

`INSERT...SELECT * FROM OPENROWSET(BULK...)` のその他の使用例については、次のトピックをご覧ください。

- [XML ドキュメントの一括インポートと一括エクスポートの例 &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)
- [データの一括インポート時の ID 値の保持 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)
- [一括インポート中の NULL の保持または既定値の使用 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)
- [データの一括インポートでのフォーマット ファイルの使用 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)
- [文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)
- [フォーマット ファイルを使用したテーブル列のスキップ &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)
- [フォーマット ファイルを使用したデータ フィールドのスキップ &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)
- [フォーマット ファイルを使用したテーブル列とデータ ファイル フィールドのマッピング &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)

## <a name="see-also"></a>参照

- [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)
- [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)
- [データの一括インポートと一括エクスポート &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)
- [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)
- [OPENDATASOURCE &#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)
- [OPENQUERY &#40;Transact-SQL&#41;](../../t-sql/functions/openquery-transact-sql.md)
- [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)
- [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)
- [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)
- [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)
- [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)
