---
title: SQL Server 2017 の Integration Services の新機能 | Microsoft Docs
ms.custom: ''
ms.date: 09/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e26d7884-e772-46fa-bfdc-38567fe976a1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2baea8e71a3730a100eda8971ad70a28f1a97773
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296467"
---
# <a name="what39s-new-in-integration-services-in-sql-server-2017"></a>SQL Server 2017 の Integration Services の新機能

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


このトピックでは、 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]で追加または更新された機能について説明します。

> [!NOTE]
> SQL Server 2017 には、SQL Server 2016 の機能と、SQL Server 2016 更新プログラムで追加された機能も含まれています。 SQL Server 2016 の新しい SSIS 機能については、 [「SQL Server 2016 で Integration Services の新機能」](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)を参照してください。

## <a name="highlights-of-this-release"></a>このリリースの重要なポイント

SQL Server 2017 の Integration Services の最も重要な新機能は以下のとおりです。

-   **Scale Out**。複数の worker コンピューター間に SSIS パッケージの実行をより簡単に配布し、単一のマスター コンピューターから実行と worker を管理します。 詳しくは、「[Integration Services Scale Out](../integration-services/scale-out/integration-services-ssis-scale-out.md)」(Integration Services の Scale Out) をご覧ください。

-   **Linux の Integration Services**。 Linux コンピューターで SSIS パッケージを実行できます。 詳しくは、「[Extract, transform, and load data on Linux with SSIS](../linux/sql-server-linux-migrate-ssis.md)」(SSIS で Linux 上のデータの抽出、変換、読み込みを行う) をご覧ください。

-   **接続性の向上**。 更新された OData コンポーネントで、Microsoft Dynamics AX Online と Microsoft Dynamics CRM Online の OData フィードに接続できます。 

## <a name="new-in-azure-data-factory"></a>Azure Data Factory の新機能

2017 年 9 月リリースの Azure Data Factory バージョン 2 のパブリック プレビュー版を使用すると、次の処理ができるようになります。
-   Azure SQL Database 上の SSIS カタログ データベース (SSISDB) にパッケージを展開する。
-   Azure に展開されているパッケージを、Azure-SSIS Integration Runtime (Azure Data Factory バージョン 2 のコンポーネント) で実行する。

詳細については、「[Lift and shift SQL Server Integration Services workloads to the cloud](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)」 (SQL Server Integration Services ワークロードをクラウドにリフト アンド シフトする) を参照してください。

これらの新機能では、SQL Server Data Tools (SSDT) のバージョン 17.2 以降が必要ですが、SQL Server 2017 または SQL Server 2016 は必要ありません。 パッケージを Azure に展開すると、常に最新のパッケージ形式となるように、パッケージの展開ウィザードによってパッケージがアップグレードされます。

## <a name="new-in-the-azure-feature-pack"></a>Azure Feature Pack の新機能

