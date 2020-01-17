---
title: Transact-SQL (VS Code) を使用して SSIS パッケージを実行する | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cdd1dc130efb795b957911c51d5d8c2243522d38
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71281618"
---
# <a name="run-an-ssis-package-from-visual-studio-code-with-transact-sql"></a>Transact-SQL を使用して Visual Studio Code から SSIS パッケージを実行する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


このクイックスタートでは、Visual Studio Code を使用して SSIS カタログ データベースに接続し、Transact-SQL ステートメントを使用して SSIS カタログに格納されている SSIS パッケージを実行する方法を示します。

Visual Studio Code は、拡張機能をサポートする Windows、macOS、および Linux のコード エディターです。拡張機能には、Microsoft SQL Server、Azure SQL Database、または Azure SQL Data Warehouse に接続するための `mssql` 拡張機能が含まれます。 VS Code の詳細については、「[Visual Studio Code](https://code.visualstudio.com/)」を参照してください。

## <a name="prerequisites"></a>Prerequisites

開始する前に、最新バージョンの Visual Studio Code がインストールされ、`mssql` 拡張機能が読み込まれていることを確認します。 これらのツールをダウンロードするには、次のページを参照してください。
-   [Visual Studio Code のダウンロード](https://code.visualstudio.com/Download)
-   [mssql 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="supported-platforms"></a>サポートされているプラットフォーム

このクイックスタートの情報を使用して、次のプラットフォームで SSIS パッケージを実行することができます。

-   SQL Server on Windows。

-   Azure SQL Database。 Azure でのパッケージの配置と実行の詳細については、「[SQL Server Integration Services ワークロードをクラウドにリフト アンド シフトする](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)」を参照してください。

Linux で SSIS パッケージを実行する場合は、このクイックスタートの情報を使用することはできません。 Linux でパッケージを実行する方法については、[SSIS を使用し、Linux でデータの抽出、変換、読み込みを行う](../linux/sql-server-linux-migrate-ssis.md)方法に関するページを参照してください。

## <a name="set-language-mode-to-sql-in-vs-code"></a>VS Code で言語モードを SQL に設定する

`mssql` コマンドと T-SQL IntelliSense を有効にするには、Visual Studio Code で言語モードを **SQL** に設定します。

1. Visual Studio Code を開き、新しいウィンドウを開きます。 

2. ステータス バーの右下隅にある **[プレーン テキスト]** をクリックします。

3. 開いた **[言語モードの選択]** ドロップダウン メニューで、 **[SQL]** を選択または入力して、**Enter** キーを押して言語モードを SQL に設定します。 

## <a name="for-azure-sql-database-get-the-connection-info"></a>Azure SQL Database の場合の接続情報の取得

Azure SQL Database でパッケージを実行するには、SSIS カタログ データベース (SSISDB) に接続するために必要な接続情報を取得します。 次の手順では、完全修飾サーバー名とログイン情報が必要です。

1. [Azure ポータル](https://portal.azure.com/)にログインします。
2. 左側のメニューから **[SQL Databases]** を選択し、 **[SQL データベース]** ページで SSISDB データベースを選びます。 
3. データベースの **[概要]** ページで、完全修飾サーバー名を確認します。 **[クリックしてコピー]** オプションを表示するには、サーバー名にマウス ポインターを移動します。 
4. Azure SQL Database サーバーのログイン情報を忘れた場合は、[SQL Database サーバー] ページに移動し、サーバーの管理者名を表示します。 必要に応じて、パスワードをリセットできます。

## <a name="connect-to-the-ssis-catalog-database"></a>SSIS カタログ データベースに接続する

Visual Studio Code を使用して、SSIS カタログへの接続を確立します。

> [!IMPORTANT]
> 続行する前に、サーバー、データベース、およびログイン情報が準備されていることを確認します。 接続プロファイル情報の入力を開始した後、Visual Studio Code からフォーカスを変更した場合は、接続プロファイルを作り直す必要があります。

1. VS Code で **Ctrl + Shift + P** (または **F1**) キーを押して、コマンド パレットを開きます。

2. 「**sqlcon**」と入力し、**Enter** キーを押します。

3. **Enter** キーを押して、 **[接続プロファイルの作成]** を選択します。 この手順では、SQL Server インスタンスの接続プロファイルを作成します。

4. 指示に従って、新しい接続プロファイルの接続プロパティを指定します。 それぞれの値を指定してから、**Enter** キーを押して続行します。 

   | 設定       | 提案される値 | 詳細 |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **サーバー名** | 完全修飾サーバー名 | Azure SQL Database サーバーに接続する場合、名前は次の形式になります。`<server_name>.database.windows.net` |
   | **データベース名** | **SSISDB** | 接続先となるデータベースの名前。 |
   | **[認証]** | SQL ログイン | SQL Server 認証を使用すると、SQL Server または Azure SQL Database に接続できます。 Azure SQL Database サーバーに接続する場合、Windows 認証を使用できません。 |
   | **User name** | サーバー管理者アカウント | このアカウントは、サーバーの作成時に指定したアカウントです。 |
   | **パスワード (SQL ログイン)** | サーバー管理者アカウントのパスワード | このパスワードは、サーバーの作成時に指定したパスワードです。 |
   | **パスワードを保存しますか?** | はい、いいえ | 毎回パスワードを入力したくない場合は、[はい] を選択します。 |
   | **このプロファイルの名前を入力してください** | **mySSISServer** などのプロファイル名 | プロファイル名が保存されていると、その後のログインの接続が高速化します。 | 

5. **Esc** キーを押して、プロファイルが作成され、接続されていることを通知する情報メッセージを閉じます。

6. ステータス バーで、接続を確認します。

## <a name="run-the-t-sql-code"></a>T-SQL コードを実行する
SSIS パッケージを実行するには、次の Transact-SQL コードを実行します。

1. **エディター** ウィンドウで、空のクエリ ウィンドウに次のクエリを入力します (このコードは、SSMS の **[パッケージ実行]** ダイアログ ボックスの **[スクリプト]** オプションによって生成されたコードです)。

2. システムの `catalog.create_execution` ストアド プロシージャ内のパラメーター値を更新します。

3. **Ctrl + Shift + E** キーを押してコードを実行し、パッケージを実行します。

```sql
Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx',
    @execution_id=@execution_id OUTPUT,
    @folder_name=N'Deployed Projects',
      @project_name=N'Integration Services Project1',
    @use32bitruntime=False,
      @reference_id=Null
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,
    @object_type=50,
      @parameter_name=N'LOGGING_LEVEL',
      @parameter_value=@var0
EXEC [SSISDB].[catalog].[start_execution] @execution_id
GO
```

## <a name="next-steps"></a>次の手順
- パッケージを実行する他の方法を検討します。
    - [SSMS を使用して SSIS パッケージを実行する](./ssis-quickstart-run-ssms.md)
    - [Transact-SQL (SSMS) を使用して SSIS パッケージを実行する](./ssis-quickstart-run-tsql-ssms.md)
    - [コマンド プロンプトから SSIS パッケージを実行する](./ssis-quickstart-run-cmdline.md)
    - [PowerShell を使用して SSIS パッケージを実行する](ssis-quickstart-run-powershell.md)
    - [C# を使用して SSIS パッケージを実行する](./ssis-quickstart-run-dotnet.md) 
