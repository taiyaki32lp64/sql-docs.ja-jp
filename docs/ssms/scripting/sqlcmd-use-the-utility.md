---
title: sqlcmd ユーティリティの使用 | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- Transact-SQL statements, executing
- command prompt utilities [SQL Server], sqlcmd
- statements [SQL Server], executing
- sqlcmd utility, about sqlcmd utility
ms.assetid: 3ec89119-7314-43ef-9e91-12e72bb63d62
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7fd1c2eafec0d0dd832e4d01d43195d7ec175485
ms.sourcegitcommit: ffb87aa292fc9b545c4258749c28df1bd88d7342
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2019
ms.locfileid: "71816612"
---
# <a name="sqlcmd---use-the-utility"></a>sqlcmd - ユーティリティの使用
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  **sqlcmd** ユーティリティは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントおよびスクリプトを対話形式でアドホック実行したり、 [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト タスクを自動化したりするためのコマンドライン ユーティリティです。 **sqlcmd** を対話形式で使用したり、 **sqlcmd**を使用して実行できるスクリプト ファイルを作成したりするには、ユーザーが [!INCLUDE[tsql](../../includes/tsql-md.md)]を理解している必要があります。 **sqlcmd** ユーティリティは一般的に次のように使用されます。  
  
-   コマンド プロンプトでの操作と同様、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを入力します。 結果はコマンド プロンプトに表示されます。 コマンド プロンプト ウィンドウを開くには、Windows の検索ボックスに「cmd」と入力し、"**コマンド プロンプト**" をクリックして開きます。 コマンド プロンプトで「 **sqlcmd** 」と入力し、その後に必要なオプションのリストを入力します。 **sqlcmd**でサポートされるオプションの一覧については、「 [sqlcmd ユーティリティ](../../tools/sqlcmd-utility.md)」を参照してください。  
  
-   実行する **ステートメントを 1 つ指定するか、実行する** ステートメントの入ったテキスト ファイルをユーティリティに指定して、 [!INCLUDE[tsql](../../includes/tsql-md.md)] sqlcmd [!INCLUDE[tsql](../../includes/tsql-md.md)] ジョブを実行します。 出力先はコマンド プロンプトにすることもできますが、通常はテキスト ファイルに出力されます。  
  
-   [クエリ エディターの](../../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md) SQLCMD モード [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   SQL Server 管理オブジェクト (SMO)  
  
-   SQL Server エージェントの CmdExec ジョブ  
  
## <a name="typically-used-sqlcmd-options"></a>一般的な sqlcmd オプション  
  
-   サーバー オプション ( **-S**) は、**sqlcmd** が接続する [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを指定します。  
  
-   認証オプション ( **-E**、 **-U**、 **-P**) は、**sqlcmd** が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続するために使用する資格情報を指定します。 **注:** オプション **-E** は既定値のため、指定する必要はありません。  
  
-   入力オプション ( **-Q**、 **-q**、 **-i**) は、**sqlcmd** への入力場所を指定します。  
  
-   出力オプション ( **-o**) は、**sqlcmd** が出力を格納するファイルを指定します。  
  
## <a name="connect-to-the-sqlcmd-utility"></a>sqlcmd ユーティリティに接続する  
  
-   Windows 認証を使用して既定のインスタンスに接続し、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを対話的に実行します。  
  
    ```  
    sqlcmd -S <ComputerName>  
    ```  
  
    > **注:** 上記の例で **-E** が指定されていないのは、このスイッチが既定値であるためです。ここでは **sqlcmd** から Windows 認証を使用して既定のインスタンスに接続しています。  
  
-   Windows 認証を使用して名前付きインスタンスに接続し、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを対話的に実行します。  
  
    ```  
    sqlcmd -S <ComputerName>\<InstanceName>  
    ```  
  
     内の複数の  
  
    ```  
    sqlcmd -S .\<InstanceName>  
    ```  
  
-   Windows 認証を使用して名前付きインスタンスに接続し、入出力ファイルを指定します。  
  
    ```  
    sqlcmd -S <ComputerName>\<InstanceName> -i <MyScript.sql> -o <MyOutput.rpt>  
    ```  
  
-   Windows 認証を使用してローカル コンピューター上の既定のインスタンスに接続し、クエリを実行して、クエリの完了後も **sqlcmd** を実行状態にしておきます。  
  
    ```  
    sqlcmd -q "SELECT * FROM AdventureWorks2012.Person.Person"  
    ```  
  
-   Windows 認証を使用してローカル コンピューター上の既定のインスタンスに接続し、クエリを実行して、ファイルへの出力を指定し、クエリの完了後に **sqlcmd** を終了します。  
  
    ```  
    sqlcmd -Q "SELECT * FROM AdventureWorks2012.Person.Person" -o MyOutput.txt  
    ```  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用して名前付きインスタンスに接続し、 [!INCLUDE[tsql](../../includes/tsql-md.md)] sqlcmd **からパスワードの入力を求めて** ステートメントを対話的に実行します。  
  
    ```  
    sqlcmd -U MyLogin -S <ComputerName>\<InstanceName>  
    ```  
  
    > **ヒント** **sqlcmd** ユーティリティでサポートされているオプションの一覧を表示するには、 `sqlcmd -?`を実行してください。  
  
## <a name="run-transact-sql-statements-interactively-by-using-sqlcmd"></a>sqlcmd を使用して Transact-SQL ステートメントを対話的に実行する  
 コマンド プロンプト ウィンドウでは、 **sqlcmd** ユーティリティを対話的に使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行できます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] sqlcmd **を使用して対話的に**ステートメントを実行するには、入力ファイルまたはクエリを指定するための **-Q**、 **-q**、 **-Z**、または **-i** オプションを使用せずにこのユーティリティを実行します。 例:  
  
 `sqlcmd -S <ComputerName>\<InstanceName>`  
  
 入力ファイルやクエリを指定せずにこのコマンドを実行すると、 **sqlcmd** は指定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続した後、新しい行に `1>` と表示し、その隣でアンダースコアを点滅させます。これを **sqlcmd** プロンプトと呼びます。 `1` は、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの最初の行であることを示します。この **sqlcmd** プロンプトが [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの入力開始位置になります。  
  
 **sqlcmd** プロンプトでは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントと、 **GO** や **EXIT** などの **sqlcmd**コマンドの両方を入力できます。 各 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは、ステートメント キャッシュと呼ばれるバッファーに格納されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] GO **コマンドを入力し、Enter キーを押すと、これらのステートメントが** に送信されます。 **sqlcmd**を終了するには、新しい行の先頭で「 **EXIT** 」または「 **QUIT** 」と入力します。  
  
 ステートメント キャッシュをクリアするには、「 **:RESET**」と入力します。 「 **^C** 」と入力すると、 **sqlcmd** は終了します。 **^C** は、 **GO** コマンドが実行された後に、ステートメント キャッシュの実行を停止するためにも使用できます。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは、 **sqlcmd** プロンプトで **sqlcmd** プロンプトと呼びます。 起動したエディターで [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを編集して、エディターを終了すると、変更された [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントがコマンド ウィンドウに表示されます。 変更された **ステートメントを実行するには、「** GO [!INCLUDE[tsql](../../includes/tsql-md.md)] 」と入力します。  
  
## <a name="quoted-strings"></a>引用符で囲まれた文字列  
 引用符で囲まれた文字列は、前処理がまったく行われずそのまま使用されます。ただし、例外として、2 つの連続する引用符を入力することで、引用符自体を文字列に挿入できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、この文字の並びを 1 つの引用符として扱います (ただし、この変換はサーバーで行われます)。スクリプト変数が文字列内に存在する場合は展開されません。  
  
 例:  
  
 `sqlcmd`  
  
 `PRINT "Length: 5"" 7'";`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Length: 5" 7'`  
  
## <a name="strings-that-span-multiple-lines"></a>複数行の文字列  
 **sqlcmd** では、複数行の文字列になるスクリプトがサポートされています。 たとえば、次の `SELECT` ステートメントは複数行にわたって記述されていますが、「 `GO`」と入力して &lt;localizedText&gt;Enter&lt;/localizedText&gt; キーを押すと、1 つの文字列として実行されます。  
  
 `SELECT First line`  
  
 `FROM Second line`  
  
 `WHERE Third line;`  
  
 `GO`  
  
## <a name="interactive-sqlcmd-example"></a>対話的な sqlcmd の例  
 **sqlcmd** を対話的に実行する例を次に示します。  
  
 コマンド プロンプト ウィンドウを開くと、次のような行が表示されます。  
  
 `C:\> _`  
  
 これは、フォルダー `C:\` が現在のフォルダーであり、ファイル名を指定すると Windows によってそのフォルダー内のファイルが検索されることを意味します。  
  
 「 **sqlcmd** 」と入力して、ローカル コンピューターの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンスに接続します。コマンド プロンプト ウィンドウの内容は次のようになります。  
  
 `C:\>sqlcmd`  
  
 `1> _`  
  
 これは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスへの接続が確立され、 `sqlcmd` で [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントと `sqlcmd` コマンドを実行できるようになったことを示しています。 `1>` の隣で点滅しているアンダースコアは、入力したステートメントやコマンドが表示される位置を示す `sqlcmd` プロンプトです。 ここで、「 **USE AdventureWorks2012** 」と入力して &lt;localizedText&gt;Enter&lt;/localizedText&gt; キーを押した後、「 **GO** 」と入力してもう一度 &lt;localizedText&gt;Enter&lt;/localizedText&gt; キーを押します。 コマンド プロンプト ウィンドウの内容は次のようになります。  
  
 `sqlcmd`  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Changed database context to 'AdventureWorks2012'.`  
  
 `1> _`  
  
 「 `USE AdventureWorks2012` 」と入力した後で &lt;localizedText&gt;Enter&lt;/localizedText&gt; キーを押すことにより、新しい行を開始するよう `sqlcmd` に要求します。 「 `GO,` 」と入力してから Enter キーを押すことにより、 `sqlcmd` ステートメントを `USE AdventureWorks2012` のインスタンスに送信するよう [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に指示します。 `sqlcmd` により、 `USE` ステートメントが正常に完了したことを示すメッセージが返されます。その後、 `1>` プロンプトが表示され、新しいステートメントやコマンドを入力できるようになります。  
  
 次の例では、 `SELECT` ステートメント、 `GO` を実行するための `SELECT`、および `EXIT` を終了するための `sqlcmd`を入力した場合に、コマンド プロンプト ウィンドウに表示される内容を示します。  
  
 `sqlcmd`  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 `SELECT TOP (3) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `BusinessEntityID   FirstName                 LastName`  
  
 `----------- -------------------------------- -----------`  
  
 `1           Syed                             Abbas`  
  
 `2           Catherine                        Abel`  
  
 `3           Kim                              Abercrombie`  
  
 `(3 rows affected)`  
  
 `1> EXIT`  
  
 `C:\>`  
  
 行 `3> GO` の後の行は、 `SELECT` ステートメントの出力です。 出力の生成後、 `sqlcmd` により `sqlcmd` プロンプトがリセットされ、 `1>`が表示されます。 行 `EXIT` で「 `1>`」と入力すると、最初にコマンド プロンプト ウィンドウを開いたときと同じ行が表示されます。 これは、 `sqlcmd` のセッションを終了したことを示します。 その状態で再度 `EXIT` コマンドを入力すると、コマンド プロンプト ウィンドウを閉じることができます。  
  
## <a name="running-transact-sql-script-files-using-sqlcmd"></a>sqlcmd を使用した Transact-SQL スクリプト ファイルの実行  
 **sqlcmd** を使用してデータベース スクリプト ファイルを実行できます。 スクリプト ファイルは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、 **sqlcmd** コマンド、およびスクリプト変数が混在したテキスト ファイルです。 変数をスクリプト化する方法の詳細については、「 [sqlcmd でのスクリプト変数の使用](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)」をご覧ください。 スクリプト ファイル内のステートメント、コマンド、およびスクリプト変数に対して**sqlcmd** で行われる処理は、対話的に入力したステートメントやコマンドの処理と似ています。 **sqlcmd** が対話入力の場合と大きく異なる点は、ユーザーがステートメント、コマンド、およびスクリプト変数を入力するまで待機するのではなく、入力ファイルを最後まで中断することなく読み取るという点です。  
  
 データベース スクリプト ファイルの作成方法はいくつかあります。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ステートメントのセットを対話的に作成およびデバッグして、クエリ ウィンドウの内容をスクリプト ファイルとして保存する。  
  
-   メモ帳などのテキスト エディターを使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを含んだテキスト ファイルを作成する。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-running-a-script-by-using-sqlcmd"></a>A. sqlcmd を使用したスクリプトの実行  
 メモ帳を起動し、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを入力します。  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 `SELECT TOP (3) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 `MyFolder` というフォルダーを作成し、スクリプトを `MyScript.sql` ファイルとして `C:\MyFolder`フォルダーに保存します。 コマンド プロンプトで、次のコマンドを入力してスクリプトを実行し、結果を `MyOutput.txt` の `MyFolder`に出力します。  
  
 `sqlcmd -i C:\MyFolder\MyScript.sql -o C:\MyFolder\MyOutput.txt`  
  
 メモ帳で `MyOutput.txt` を開くと、次のような内容が表示されます。  
  
 `Changed database context to 'AdventureWorks2012'.`  
  
 `BusinessEntityID FirstName   LastName`  
  
 `---------------- ----------- -----------`  
  
 `1                Syed        Abbas`  
  
 `2                Catherine   Abel`  
  
 `3                Kim         Abercrombie`  
  
 `(3 rows affected)`  
  
### <a name="b-using-sqlcmd-with-a-dedicated-administrative-connection"></a>B. sqlcmd と専用管理者接続の併用  
 次の例では、 `sqlcmd` を使用して、ブロッキングの問題が発生しているサーバーに専用管理者接続 (DAC) で接続します。  
  
 `C:\>sqlcmd -S ServerName -A`  
  
 `1> SELECT session_id, blocking_session_id FROM sys.dm_exec_requests WHERE blocking_session_id <> 0;`  
  
 `2> GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `session_id   blocking_session_id`  
  
 `------ -------`  
  
 `62       64`  
  
 `(1 rows affected)`  
  
 `sqlcmd` を使用してブロック中のプロセスを終了します。  
  
 `1> KILL 64;`  
  
 `2> GO`  
  
### <a name="c-using-sqlcmd-to-execute-a-stored-procedure"></a>C. sqlcmd を使用したストアド プロシージャの実行  
 次の例では、 `sqlcmd`を使用してストアド プロシージャを実行します。 次のストアド プロシージャを作成します。  
  
 `USE AdventureWorks2012;`  
  
 `IF OBJECT_ID ( ' dbo.ContactEmailAddress, 'P' ) IS NOT NULL`  
  
 `DROP PROCEDURE dbo.ContactEmailAddress;`  
  
 `GO`  
  
 `CREATE PROCEDURE dbo.ContactEmailAddress`  
  
 `(`  
  
 `@FirstName nvarchar(50)`  
  
 `,@LastName nvarchar(50)`  
  
 `)`  
  
 `AS`  
  
 `SET NOCOUNT ON`  
  
 `SELECT EmailAddress`  
  
 `FROM Person.Person`  
  
 `WHERE FirstName = @FirstName`  
  
 `AND LastName = @LastName;`  
  
 `SET NOCOUNT OFF`  
  
 `sqlcmd` プロンプトで、次のコマンドを入力します。  
  
 `C:\sqlcmd`  
  
 `1> :Setvar FirstName Gustavo`  
  
 `1> :Setvar LastName Achong`  
  
 `1> EXEC dbo.ContactEmailAddress $(Gustavo),$(Achong)`  
  
 `2> GO`  
  
 `EmailAddress`  
  
 `-----------------------------`  
  
 `gustavo0@adventure-works.com`  
  
### <a name="d-using-sqlcmd-for-database-maintenance"></a>D. sqlcmd を使用したデータベースのメンテナンス  
 次の例では、 `sqlcmd` を使用してデータベースのメンテナンス タスクを実行します。 次のコードを使用して `C:\BackupTemplate.sql` を作成します。  
  
 `USE master;`  
  
 `BACKUP DATABASE [$(db)] TO DISK='$(bakfile)';`  
  
 `sqlcmd` プロンプトで、次のコマンドを入力します。  
  
 `C:\ >sqlcmd`  
  
 `1> :connect <server>`  
  
 `Sqlcmd: Successfully connected to server <server>.`  
  
 `1> :setvar db msdb`  
  
 `1> :setvar bakfile c:\msdb.bak`  
  
 `1> :r c:\BackupTemplate.sql`  
  
 `2> GO`  
  
 `Changed database context to 'master'.`  
  
 `Processed 688 pages for database 'msdb', file 'MSDBData' on file 2.`  
  
 `Processed 5 pages for database 'msdb', file 'MSDBLog' on file 2.`  
  
 `BACKUP DATABASE successfully processed 693 pages in 0.725 seconds (7.830 MB/sec)`  
  
### <a name="e-using-sqlcmd-to-execute-code-on-multiple-instances"></a>E. sqlcmd を使用した複数のインスタンスでのコードの実行  
 ファイル内の次のコードは、2 つのインスタンスに接続するスクリプトです。 2 番目のインスタンスへの接続の前に `GO` が記述されていることに注意してください。  
  
 `:CONNECT <server>\,<instance1>`  
  
 `EXEC dbo.SomeProcedure`  
  
 `GO`  
  
 `:CONNECT <server>\,<instance2>`  
  
 `EXEC dbo.SomeProcedure`  
  
 `GO`  
  
### <a name="e-returning-xml-output"></a>E. XML 出力の取得  
 次の例では、XML 出力が、連続するストリームでフォーマットされずに返されます。  
  
 `C:\>sqlcmd -d AdventureWorks2012`  
  
 `1> :XML ON`  
  
 `1> SELECT TOP 3 FirstName + ' ' + LastName + ', '`  
  
 `2> FROM Person.Person`  
  
 `3> GO`  
  
 `Syed Abbas, Catherine Abel, Kim Abercrombie,`  
  
### <a name="f-using-sqlcmd-in-a-windows-script-file"></a>F. Windows スクリプト ファイルでの sqlcmd の使用  
 **などの**sqlcmd `sqlcmd -i C:\InputFile.txt -o C:\OutputFile.txt,` コマンドは、.bat ファイルで VBScript と共に実行できます。 この場合、対話型のオプションは使用しないでください。 また、.bat ファイルを実行するコンピューターには**sqlcmd** がインストールされている必要があります。  
  
 最初に、次の 4 つのファイルを作成します。  
  
-   C:\badscript.sql  
  
    ```  
    SELECT batch_1_this_is_an_error  
    GO  
    SELECT 'batch #2'  
    GO  
    ```  
  
-   C:\goodscript.sql  
  
    ```  
    SELECT 'batch #1'  
    GO  
    SELECT 'batch #2'  
    GO  
    ```  
  
-   C:\returnvalue.sql  
  
    ```  
    :exit(select 100)  
    @echo off  
    C:\windowsscript.bat  
    @echo off  
  
    echo Running badscript.sql  
    sqlcmd -i badscript.sql -b -o out.log  
    if not errorlevel 1 goto next1  
    echo == An error occurred   
  
    :next1  
  
    echo Running goodscript.sql  
    sqlcmd -i goodscript.sql -b -o out.log  
    if not errorlevel 1 goto next2  
    echo == An error occurred   
  
    :next2  
    echo Running returnvalue.sql  
    sqlcmd -i returnvalue.sql -o out.log  
    echo SQLCMD returned %errorlevel% to the command shell  
  
    :exit  
    ```  
  
-   C:\windowsscript.bat  
  
    ```  
    @echo off  
  
    echo Running badscript.sql  
    sqlcmd -i badscript.sql -b -o out.log  
    if not errorlevel 1 goto next1  
    echo == An error occurred   
  
    :next1  
  
    echo Running goodscript.sql  
    sqlcmd -i goodscript.sql -b -o out.log  
    if not errorlevel 1 goto next2  
    echo == An error occurred   
  
    :next2  
    echo Running returnvalue.sql  
    sqlcmd -i returnvalue.sql -o out.log  
    echo SQLCMD returned %errorlevel% to the command shell  
  
    :exit  
    ```  
  
 その後、コマンド プロンプトで次のように `C:\windowsscript.bat`を実行します。  
  
 `C:\>windowsscript.bat`  
  
 `Running badscript.sql`  
  
 `== An error occurred`  
  
 `Running goodscript.sql`  
  
 `Running returnvalue.sql`  
  
 `SQLCMD returned 100 to the command shell`  
  
### <a name="g-using-sqlcmd-to-set-encryption-on-azure-sql-database"></a>G. sqlcmd を使用した Azure SQL Database での暗号化の設定  
 **データへの接続時に**sqlcmd [!INCLUDE[ssSDS](../../includes/sssds-md.md)] を実行して、通信を暗号化するかどうか、および証明書を信頼するかどうかを指定できます。 次の 2 つの **sqlcmd**``オプションを使用できます。  
  
-   暗号化された接続を要求するには、クライアント側で -N スイッチを使用します。 このオプションは、ADO.net オプションの `ENCRYPT = true`と同等です。  
  
-   サーバーの証明書を信頼し、その有効性を検証しないように設定するには、クライアント側で -C スイッチを使用します。 このオプションは、ADO.net オプションの `TRUSTSERVERCERTIFICATE = true`と同等です。  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] サービスは、SQL Server インスタンスで使用できるすべての `SET` オプションをサポートするわけではありません。 次の `SET` オプションを `ON` または `OFF`に設定すると、エラーがスローされます。  
  
-   [SET ANSI_DEFAULTS]  
  
-   [SET ANSI_NULLS]  
  
-   SET REMOTE_PROC_TRANSACTIONS  
  
-   SET ANSI_NULL_DEFAULT  
  
 次の SET オプションは例外をスローしませんが、使用できません。 これらのオプションは非推奨とされます：  
  
-   [SET CONCAT_NULL_YIELDS_NULL]  
  
-   [SET ANSI_PADDING]  
  
-   [SET QUERY_GOVERNOR_COST_LIMIT]  
  
#### <a name="syntax"></a>構文  
 次の構文の例は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client Provider の設定に `ForceProtocolEncryption = False`、 `Trust Server Certificate = No`  
  
 Windows 資格情報を使用して接続し、通信を暗号化する:  
  
```  
SQLCMD -E -N  
  
```  
  
 Windows 資格情報を使用して接続し、サーバーの証明書を信頼する:  
  
```  
SQLCMD -E -C  
  
```  
  
 Windows 資格情報を使用して接続し、通信を暗号化して、サーバーの証明書を信頼する:  
  
```  
SQLCMD -E -N -C  
  
```  
  
 次の構文の例は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client Provider の設定に `ForceProtocolEncryption = True`と `TrustServerCertificate = Yes`が含まれる場合を示しています。  
  
 Windows 資格情報を使用して接続し、通信を暗号化して、サーバーの証明書を信頼する:  
  
```  
SQLCMD -E  
  
```  
  
 Windows 資格情報を使用して接続し、通信を暗号化して、サーバーの証明書を信頼する:  
  
```  
SQLCMD -E -N  
  
```  
  
 Windows 資格情報を使用して接続し、通信を暗号化して、サーバーの証明書を信頼する:  
  
```  
SQLCMD -E -C  
  
```  
  
 Windows 資格情報を使用して接続し、通信を暗号化して、サーバーの証明書を信頼する:  
  
```  
SQLCMD -E -N -C  
  
```  
  
 プロバイダーで `ForceProtocolEncryption = True` が指定されている場合、接続文字列で `Encrypt=No` が設定されていても暗号化が有効になります。  
  
## <a name="more-about-sqlcmd"></a>sqlcmd に関する詳細情報  
 [sqlcmd ユーティリティ](../../tools/sqlcmd-utility.md)   
 [sqlcmd でのスクリプト変数の使用](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)   
 [クエリ エディターによる SQLCMD スクリプトの編集](../../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)   
 [ジョブ ステップの管理](../../ssms/agent/manage-job-steps.md)   
 [CmdExec ジョブ ステップの作成](../../ssms/agent/create-a-cmdexec-job-step.md)  
  
  