SQL Server の接続性の向上だけでなく、Integration Services Feature Pack for Azure に Azure Data Lake Store のサポートが追加されました。 詳しくは、ブログの投稿「[New Azure Feature Pack Release Strengthening ADLS Connectivity](https://blogs.msdn.microsoft.com/ssis/2017/08/29/new-azure-feature-pack-release-strengthening-adls-connectivity/)」(新しい Azure Feature Pack のリリースで強化された ADLS 接続) をご覧ください。 また、「[Integration Services (SSIS) 用の Azure Feature Pack](azure-feature-pack-for-integration-services-ssis.md)」もご覧ください。

## <a name="new-in-sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT) の新機能

Visual Studio 2017 または Visual Studio 2015 で SQL Server バージョン 2012 から 2017 までを対象とする SSIS プロジェクトとパッケージを開発できるようになりました。 詳細については、「 [SQL Server Data Tools (SSDT) のダウンロード](../ssdt/download-sql-server-data-tools-ssdt.md)」を参照してください。

## <a name="new-in-ssis-in-sql-server-2017-rc1"></a>SQL Server 2017 RC1 での SSIS の新機能

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>SSIS の Scale Out での新しい機能と変更された機能

-   スケール アウト マスターで高可用性を実現できるようになりました。 SSISDB に対して Always On を有効にし、Scale Out Master サービスをホストするサーバーに Windows Server フェールオーバー クラスタリングをセットアップできます。 Scale Out Master にこの変更を適用することで、単一障害点を回避し、スケール アウト配置全体の高可用性を実現できます。
-   スケール アウト ワーカーの実行ログのフェールオーバー処理が改善されました。 Scale Out Worker が予期せず停止した場合、実行ログはローカル ディスクに保存されます。 後で worker が再起動すると、保存されているログを再度読み込んで、SSISDB への保存を続けます。
-   ストアド プロシージャ **[catalog].[create_execution]** の *runincluster* パラメーターは、一貫性とわかりやすさを理由に、名前が *runinscaleout* に変更されました。 このパラメーター名の変更には、次の影響があります。
    -   Scale Out でパッケージを実行する既存のスクリプトがある場合は、スクリプトが RC1 で動作するように、パラメーター名を *runincluster* から *runinscaleout* に変更します。
    -   SQL Server Management Studio (SSMS) 17.1 とそれより前のバージョンでは、RC1 の Scale Out でパッケージの実行をトリガーできません。 エラー メッセージ: " *@runincluster* はプロシージャ **create_execution** のパラメーターではありません。" この問題は、SSMS の次のリリースであるバージョン 17.2 で解決されています。 SSMS のバージョン 17.2 以降では、新しいパラメーター名と Scale Out でのパッケージ実行がサポートされています。SSMS バージョン 17.2 が利用可能になるまでは、回避策として、既存バージョンの SSMS を使用してパッケージ実行スクリプトを生成し、そのスクリプトで *runincluster* パラメーターの名前を *runinscaleout* に変更したうえで、スクリプトを実行します。
-   SSIS カタログに、SSIS パッケージを実行する既定のモードを指定するための新しいグローバル プロパティが追加されました。 *runinscaleout* パラメーターを null に設定して **[catalog].[create_execution]** ストアド プロシージャを呼び出すと、この新しいプロパティが適用されます。 このモードは、SSIS SQL エージェント ジョブにも適用されます。 新しいグローバル プロパティは、SSMS の SSISDB ノードの [プロパティ] ダイアログ ボックスで、または次のコマンドで設定できます。
    ```sql
    EXEC [catalog].[configure_catalog] @property_name=N'DEFAULT_EXECUTION_MODE', @property_value=1
    ```

## <a name="new-in-ssis-in-sql-server-2017-ctp-21"></a>SQL Server 2017 CTP 2.1 での SSIS の新機能

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>SSIS の Scale Out での新しい機能と変更された機能

-   Scale Out で実行をトリガーするときに、**Use32BitRuntime** パラメーターを使用できるようになりました。
-   Scale Out でのパッケージ実行に対する SSISDB へのログ記録のパフォーマンスが向上しました。 イベント メッセージとメッセージ コンテキストのログが、1 つずつではなくバッチ モードで SSISDB に書き込まれるようになりました。 この機能強化についての追加の注意事項を次に示します。        
    - 現在のバージョンの SQL Server Management Studio (SSMS) での一部のレポートでは、現在、Scale Out での実行に対するこれらのログが表示されません。SSMS の次のリリースではサポートされる予定です。 影響を受けるレポートは、"*すべての接続*" レポート、"*エラー コンテキスト*" レポート、Integration Service ダッシュボードの "*接続情報*" セクションなどです。
    - 新しい列 **event_message_guid** が追加されました。 Scale Out でこれらの実行ログのクエリを行うときは、**event_message_id** を使うのではなく、この列を使って [catalog].[event_message_context] ビューと [catalog].[event_messages] ビューを結合します。
-   SSIS Scale Out 用の管理アプリケーションを入手するには、[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17.1 以降をダウンロードしてください。

## <a name="new-in-ssis-in-sql-server-2017-ctp-20"></a>SQL Server 2017 CTP 2.0 での SSIS の新機能

SQL Server 2017 CTP 2.0 には、SSIS の新機能はありません。

## <a name="new-in-ssis-in-sql-server-2017-ctp-14"></a>SQL Server 2017 CTP 1.4 での SSIS の新機能

SQL Server 2017 CTP 1.4 には、SSIS の新機能はありません。

## <a name="new-in-ssis-in-sql-server-2017-ctp-13"></a>SQL Server 2017 CTP 1.3 での SSIS の新機能

SQL Server 2017 CTP 1.3 には、SSIS の新機能はありません。

## <a name="new-in-ssis-in-sql-server-2017-ctp-12"></a>SQL Server 2017 CTP 1.2 での SSIS の新機能

SQL Server 2017 CTP 1.2 には、SSIS の新機能はありません。

## <a name="new-in-ssis-in-sql-server-2017-ctp-11"></a>SQL Server 2017 CTP 1.1 での SSIS の新機能

SQL Server 2017 CTP 1.1 には、SSIS の新機能はありません。

## <a name="new-in-ssis-in-sql-server-2017-ctp-10"></a>SQL Server 2017 CTP 1.0 での SSIS の新機能

### <a name="scale-out-for-ssis"></a>SSIS のスケール アウト

スケール アウト機能により、複数のコンピューターで [!INCLUDE[ssIS_md](../includes/ssis-md.md)] を実行することが簡単になりました。 
   
Scale Out Master と Scale Out Worker をインストールすると、パッケージを配布し、さまざまな Worker で自動的に実行できます。 実行が予期せずに終了した場合、自動的に再試行されます。 また、Master を利用し、すべての実行と Worker が中央管理されます。
   
詳細については、[「Integration Services Scale Out」](../integration-services/scale-out/integration-services-ssis-scale-out.md) を参照してください。
   
### <a name="support-for-microsoft-dynamics-online-resources"></a>Microsoft Dynamics オンライン リソースのサポート

OData ソースと OData 接続マネージャーで、Microsoft Dynamics AX Online と Microsoft Dynamics CRM Online の OData フィードに接続できるようになりました。

