---
title: sqlcmd でのスクリプト変数の使用 | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- scripts [SQL Server], sqlcmd utility
- variables [SQL Server], scripts
- scripting variables [SQL Server]
- sqlcmd utility, scripts
- setvar command
ms.assetid: 793495ca-cfc9-498d-8276-c44a5d09a92c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 142fd6bdd0ceb39003aba5c8ec8131c9df6427dd
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262859"
---
# <a name="sqlcmd---use-with-scripting-variables"></a>sqlcmd - スクリプト変数の使用
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  スクリプトで使用される変数は、スクリプト変数と呼ばれます。 スクリプト変数を使用すると、1 つのスクリプトを複数のシナリオで使用できます。 たとえば、1 つのスクリプトを複数のサーバーに対して実行する場合、各サーバー用にスクリプトを変更するのではなく、サーバー名にスクリプト変数を使用することができます。 サーバー名をスクリプト変数で指定することで、同じスクリプトを複数のサーバーで実行することができるようになります。  
  
 スクリプト変数は、 **setvar** コマンドを使用して明示的に定義するか、または **sqlcmd -v** オプションを使用して暗黙的に定義できます。  
  
 このトピックでは、 **SET**を使用して Cmd.exe コマンド プロンプトで環境変数を定義する例も紹介しています。  
  
## <a name="setting-scripting-variables-by-using-the-setvar-command"></a>setvar コマンドを使用したスクリプト変数の設定  
 **setvar** コマンドは、スクリプト変数を定義するのに使用します。 **setvar** コマンドを使用して定義されている変数は、内部的に格納されます。 スクリプト変数は、 **SET**を使用してコマンド プロンプトで定義されている環境変数と混同しないようにする必要があります。 環境変数でもなく **setvar**コマンドを使用して定義したものでもない変数をスクリプト内で参照していると、エラー メッセージが表示され、スクリプトの実行は停止されます。 詳細については、「 **sqlcmd ユーティリティ** 」の [-b](../../tools/sqlcmd-utility.md)オプションの説明を参照してください。  
  
## <a name="variable-precedence-low-to-high"></a>変数の優先順位 (低から高)  
 複数の種類の変数に同じ名前が付いている場合、優先順位の最も高い変数が使用されます。  
  
1.  システム レベル環境変数  
  
2.  ユーザー レベル環境変数  
  
3.  **SET X=Y**の起動前にコマンド プロンプトで設定されたコマンド シェル ( **SET X=Y**)  
  
4.  **sqlcmd-v** X=Y  
  
5.  **:Setvar** X Y  
  
> [!NOTE]  
>  環境変数を表示するには、 **[コントロール パネル]** の **[システム]** アイコンを開き、 **[詳細設定]** タブをクリックします。  
  
## <a name="implicitly-setting-scripting-variables"></a>スクリプト変数の暗黙的な設定  
 関連する **sqlcmd** 変数を含むオプションを指定して **sqlcmd** を起動すると、 **sqlcmd** 変数には、そのオプションを使用して指定されている値が暗黙的に設定されます。 次の例では、 `sqlcmd` が `-l` オプションを指定して起動されています。 このコマンドを実行すると、SQLLOGINTIMEOUT 変数が暗黙的に設定されます。  
  
```
c:\> sqlcmd -l 60
```
 
**-v** オプションを使用して、スクリプト内に存在するスクリプト変数を設定することもできます。 次のスクリプト (ファイル名は `testscript.sql`) では、 `ColumnName` がスクリプト変数です。  
 
```
USE AdventureWorks2012;

SELECT x.$(ColumnName)
FROM Person.Person x
WHERE x.BusinessEntityID < 5;
```

その後、 `-v` オプションを使用して、取得する列の名前を指定できます。  
 
```
sqlcmd -v ColumnName ="FirstName" -i c:\testscript.sql
```

同じスクリプトを使用して別の列を取得するには、 `ColumnName` スクリプト変数の値を変更します。  
  
```
sqlcmd -v ColumnName ="LastName" -i c:\testscript.sql
```

## <a name="guidelines-for-scripting-variable-names-and-values"></a>スクリプト変数の名前と値に関するガイドライン  
 スクリプト変数に名前を指定する場合は、次のガイドラインを考慮してください。  
  
-   変数名には空白文字または引用符を使用できません。  
  
-   変数名には、 *$(var)* のような変数式と同じ形式を使用することはできません。  
  
-   スクリプト変数では、大文字と小文字が区別されません。  
  
    > [!NOTE]  
    >  **sqlcmd** 環境変数に値が割り当てられていない場合、この変数は削除されます。 値を指定せずに **:setvar VarName** を使用すると、変数は削除されます。  
  
 スクリプト変数に値を指定する場合は、次のガイドラインを考慮してください。  
  
