---
title: .NET コード (C#) を使用して SSIS プロジェクトを配置する | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 43820f44e789330ed437c104e385090a8179a2b3
ms.sourcegitcommit: ef830f565ee07dc7d4388925cc3c86c5d2cfb4c7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2019
ms.locfileid: "74947122"
---
# <a name="deploy-an-ssis-project-with-c-code-in-a-net-app"></a>.NET アプリで C# コードを使用して SSIS プロジェクトを配置する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


このクイックスタートでは、データベース サーバーに接続し、SSIS プロジェクトをデプロイする C# コードを記述する方法について説明します。

C# アプリを作成するには、Visual Studio、Visual Studio Code、または他の任意のツールを使用できます。

## <a name="prerequisites"></a>前提条件

開始する前に Visual Studio または Visual Studio Code がインストールされていることを確認します。 Visual Studio の無償の Community エディション、または無償の Visual Studio Code を「[Visual Studio のダウンロード](https://www.visualstudio.com/downloads/)」からダウンロードします。

Azure SQL Database サーバーは、ポート 1433 でリッスンします。 企業のファイアウォール内から Azure SQL Database サーバーに接続しようとする場合、正常に接続するには、このポートを企業のファイアウォールで開ける必要があります。

## <a name="supported-platforms"></a>サポートされているプラットフォーム

このクイックスタートの情報を利用し、次のプラットフォームに SSIS プロジェクトをデプロイできます。

-   SQL Server on Windows。

-   Azure SQL Database。 Azure でパッケージをデプロイし、実行する方法については、「[SQL Server Integration Services ワークロードをクラウドにリフト アンド シフトする](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)」を参照してください。

SQL Server on Linux に SSIS パッケージをデプロイする場合は、このクイックスタートの情報を使用できません。 Linux でパッケージを実行する方法については、[SSIS を使用し、Linux でデータの抽出、変換、読み込みを行う](../linux/sql-server-linux-migrate-ssis.md)方法に関するページを参照してください。

## <a name="for-azure-sql-database-get-the-connection-info"></a>Azure SQL Database の場合の接続情報の取得

プロジェクトを Azure SQL Database にデプロイするには、SSIS カタログ データベース (SSISDB) に接続するために必要な接続情報を取得します。 次の手順では、完全修飾サーバー名とログイン情報が必要です。

1. [Azure Portal](https://portal.azure.com/) にログインします。
2. 左側のメニューから **[SQL Databases]** を選択し、 **[SQL データベース]** ページで SSISDB データベースを選びます。 
3. データベースの **[概要]** ページで、完全修飾サーバー名を確認します。 **[クリックしてコピー]** オプションを表示するには、サーバー名にマウス ポインターを移動します。 
4. Azure SQL Database サーバーのログイン情報を忘れた場合は、[SQL Database サーバー] ページに移動し、サーバーの管理者名を表示します。 必要に応じて、パスワードをリセットできます。
5. **[データベース接続文字列の表示]** をクリックします。
6. 完全な **ADO.NET** 接続文字列を確認します。 任意で、コードで `SqlConnectionStringBuilder` を使用し、入力した個々のパラメーター値でこの接続文字列を再作成できます。

## <a name="supported-authentication-method"></a>サポートされている認証方法

[デプロイの認証方法](ssis-quickstart-deploy-ssms.md#authentication-methods-for-deployment)を参照してください。

## <a name="create-a-new-visual-studio-project"></a>新しい Visual Studio プロジェクトの作成

1. Visual Studio で、 **[ファイル]** 、 **[新規]** 、 **[プロジェクト]** の順に選択します。 
2. **[新しいプロジェクト]** ダイアログで、 **[Visual C#]** を展開します。
3. **[コンソール アプリ]** を選択し、プロジェクト名に *deploy_ssis_project* を入力します。
4. **[OK]** をクリックして Visual Studio で新しいプロジェクトを開きます。

## <a name="add-references"></a>参照の追加
1. ソリューション エクスプローラーで、 **[参照]** フォルダーを右クリックし、 **[参照の追加]** を選択します。 **[参照マネージャー]** ダイアログ ボックスが表示されます。
2. **[参照マネージャー]** ダイアログ ボックスで、 **[アセンブリ]** を展開して **[拡張機能]** を選択します。
3. 次の 2 つの参照を選択して追加します。
    -   Microsoft.SqlServer.Management.Sdk.Sfc
    -   Microsoft.SqlServer.Smo
4. **[参照]** ボタンをクリックして、参照を **Microsoft.SqlServer.Management.IntegrationServices** に追加します (このアセンブリはグローバル アセンブリ キャッシュ (GAC) にのみインストールされます)。 **[参照するファイルの選択]** ダイアログ ボックスが表示されます。
5. **[参照するファイルの選択]** ダイアログ ボックスで、アセンブリを含む GAC フォルダーに移動します。 通常このフォルダーは `C:\Windows\assembly\GAC_MSIL\Microsoft.SqlServer.Management.IntegrationServices\14.0.0.0__89845dcd8080cc91` です。
6. フォルダー内のアセンブリ (.dll ファイル) を選択し、 **[追加]** をクリックします。
7. **[OK]** をクリックして **[参照マネージャー]** ダイアログ ボックスを閉じ、3 つの参照を追加します。 参照があることを確認するには、ソリューション エクスプローラーで **[参照]** リストを確認します。

## <a name="add-the-c-code"></a>C# コードを追加する 
1. **Program.cs** を開きます。

2. **Program.cs** のコンテンツを次のコードに置き換えます。 サーバー、データベース、ユーザー、およびパスワードの適切な値を追加します。

> [!NOTE]
> 次の例では、Windows 認証を使用します。 SQL Server 認証を使用するには、`Integrated Security=SSPI;` 引数を `User ID=<user name>;Password=<password>;` に置き換えます。 Azure SQL Database サーバーに接続する場合、Windows 認証を使用できません。

```csharp
using Microsoft.SqlServer.Management.IntegrationServices;
using System;
using System.Data.SqlClient;
using System.IO;

namespace deploy_ssis_project
{
    class Program
    {
        static void Main(string[] args)
        {
            // Variables
            string targetServerName = "localhost";
            string targetFolderName = "Project1Folder";
            string projectName = "Integration Services Project1";
            string projectFilePath = @"C:\Projects\Integration Services Project1\Integration Services Project1\bin\Development\Integration Services Project1.ispac";

            // Create a connection to the server
            string sqlConnectionString = "Data Source=" + targetServerName +
                ";Initial Catalog=master;Integrated Security=SSPI;";
            SqlConnection sqlConnection = new SqlConnection(sqlConnectionString);

            // Create the Integration Services object
            IntegrationServices integrationServices = new IntegrationServices(sqlConnection);

            // Get the Integration Services catalog
            Catalog catalog = integrationServices.Catalogs["SSISDB"];

            // Create the target folder
            CatalogFolder folder = new CatalogFolder(catalog,
                targetFolderName, "Folder description");
            folder.Create();

            Console.WriteLine("Deploying " + projectName + " project.");

            byte[] projectFile = File.ReadAllBytes(projectFilePath);
            folder.DeployProject(projectName, projectFile);

            Console.WriteLine("Done.");
        }
    }
}
```

## <a name="run-the-code"></a>コードの実行

1. アプリケーションを実行するには **F5** キーを押します。
2. SSMS で、プロジェクトが配置されていることを確認します。

## <a name="next-steps"></a>次のステップ
- パッケージを配置する他の方法を検討します。
    - [SSMS を使用して SSIS パッケージを配置する](./ssis-quickstart-deploy-ssms.md)
    - [Transact-SQL (SSMS) を使用して SSIS パッケージを配置する](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Transact-SQL (VS Code) を使用して SSIS パッケージを配置する](ssis-quickstart-deploy-tsql-vscode.md)
    - [コマンド プロンプトから SSIS パッケージを配置する](./ssis-quickstart-deploy-cmdline.md)
    - [PowerShell を使用して SSIS パッケージを配置する](ssis-quickstart-deploy-powershell.md)
- 配置されたパッケージを実行します。 パッケージを実行するには、いくつかのツールおよび言語から選択することができます。 詳細については、次の記事を参照してください。
    - [SSMS を使用して SSIS パッケージを実行する](./ssis-quickstart-run-ssms.md)
    - [Transact-SQL (SSMS) を使用して SSIS パッケージを実行する](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-SQL (VS Code) を使用して SSIS パッケージを実行する](ssis-quickstart-run-tsql-vscode.md)
    - [コマンド プロンプトから SSIS パッケージを実行する](./ssis-quickstart-run-cmdline.md)
    - [PowerShell を使用して SSIS パッケージを実行する](ssis-quickstart-run-powershell.md)
    - [C# を使用して SSIS パッケージを実行する](./ssis-quickstart-run-dotnet.md) 
