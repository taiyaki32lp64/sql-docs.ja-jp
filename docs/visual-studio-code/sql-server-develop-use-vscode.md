---
title: SQL Server に対して Visual Studio Code の mssql 拡張機能を使用する
titleSuffix: SQL Server
description: Visual Studio Code の mssql 拡張機能を使用して、SQL Server on Linux 用の Transact-SQL スクリプトを編集して実行します。
ms.topic: conceptual
ms.prod: sql
ms.technology: tools-other
ms.assetid: 9766ee75-32d3-4045-82a6-4c7968bdbaa6
author: markingmyname
ms.author: maghan
ms.date: 10/28/2019
ms.openlocfilehash: 91cc06b4d0d2791f91a26ecc1800859713267d9b
ms.sourcegitcommit: 82b70c39550402a2b0b327db32bf5ecf88b50d3c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73588986"
---
# <a name="use-visual-studio-code-to-create-and-run-transact-sql-scripts"></a>Visual Studio Code を使用して Transact-SQL スクリプトを作成して実行する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、Visual Studio Code の **mssql** 拡張機能を使用して SQL Server データベースを開発する方法について説明します。 Visual Studio Code はクロスプラットフォームであるため、Linux、macOS、および Windows で **mssql** 拡張機能を使用できます。

## <a name="install-and-start-visual-studio-code"></a>Visual Studio Code をインストールして起動する

Visual Studio Code は、拡張機能をサポートするクロスプラットフォームのグラフィカル コード エディターです。

