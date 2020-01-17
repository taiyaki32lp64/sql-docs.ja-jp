---
title: CREATE EXTERNAL LIBRARY (Transact-SQL) - SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL LIBRARY
- CREATE_EXTERNAL_LIBRARY_TSQL
- EXTERNAL LIBRARY
- EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EXTERNAL LIBRARY
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-current||=sqlallproducts-allversions'
ms.openlocfilehash: cb698f95037cb6ab39c5a98dbf725f9decc66cd0
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73536256"
---
# <a name="create-external-library-transact-sql"></a>CREATE EXTERNAL LIBRARY (Transact-SQL)  

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

指定したバイト ストリームまたはファイル パスから R、Python、Java パッケージ ファイルをデータベースにアップロードします。 このステートメントは、データベース管理者が新しい外部言語ランタイムに必要な成果物および [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] でサポートされる OS プラットフォームをアップロードする汎用メカニズムとして機能します。 

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||sqlallproducts-allversions"
> [!NOTE]
> SQL Server 2017 では、R 言語と Windows プラットフォームがサポートされています。 Windows および Linux プラットフォームの R、Python、外部言語は SQL Server 2019 以降でサポートされています。
::: moniker-end

::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"
> [!NOTE]
> Azure SQL Database では、**sqlmlutils** を使用してライブラリをインストールすることができます。 詳細については、「[sqlmlutils を使用してパッケージを追加する](/azure/sql-database/sql-database-machine-learning-services-add-r-packages#add-a-package-with-sqlmlutils)」を参照してください。
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="syntax-for-sql-server-2019"></a>SQL Server 2019 の構文

```text
CREATE EXTERNAL LIBRARY library_name  
[ AUTHORIZATION owner_name ]  
FROM <file_spec> [ ,...2 ]  
WITH ( LANGUAGE = <language> )  
[ ; ]  

<file_spec> ::=  
{  
    (CONTENT = { <client_library_specifier> | <library_bits> }  
    [, PLATFORM = <platform> ])  
}  

<client_library_specifier> :: = 
{
    '[file_path\]manifest_file_name'  
} 

<library_bits> :: =  
{ 
      varbinary_literal 
    | varbinary_expression 
}

<platform> :: = 
{
      WINDOWS
    | LINUX
}

<language> :: = 
{
      'R'
    | 'Python'
    | <external_language>
}

```
::: moniker-end
::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
## <a name="syntax-for-sql-server-2017"></a>SQL Server 2017 の構文

```text
CREATE EXTERNAL LIBRARY library_name  
[ AUTHORIZATION owner_name ]  
FROM <file_spec> [ ,...2 ]  
WITH ( LANGUAGE = 'R' )  
[ ; ]  

<file_spec> ::=  
{  
    (CONTENT = { <client_library_specifier> | <library_bits> }  
    [, PLATFORM = WINDOWS ])  
}  

<client_library_specifier> :: = 
{
    '[file_path\]manifest_file_name'
} 

<library_bits> :: =  
{ 
      varbinary_literal 
    | varbinary_expression 
}
```
::: moniker-end

::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"
## <a name="syntax-for-azure-sql-database"></a>Azure SQL Database の構文

```text
CREATE EXTERNAL LIBRARY library_name  
[ AUTHORIZATION owner_name ]  
FROM <file_spec> [ ,...2 ]  
WITH ( LANGUAGE = 'R' )  
[ ; ]  

<file_spec> ::=  
{  
    (CONTENT = <library_bits>)  
}  

<library_bits> :: =  
{ 
      varbinary_literal 
    | varbinary_expression 
}
```
::: moniker-end

### <a name="arguments"></a>引数

**library_name**

ライブラリは、ユーザーを対象としたデータベースに追加されます。 ライブラリ名は、特定のユーザーまたは所有者のコンテキスト内で一意と見なされる必要があります。 たとえば、**RUser1** と **RUser2** の 2 人のユーザーは、どちらも個別に R ライブラリ `ggplot2` をアップロードできます。 ただし、**RUser1** が新しいバージョンの `ggplot2` をアップロードする場合は、2 番目のインスタンスの名前を別のものにするか、既存のライブラリを置き換える必要があります。 

ライブラリ名は任意に割り当てることはできません。ライブラリ名は外部スクリプトからライブラリを読み込むために必要な名前と同じにする必要があります。

**owner_name**

外部ライブラリを所有しているユーザーまたはロールの名前を指定します。 このオプションを指定しない場合は、所有権は現在のユーザーに与えられます。

データベース所有者が所有するライブラリは、データベースとランタイムに対してグローバルと見なされます。 つまり、データベース所有者は、多くのユーザーによって共有されているライブラリまたはパッケージの共通セットが含まれているライブラリを作成できます。 `dbo` ユーザー以外のユーザーによって外部ライブラリが作成されると、その外部ライブラリは、そのユーザーに対してのみプライベートになります。

ユーザー **RUser1** が外部スクリプトを実行するときに、`libPath` の値に複数のパスを含めることができます。 最初のパスは常に、データベースの所有者によって作成された共有のライブラリへのパスになります。 `libPath` の 2 番目の部分では、**RUser1** によって個別にアップロードされたパッケージを含むパスを指定します。

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**file_spec**

特定のプラットフォーム用のパッケージのコンテンツを指定します。 プラットフォームごとに 1 つのファイル成果物のみがサポートされます。

ファイルは、ローカル パスまたはネットワーク パスの形式で指定することができます。

**<client_library_specifier>** で指定したファイルにアクセスしようとすると、SQL Server では現在の Windows ログインのセキュリティ コンテキストの権限が借用されます。 **<client_library_specifier>** でネットワーク上の場所 (UNC パス) を指定した場合は、委任制限があり、現在のログインの権限借用範囲はネットワーク上の場所まで拡大されません。 この場合、アクセスは SQL Server サービス アカウントのセキュリティ コンテキストを使って行われます。 詳しくは、「[資格情報 (データベース エンジン)](../../relational-databases/security/authentication-access/credentials-database-engine.md)」をご覧ください。

必要に応じて、ファイルの OS プラットフォームを指定できます。 特定の言語またはランタイムの OS プラットフォームごとに 1 つのファイル成果物またはコンテンツのみが許可されます。
::: moniker-end

**library_bits**

アセンブリと同様に、パッケージのコンテンツを 16 進数のリテラルとして指定します。 

このオプションは、ライブラリを作成または既存のライブラリを変更する (およびそれを行うために必要なアクセス許可を持つ) 必要があるが、サーバー上のファイル システムが制限されていて、サーバーがアクセスできる場所にライブラリ ファイルをコピーできない場合に役立ちます。

::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
**PLATFORM = WINDOWS**

ライブラリのコンテンツのプラットフォームを指定します。 既定値は、SQL Server が実行されているホスト プラットフォームに設定されます。 そのため、ユーザーが値を指定する必要はありません。 複数のプラットフォームがサポートされている場合、またはユーザーが別のプラットフォームを指定する必要がある場合に必要です。
SQL Server 2017 では、サポートされているプラットフォームは Windows のみです。
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**PLATFORM**

ライブラリのコンテンツのプラットフォームを指定します。 既定値は、SQL Server が実行されているホスト プラットフォームに設定されます。 そのため、ユーザーが値を指定する必要はありません。 複数のプラットフォームがサポートされている場合、またはユーザーが別のプラットフォームを指定する必要がある場合に必要です。
SQL Server 2019 でサポートされているプラットフォームは、Windows と Linux です。
::: moniker-end

::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
**LANGUAGE = 'R'**

パッケージの言語を指定します。
R は SQL Server 2017 でサポートされています。
::: moniker-end

::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"
**LANGUAGE = 'R'**

パッケージの言語を指定します。
R は Azure SQL Database でサポートされています。
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**language**

パッケージの言語を指定します。 値は `R`、`Python`、または外部言語の名前にできます (「[CREATE EXTERNAL LANGUAGE](create-external-language-transact-sql.md)」を参照してください)。
::: moniker-end

## <a name="remarks"></a>Remarks

::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
R 言語の場合、ファイルを使用するときに、Windows の .ZIP 拡張子を使用して、ZIP アーカイブ ファイルの形式でパッケージを準備する必要があります。 
SQL Server 2017 では、Windows プラットフォームのみがサポートされています。
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
R 言語の場合、ファイルを使用するときに .ZIP 拡張子を使用して、ZIP アーカイブ ファイルの形式でパッケージを準備する必要があります。  

Python 言語の場合、.whl または .zip ファイルのパッケージは zip アーカイブ ファイルの形式で準備する必要があります。 パッケージが既に .zip ファイルになっている場合、新しい .zip ファイルに含める必要があります。 現在のところ、.whl または .zip ファイルとしてパッケージを直接アップロードすることはできません。
::: moniker-end

`CREATE EXTERNAL LIBRARY` ステートメントは、ライブラリ ビットをデータベースにアップロードします。 ユーザーが [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) を使用して外部スクリプトを実行し、パッケージまたはライブラリを呼び出すと、ライブラリがインストールされます。

インスタンスにアップロードされたライブラリは、パブリックまたはプライベートのいずれかにすることができます。 `dbo` のメンバーによってライブラリが作成された場合、そのライブラリはパブリックで、すべてのユーザーと共有することができます。 それ以外の場合、ライブラリはそのユーザーのみのプライベートになります。

## <a name="permissions"></a>アクセス許可

`CREATE EXTERNAL LIBRARY` アクセス許可が必要です。 既定では、**db_owner** ロールのメンバーである **dbo** を持つすべてのユーザーに、外部ライブラリを作成する権限があります。 その他のすべてのユーザーには、特権として CREATE EXTERNAL LIBRARY を指定して、[GRANT](https://docs.microsoft.com/sql/t-sql/statements/grant-database-permissions-transact-sql) ステートメントを使用する権限を明示的に付与する必要があります。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
SQL Server 2019 では、ユーザーには 'CREATE EXTERNAL LIBRARY' アクセス許可に加えて、その外部言語の外部ライブラリを作成するために、外部言語に対する参照アクセス許可も必要です。

```sql
GRANT REFERENCES ON EXTERNAL LANGUAGE::Java to user
GRANT CREATE EXTERNAL LIBRARY to user
```

::: moniker-end

任意のライブラリを変更するには、別のアクセス許可 `ALTER ANY EXTERNAL LIBRARY` が必要です。

ファイル パスを使って外部アセンブリを作成するには、ユーザーが Windows 認証済みログインであるか、sysadmin 固定サーバー ロールのメンバーであることが必要です。

## <a name="examples"></a>使用例

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||sqlallproducts-allversions"
### <a name="add-an-external-library-to-a-database"></a>外部ライブラリをデータベースに追加する  

次の例では、`customPackage` と呼ばれる外部ライブラリをデータベースに追加します。

```sql
CREATE EXTERNAL LIBRARY customPackage
FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip') WITH (LANGUAGE = 'R');
```

ライブラリがインスタンスに正常にアップロードされたら、ユーザーが `sp_execute_external_script` プロシージャを実行して、ライブラリをインストールします。

```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'library(customPackage)'
```
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
SQL Server 2019 の Python 言語の場合、`'R'` を `'Python'` に替えてもこの例は機能します。
::: moniker-end

### <a name="installing-packages-with-dependencies"></a>依存関係を持つパッケージをインストールする

インストールするパッケージに依存関係がある場合は、ターゲットのパッケージをインストールする_前に_、最 1 レベルと第 2 レベルの両方の依存関係を分析し、必要なすべてのパッケージが利用できることを確認することが非常に重要です。

たとえば、新しいパッケージ `packageA` をインストールするとします。

+ `packageA` は `packageB` に依存関係があります
+ `packageB` は `packageC` に依存関係があります

`packageA` を正常にインストールするには、`packageA` を SQL Server に追加するのと同時に、`packageB` と `packageC` 用のライブラリを作成する必要があります。 必要なパッケージのバージョンも必ず確認してください。

実際には、一般的なパッケージのパッケージの依存関係は、通常、この単純な例よりもはるかに複雑です。 たとえば、**ggplot2** には 30 を超えるパッケージが必要で、それらのパッケージには、サーバーで入手できない追加のパッケージが必要な場合があります。 パッケージが不足していたり、パッケージのバージョンが違っていたりすると、インストールが失敗する可能性があります。

パッケージ マニフェストを見ただけでは、すべての依存関係を判断するのは難しいため、[miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) などのパッケージを使用して、インストールを正常に完了させるために必要なすべてのパッケージを特定することをお勧めします。

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"

+ ターゲット パッケージとその依存関係をアップロードします。 すべてのファイルは、サーバーからアクセスできるフォルダー内にある必要があります。

    ```sql
    CREATE EXTERNAL LIBRARY packageA 
    FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageA.zip') 
    WITH (LANGUAGE = 'R'); 
    GO

    CREATE EXTERNAL LIBRARY packageB FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageB.zip') 
    WITH (LANGUAGE = 'R');
    GO

    CREATE EXTERNAL LIBRARY packageC FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageC.zip') 
    WITH (LANGUAGE = 'R');
    GO
    ```

+ 最初に必要なパッケージをインストールします。

    必要なパッケージが既にインスタンスにアップロードされている場合、もう一度追加する必要はありません。 既存のパッケージのバージョンが正しいことだけを確認してください。 
    
    `sp_execute_external_script` を最初に実行してパッケージ `packageA` をインストールすると、必要なパッケージ `packageC` と `packageB` が正しい順序でインストールされます。

    ただし、必要なパッケージが使用できない場合、ターゲット パッケージ `packageA` のインストールが失敗します。

    ```sql
    EXEC sp_execute_external_script 
    @language =N'R', 
    @script=N'
    # load the desired package packageA
    library(packageA)
    '
    ```
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
SQL Server 2019 の Python 言語の場合、`'R'` を `'Python'` に替えてもこの例は機能します。
::: moniker-end

### <a name="create-a-library-from-a-byte-stream"></a>バイト ストリームからライブラリを作成する

パッケージ ファイルをサーバー上の場所に保存できない場合は、パッケージのコンテンツを変数で渡すことができます。 次の例では、ビットを 16 進数リテラルとして渡して、ライブラリを作成します。

```SQL
CREATE EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xABC123...) WITH (LANGUAGE = 'R');
```

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
SQL Server 2019 の Python 言語の場合、 **'R'** を **'Python'** に替えてもこの例は機能します。
::: moniker-end

> [!NOTE]
> このコード サンプルは構文のみを示しています。`CONTENT =` のバイナリ値は読みやすさのため切り捨てられており、作業ライブラリを作成しません。 バイナリ変数の実際の内容はこれよりも長くなります。

### <a name="change-an-existing-package-library"></a>既存のパッケージ ライブラリを変更する

`ALTER EXTERNAL LIBRARY` DDL ステートメントは、新しいライブラリのコンテンツを追加または既存のライブラリのコンテンツを変更するために使用できます。 既存のライブラリを変更するには、`ALTER ANY EXTERNAL LIBRARY` アクセス許可が必要です。

詳細については、「[ALTER EXTERNAL LIBRARY](alter-external-library-transact-sql.md)」を参照してください。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="add-a-java-jar-file-to-a-database"></a>Java .jar ファイルをデータベースに追加する  

次の例では、`customJar` と呼ばれる外部 jar ファイルをデータベースに追加します。

```sql
CREATE EXTERNAL LIBRARY customJar
FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\customJar.jar') 
WITH (LANGUAGE = 'Java');
```

ライブラリがインスタンスに正常にアップロードされたら、ユーザーが `sp_execute_external_script` プロシージャを実行して、ライブラリをインストールします。

```sql
EXEC sp_execute_external_script
    @language = N'Java'
    , @script = N'customJar.MyCLass.myMethod'
    , @input_data_1 = N'SELECT * FROM dbo.MyTable'
WITH RESULT SETS ((column1 int))
```

### <a name="add-an-external-package-for-both-windows-and-linux"></a>Windows と Linux の両方の外部のパッケージを追加する

最大 2 つの `<file_spec>` を指定できます。1 つは Windows 用、1 つは Linux 用です。

```sql
CREATE EXTERNAL LIBRARY lazyeval 
FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\packageA.zip', PLATFORM = WINDOWS),
(CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\packageA.tar.gz', PLATFORM = LINUX)
WITH (LANGUAGE = 'R')
```

`sp_execute_external_script` を使用してパッケージをインストールする場合、SQL Server インスタンスが実行されているプラットフォームに応じて、そのプラットフォームのライブラリ コンテンツがインストールされます。

```sql
EXECUTE sp_execute_external_script 
    @LANGUAGE = N'R',
    @SCRIPT = N'
library(packageA)
```
::: moniker-end

## <a name="see-also"></a>参照

[ALTER EXTERNAL LIBRARY (Transact-SQL)](alter-external-library-transact-sql.md)  
[DROP EXTERNAL LIBRARY (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
