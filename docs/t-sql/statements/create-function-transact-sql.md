---
title: CREATE FUNCTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/06/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FUNCTION
- CREATE FUNCTION
- CREATE_FUNCTION_TSQL
- FUNCTION_TSQL
- TVF
- MSTVF
dev_langs:
- TSQL
helpviewer_keywords:
- invoking functions
- extended stored procedures [SQL Server], functions
- table-valued parameters
- user-defined functions [SQL Server], creating
- CLR functions [SQL Server]
- CREATE FUNCTION statement
- nondeterministic functions
- user-defined data types
- functions [SQL Server], creating
- inline table-valued functions [SQL Server]
- multi-statement table-valued functions [SQL Server]
- table-valued functions [SQL Server], CREATE FUNCTION
- parameters [SQL Server], functions
- nesting user-defined functions
- deterministic functions
- scalar-valued functions
- scalar UDF
- MSTVF
- TVF
- functions [SQL Server], invoking
ms.assetid: 864b393f-225f-4895-8c8d-4db59ea60032
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 35cf1b37a7c10992e17a52e4a44a473127ffb586
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982794"
---
# <a name="create-function-transact-sql"></a>CREATE FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] でユーザー定義関数を作成します。 ユーザー定義関数は、パラメーターを受け取り、複雑な計算などのアクションを実行し、そのアクションの結果を値として返す [!INCLUDE[tsql](../../includes/tsql-md.md)] または共通言語ランタイム (CLR) のルーチンです。 戻り値は、スカラー (単一) 値またはテーブルにすることができます。 このステートメントを使用して、次の方法で使用できる再利用可能なルーチンを作成します。  
  
-   SELECT などの [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント内で使用する  
  
-   関数を呼び出すアプリケーション内で使用する  
  
-   別のユーザー定義関数の定義内で使用する  
  
-   ビューをパラメーター化したり、インデックス付きビューの機能を向上させる  
  
-   テーブルの列を定義する  
  
-   列の CHECK 制約を定義する  
  
-   ストアド プロシージャを置換する  
  
-   セキュリティ ポリシーのフィルター述語としてのインライン関数を使用します。  
  
> [!NOTE]  
> このトピックでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への .NET Framework CLR の統合について説明します。 CLR 統合は、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] には適用されません。

> [!NOTE]  
> [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] については、「[CREATE FUNCTION (SQL Data Warehouse)](../../t-sql/statements/create-function-sql-data-warehouse.md)」を参照してください。
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Transact-SQL Scalar Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ = default ] [ READONLY ] }   
    [ ,...n ]  
  ]  
)  
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN scalar_expression  
    END  
[ ; ]  
```  
  
```  
-- Transact-SQL Inline Table-Valued Function Syntax   
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] [ READONLY ] }   
    [ ,...n ]  
  ]  
)  
RETURNS TABLE  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    RETURN [ ( ] select_stmt [ ) ]  
[ ; ]  
  
```  
  
```  
-- Transact-SQL Multi-Statement Table-Valued Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] [READONLY] }   
    [ ,...n ]  
  ]  
)  
RETURNS @return_variable TABLE <table_type_definition>  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN  
    END  
[ ; ]  
  
```  

```  
-- Transact-SQL Function Clauses   
<function_option>::=   
{  
    [ ENCRYPTION ]  
  | [ SCHEMABINDING ]  
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
  | [ EXECUTE_AS_Clause ]  
  | [ INLINE = { ON | OFF }]  
}  
  
<table_type_definition>:: =   
( { <column_definition> <column_constraint>   
  | <computed_column_definition> }   
    [ <table_constraint> ] [ ,...n ]  
)   
<column_definition>::=  
{  
    { column_name data_type }  
    [ [ DEFAULT constant_expression ]   
      [ COLLATE collation_name ] | [ ROWGUIDCOL ]  
    ]  
    | [ IDENTITY [ (seed , increment ) ] ]  
    [ <column_constraint> [ ...n ] ]   
}  
  
<column_constraint>::=   
{  
    [ NULL | NOT NULL ]   
    { PRIMARY KEY | UNIQUE }  
      [ CLUSTERED | NONCLUSTERED ]   
      [ WITH FILLFACTOR = fillfactor   
        | WITH ( < index_option > [ , ...n ] )  
      [ ON { filegroup | "default" } ]  
  | [ CHECK ( logical_expression ) ] [ ,...n ]  
}  
  
<computed_column_definition>::=  
column_name AS computed_column_expression   
  
<table_constraint>::=  
{   
    { PRIMARY KEY | UNIQUE }  
      [ CLUSTERED | NONCLUSTERED ]   
      ( column_name [ ASC | DESC ] [ ,...n ] )  
        [ WITH FILLFACTOR = fillfactor   
        | WITH ( <index_option> [ , ...n ] )  
  | [ CHECK ( logical_expression ) ] [ ,...n ]  
}  
  
<index_option>::=  
{   
    PAD_INDEX = { ON | OFF }   
  | FILLFACTOR = fillfactor   
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }   
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS ={ ON | OFF }   
}  
```  
  
```  
-- CLR Scalar Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS { return_data_type }  
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```  
  
```  
-- CLR Table-Valued Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS TABLE <clr_table_type_definition>   
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ ORDER ( <order_clause> ) ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```  

```  
-- CLR Function Clauses  
<order_clause> ::=   
{  
   <column_name_in_clr_table_type_definition>  
   [ ASC | DESC ]   
} [ ,...n]   
  
<method_specifier>::=  
    assembly_name.class_name.method_name  
  
<clr_function_option>::=  
}  
    [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
  | [ EXECUTE_AS_Clause ]  
}  
  
<clr_table_type_definition>::=   
( { column_name data_type } [ ,...n ] )  
  
