---
title: Azure で SSIS パッケージを実行する | Microsoft Docs
description: Azure SQL Database にデプロイされている SSIS パッケージの実行に利用できる方法の概要について示します。
ms.date: 05/29/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
ms.openlocfilehash: 3469a162645816a3b90657b0c2a3b81b37e6cade
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054627"
---
# <a name="run-sql-server-integration-services-ssis-packages-deployed-in-azure"></a>Azure でデプロイされている SQL Server Integration Services (SSIS) パッケージを実行する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



この記事で説明する方法の 1 つを選択することで、Azure SQL Database サーバーで SSISDB カタログにデプロイされている SSIS パッケージを実行できます。 パッケージは直接実行するか、Azure Data Factory パイプラインの一部として実行できます。 Azure 上の SSIS の概要については、「[Azure で SSIS パッケージをデプロイし、実行する](ssis-azure-lift-shift-ssis-packages-overview.md)」を参照してください。

- パッケージを直接実行する

  - [SSMS を使用しての実行](#ssms)

  - [ストアド プロシージャを使用しての実行](#sproc)

  - [スクリプトまたはコードを使用しての実行](#script)

- Azure Data Factory パイプラインの一部としてパッケージを実行する

  - [SSIS パッケージ アクティビティの実行で実行する](#exec_activity)

  - [ストアド プロシージャ アクティビティを使用して実行する](#sproc_activity)

> [!NOTE]
> `dtexec.exe` によるパッケージの実行は、Azure にデプロイされているパッケージではテストされていません。

## <a name="ssms"></a> SSMS でのパッケージの実行

SQL Server Management Studio (SSMS) では、SSIS カタログ データベース SSISDB にデプロイされたパッケージを右クリックして **[実行]** を選択することで、 **[パッケージの実行]** ダイアログ ボックスを開くことができます。 詳細については、「[SQL Server Management Studio (SSMS) を使用して SSIS プロジェクトを配置する](../ssis-quickstart-run-ssms.md)」を参照してください。

## <a name="sproc"></a> ストアド プロシージャでパッケージを実行する

Azure SQL Database に接続し、Transact-SQL コードを実行できるあらゆる環境で、次のストアド プロシージャを呼び出すことでパッケージを実行できます。

1. **[catalog].[create_execution]** . 詳細については、「[catalog.create_execution](../system-stored-procedures/catalog-create-execution-ssisdb-database.md)」を参照してください。

2. **[catalog].[set_execution_parameter_value]** . 詳細については、「[catalog.set_execution_parameter_value](../system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)」を参照してください。

3. **[catalog].[start_execution]** 詳細については、「[catalog.start_execution](../system-stored-procedures/catalog-start-execution-ssisdb-database.md)」を参照してください。

詳細については、次の例をご覧ください。

- [Transact-SQL を使用して SSMS から SSIS パッケージを実行する](../ssis-quickstart-run-tsql-ssms.md)

- [Transact-SQL を使用して Visual Studio Code から SSIS パッケージを実行する](../ssis-quickstart-run-tsql-vscode.md)

## <a name="script"></a> スクリプトまたはコードでパッケージを実行する

マネージド API を呼び出すことができるあらゆる開発環境で、`Microsoft.SQLServer.Management.IntegrationServices` 名前空間で `Package` オブジェクトの `Execute` メソッドを呼び出すことでパッケージを実行できます。

詳細については、次の例をご覧ください。

- [PowerShell を使用して SSIS パッケージを実行する](../ssis-quickstart-run-powershell.md)

- [.NET アプリで C# コードを使用して SSIS パッケージを実行する](../ssis-quickstart-run-dotnet.md)

## <a name="exec_activity"></a> SSIS パッケージの実行アクティビティを使用してパッケージを実行する

詳細については、[Azure Data Factory で SSIS パッケージの実行アクティビティを使用して SSIS パッケージを実行する](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)方法に関するページを参照してください。

## <a name="sproc_activity"></a> ストアド プロシージャ アクティビティを使用してパッケージを実行する

詳細については、「[Azure Data Factory のストアド プロシージャ アクティビティを使用して SSIS パッケージを実行する](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-stored-procedure-activity)」をご覧ください。

## <a name="next-steps"></a>次の手順

Azure にデプロイされている SSIS パッケージのスケジュール設定オプションについて学習してください。 詳細については、「[Azure で SSIS パッケージのスケジュールを設定する](ssis-azure-schedule-packages.md)」を参照してください。