-   **setvar** または **-v** オプションを使用して定義する変数値は、空白を含む文字列値の場合に引用符で囲む必要があります。  
  
-   変数値に引用符が使用されている場合は、その引用符をエスケープする必要があります。 たとえば、`setvar MyVar "spac""e"`のように指定します。  
  
## <a name="guidelines-for-cmdexe-set-variable-values-and-names"></a>Cmd.exe の SET による変数の値と名前に関するガイドライン  
 SET を使用して定義される変数は、Cmd.exe 環境で使用されるため、 **sqlcmd**で参照できます。 次のガイドラインを考慮してください。  
  
-   変数名には空白文字または引用符を使用できません。  
  
-   変数値には空白文字または引用符を使用できます。  
  
## <a name="sqlcmd-scripting-variables"></a>sqlcmd スクリプト変数  
 **sqlcmd** で定義される変数はスクリプト変数と呼ばれます。 次の表は、 **sqlcmd** スクリプト変数の一覧です。  
  
|        変数         | 関連するオプション | R/W |         既定         |
| ----------------------- | -------------- | --- | ----------------------- |
| SQLCMDUSER\*             | -U             | R   | ""                      |
| SQLCMDPASSWORD\*         | -P             | --  | ""                      |
| SQLCMDSERVER\*           | -S             | R   | "DefaultLocalInstance"  |
| SQLCMDWORKSTATION       | -H             | R   | "ComputerName"          |
| SQLCMDDBNAME            | -d             | R   | ""                      |
| SQLCMDLOGINTIMEOUT      | -l             | R/W | "8" (秒)           |
| SQLCMDSTATTIMEOUT       | -t             | R/W | "0" = 無制限に待機 |
| SQLCMDHEADERS           | -H             | R/W | "0"                     |
| SQLCMDCOLSEP            | -S             | R/W | " "                     |
| SQLCMDCOLWIDTH          | -w             | R/W | "0"                     |
| SQLCMDPACKETSIZE        | -A             | R   | "4096"                  |
| SQLCMDERRORLEVEL        | -M             | R/W | "0"                     |
| SQLCMDMAXVARTYPEWIDTH   | -y             | R/W | "256"                   |
| SQLCMDMAXFIXEDTYPEWIDTH | -y             | R/W | "0" = 無制限         |
| SQLCMDEDITOR            |                | R/W | "edit.com"              |
| SQLCMDINI               |                | R   | ""                      |

SQLCMDUSER、SQLCMDPASSWORD および SQLCMDSERVER は、 **:Connect** が使用されるときに設定されます。  

R は、その値がプログラムの初期化時に一度だけ設定できることを示します。  
  
R/W は、 **setvar** コマンドを使用して値を再設定できること、および後続のコマンドで新しい値が使用されることを示します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-the-setvar-command-in-a-script"></a>A. スクリプトでの setvar コマンドの使用  
 多くの **sqlcmd** オプションは、スクリプトで **setvar** コマンドを使用して制御できます。 次の例では、スクリプト `test.sql` が作成されます。このスクリプトでは、変数 `SQLCMDLOGINTIMEOUT` が `60` 秒に設定され、別のスクリプト変数 `server`が `testserver`に設定されています。 `test.sql`のコードを次に示します。  

```
:setvar SQLCMDLOGINTIMEOUT 60
:setvar server "testserver"
:connect $(server) -l $(SQLCMDLOGINTIMEOUT)

USE AdventureWorks2012;

SELECT FirstName, LastName
FROM Person.Person;
```

このスクリプトは、sqlcmd を使用して呼び出されます。

```
sqlcmd -i c:\test.sql
```
  
### <a name="b-using-the-setvar-command-interactively"></a>B. setvar コマンドの対話的な使用  
 次の例では、 `setvar` コマンドを使用してスクリプト変数を対話的に設定する方法を示します。  

```
sqlcmd
:setvar  MYDATABASE AdventureWorks2012
USE $(MYDATABASE);
GO
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
Changed database context to 'AdventureWorks2012'
1>
```
  
### <a name="c-using-command-prompt-environment-variables-within-sqlcmd"></a>C. sqlcmd 内でのコマンド プロンプト環境変数の使用  
 次の例では、4 つの環境変数を設定した後、 `are` から呼び出します。 `sqlcmd`  

```
C:\>SET tablename=Person.Person
C:\>SET col1=FirstName
C:\>SET col2=LastName
C:\>SET title=Ms.
C:\>sqlcmd -d AdventureWorks2012
1> SELECT TOP 5 $(col1) + ' ' + $(col2) AS Name
2> FROM $(tablename)
3> WHERE Title ='$(title)'
4> GO
```
  
