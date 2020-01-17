---
title: SSMS で SSIS プロジェクトを配置する | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 04f7231dc4781b3c7194a7a34002b67087c9eaf2
ms.sourcegitcommit: ef830f565ee07dc7d4388925cc3c86c5d2cfb4c7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2019
ms.locfileid: "74947116"
---
# <a name="deploy-an-ssis-project-with-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) を使用して SSIS プロジェクトを配置する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


このクイックスタートでは、SQL Server Management Studio (SSMS) を使用して SSIS Catalog データベースに接続し、Integration Services Deployment Wizard を実行して SSIS プロジェクトを SSIS Catalog にデプロイする方法について説明します。 

SQL Server Management Studio は、SQL Server から SQL Database まで、SQL インフラストラクチャを管理するための統合環境です。 SSMS については、「[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)」をご覧ください。

## <a name="prerequisites"></a>前提条件

始める前に、最新バージョンの SQL Server Management Studio があることを確認します。 SSMS をダウンロードするには、「[SQL Server Management Studio (SSMS) のダウンロード](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)」を参照してください。

Azure SQL Database へのデプロイに関連してこの記事で説明している検証には、SQL Server Data Tools (SSDT) version 17.4 以降が必要です。 最新版の SSDT を入手する方法については、「[SQL Server Data Tools (SSDT) のダウンロード](../ssdt/download-sql-server-data-tools-ssdt.md)」をご覧ください。

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

## <a name="authentication-methods-for-deployment"></a>デプロイの認証方法

デプロイ ウィザードで SQL Server にデプロイする場合、Windows 認証を使用する必要があります。SQL Server 認証は使用できません。

Azure SQL Database サーバーにデプロイする場合、SQL Server 認証または Azure Active Directory 認証を使用する必要があります。Windows 認証は使用できません。

## <a name="connect-to-the-ssisdb-database"></a>SSISDB データベースに接続する

SQL Server Management Studio を使って、SSIS カタログへの接続を確立します。 

1. SQL Server Management Studio を開きます。

