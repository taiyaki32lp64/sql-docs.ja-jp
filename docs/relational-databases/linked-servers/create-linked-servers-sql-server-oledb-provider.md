---
title: リンク サーバー プロバイダーを作成する
ms.date: 07/01/2019
ms.prod: sql
ms.technology: ''
ms.prod_service: database-engine
ms.reviewer: MikeRayMSFT
ms.topic: conceptual
author: pmasl
ms.author: pelopes
manager: rothj
ms.custom: seo-dt-2019
ms.openlocfilehash: 933a37dd4ef627796b7688510bd235c80db417be
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095991"
---
# <a name="microsoft-sql-server-distributed-queries-ole-db-connectivity"></a>Microsoft SQL Server 分散クエリ: OLE DB 接続

この記事では、Microsoft SQL Server クエリ プロセッサと OLE DB プロバイダーのやり取りによって分散クエリと異種クエリがどのように実現されるかについて説明します。 主に OLE DB プロバイダーの開発者を対象としており、OLE DB の仕様を確実に理解していることを前提としています。 SQL Server クエリ プロセッサと OLE DB プロバイダーの間の OLE DB インターフェイスに重点を置いており、分散クエリ機能自体には重点を置いていません。 分散クエリ機能の詳細については、「[リンク サーバー](../../relational-databases/linked-servers/linked-servers-database-engine.md)」を参照してください。

## <a name="overview-and-terminology"></a>概要と用語

 Microsoft SQL Server では、分散クエリを使用することで、SQL Server ユーザーが、SQL Server をベースにしたサーバーの外部にあるデータ、つまり SQL Server を実行している他のサーバー内、または OLE DB インターフェイスを公開している他のデータ ソース内のいずれかにあるデータにアクセスできます。 OLE DB によって、異種データ ソースから表形式データへの統一されたアクセス方法が提供されます。

この記事で使用する分散クエリとは、1 つ以上の外部 OLE DB データ ソースにあるテーブルや行を参照する `SELECT`、`INSERT`、`UPDATE`、または `DELETE` ステートメントのことです。

リモート テーブルとは、OLE DB データ ソースに格納されており、クエリを実行する SQL Server が実行されているサーバーの外部にあるテーブルのことです。 分散クエリでは、1 つ以上のリモート テーブルにアクセスします。

### <a name="ole-db-provider-categories"></a>OLE DB プロバイダーのカテゴリ

以下は、SQL Server 分散クエリ実行の観点から、OLE DB プロバイダーを機能に基づいて分類したものです。 定義されているように、これらは相互に排他的ではありません。特定のプロバイダーが以下の複数のカテゴリに属することができます。

- SQL コマンド プロバイダー

- インデックス プロバイダー

- シンプル テーブル プロバイダー

- SQL 以外のコマンド プロバイダー

#### <a name="sql-command-providers"></a>SQL コマンド プロバイダー

`Command` オブジェクトをサポートし、SQL Server によって認識される SQL 標準言語を使用するプロバイダーが、このカテゴリに属します。 特定の OLE DB プロバイダーが SQL Server によって SQL コマンド プロバイダーとして扱われるための特定の要件は、次のとおりです。

- `Command` オブジェクトと、そのすべての必須 OLE DB インターフェイス (`ICommand`、`ICommandText`、`IColumnsInfo`、`ICommandProperties`、および `IAccessor`) をプロバイダーでサポートする必要があります。

- プロバイダーによってサポートされる SQL 言語は、少なくとも SQL Subminimum である必要があります。 その言語は、`DBPROP_SQLSUPPORT` プロパティを使用してプロバイダーによって報告される必要があります。

SQL コマンド プロバイダーの例として、Microsoft OLE DB Provider for SQL Server と Microsoft OLE DB Provider for ODBC があります。

#### <a name="index-providers"></a>インデックス プロバイダー

インデックス プロバイダーとは、OLE DB に従ってインデックスをサポートおよび公開し、インデックス ベースでベース テーブルを参照できるようにするプロバイダーです。 特定の OLE DB プロバイダーが SQL Server によってインデックス プロバイダーとして扱われるための特定の要件は、次のとおりです。

- TABLES、COLUMNS、INDEXES の各スキーマ行セットを含む `IDBSchemaRowset` インターフェイスをプロバイダーでサポートする必要があります。

- `IOpenRowset` を使用して (インデックス名および対応するベース テーブル名を指定することによって) インデックスに基づいて行セットを開くことを、プロバイダーでサポートする必要があります。

- `Index` オブジェクトによって、そのすべての必須インターフェイス (`IRowset`、`IRowsetIndex`、`IAccessor`、`IColumnsInfo`、`IRowsetInfo`、および `IConvertTypes`) がサポートされている必要があります。

- インデックス付きのベース テーブルに対して (`IOpenRowset` を使用して) 開かれた行セットでは、ブックマークに基づいて行に位置付けるための `IRowsetLocate` インターフェイスがサポートされている必要があります。

OLE DB プロバイダーが上記の要件を満たしている場合、ユーザーは `Index As Access Path` プロバイダー オプションを設定して、SQL Server がプロバイダーのインデックスを使用してクエリを評価できるようにすることができます。 既定では、このオプションが設定されない限り、SQL Server でプロバイダーのインデックスは使用されません。

>[!NOTE]
>SQL Server では、SQL Server から OLE DB プロバイダーへのアクセス方法に影響するさまざまなオプションがサポートされています。 SQL Server Enterprise Manager の `Linked Server Properties` ダイアログ ボックスを使用して、これらのオプションを設定できます。

#### <a name="simple-table-providers"></a>シンプル テーブル プロバイダー

`IOpenRowset` インターフェイスを介してベース テーブルに対して行セットを開くことを公開するプロバイダーです。 このようなプロバイダーは、SQL コマンド プロバイダーでもインデックス プロバイダーでもありません。そうではなく、SQL Server 分散クエリで使用できる最もシンプルなプロバイダーのクラスです。

このようなプロバイダーに対して、SQL Server によるテーブル スキャンは分散クエリの評価中にのみ実行できます。

#### <a name="non-sql-command-providers"></a>SQL 以外のコマンド プロバイダー

`Command` オブジェクトとその必須インターフェイスをサポートしているが、SQL Server によって認識される SQL 標準言語をサポートしていないプロバイダーは、このカテゴリに分類されます。

SQL 以外のコマンド プロバイダーの 2 つの例として、Microsoft OLE DB Provider for Indexing Service と、[Microsoft OLE DB Provider for Microsoft Active Directory Service](../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md) があります。

### <a name="transact-sql-subset"></a>Transact-SQL サブセット

必須の OLE DB インターフェイスをプロバイダーでサポートしている場合、次の各クラスの Transact-SQL ステートメントが分散クエリ用にサポートされます。

- リモート テーブルを対象テーブルとする `SELECT` INTO ステートメントを除き、すべての `SELECT` ステートメントを使用できます。

- 挿入に必要なインターフェイスをプロバイダーでサポートしている場合は、リモート テーブルに対して `INSERT` ステートメントを使用できます。 INSERT の OLE DB 要件の詳細については、この記事で後述する「\"INSERT ステートメント\"」を参照してください。

- プロバイダーが、指定されたテーブルに対する OLE DB インターフェイス要件を満たしている場合、リモート テーブルに対して `UPDATE` ステートメントと DELETE ステートメントを使用できます。 リモート テーブルを更新または削除できる OLE DB インターフェイスの要件と条件については、この記事で後述する「\"UPDATE ステートメントと DELETE ステートメント\"」を参照してください。

### <a name="cursor-support"></a>カーソルのサポート

必要な OLE DB 機能をプロバイダーでサポートしている場合は、分散クエリに対してスナップショット カーソルとキーセット カーソルの両方がサポートされます。 動的カーソルは、分散クエリに対してはサポートされていません。 分散クエリに対する動的カーソルのユーザー要求は、キーセット カーソルにダウングレードされます。

スナップショット カーソルはカーソルを開いたときに設定され、結果セットは変更されません。基になるテーブルに対する更新、挿入、削除は、カーソルに反映されません。

キーセット カーソルはカーソルを開いたときに設定され、結果セットはカーソルの有効期間全体にわたって未変更のままです。 ただし、基になるテーブルに対する更新と削除は、行がアクセスされるときにカーソル内で参照可能になります。 カーソルのメンバーシップに影響する可能性がある基になるテーブルへの挿入は、参照可能になりません。

リモート テーブルに対する更新および削除の条件をプロバイダーが満たしている場合は、分散クエリ上で定義されてリモート テーブルを参照するカーソルによって、リモート テーブルを更新または削除できます (たとえば、テーブルの `UPDATE` \| DELETE `<remote-table>` `WHERE` CURRENT OF `<cursor-name>`)。 詳細については、この記事で後述する「\"UPDATE ステートメントと DELETE ステートメント\"」を参照してください。

#### <a name="keyset-cursor-support-requirements"></a>キーセット カーソルのサポート要件

キーセット カーソルは、Transact-SQL 構文のすべての要件が満たされていて、次のいずれかが存在する場合に、分散クエリでサポートされます。

- OLE DB プロバイダーによって、すべてのリモート テーブル上の再利用可能なブックマークがクエリ内でサポートされている。 再利用可能なブックマークは、特定のテーブル上の行セットから使用でき、同じテーブルの別の行セット上で使用できます。 再利用可能なブックマークのサポートは、`IDBSchemaRowset` の TABLES_INFO スキーマ行セットを使用して、BOOKMARK_DURABILITY 列を BMK_DURABILITY_INTRANSACTION またはより高い持続性に設定することによって示されます。

- すべてのリモート テーブルで `IDBSchemaRowset` インターフェイスの INDEXES 行セットを通じて一意のキーが公開されている。 UNIQUE 列が VARIANT_TRUE に設定されたインデックス エントリが必要です。

キーセット カーソルは、*OpenQuery* 関数を含む分散クエリに対してはサポートされていません。

#### <a name="updatable-keyset-cursor-requirements"></a>更新可能なキーセット カーソルの要件

リモート テーブルは、分散クエリで定義されたキーセット カーソルを使用して更新または削除できます (たとえば、`UPDATE` \| DELETE `<remote-table>` `WHERE` CURRENT OF `<cursor-name>`)。 次に、更新可能なカーソルが分散クエリに対して許可される条件を示します。

- 更新可能なカーソルは、プロバイダーがリモート テーブルに対する更新と削除の条件も満たしている場合に許可されます。 詳細については、この記事で後述する「\"UPDATE ステートメントと DELETE ステートメント\"」を参照してください。

- すべての更新可能なキーセット カーソル操作は、読み取り繰り返し可能の分離レベルまたはそれより高い分離レベルを持つユーザー定義のトランザクション内に存在する必要があります。 さらに、プロバイダーで、`ITransactionJoin` インターフェイスを使用して分散トランザクションをサポートする必要があります。

## <a name="ole-db-provider-interaction-phases"></a>OLE DB プロバイダーの相互作用フェーズ

 すべての分散クエリの実行シナリオに共通する 6 つの操作があります。

