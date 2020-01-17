---
title: ALTER EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL LIBRARY
- ALTER_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL LIBRARY
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-current||=sqlallproducts-allversions'
ms.openlocfilehash: 9da237047e7b42b83cc8aa039d6bd04aaca9549a
ms.sourcegitcommit: ba44730f5cc33295ae2ed1f281186dd266bad4ef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2019
ms.locfileid: "74191073"
---
# <a name="alter-external-library-transact-sql"></a>ALTER EXTERNAL LIBRARY (Transact-SQL)  

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

既存の外部パッケージ ライブラリのコンテンツを変更します。

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||sqlallproducts-allversions"
> [!NOTE]
> SQL Server 2017 では、R 言語と Windows プラットフォームがサポートされています。 Windows および Linux プラットフォームの R、Python、外部言語は SQL Server 2019 以降でサポートされています。
::: moniker-end

::: moniker range="=azuresqldb-current"
> [!NOTE]
> Azure SQL Database では、ライブラリを削除し、**sqlmlutils** を使用して変更されたバージョンをインストールすることで、ライブラリを変更することができます。 **sqlmlutils** の詳細については、「[sqlmlutils を使用してパッケージを追加する](/azure/sql-database/sql-database-machine-learning-services-add-r-packages#add-a-package-with-sqlmlutils)」を参照してください。
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="syntax-for-sql-server-2019"></a>SQL Server 2019 の構文

```text
ALTER EXTERNAL LIBRARY library_name
[ AUTHORIZATION owner_name ]
SET <file_spec>
WITH ( LANGUAGE = <language> )
[ ; ]

<file_spec> ::=
{
    (CONTENT = { <client_library_specifier> | <library_bits> | NONE}
    [, PLATFORM = <platform> )
}

<client_library_specifier> :: =
{
      '[\\computer_name\]share_name\[path\]manifest_file_name'
    | '[local_path\]manifest_file_name'
    | '<relative_path_in_external_data_source>'
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
ALTER EXTERNAL LIBRARY library_name
[ AUTHORIZATION owner_name ]
SET <file_spec>
WITH ( LANGUAGE = 'R' )
[ ; ]

<file_spec> ::=
{
    (CONTENT = { <client_library_specifier> | <library_bits> | NONE}
    [, PLATFORM = WINDOWS )
}

<client_library_specifier> :: =
{
      '[\\computer_name\]share_name\[path\]manifest_file_name'
    | '[local_path\]manifest_file_name'
    | '<relative_path_in_external_data_source>'
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

既存のパッケージ ライブラリの名前を指定します。 ライブラリは、ユーザーに範囲指定されます。 ライブラリ名は、特定のユーザーまたは所有者のコンテキスト内で一意と見なされる必要があります。

ライブラリ名を任意に割り当てることはできません。 つまり、呼び出し元のランタイムがパッケージの読み込み時に想定している名前を使用する必要があります。

**owner_name**

外部ライブラリを所有しているユーザーまたはロールの名前を指定します。

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**file_spec**

特定のプラットフォーム用のパッケージのコンテンツを指定します。 プラットフォームごとに 1 つのファイル成果物のみがサポートされます。

ファイルは、ローカル パスまたはネットワーク パスの形式で指定することができます。 データ ソース オプションが指定されている場合、ファイル名は `EXTERNAL DATA SOURCE` で参照されているコンテナーに対する相対パスにすることができます。

必要に応じて、ファイルの OS プラットフォームを指定できます。 特定の言語またはランタイムの OS プラットフォームごとに 1 つのファイル成果物またはコンテンツのみが許可されます。

::: moniker-end

**library_bits**

アセンブリと同様に、パッケージのコンテンツを 16 進数のリテラルとして指定します。

このオプションは、ライブラリを変更するのにアクセス許可はあるが、サーバー上のファイルへのアクセスが制限されていて、サーバーがアクセスできるパスにコンテンツを保存できない場合に役に立ちます。

代わりに、パッケージのコンテンツを変数としてバイナリ形式で渡すことができます。

::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
**platform = WINDOWS**

ライブラリのコンテンツのプラットフォームを指定します。 この値は、さまざまなプラットフォームを追加する既存のライブラリを変更する場合に必要です。
SQL Server 2017 では、サポートされているプラットフォームは Windows のみです。
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**platform**

ライブラリのコンテンツのプラットフォームを指定します。 この値は、さまざまなプラットフォームを追加する既存のライブラリを変更する場合に必要です。 
SQL Server 2019 でサポートされているプラットフォームは、Windows と Linux です。
::: moniker-end

::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
**LANGUAGE = 'R'**

パッケージの言語を指定します。 R は SQL Server 2017 でサポートされています。
::: moniker-end

::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"
**LANGUAGE = 'R'**

パッケージの言語を指定します。 R は Azure SQL Database でサポートされています。
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**language**

パッケージの言語を指定します。 値は **R**、**Python**、または外部言語の名前にできます (「[CREATE EXTERNAL LANGUAGE](create-external-language-transact-sql.md)」を参照してください)。
::: moniker-end

## <a name="remarks"></a>解説

::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
R 言語の場合、Windows の .ZIP 拡張子を使用して、ZIP アーカイブ ファイルの形式でパッケージを準備する必要があります。 SQL Server 2017 では、Windows プラットフォームのみがサポートされています。  
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
R 言語の場合、ファイルを使用するときに .ZIP 拡張子を使用して、ZIP アーカイブ ファイルの形式でパッケージを準備する必要があります。 

Python 言語の場合、.whl または .zip ファイルのパッケージは zip アーカイブ ファイルの形式で準備する必要があります。 パッケージが既に .zip ファイルになっている場合、新しい .zip ファイルに含める必要があります。 現在のところ、.whl または .zip ファイルとしてパッケージを直接アップロードすることはできません。
::: moniker-end

`ALTER EXTERNAL LIBRARY` ステートメントは、ライブラリ ビットのデータベースへのアップロードのみを行います。 ユーザーがライブラリを呼び出す [sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) でコードを実行すると、変更したライブラリがインストールされます。

## <a name="permissions"></a>アクセス許可

既定では、**dbo** ユーザーまたはロール **db_owner** のすべてのメンバーが、ALTER EXTERNAL LIBRARY を実行する権限を持っています。 さらに、外部ライブラリを作成したユーザーも、その外部ライブラリを変更できます。

## <a name="examples"></a>例

次の例では、`customPackage` と呼ばれる外部ライブラリを変更します。

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||sqlallproducts-allversions"
### <a name="replace-the-contents-of-a-library-using-a-file"></a>ファイルを使用してライブラリのコンテンツを置き換える

次の例では、更新されたビットを含む ZIP 形式のファイルを使用して、`customPackage` と呼ばれる外部ライブラリを変更します。

```sql
ALTER EXTERNAL LIBRARY customPackage 
SET 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```

更新されたライブラリをインストールするには、ストアド プロシージャ `sp_execute_external_script` を実行します。

```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'library(customPackage)'
;
```
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
SQL Server 2019 の Python 言語の場合、`'R'` を `'Python'` に替えてもこの例は機能します。
::: moniker-end

### <a name="alter-an-existing-library-using-a-byte-stream"></a>バイト ストリームを使用して既存のライブラリを変更する

次の例では、新しいビットを 16 進数リテラルとして渡すことで、既存のライブラリを変更します。

```SQL
ALTER EXTERNAL LIBRARY customLibrary 
SET (CONTENT = 0xABC123...) WITH (LANGUAGE = 'R');
```

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
SQL Server 2019 の Python 言語の場合、`'R'` を `'Python'` に替えてもこの例は機能します。
::: moniker-end

> [!NOTE]
> このコード サンプルは構文のみを示しています。`CONTENT =` のバイナリ値は読みやすさのため切り捨てられており、作業ライブラリを作成しません。 バイナリ変数の実際の内容はこれよりも長くなります。

## <a name="see-also"></a>参照

[CREATE EXTERNAL LIBRARY (Transact-SQL)](create-external-library-transact-sql.md)  
[DROP EXTERNAL LIBRARY (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md) 
