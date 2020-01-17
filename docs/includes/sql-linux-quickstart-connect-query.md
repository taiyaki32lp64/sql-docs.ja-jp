## <a name="connect-locally"></a>ローカル接続

次の手順では、**sqlcmd** を使用して新しい SQL Server インスタンスにローカル接続します。

1. **sqlcmd** に SQL Server 名 (-S)、ユーザー名 (-U)、およびパスワード (-P) のパラメーターを指定して実行します。 このチュートリアルでは、ローカルに接続するため、サーバー名は `localhost` です。 ユーザー名は `SA` で、パスワードはセットアップ時に SA アカウントに指定したものです。

   ```bash
   sqlcmd -S localhost -U SA -P '<YourPassword>'
   ```

   > [!TIP]
   > コマンド ラインでパスワードを省略すると、入力を求められます。

   > [!TIP]
   > 後でリモート接続する場合は、 **-S** パラメーターとしてコンピューター名または IP アドレスを指定し、ファイアウォールでポート 1433 が開いていることを確認してください。

1. 成功すると、**sqlcmd** コマンド プロンプト `1>` が表示されます。

1. 接続エラーが発生した場合は、まずエラー メッセージから問題を診断します。 次に、[接続のトラブルシューティングに関する推奨事項](../linux/sql-server-linux-troubleshooting-guide.md#connection)を確認します。

## <a name="create-and-query-data"></a>データの作成とクエリ
以下のセクションでは、**sqlcmd** を使用して新しいデータベースを作成し、データを追加して簡単なクエリを実行します。

### <a name="create-a-new-database"></a>新しいデータベースの作成

次の手順では、`TestDB` という名前の新しいデータベースを作成します。

1. **sqlcmd** のコマンド プロンプトに次の Transact-SQL コマンドを貼り付け、テスト データベースを作成します。

   ```sql
   CREATE DATABASE TestDB
   ```

1. 次の行に、サーバー上のすべてのデータベースの名前を返すクエリを記述します。

   ```sql
   SELECT Name from sys.Databases
   ```

1. 前の 2 つのコマンドは、すぐに実行されていません。 前のコマンドを実行するには、新しい行に「`GO`」と入力する必要があります。

   ```sql
   GO
   ```

> [!TIP]
> Transact-SQL ステートメントおよびクエリの作成の詳細については、「[チュートリアル:Transact-SQL ステートメントの作成](../t-sql/tutorial-writing-transact-sql-statements.md)」を参照してください。

### <a name="insert-data"></a>データの挿入

次に、新しいテーブル `Inventory` を作成し、2 つの新しい行を挿入します。

1. **sqlcmd** のコマンド プロンプトで、コンテキストを新しい `TestDB` データベースに切り替えます。

   ```sql
   USE TestDB
   ```

1. `Inventory` という名前の新しいテーブルを作成します。

   ```sql
   CREATE TABLE Inventory (id INT, name NVARCHAR(50), quantity INT)
   ```

1. 新しいテーブルにデータを挿入します。

   ```sql
   INSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);
   ```

1. 「`GO`」と入力して前のコマンドを実行します。

   ```sql
   GO
   ```

### <a name="select-data"></a>データの選択

ここで、`Inventory` テーブルからデータを返すクエリを実行します。

1. **sqlcmd** のコマンド プロンプトで、数量が 152 より大きい`Inventory` テーブルから行を返すクエリを入力します。

   ```sql
   SELECT * FROM Inventory WHERE quantity > 152;
   ```

1. 次のコマンドを実行します。

   ```sql
   GO
   ```

### <a name="exit-the-sqlcmd-command-prompt"></a>sqlcmd コマンド プロンプトの終了

**sqlcmd** セッションを終了するには、「`QUIT`」と入力します。

```sql
QUIT
```

## <a name="performance-best-practices"></a>パフォーマンスのベスト プラクティス

SQL Server on Linux をインストールしたら、運用シナリオでのパフォーマンスの向上に、Linux と SQL Server の構成のベスト プラクティスを確認してください。 詳細については、「[パフォーマンスのベスト プラクティスと SQL Server on Linux の構成ガイドライン](../linux/sql-server-linux-performance-best-practices.md)」を参照してください。

## <a name="cross-platform-data-tools"></a>クロスプラットフォーム データツール

SQL Server の管理には、**sqlcmd** 以外に次のクロスプラットフォーム ツールを使用できます。

|||
|---|---|
| [Azure Data Studio](../azure-data-studio/index.md) | クロスプラットフォームの GUI データベース管理ユーティリティ。 |
| [Visual Studio Code](../linux/sql-server-linux-develop-use-vscode.md) | Transact-SQL ステートメントを mssql 拡張機能を使用して実行するクロスプラットフォーム GUI コードエディター。 |
| [PowerShell Core](../linux/sql-server-linux-manage-powershell-core.md) | コマンドレットを使用する、クロスプラットフォームの自動化および構成ツール。 |
| [mssql-cli](https://github.com/dbcli/mssql-cli/tree/master/doc) | Transact-SQL コマンドを実行するクロスプラットフォーム コマンドライン インターフェイス。 |

## <a name="connecting-from-windows"></a>Windows からの接続

Windows 上の SQL Server ツールは、あらゆるリモート SQL Server インスタンスへの接続と同じ方法で Linux 上の SQL Server インスタンスに接続します。

Linux コンピューターに接続できる Windows コンピューターがある場合は、**sqlcmd** を実行する Windows コマンド プロンプトから、このトピックと同じ手順を試してみてください。 localhost ではなくターゲットの Linux コンピューター名または IP アドレスを使用していることを確認し、TCP ポート 1433 が開いていることを確かめます。 Windows からの接続に問題がある場合は、[接続のトラブルシューティングに関する推奨事項](../linux/sql-server-linux-troubleshooting-guide.md#connection)を参照してください。

Windows で実行し、Linux 上の SQL Server に接続するその他のツールについては、以下を参照してください。

- [SQL Server Management Studio (SSMS)](../linux/sql-server-linux-manage-ssms.md)
- [Windows PowerShell](../linux/sql-server-linux-manage-powershell.md)
- [SQL Server Data Tools (SSDT)](../linux/sql-server-linux-develop-use-ssdt.md)

## <a name="other-deployment-scenarios"></a>その他の展開シナリオ

他のインストール シナリオについては、次のリソースを参照してください。

|||
|---|---|
| [アップグレード](../linux/sql-server-linux-setup.md#upgrade) | Linux 上の SQL Server のアップグレード方法および既存のインストールについて説明する |
| [アンインストール](../linux/sql-server-linux-setup.md#uninstall) | Linux 上の SQL Server をアンインストールする |
| [無人インストール](../linux/sql-server-linux-setup.md#unattended) | プロンプトを表示せずにインストールするスクリプトを作成する方法を説明する |
| [オフライン インストール](../linux/sql-server-linux-setup.md#offline) | オフライン インストール パッケージを手動でダウンロードする方法を説明する |

> [!TIP]
> よく寄せられる質問に対する回答については、「[SQL Server on Linux に関する FAQ](../linux/sql-server-linux-faq.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [SQL Server on Linux のチュートリアルの参照](../linux/sql-server-linux-migrate-restore-database.md)