1. お使いのコンピューターに [Visual Studio Code をダウンロードしてインストール](https://code.visualstudio.com/)します。

2. Visual Studio Code を起動します。

    >[!NOTE]
    >xrdp リモート デスクトップ セッションを介して接続しているときに Visual Studio Code が起動しない場合は、「[XRDP を使用して接続したときに Ubuntu で VS Code が動作しない](https://github.com/Microsoft/vscode/issues/3451)」を参照してください。

## <a name="install-the-mssql-extension"></a>mssql 拡張機能をインストールする

[Visual Studio Code の mssql 拡張機能](https://aka.ms/mssql-marketplace)を使用すると、SQL Server に接続し、Transact-SQL (T-SQL) を使用してクエリを実行し、その結果を表示できます。

1. Visual Studio Code で、 **[表示]**  >  **[コマンド パレット]** を選択する、**Ctrl** + **Shift** + **P** を押す、または **F1** を押して **[コマンド パレット]** を開きます。

2. **[コマンド パレット]** で、ドロップダウンから **[拡張機能:拡張機能のインストール]** を選択します。

3. **[拡張機能]** ウィンドウで、「*mssql*」と入力します。

4. **[SQL Server (mssql)]** 拡張機能を選択し、 **[インストール]** を選択します。

   ![mssql 拡張機能をインストールする](./media/sql-server-develop-use-vscode/vscode-extension.png)

5. インストールが完了したら、 **[再読み込み]** を選択して拡張機能を有効にします。

## <a name="create-or-open-a-sql-file"></a>SQL ファイルを作成するか開く

mssql 拡張機能では、言語モードが **SQL** に設定されている場合に、コード エディターで mssql コマンドと T-SQL IntelliSense を有効にできます。

1. **[ファイル]**  >  **[新しいファイル]** を選択するか、**Ctrl** + **N** を押します。 Visual Studio Code では、既定で新しいプレーン テキスト ファイルが開きます。 

2. 下部のステータス バーの **[プレーン テキスト]** を選択するか、**Ctrl** + **K**  >  **M** を押し、[言語] ドロップダウンから **[SQL]** を選択します。 

   ![SQL 言語モード](./media/sql-server-develop-use-vscode/vscode-language-mode.png)

   > [!NOTE]
   > この拡張機能を初めて使用する場合は、サポートされている SQL Server ツールが拡張機能によってインストールされます。

ファイル拡張子が *.sql* である既存のファイルを開くと、言語モードが自動的に SQL に設定されます。  

## <a name="connect-to-sql-server"></a>SQL Server への接続

次の手順に従って接続プロファイルを作成し、SQL Server に接続します。

1. **Ctrl** + **Shift** + **P** を押すか、**F1** を押して **[コマンド パレット]** を開きます。 

2. 「*sql*」と入力して mssql コマンドを表示するか、*sqlcon* と入力し、ドロップダウンから **[MS SQL:接続]** を選択します。

   ![mssql コマンド](./media/sql-server-develop-use-vscode/vscode-commands.png)

   >[!NOTE]
   >mssql コマンドを実行する前に、SQL ファイル (作成した空の SQL ファイルなど) がコード エディターでフォーカスされている必要があります。

3. **[MS SQL:接続プロファイルの管理]** コマンドを選択します。

4. 次に、 **[作成]** を選択して、お使いの SQL Server 用の新しい接続プロファイルを作成します。

5. 指示に従って、新しい接続プロファイルの接続プロパティを指定します。 それぞれの値を指定した後、**Enter** キーを押して続行します。

   | 接続プロパティ | [説明] |
   |---|---|
   | **サーバー名または ADO 接続文字列** | SQL Server インスタンス名を指定します。 ローカル コンピューター上の SQL Server インスタンスに接続するには、*localhost* を使用します。 リモート SQL Server に接続するには、ターゲットの SQL Server の名前か、その IP アドレスを入力します。 SQL Server コンテナーに接続するには、コンテナーのホスト コンピューターの IP アドレスを指定します。 ポートを指定する必要がある場合は、コンマを使用して名前と区別します。 たとえば、ポート 1401 でリッスンしているサーバーの場合は、「`<servername or IP>,1401`」と入力します。<br/><br/>別の方法として、お使いのデータベースの ADO 接続文字列をここに入力できます。 |
   | **データベース名** (省略可能) | 使用するデータベース。 既定のデータベースに接続するには、ここにデータベース名を指定しないでください。 |
   | **認証の種類** | **[統合]** または **[SQL ログイン]** を選択します。 |
   | **User name** | **[SQL ログイン]** を選択した場合は、サーバー上のデータベースにアクセスできるユーザーの名前を入力します。 |
   | **パスワード** | 指定したユーザーのパスワードを入力します。 |
   | **パスワードを保存する** | **Enter** キーを押すことで **[はい]** を選択して、パスワードを保存します。 **[いいえ]** を選択すると、接続プロファイルを使用するたびにパスワードの入力を求められます。 |
   | **プロファイル名** (省略可能) | 接続プロファイルの名前を入力します (*localhost プロファイル* など)。 |

   すべての値を入力して **Enter** キーを押すと、Visual Studio Code によって接続プロファイルが作成され、SQL Server に接続します。

   > [!TIP]
   > 接続に失敗した場合は、Visual Studio Code の **[出力]** パネルに表示されるエラー メッセージから問題を診断してください。 **[出力]** パネルを開くには、 **[表示]**  >  **[出力]** を選択します。 [接続のトラブルシューティングに関する推奨事項](../linux/sql-server-linux-troubleshooting-guide.md)も確認してください。

6. 下部のステータス バーで、接続を確認します。

   ![[接続状態]](./media/sql-server-develop-use-vscode/vscode-connection-status.png)

前の手順の代わりに、ユーザー設定ファイル (*settings.json*) 内に接続プロファイルを作成して編集することもできます。 この設定ファイルを開くには、 **[ファイル]**  >  **[ユーザー設定]**  >  **[設定]** を選択します。 詳細については、[接続プロファイルの管理](https://github.com/Microsoft/vscode-mssql/wiki/manage-connection-profiles)に関する記事を参照してください。

## <a name="create-a-sql-database"></a>SQL データベースを作成する

1. 先ほど開始した新しい SQL ファイル内で、「*sql*」と入力して、編集可能なコード スニペットの一覧を表示します。

   ![SQL スニペット](./media/sql-server-develop-use-vscode/vscode-sql-snippets.png)

2. **[sqlCreateDatabase]** を選択します。

3. スニペットに「`TutorialDB`」と入力して、'DatabaseName' を置き換えます。

   ```sql
   -- Create a new database called 'TutorialDB'
   -- Connect to the 'master' database to run this snippet
   USE master
   GO
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO
   ```

4. **Ctrl** + **Shift** + **E** を押して Transact-SQL コマンドを実行します。 クエリ ウィンドウで結果を確認します。

    ![データベースのメッセージを作成する](./media/sql-server-develop-use-vscode/vscode-create-database-messages.png)

    > [!TIP]
    > mssql コマンドのショートカットキーをカスタマイズできます。 「[ショートカットのカスタマイズ](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts)」を参照してください。

## <a name="create-a-table"></a>テーブルの作成

1. コード エディター ウィンドウの内容を削除します。

2. **Ctrl** + **Shift** + **P** を押すか、**F1** を押して **[コマンド パレット]** を開きます。

3. 「*sql*」と入力して mssql コマンドを表示するか、*sqluse* と入力し、 **[MS SQL:データベースの使用]** コマンドを選択します。

4. 新しい **TutorialDB** データベースを選択します。

   ![データベースを使用する](./media/sql-server-develop-use-vscode/vscode-use-database.png)

5. コード エディターで、「*sql*」と入力してスニペットを表示し、 **[sqlCreateTable]** を選択した後、**Enter** キーを押します。

6. スニペットに、テーブル名として「`Employees`」と入力します。

7. **Tab** キーを押して次のフィールドに移動し、スキーマ名として「`dbo`」と入力します。

8. 列の定義を次の列に置き換えます。

   ```sql
   EmployeesId INT NOT NULL PRIMARY KEY,
   Name [NVARCHAR](50)  NOT NULL,
   Location [NVARCHAR](50)  NOT NULL
   ```

9. **Ctrl** + **Shift** + **E** を押してテーブルを作成します。

## <a name="insert-and-query"></a>挿入とクエリ

1. 次のステートメントを追加して、**Employees** テーブルに 4 つの行を挿入します。

   ```sql
   -- Insert rows into table 'Employees'
   INSERT INTO Employees
      ([EmployeesId],[Name],[Location])
   VALUES
      ( 1, N'Jared', N'Australia'),
      ( 2, N'Nikita', N'India'),
      ( 3, N'Tom', N'Germany'),
      ( 4, N'Jake', N'United States')
   GO
   -- Query the total count of employees
   SELECT COUNT(*) as EmployeeCount FROM dbo.Employees;
   -- Query all employee information
   SELECT e.EmployeesId, e.Name, e.Location
   FROM dbo.Employees as e
   GO
   ```

   入力している間に、T-SQL IntelliSense によってステートメントが完了します。

   ![T-SQL IntelliSense](./media/sql-server-develop-use-vscode/vscode-intellisense.png)

   > [!TIP]
   > mssql 拡張機能には、INSERT ステートメントと SELECT ステートメントを作成するために役立つコマンドもあります。 これらは、前の例では使用されていません。

2. **Ctrl** + **Shift** + **E** を押してコマンドを実行します。 2 つの結果セットが **[結果]** ウィンドウに表示されます。

   ![[結果]](./media/sql-server-develop-use-vscode/vscode-result-grid.png)

## <a name="view-and-save-the-result"></a>結果を表示して保存する

1. **[表示]**  >  **[エディターのレイアウト]**  >  **[Flip Layout]\(レイアウトの入れ替え\)** を選択して、垂直または水平分割レイアウトに切り替えます。

2. **[結果]** パネル見出しと **[メッセージ]** パネル見出しを選択して、これらのパネルを折りたたむか展開します。

   ![見出しを切り替える](./media/sql-server-develop-use-vscode/vscode-toggle-messages-pannel.png)

   > [!TIP]
   > mssql 拡張機能の既定の動作をカスタマイズできます。 「[拡張オプションのカスタマイズ](https://github.com/Microsoft/vscode-mssql/wiki/customize-options)」を参照してください。

3. これらの結果にズームインするには、2 番目の結果グリッドの [最大化] グリッド アイコンを選択します。

   ![グリッドを最大化する](./media/sql-server-develop-use-vscode/vscode-maximize-grid.png)

   > [!NOTE]
   > [最大化] アイコンは、T-SQL スクリプトで 2 つ以上の結果グリッドが生成される場合に表示されます。

4. グリッドを右クリックして、グリッドのコンテキスト メニューを開きます。

   ![コンテキスト メニュー](./media/sql-server-develop-use-vscode/vscode-grid-context-menu.png)

5. **[すべて選択]** を選択します。

6. グリッドのコンテキスト メニューをもう一度開き、 **[JSON として保存]** を選択して、結果を *.json* ファイルに保存します。

7. JSON ファイルのファイル名を指定します。

8. JSON ファイルが 保存されたことを確認し、Visual Studio Code で開きます。

   ![JSON として保存する](./media/sql-server-develop-use-vscode/vscode-save-as-json.png)

SQL スクリプトを保存しておき、後で管理や大規模な開発プロジェクトのために実行する必要がある場合は、 *.sql* 拡張子を付けてスクリプトを保存します。

## <a name="next-steps"></a>次の手順

T-SQL を初めて使用する場合は、「[チュートリアル:Transact-SQL ステートメントの作成](https://docs.microsoft.com/sql/t-sql/tutorial-writing-transact-sql-statements)」と「[Transact-SQL リファレンス (データベース エンジン)](https://docs.microsoft.com/sql/t-sql/language-reference)」を参照してください。

mssql 拡張機能の使用または開発の貢献に関する詳細については、[mssql 拡張機能プロジェクト Wiki](https://github.com/Microsoft/vscode-mssql/wiki) を参照してください。

Visual Studio Code の使用方法の詳細については、[Visual Studio Code のドキュメント](https://code.visualstudio.com/docs)を参照してください。