---
title: CREATE EXTERNAL LANGUAGE (Transact-SQL) - SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: dphansen
ms.technology: language-extensions
ms.topic: language-reference
author: nelgson
ms.author: negust
manager: cgronlun
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3f2911406b902ea4d4e7840676dcf08b0318664d
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73536244"
---
# <a name="create-external-language-transact-sql"></a>CREATE EXTERNAL LANGUAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

指定したファイル パスまたはバイト ストリームから、データベースに外部言語拡張機能を登録します。 このステートメントは、データベース管理者が SQL Server によってサポートされている任意の OS プラットフォームで新しい外部言語拡張機能を登録する汎用メカニズムとして機能します。 詳細については、[Language Extensions (言語拡張)](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview) に関する記事を参照してください。

> [!NOTE]
> 現在、外部言語としては **Java** のみがサポートされています。 **R** と **Python** は予約済みの名前であり、それらの特定の名前で外部言語を作成することはできません。 **R** および **Python** を使う方法について詳しくは、「[SQL Server Machine Learning Services (SQL Server Machine Learning Services)](https://docs.microsoft.com/sql/advanced-analytics/)」をご覧ください。

## <a name="syntax"></a>構文

```text
CREATE EXTERNAL LANGUAGE language_name  
[ AUTHORIZATION owner_name ]  
FROM <file_spec> [ ,...2 ]  
WITH (<option_spec>)
[ ; ]  

<file_spec> ::=  
{
    ( CONTENT = { <external_lang_specifier> | <content_bits>,
    FILE_NAME = <external_lang_file_name>
    [ , PLATFORM = <platform> ]
    [ , PARAMETERS = <external_lang_parameters> ]
    [ , ENVIRONMENT_VARIABLES = <external_lang_env_variables> )
}

<external_lang_specifier> :: =  
{
    '[file_path\]os_file_name'  
}

<content_bits> :: =  
{
    varbinary_literal
    | varbinary_expression
}

<external_lang_file_name> :: =  
'extension_file_name'


<platform> :: =
{
    WINDOWS
  | LINUX
}

<external_lang_parameters> :: =  
'extension_specific_parameters'
```

### <a name="arguments"></a>引数

**language_name**

言語は、データベース スコープのオブジェクトです。 言語名は、データベース内で一意であることが必要です。

**owner_name**

外部言語を所有しているユーザーまたはロールの名前を指定します。 このオプションを指定しない場合は、所有権は現在のユーザーに与えられます。 アクセス許可によっては、特定の言語を使用するスクリプトを実行するために、他のユーザーに明示的なアクセス許可を付与することが必要な場合があります。

**file_spec**

言語拡張機能の内容を指定します。 プラットフォームごとに、特定の言語に対して 1 つの filespec だけを指定できます。

**external_lang_specifier**

拡張機能のコードが含まれる .zip または tar.gz ファイルの完全なファイル パスです。 この内容では、.zip ファイル (Windows の場合) または tar.gz (Linux の場合) へのパスを指定できます。

**content_bits**

アセンブリと同様に、言語の内容を 16 進数のリテラルとして指定します。

このオプションは、言語を作成するか、既存の言語を変更する必要があり (そして、それを行うために必要なアクセス許可を持っていて)、しかしサーバー上のファイル システムが制限されていて、サーバーがアクセスできる場所にライブラリ ファイルをコピーできない場合に、役に立ちます。

**external_lang_file_name**

拡張機能の .dll または .so ファイルの名前です。 これは、<external_lang_specifier> の .zip または tar.gz に複数の .dll ファイルまたは .so ファイルが含まれる場合に、正しいファイルを示すために必要です。

**external_lang_parameters**

外部言語ランタイムにパラメーターのセットを提供できます。 パラメーターの値は、外部プロセスが開始した後で、外部のランタイムに提供されます。 ただし、外部プロセスの開始前でも、言語拡張機能は環境変数にアクセスできます。

**external_lang_env_variables**

これにより、外部プロセスの開始前に、外部言語ランタイムに環境変数のセットを提供できます。 環境変数の例は、たとえば、ランタイム自体のホーム ディレクトリです。 例:JRE_HOME。

**platform**

このパラメーターは、ハイブリッド OS のシナリオに必要です。 ハイブリッド アーキテクチャでは、プラットフォームごとに 1 回、言語を登録する必要があります。 プラットフォームと言語の名前は、外部言語ごとの一意のキーになります。 プラットフォームを指定しないと、現在の OS が想定されます。

## <a name="remarks"></a>Remarks

現在、**PARAMETERS** と **ENVIRONMENT_VARIABLES** はサポートされていません。

## <a name="permissions"></a>アクセス許可

`CREATE EXTERNAL LANGUAGE` アクセス許可が必要です。 既定では、**db_owner** ロールのメンバーである **dbo** を持つすべてのユーザーに、外部言語を作成するためのアクセス許可があります。 他のすべてのユーザーについては、[GRANT](https://docs.microsoft.com/sql/t-sql/statements/grant-database-permissions-transact-sql) ステートメントを使用し、特権として CREATE EXTERNAL LANGUAGE を指定して、アクセス許可を明示的に付与する必要があります。

ライブラリを変更するには、別のアクセス許可 `ALTER ANY EXTERNAL LANGUAGE` が必要です。

### <a name="execute-external-script-permission"></a>EXECUTE EXTERNAL SCRIPT アクセス許可

EXECUTE EXTERNAL SCRIPT アクセス許可を使用すると、特定の言語で外部スクリプトの実行を許可できます。 これは、特定の言語での実行アクセス許可の付与を許可しない EXECUTE ANY EXTERNAL SCRIPT データベース許可とは異なります。

これは、**dbo** 以外のユーザーは、特定の言語を実行するためのアクセス許可を付与してもらう必要があることを意味します。

```sql
GRANT EXECUTE EXTERNAL SCRIPT ON EXTERNAL LANGUAGE ::language_name 
TO database_principal_name;
```

### <a name="reference-permissions-to-external-libraries"></a>外部ライブラリに対する参照アクセス許可

アセンブリと同様、外部ライブラリと外部言語の間にリンクが存在するように、外部言語に対する参照アクセス許可が必要です。 たとえば、外部言語を削除する場合、ユーザーは最初に、その言語を参照しているすべての外部ライブラリを削除する必要があります。 外部言語は、階層内で外部ライブラリより上位レベルのオブジェクトと見ることができます。

## <a name="examples"></a>使用例

### <a name="a-create-an-external-language-in-a-database"></a>A. データベース内の外部言語を作成する  

次の例では、Windows 上の SQL Server のデータベースに、Java という名前の外部言語を追加します。

```sql
CREATE EXTERNAL LANGUAGE Java 
FROM (CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll');
GO
```

### <a name="b-create-an-external-language-for-both-windows-and-linux"></a>B. Windows と Linux の両方に外部言語を作成する

最大 2 つの `<file_spec>` を指定できます。1 つは Windows 用、1 つは Linux 用です。

```sql
CREATE EXTERNAL LANGUAGE Java
FROM
(CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll', PLATFORM = WINDOWS),
(CONTENT = N'<path-to-tar.gz>', FILE_NAME = 'javaextension.so', PLATFORM = LINUX);
GO
```
### <a name="c-grant-permissions-to-execute-external-script"></a>C. 外部スクリプトを実行するアクセス許可を付与する

次の例では、**mylogin** プリンシパルに、**Java** 外部言語を使用してスクリプトを実行するアクセス権を付与します。

```sql
GRANT EXECUTE EXTERNAL SCRIPT ON EXTERNAL LANGUAGE ::Java 
TO mylogin;
```


## <a name="see-also"></a>参照

[ALTER EXTERNAL LANGUAGE (Transact-SQL)](alter-external-language-transact-sql.md)  
[DROP EXTERNAL LANGUAGE (Transact-SQL)](drop-external-language-transact-sql.md)  
[sys.external_languages](../../relational-databases/system-catalog-views/sys-external-languages-transact-sql.md)  
[sys.external_language_files](../../relational-databases/system-catalog-views/sys-external-language-files-transact-sql.md)  
