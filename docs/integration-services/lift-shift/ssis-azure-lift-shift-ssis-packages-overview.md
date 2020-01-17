---
title: Azure で SSIS パッケージをデプロイし、実行する | Microsoft Docs
description: SQL Server Integration Services (SSIS) プロジェクト、パッケージ、ワークロードを Microsoft Azure クラウドに移動する方法について説明します。
ms.date: 09/23/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
ms.openlocfilehash: 0a402c50e8a7f1c2467b00fbbaa599d6c289ebab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67896180"
---
# <a name="lift-and-shift-sql-server-integration-services-workloads-to-the-cloud"></a>SQL Server Integration Services ワークロードをクラウドにリフト アンド シフトする

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


SQL Server Integration Services (SSIS) プロジェクト、パッケージ、ワークロードを Azure クラウドに移動できるようになりました。 SQL Server Management Studio (SSMS) などのよく使われるツールを利用して、SSIS プロジェクトとパッケージを Azure SQL Database の SSIS カタログ (SSISDB) または SQL Database Managed Instance でデプロイ、実行、管理します。

## <a name="benefits"></a>利点
オンプレミスの SSIS ワークロードを Azure に移動すると、次の潜在的な利点があります。
-   **運用コストを削減**し、SSIS をオンプレミスまたは Azure の仮想マシンで実行するのに必要なインフラストラクチャを管理するための作業負荷を軽減します。
-   クラスターごとの複数のノードを指定する機能と、Azure および Azure SQL Database の高可用性機能により、**高可用性が向上**します。
-   ノード (スケール アップ) ごとに複数のコアとクラスター (スケール アウト) ごとに複数のノードを指定する機能により、**スケーラビリティが向上**します。

## <a name="architecture-of-ssis-on-azure"></a>Azure での SSIS のアーキテクチャ
次の表に、オンプレミスの SSIS と Azure の SSIS の違いを示します。

最も重要な違いは、ランタイムからの記憶域の分離です。 Azure Data Factory では、Azure で SSIS パッケージのランタイム エンジンをホストします。 ランタイム エンジンは、Azure SSIS 統合ランタイム (Azure SSIS IR) と呼ばれます。 詳細については、「[Azure SSIS 統合ランタイム](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime)」を参照してください。

| 場所 | ストレージ | ランタイム | スケーラビリティ |
|---|---|---|---|
| オンプレミス | SQL Server | SQL Server でホストされている SSIS ランタイム | SSIS Scale Out (SQL Server 2017 以降)<br/><br/>カスタム ソリューション (SQL Server の以前のバージョン) |
| Azure 上 | SQL Database または Azure SQL Database Managed Instance | Azure SSIS 統合ランタイム、Azure Data Factory のコンポーネント | Azure SSIS 統合ランタイムのスケーリング オプション |
| | | | |

## <a name="provision-ssis-on-azure"></a>Azure での SSIS のプロビジョニング

**プロビジョニング**。 Azure で SSIS パッケージをデプロイして実行するには、事前に SSIS カタログ (SSISDB) と Azure SSIS Integration Runtime をプロビジョニングする必要があります。

-   Azure portal で Azure 上に SSIS をプロビジョニングするには、次の記事に記載されているプロビジョニング手順に従ってください:「[Azure Data Factory に Azure-SSIS 統合ランタイムをプロビジョニングする](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure)」。 

-   PowerShell を使って Azure 上に SSIS をプロビジョニングするには、次の記事に記載されているプロビジョニング手順に従ってください:「[PowerShell を使用して Azure-SSIS 統合ランタイムを Azure Data Factory にプロビジョニングする](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure-powershell)」。

Azure SSIS IR は 1 回だけプロビジョニングを行う必要があります。 その後は、SQL Server Data Tools (SSDT) や SQL Server Management Studio (SSMS) などの使い慣れたツールを使用して、パッケージの配置、構成、実行、監視、スケジュール、および管理ができます。

