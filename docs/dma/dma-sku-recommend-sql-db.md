---
title: オンプレミスデータベースの適切な Azure SQL Database SKU を特定します (Data Migration Assistant) |Microsoft Docs
description: Data Migration Assistant を使用して、オンプレミスデータベースの適切な Azure SQL Database SKU を識別する方法について説明します。
ms.custom: ''
ms.date: 05/06/2019
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
ms.author: jtoland
ms.openlocfilehash: d6d329b97946d9d8042641653ed0167510a19b17
ms.sourcegitcommit: ac90f8510c1dd38d3a44a45a55d0b0449c2405f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72586735"
---
# <a name="identify-the-right-azure-sql-databasemanaged-instance-sku-for-your-on-premises-database"></a>オンプレミスデータベースの適切な Azure SQL Database/Managed Instance SKU を特定する

データベースをクラウドに移行することは、特にデータベースに最適な Azure データベースターゲットと SKU を選択する場合には複雑になることがあります。 データベース Migration Assistant (DMA) の目標は、これらの質問に対処し、ユーザーにわかりやすい出力でこれらの SKU の推奨事項を提供することで、データベースの移行を容易にすることです。

この記事では、DMA の Azure SQL Database SKU に関する推奨事項について説明します。 Azure SQL Database には、次のようないくつかの展開オプションがあります。

- 1つのデータベース
- エラスティックプール
- マネージド インスタンス

SKU の推奨事項機能を使用すると、データベースをホストしているコンピューターから収集されたパフォーマンスカウンターに基づいて、最小推奨 Azure SQL Database 単一データベースまたはマネージインスタンス SKU の両方を識別できます。 この機能は、価格レベル、コンピューティングレベル、最大データサイズに関連する推奨事項と、1か月あたりの推定コストを提供します。 また、推奨されるすべてのデータベースに対して、単一データベースとマネージインスタンスを Azure に一括でプロビジョニングする機能も用意されています。

> [!NOTE]
> 現在、この機能は、コマンドラインインターフェイス (CLI) を介してのみ使用できます。

次に示すのは、Azure SQL Database SKU の推奨事項を特定し、対応する単一データベースまたは Azure のマネージインスタンスを DMA を使用してプロビジョニングするための手順です。

## <a name="prerequisites"></a>[前提条件]