```  
  
```  
-- In-Memory OLTP: Syntax for natively compiled, scalar user-defined function  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
 ( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ NULL | NOT NULL ] [ = default ] [ READONLY ] }   
    [ ,...n ]   
  ]   
)   
RETURNS return_data_type  
     WITH <function_option> [ ,...n ]   
    [ AS ]   
    BEGIN ATOMIC WITH (set_option [ ,... n ])   
        function_body   
        RETURN scalar_expression  
    END  
  
<function_option>::=   
{  
  |  NATIVE_COMPILATION   
  |  SCHEMABINDING   
  | [ EXECUTE_AS_Clause ]   
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]   
}  
  
```  
  
## <a name="arguments"></a>引数
*OR ALTER*  
 **適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 条件付きで、既に存在する場合にのみ関数を変更します。 
 
> [!NOTE]  
> CLR のオプションの [OR ALTER] 構文は、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU1 以降で使用できます。   
 
 *schema_name*  
 ユーザー定義関数が属するスキーマの名前を指定します。  
  
 *function_name*  
 ユーザー定義関数の名前です。 関数名は、[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。また、データベース内、およびそのスキーマに対して一意である必要があります。  
  
> [!NOTE]  
> パラメーターを指定しない場合でも、関数名の後にはかっこが必要です。  
  
 @*parameter_name*  
 ユーザー定義関数内のパラメーターです。 1 つ以上のパラメーターを宣言できます。  
  
 1 つの関数では、最高 2,100 個のパラメーターを使用できます。 宜言した各パラメーターの値は、関数の実行時に、ユーザーが指定する必要があります (そのパラメーターの既定値が定義されていない場合)。  
  
 最初の文字をアット マーク (@) にしてパラメーター名を指定します。 パラメーター名は識別子のルールに従っている必要があります。 パラメーターは関数に対してローカルです。同じパラメーター名を他の関数で使用できます。 パラメーターは定数の代わりとしてのみ使用できます。パラメーターは、テーブル名、列名、またはその他のデータベース オブジェクト名の代わりに使用することはできません。  
  
> [!NOTE]  
> ストアド プロシージャまたはユーザー定義関数でパラメーターを渡すとき、あるいはバッチ ステートメントで変数を宣言して設定するときには、ANSI_WARNINGS が無視されます。 たとえば、変数を **char(3)** と定義し、これに 4 文字以上の値を設定すると、データが定義されたサイズに合わせて切り捨てられてから、`INSERT` または `UPDATE` ステートメントが成功します。  
  
 [ *type_schema_name*. ] *parameter_data_type*  
 パラメーターのデータ型です。このデータ型が属するスキーマを指定することもできます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数の場合は、CLR ユーザー定義型およびユーザー定義テーブル型を含めたデータ型のうち、**timestamp** を除くすべてのデータ型を指定できます。 CLR 関数の場合は、CLR ユーザー定義型を含めたデータ型のうち、**text**、**ntext**、**image**、ユーザー定義テーブル型、**timestamp** を除くすべてのデータ型を指定できます。 非スカラー型である **cursor** と **table** は、[!INCLUDE[tsql](../../includes/tsql-md.md)] または CLR 関数でパラメーター データ型として指定できません。  
  
*type_schema_name* が指定されていない場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)] は次の順序で *scalar_parameter_data_type* を探します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム データ型の名前を含むスキーマ  
-   現在のデータベースにおける現在のユーザーの既定のスキーマ。  
-   現在のデータベースの **dbo** スキーマ。  
  
[ =*default* ]  
パラメーターの既定値です。 *default* 値が定義されている場合は、パラメーターに値を指定せずに関数を実行できます。  
  
> [!NOTE]  
> **varchar(max)** および **varbinary(max)** データ型の場合を除いて、CLR 関数には既定のパラメーター値を指定できます。  
  
 関数のパラメーターに既定値がある場合に、既定値を取得する目的でその関数を呼び出すときは、DEFAULT キーワードを指定する必要があります。 この動作は、ストアド プロシージャで既定値を持つパラメーターを使用する場合とは異なります。ストアド プロシージャの場合は、パラメーターを省略すると既定値が暗黙的に使用されます。 ただし、EXECUTE ステートメントを使用してスカラー関数を呼び出す場合は、DEFAULT キーワードは必要ありません。  
  
 READONLY  
 パラメーターを関数の定義内で更新または変更できないことを示します。 パラメーターの型がユーザー定義のテーブル型の場合は、READONLY を指定する必要があります。  
  
 *return_data_type*  
 スカラー ユーザー定義関数の戻り値です。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数の場合は、CLR ユーザー定義型を含めたデータ型のうち、**timestamp** を除くすべてのデータ型を指定できます。 CLR 関数の場合は、CLR ユーザー定義型を含めたデータ型のうち、**text**、**ntext**、**image**、**timestamp** を除くすべてのデータ型を指定できます。 非スカラー型である **cursor** と **table** は、[!INCLUDE[tsql](../../includes/tsql-md.md)] または CLR 関数で戻りデータ型として指定できません。  
  
 *function_body*  
 総合して副作用 (テーブルの変更など) がない一連の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが、関数の値を定義することを指定します。 *function_body* は、スカラー関数と複数ステートメントのテーブル値関数 (MSTVF) でのみ使用されます。  
  
 スカラー関数の *function_body* は、総合してスカラー値と評価される一連の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントです。  
  
 MSTVF の *function_body* は、TABLE 戻り変数を設定する一連の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントです。  
  
 *scalar_expression*  
 スカラー関数が返すスカラー値を指定します。  
  
 TABLE  
 テーブル値関数 (TVF) の戻り値がテーブルになるように指定します。 TVF に渡すことができるのは、定数と @*local_variables* のみです。  
  
 インライン TVF の TABLE 戻り値は、単一の SELECT ステートメントを使用して定義されます。 インライン関数には、関連付けられている戻り変数はありません。  
  
 <a name="mstvf"></a> MSTVF の \@*return_variable* は TABLE 変数で、その関数の値として返される必要がある行の格納および蓄積に使用されます。 \@ *return_variable* は [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数にのみ指定でき、CLR 関数には指定できません。  
  
 *select_stmt*  
 インライン テーブル値関数 (TVF) の戻り値を定義する単一の SELECT ステートメントです。  
  
 ORDER (\<order_clause>) は、テーブル値関数から結果が返される順序を指定します。 詳細については、このトピックで後述する「[並べ替え順序の使用に関するガイダンス](#using-sort-order-in-clr-table-valued-functions)」を参照してください。  
  
 EXTERNAL NAME \<method_specifier> *assembly_name*.*class_name*.*method_name*    
 **適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP1 以降)
  
 アセンブリおよび作成した関数名が参照するメソッドを指定します。  
  
-   *assembly_name* - 次の `name` 列にある値と一致する必要があります   
    `SELECT * FROM sys.assemblies;`  
    これは、`CREATE ASSEMBLY` ステートメントで使用された名前です。  
  
-   *class_name* - 次の `assembly_name` 列にある値と一致する必要があります  
    `SELECT * FROM sys.assembly_modules;`  
    多くの場合、値には、埋め込まれたピリオドまたはドット (.) が含まれています。 このような場合は、Transact-SQL 構文で、値を角かっこ ([]) または二重引用符 ("") で囲む必要があります。  
  
-   *method_name* - 次の `method_name` 列にある値と一致する必要があります   
    `SELECT * FROM sys.assembly_modules;`  
    メソッドを静的にする必要があります。  
  
一般的な例として、MyFood.DLL において、すべての型が MyFood 名前空間にあるため、`EXTERNAL NAME` 値は次のようになることがあります。   
`MyFood.[MyFood.MyClass].MyStaticMethod`  
  
> [!NOTE]  
> 既定では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は CLR コードを実行できません。 共通言語ランタイム モジュールを参照するデータベース オブジェクトを作成、変更、および削除することはできますが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でこれらの参照を実行するには、[clr enabled オプション](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)を有効にする必要があります。 このオプションを有効にするには、[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) を使用します。  
  
> [!NOTE]  
> このオプションは、包含データベースでは使用できません。  
  
 *\<* table_type_definition *>* ( { \<column_definition> \<column_constraint>    | \<computed_column_definition> }    [ \<table_constraint> ] [ ,...*n* ] ) [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数のテーブル データ型を定義します。 テーブルの定義には、列の定義、および列またはテーブルの制約が含まれます。 テーブルは、常にプライマリ ファイル グループに保存されます。  
  
 \< clr_table_type_definition >  ( { *column_name**data_type* } [ ,...*n* ] )    
 **適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP1 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] ([一部のリージョンではプレビュー](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))。  
  
 CLR 関数のテーブル データ型を定義します。 テーブルの定義には、列名およびデータ型のみが含まれます。 テーブルは、常にプライマリ ファイル グループに保存されます。  
  
 NULL|NOT NULL  
 ネイティブにコンパイルされた、スカラー ユーザー定義関数でのみサポートされます。 詳しくは、「[インメモリ OLTP でのユーザー定義のスカラー関数](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)」をご覧ください。  
  
 NATIVE_COMPILATION  
 ユーザー定義の関数をネイティブでコンパイルするかどうかを示します。 この引数は、ネイティブにコンパイルされたスカラー ユーザー定義関数に必要です。  
  
 BEGIN ATOMIC WITH  
 ネイティブにコンパイルされたスカラー ユーザー定義関数でのみサポートされます。これは必須です。 詳細については、「 [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)」を参照してください。  
  
 SCHEMABINDING  
 SCHEMABINDING の引数は、ネイティブにコンパイルされたスカラー ユーザー定義関数に必要です。  
  
 EXECUTE AS  
 EXECUTE AS は、ネイティブにコンパイルされたスカラー ユーザー定義関数に必要です。  
  
 **\<function_option>::= および \<clr_function_option>::=** 
  
 関数に以下のオプションを 1 つ以上指定します。  
  
 ENCRYPTION  
 **適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP1 以降)  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]で、CREATE FUNCTION ステートメントの元のテキストを、暗号化した形式に変換することを示します。 暗号化した形式の出力は、どのカタログ ビューでも直接見ることはできません。 システム テーブルまたはデータベース ファイルへのアクセス権を持たないユーザーは、暗号化した形式のテキストを取得できません。 ただし、[DAC ポート](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)経由でシステム テーブルにアクセスする権限、または直接データベース ファイルにアクセスする権限を持っているユーザーは、このテキストを使用できます。 また、サーバー プロセスにデバッガーをアタッチできるユーザーは、実行時、元のプロシージャをメモリから取得できます。 システム メタデータのアクセス方法について詳しくは、「[メタデータ表示の構成](../../relational-databases/security/metadata-visibility-configuration.md)」をご覧ください。  
  
 このオプションを使用すると、その関数を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーションの一部としてパブリッシュできなくなります。 CLR 関数にはこのオプションを指定できません。  
  
 SCHEMABINDING  
 参照するデータベース オブジェクトに対して、その関数がバインドされるように指定します。 SCHEMABINDING を指定した場合、ベース オブジェクトに対して関数定義に影響を与えるような変更は行えません。 まず関数定義を変更または削除して、変更するオブジェクトとの依存関係を解消する必要があります。  
  
 関数が参照するオブジェクトへのバインドは、次のいずれかの操作が行われた場合にのみ削除されます。 
  
-   関数を削除した場合。  
  
-   関数を、`SCHEMABINDING` オプションを指定せずに `ALTER` ステートメントを使用して変更した場合。  
  
関数をスキーマにバインドできるのは、次の条件が満たされている場合に限られます。  
  
-   関数が [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数である。  
  
-   関数が参照するユーザー定義関数とビューも同様にスキーマにバインドされている。  
  
-   関数が参照するオブジェクトが、2 つの要素から成る名前を使用して参照されている。  
  
-   関数およびその関数が参照するオブジェクトが、同じデータベースに属している。  
  
-   `CREATE FUNCTION` ステートメントを実行したユーザーが、その関数で参照されるデータベース オブジェクトに対する `REFERENCES` 権限を持っている。  
  
RETURNS NULL ON NULL INPUT | **CALLED ON NULL INPUT**  
スカラー関数の **OnNULLCall** 属性を指定します。 指定しない場合は、既定で CALLED ON NULL INPUT が暗黙的に使用されます。 つまり、NULL が引数として渡された場合でも、関数本体が実行されます。  
  
CLR 関数で RETURNS NULL ON NULL INPUT が指定されていると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、受け取った引数のいずれかが NULL であった場合に関数の本体を呼び出すことなく NULL を返すことができます。 \<method_specifier> に指定された CLR 関数のメソッドに RETURNS NULL ON NULL INPUT を示すカスタム属性が既に設定されている場合に、CREATE FUNCTION ステートメントで CALLED ON NULL INPUT を指定すると、CREATE FUNCTION ステートメントの指定が優先されます。 CLR テーブル値関数には、**OnNULLCall** 属性を指定できません。 
  
EXECUTE AS 句  
ユーザー定義関数が実行されるセキュリティ コンテキストを指定します。 つまり、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が、関数で参照されているデータベース オブジェクトに対する権限を検証する際に使用するユーザー アカウントを制御できます。  
  
> [!NOTE]  
> インライン テーブル値関数には `EXECUTE AS` を指定できません。
  
詳細については、「[EXECUTE AS 句 &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)」を参照してください。  

INLINE = { ON | OFF }  
このスカラー UDF をインライン化する必要があるかどうかを指定します。 この句は、スカラー ユーザー定義関数にのみ適用されます。 `INLINE` 句は必須ではありません。 `INLINE` 句を指定しないと、UDF をインライン化できるかどうかに基づいて、自動的に ON/OFF が設定されます。 `INLINE=ON` が指定されていても、UDF がインライン化できない場合は、エラーがスローされます。 詳細については、「[スカラー UDF のインライン化](../../relational-databases/user-defined-functions/scalar-udf-inlining.md)」を参照してください。
  
 **\< column_definition >::=** 
  
 Table データ型を定義します。 テーブルの宣言には、列の定義および制約が含まれます。 CLR 関数では、*column_name* と *data_type* のみを指定できます。  
  
 *column_name*  
 テーブルの列名です。 列名は、識別子のルールに従っていること、およびテーブル内で一意であることが必要です。 *column_name* は 1 ～ 128 文字で指定できます。  
  
 *data_type*  
 列のデータ型を指定します。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数の場合は、CLR ユーザー定義型を含めたデータ型のうち、**timestamp** を除くすべてのデータ型を指定できます。 CLR 関数の場合は、CLR ユーザー定義型を含めたデータ型のうち、**text**、**ntext**、**image**、**char**、**varchar**、**varchar(max)** 、**timestamp** を除くすべてのデータ型を指定できます。非スカラー型の **cursor** は、[!INCLUDE[tsql](../../includes/tsql-md.md)] 関数と CLR 関数の両方で、列のデータ型として指定できません。  
  
 DEFAULT *constant_expression*  
 挿入の際に明示的な値を指定しない場合に、列に入力される値を指定します。 *constant_expression* は、定数、NULL、またはシステム関数値です。 DEFAULT 定義は、IDENTITY プロパティを持つ列を除くすべての列に適用できます。 CLR テーブル値関数には DEFAULT を指定できません。  
  
 COLLATE *collation_name*  
 列の照合順序を指定します。 指定しない場合、データベースの既定の照合順序が列に割り当てられます。 照合順序名には、Windows 照合順序名または SQL 照合順序名を指定できます。 照合順序の一覧と詳細については、「[Windows 照合順序名 &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)」と「[SQL Server 照合順序名 &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md)」をご覧ください。  
  
 COLLATE 句を使用して照合順序を変更できるのは、**char**、**varchar**、**nchar**、**nvarchar** データ型の列だけです。  
  
 > [!NOTE]
 > CLR テーブル値関数には `COLLATE` を指定できません。  
  
 ROWGUIDCOL  
 新しい列が行グローバル一意識別子列であることを示します。 1 つのテーブルにつき、1 つの **uniqueidentifier** 列だけを ROWGUIDCOL 列に指定できます。 ROWGUIDCOL プロパティは **uniqueidentifier** 列にだけ割り当てることができます。  
  
 ROWGUIDCOL プロパティは、列に格納されている値の一意性を設定しません。 また、テーブルに挿入される新しい行の値を自動的に生成しません。 各列に対して一意な値を生成するには、INSERT ステートメントで NEWID 関数を使用します。 既定値も指定できますが、NEWID を既定値として指定することはできません。  
  
 IDENTITY  
 新しい列が ID 列であることを指定します。 テーブルに行が新しく追加されると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は列に一意な増加値を設定します。 ID 列は通常、PRIMARY KEY 制約と共に使用され、テーブルの一意な行識別子 (ROWID) の役割を果たします。 IDENTITY プロパティは、**tinyint**、**smallint**、**int**、**bigint**、**decimal(p,0)** 、**numeric(p,0)** のいずれかの列に割り当てることができます。 ID 列は 1 つのテーブルにつき 1 つだけ作成できます。 バインドされた既定値および DEFAULT 制約を ID 列と組み合わせて使用することはできません。 *seed* と *increment* は、両方を指定するか、どちらも指定しないでください。 どちらも指定しないときの既定値は (1,1) です。  
  
 CLR テーブル値関数には IDENTITY を指定できません。  
  
 *seed*  
 テーブル内の先頭行に割り当てる整数値を指定します。  
  
 *increment*  
 テーブル内の連続する行に対して、*seed* の値に加える整数値です。  
  
 **\< column_constraint >::= および \< table_constraint>::=** 
  
 指定された列またはテーブルの制約を定義します。 CLR 関数の場合、制約の種類として指定できるのは NULL だけです。 名前付き制約は使用できません。  
  
 NULL | NOT NULL  
 列で NULL 値を許すかどうかを示します。 NULL は厳密には制約ではありませんが、NOT NULL と同じように指定することができます。 CLR テーブル値関数には NOT NULL を指定できません。  
  
 PRIMARY KEY  
 一意なインデックスによって、指定した列にエンティティの整合性を設定する制約です。 テーブル値ユーザー定義関数では、1 つのテーブルにつき 1 つの列にのみ PRIMARY KEY 制約を作成できます。 CLR テーブル値関数には PRIMARY KEY を指定できません。  
  
 UNIQUE  
 一意なインデックスによって、指定した 1 つ以上の列にエンティティの整合性を提供する制約です。 1 つのテーブルには複数の UNIQUE 制約を指定できます。 CLR テーブル値関数には UNIQUE を指定できません。  
  
 CLUSTERED | NONCLUSTERED  
 PRIMARY KEY または UNIQUE 制約に対して、クラスター化インデックスまたは非クラスター化インデックスを作成することを示します。 PRIMARY KEY 制約では CLUSTERED が、UNIQUE 制約では NONCLUSTERED が、それぞれ使用されます。  
  
 CLUSTERED は 1 つの制約にのみ指定できます。 UNIQUE 制約で CLUSTERED が指定され、PRIMARY KEY 制約も指定した場合には、PRIMARY KEY は NONCLUSTERED を使用します。  
  
 CLR テーブル値関数には、CLUSTERED および NONCLUSTERED を指定できません。  
  
 CHECK  
 1 つ以上の列に入力できる値を制限することによってドメインの整合性を設定する制約です。 CLR テーブル値関数には CHECK 制約を指定できません。  
  
 *logical_expression*  
 TRUE または FALSE を返す論理式です。  
  
 **\<computed_column_definition>::=**  
  
 計算列を指定します。 計算列について詳しくは、「[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)」をご覧ください。  
  
 *column_name*  
 計算列の名前です。  
  
 *computed_column_expression*  
 計算列の値を定義する式です。  
  
 **\<index_option>::=**  
  
 PRIMARY KEY インデックスまたは UNIQUE インデックスのインデックス オプションを指定します。 インデックス オプションについて詳しくは、「[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)」をご覧ください。  
  
 PAD_INDEX = { ON | **OFF** }  
 インデックスの埋め込みを指定します。 既定値は OFF です。  
  
 FILLFACTOR = *fillfactor*  
 インデックスの作成時または変更時に、[!INCLUDE[ssDE](../../includes/ssde-md.md)] が各インデックス ページのリーフ レベルをどの程度まで埋めるかを、パーセント値で指定します。 *fillfactor* 値には、1 ～ 100 の整数値を指定してください。 既定値は 0 です。  
  
 IGNORE_DUP_KEY = { ON | **OFF** }  
 挿入操作で、一意のインデックスに重複するキー値を挿入しようとした場合のエラー応答を指定します。 IGNORE_DUP_KEY オプションは、インデックスが作成または再構築された後の挿入操作のみに適用されます。 既定値は OFF です。  
  
 STATISTICS_NORECOMPUTE = { ON | **OFF** }  
 分布統計を再計算するかどうかを指定します。 既定値は OFF です。  
  
 ALLOW_ROW_LOCKS = { **ON** | OFF }  
 行ロックを許可するかどうかを指定します。 既定値は ON です。  
  
 ALLOW_PAGE_LOCKS = { **ON** | OFF }  
 ページ ロックを許可するかどうかを指定します。 既定値は ON です。  
  
## <a name="best-practices"></a>ベスト プラクティス  
ユーザー定義関数の作成時に `SCHEMABINDING` 句を使用しないと、基になるオブジェクトに加えられた変更が関数の定義に影響して、関数が呼び出されたときに予期しない結果が生じる可能性があります。 基になるオブジェクトに対する変更によって関数が古くならないように、次のいずれかの操作を行うことをお勧めします。  
  
-   関数を作成するときには、`WITH SCHEMABINDING` 句を指定します。 これにより、関数定義で参照されているオブジェクトは、一緒に関数も変更しない限り変更できなくなります。  
  
-   関数の定義で指定されているオブジェクトを変更した後に [sp_refreshsqlmodule](../../relational-databases/system-stored-procedures/sp-refreshsqlmodule-transact-sql.md) ストアド プロシージャを実行します。  
  
> [!IMPORTANT]  
> インライン テーブル値関数 (インライン TVF) および複数ステートメント テーブル値関数 (MSTVF) の詳細とパフォーマンスに関する考慮事項については、「[ユーザー定義関数の作成 (データベース エンジン)](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)」を参照してください。 

## <a name="data-types"></a>データ型  
 CLR 関数で指定するパラメーターは、以前 *scalar_parameter_data_type* 用に定義されていた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 型にしてください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のシステム データ型と CLR 統合データ型または [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 共通言語ランタイム データ型との比較については、「[CLR パラメーター データのマッピング](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)」をご覧ください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、クラスにオーバーロードされているメソッドを正しく参照するには、\<method_specifier> で指定するメソッドに以下の特性が必要です。 
  
-   [ ,...*n* ] での指定と同数のパラメーターを受け取る。  
  
-   すべてのパラメーターを、参照ではなく値で受け取る。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 関数で指定されたパラメーター型と互換性のあるパラメーター型を使用する。  
  
 CLR 関数から返されるデータ型がテーブル型 (RETURNS TABLE) である場合、\<method_specifier> のメソッドから返されるデータ型は、**IEnumerator** または **IEnumerable** である必要があります。また、関数の作成者によってインターフェイスが実装されることが前提となります。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数とは異なり、CLR 関数では、\<table_type_definition> に PRIMARY KEY、UNIQUE、または CHECK 制約を含めることができません。 \<table_type_definition> に指定する列のデータ型は、\<method_specifier> のメソッドの実行時に返される結果セット内の、対応する列の型に一致する必要があります。 この型チェックは、関数の作成時には実行されません。 
  
 CLR 関数のプログラミング方法について詳しくは、「[CLR ユーザー定義関数](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)」をご覧ください。  
  
## <a name="general-remarks"></a>全般的な解説  
 スカラー関数は、スカラー式が使用されている場所で呼び出すことができます。 これには、計算列および CHECK 制約定義が含まれます。 スカラー関数は、[EXECUTE](../../t-sql/language-elements/execute-transact-sql.md) ステートメントを使用して実行することもできます。 スカラー関数は、2 つ以上の要素から構成される名前を使用して呼び出す必要があります ( *<schema>.<function>* )。 マルチパート名の詳細については、「[Transact-SQL 構文表記規則 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)」を参照してください。 `SELECT`、`INSERT`、`UPDATE`、`DELETE` の各ステートメントの `FROM` 句でテーブル式を使用できる場合は、テーブル値関数を呼び出すことができます。 詳しくは、「[ユーザー定義関数の実行](../../relational-databases/user-defined-functions/execute-user-defined-functions.md)」をご覧ください。  
  
## <a name="interoperability"></a>相互運用性  
 関数で有効なステートメントは以下のとおりです。  
  
-   代入ステートメント。  

-   `TRY...CATCH` ステートメントを除く、フロー制御ステートメント。  

-   ローカル データ変数およびローカル カーソルを定義する `DECLARE` ステートメント。  

-   ローカル変数に値を代入する式を持つ選択リストが含まれている `SELECT` ステートメント。  

-   関数内で宣言、オープン、クローズ、割り当ての解除を実行するローカル カーソルを参照するカーソル操作。 `INTO` 句を使用してローカル変数に値を代入する `FETCH` ステートメントのみが許可され、クライアントにデータを返す `FETCH` ステートメントは許可されません。  

-   ローカルなテーブル変数を変更する、`INSERT`、`UPDATE`、および `DELETE` ステートメント。  

-   拡張ストアド プロシージャを呼び出す `EXECUTE` ステートメント。  

詳しくは、「[ユーザー定義関数の作成 &#40;データベース エンジン&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)」をご覧ください。  
  
### <a name="computed-column-interoperability"></a>計算列の相互運用性  
 関数には次のプロパティがあります。 これらのプロパティの値によって、保存される計算列またはインデックス付き計算列で関数を使用できるかどうかが決まります。  
  
|プロパティ|[説明]|注|  
|--------------|-----------------|-----------|  
|**IsDeterministic**|関数が決定的か非決定的かを示します。|決定的関数では、ローカル データ アクセスが可能です。 決定的関数とは、たとえば、特定の一連の入力値を使用して同じ状態のデータベースで呼び出されるたびに、必ず同じ結果を返す関数です。|  
|**IsPrecise**|関数が正確か不正確かを示します。|不正確な関数には、浮動小数点演算などの演算を含みます。|  
|**IsSystemVerified**|関数の有効桁数のプロパティと決定性のプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で確認できます。||  
|**SystemDataAccess**|関数が、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のローカル インスタンスのシステム データ (システム カタログまたは仮想システム テーブル) にアクセスします。||  
|**UserDataAccess**|関数が、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のローカル インスタンスのユーザー データにアクセスします。|ユーザー定義テーブルと一時テーブルが含まれますが、テーブル変数は含まれません。|  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数の有効桁数のプロパティと決定性のプロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって自動的に決定されます。 CLR 関数のデータ アクセス プロパティと決定性のプロパティは、ユーザーが指定できます。 詳しくは、「[CLR 統合のカスタム属性の概要](https://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820)」をご覧ください。  
  
 これらのプロパティの現在の値を表示するには、[OBJECTPROPERTYEX](../../t-sql/functions/objectpropertyex-transact-sql.md) を使用します。  
  
> [!IMPORTANT]
> 関数は、決定的になるように `SCHEMABINDING` を使用して作成する必要があります。  
  
ユーザー定義関数に以下のプロパティ値がある場合、その関数を呼び出す計算列をインデックスで使用できます。  
  
-   **IsDeterministic** = true  
-   **IsSystemVerified** = true (保存される計算列である場合以外)  
-   **UserDataAccess** = false    
-   **SystemDataAccess** = false  
  
詳細については、「 [計算列のインデックス](../../relational-databases/indexes/indexes-on-computed-columns.md)」を参照してください。  
  
### <a name="calling-extended-stored-procedures-from-functions"></a>関数からの拡張ストアド プロシージャ呼び出し  
 拡張ストアド プロシージャは、関数の内部から呼び出された場合、結果セットをクライアントに返しません。 結果セットをクライアントに返す ODS API はすべて FAIL を返します。 拡張ストアド プロシージャは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続し直すことはできますが、その拡張ストアド プロシージャを起動した関数と同じトランザクションに参加することはできません。  
  
 バッチやストアド プロシージャから起動される場合と同じように、拡張ストアド プロシージャは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行している Windows セキュリティ アカウントのコンテキストで実行されます。 ストアド プロシージャの所有者は、その EXECUTE 権限をユーザーに与えるときに、この点を考慮する必要があります。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
 ユーザー定義関数は、データベースの状態を変更するアクションの実行に使用することはできません。  
  
 出力先がテーブルである `OUTPUT INTO` 句をユーザー定義関数に含めることはできません。  
  
 以下の [!INCLUDE[ssSB](../../includes/sssb-md.md)] ステートメントは、[!INCLUDE[tsql](../../includes/tsql-md.md)] ユーザー定義関数の定義に含めることができません。  
  
-   `BEGIN DIALOG CONVERSATION`  
  
-   `END CONVERSATION`  
  
-   `GET CONVERSATION GROUP`  
  
-   `MOVE CONVERSATION`  
  
-   `RECEIVE`  
  
-   `SEND`  
  
ユーザー定義関数は入れ子にすることができます。つまり、1 つのユーザー定義関数で、別のユーザー定義関数を呼び出すことができます。 呼び出された関数が実行を開始すると入れ子レベルが 1 つ上がり、呼び出された関数が実行を終了するとレベルが 1 つ下がります。 ユーザー定義関数は、32 レベルまで入れ子にすることができます。 入れ子レベルが最大値を超えると、関数チェーン全体の呼び出しが失敗します。 マネージド コードへの参照、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ユーザー定義関数は、32 レベルの入れ子制限の 1 つのレベルとしてカウントします。 マネージド コード内から呼び出されたメソッドは、この制限としてはカウントされません。  
  
### <a name="using-sort-order-in-clr-table-valued-functions"></a>並べ替え順序の使用に関するガイダンス  
CLR テーブル値関数で `ORDER` 句を使用する場合は、以下のガイドラインに従ってください。  
  
-   結果が常に指定した順序で並べられるようにする必要があります。 結果が指定した順序で並んでいないと、クエリを実行したときに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でエラー メッセージが生成されます。  
  
-   `ORDER` 句を指定した場合は、テーブル値関数の出力を列の照合順序に従って (明示的または暗黙的に) 並べ替える必要があります。 たとえば、列の照合順序が中国語である場合 (テーブル値関数の DDL で指定するか、またはデータベースの照合順序から取得) は、返される値が中国語の並べ替え規則に従って並べられていなければなりません。  
  
-   `ORDER` 句を指定した場合は、結果が返される際に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって、クエリ プロセッサで ORDER 句を使用してさらに最適化を行うかどうかが常に確認されます。 `ORDER` 句は、クエリ プロセッサに役立つことがわかっている場合にのみ使用してください。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のクエリ プロセッサでは、次の場合に `ORDER` 句が自動的に利用されます。  
  
    -   `ORDER` 句がインデックスと互換性のある挿入クエリ。  
  
    -   `ORDER` 句と互換性のある `ORDER BY` 句。  
  
    -   `GROUP BY` が `ORDER` 句と互換性のある、集計。  
  
    -   個別の列が `ORDER` 句と互換性のある `DISTINCT` 集計。  
  
SELECT クエリを実行するときは、そのクエリで `ORDER BY` を一緒に指定しないと、`ORDER` 句で順序どおりの結果が得られるかどうかは保証されません。 テーブル値関数の並べ替え順に含まれる列に対してクエリを実行する方法については、「[sys.function_order_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-function-order-columns-transact-sql.md)」を参照してください。  
  
## <a name="metadata"></a>メタデータ  
 次の表に、ユーザー定義関数に関するメタデータを返すために使用できるシステム カタログ ビューを示します。  
  
|システム ビュー|[説明]|  
|-----------------|-----------------|  
|[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)|以下の「例」の E を参照してください。|  
|[sys.assembly_modules](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)|CLR ユーザー定義関数の情報を表示します。|  
|[sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)|ユーザー定義関数で定義されているパラメーターの情報を表示します。|  
|[sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)|関数が参照する基になるオブジェクトを表示します。|  
  
## <a name="permissions"></a>アクセス許可  
 データベースの `CREATE FUNCTION` 権限と、関数を作成するスキーマの `ALTER` 権限が必要です。 関数でユーザー定義型が指定されている場合は、その型に対する `EXECUTE` 権限が必要です。  
  
## <a name="examples"></a>使用例  

> [!NOTE]
> UDF のその他の例とパフォーマンスに関する考慮事項については、「[ユーザー定義関数の作成 (データベース エンジン)](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)」を参照してください。 

### <a name="a-using-a-scalar-valued-user-defined-function-that-calculates-the-iso-week"></a>A. ISO 週番号を計算するスカラー値ユーザー定義関数を使用する  
 次の例では、ユーザー定義関数 `ISOweek` を作成します。 この関数は、日付引数を受け取って、ISO 週番号を計算します。 この関数が正しい計算を行うためには、関数を呼び出す前に `SET DATEFIRST 1` を呼び出す必要があります。  
  
 また、この例では、[EXECUTE AS](../../t-sql/statements/execute-as-clause-transact-sql.md) 句を使用して、ストアド プロシージャを実行できるセキュリティ コンテキストを指定します。 この例のオプション `CALLER` は、プロシージャが呼び出し元ユーザーのコンテキストで実行されることを指定しています。 指定できるその他のオプションは、`SELF`、`OWNER`、および *user_name* です。  
  
 以下に関数呼び出しを示します。 `DATEFIRST` が `1` に設定されていることにご注意ください。  
  
```sql
CREATE FUNCTION dbo.ISOweek (@DATE datetime)  
RETURNS int  
WITH EXECUTE AS CALLER  
AS  
BEGIN  
     DECLARE @ISOweek int;  
     SET @ISOweek= DATEPART(wk,@DATE)+1  
          -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104');  