- 接続の確立およびプロパティ取得の操作では、SQL Server が OLE DB プロバイダーに接続する方法と、使用されるプロバイダーのプロパティを示します。

- テーブル名の解決およびメタデータ取得操作では、SQL Server によってリモート テーブル名 (リンク サーバー ベースの名前またはアドホック名という 2 つの方法のいずれかで指定) がどのようにプロバイダー内の適切なデータ オブジェクトに解決されるかを示します。 これには、分散クエリをコンパイルおよび最適化するためにプロバイダーから SQL Server に取得されるテーブル メタデータも含まれます。

- トランザクション管理操作では、OLE DB プロバイダーとのトランザクションに関連したすべての操作を指定します。

- データ型の処理操作では、分散クエリの処理中に SQL Server で OLE DB プロバイダーからデータを使用するとき、または OLE DB プロバイダーにデータをエクスポートするときに、SQL Server によって OLE DB データ型がどのように処理されるかを示します。

- エラー処理操作では、SQL Server がプロバイダーからの拡張エラー情報を使用する方法を示します。

- セキュリティ操作では、SQL Server のセキュリティとプロバイダーのセキュリティがどのように相互作用するかを指定します。

### <a name="connection-establishment-and-property-retrieval"></a>接続の確立とプロパティの取得

SQL Server では 2 つのリモート データ オブジェクト名前付け規則がサポートされています。リンク サーバー ベースの 4 部構成の名前と、`OPENROWSET` 関数を使用したアドホック名です。

#### <a name="linked-server-based-names"></a>リンク サーバー ベースの名前

リンク サーバーは、OLE DB データ ソースに対する抽象化として機能します。 リンク サーバー ベースの名前は 4 部構成の名前で、形式は、`<linked-server>.<catalog>`. `<schema>.<object>` (`<linked-server>` はリンク サーバーの名前) です。 SQL Server では、`<linked-server>` を解釈することで、OLE DB プロバイダーと、そのプロバイダーに対してデータ ソースを識別する接続属性が派生されます。 名前を構成する他の 3 つの部分は、特定のリモート テーブルを識別するために、OLE DB データ ソースによって解釈されます。 :::

#### <a name="ad-hoc-names"></a>アドホック名

アドホック名は、`OPENROWSET` 関数または `OPENDATASOURCE` 関数に基づく名前です。 これには、分散クエリでリモート テーブルが参照されるたびに、すべての接続情報 (使用する OLE DB プロバイダー、データ ソースを識別するために必要な属性、ユーザー ID、パスワード) が含まれます。

既定では、sysadmin ロールのメンバーを除き、アドホック名を使用することはできません。 OLE DB プロバイダーに対してアドホック名を使用するには、プロバイダー オプション `DisallowAdhocAccess` を `0` に設定する必要があります。

リンク サーバー名が使用されている場合、SQL Server によって、リンク サーバーの定義から OLE DB プロバイダー名とプロバイダーの初期化プロパティが抽出されます。 アドホック名が使用されている場合は、同じ情報が `OPENROWSET` 関数の引数から SQL Server によって抽出されます。

4 部構成の名前とアドホック名ベースの構文を使用してリンク サーバーを設定する方法の詳細については、「[リンク サーバーの作成](create-linked-servers-sql-server-database-engine.md)」を参照してください。

### <a name="connecting-to-an-ole-db-provider"></a>OLE DB プロバイダーへの接続

次に示すのは、SQL Server から OLE DB プロバイダーへの接続時に SQL Server によって実行される手順の概要です。

1. SQL Server によってデータ ソース オブジェクトが作成されます。

   SQL Server で、プロバイダーの `ProgID` を使用して、そのプロバイダーのデータ ソース オブジェクト (DSO) がインスタンス化されます。 ProgID では、リンク サーバー構成の `provider_name` パラメーターとして指定するか、アドホック名の場合は `OPENROWSET` 関数の最初の引数として指定します。

   SQL Server で、OLE DB サービス コンポーネント インターフェイス `IDataInitialize` を使用して、プロバイダーの DSO がインスタンス化されます。 これにより、サービス コンポーネント マネージャーで、プロバイダーのネイティブ機能を上回る、スクロールや更新のサポートなどのサービスを集約できます。 さらに、`IDataInitialize` を使用してプロバイダーをインスタンス化すると、OLE DB サービス コンポーネントでプロバイダーへの接続をプールできるようになり、接続と初期化のオーバーヘッドの一部が減少します。

   特定のプロバイダーを SQL Server と同じプロセスで、または独自のプロセスでインスタンス化されるように構成できます。 別のプロセスでインスタンス化すると、SQL Server のプロセスがプロバイダーでのエラーから保護されます。 同時に、SQL Server からプロセス外の OLE DB 呼び出しをマーシャリングすることに関連したパフォーマンスのオーバーヘッドが発生します。 `Allow In Process` プロバイダー オプションを設定することにより、プロバイダーをプロセス内またはプロセス外でインスタンス化されるように構成できます。 詳細については、[プロバイダーのオプションの設定](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)に関する記事を参照してください。

   OLE DB サービス コンポーネントとセッション プールの詳細については、プロバイダーの要件に関する OLE DB のドキュメントを参照してください。

2. データ ソースが初期化されます。

   DSO が作成された後、サーバー構成オプション `remote login timeout` が 0 よりも大きい場合は、`IDBProperties` インターフェイスによって DBPROP_INIT_TIMEOUT 初期化プロパティが設定されます。これは必須プロパティです。

   これらのプロパティが設定されるのは、リンク サーバー定義において、または `OPENROWSET` 関数の 2 番目の引数において、指定されているか暗黙的に示されている場合です。

   - `DBPROP_INIT_PROVIDERSTRING`

   - `DBPROP_INIT_DATASOURCE`

   - `DBPROP_INIT_LOCATION`

   - `DBPROP_INIT_CATALOG`

   - `DBPROP_AUTH_USERID`

   - `DBPROP_AUTH_PASSWORD`

   これらのプロパティが設定された後、指定されたプロパティを使用して DSO を初期化するために、`IDBInitialize::Initialize` が呼び出されます。

3. SQL Server によってプロバイダー固有の情報が収集されます。

   SQL Server によって、分散クエリ評価で使用されるいくつかのプロバイダー プロパティが収集されます。これらのプロパティは、`IDBProperties::GetProperties` を呼び出すことによって取得されます。 これらのプロパティはすべてオプションです。ただし、関連するすべてのプロパティをサポートすることで、SQL Server がプロバイダーの機能を最大限に活用できるようになります。 たとえば、SQL Server からプロバイダーにクエリを送信できるかどうかを判別するには、`DBPROP_SQLSUPPORT` が必要です。 このプロパティがサポートされていない場合、SQL Server ではリモート プロバイダーが (SQL コマンド プロバイダーであったとしても) SQL コマンド プロバイダーとして使用されません。 次の表の「既定値」列は、プロパティがプロバイダーでサポートされていない場合に、SQL Server によって想定される値を示しています。