> [!NOTE]
> Azure-SSIS 統合ランタイムは、すべての Azure リージョンで利用できるわけではありません。 サポートされているリージョンについては、「[リージョン別の利用可能な製品 - Microsoft Azure](https://azure.microsoft.com/regions/services/)」を参照してください。

**スケール アップとスケール アウト**。Azure SSIS IR をプロビジョニングする際に、次のオプションの値を指定して、スケール アップとスケール アウトができます。
-   ノード サイズ (コアの数を含む) とクラスター内のノードの数。
-   SSIS カタログ データベース (SSISDB) をホストする Azure SQL Database の既存のインスタンス、およびデータベース用のサービス層。
-   ノードごとの最大並列実行。

**パフォーマンスの向上**。 詳細については、「[Azure-SSIS 統合ランタイムを高パフォーマンス用に構成する](https://docs.microsoft.com/azure/data-factory/configure-azure-ssis-integration-runtime-performance)」を参照してください。

**コストの削減**。 コストを削減するには、必要がある場合にのみ Azure-SSIS IR を実行します。 詳しくは、「[Azure SSIS 統合ランタイムをスケジュールに従って起動および停止する方法](https://docs.microsoft.com/azure/data-factory/how-to-schedule-azure-ssis-integration-runtime)」をご覧ください。

## <a name="design-packages"></a>パッケージの設計

SSDT のオンプレミス、または SSDT がインストールされた Visual Studio で、**パッケージの設計とビルド**を続行します。

### <a name="connect-to-data-sources"></a>データ ソースに接続する

**Windows 認証**を使用してクラウドからオンプレミスのデータ ソースに接続するには、「[Azure の SSIS パッケージで Windows 認証を使用し、データ ソースとファイル共有に接続する](ssis-azure-connect-with-windows-auth.md)」をご覧ください。

ファイルとファイル共有に接続するには、「[Azure でデプロイされた SSIS パッケージを使用して、オンプレミスおよび Azure のファイルを開いて保存する](ssis-azure-files-file-shares.md)」をご覧ください。

### <a name="available-ssis-components"></a>使用可能な SSIS コンポーネント

SSISDB をホストする SQL Database のインスタンスをプロビジョニングする際に、SSIS 用 Azure Feature Pack と Access Redistributable もインストールされます。 これらのコンポーネントは、組み込みのコンポーネントでサポートされるデータ ソースの他に、さまざまな **Azure** データ ソース、および **Excel ファイルと Access ファイル**への接続を提供します。

追加のコンポーネントもインストールできます。たとえば、既定ではインストールされないドライバーをインストールできます。 詳しくは、「[Customize setup for the Azure-SSIS integration runtime](/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup)」(Azure-SSIS 統合ランタイムの設定をカスタマイズする) をご覧ください。

Enterprise Edition のライセンスがある場合は、追加コンポーネントを使用できます。 詳しくは、「[Azure-SSIS Integration Runtime の Enterprise Edition をプロビジョニングする](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-enterprise-edition)」をご覧ください。

ISV は、ライセンスのあるコンポーネントのインストールを Azure で使用できるように更新する必要があります。 詳しくは、「[Azure SSIS 統合ランタイムの有料 (ライセンスあり) カスタム コンポーネントをインストールする](https://docs.microsoft.com/azure/data-factory/how-to-develop-azure-ssis-ir-licensed-components)」をご覧ください。

### <a name="transaction-support"></a>トランザクションのサポート

オンプレミスと Azure 仮想マシンでの SQL Server では、Microsoft 分散トランザクション コーディネーター (MSDTC) トランザクションを使用することができます。 Azure SSIS IR の各ノードで MSDTC を構成するには、カスタム設定の機能を使用します。 詳細については、「[Custom setup for the Azure-SSIS integration runtime](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup)」(Azure-SSIS 統合ランタイムのカスタム設定) を参照してください。

Azure SQL Database では、エラスティック トランザクションのみを使用できます。 詳細については、「[クラウド データベースにまたがる分散トランザクション](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-transactions-overview)」を参照してください。

## <a name="deploy-and-run-packages"></a>パッケージの配置と実行

開始するには、「[チュートリアル:Azure で SQL Server Integration Services (SSIS) パッケージをデプロイし、実行する](ssis-azure-deploy-run-monitor-tutorial.md)」をご覧ください。

### <a name="prerequisites"></a>Prerequisites

SSIS パッケージを Azure にデプロイするには、次のいずれかのバージョンの SQL Server Data Tools (SSDT) が必要です。
-   Visual Studio 2017 の場合、バージョン 15.3 以降。
-   Visual Studio 2015 の場合、バージョン 17.2 以降。

### <a name="connect-to-ssisdb"></a>SSISDB に接続する

SSISDB をホストする **SQL Database の名前**が、SSDT および SSMS からパッケージを配置して実行する際に使用する 4 つの部分から成る名前の最初の部分になります。次のような形式です: `<sql_database_name>.database.windows.net`。 Azure で SSIS カタログ データベースに接続する方法について詳しくは、「[Azure の SSIS カタログ (SSISDB) に接続する](ssis-azure-connect-to-catalog-database.md)」をご覧ください。

### <a name="deploy-projects-and-packages"></a>プロジェクトとパッケージをデプロイする

Azure の SSISDB にプロジェクトをデプロイする場合には、パッケージ配置モデルではなく、**プロジェクト配置モデル**を使用する必要があります。

Azure でプロジェクトをデプロイするには、次の使い慣れたツールやスクリプト作成オプションのいずれかを使用できます。
-   SQL Server Management Studio (SSMS)
-   Transact-SQL (SSMS、Visual Studio Code、または別のツールから)
-   コマンドライン ツール
-   PowerShell または C# と SSIS の管理オブジェクト モデル

デプロイ プロセスでは、パッケージが Azure SSIS Integration Runtime で実行できることを確認するための検証が行われます。 詳しくは、「[Azure にデプロイされた SQL Server Integration Services (SSIS) パッケージを検証する](ssis-azure-validate-packages.md)」をご覧ください。

SSMS と Integration Services デプロイ ウィザードを使用するデプロイの例については、「[チュートリアル:Azure で SQL Server Integration Services (SSIS) パッケージをデプロイし、実行する](ssis-azure-deploy-run-monitor-tutorial.md)」をご覧ください。

### <a name="version-support"></a>バージョンのサポート

SSIS の任意のバージョンで作成されたパッケージを Azure にデプロイすることができます。 Azure にパッケージをデプロイするときに、検証エラーがなければ、パッケージは最新のパッケージ形式に自動的にアップグレードされます。 つまり、常に SSIS の最新バージョンにアップグレードされます。

### <a name="run-packages"></a>パッケージを実行する

Azure にデプロイされた SSIS パッケージを実行するには、さまざまな方法を使用できます。 詳しくは、「[Azure でデプロイされている SQL Server Integration Services (SSIS) パッケージを実行する](ssis-azure-run-packages.md)」をご覧ください。

### <a name="run-packages-in-an-azure-data-factory-pipeline"></a>Azure Data Factory パイプラインでパッケージを実行する

Azure Data Factory パイプラインで SSIS パッケージを実行するには、SSIS パッケージの実行アクティビティを使います。 詳細については、[Azure Data Factory で SSIS パッケージの実行アクティビティを使用して SSIS パッケージを実行する](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)方法に関するページを参照してください。

SSIS パッケージの実行アクティビティを使って Data Factory パイプラインでパッケージを実行するときは、実行時に値をパッケージに渡すことができます。 1 つまたは複数のランタイム値を渡すには、SSISDB と SQL Server Management Studio (SSMS) で SSIS 実行環境を作成します。 各環境で変数を作成し、プロジェクトまたはパッケージのパラメーターに対応する値を渡します。 それらの環境変数とプロジェクトまたはパッケージのパラメーターが関連付けられるように、SSMS で SSIS パッケージを構成します。 パイプラインでパッケージを実行するときは、SSIS パッケージの実行アクティビティ UI の [設定] タブで異なる環境パスを指定することで環境を切り替えます。 SSIS 環境について詳しくは、「[サーバー環境の作成とマップ](../packages/deploy-integration-services-ssis-projects-and-packages.md#create-and-map-a-server-environment)」をご覧ください。

## <a name="monitor-packages"></a>パッケージの監視

実行中のパッケージを監視するには、SSMS で次のレポート オプションを使います。
-   **[SSISDB]** を右クリックし、 **[アクティブな操作]** を選択して、 **[アクティブな操作]** ダイアログ ボックスを開きます。
-   オブジェクト エクスプローラーでパッケージを選択し、右クリックして **[レポート]** を選択し、 **[標準レポート]** 、 **[すべての実行]** の順に選択します。

Azure SSIS 統合ランタイムを監視するには、[Azure SSIS 統合ランタイムの監視](https://docs.microsoft.com/azure/data-factory/monitor-integration-runtime#azure-ssis-integration-runtime)に関するページを参照してください。

## <a name="schedule-packages"></a>パッケージのスケジュール設定
Azure にデプロイされたパッケージの実行をスケジュール設定するには、さまざまなツールを使用できます。 詳しくは、「[Azure でデプロイされている SQL Server Integration Services (SSIS) パッケージの実行スケジュールを設定する](ssis-azure-schedule-packages.md)」をご覧ください。

## <a name="next-steps"></a>次の手順
Azure で SSIS ワークロードの使用を開始するには、次の記事を参照してください。
-   [チュートリアル: Azure で SQL Server Integration Services (SSIS) パッケージをデプロイし、実行する](ssis-azure-deploy-run-monitor-tutorial.md)
-   [Azure Data Factory に Azure-SSIS 統合ランタイムをプロビジョニングする](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure)