2. **[サーバーへの接続]** ダイアログ ボックスで、次の情報を入力します。

   | 設定       | 推奨値 | 詳細情報 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **サーバーの種類** | データベース エンジン | この値は必須です。 |
   | **サーバー名** | 完全修飾サーバー名 | Azure SQL Database サーバーに接続する場合、名前は次の形式になります。`<server_name>.database.windows.net` |
   | **認証** | SQL Server 認証 | SQL Server 認証を使用すると、SQL Server または Azure SQL Database に接続できます。 この記事の「[デプロイ ウィザードでの認証方法](#authentication-methods-for-deployment)」を参照してください。 |
   | **Login** | サーバー管理者アカウント | このアカウントは、サーバーの作成時に指定したアカウントです。 |
   | **パスワード** | サーバー管理者アカウントのパスワード | このパスワードは、サーバーの作成時に指定したパスワードです。 |

3. **[接続]** をクリックします。 SSMS で [オブジェクト エクスプローラー] ウィンドウが開きます。 

4. オブジェクト エクスプローラーで、 **[Integration Services カタログ]** 、 **[SSISDB]** の順に展開し、SSIS カタログ データベース内のオブジェクトを表示します。

## <a name="start-the-integration-services-deployment-wizard"></a>Integration Services 配置ウィザードを起動する
1. オブジェクト エクスプローラーで、**Integration Services Catalogs** ノードと **SSISDB** ノードが展開されている状態で、フォルダーを展開します。

2.  **[プロジェクト]** ノードを選びます。

3.  **[プロジェクト]** ノードを右クリックして、 **[プロジェクトの配置]** を選びます。 Integration Services 配置ウィザードが開きます。 現在のカタログから、またはファイル システムから、プロジェクトを配置することができます。

## <a name="deploy-a-project-with-the-wizard"></a>ウィザードを使用してプロジェクトを配置する
1. ウィザードの **[概要]** ページで、概要を確認します。 **[次へ]** をクリックして、 **[ソースの選択]** ページを開きます。

2. **[ソースの選択]** ページで、配置する既存の SSIS プロジェクトを選びます。
    -   開発環境でプロジェクトをビルドする方法で作成したプロジェクト デプロイ ファイルをデプロイするには、 **[プロジェクト配置ファイル]** を選択し、.ispac ファイルのパスを入力します。
    -   SSIS カタログ データベースに既にデプロイされているプロジェクトをデプロイするには、 **[Integration Services カタログ]** を選択し、サーバー名とカタログ内のプロジェクトのパスを入力します。
    **[次へ]** をクリックして、 **[配置先の選択]** ページを表示します。
  
3.  **[配置先の選択]** ページで、プロジェクトの配置先を選びます。
    -   完全修飾サーバー名を入力します。 ターゲット サーバーが Azure SQL Database サーバーの場合、名前は `<server_name>.database.windows.net` 形式になります。
    -   認証情報を入力し、 **[接続]** を選択します。 この記事の「[デプロイ ウィザードでの認証方法](#authentication-methods-for-deployment)」を参照してください。
    -   次に、 **[参照]** を選択し、SSISDB でターゲット フォルダーを選択します。
    -   **[次へ]** を選択し、 **[レビュー]** ページを開きます。 ( **[次へ]** ボタンは、 **[接続]** を選択した後でないと有効になりません。)
  
4.  **[レビュー]** ページで、選択した設定を確認します。
    -   選択内容を変更するには、 **[戻る]** をクリックするか、左ペインでいずれかの手順をクリックします。
    -   **[配置]** をクリックして、配置プロセスを開始します。

5.  Azure SQL Database サーバーにデプロイしている場合、 **[検証]** ページが開き、Azure SSIS Integration Runtime で予定されているパッケージ実行を妨げる既知の問題がないか、プロジェクトのパッケージが調べられます。 詳細については、「[Azure にデプロイされた SSIS パッケージの検証](lift-shift/ssis-azure-validate-packages.md)」を参照してください。

6.  配置プロセスが完了すると、 **[結果]** ページが開きます。 このページでは、各アクションが成功したか、失敗したかを表示します。
    -   アクションが失敗した場合は、 **[結果]** 列の **[失敗]** をクリックすると、エラーの説明が表示されます。
    -   必要に応じて、 **[レポートの保存]** をクリックして結果を XML ファイルに保存します。
    -   **[閉じる]** をクリックしてウィザードを終了します。

## <a name="next-steps"></a>次のステップ
- パッケージを配置する他の方法を検討します。
    - [Transact-SQL (SSMS) を使用して SSIS パッケージを配置する](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Transact-SQL (VS Code) を使用して SSIS パッケージを配置する](ssis-quickstart-deploy-tsql-vscode.md)
    - [コマンド プロンプトから SSIS パッケージを配置する](./ssis-quickstart-deploy-cmdline.md)
    - [PowerShell を使用して SSIS パッケージを配置する](ssis-quickstart-deploy-powershell.md)
    - [C# を使用して SSIS パッケージを配置する](./ssis-quickstart-deploy-dotnet.md) 
- 配置されたパッケージを実行します。 パッケージを実行するには、いくつかのツールおよび言語から選択することができます。 詳細については、次の記事を参照してください。
    - [SSMS を使用して SSIS パッケージを実行する](./ssis-quickstart-run-ssms.md)
    - [Transact-SQL (SSMS) を使用して SSIS パッケージを実行する](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-SQL (VS Code) を使用して SSIS パッケージを実行する](ssis-quickstart-run-tsql-vscode.md)
    - [コマンド プロンプトから SSIS パッケージを実行する](./ssis-quickstart-run-cmdline.md)
    - [PowerShell を使用して SSIS パッケージを実行する](ssis-quickstart-run-powershell.md)
    - [C# を使用して SSIS パッケージを実行する](./ssis-quickstart-run-dotnet.md) 