- 最新バージョンの[DMA](https://aka.ms/get-dma)をダウンロードしてインストールします。 以前のバージョンのツールが既にある場合は、それを開くと、DMA をアップグレードするように求められます。
- すべてのスクリプトを実行するために必要な[PowerShell バージョン 5.1](https://www.microsoft.com/download/details.aspx?id=54616)以降がコンピューターにインストールされていることを確認します。 コンピューターにインストールされている PowerShell のバージョンを findoug する方法については、「 [Windows powershell 5.1 のダウンロードとインストール](https://docs.microsoft.com/skypeforbusiness/set-up-your-computer-for-windows-powershell/download-and-install-windows-powershell-5-1)」を参照してください。
- コンピューターに Azure Powershell モジュールがインストールされていることを確認します。 詳細については、「 [Install the Azure PowerShell module](https://docs.microsoft.com/powershell/azure/install-az-ps?view=azps-1.8.0)」を参照してください。
- パフォーマンスカウンターを収集するために必要な PowerShell ファイル**SkuRecommendationDataCollectionScript**が、DMA フォルダーにインストールされていることを確認します。
- このプロセスを実行するコンピューターに、データベースをホストしているコンピューターに対する管理者権限があることを確認します。

## <a name="collect-performance-counters"></a>パフォーマンスカウンターの収集

プロセスの最初の手順では、データベースのパフォーマンスカウンターを収集します。 パフォーマンスカウンターを収集するには、データベースをホストするコンピューターで PowerShell コマンドを実行します。 DMA はこの PowerShell ファイルのコピーを提供しますが、独自の方法を使用してコンピューターからパフォーマンスカウンターをキャプチャすることもできます。

各データベースに対してこのタスクを個別に実行する必要はありません。 コンピューターから収集されたパフォーマンスカウンターは、コンピューターでホストされているすべてのデータベースの SKU を推奨するために使用できます。

1. DMA フォルダーで、PowerShell ファイル SkuRecommendationDataCollectionScript を見つけます。 このファイルは、パフォーマンスカウンターを収集するために必要です。

    ![PowerShell ファイルが DMA フォルダーに表示される](../dma/media/dma-sku-recommend-data-collection-file.png)

2. 次の引数を指定して PowerShell スクリプトを実行します。
    - **ComputerName**: データベースをホストするコンピューターの名前。
    - **Outputfilepath**: 収集されたカウンターを保存する出力ファイルのパス。
    - **CollectionTimeInSeconds**: パフォーマンスカウンターデータを収集する時間の長さ。 パフォーマンスカウンターを少なくとも40分間キャプチャして、意味のある推奨事項を取得します。 キャプチャの実行時間が長いほど、推奨事項が正確になります。 また、必要なデータベースに対してワークロードが実行されていることを確認し、より正確な推奨事項を有効にします。
    - **Dbconnectionstring**: パフォーマンスカウンターデータを収集しているコンピューターでホストされている master データベースを指す接続文字列。

    呼び出しの例を次に示します。

    ```
    .\SkuRecommendationDataCollectionScript.ps1
     -ComputerName Foobar1
     -OutputFilePath D:\counters2.csv
     -CollectionTimeInSeconds 2400
     -DbConnectionString "Server=localhost;Initial Catalog=master;Integrated Security=SSPI;"
    ```

    コマンドの実行後、プロセスは、指定した場所にパフォーマンスカウンターを含むファイルを出力します。 このファイルは、プロセスの次の部分の入力として使用できます。これにより、単一データベースとマネージインスタンスの両方のオプションについて SKU の推奨事項が提供されます。

## <a name="use-the-dma-cli-to-get-sku-recommendations"></a>DMA CLI を使用して SKU の推奨事項を取得する

このプロセスの入力として作成したパフォーマンスカウンターの出力ファイルを使用します。

シングルデータベースオプションの場合、DMA は、Azure SQL Database 単一データベースの価格レベル、コンピューティングレベル、およびコンピューター上の各データベースの最大データサイズに関する推奨事項を提供します。 コンピューターに複数のデータベースがある場合は、推奨されるデータベースを指定することもできます。 DMA では、各データベースの月額料金を見積もることもできます。

マネージインスタンスの場合、推奨事項でリフトアンドシフトのシナリオがサポートされます。 その結果、DMA によって、Azure SQL Database マネージインスタンスの価格レベル、コンピューティングレベル、およびコンピューター上のデータベースセットの最大データサイズに関する推奨事項が提供されます。 ここでも、コンピューターに複数のデータベースがある場合は、推奨設定を行うデータベースを指定することもできます。 また、DMA を使用すると、マネージインスタンスの月額料金を見積もることができます。

DMA CLI を使用して SKU の推奨事項を取得するには、コマンドプロンプトで次の引数を指定して dmacmd を実行します。

- **/Action = SkuRecommendation**: SKU 評価を実行するには、この引数を入力します。
- **/SkuRecommendationInputDataFilePath**: 前のセクションで収集したカウンターファイルへのパスです。
- **/SkuRecommendationTsvOutputResultsFilePath**: 出力を書き込むパスは、TSV 形式になります。
- **/SkuRecommendationJsonOutputResultsFilePath**: 出力を書き込むパスは JSON 形式になります。
- **/SkuRecommendationHtmlResultsFilePath**: 出力結果を HTML 形式で書き込むためのパス。

さらに、次のいずれかの引数を選択します。

- 価格更新を禁止する
  - **/SkuRecommendationPreventPriceRefresh**: True に設定すると、価格更新が発生しなくなり、既定の価格が想定されます。 オフラインモードで実行している場合は、を使用します。 このパラメーターを使用しない場合は、以下のパラメーターを指定して、指定した領域に基づいて最新の価格を取得する必要があります。
- 最新の価格を取得する
  - **/SkuRecommendationCurrencyCode**: 価格を表示する通貨 (例: "USD")。
  - **/SkuRecommendationOfferName**: プラン名 (例: "MS-azr-0003P")。 詳細については、 [Microsoft Azure プランの詳細](https://azure.microsoft.com/support/legal/offer-details/)に関するページを参照してください。
    - **/SkuRecommendationRegionName**: リージョン名 (たとえば、"WestUS")。
    - **/SkuRecommendationSubscriptionId**: サブスクリプション ID。
    - **/Azureauthenticationtenantid**: 認証テナント。
    - **/Azureauthenticationclientid**: 認証に使用される AAD アプリのクライアント ID。
    - 次のいずれかの認証オプション。
      - Interactive
        - **Azureauthenticationinteractiveauthentication**: 認証ポップアップウィンドウの場合は true に設定されます。
      - 証明書ベース
        - **AzureAuthenticationCertificateStoreLocation**: 証明書ストアの場所 (例: "CurrentUser") に設定します。
        - **Azureauthenticationcertificatethumbprint**: 証明書の拇印に設定します。
      - トークンベース
        - **Azureauthenticationtoken**: 証明書トークンに設定されます。

> [!NOTE]
> 対話型認証のために ClientId と TenantId を取得するには、新しい AAD アプリケーションを構成する必要があります。 認証とこれらの資格情報の取得の詳細については、「 [Microsoft Azure BILLING api のサンプル: RATECARD API](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)」の記事で、「**手順 1: AAD テナントでのネイティブクライアントアプリケーションの構成**」に記載されている手順に従います。

最後に、推奨設定が必要なデータベースを指定するために使用できるオプションの引数があります。 

- **/SkuRecommendationDatabasesToRecommend**: 推奨設定を行うデータベースの一覧。 データベース名は大文字と小文字が区別されます。 (1) は、それぞれ二重引用符で囲んで (2)、二重引用符で囲み、(3) それぞれの名前の間に1つのスペースで区切られます (例:/SkuRecommendationDatabasesToRecommend = "Database1" "Database2" "Database3"). このパラメーターを省略すると、入力 .csv ファイルで識別されるすべてのユーザーデータベースに対して推奨設定が提供されます。  

呼び出しの例を次に示します。

**サンプル 1: 既定の価格で推奨事項を取得する。オフラインモードで実行する場合、または認証資格情報がない場合は、を使用します。**

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true
```

**サンプル 2: 指定された地域 (例: "UKWest") の最新価格で推奨事項を取得する。**

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationInteractiveAuthentication=true
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
```

**サンプル 3: 特定のデータベース (例: "TPCDS1G, EDW_3G, TPCDS10G") の推奨事項を取得する。**

```
.\DmaCmd.exe /Action=SkuRecommendation 
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv" 
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv" 
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json" 
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html" 
/SkuRecommendationCurrencyCode=USD 
/SkuRecommendationOfferName=MS-AZR-0044p 
/SkuRecommendationRegionName=UKWest 
/SkuRecommendationSubscriptionId=<Your Subscription Id> 
/SkuRecommendationDatabasesToRecommend=“TPCDS1G” “EDW_3G” “TPCDS10G” 
/AzureAuthenticationInteractiveAuthentication=true 
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId> 
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
```

単一データベースの推奨事項の場合、TSV 出力ファイルは次のようになります。

![PowerShell の単一 db ファイルが DMA フォルダーに表示される](../dma/media/dma-sku-recommend-single-db-recommendations.png)

マネージインスタンスの推奨事項については、TSV 出力ファイルは次のようになります。

![PowerShell マネージインスタンスファイルが DMA フォルダーに表示される](../dma/media/dma-sku-recommend-mi-recommendations.png)

出力ファイルの各列の説明は次のとおりです。

- **DatabaseName** -データベースの名前。
- **Metrictype** -単一データベース/マネージインスタンス層 Azure SQL Database 推奨されます。
- **Metricvalue** -単一データベース/マネージインスタンス SKU の Azure SQL Database をお勧めします。
- **PricePerMonth** –対応する SKU の月あたりの推定料金です。
- **Regionname** –対応する SKU のリージョン名。 
- **I(推奨**)-各レベルに対して SKU の最小推奨事項を作成します。 次に、ヒューリスティックを適用して、データベースの適切なレベルを決定します。 これは、データベースに推奨されるレベルを表します。 
- **ExclusionReasons** -この値は、レベルが推奨されている場合は空白です。 推奨されていない階層ごとに、選択されなかった理由が示されます。
- 適用された規則-適用され**た規則の**短い表記。

最終的に推奨されるレベル ( **Metrictype**) と値 (つまり**metrictype**) は、 **Iの推奨**列が TRUE である場所で見つかりました。 Azure でクエリを実行するために必要な最小 SKU を反映します。オンプレミスのデータベース。 マネージインスタンスの場合、現在のところ、DMA では、最も一般的に使用される8vcore から 40vcore Sku への推奨事項がサポートされています。 たとえば、standard レベルでは、推奨される最小 SKU が S4 の場合、S3 以下を選択すると、クエリがタイムアウトになるか、実行に失敗します。

HTML ファイルには、この情報がグラフィック形式で含まれています。 最終的な推奨事項を表示し、プロセスの次の部分をプロビジョニングするためのわかりやすい手段を提供します。 HTML 出力の詳細については、次のセクションを参照してください。

## <a name="provision-recommended-skus-to-azure"></a>推奨される Sku を Azure にプロビジョニングする

わずか数回のクリックで、特定された推奨事項を使用して、データベースを移行できる Azure のターゲット Sku をプロビジョニングできます。 HTML ファイルを使用して Azure サブスクリプションを入力できます。データベースの価格レベル、コンピューティングレベル、最大データサイズを選択します。とは、データベースをプロビジョニングするためのスクリプトを生成します。 このスクリプトは、PowerShell を使用して実行できます。

このプロセスは、1台のコンピューターで実行することも、複数のコンピューターで実行して、大規模な SKU の推奨事項を確認することもできます。 現在、DMA では、コマンドラインインターフェイスを使用してプロセス全体をサポートすることで、シンプルでスケーラブルなエクスペリエンスを実現しています。

プロビジョニング情報を入力して推奨設定を変更するには、次のように HTML ファイルを更新します。

**単一データベースの推奨事項**

![Azure SQL DB SKU の推奨事項画面](../dma/media/dma-sku-recommend-single-db-recommendations1.png)

1. HTML ファイルを開き、次の情報を入力します。
    - **サブスクリプション id** -データベースのプロビジョニング先となる Azure サブスクリプションのサブスクリプション id。
    - [**リソースグループ]** -データベースをデプロイするリソースグループ。 存在するリソースグループを入力してください。
    - **Region** -データベースをプロビジョニングするリージョン。 サブスクリプションで選択したリージョンがサポートされていることを確認します。
    - **サーバー名**-データベースを配置する Azure SQL Database サーバー。 存在しないサーバー名を入力すると、サーバー名が作成されます。
    - **管理者のユーザー**名-サーバー管理者のユーザー名。
    - **管理者パスワード**-サーバー管理者パスワード。 パスワードは8文字以上、長さが128文字以下でなければなりません。 パスワードには、英大文字、英小文字、数字 (0-9)、英数字以外の文字 (!、$、#、% など) の3つのカテゴリの文字を含める必要があります。 パスワードには、ユーザー名のすべてまたは一部 (3 + 連続する文字) を含めることはできません。

2. 各データベースの推奨事項を確認し、必要に応じて価格レベル、コンピューティングレベル、最大データサイズを変更します。 現在プロビジョニングしないデータベースは、必ず選択解除してください。

3. **[プロビジョニングスクリプトの生成]** を選択し、スクリプトを保存して、PowerShell で実行します。

    このプロセスでは、HTML ページで選択したすべてのデータベースが作成されます。

**マネージインスタンスの推奨事項について**

![Azure SQL MI SKU の推奨事項画面](../dma/media/dma-sku-recommend-mi-recommendations1.png)

1. HTML ファイルを開き、次の情報を入力します。
    - **サブスクリプション id** -データベースのプロビジョニング先となる Azure サブスクリプションのサブスクリプション id。
    - [**リソースグループ]** -データベースをデプロイするリソースグループ。 存在するリソースグループを入力してください。
    - **Region** -データベースをプロビジョニングするリージョン。 サブスクリプションで選択したリージョンがサポートされていることを確認します。
    - **[インスタンス名]** –データベースの移行先となる Azure SQL Managed Instance のインスタンス。 インスタンス名には、小文字、数字、および '-' のみを使用できますが、先頭または末尾を '-' にしたり、63文字を超えたりすることはできません。
    - **インスタンス管理者のユーザー名**–インスタンス管理者のユーザー名。 ログイン名が次の要件を満たしていることを確認してください。これは、一般的なシステム名 (admin、administrator、sa、root、dbmanager、loginmanager など)、または組み込みのデータベースユーザーまたはロール (dbo、guest、public など) ではなく、SQL 識別子です。 名前に空白文字、Unicode 文字、またはアルファベット以外の文字が含まれていないこと、および数字や記号で始まらないことを確認します。 
    - **インスタンス管理者パスワード**-インスタンス管理者パスワード。 パスワードは16文字以上、長さが128文字以下でなければなりません。 パスワードには、英大文字、英小文字、数字 (0-9)、英数字以外の文字 (!、$、#、% など) の3つのカテゴリの文字を含める必要があります。 パスワードには、ユーザー名のすべてまたは一部 (3 + 連続する文字) を含めることはできません。
    - **[Vnet 名]** –マネージインスタンスをプロビジョニングする必要がある vnet の名前。 既存の VNet 名を入力します。
    - **[サブネット名]** –マネージインスタンスをプロビジョニングするサブネットの名前。 既存のサブネット名を入力します。

2. 各インスタンスの推奨事項を確認し、必要に応じて価格レベル、コンピューティングレベル、最大データサイズを変更します。 現在、推奨事項は8vcore から 40vcore Sku に制限されていますが、必要に応じて、64vcore と 80vcore Sku をプロビジョニングするオプションもあります。 現在プロビジョニングしていないすべてのインスタンスの選択を解除してください。

    このプロセスでは、HTML ページで選択したすべてのデータベースが作成されます。

    > [!NOTE]
    > サブネット (特に初めて) でマネージインスタンスを作成するには、完了までに数時間かかることがあります。 PowerShell を使用してプロビジョニングスクリプトを実行した後、Azure Portal でデプロイの状態を確認できます。

## <a name="next-step"></a>次の手順

- CLI から DMA を実行するためのコマンドの完全な一覧については、「[コマンドラインから Data Migration Assistant を実行](https://docs.microsoft.com/sql/dma/dma-commandline?view=sql-server-2017)する」を参照してください。
