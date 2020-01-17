---
title: ALTER FUNCTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/07/2017
ms.prod: sql
ms.prod_service: database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_FUNCTION_TSQL
- ALTER FUNCTION
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER FUNCTION statement
- modifying functions
- functions [SQL Server], modifying
ms.assetid: 89f066ee-05ac-4439-ab04-d8c3d5911179
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7de5bc19cd49959663bf4ead3f8ebff62b3b982b
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982858"
---
# <a name="alter-function-transact-sql"></a>ALTER FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  CREATE FUNCTION ステートメントを実行して作成された既存の [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数または CLR 関数を、権限を変更せずに、また、従属する関数、ストアド プロシージャ、またはトリガーに影響を及ぼさずに変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Transact-SQL Scalar Function Syntax    
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ = default ] }   
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
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
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
-- Transact-SQL Multistatement Table-valued Function Syntax
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
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
-- CLR Scalar and Table-Valued Function Syntax
ALTER FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS { return_data_type | TABLE <clr_table_type_definition> }  
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```
  
```
-- CLR Function Clauses
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
-- Syntax for In-Memory OLTP: Natively compiled, scalar user-defined function  
ALTER FUNCTION [ schema_name. ] function_name    
 ( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ NULL | NOT NULL ] [ = default ] }   
    [ ,...n ]   
  ]   
)   
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]   
    [ AS ]   
    BEGIN ATOMIC WITH (set_option [ ,... n ])  
        function_body   
        RETURN scalar_expression  
    END  
    
