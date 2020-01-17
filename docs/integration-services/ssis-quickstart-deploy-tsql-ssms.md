---
title: Transact-SQL (SSMS) を使用して SSIS プロジェクトを配置する | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b854e6c7db8bb042ced1c883e17fb4ac6d484fe7
ms.sourcegitcommit: ef830f565ee07dc7d4388925cc3c86c5d2cfb4c7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2019
ms.locfileid: "74947094"
---
# <a name="deploy-an-ssis-project-from-ssms-with-transact-sql"></a>Transact-SQL を使用して SSMS から SSIS プロジェクトを配置する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



このクイックスタートでは、SQL Server Management Studio (SSMS) を使用して SSIS カタログ データベースに接続し、Transact-SQL ステートメントを使用して SSIS プロジェクトを SSIS カタログに配置する方法を示します。 

SQL Server Management Studio は、SQL Server から SQL Database まで、SQL インフラストラクチャを管理するための統合環境です。 SSMS については、「[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)」をご覧ください。

## <a name="prerequisites"></a>前提条件

始める前に、最新バージョンの SQL Server Management Studio があることを確認します。 SSMS をダウンロードするには、「[SQL Server Management Studio (SSMS) のダウンロード](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)」を参照してください。

## <a name="supported-platforms"></a>サポートされているプラットフォーム

このクイックスタートの情報を利用し、次のプラットフォームに SSIS プロジェクトをデプロイできます。

-   SQL Server on Windows。

Azure SQL Database に SSIS パッケージをデプロイする場合は、このクイックスタートの情報を使用できません。 `catalog.deploy_project` ストアド プロシージャでは、ローカル ファイル システム内 (オンプレミス) の `.ispac` ファイルへのパスが必要です。 Azure でパッケージをデプロイし、実行する方法については、「[SQL Server Integration Services ワークロードをクラウドにリフト アンド シフトする](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)」を参照してください。

SQL Server on Linux に SSIS パッケージをデプロイする場合は、このクイックスタートの情報を使用できません。 Linux でパッケージを実行する方法については、[SSIS を使用し、Linux でデータの抽出、変換、読み込みを行う](../linux/sql-server-linux-migrate-ssis.md)方法に関するページを参照してください。

## <a name="supported-authentication-method"></a>サポートされている認証方法

[デプロイの認証方法](ssis-quickstart-deploy-ssms.md#authentication-methods-for-deployment)を参照してください。

## <a name="connect-to-the-ssis-catalog-database"></a>SSIS カタログ データベースに接続する

SQL Server Management Studio を使って、SSIS カタログへの接続を確立します。 

1. SQL Server Management Studio を開きます。

2. **[サーバーへの接続]** ダイアログ ボックスで、次の情報を入力します。

   | 設定       | 推奨値 | 詳細情報 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **サーバーの種類** | データベース エンジン | この値は必須です。 |
   | **サーバー名** | 完全修飾サーバー名 |  |
   | **認証** | SQL Server 認証 | |
   | **Login** | サーバー管理者アカウント | このアカウントは、サーバーの作成時に指定したアカウントです。 |
   | **パスワード** | サーバー管理者アカウントのパスワード | このパスワードは、サーバーの作成時に指定したパスワードです。 |

3. **[接続]** をクリックします。 SSMS で [オブジェクト エクスプローラー] ウィンドウが開きます。 

4. オブジェクト エクスプローラーで、 **[Integration Services カタログ]** 、 **[SSISDB]** の順に展開し、SSIS カタログ データベース内のオブジェクトを表示します。


## <a name="run-the-t-sql-code"></a>T-SQL コードを実行する
SSIS プロジェクトを配置するには、次の Transact-SQL コードを実行します。

1.  SSMS で、新しいクエリ ウィンドウを開き、次のコードを貼り付けます。

2.  システムの `catalog.deploy_project` ストアド プロシージャ内のパラメーター値を更新します。

3.  **SSISDB** が現在のデータベースであることを確認します。

4.  スクリプトを実行します。

5. オブジェクト エクスプローラーで、必要に応じて **SSISDB** のコンテンツを更新し、配置したプロジェクトを確認します。

```sql
DECLARE @ProjectBinary AS varbinary(max)
DECLARE @operation_id AS bigint
SET @ProjectBinary =
    (SELECT * FROM OPENROWSET(BULK '<project_file_path>.ispac', SINGLE_BLOB) AS BinaryData)

EXEC catalog.deploy_project @folder_name = '<target_folder>',
    @project_name = '<project_name',
    @Project_Stream = @ProjectBinary,
    @operation_id = @operation_id out
```

## <a name="next-steps"></a>次のステップ
- パッケージを配置する他の方法を検討します。
    - [SSMS を使用して SSIS パッケージを配置する](./ssis-quickstart-deploy-ssms.md)
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