### <a name="d-using-user-level-environment-variables-within-sqlcmd"></a>D. sqlcmd 内でのユーザーレベル環境変数の使用  
 次の例では、ユーザーレベル環境変数 `%Temp%` をコマンド プロンプトで設定し、 `sqlcmd` 入力ファイルに渡します。 ユーザーレベル環境変数を取得するには、 **[コントロール パネル]** の **[システム]** をダブルクリックします。 **[詳細設定]** タブをクリックし、 **[環境変数]** をクリックします。  
  
 入力ファイル `c:\testscript.txt`のコードを次に示します。

```
:OUT $(MyTempDirectory)
USE AdventureWorks2012;

SELECT FirstName
FROM AdventureWorks2012.Person.Person
WHERE BusinessEntityID` `< 5;
```

コマンド プロンプトで、次のコードを入力します。

```
C:\ >SET MyTempDirectory=%Temp%\output.txt
C:\ >sqlcmd -i C:\testscript.txt
```

 出力ファイル C:\Documents and Settings\\<user\>\Local Settings\Temp\output.txt には、次の結果が送信されます。  

```
Changed database context to 'AdventureWorks2012'.
FirstName
--------------------------------------------------
Gustavo
Catherine
Kim
Humberto

(4 rows affected)
```

### <a name="e-using-a-startup-script"></a>E. スタートアップ スクリプトの使用  
 **sqlcmd** スタートアップ スクリプトは、 **sqlcmd** の起動時に実行されます。 次の例では、環境変数 `SQLCMDINI`が設定されます。 以下の内容を次に示します: `init.sql.`  

```
SET NOCOUNT ON
GO

DECLARE @nt_username nvarchar(128)
SET @nt_username = (SELECT rtrim(convert(nvarchar(128), nt_username))
FROM sys.dm_exec_sessions WHERE spid = @@SPID)
SELECT  @nt_username + ' is connected to ' +
rtrim(CONVERT(nvarchar(20), SERVERPROPERTY('servername'))) +
' (' +`  
rtrim(CONVERT(nvarchar(20), SERVERPROPERTY('productversion'))) +
')'
:setvar SQLCMDMAXFIXEDTYPEWIDTH 100
SET NOCOUNT OFF
GO

:setvar SQLCMDMAXFIXEDTYPEWIDTH
```

 次のコードにより、 `init.sql` の起動時に `sqlcmd` ファイルが呼び出されます。  
  
```
c:\> SET sqlcmdini=c:\init.sql
>1 Sqlcmd
```

 出力結果は次のとおりです。  

```
>1 < user > is connected to < server > (9.00.2047.00)
```

  
> [!NOTE]  
>  **-X** オプションを使用すると、スタートアップ スクリプト機能が無効になります。  
  
### <a name="f-variable-expansion"></a>F. 変数の拡張  
 次の例では、 **sqlcmd** 変数の形式でデータを使用する方法を示します。  

```
USE AdventureWorks2012;
CREATE TABLE AdventureWorks2012.dbo.VariableTest
(
Col1 nvarchar(50)
);
GO
```

 `Col1` の `dbo.VariableTest` に、値 `$(tablename)`を含む 1 行を挿入します。  

```
INSERT INTO AdventureWorks2012.dbo.VariableTest(Col1)
VALUES('$(tablename)');
GO
```
  
 `sqlcmd` プロンプトで、 `$(tablename)`に変数を設定していない場合、次のステートメントでは行が返されます。  
  
```
C:\> sqlcmd
>1 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = '$(tablename)';
>2 GO
>3 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = N'$(tablename)';
>4 GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

```
>1 Col1
>2 ------------------
>3 $(tablename)
>4
>5 (1 rows affected)
```

 変数 `MyVar` が `$(tablename)`に設定されている場合は次のようになります。  

```
>6 :setvar MyVar $(tablename)
```

 次のステートメントでは、行だけでなく、"'tablename' スクリプト変数が定義されていません。" というメッセージも返されます。  

```
>6 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = '$(tablename)';
>7 GO

>1 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = N'$(tablename)';
>2 GO
```

 次のステートメントでは行が返されます。  

```
>1 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = '$(MyVar)';
>2 GO
```

```
>1 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = N'$(MyVar)';
>2 GO
```
  
## <a name="see-also"></a>参照  
 [sqlcmd ユーティリティの使用](../../relational-databases/scripting/sqlcmd-use-the-utility.md)   
 [-b](../../tools/sqlcmd-utility.md)   
 [コマンド プロンプト ユーティリティ リファレンス &#40;データベース エンジン&#41;](../../tools/command-prompt-utility-reference-database-engine.md)  
  
  