--Special cases: Jan 1-3 may belong to the previous year  
     IF (@ISOweek=0)   
          SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1   
               AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1;  
--Special case: Dec 29-31 may belong to the next year  
     IF ((DATEPART(mm,@DATE)=12) AND   
          ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28))  
          SET @ISOweek=1;  
     RETURN(@ISOweek);  
END;  
GO  
SET DATEFIRST 1;  
SELECT dbo.ISOweek(CONVERT(DATETIME,'12/26/2004',101)) AS 'ISO Week';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
``` 
ISO Week  
----------------  
52  
```  
  
### <a name="b-creating-an-inline-table-valued-function"></a>B. インライン テーブル値関数を作成する  
 次の例は、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベース内のインライン テーブル値関数を返します。 ここでは、店舗に販売された製品ごとに 3 つの列を返します。`ProductID`、`Name`、`YTD Total`(今年に入ってからの店舗別合計の集計) です。  
  
```sql  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
GO  
```

 関数を呼び出すには、次のクエリを実行します。    

```sql  
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
### <a name="c-creating-a-multi-statement-table-valued-function"></a>C. 複数ステートメントのテーブル値関数を作成する  
 次の例は、テーブル値関数 `fn_FindReports(InEmpID)` を AdventureWorks2012 データベースに作成します。 有効な従業員 ID をこの関数に指定すると、その従業員に対して直接または間接の報告関係にあるすべての従業員に対応した表が返されます。 この関数は、再帰共通テーブル式 (CTE) を使用して、従業員の階層リストを生成します。 再帰 CTE の詳細については、「[WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)」を参照してください。  
  
```sql  
CREATE FUNCTION dbo.ufn_FindReports (@InEmpID INTEGER)  
RETURNS @retFindReports TABLE   
(  
    EmployeeID int primary key NOT NULL,  
    FirstName nvarchar(255) NOT NULL,  
    LastName nvarchar(255) NOT NULL,  
    JobTitle nvarchar(50) NOT NULL,  
    RecursionLevel int NOT NULL  
)  
--Returns a result set that lists all the employees who report to the   
--specific employee directly or indirectly.*/  
AS  
BEGIN  
WITH EMP_cte(EmployeeID, OrganizationNode, FirstName, LastName, JobTitle, RecursionLevel) -- CTE name and columns  
    AS (  
        -- Get the initial list of Employees for Manager n
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, 0   
        FROM HumanResources.Employee e   
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        WHERE e.BusinessEntityID = @InEmpID  
        UNION ALL  
        -- Join recursive member to anchor
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, RecursionLevel + 1   
        FROM HumanResources.Employee e   
            INNER JOIN EMP_cte  
            ON e.OrganizationNode.GetAncestor(1) = EMP_cte.OrganizationNode  
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        )  
-- copy the required columns to the result of the function   
   INSERT @retFindReports  
   SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
   FROM EMP_cte   
   RETURN  