<function_option>::=   
{ |  NATIVE_COMPILATION   
  |  SCHEMABINDING   
  | [ EXECUTE_AS_Clause ]   
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]   
}  
```   
  
## <a name="arguments"></a>引数  
 *schema_name*  
 ユーザー定義関数が属するスキーマの名前を指定します。  
  
 *function_name*  
 変更するユーザー定義関数です。  
  
> [!NOTE]  
>  パラメーターを指定しない場合でも、関数名の後にはかっこが必要です。  
  
 **@** _parameter_name_  
 ユーザー定義関数内のパラメーターです。 1 つ以上のパラメーターを宣言できます。  
  
 1 つの関数では、最高 2,100 個のパラメーターを使用できます。 宜言した各パラメーターの値は、関数の実行時に、ユーザーが指定する必要があります (そのパラメーターの既定値が定義されていない場合)。  
  
 パラメーター名は、最初の文字をアット マーク ( **@** ) にして指定します。 パラメーター名は[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。 パラメーターは関数に対してローカルです。同じパラメーター名を他の関数で使用できます。 パラメーターは定数の代わりとしてのみ使用できます。パラメーターは、テーブル名、列名、またはその他のデータベース オブジェクト名の代わりに使用することはできません。  
  
> [!NOTE]  
>  ストアド プロシージャでパラメーターを引き渡す場合や、バッチ ステートメントで変数を宣言または設定する場合、またはユーザー定義関数においては、ANSI_WARNINGS は無視されます。 たとえば、変数を **char(3)** と定義し、これに 4 文字以上の値を設定すると、データが定義されたサイズに合わせて切り捨てられてから、INSERT または UPDATE ステートメントが成功します。  
  
 [ *type_schema_name.* ] *parameter_data_type*  
 パラメーターのデータ型です。このデータ型が属するスキーマを指定することもできます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数の場合は、CLR ユーザー定義型を含めたデータ型のうち、**timestamp** を除くすべてのデータ型を指定できます。 CLR 関数の場合は、CLR ユーザー定義型を含めたデータ型のうち、**text**、**ntext**、**image**、**timestamp** を除くすべてのデータ型を指定できます。 非スカラー型である **cursor** と **table** は、[!INCLUDE[tsql](../../includes/tsql-md.md)] または CLR 関数でパラメーター データ型として指定できません。  
  
 *type_schema_name* が指定されていない場合、[!INCLUDE[ssDEversion2005](../../includes/ssdeversion2005-md.md)] は次の順序で *parameter_data_type* を探します。  
  
-   SQL Server システム データ型の名前を含むスキーマ。  
  
-   現在のデータベースにおける現在のユーザーの既定のスキーマ。  
  
-   現在のデータベースの **dbo** スキーマ。  
  
 [ **=** _default_ ]  
 パラメーターの既定値です。 *default* 値が定義されている場合は、パラメーターに値を指定せずに関数を実行できます。  
  
> [!NOTE]  
>  **varchar(max)** および **varbinary(max)** データ型の場合を除いて、CLR 関数には既定のパラメーター値を指定できます。  
  
 関数のパラメーターが既定値を持つ場合は、既定値を得るために、関数を呼び出すときに DEFAULT キーワードを指定する必要があります。 この動作は、ストアド プロシージャで既定値を持つパラメーターを使用する場合とは異なります。ストアド プロシージャの場合は、パラメーターを省略すると既定値が暗黙的に使用されます。  
  
 *return_data_type*  
 スカラー ユーザー定義関数の戻り値です。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数の場合は、CLR ユーザー定義型を含めたデータ型のうち、**timestamp** を除くすべてのデータ型を指定できます。 CLR 関数の場合は、CLR ユーザー定義型を含めたデータ型のうち、**text**、**ntext**、**image**、**timestamp** を除くすべてのデータ型を指定できます。 非スカラー型である **cursor** と **table** は、[!INCLUDE[tsql](../../includes/tsql-md.md)] または CLR 関数で戻りデータ型として指定できません。  
  
 *function_body*  
 総合して副作用 (テーブルの変更など) がない一連の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが、関数の値を定義することを指定します。 *function_body* は、スカラー関数と複数ステートメントのテーブル値関数でのみ使用されます。  
  
 スカラー関数の *function_body* は、総合してスカラー値と評価される一連の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントです。  
  
 複数ステートメントのテーブル値関数の *function_body* は、TABLE 戻り変数にデータを格納する一連の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントです。  
  
 *scalar_expression*  
 スカラー関数がスカラー値を返すように指定します。  
  
 TABLE  
 テーブル値関数の戻り値がテーブルになるように指定します。 テーブル値関数に渡すことができるのは、定数および **@** _local\_variables_ だけです。  
  
 インライン テーブル値関数の TABLE 戻り値は、単一の SELECT ステートメントを使用して定義します。 インライン関数には、関連付けられている戻り変数はありません。  
  
 複数ステートメントのテーブル値関数の **@** _return\_variable_ は TABLE 変数で、その関数の値として返される行の格納および蓄積に使用されます。 **@** _return\_variable_ は [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数にのみ指定でき、CLR 関数には指定できません。  
  
 *select-stmt*  
 インライン テーブル値関数の戻り値を定義する単一の SELECT ステートメントです。  
  
 EXTERNAL NAME \<method_specifier>*assembly_name.class_name*.*method_name*  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 関数にバインドするアセンブリのメソッドを指定します。 *assembly_name* は、表示がオンになっている現在のデータベースに存在する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアセンブリと一致している必要があります。 *class_name* は、有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別子であること、およびアセンブリにクラスとして存在していることが必要です。 名前空間部分を区切るためにピリオド ( **.** ) を使う名前空間修飾名がクラスにある場合は、クラス名をかっこ ( **[ ]** ) または引用符 ( **""** ) で区切る必要があります。 *method_name* は、有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別子であること、および指定されているクラスの静的メソッドとして存在していることが必要です。  
  
> [!NOTE]  
>  既定では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は CLR コードを実行できません。 共通言語ランタイム モジュールを参照するデータベース オブジェクトを作成、変更、および削除することはできますが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でこれらの参照を実行するには、[clr enabled オプション](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)を有効にする必要があります。 このオプションを有効にするには、[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) を使用します。  
  
> [!NOTE]  
>  このオプションは、包含データベースでは使用できません。  
  
 _\<_table\_type\_definition_\>_ **(** { \<column_definition\> \<column\_constraint\> | \<computed\_column\_definition\> } [ \<table\_constraint\> ] [ **,** ...*n* ] **)**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数のテーブル データ型を定義します。 テーブルの定義には、列の定義、および列またはテーブルの制約が含まれます。  
  
\< clr_table_type_definition \> **(** { *column_name**data_type* } [ **,** ...*n* ] **)** **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([一部のリージョンではプレビュー](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))。  
  
 CLR 関数のテーブル データ型を定義します。 テーブルの定義には、列名およびデータ型のみが含まれます。  
  
 NULL|NOT NULL  
 ネイティブにコンパイルされた、スカラー ユーザー定義関数でのみサポートされます。 詳しくは、「[インメモリ OLTP でのユーザー定義のスカラー関数](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)」をご覧ください。  
  
 NATIVE_COMPILATION  
 ユーザー定義の関数をネイティブでコンパイルするかどうかを示します。 この引数は、ネイティブにコンパイルされたスカラー ユーザー定義関数に必要です。  
  
 NATIVE_COMPILATION 引数は、関数に対して ALTER を適用する場合に必要であり、関数が NATIVE_COMPILATION 引数を使用して作成されている場合にのみ使用できます。  
  
 BEGIN ATOMIC WITH  
 ネイティブにコンパイルされたスカラー ユーザー定義関数でのみサポートされます。これは必須です。 詳細については、「 [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)」を参照してください。  
  
 SCHEMABINDING  
 SCHEMABINDING の引数は、ネイティブにコンパイルされたスカラー ユーザー定義関数に必要です。  
  
 **\<function_option>::= および \<clr_function_option>::=**  
  
 関数に以下のオプションを 1 つ以上指定します。  
  
 ENCRYPTION  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 ALTER FUNCTION ステートメントのテキストを含むカタログ ビューの列を、[!INCLUDE[ssDE](../../includes/ssde-md.md)]が暗号化することを示します。 ENCRYPTION を使用すると、その関数を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーションの一部としてパブリッシュできなくなります。 CLR 関数には ENCRYPTION を指定できません。  
  
 SCHEMABINDING  
 参照するデータベース オブジェクトに対して、その関数がバインドされるように指定します。 このバインドによって、他のスキーマ バインド オブジェクトがその関数を参照している場合に関数が変更されるのを防ぐことができます。  
  
 関数が参照するオブジェクトへのバインドは、次のいずれかの操作が行われた場合にのみ削除されます。  
  
-   関数を削除した場合。  
  
-   関数を、SCHEMABINDING オプションを指定せずに ALTER ステートメントを使用して変更した場合。  
  
関数をスキーマ バインドにする前に必要な条件の一覧については、「[CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)」をご覧ください。  
  
 RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT  
 スカラー値関数の **OnNULLCall** 属性を指定します。 指定しない場合は、既定で CALLED ON NULL INPUT が暗黙的に使用されます。 つまり、NULL が引数として渡された場合でも、関数本体が実行されます。  
  
 CLR 関数で RETURNS NULL ON NULL INPUT が指定されていると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、受け取った引数のいずれかが NULL であった場合に関数の本体を呼び出すことなく NULL を返すことができます。 \<method_specifier> に指定されたメソッドに RETURNS NULL ON NULL INPUT を示すカスタム属性が既に設定されている場合に、ALTER FUNCTION ステートメントで CALLED ON NULL INPUT を指定すると、ALTER FUNCTION ステートメントの指定が優先されます。 CLR テーブル値関数には、**OnNULLCall** 属性を指定できません。  
  
 EXECUTE AS 句  
 ユーザー定義関数が実行されるセキュリティ コンテキストを指定します。 これにより、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が、関数で参照されているデータベース オブジェクトに対する権限を検証する際に使用するユーザー アカウントを制御できます。  
  
> [!NOTE]  
>  インライン ユーザー定義関数には EXECUTE AS を指定できません。  
  
 詳細については、「[EXECUTE AS 句 &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)」を参照してください。  
  
**\< column_definition >::=**
  
 Table データ型を定義します。 テーブルの宣言には、列の定義および制約が含まれます。 CLR 関数では、*column_name* と *data_type* のみを指定できます。  
  
 *column_name*  
 テーブルの列名です。 列名は、識別子のルールに従っていること、およびテーブル内で一意であることが必要です。 *column_name* は 1 ～ 128 文字で指定できます。  
  
 *data_type*  
 列のデータ型を指定します。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数の場合は、CLR ユーザー定義型を含めたデータ型のうち、**timestamp** を除くすべてのデータ型を指定できます。 CLR 関数の場合は、CLR ユーザー定義型を含めたデータ型のうち、**text**、**ntext**、**image**、**char**、**varchar**、**varchar(max)** 、**timestamp** を除くすべてのデータ型を指定できます。非スカラー型の **cursor** は、[!INCLUDE[tsql](../../includes/tsql-md.md)] 関数と CLR 関数の両方で、列のデータ型として指定できません。  
  
 DEFAULT *constant_expression*  
 挿入の際に明示的な値を指定しない場合に、列に入力される値を指定します。 *constant_expression* は、定数、NULL、またはシステム関数値です。 DEFAULT 定義は、IDENTITY プロパティを持つ列を除くすべての列に適用できます。 CLR テーブル値関数には DEFAULT を指定できません。  
  
 COLLATE *collation_name*  
 列の照合順序を指定します。 指定しない場合、データベースの既定の照合順序が列に割り当てられます。 照合順序名には、Windows 照合順序名または SQL 照合順序名を指定できます。 一覧と詳細については、「[Windows 照合順序名 &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)」と「[SQL Server 照合順序名 &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md)」を参照してください。  
  
 COLLATE 句を使用して照合順序を変更できるのは、**char**、**varchar**、**nchar**、**nvarchar** データ型の列だけです。  
  
 CLR テーブル値関数には COLLATE を指定できません。  
  
 ROWGUIDCOL  
 新しい列が行グローバル一意識別子列であることを指定します。 1 つのテーブルにつき、1 つの **uniqueidentifier** 列だけを ROWGUIDCOL 列に指定できます。 ROWGUIDCOL プロパティは **uniqueidentifier** 列にだけ割り当てることができます。  
  
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
  
 PAD_INDEX = { ON | OFF }  
 インデックスの埋め込みを指定します。 既定値は OFF です。  
  
 FILLFACTOR = *fillfactor*  
 インデックスの作成時または変更時に、[!INCLUDE[ssDE](../../includes/ssde-md.md)] が各インデックス ページのリーフ レベルをどの程度まで埋めるかを、パーセント値で指定します。 *fillfactor* 値には、1 ～ 100 の整数値を指定してください。 既定値は 0 です。  
  
 IGNORE_DUP_KEY = { ON | OFF }  
 挿入操作で、一意のインデックスに重複するキー値を挿入しようとした場合のエラー応答を指定します。 IGNORE_DUP_KEY オプションは、インデックスが作成または再構築された後の挿入操作のみに適用されます。 既定値は OFF です。  
  
 STATISTICS_NORECOMPUTE = { ON | OFF }  
 分布統計を再計算するかどうかを指定します。 既定値は OFF です。  
  
 ALLOW_ROW_LOCKS = { ON | OFF }  
 行ロックを許可するかどうかを指定します。 既定値は ON です。  
  
 ALLOW_PAGE_LOCKS = { ON | OFF }  
 ページ ロックを許可するかどうかを指定します。 既定値は ON です。  
  
## <a name="remarks"></a>Remarks  
 ALTER FUNCTION を使用してスカラー値関数をテーブル値関数に変更することも、その逆の変更を行うこともできません。 さらに、ALTER FUNCTION を使用してインライン関数を複数ステートメント関数に変更することも、その逆の変更を行うこともできません。 ALTER FUNCTION を使用して [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数を CLR 関数に変更したり、その逆の変更を行ったりすることもできません。  
  
 以下の Service Broker ステートメントは、[!INCLUDE[tsql](../../includes/tsql-md.md)] ユーザー定義関数の定義に含めることができません。  
  
-   BEGIN DIALOG CONVERSATION  
-   END CONVERSATION  
-   GET CONVERSATION GROUP  
-   MOVE CONVERSATION  
-   RECEIVE  
-   SEND  
  
## <a name="permissions"></a>アクセス許可  
 関数またはスキーマに対する ALTER 権限が必要です。 関数でユーザー定義型が指定されている場合は、その型に対する EXECUTE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [DROP FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-function-transact-sql.md)   
 [パブリケーション データベースでのスキーマの変更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
