---
title: Data Migration Assistant を使用してエンタープライズを評価し、評価レポートを統合する
description: SQL Server をアップグレードする前、または Azure SQL Database に移行する前に、DMA を使用して企業を評価し、評価レポートを統合する方法について説明します。
ms.date: 06/21/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: ec8ededac012ccb2b3d4b62fc40d84132a6fb882
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056648"
---
# <a name="assess-an-enterprise-and-consolidate-assessment-reports-with-dma"></a>企業を評価し、DMA で評価レポートを統合する

次のステップバイステップの手順では、Data Migration Assistant を使用して、オンプレミスの SQL Server または Azure Vm で実行されている SQL Server のアップグレード、または Azure SQL Database への移行について、適切なスケール評価を実行する方法について説明します。

## <a name="prerequisites"></a>Prerequisites

- DMA を開始するネットワーク上のツールコンピューターを指定します。 このコンピューターが SQL Server ターゲットに接続されていることを確認します。
- ダウンロードしてインストールする:
  - [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) v 3.6 以降。
  - [PowerShell](https://aka.ms/wmf5download) v1.0 以降。
  - [.NET Framework](https://www.microsoft.com/download/details.aspx?id=30653) version 4.5 以降。
  - [SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17.0 以降。
  - [Power BI デスクトップ](https://docs.microsoft.com/power-bi/desktop-get-the-desktop)。
  - [Azure PowerShell モジュール](https://docs.microsoft.com/powershell/azure/install-az-ps?view=azps-1.0.0)
- ダウンロードと抽出:
  - [DMA は Power BI テンプレートを報告](https://techcommunity.microsoft.com/gxcuf89792/attachments/gxcuf89792/MicrosoftDataMigration/56/2/PowerBI-Reports.zip)します。
  - [Loadwarehouse スクリプト](https://techcommunity.microsoft.com/gxcuf89792/attachments/gxcuf89792/MicrosoftDataMigration/56/1/LoadWarehouse1.zip)。

## <a name="loading-the-powershell-modules"></a>PowerShell モジュールを読み込んでいます

Powershell モジュールを PowerShell modules ディレクトリに保存すると、使用前にモジュールを明示的に読み込むことなくモジュールを呼び出すことができます。

モジュールを読み込むには、次の手順を実行します。

1. C:\Program Files\WindowsPowerShell\Modules に移動し、 **DataMigrationAssistant**という名前のフォルダーを作成します。
2. [PowerShell モジュール](https://techcommunity.microsoft.com/gxcuf89792/attachments/gxcuf89792/MicrosoftDataMigration/56/4/PowerShell-Modules2.zip)を開き、作成したフォルダーに保存します。

      ![PowerShell モジュール](../dma/media//dma-consolidatereports/dma-powershell-modules.png)

    各フォルダーには、次の図に示すように、関連付けられた hbase-runner.psm1 ファイルが含まれています。

   ![PowerShell modules hbase-runner.psm1 files](../dma/media//dma-consolidatereports/dma-powershell-modules-psm1-files.png)

   > [!NOTE]
   > 含まれているフォルダーと hbase-runner.psm1 ファイルの名前は同じである必要があります。

   > [!IMPORTANT]
   > モジュールが正しく読み込まれるようにするには、PowerShell ファイルを WindowsPowerShell ディレクトリに保存した後でブロックを解除しなければならない場合があります。 PowerShell ファイルのブロックを解除するには、ファイルを右クリックし、 **[プロパティ]** を選択します。次に、 **[ブロック解除]** ボックスをオンにして、[ **Ok]** を選択します。

   ![hbase-runner.psm1 ファイルのプロパティ](../dma/media//dma-consolidatereports/dma-psm1-file-properties.png)

    PowerShell では、新しい PowerShell セッションが開始されたときに、これらのモジュールを自動的に読み込む必要があります。

## <a name="create-inventory"></a>SQL Server のインベントリを作成する

PowerShell スクリプトを実行して SQL Server を評価する前に、評価する SQL server のインベントリを作成する必要があります。

このインベントリは、次の2つの形式のいずれかになります。

- Excel CSV ファイル
- SQL Server テーブル

### <a name="if-using-a-csv-file"></a>CSV ファイルを使用する場合

> [!IMPORTANT]
> インベントリファイルがコンマ区切り (CSV) ファイルとして保存されていることを確認します。
>
> 既定のインスタンスの場合は、[インスタンス名] を「MSSQLServer」に設定します。


Csv ファイルを使用してデータをインポートする場合は、データ**インスタンス名**と**データベース名**の列が2つだけであり、列にヘッダー行がないことを確認します。

 ![csv ファイルの内容](../dma/media//dma-consolidatereports/dma-csv-file-contents.png)

### <a name="if-using-a-sql-server-table"></a>SQL Server テーブルを使用する場合

> [!IMPORTANT]
> 既定のインスタンスの場合は、[インスタンス名] を「MSSQLServer」に設定します。

**Estateinventory**という名前のデータベースと、 **databaseinventory**という名前のテーブルを作成します。 このインベントリデータを含むテーブルには、次の4つの列が存在する限り、任意の数の列を含めることができます。

- ServerName
- InstanceName
- DatabaseName
- AssessmentFlag

![SQL Server テーブルの内容](../dma/media//dma-consolidatereports/dma-sql-server-table-contents.png)

このデータベースがツールコンピューター上にない場合は、ツールコンピューターにこの SQL Server インスタンスへのネットワーク接続があることを確認してください。

CSV ファイルに対して SQL Server テーブルを使用する利点は、[評価フラグ] 列を使用して、評価のために取得されるインスタンス/データベースを制御できることです。これにより、評価をより小さなチャンクに分割しやすくなります。  その後、複数の評価にまたがることができます (この記事で後述する「評価の実行」を参照してください)。これは、複数の CSV ファイルを維持するよりも簡単です。

オブジェクトの数とその複雑さによっては、評価に非常に長い時間 (時間 +) がかかることがあるので、評価を管理しやすいチャンクに分けることが賢明です。

## <a name="running-a-scaled-assessment"></a>スケーリングされた評価の実行

PowerShell モジュールを modules ディレクトリに読み込んでインベントリを作成したら、PowerShell を開き、dmaDataCollector 関数を実行して、スケーリングされた評価を実行する必要があります。
 
  ![dmaDataCollector 関数の一覧](../dma/media//dma-consolidatereports/dma-dmaDataCollector-function-listing.png)

次の表では、dmaDataCollector 関数に関連付けられているパラメーターについて説明します。

|パラメーター  |[説明] |
|---------|---------|
|**getServerListFrom** | インベントリ。 指定できる値は、 **SqlServer**と**CSV**です。<br/>詳細については、「 [SQL server のインベントリを作成](#create-inventory)する」を参照してください。 |
|**csvPath** | CSV インベントリファイルへのパスです。  **GetServerListFrom**が**CSV**に設定されている場合にのみ使用されます。 |
|**serverName** | **GetServerListFrom**パラメーターで**SqlServer**を使用する場合の、インベントリの SQL Server インスタンス名。 |
|**databaseName** | インベントリテーブルをホストしているデータベース。 |
|**AssessmentName** | DMA 評価の名前。 |
|**TargetPlatform** | 実行する評価ターゲットの種類。  指定できる値は、 **AzureSQLDatabase**、 **SQLServer2012**、 **SQLServer2014**、 **Sqlserver2016-ssei-expr**、 **SQLServerLinux2017**、 **SQLServerWindows2017**、および**managedsqlserver**です。 |
|**AuthenticationMethod** | 評価するターゲット SQL Server に接続するための認証方法。 指定できる値は、 **sqlauth**と**windowsauth**です。 |
|**OutputLocation** | JSON 評価出力ファイルを格納するディレクトリ。 評価されるデータベースの数とデータベース内のオブジェクトの数によっては、評価に非常に長い時間がかかることがあります。 すべての評価が完了した後で、ファイルが書き込まれます。 |

予期しないエラーが発生した場合、このプロセスによって開始されたコマンドウィンドウは終了します。  エラーログを確認して、失敗した原因を特定します。
 
  ![エラー ログの場所](../dma/media//dma-consolidatereports/dma-error-log-file-location.png)

## <a name="consuming-the-assessment-json-file"></a>評価 JSON ファイルを使用しています

評価が完了したら、分析のために SQL Server にデータをインポートする準備が整いました。 評価 JSON ファイルを使用するには、PowerShell を開き、dmaProcessor 関数を実行します。
 
  ![dmaProcessor 関数の一覧表示](../dma/media//dma-consolidatereports/dma-dmaProcessor-function-listing.png)

次の表では、dmaProcessor 関数に関連付けられているパラメーターについて説明します。

|パラメーター  |[説明] |
|---------|---------|
|**processTo** | JSON ファイルが処理される場所。 指定できる値は、 **SQLServer**と**AzureSQLDatabase**です。 |
|**serverName** | データが処理される SQL Server インスタンス。  **Processto**パラメーターに**AzureSQLDatabase**を指定する場合は、SQL Server 名のみを含めます (. database.windows.net を含めないでください)。 Azure SQL Database を対象とする場合、2つのログインの入力を求められます。1つ目は Azure テナントの資格情報ですが、2つ目は Azure SQL Server の管理者ログインです。 |
|**作成した Mareporting** | JSON ファイルを処理するために作成するステージングデータベース。  指定したデータベースが既に存在し、このパラメーターを1に設定した場合、オブジェクトは作成されません。  このパラメーターは、削除された1つのオブジェクトを再作成する場合に便利です。 |
|**CreateDataWarehouse** | Power BI レポートによって使用されるデータウェアハウスを作成します。 |
|**databaseName** | DMAReporting データベースの名前。 |
|**warehouseName** | データウェアハウスデータベースの名前。 |
|**jsonDirectory** | JSON 評価ファイルが格納されているディレクトリ。  ディレクトリに複数の JSON ファイルがある場合は、1つずつ処理されます。 |

DmaProcessor 関数は、1つのファイルを処理するのに数秒かかる必要があります。

## <a name="loading-the-data-warehouse"></a>データウェアハウスを読み込んでいます

DmaProcessor が評価ファイルの処理を完了すると、データが ReportData テーブルの DMAReporting データベースに読み込まれます。 この時点で、データウェアハウスを読み込む必要があります。

1. LoadWarehouse スクリプトを使用して、ディメンション内の欠損値を設定します。

    このスクリプトは、DMAReporting データベースの ReportData テーブルからデータを取得し、ウェアハウスに読み込みます。  この読み込み処理中にエラーが発生した場合、ディメンションテーブルにエントリが欠落している可能性があります。

2. データウェアハウスを読み込みます。
 
      ![LoadWarehouse のコンテンツが読み込まれました](../dma/media//dma-consolidatereports/dma-LoadWarehouse-loaded.png)

## <a name="set-your-database-owners"></a>データベースの所有者を設定する

必須ではありませんが、レポートから最大の値を取得するには、 **dimDBOwner**ディメンションでデータベース所有者を設定し、 **FactAssessment**テーブルの**DBOwnerKey**を更新することをお勧めします。  このプロセスに従うと、特定のデータベース所有者に基づいて Power BI レポートをスライスおよびフィルター処理できます。

LoadWarehouse スクリプトを使用して、データベース所有者を設定するための基本的な TSQL ステートメントを指定することもできます。

  ![LoadWarehouse 設定所有者](../dma/media//dma-consolidatereports/dma-LoadWarehouse-set-owners.png)

## <a name="dma-reports"></a>DMA レポート

1. Power BI Desktop で、DMA レポート Power BI テンプレートを開きます。
2. **DMAWarehouse**データベースをポイントするサーバーの詳細を入力し、 **[読み込み]** を選択します。

   ![DMA レポート Power BI テンプレートが読み込まれました](../dma/media//dma-consolidatereports/dma-reports-powerbi-template-loaded.png)

   **DMAWarehouse**データベースのデータがレポートによって更新されると、次のようなレポートが表示されます。

   ![DMAWarehouse レポートビュー](../dma/media//dma-consolidatereports/dma-DMAWarehouse-report1.png)

   > [!TIP]
   > 予期していたデータが表示されない場合は、アクティブなブックマークを変更してみてください。  詳細については、次のセクションの詳細を参照してください。

## <a name="working-with-dma-reports"></a>DMA レポートの操作

DMA レポートを操作するには、次の方法でブックマークとスライサーを使用してフィルター処理を行います。

- 評価の種類 (Azure SQL DB、Azure SQL MI、オンプレミスの SQL) 
- [インスタンス名]
- [データベース名]
- チーム名

[ブックマークとフィルター] ブレードにアクセスするには、メインレポートページの [フィルター] ブックマークを選択します。

![DMA レポートのブックマークとフィルター](../dma/media//dma-consolidatereports/dma-report-bookmarks-filters.png)

フィルターブックマークを選択すると、次のブレードが有効になります。

![DMA レポートビューブレード](../dma/media//dma-consolidatereports/dma-report-views-blade.png)

ブックマークを使用すると、次のようにレポートコンテキストを切り替えることができます。

- Azure SQL DB クラウドの評価
- Azure SQL MI クラウドの評価
- オンプレミスの評価

![DMA レポートビューのブックマーク](../dma/media//dma-consolidatereports/dma-report-bookmarks1.png)

[フィルター] ブレードを非表示にするには、CTRL キーを押しながら [戻る] ボタンをクリックします。

![DMA レポートビュー戻るボタン](../dma/media//dma-consolidatereports/dma-report-bookmarks-back.png)

レポートページの左下に、次のいずれかのアイテムにフィルターが適用されているかどうかを示すメッセージが表示されます。

- FactAssessment – InstanceName
- FactAssessment – DatabaseName
- dimDBOwner-DBOwner

![フィルター適用済みのプロンプト](../dma/media//dma-consolidatereports/dma-filter-applied-prompt.png)

> [!NOTE]
> Azure SQL Database 評価のみを実行する場合は、クラウドレポートのみが設定されます。 逆に、オンプレミスの評価のみを実行する場合は、オンプレミスのレポートのみが設定されます。 ただし、Azure とオンプレミスの評価の両方を実行し、両方の評価をウェアハウスに読み込む場合は、関連するアイコンを CTRL キーを押しながら、クラウドレポートとオンプレミスレポートを切り替えることができます。

## <a name="reports-visuals"></a>レポートのビジュアル

Power BI レポートに表示される詳細については、次のセクションで説明します。

### <a name="readiness-"></a>訴訟

  ![DMA 準備の割合](../dma/media//dma-consolidatereports/dma-readiness-percentage.png)

このビジュアルは、選択コンテキスト (すべてのインスタンス、データベース [のマルチプル]) に基づいて更新されます。

### <a name="readiness-count"></a>準備数

  ![DMA の準備数](../dma/media//dma-consolidatereports/dma-readiness-count.png)

このビジュアルは、まだ移行の準備ができていないデータベースの数を移行する準備ができているデータベースの数を示しています。

### <a name="readiness-bucket"></a>準備バケット

  ![DMA 準備バケット](../dma/media//dma-consolidatereports/dma-readiness-bucket.png)

このビジュアルには、次の準備バケットによるデータベースの内訳が表示されます。

- 100% 準備完了
- 75-99% 準備完了
- 50-75% 準備完了
- 準備ができていません

### <a name="issues-word-cloud"></a>Word Cloud を発行する
 
  ![DMA が WordCloud を発行する](../dma/media//dma-consolidatereports/dma-issues-word-cloud.png)

このビジュアルは、選択コンテキスト内で現在発生している問題を示しています (すべて、インスタンス、データベース [のマルチプル])。 画面に表示される単語が大きいほど、そのカテゴリの問題の数が多くなります。 マウスポインターを word の上に置くと、そのカテゴリで発生した問題の数が表示されます。

### <a name="database-readiness"></a>データベースの準備

  ![DMA データベース準備レポート](../dma/media//dma-consolidatereports/dma-database-readiness-report.png)

このセクションは、レポートの主要な部分であり、インスタンスデータベースの準備状態を示しています。 このレポートのドリルダウン階層は次のとおりです。

- InstanceDatabase
- ChangeCategory
- Title
- ObjectType
- ImpactedObjectName

 ![DMA データベース準備レポートのドリルダウン](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown.png)

このレポートは、修復プランレポートを作成するためのフィルターポイントとしても機能します。

修復プランレポートをドリルダウンするには、このグラフ内のデータポイントを右クリックし、 **[ドリルスルー]** をポイントして、 **[修復プラン]** を選択します。

このタスクは、[ドリルスルー] オプションを選択したポイントに基づいて、修復プランレポートを現在の階層レベルにフィルター処理します。

  ![DMA データベース準備レポートドリルダウンフィルター処理済み](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown-filtered.png)

  ![DMA 修復プランレポート](../dma/media//dma-consolidatereports/dma-remediation-plan-report.png)

また、**視覚化フィルター (視覚エフェクトフィルター** )」ブレードのフィルターを使用して、独自の修復プランレポートを作成することもできます。
 
  ![DMA 修復プランレポートのフィルターオプション](../dma/media//dma-consolidatereports/dma-remediation-plan-report-filter-options.png)

### <a name="script-disclaimer"></a>スクリプトの免責事項

*この記事に記載されているサンプルスクリプトは、Microsoft の標準サポートプログラムまたはサービスではサポートされていません。すべてのスクリプトは、いかなる種類の保証も伴わず、現状有姿のままで提供されます。マイクロソフトはさらに、商品性または特定目的への適合性に関する黙示の保証を含め、一切の黙示の保証を一切いたしません。サンプルスクリプトとドキュメントの使用またはパフォーマンスに起因するリスク全体が、お客様に残ります。Microsoft、その作成者、また、スクリプトの作成、運用、または配信に関係する人は、マイクロソフトがこのような損害の可能性についてのアドバイスを受けたとしても、サンプルスクリプトやドキュメントを使用したり、使用できなかったりした場合でも、いかなる損害 (制限なし、損失、ビジネスの中断、ビジネス情報の損失、またはその他の これらのスクリプトを他のサイト、リポジトリ、ブログに reposting する前に、アクセス許可をシークします。*
