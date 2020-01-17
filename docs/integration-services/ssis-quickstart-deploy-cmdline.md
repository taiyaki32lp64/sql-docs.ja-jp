---
title: コマンド プロンプトから SSIS プロジェクトを配置する | Microsoft Docs
ms.date: 05/21/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 182dcae5867cd05d508357160aecb5c46d1d5e82
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71281776"
---
# <a name="deploy-an-ssis-project-from-the-command-prompt-with-isdeploymentwizardexe"></a>ISDeploymentWizard.exe を使用して、コマンド プロンプトから SSIS プロジェクトを配置する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


このクイック スタートでは、Integration Services 配置ウィザード `ISDeploymentWizard.exe` を実行して、コマンド プロンプトから、SSIS プロジェクトを配置する方法を示します。

Integration Services 配置ウィザードの詳細については、「[Integration Services 配置ウィザード](packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard)」を参照してください。

## <a name="prerequisites"></a>Prerequisites

Azure SQL Database へのデプロイに関連してこの記事で説明している検証には、SQL Server Data Tools (SSDT) version 17.4 以降が必要です。 最新版の SSDT を入手する方法については、「[SQL Server Data Tools (SSDT) のダウンロード](../ssdt/download-sql-server-data-tools-ssdt.md)」をご覧ください。

Azure SQL Database サーバーは、ポート 1433 でリッスンします。 企業のファイアウォール内から Azure SQL Database サーバーに接続しようとする場合、正常に接続するには、このポートを企業のファイアウォールで開ける必要があります。

## <a name="supported-platforms"></a>サポートされているプラットフォーム

このクイックスタートの情報を利用し、次のプラットフォームに SSIS プロジェクトをデプロイできます。

-   SQL Server on Windows。

-   Azure SQL Database。 Azure でパッケージをデプロイし、実行する方法については、「[SQL Server Integration Services ワークロードをクラウドにリフト アンド シフトする](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)」を参照してください。

SQL Server on Linux に SSIS パッケージをデプロイする場合は、このクイックスタートの情報を使用できません。 Linux でパッケージを実行する方法については、[SSIS を使用し、Linux でデータの抽出、変換、読み込みを行う](../linux/sql-server-linux-migrate-ssis.md)方法に関するページを参照してください。

## <a name="for-azure-sql-database-get-the-connection-info"></a>Azure SQL Database の場合の接続情報の取得

プロジェクトを Azure SQL Database にデプロイするには、SSIS カタログ データベース (SSISDB) に接続するために必要な接続情報を取得します。 次の手順では、完全修飾サーバー名とログイン情報が必要です。

1. [Azure ポータル](https://portal.azure.com/)にログインします。
2. 左側のメニューから **[SQL Databases]** を選択し、 **[SQL データベース]** ページで SSISDB データベースを選びます。 
3. データベースの **[概要]** ページで、完全修飾サーバー名を確認します。 **[クリックしてコピー]** オプションを表示するには、サーバー名にマウス ポインターを移動します。 
4. Azure SQL Database サーバーのログイン情報を忘れた場合は、[SQL Database サーバー] ページに移動し、サーバーの管理者名を表示します。 必要に応じて、パスワードをリセットできます。

## <a name="wizard_auth"></a> デプロイ ウィザードでの認証方法

デプロイ ウィザードで SQL Server にデプロイする場合、Windows 認証を使用する必要があります。SQL Server 認証は使用できません。

Azure SQL Database サーバーにデプロイする場合、SQL Server 認証または Azure Active Directory 認証を使用する必要があります。Windows 認証は使用できません。

## <a name="start-the-integration-services-deployment-wizard"></a>Integration Services 配置ウィザードを起動する
1. コマンド プロンプト ウィンドウを開きます。

2. `ISDeploymentWizard.exe` を実行します。 Integration Services 配置ウィザードが開きます。

    `ISDeploymentWizard.exe` を含むフォルダーが `path` 環境変数にない場合、そのディレクトリに変更するために `cd` コマンドを使用する必要がある場合があります。 SQL Server 2017 の場合、このフォルダーは通常 `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn` です。

## <a name="deploy-a-project-with-the-wizard"></a>ウィザードを使用してプロジェクトを配置する
1. ウィザードの **[概要]** ページで、概要を確認します。 **[次へ]** をクリックして、 **[ソースの選択]** ページを開きます。

2. **[ソースの選択]** ページで、配置する既存の SSIS プロジェクトを選びます。
    -   開発環境でプロジェクトをビルドする方法で作成したプロジェクト デプロイ ファイルをデプロイするには、 **[プロジェクト配置ファイル]** を選択し、.ispac ファイルのパスを入力します。
    -   SSIS カタログ データベースに既にデプロイされているプロジェクトをデプロイするには、 **[Integration Services カタログ]** を選択し、サーバー名とカタログ内のプロジェクトのパスを入力します。
    **[次へ]** をクリックして、 **[配置先の選択]** ページを表示します。
  
3.  **[配置先の選択]** ページで、プロジェクトの配置先を選びます。
    -   完全修飾サーバー名を入力します。 ターゲット サーバーが Azure SQL Database サーバーの場合、名前は `<server_name>.database.windows.net` 形式になります。
    -   認証情報を入力し、 **[接続]** を選択します。 この記事の「[デプロイ ウィザードでの認証方法](#wizard_auth)」を参照してください。
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

## <a name="next-steps"></a>次の手順
- パッケージを配置する他の方法を検討します。
    - [SSMS を使用して SSIS パッケージを配置する](./ssis-quickstart-deploy-ssms.md)
    - [Transact-SQL (SSMS) を使用して SSIS パッケージを配置する](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Transact-SQL (VS Code) を使用して SSIS パッケージを配置する](ssis-quickstart-deploy-tsql-vscode.md)
    - [PowerShell を使用して SSIS パッケージを配置する](ssis-quickstart-deploy-powershell.md)
    - [C# を使用して SSIS パッケージを配置する](./ssis-quickstart-deploy-dotnet.md) 
- 配置されたパッケージを実行します。 パッケージを実行するには、いくつかのツールおよび言語から選択することができます。 詳細については、次の記事をご覧ください。
    - [SSMS を使用して SSIS パッケージを実行する](./ssis-quickstart-run-ssms.md)
    - [Transact-SQL (SSMS) を使用して SSIS パッケージを実行する](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-SQL (VS Code) を使用して SSIS パッケージを実行する](ssis-quickstart-run-tsql-vscode.md)
    - [コマンド プロンプトから SSIS パッケージを実行する](./ssis-quickstart-run-cmdline.md)
    - [PowerShell を使用して SSIS パッケージを実行する](ssis-quickstart-run-powershell.md)
    - [C# を使用して SSIS パッケージを実行する](./ssis-quickstart-run-dotnet.md) 