プロパティ| 既定値| 新しく使用する機能 |
|:----|:----|:----|
|`DBPROP_DBMSNAME`|なし|エラー メッセージに使用されます。|
|`DBPROP_DBMSVER` |なし|エラー メッセージに使用されます。|
|`DBPROP_PROVIDERNAME`|なし|エラー メッセージに使用されます。|
|`DBPROP_PROVIDEROLEDBVER1`|1.5|2\.0 機能が使用できるかどうかを判別するために使用されます。
|`DBPROP_CONCATNULLBEHAVIOR`|なし|プロバイダーの `NULL` 連結動作が SQL Server の動作と同じかどうかを判別するために使用されます。|
|`DBPROP_NULLCOLLATION`|なし|`NULLCOLLATION` が SQL Server インスタンスの null 照合順序の動作と一致する場合にのみ、並べ替え/インデックス使用を許可します。|
|`DBPROP_OLEOBJECTS`|なし|ラージ データ オブジェクト列用の構造化ストレージ インターフェイスをプロバイダーがサポートしているかどうかを判別します。|
|`DBPROP_STRUCTUREDSTORAGE`|なし|ラージ オブジェクト型に対して、(`ILockBytes`、`Istream`、および `ISequentialStream` のうち) どの構造化ストレージ インターフェイスがサポートされているかを判別します。|
|`DBPROP_MULTIPLESTORAGEOBJECTS`|False|複数のラージ オブジェクト列を同時に開くことができるかどうかを判別します。|
|`DBPROP_SQLSUPPORT`|なし|SQL クエリをプロバイダーに送信できるかどうかを判別します。|
|`DBPROP_CATALOGLOCATION`|`DBPROPVAL_CL_START`|マルチパート テーブル名を作成するために使用されます。
|`SQLPROP_DYNAMICSQL`|False|SQL Server 固有のプロパティ: `VARIANT_TRUE` が返された場合は、パラメーター化クエリの実行で `?` パラメーター マーカーがサポートされることを示します。
|`SQLPROP_NESTEDQUERIES`|False|SQL Server 固有のプロパティ: `VARIANT_TRUE` が返された場合、`FROM` 句内の入れ子になった `SELECT` ステートメントをプロバイダーでサポートしていることを示します。
|`SQLPROP_GROUPBY`|False|SQL Server 固有のプロパティ: `VARIANT_TRUE` が返された場合、SQL-92 標準の指定どおりに `SELECT` ステートメント内の GROUP BY 句をプロバイダーでサポートしていることを示します。
|`SQLPROP_DATELITERALS `|False|SQL Server 固有のプロパティ: `VARIANT_TRUE` が返された場合、SQL Server Transact-SQL 構文に従って datetime リテラルをプロバイダーでサポートしていることを示します。
|`SQLPROP_ANSILIKE `|False|SQL Server 固有のプロパティ: このプロパティは、SQL の最小限のレベルをサポートするプロバイダーにとって重要です。このプロパティでは、`LIKE` 演算子が SQL-92 エントリ レベル (ワイルドカード文字としての \'%\' および \'_\') に従ってサポートされています。
|`SQLPROP_SUBQUERIES `|False|SQL Server プロパティ:このプロパティは、SQL の最小限のレベルをサポートするプロバイダーで重要です。 このプロパティは、プロバイダーが SQL-92 エントリ レベルで指定されたサブクエリをサポートしていることを示します。 これには、相関サブクエリ、`IN`、`EXISTS`、`ALL`、および `ANY` 演算子をサポートする、`SELECT` リスト内および `WHERE` 句内でのサブクエリが含まれます。
|`SQLPROP_INNERJOIN`|False|SQL Server 固有のプロパティ: このプロパティは、SQL の最小限のレベルをサポートするプロバイダーにとって重要です。 このプロパティは、`FROM` 句での複数のテーブルを使用した結合のサポートを示します。 ------ ---

次の 3 つのリテラルが `IDBInfo::GetLiteralInfo` から取得されます。`DBLITERAL_CATALOG_SEPARATOR`、`DBLITERAL_SCHEMA_SEPARATOR` (カタログ、スキーマ、およびオブジェクト名の部分を指定して完全なオブジェクト名を構築するため)、`DBLITERAL_QUOTE` (プロバイダーに送信される SQL クエリで識別子名を引用するため)。

プロバイダーで区切りリテラルがサポートされていない場合、SQL Server ではピリオド (.) が既定の区切り文字として使用されます。 プロバイダーでカタログ区切り文字だけがサポートされ、スキーマ区切り文字がサポートされていない場合、SQL Server では、カタログ区切り文字がスキーマ区切り文字としても使用されます。 プロバイダーで `DBLITERAL_QUOTE` がサポートされていない場合、SQL Server では引用記号として単一引用符 (`'`) が使用されます。

>[!NOTE]
>プロバイダーの名前の区切りリテラルがこれらの既定値と一致しない場合、4 つの部分で構成される名前を使用して SQL Server からテーブルにアクセスするためには、プロバイダーによってそれらの区切りリテラルが `IDBInfo` を使用して公開されている必要があります。 これらのリテラルが公開されていない場合、そのようなプロバイダーに対してはパススルー クエリのみを使用できます。

`SQLPROP_DYNAMICSQL` および `SQLPROP_NESTEDQUERIES` プロパティを公開する方法の詳細については、「[SQL Server 固有のプロパティ](#appendixc)」を参照してください。

### <a name="table-name-resolution-and-meta-data-retrieval"></a>テーブル名の解決とメタデータ取得

SQL Server では、分散クエリ内の指定されたリモート テーブル名が、OLE DB データ ソース内の特定のテーブルまたはビューに解決されます。 リンク サーバー ベースとアドホック命名スキームは両方とも、プロバイダーによって解釈される、3 つの部分で構成される名前になります。 リンク サーバー ベースの名前の場合、4 つの部分で構成される名前の最後の 3 つの部分は、カタログ、スキーマ、およびオブジェクトの名前を形成します。 アドホック名の場合、`OPENROWSET` 関数の 3 番目の引数に、カタログ名、スキーマ名、およびオブジェクト名を定義する 3 つの部分で構成される名前を指定します。 カタログ名とスキーマ名の一方または両方を空にすることができます (4 つの部分で構成される名前は、カタログ名とスキーマ名が空の場合、`<server-name>...<object-name>` のようになります)。このような場合、SQL Server では、スキーマ行セット テーブル内で検索する対象の対応する値として、`NULL` が使用されます。

SQL Server によって適用される名前解決規則およびメタデータ取得手順は、プロバイダーで `Session` オブジェクトに対する `IDBSchemaRowset` インターフェイスがサポートされているかどうかによって異なります。

`IDBSchemaRowset` がサポートされている場合は、`TABLES`、`COLUMNS`、`INDEXES`、`TABLES_INFO` の各スキーマ行セットが `IDBSchemaRowset` インターフェイスから使用されます (`TABLES_INFO` スキーマ行セットは OLE DB 2.0 で定義されています)。SQL Server では、`IDBSchemaRowset` インターフェイスによって返されたスキーマ行セットを制約して、指定されたリモート テーブル名の部分に一致するスキーマ行を検索します。 次に、スキーマ行セットに対する、プロバイダーによってサポートされる制約に関連した規則と、それらを使用してリモート テーブルのメタデータが SQL Server で取得される方法について説明します。

- `TABLE_NAME` および `COLUMN_NAME` 列に対する制約は、常に必須です。

- プロバイダーで `TABLE_CATALOG` (または `TABLE_SCHEMA`) がサポートされている場合、SQL Server では `TABLE_CATALOG` (または `TABLE_SCHEMA`) に対してその制約が使用されます。 リモート テーブル名にカタログ (またはスキーマ) 名が指定されていない場合、対応する制約の値として `NULL` 値が使用されます。 カタログ (またはスキーマ) 名が指定されている場合、`TABLE_CATALOG` (または `TABLE_SCHEMA`) での対応する制約がプロバイダーによってサポートされている必要があります。

- `TABLE_SCHEMA` 列に対する制約は、プロバイダーによって `COLUMNS` と `TABLES` の両方でサポートされているか、どちらでもサポートされていない必要があります。 カタログ名の制約は、プロバイダーによって `TABLES` と `COLUMNS` の両方の行セットに対してサポートされているか、どちらに対してもサポートされていない必要があります。

- INDEXES に対して何らかの制約がサポートされている場合、スキーマの制約は、プロバイダーによって `TABLES` と INDEXES の両方に対してサポートされているか、どちらに対してもサポートされていない必要があります。カタログ名の制約は、プロバイダーによって `XES or support them on neither. The provider must either support catalog name restriction on both `TABLES` and ` と INDEXES` の両方の行セットに対してサポートされているか、どちらに対してもサポートされていない必要があります。

上記の規則に従って制約を設定することで、`TABLES` スキーマ行セットから `TABLE_CATALOG`、`TABLE_SCHEMA`、`TABLE_NAME`、`TABLE_TYPE`、`TABLE_GUID` の各列が SQL Server によって取得されます。

`COLUMNS` スキーマ行セットからは、`TABLE_CATALOG`、`TABLE_SCHEMA`、`TABLE_NAME`、`COLUMN_NAME`、`COLUMN_GUID`、`ORDINAL_POSITION`、`COLUMN_FLAGS`、`IS_NULLABLE`、`DATA_TYPE`、`TYPE_GUID`、`CHARACTER_MAXIMUM_LENGTH`、`NUMERIC_PRECISION`、`NUMERIC_SCALE` の各列が SQL Server によって取得されます。 `COLUMN_NAME`、`DATA_TYPE`、`ORDINAL_POSITION` からは、null 以外の有効な値が返される必要があります。 `DATA_TYPE` が `DBTYPE_NUMERIC` または `DBTYPE_DECIMAL` の場合、対応する `NUMERIC_PRECISION` と `NUMERIC_SCALE` は null 以外の有効な値である必要があります。

前の規則に従って制約を設定することで、オプションの `INDEXES` スキーマ行セットから、指定されたリモート テーブルのインデックスが SQL Server によって検索されます。 見つかった一致するインデックス エントリから、`TABLE_CATALOG`、`TABLE_SCHEMA`、`TABLE_NAME`、`INDEX_CATALOG`、`INDEX_SCHEMA`、`INDEX_NAME`、`PRIMARY_KEY`、`UNIQUE`、`CLUSTERED`、`FILL_FACTOR`、`ORDINAL_POSITION`、`COLUMN_NAME`、`COLLATION`、`CARDINALITY`、`PAGES` の各列が SQL Server によって取得されます。

オプションの `TABLES_INFO` 行セットから、ブックマークのサポート、ブックマークの種類と長さなど、指定されたリモート テーブルに関する追加情報が SQL Server によって検索されます。 `TABLES_INFO` 行セットの `DESCRIPTION` 列を除くすべての列が使用されます。 `TABLES_INFO` 行セット内の情報は、次のように使用されます。

- `BOOKMARK_DURABILITY` 列は、より効率的なキーセット カーソルを実装するために使用されます。 この列の値が `BMK_DURABILITY_INTRANSACTION` またはより高い持続性の値である場合、SQL Server では、キーセット カーソルを実装するためにブックマーク ベースの取得とリモート テーブル行の更新が使用されます。

- `BOOKMARK_TYPE`、`BOOKMARK_DATA TYPE`、`BOOKMARK_MAXIMUM_LENGTH` の各列は、クエリのコンパイル時にブックマーク メタデータを判別するために使用されます。 これらの列がサポートされていない場合、SQL Server ではコンパイル時に `IOpenRowset` を使用してベース テーブルの行セットが開かれ、ブックマーク情報が取得されます。

`IDBSchemaRowset` がサポートされておらず、リモート テーブル名にカタログ名またはスキーマ名が含まれている場合、SQL Server によって `IDBSchemaRowset` が要求され、エラーが返されます。 ただし、カタログ名もスキーマ名も指定されていない場合、SQL Server では、リモート テーブルに対応する行セットが開かれ、行セット オブジェクトの必須 `IColumnsInfo` インターフェイスから列のメタデータが取得されます。

SQL Server では、`IOpenRowset::OpenRowset` を呼び出すことで、テーブルに対応する行セットが開かれます。 `OPENROWSET` に提供されるテーブル名は、カタログ、スキーマ、およびオブジェクト名の各部分から構築されます。

- 名前の各部分 (`catalog`、`schema`、`object name`) は、プロバイダーの引用記号 (`DBLITERAL_QUOTE`) で囲まれてから、それらの間に `DBLITERAL_CATALOG_SEPARATOR` 文字と `DBLITERAL_SCHEMA_SEPARATOR` 文字が埋め込まれて連結されます。 名前の構築は、`IOpenRowset` 内の OLE DB 規則に従います。

- テーブルの列メタデータは、行セット オブジェクトが開かれた後に、`IColumnsInfo::GetColumnInfo` によって取得されます。

`IDBSchemaRowset` が TABLES、COLUMNS、TABLES_INFO 行セットでサポートされていない場合、SQL Server によってベース テーブルに対して行セットが 2 回開かれます。1 回はクエリのコンパイル時で、メタデータが取得されます。もう 1 回はクエリ実行時です。 行セットを開くことにより副作用が発生するプロバイダー (たとえば、リアルタイム デバイスの状態を変更するコードを実行する、電子メールを送信する、任意のユーザー提供コードを実行するなど) では、この動作を認識しておく必要があります。

### <a name="statistics-retrieval"></a>統計情報の取得

プロバイダーでベース テーブルの分布統計をサポートしている場合、SQL Server ではこれらの統計が使用されます。 SQL Server クエリ プロセッサには、次の 2 種類の統計情報が必要です。

- **列 (または組) のカーディナリティ**。 これは、テーブルの 1 つの列 (または列の組み合わせ) 内にある一意の値の数です。 これを使用して、列に対する述語の選択度を見積もることができます。 分布統計をサポートするプロバイダーでは、少なくとも 1 種類のカーディナリティがサポートされている必要があります。

- **ヒストグラム**。 値の分布が一様でない場合、 一意の値の数は、述語の選択度を正確に見積もるためには不十分です。 この場合、ヒストグラムを使用して、テーブル内の列の値の分布に関するより詳細な情報を提供できます。

統計を使用できるようにすることで、SQL Server クエリ オプティマイザーは、クエリ内の中間操作のカーディナリティをより正確に推定できるようになります。これにより、クエリの実行プランがより適切に生成されます。

OLE DB プロバイダーでは、次のように分布統計がサポートされている必要があります。

- **必須**。 (1) と (2) のプロパティをサポートします。(1) 列または組のカーディナリティがサポートされているかどうか、およびヒストグラムがサポートされているかどうかを示す `DBPROP_TABLESTATISTICS` と、(2) `DBPROPVAL_ORS_HISTOGRAM` ビットを使用して、ヒストグラムがサポートされているかどうかを示す `DBPROP_OPENROWSETSUPPORT`。

- **必須**。 `TABLE_STATISTICS` スキーマ行セット。 `TABLE_STATISTICS` スキーマ行セットでは、指定したデータベースで使用可能な統計が一覧表示されます。 また、スキーマ行セット自体に列と組のカーディナリティが含まれており、特定の列でヒストグラムがサポートされているかどうかを示しています。 SQL Server で統計が使用されるためには、このスキーマ行セット内に列 `TABLE_NAME`、`STATISTICS_NAME`、`STATISTICS_TYPE`、`COLUMN_NAME`、`ORDINAL_POSITION` が必須です。 `COLUMN_CARDINALITY` または `TUPLE_CARDINALITY` の少なくとも 1 つは必須です。 ヒストグラムをサポートする場合には、`NO_OF_RANGES` も必須です。

- **オプション**。 必要に応じて、プロバイダーでヒストグラムをサポートする場合は、対応する統計の `DBID` を指定してヒストグラムの行セットを開くことができるようにする、`IOpenRowset::OpenRowset` メソッドの拡張機能をサポートする必要があります。

統計インターフェイスの詳細については、OLE DB 2.6 の仕様を参照してください。

### <a name="constraints"></a>制約

また、OLE DB プロバイダーで OLE DB 2.6 のスキーマ行セットである `CHECK` をサポートしている場合、リモート データ ソース内のベース テーブルに定義されている `CHECK_CONSTRAINTS_BY_TABLE` 制約も、SQL Server クエリ オプティマイザーによって使用されます。 スキーマ行セットの `CHECK_CLAUSE` 列では、SQL-92 に準拠した構文で `CHECK` 句の述語を返す必要があります。 クエリ オプティマイザーでは、テーブルにチェック制約が存在するため、常に false であるか、常に true であることがわかっている述語を排除または簡略化するために、制約情報が使用されます。

### <a name="transaction-management"></a>トランザクション管理

SQL Server では、プロバイダーの `ITransactionLocal` (ローカル トランザクション用) および `ITransactionJoin` (分散トランザクション用) の各 OLE DB インターフェイスを使用することで、分散データへのトランザクション ベースのアクセスがサポートされます。 プロバイダーに対してローカル トランザクションを開始すると、SQL Server によってアトミック書き込み操作が保証されます。 SQL Server では、分散トランザクションを使用することにより、複数のノードに関係するトランザクションの結果 (コミットまたは中止) がすべてのノードで同じになるようにします。 プロバイダーで必要な OLE DB のトランザクション関連のインターフェイスをサポートしていない場合、ローカル トランザクション コンテキストによっては、そのプロバイダーに対する更新操作は許可されません。

次の表では、プロバイダーの機能とローカル トランザクション コンテキストを特定して、ユーザーが分散クエリを実行した場合の動作について説明します。 プロバイダーに対する読み取り操作では、`SELECT` ステートメントか、リモート テーブルが `SELECT INTO` の入力側に読み込まれるときは、`INSERT`、`UPDATE`、または `DELETE` ステートメントを参照します。 プロバイダーに対する書き込み操作では、リモート テーブルを対象とする `INSERT`、`UPDATE`、または `DELETE` ステートメントを参照します。

プロバイダーの機能とトランザクション コンテキストに基づく分散クエリの結果:

|分散クエリの発生|プロバイダーで `ITransactionLocal` をサポートしていない|プロバイダーで `ITransactionLocal` をサポートしているが、`ITransactionJoin` をサポートしていない|プロバイダーで `ITransactionLocal` と `ITransactionJoin` の両方をサポートしている|
|:-----|:-----|:-----|:-----|
| トランザクション内で、トランザクション自体によって (ユーザー トランザクションなし)。|既定では、読み取り操作のみが許可されます。 プロバイダー レベルのオプション `Nontransacted Updates` が有効になっている場合は、書き込み操作が許可されます (このオプションが有効になっている場合、SQL Server では、プロバイダーのデータに対する原子性と一貫性を保証できません。 これにより、書き込み操作の部分的な影響がリモート データ ソースに反映され、元に戻すことができなくなる可能性があります)。| すべてのステートメントがリモート データに対して許可されます。 キーセット カーソルは読み取り専用です。 ローカル トランザクションは、現在の SQL Server セッションの分離レベルを使用してプロバイダーで開始され、ステートメントの評価が正常に終了した時点でコミットされます (`SET TRANSACTION ISOLATION LEVEL` ステートメントを使用して変更されていない限り、SQL Server セッションの既定の分離レベルは `READ COMMITTED` です。 プロバイダーでは、要求される分離レベルをサポートしている必要があります)。 | すべてのステートメントを使用できます。 キーセット カーソルは読み取り専用です。 ローカル トランザクションは、現在の SQL Server セッションの分離レベルを使用してプロバイダーで開始され、ステートメントの評価が正常に終了した時点でコミットされます。 |
| ユーザー トランザクション内 (つまり、`BEGIN TRAN` または `BEGIN DISTRIBUTED TRAN` と `COMMIT` との間)。 | トランザクションの分離レベルが `READ COMMITTED` (既定値) 以下の場合は、読み取り操作が許可されます。 より高い分離レベルの場合、分散クエリは許可されません。 | 読み取り操作のみが許可されます。 現在の SQL Server セッションの分離レベルを使用して、新しい分散トランザクションがプロバイダーで開始されます。 |すべてのステートメントを使用できます。 新しい分散トランザクションは、現在の SQL Server セッションの分離レベルを使用してプロバイダーで開始され、ユーザー トランザクションのコミット時にコミットされます。 データ変更ステートメントの場合、既定では、分散トランザクションで入れ子になったトランザクションが SQL Server によって開始されます。これにより、データ変更ステートメントを、周囲のトランザクションを停止せずに特定のエラー条件下で停止させることができます。 `XACT_ABORT SET` オプションがオンの場合、SQL Server では、入れ子になったトランザクションのサポートは不要であり、データ変更ステートメントの実行中にエラーが発生した場合は、周囲のトランザクションを停止します。 |
|  |  |  |

### <a name="data-type-handling-in-distributed-queries"></a>分散クエリでのデータ型の処理

OLE DB プロバイダーでは、OLE DB で定義されたデータ型 (OLE DB の `DBTYPE` によって示される) に関連したデータを公開します。 SQL Server では、サーバー内部の外部データをネイティブ SQL Server 型として処理します。この結果、データが SQL Server によって消費されるか SQL Server によってエクスポートされるときに、OLE DB データ型から SQL Server ネイティブ型へのマッピング、およびその逆のマッピングがそれぞれ行われます。 このマッピングは、特に明記されていない限り、暗黙的に行われます。

分散クエリ内のデータ型は、次の 2 つのマッピング方法のいずれかを使用して処理されます。

- 消費側のマッピングでは、`SELECT` ステートメント内および INSERT、UPDATE、DELETE ステートメントの入力側にリモート テーブルが示されている場合、OLE DB のデータ型から SQL Server のネイティブ データ型に消費側で型がマッピングされます。

- エクスポート側のマッピングでは、`INSERT` または `UPDATE` ステートメントの対象テーブルとしてリモート テーブルが示されている場合、SQL Server データ型から OLE DB データ型にエクスポート側で型がマッピングされます。

SQL Server と OLE DB のデータ型マッピング テーブル。

| OLE DB 型 | `DBCOLUMNFLAG` | SQL Server データ型 |
|-----|-----|-----|
|`DBTYPE_I1`*| |`numeric(3, 0)`|
|`DBTYPE_I2`| |`smallint`|
|`DBTYPE_I4`| |`int`|
|`DBTYPE_I8`| |`numeric(19,0)`|
|`DBTYPE_UI1`| |`tinyint`|
|`DBTYPE_UI2`*| |`numeric(5,0)`|
|`DBTYPE_UI4`*| |`numeric(10,0)`|
|`DBTYPE_UI8`*| |`numeric(20,0)`|
|`DBTYPE_R4`| |`float`|
|`DBTYPE_R8`| |`real`|
|`DBTYPE_NUMERIC`| |`numeric`|
|`DBTYPE_DECIMAL`| |`decimal`|
|`DBTYPE_CY`| |`money`|
|`DBTYPE_BSTR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true`<br>内の複数の<br> 最大長 > 4000 文字|ntext|
|`DBTYPE_BSTR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true`|NCHAR|
|`DBTYPE_BSTR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=false`|NVARCHAR|
|`DBTYPE_IDISPATCH`| |エラー|
|`DBTYPE_ERROR`| |エラー|
|`DBTYPE_BOOL`| |`bit`|
|`DBTYPE_VARIANT`*| |NVARCHAR|
|`DBTYPE_IUNKNOWN`| |エラー|
|`DBTYPE_GUID`| |`uniqueidentifier`|
|`DBTYPE_BYTES`|`DBCOLUMNFLAGS_ISLONG=true` <br>内の複数の<br> 最大長 > 8000|`image`|
|`DBTYPE_BYTES`|`DBCOLUMNFLAGS_ISROWVER=true`、`DBCOLUMNFLAGS_ISFIXEDLENGTH=true`、列サイズ = 8 <br>内の複数の<br> 最大長は報告されない。 | `timestamp` |
|`DBTYPE_BYTES`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` | `binary` |
|`DBTYPE_BYTES`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` | `varbinary`|
|`DBTYPE_STR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` | `char`|
|`DBTYPE_STR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` | `varchar` |
|`DBTYPE_STR`| `DBCOLUMNFLAGS_ISLONG=true` <br>内の複数の<br> 最大長 > 8000 文字 <br>内の複数の<br>   最大長は報告されない。 | `text`|
|`DBTYPE_WSTR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` |`nchar`|
|`DBTYPE_WSTR` | `DBCOLUMNFLAGS_ISFIXEDLENGTH=false`|`nvarchar`|
|`DBTYPE_WSTR`| `DBCOLUMNFLAGS_ISLONG=true` <br>内の複数の<br> 最大長 > 4000 文字 <br>内の複数の<br>   最大長は報告されない。 | `ntext`|
|`DBTYPE_UDT`| |エラー|
|`DBTYPE_DATE`* | | `datetime` |
|`DBTYPE_DBDATE` | | `datetime` (明示的な変換が必要)|
|`DBTYPE_DBTIME`| | `datetime` (明示的な変換が必要)|
|`DBTYPE_DBTIMESTAMP`* | | `datetime`|
|`DBTYPE_ARRAY` | |エラー|
|`DBTYPE_BYREF` | | 無視 |
|`DBTYPE_VECTOR` | |エラー|
|`DBTYPE_RESERVED`| |エラー|

\* SQL Server 型の表記への何らかの形式の変換を示します。これは、SQL Server に正確な同等のデータ型がないためです。 このような変換によって、精度の損失、オーバーフロー、またはアンダーフローが生じる可能性があります。 対応するデータ型が SQL Server の将来のバージョンでサポートされた場合、既定の暗黙的なマッピングは将来変更される可能性があります。

>[!NOTE]
>`numeric(p,s)` は、精度が `p` で小数点以下桁数が `s` の SQL Server データ型 `numeric` を示しています。 `DBTYPE_NUMERIC` と `DBTYPE_DECIMAL` に許容される最大精度は 38 です。 プロバイダーは、アクセサーの作成時に `DBTYPE_BSTR` 列へのバインディングを `DBTYPE_WSTR`としてサポートする必要があります。 `DBTYPE_VARIANT` 列は、Unicode 文字列 `nvarchar` として使用されます。 これには、プロバイダーから`DBTYPE_VARIANT`へ`DBTYPE_WSTR`の変換がサポートされている必要があります。 プロバイダーは、OLE DB で定義されているように、この変換を実装することが想定されています。 詳細については、[OLE DB 仕様のデータ型](#appendixa)を参照してください。

#### <a name="interpreting-data-type-mapping"></a>データ型マッピングの解釈

SQL Server 型へのマッピングは、OLE DB データ型と、列またはスカラー値を記述する DBCOLUMNFLAGS 値によって決まります。 `COLUMNS` スキーマ行セットの場合、`COLUMN_FLAGS` 列と `DATA_TYPE` 列でこれらの値を表します。 `IColumnsInfo::GetColumnInfo` インターフェイスの場合、`DBCOLUMNINFO` 構造体の `wType` メンバーと `dwFlags` メンバーでこの情報を表します。

特定の `DBTYPE` および `DBCOLUMNFLAG` 値を持つ特定の列に対して消費側マッピングを使用するには、テーブル内で対応する SQL Server 型を探します。 式に含まれるリモート テーブルの列の型の規則は、次の単純な規則によって記述できます。

>テーブル内の対応するマップされた SQL Server 型が同じコンテキストで有効である場合、Transact-SQL 式では、指定されたリモート列の値が有効です。

テーブルとルールでは、次のものが定義されます。

- 比較と式。

一般に、`X <op> <remote-column>` は、`<op>` が `X` のデータ型と `<remote-column>` のマップ先のデータ型で有効な演算子である場合に、有効な式です。

- 明示的な変換。

`Convert(X, <remote-column>)` は、`<remote-column>` の `DBTYPE` がネイティブ データ型である `Y` に (上の表に従って) マップされ、`Y` から `X` への明示的な変換が許可されている場合に使用できます。

ユーザーがリモート データを既定以外のネイティブ データ型に変換する場合は、明示的な変換を使用する必要があります。

リモート テーブルに対して `UPDATE` および `INSERT` ステートメントでエクスポート側マッピングを使用するには、ネイティブの SQL Server データ型を同じテーブルを使用して OLE DB データ型にマップします。 次のいずれかが存在する場合には、SQL Server 型である `S1` から特定の OLE DB 型 `T` へのマッピングが可能です。

- 対応するマッピングがマッピング テーブル内に直接見つかる。

- `S2` がマッピング テーブル内の型 `T` にマップされるように、`S1` から別の SQL Server 型 `S2` への暗黙的な変換が可能である。

#### <a name="large-object-lob-handling"></a>ラージ オブジェクト (LOB) の処理

マッピング テーブルに示されているように、`DBTYPE_STR`、`DBTYPE_WSTR`、`DBTYPE_BSTR` 型の列でも `DBCOLUMNFLAGS_ISLONG` が報告される場合、または最大長が 4,000 文字を超えている場合 (または最大長が報告されない場合)、SQL Server ではそれらを必要に応じて `text` または `ntext` として扱います。 同様に、`DBTYPE_BYTES` 列の場合、`DBCOLUMNFLAGS_ISLONG` が設定されているか、最大長が 8,000 バイトを超えている場合 (または最大長が報告されない場合)、列は `image` 列として扱われます。 `Text`、`ntext`、`image` の各列は、LOB 列と呼ばれます。

SQL Server では、OLE DB プロバイダーの LOB に対してテキストとイメージのフル機能は公開されません。 `TEXTPTRS` は、OLE DB プロバイダーのラージ オブジェクトに対してサポートされていません。そのため、関連する機能はどれもサポートされません (たとえば、`TEXTPTR` システム関数や、`READTEXT`、`WRITETEXT`、`UPDATETEXT` の各ステートメント)。 LOB 列全体を取得する `SELECT` ステートメントは、リモート テーブル内のラージ オブジェクト列全体に対する `UPDATE` および `INSERT` ステートメントと同様に、サポートされています。

プロバイダーでサポートされている場合、SQL Server では LOB 列に対して、構造化ストレージ インターフェイスを使用します。 構造化ストレージ インターフェイスは、優先順位と機能の低い方から、`ISequentialStream`、`Istream`、または `ILockBytes` となります。 これらのインターフェイスが 1 つ以上サポートされている場合、プロバイダーでは、`IDBProperties` インターフェイスを使用してクエリが実行されたときに、`DBPROP_OLEOBJECTS` プロパティの値として DBPROPVAL_OO_BLOB を返す必要があります。 また、プロバイダーでは、サポートしているインターフェイスに対するサポートを `DBPROP_STRUCTUREDSTORAGE` プロパティで示す必要があります。

LOB 列の構造化ストレージ インターフェイスをプロバイダーがサポートしていない場合、SQL Server では、このインターフェイスを独自に具体化し、`text`、`ntext`、または `image` 列として公開します。

#### <a name="accessing-lob-columns"></a>LOB 列へのアクセス

プロバイダーが構造化ストレージ インターフェイスのいずれかをサポートしている場合、SQL Server では次の手順を実行してクエリの実行中に LOB 列を取得します。

1. SQL Server では、`IOpenRowset::OpenRowset` を使用して行セットを開く前に、ラージ オブジェクト列について 1 つ以上の構造化ストレージ インターフェイス (`ISequentialStream`、`Istream`、`ILockBytes`) のサポートを要求します。 プロバイダーでサポートされている 1 つ目のインターフェイスは必須です。追加のインターフェイスは、対応する DBPROP 構造体の *dwOptions* 要素を DBPROPOPTIONS_SETIFCHEAP に設定することによって、\"低コストの場合は設定される\" ものとして要求されます。 たとえば、プロバイダーで `ISequentialStream` と `ILockBytes` の両方をサポートしている場合、`ISequentialStream` は必須であり、`ILockBytes` は、\"低コストの場合は設定される\" ものとして要求されます。

4. 行セットが開かれた後、SQL Server では `IRowsetInfo::GetProperties` を使用して、行セットで使用可能な実際のインターフェイスを識別します。 プロバイダーから返された最後の、つまり最も適したインターフェイスが使用されます。 SQL Server でラージ オブジェクト列に対してアクセサーを作成するとき、その列はインターフェイスに設定されたバインディングの DBOBJECT 構造体の *iid* 要素を使用して、DBTYPE_IUNKNOWN としてバインドされます。

#### <a name="reading-from-lob-columns"></a>LOB 列からの読み取り

ラージ オブジェクト列から読み取るには、`IRowset::GetData` から行バッファーに返される、要求された構造化ストレージ インターフェイスのインターフェイス ポインターを使用します。 プロバイダーが同時に複数の開かれた LOB をサポートしていない場合 (つまり、`DBPROP_MULTIPLE_STORAGEOBJECTS` をサポートしていない場合)、および行に複数のラージ オブジェクト列がある場合、SQL Server では LOB 列がローカル作業テーブルにコピーされます。

#### <a name="update-and-insert-statements-on-lob-columns"></a>LOB 列に対する `UPDATE` ステートメントと `INSERT` ステートメント

SQL Server では、プロバイダーが提供するインターフェイスを使用してストレージ オブジェクトを変更するのではなく、新しいストレージ オブジェクトへのポインターをプロバイダーに渡します。 LOB 列ごとに、ストレージ オブジェクトに対して更新または挿入される値が、選択した構造化ストレージ インターフェイスを使用して作成されます。 `UPDATE` 操作であるか `INSERT` 操作であるかに応じて、ストレージ オブジェクトへのポインターが、`IRowsetChange::SetData` または `IRowsetChange::InsertRow` をそれぞれ使用してプロバイダーに渡されます。

### <a name="error-handling"></a>エラー処理

OLE DB プロバイダーに対する特定のメソッド呼び出しによってエラー コードが返されると、SQL Server エラー状態に関する情報をユーザーに返す前に、プロバイダーの拡張エラー情報が検索されます。

SQL Server では、OLE DB で指定された OLE DB エラー オブジェクトが使用されます。 大まかな手順の一部を次に示します。

1. メソッドの呼び出しによってプロバイダーからエラー コードが返されると、SQL Server によって `ISupportErrorInfo` インターフェイスが検索されます。 このインターフェイスがサポートされている場合、SQL Server では、`ISupportErrorInfo::InterfaceSupportsErrorInfo` を呼び出して、エラー コードを生成したインターフェイスによってエラー オブジェクトがサポートされているかどうかを確認します。

<!-- -->

5. インターフェイスによってエラー オブジェクトがサポートされている場合、SQL Server では、`GetErrorInfo` 関数を呼び出して、現在のエラー オブジェクトの `IErrorInfo` インターフェイス ポインターを取得します。

6. SQL Server により、`IErrorInfo` インターフェイスを使用して `IErrorRecords` インターフェイスへのポインターが取得されます。

7. SQL Server により、`IErrorRecords` を使用してオブジェクト内のすべてのエラー レコードがループ処理され、各レコードに対応するエラー メッセージ テキストが取得されます。

プロバイダーのエラー オブジェクトがどのように使用されるかについて詳しくは、OLE DB のドキュメントを参照してください。

### <a name="security"></a>Security

コンシューマーが OLE DB プロバイダーに接続するとき、コンシューマーが統合セキュリティ ユーザーとして認証されることを望まない限り、通常はプロバイダーによってユーザー ID とパスワードが要求されます。 分散クエリの場合、分散クエリを実行する SQL Server ログインの代わりに、SQL Server が OLE DB プロバイダーのコンシューマーとして機能します。 SQL Server により、現在の SQL Server ログインがリンク サーバー上のユーザー ID とパスワードにマップされます。

これらのマッピングは、ユーザーが特定のリンク サーバーに対して指定することができ、システム ストアド プロシージャである `sp_addlinkedsrvlogin` と `sp_droplinkedsrvlogin` によって設定および管理できます。 `IDBProperties::SetProperties` を使用して DBPROP_AUTH_USERID および DBPROP_AUTH_PASSWORD という初期化グループ プロパティを設定することにより、マッピングによって決定されるユーザー ID とパスワードが接続の確立時にプロバイダーに渡されます。

クライアントが Windows 認証を使用して SQL Server に接続し、ログインに `sp_addlinkedsrvlogin` を使用した `self` マッピングが設定されている場合、SQL Server では、クライアントのセキュリティ コンテキストを借用し、接続の確立時にプロバイダーに対して `DBPROP_AUTH_INTEGRATED` プロパティを設定しようとします。 この処理は "*委任*" と呼ばれます。

接続に使用するセキュリティ コンテキストが決定された後、このセキュリティ コンテキストの認証と、データ ソース内のデータ オブジェクトに対するそのコンテキストのアクセス許可のチェックは、完全に OLE DB プロバイダーに任されます。

詳細については、[`sp_addlinkedsrvlogin`](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) および [`sp_droplinkedsrvlogin`](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md) を参照してください。

## <a name="query-execution-scenarios"></a>クエリ実行のシナリオ

 分散クエリを評価するとき、次の 1 つまたは複数のシナリオで SQL Server と OLE DB プロバイダーのやり取りが行われます。

- リモート クエリ

- インデックス アクセス

- 純粋なテーブル スキャン

- `UPDATE` ステートメントと DELETE ステートメント

- `INSERT` ステートメント

- パススルー クエリ

### <a name="remote-query"></a>Remote Query

SQL Server によって、元のクエリの一部を評価する SQL クエリが生成されます。このクエリは、プロバイダーによって全体を評価できます。 このシナリオは、SQL コマンド プロバイダーに対してのみ可能です。 SQL クエリを生成することによって SQL Server からプロバイダーに操作がプッシュされる範囲は、プロバイダーがサポートする SQL 文法によって異なります。 プロバイダーでは、次の方法で SQL サポートのレベルを示す必要があります。

1. `DBPROP_SQLSUPPORT` プロパティを使用して、SQL の最小限、ODBC コア、または SQL-92 エントリ レベルのサポートを指定します。 SQL の最小限の構文レベルは、SQL Server でサポートされている新しいレベルで、これにより、SQL の単純なサブセットをサポートするシンプルなプロバイダーに SQL Server からリモート クエリを送信できます。 このレベルには、サブクエリを含まない、`FROM` 句に複数のテーブルを含まない (したがって結合がない)、および GROUP BY を含まない基本的な `SELECT` ステートメントが該当します。 これらの各構文レベルのプロバイダーに対してリモート クエリを生成するために SQL Server によって使用される SQL 文法のサブセットについては、「[リモート クエリの生成に使用される SQL サブセット](#appendixb)」を参照してください。

1. DBPROP_SQLSUPPORT によって報告される、構文レベルに含まれていない個々の SQL 機能のサポートを示すために、さまざまな SQL Server 固有のプロパティをサポートします。 プロパティの一覧と、各プロパティが SQL Server によってどのように使用されるかについては、このセクションで後述します。

SQL Server では、Transact-SQL 文字列内のパラメーター マーカーとして疑問符 (?) を指定して、パラメーター化クエリの実行が使用されます。 パラメーター化クエリの実行は、SQL Server、Microsoft Jet、および Oracle OLE DB プロバイダーに対して使用されます。 他のプロバイダーに対して、プロバイダーが `Command` オブジェクトで `ICommandWithParameters` をサポートし、次の条件のうち少なくとも 1 つが満たされている場合は、パラメーター化クエリの実行が使用されます。

- プロバイダーでは、`DBPROP_SQLSUPPORT` プロパティを使用して SQL Server サポートの ODBC コア レベルを示します。

- プロバイダーでは、`IDBPProperties` を使用して SQLPROP_DYNCMICSQL SQL Server 固有のプロパティをサポートすることによって、疑問符 (?) パラメーター マーカーのサポートを示します。 詳細については、プロバイダーのプロパティに関する次のセクションを参照してください。

- 管理者は、プロバイダーに対して `Dynamic Parameters` プロバイダー オプションを設定して、SQL Server でパラメーター化クエリを生成できるようにします。

リモートで実行される SQL テキストが SQL Server によって生成されるとき、`IDBInfo` インターフェイスの `DBLITERAL_QUOTE` リテラルによって報告される引用記号でテーブル名と列名が囲まれます。 このリテラルがサポートされていない場合、テーブル名と列名は引用記号で囲まれません。

プロバイダーでパラメーター化クエリの実行をサポートしている場合、SQL Server により、パラメーター化クエリの実行方法が考慮され、ローカル テーブルとリモート テーブルの結合が評価されます。 パラメーター化クエリは、ローカル テーブルの各行から生成されたパラメーター値に対して繰り返し実行されます。 この方法では、プロバイダーから取得される行の数を減らすことができ、少数の行を含むローカル テーブルを多数の行を含むリモート テーブルと結合する場合に便利です。 このリモート結合方法は、`REMOTE` 結合オプティマイザー ヒントによって適用できます。 パラメーター化クエリの実行の詳細については、「[方法: パラメーター化クエリを実行する](../../connect/php/how-to-perform-parameterized-queries.md)」を参照してください。

リモート クエリ シナリオにおけるプロバイダーに対する大まかな手順を次に示します。

1. SQL Server により、`IDBCreateCommand::CreateCommand` を使用して `Session` オブジェクトから `Command` オブジェクトが作成されます。

9. `Remote Query Timeout` サーバー構成オプションが 0 より大きい値に設定されている場合、SQL Server により、`Command` オブジェクトの `DBPROP_COMMANDTIMEOUT` プロパティが、`ICommandProperties::SetProperties` を使用して同じ値に設定されます。コマンド テキストを、生成された Transact-SQL 文字列に設定するために、`ICommand::SetCommandText` が呼び出される必要があります。

10. コマンドを準備するために、SQL Server によって `ICommandPrepare::Prepare` が呼び出されます。 プロバイダーでこのインターフェイスがサポートされていない場合、SQL Server の手順 4 に進みます。

11. 生成されたクエリがパラメーター化されている場合、SQL Server では、`ICommandWithParameters::SetParameterInfo` を使用してパラメーターを記述し、`IAccessor::CreateAccessor` を使用してパラメーターのアクセサーを作成します。

12. SQL Server によって `ICommand::Execute` が呼び出されて、コマンドが実行され、行セットが作成されます。

13. SQL Server では、`IRowset` インターフェイスを使用してテーブルの行を移動し、使用します。 行をフェッチするには `IRowset::GetNextRows`、行セットの先頭に位置変更するには `IRowset::RestartPosition`、行を解放するには `IRowset::ReleaseRows` を使用します。

#### <a name="provider-properties-of-interest-for-remote-query-execution"></a>リモート クエリの実行に関連するプロバイダー プロパティ

プロバイダーで、DBPROP_SQLSUPPORT によって報告される構文レベルに含まれていない SQL 機能をサポートしている場合は、プロバイダー固有のさまざまなプロパティを使用してそれらを示すことができます。

- SQLPROP_GROUPBY。 このプロパティは、SQL の最小限のレベルをサポートするプロバイダーにとって重要です。 このプロパティで、プロバイダーが `SELECT` ステートメント内の GROUP BY 句と HAVING 句をサポートしていることを示します。 また、このプロパティでは、プロバイダーが次の 5 つの集計関数、つまり MIN、MAX、SUM、COUNT、および AVG をサポートしていることも示します。 これらの集計関数の引数で、プロバイダーによって DISTINCT がサポートされていない可能性があります。

- SQLPROP_SUBQUERIES。 このプロパティは、SQL の最小限のレベルをサポートするプロバイダーで重要です。 プロバイダーが SQL-92 エントリ レベルに指定されているサブクエリをサポートしていることを示します。 これには、`SELECT` リスト内のサブクエリと、`WHERE` 句内のサブクエリが含まれ、相関サブクエリ、`IN`、`EXISTS`、`ALL`、および `ANY` 演算子がサポートされます。

- SQLPROP_DATELITERALS。 このプロパティは、あらゆるプロバイダー (SQL-92 エントリ レベルをサポートするプロバイダーを含む) にとって重要です。 datetime リテラルに対する標準リテラル構文のサポートは、SQL-92 エントリ レベルに含まれていません。 この SQL Server 固有のプロパティでは、プロバイダーが SQL-92 標準で指定されている datetime リテラル構文をサポートしていることを示します。

- SQLPROP_ANSILIKE。 SQL の最小限のレベルをサポートするプロバイダーにとって重要です。 このプロパティでは、プロバイダーが SQL-92 エントリ レベルに従って `LIKE` 演算子を (\'%\' および \'_\' をワイルドカード文字として) サポートしていることを示します。 SQL の最小限のレベルには `LIKE` のサポートが含まれていないため、これは SQL の最小限のレベルをサポートしているプロバイダーに対して有用です。

- SQLPROP_INNERJOIN。 このプロパティは、SQL の最小限のレベルをサポートするプロバイダーにとって重要です。 `FROM` 句内の複数のテーブルがサポートされていることを示します。 SQL の最小限のレベルのみをサポートしているプロバイダーに対して有用です (SQL の最小限のレベルには結合のサポートが含まれていないため)。 これは、明示的な JOIN キーワードに対するサポートや、OUTER 結合に対するサポートを示すものではありません。 `FROM` 句での、テーブルのリストを使用した暗黙的な結合のみをサポートしていることを示します。

- SQLPROP_DYNAMICSQL。 パラメーター マーカーとしての `?` に対するサポートを示します。 パラメーター マーカーは、`WHERE` 句または `SELECT` リスト内のスカラー項目の代わりにサポートされる必要があります。 パラメーター マーカー `?` のサポートによって、SQL Server からプロバイダーにパラメーター化クエリを送信できます。

- SQLPROP_NESTEDQUERIES。 `FROM` 句での入れ子になった SELECT (たとえば、`SELECT * FROM (SELECT * FROM T))`) のサポートを示します。 多くの場合、SQL Server では、リモートで実行されるクエリ文字列を生成するときに、クエリの `FROM` 句で入れ子になった `SELECT` ステートメントを使用します。 入れ子になった `SELECT` のサポートは SQL-92 エントリ レベルでは必須ではないため、SQL Server では、プロバイダーもこのプロパティを設定していない限り、入れ子になった `SELECT` ステートメントを持つクエリをプロバイダーに委任しません。 または、管理者がプロバイダーに `Nested Queries` プロバイダー オプションを設定することで、SQL Server でプロバイダーに対して入れ子になったクエリを生成させることもできます。

プロバイダーでは、`SQLPROPSET_OPTHINTS` という SQL Server 固有のプロパティ セットを使用してこれらのプロパティをサポートでき、`PROPID` の値を定義できます。 プロパティ セット `SQLPROPSET_OPTHINTS` と 2 つのプロパティは、次の定数を使用して定義されます。

```
extern const GUID `SQLPROPSET_OPTHINTS` = { 0x2344480c, 0x33a7, 0x11d1, { 0x9b, 0x1a, 0x0, 0x60, 0x8, 0x26, 0x8b, 0x9e } };
enum SQLPROPERTIES {
SQLPROP_NESTEDQUERIES = 0x4,
SQLPROP_DYNAMICSQL = 0x5,
SQLPROP_GROUPBY = 0x6,
SQLPROP_DATELITERALS = 0x7,
SQLPROP_ANSILIKE = 0x8,
SQLPROP_INNERJOIN = 0x9,
SQLPROP_SUBQUERIES = 0x10
};
```

#### <a name="character-set-and-sort-order-implications"></a>文字セットと並べ替え順序の影響

SQL Server では、列レベルごとに文字データの照合順序を指定できます。 照合順序には、文字セットと、Unicode 以外の文字データ用の並べ替え順序指定の両方 (`char` 列と `varchar` 列) が含まれます。 Unicode データの場合 (`nchar` 列と `nvarchar` 列)、照合順序では並べ替え順序のみが指定されます。

SQL Server では、リンク サーバーで使用される文字セット (Unicode 以外のデータの場合)、並べ替え順序、文字列比較のセマンティクスがローカル サーバーで使用されているものと同じ場合にのみ、プロバイダーに対して文字列比較を委任します。

SQL Server リンク サーバーの場合は、SQL Server によって照合順序の互換性が自動的に決定されます。 他のプロバイダーについては、管理者が、特定のリンク サーバーからの文字データの照合順序を SQL Server に示す必要があります。 SQL Server では、`Collation Name` という新しいリンク サーバー オプションがサポートされています。 管理者は、リンク サーバーで採用されている照合順序のセマンティクスが SQL Server 標準の照合順序の 1 つと同じであると判断した場合、`Collation Name` オプションをその照合順序名に設定できます。 `Collation Name` オプションを設定するには、`sp_serveroption` システム ストアド プロシージャを使用します。 このオプションは、次の両方の条件が満たされている場合にのみ設定する必要があります。

- リモートの並べ替え順序と文字セットが、指定された SQL Server の照合順序と同じである。

- OLE DB プロバイダーによって使用される文字列比較のセマンティクスが、SQL-92 標準仕様の比較セマンティクスに従っているか、SQL Server の比較セマンティクスに同等に従っている。

SQL Server 7.0 でサポートされている Collation Compatible オプションは、旧バージョンとの互換性のために引き続きサポートされています。 それを True に設定することは、Collation Name オプションを SQL Server マスター データベースの既定の照合順序に設定することと同じです。 新しいアプリケーションでは、Collation Compatible オプションの代わりに Collation Name オプションを使用してください。

### <a name="indexed-access"></a>インデックス アクセス

SQL Server では、プロバイダーによって公開されているインデックスを使用して、分散クエリの特定の述語を評価します。 このシナリオが可能なのは、インデックス プロバイダーに対して、およびユーザーが `Index as Access Path` プロバイダー オプションを設定した場合のみです。 以下では、インデックスを使用してクエリを実行する際に、プロバイダーに対して SQL Server で実行される主要な手順を大まかに示します。

1. 完全なテーブル名とインデックス名を指定した `IOpenRowset::OpenRowset` を使用して、インデックス行セットを開きます。 完全なテーブル名とインデックス名は、リモート クエリのシナリオで前述したとおりに生成されます。

1. テーブルの完全名を指定した `IOpenRowset::OpenRowset` を使用して、ベース テーブルの行セットを開きます。

1. `IRowsetIndex::SetRange` を使用し、クエリ述語に基づいてインデックス行セットの範囲を設定します。

1. インデックス行セットに対して、`IRowset` を使用してインデックス行セットから行をスキャンします。

1. 取得されたインデックス行のブックマーク列を使用して、ベース テーブルの行セットから対応する行を `IRowsetLocate::GetRowsByBookmark` でフェッチします。

ベース テーブルに対して開かれる行セットには、`DBPROP_IRowsetLocate` と `DBPROP_BOOKMARKS` の行セット プロパティが必要です。

### <a name="pure-table-scans"></a>純粋なテーブル スキャン

SQL Server でプロバイダーからリモート テーブル全体をスキャンし、すべてのクエリ評価をローカルで実行します。 テーブルに対応する行セットは、`IOpenRowset::OpenRowset` を呼び出すことによって開かれます。 SQL Server により、カタログ、スキーマ、およびオブジェクト名の各部分から `OPENROWSET` に提供されるテーブル名が次のように構築されます。

1. 名前の各部分をプロバイダーの引用記号 (`DBLITERAL_QUOTE`) で囲んでから、`DBLITERAL_CATALOG_SEPARATOR` 文字を間に埋め込んで連結します。

1. 行セット オブジェクトを開くと、SQL Server では `IColumnsInfo` インターフェイスを使用して、実行時のメタデータがテーブルのコンパイル時のメタデータと同じであることが確認されます。

1. SQL Server では、`IRowset` インターフェイスを使用してテーブルの行を移動し、使用します。 行をフェッチするには `IRowset::GetNextRows`、行セットの先頭に位置変更するには `IRowset::RestartPosition`、行を解放するには `IRowset::ReleaseRows` を使用します。

### <a name="update-and-delete-statements"></a>`UPDATE` ステートメントと `DELETE` ステートメント

リモート テーブルを SQL Server 分散クエリから更新または削除するには、次の条件が満たされている必要があります。

- プロバイダーで、更新または削除の対象となるテーブルの `IOpenRowset` で開かれた行セットについて、ブックマークをサポートしている必要があります。

- プロバイダーで、更新または削除の対象となるテーブルの `IOpenRowset` で開かれた行セットについて、`IRowsetLocate` インターフェイスと `IRowsetChange` インターフェイスをサポートしている必要があります。

- `IRowsetChange` インターフェイスで、更新 (`SetData`) と削除 (`DeleteRows`) のメソッドをサポートしている必要があります。

- プロバイダーで `ITransactionLocal` がサポートされていない場合、`UPDATE` ステートメントと `DELETE` ステートメントは、そのプロバイダーに対して `Non-transacted` オプションが設定されていて、ステートメントがユーザー トランザクションに含まれていない場合にのみ使用できます。

- プロバイダーで `ITransactionJoin` がサポートされていない場合、`UPDATE` ステートメントまたは `DELETE` ステートメントは、ユーザー トランザクションに含まれていない場合にのみ使用できます。

更新されたテーブルに対して開かれる行セットには、`DBPROP_IRowsetLocate`、`DBPROP_IRowsetChange`、および `DBPROP_BOOKMARKS` の各行セット プロパティが必要です。 `DBPROP_UPDATABILITY` 行セット プロパティは、実行された操作が `UPDATE` または `DELETE` のどちらであるかに応じて、それぞれ `DBPROPVAL_UP_CHANGE` または `DBPROPVAL_UP_DELETE` に設定されます。

`UPDATE` または `DELETE` の操作を処理するために、プロバイダーに対して以下の大まかな手順が実行されます。

1. SQL Server により、`IOpenRowset` インターフェイスを使用してベース テーブルの行セットが開かれます。 SQL Server では、行セットに前述のプロパティが必要です。

1. SQL Server によって、更新または削除する条件を満たす行のセットが判別されます。

1. SQL Server では、ブックマークを使用し、条件を満たす行に `IRowsetLocate` インターフェイスによって配置します。

1. `UPDATE` 操作には `IRowsetChange::SetData` を使用し、削除操作には `IRowsetChange::DeleteRows` を使用して、条件を満たす行に対して必要な変更を実行します。

### <a name="insert-statement"></a>`INSERT` ステートメント

リモート テーブルに対する `INSERT` ステートメントをサポートするための条件は、`UPDATE` ステートメントと `DELETE` ステートメントの場合ほど厳格ではありません。

- 挿入先のベース テーブルで開かれた行セットに対する `IRowsetChange::InsertRow` をプロバイダーでサポートしている必要があります。

- プロバイダーで `ITransactionLocal` がサポートされていない場合、`INSERT` ステートメントは、そのリンク サーバーに対して `Non-transacted updates` オプションが設定されていて、ステートメントがユーザー トランザクションに含まれていない場合にのみ使用できます。

- プロバイダーで `ITransactionJoin` がサポートされていない場合、`INSERT` ステートメントは、ユーザー トランザクションに含まれていない場合にのみ使用できます。

SQL Server では、`IOpenRowset::OpenRowset` を使用してベース テーブルで行セットを開き、`IRowsetChange::InsertRow` を呼び出して、ベース行セットに新しい行を挿入します。

### <a name="pass-through-queries"></a>パススルー クエリ

このシナリオは、リモート クエリのシナリオに似ていますが、`ICommand` に指定されたコマンド テキストがユーザーによって送信されたコマンド文字列であり、SQL Server によって解釈されないという点が異なります。 SQL Server では、`ICommandText::SetCommandText` を呼び出すときに、言語識別子として `DBGUID_DEFAULT` を使用します。 `DBGUID_DEFAULT` により、プロバイダーが既定の言語を使用する必要があることが示されます。 このコマンド テキストで複数の結果セットが返される場合、たとえば、複数の結果セットを返すストアド プロシージャをコマンドで呼び出した場合、コマンドの最初の結果セットのみが SQL Server によって使用されます。

SQL Server で使用されるすべての OLE DB インターフェイスの一覧については、「[SQL Server によって使用される OLE DB インターフェイス](#appendixa)」を参照してください。

### <a name="conclusion"></a>まとめ

Microsoft SQL Server によって、異種データ ソースにあるデータにアクセスするための最も信頼性の高いツール セットが提供されます。 SQL Server によって公開されている OLE DB インターフェイスを理解することで、開発者は分散クエリの高度な制御と高度な処理を実現できます。

## <a name="appendixa"></a>SQL Server によって使用される OLE DB インターフェイス

次の表は、SQL Server によって使用されるすべての OLE DB インターフェイスを示しています。 「必須」列は、インターフェイスが SQL Server に必要な最小限の OLE DB 機能の一部であるか、またはオプションかを示します。 特定のインターフェイスが必須としてマークされていない場合でも、SQL Server からプロバイダーへのアクセスは可能ですが、プロバイダーに対して特定の SQL Server 機能または最適化を実行することはできません。

オプションのインターフェイスの場合、「シナリオ」列には、指定したインターフェイスを使用する 6 つのシナリオのうち 1 つ以上が示されています。 たとえば、ベース テーブル行セットの `IRowsetChange` インターフェイスはオプションのインターフェイスです。このインターフェイスは、`UPDATE`、DELETE、`INSERT` の各ステートメントのシナリオで使用されます。 このインターフェイスがサポートされていない場合、UPDATE、DELETE、`INSERT` の各ステートメントをそのプロバイダーに対してサポートすることはできません。 オプションであるその他のインターフェイスの一部には、「シナリオ」列に \"パフォーマンス\" とマークされています。これは、そのインターフェイスを使用すると全般的なパフォーマンスが高くなることを示しています。 たとえば、`IDBSchemaRowset` インターフェイスがサポートされていない場合、SQL Server では行セットを 2 回開く必要があります (メタデータのために 1 回、クエリ実行のために 1 回)。 `IDBSchemaRowset` をサポートすることにより、SQL Server のパフォーマンスが向上します。

|Object|インターフェイス|Required|コメント|シナリオ|
|:-----|:-----|:-----|:-----|:-----|
|データ ソース オブジェクト|`IDBInitialize`|はい|データおよびセキュリティ コンテキストの初期化とセットアップを行います。| |
| |`IDBCreateSession`|はい|DB セッション オブジェクトを作成します。| |
| |`IDBProperties`|はい|プロバイダーの機能に関する情報を取得し、初期化プロパティを設定します。必須プロパティ:DBPROP_INIT_TIMEOUT.| |
| |`IDBInfo`|いいえ|引用符で囲んだリテラル、カタログ、名前、パーツ、区切り記号、文字などを取得します。|リモート クエリ。|
|DB セッション オブジェクト|`IDBSchemaRowset`|いいえ|テーブルまたは列のメタデータを取得します。 必要な行セット: `TABLES`、`COLUMNS`、`PROVIDER_TYPES`。その他 (使用可能な場合に使用される): `INDEXES`、`TABLE_STATISTICS`。|パフォーマンス、インデックス アクセス。|
| |`IOpenRowset`|はい|テーブル、インデックス、またはヒストグラムについての行セットを開きます。| |
| |`IGetDataSource`|はい|DB セッション オブジェクトから DSO に戻るために使用します。| |
| |`IDBCreateCommand`|いいえ|クエリをサポートするプロバイダー用のコマンド オブジェクト (クエリ) を作成するために使用します。|リモート クエリ、パススルー クエリ。|
| |`ITransactionLocal`|いいえ|トランザクション更新に使用します。|`UPDATE` および `DELETE`、`INSERT` ステートメント。|
| |`ITransactionJoin`|いいえ|分散トランザクション サポートに使用します。|ユーザー トランザクション内の場合、`UPDATE` および `DELETE`、`INSERT` ステートメント。|
|行セット オブジェクト|IRowset|はい|行をスキャンします。| |
| |`IAccessor`|はい|行セット内の列にバインドします。| |
| |`IColumnsInfo`|はい|行セット内の列に関する情報を取得します。| |
| |`IRowsetInfo`|はい|行セット プロパティに関する情報を取得します。| |
| |`IRowsetLocate`|いいえ|`UPDATE`/`DELETE` 操作のため、およびインデックス ベースの参照を実行するために必要です。ブックマークによって行を検索するために使用されます。|インデックス アクセス、`UPDATE` および `DELETE` ステートメント。|
| |`IRowsetChange`|いいえ|行セットに対する `INSERTS`/`UPDATES`/ `DELETES` に必要です。 ベース テーブルに対する行セットは、`INSERT`、`UPDATE`、および `DELETE`の各ステートメントのために、このインターフェイスをサポートしている必要があります。|`UPDATE` および `DELETE`、`INSERT` ステートメント。|
| |`IConvertType`|はい|行セットが、その行セット内の列の特定のデータ型変換をサポートしているかどうかを確認するために使用します。| |
|インデックス|`IRowset`|はい|行をスキャンします。|インデックス アクセス、パフォーマンス。|
| |`IAccessor`|はい|行セット内の列にバインドします。|インデックス アクセス、パフォーマンス。|
| |`IColumnsInfo`|はい|行セット内の列に関する情報を取得します。|インデックス アクセス、パフォーマンス。|
| |`IRowsetInfo`|はい|行セット プロパティに関する情報を取得します。|インデックス アクセス、パフォーマンス。|
| |`IRowsetIndex`|はい|インデックスについての行セットにのみ必要で、インデックス機能 (範囲の設定、シーク) に使用されます。|インデックス アクセス、パフォーマンス。|
|コマンド|`ICommand`|はい| |リモート クエリ、パススルー クエリ。|
| |`ICommandText`|はい|クエリ テキストの定義に使用します。|リモート クエリ、パススルー クエリ。|
| |`IColumnsInfo`|はい|クエリ結果の列のメタデータを取得するために使用します。|リモート クエリ、パススルー クエリ。|
| |`ICommandProperties`|はい|コマンドが返す行セットに対して必要なプロパティを指定するために使用します。|リモート クエリ、パススルー クエリ。|
| |`ICommandWithParameters`|いいえ|パラメーター化クエリの実行に使用します。|リモート クエリ、パフォーマンス。|
| |`ICommandPrepare`|いいえ|メタデータを取得するコマンド (使用可能な場合はパススルー クエリで使用される) を準備するために使用します。|リモート クエリ、パフォーマンス。|
|エラー オブジェクト|`IErrorRecords`|はい|1 つのエラー レコードに対応する、`IErrorInfo` インターフェイスへのポインターを取得するために使用します。| |
| |`IErrorInfo`|はい|1 つのエラー レコードに対応する、`IErrorInfo` インターフェイスへのポインターを取得するために使用します。| |
|任意のオブジェクト|`ISupportErrorInfo`|いいえ|特定のインターフェイスがエラー オブジェクトをサポートしているかどうかを確認するために使用します。| |
|  |  |  |  |  |

>[!NOTE]
>`Index` オブジェクト、`Command` オブジェクト、および `Error` オブジェクトは必須ではありません。 ただし、サポートされている場合、「必須」列に示されているとおり、一覧にあるインターフェイスは必須です。

## <a name="appendixb"></a>リモート クエリの生成に使用される SQL サブセット

SQL コマンド プロバイダーに対して SQL Server クエリ プロセッサによって生成される SQL サブセットは、`DBPROP_SQLSUPPORT`プロパティで示されているとおり、プロバイダーがサポートしている構文レベルによって異なります。

SQL エントリ レベルまたは ODBC コアをサポートする SQL コマンド プロバイダー

SQL Server では、SQL-92 エントリ レベルまたは ODBC コアのどちらかをサポートする SQL コマンド プロバイダーによって評価されるクエリに対して、SQL 言語の次のサブセットを使用します。

1. `SELECT`、`FROM`、`WHERE`、`GROUP BY`、`UNION`、`UNION ALL`、`ORDER BY DESC`、`ASC`、`HAVING` の各句を含む `SELECT` ステートメント。

1. `UNION` と `UNION ALL` は、SQL-92 エントリ レベルをサポートするプロバイダーに対してのみ生成され、ODBC コアをサポートするプロバイダーに対しては生成されません。

1. `SELECT` 句:

   - `SELECT` リスト内のスカラー サブクエリ。

   - `AS` キーワードを含まない列の別名。

1. `FROM` 句:

   - 明示的な結合キーワードは使用されません。コンマ区切りのテーブル名が内部結合を指定するために使用され、外部結合はリモート クエリでは指定されません。

   - `FROM` ( `<nested query>` ) `<alias>`という形式の入れ子になったクエリ。

   - AS キーワードを使用しないテーブルの別名。

1. `WHERE` 句では、`NOT` `EXISTS`、`ANY`、`ALL`でサブクエリを使用します。

1. 式:

   - 使用される集計関数: `MIN([DISTINCT])`、`MAX([DISTINCT])`、`COUNT([DISTINCT])`、`SUM([DISTINCT])`、`AVG([DISTINCT])`、`COUNT(*)`。

   - 比較演算子: `<`、`=`、`<=`、`>`、`<>`、`>=`、`IS NULL`、`IS NOT NULL`。

   - ブール演算子: `AND`、`OR`、`NOT`。

 - 算術演算子: `+`、`-`、`*`、`/`。

1. 定数:

- 数値リテラルと通貨リテラルは、常に `( )` で囲まれます。

- 文字リテラルは、引用符 `' '` で囲まれます。

SQL の最小限のレベルをサポートする SQL コマンド プロバイダー

SQL の最小限のレベルをサポートする SQL コマンド プロバイダーに対して、SQL Server では次の文法を使用して SQL が生成されます。

この文法は、ODBC 3.0 で説明されている SQL の最小限の文法を使用して派生しました。 この文法との違いはすべて強調表示されています。 `*bold italics`* (太字斜体) で示されている項目は、ODBC 3.0 で説明されている SQL の最小限の文法に追加された項目です。 緑色で削除済みと表示されている項目は、この文法から削除された項目です。

*select-statement* ::=

`SELECT [ALL | DISTINCT] *select-list* FROM *table-reference-list*[WHERE *search-condition*] [order-by-clause]`

`SELECT` clause

select-list ::= `*` | `select-sublist [, select-sublist]...`

select-sublist ::= expression * [`alias`]*

`*alias ::= user-defined-name`*

`FROM clause`

table-reference-list ::= table-reference

table-identifier ::= user-defined-name

table-name ::= table-identifier

table-reference ::= table-name

`WHERE clause`

search-condition ::= boolean-term \[OR search-condition\]

boolean-term ::= boolean-factor \[AND boolean-term\]

boolean-factor ::= \[NOT\] boolean-primary

boolean-primary ::= comparison-predicate \| ( search-condition )

comparison-predicate ::= expression comparison-operator expression

*\| `expression IS \[NOT\] NULL`*

comparison-operator ::= `< \| >` \| `<= \| >`= \| = \| `<>`

`ORDER BY clause`

order-by-clause ::= ORDER BY sort-specification \[, sort-specification\]\..

sort-specification ::= { \| column-name } \[ASC \| DESC\]

`Common syntactic elements`

expression ::= term \| expression {+\|--} term

term ::= factor \| term {\*\|/} factor

factor ::= \[+\|--\] primary

primary ::= column-name

\| literal

\| ( expression )

column-name ::= \[table-name.\]column-identifier

literal ::= character-string-literal

*\| integer-literal*

*\| exact-numeric-literal*

character-string-literal ::= \'{character}...\'

(character は、ドライバーまたはデータ ソースの文字セットに含まれる任意の文字です。 1 つのリテラル引用符文字 (\') を character-string-literal に含めるには、リテラル引用符文字を 2 個 (\'\') 使用します。)

`*integer-literal ::=* \[*+ \| -*\] *unsigned-integer`*

`*exact-numeric-literal::=* \[*+ \| -*\] *unsigned-integer* \[*period unsigned-integer*\]`

`*\| period unsigned-integer`*

base-table-name ::= base-table-identifier

base-table-identifier ::= user-defined-name

column-identifier ::= user-defined-name

user-defined-name ::= letter\[digit \| letter \| _\]\..

unsigned-integer ::= {digit}...

digit ::= 0 \| 1 \| 2 \| 3 \| 4 \| 5 \| 6 \| 7 \| 8 \| 9

period ::= . 

## <a name="appendixc"></a>SQL Server 固有のプロパティ

```
enum SQLPROPERTIES
       {
       SQLPROP_NOHPNEEDED = 0x1,
       SQLPROP_FREETHREADED = 0x2,
       SQLPROP_UMSENABLED = 0x3,
       SQLPROP_NESTEDQUERIES = 0x4,
       SQLPROP_DYNAMICSQL = 0x5,
       SQLPROP_GROUPBY = 0x6,
       SQLPROP_DATELITERALS = 0x7,
       SQLPROP_ANSILIKE = 0x8,
       SQLPROP_INNERJOIN = 0x9,
       SQLPROP_SUBQUERIES = 0x10, 
       SQLPROP_PARALLELSCAN = 0x11,
       SQLPROP_COLUMNCOLLATION = 0x12,
       SQLPROP_CARDINALITY = 0x13,
       SQLPROP_SIMPLEUPDATES = 0x14,
       SQLPROP_SQLLIKE = 0x15,
       SQLPROP_BITREMOTING = 0x16,
       SQLPROP_UNICODELITERALS = 0x17,
       SQLPROP_USELATESTCOLLATIONVERSION = 0x18
       };

```