END;  
GO  
-- Example invocation  
SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
FROM dbo.ufn_FindReports(1);   
  
GO  
```  
  
### <a name="d-creating-a-clr-function"></a>D. CLR 関数を作成する  
 この例では、CLR 関数 `len_s` を作成します。 関数が作成される前に、アセンブリ `SurrogateStringFunction.dll` がローカル データベースに登録されます。  
  
**適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP1 以降)  
  
```sql  
DECLARE @SamplesPath nvarchar(1024);  
-- You may have to modify the value of this variable if you have  
-- installed the sample in a location other than the default location.  
SELECT @SamplesPath = REPLACE(physical_name, 'Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\master.mdf', 
                                              'Microsoft SQL Server\130\Samples\Engine\Programmability\CLR\')   
    FROM master.sys.database_files   
    WHERE name = 'master';  
  
CREATE ASSEMBLY [SurrogateStringFunction]  
FROM @SamplesPath + 'StringManipulate\CS\StringManipulate\bin\debug\SurrogateStringFunction.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
GO  
  
CREATE FUNCTION [dbo].[len_s] (@str nvarchar(4000))  
RETURNS bigint  
AS EXTERNAL NAME [SurrogateStringFunction].[Microsoft.Samples.SqlServer.SurrogateStringFunction].[LenS];  
GO  
```  
  
 CLR テーブル値関数の作成方法の例については、「[CLR テーブル値関数](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md)」を参照してください。  
  
### <a name="e-displaying-the-definition-of-includetsqlincludestsql-mdmd-user-defined-functions"></a>E. [!INCLUDE[tsql](../../includes/tsql-md.md)] ユーザー定義関数の定義を表示する  
  
```sql  
SELECT definition, type   
FROM sys.sql_modules AS m  
JOIN sys.objects AS o ON m.object_id = o.object_id   
    AND type IN ('FN', 'IF', 'TF');  
GO  
```  
  
 `ENCRYPTION` オプションを使用して作成した関数の定義は、sys.sql_modules で表示することができません。しかし、暗号化された関数に関するその他の情報は表示されます。  
  
## <a name="see-also"></a>参照  
 [ユーザー定義関数の作成 &#40;データベース エンジン&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)   
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)    
 [DROP FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-function-transact-sql.md)   
 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [CLR ユーザー定義関数](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
  
 
