---
title: SQL サンプルでデータを生成 WideWorldImporters
ms.date: 04/04/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 0f880ea881b53c2600fb1fffdf7da5d16ab8d423
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056282"
---
# <a name="wideworldimporters-data-generation"></a>WideWorldImporters データ生成
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
リリースされたバージョンの WideWorldImporters および WideWorldImportersDW データベースには、2013年1月1日から、データベースが生成された日までのデータが含まれています。

これらのサンプルデータベースを使用する場合は、より新しいサンプルデータを含めることをお勧めします。

## <a name="data-generation-in-wideworldimporters"></a>WideWorldImporters でのデータ生成

現在の日付までのサンプルデータを生成するには:

1. WideWorldImporters データベースのクリーンバージョンをまだインストールしていない場合は、インストールします。 インストール手順については、「[インストールと構成](wide-world-importers-oltp-install-configure.md)」を参照してください。
2. データベースで次のステートメントを実行します。

    ```
        EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
            @AverageNumberOfCustomerOrdersPerDay = 60,
            @SaturdayPercentageOfNormalWorkDay = 50,
            @SundayPercentageOfNormalWorkDay = 0,
            @IsSilentMode = 1,
            @AreDatesPrinted = 1;
    ```

    このステートメントは、現在の日付までのサンプルの売上および購入データをデータベースに追加します。 日単位のデータ生成の進行状況が表示されます。 データの生成には、データを必要とする年ごとに約10分かかることがあります。 データ生成にはランダムな要因があるため、実行の間に生成されるデータにはいくつかの違いがあります。

    1日あたりの注文に対して生成されるデータの量を増減するには、`@AverageNumberOfCustomerOrdersPerDay`パラメーターの値を変更します。 `@SaturdayPercentageOfNormalWorkDay` および `@SundayPercentageOfNormalWorkDay` パラメーターを使用して、週末の日付の注文量を決定します。

## <a name="import-generated-data-in-wideworldimportersdw"></a>WideWorldImportersDW で生成されたデータをインポートする

WideWorldImportersDW OLAP データベースの現在の日付までサンプルデータをインポートするには、次のようにします。

1. 前のセクションの手順に従って、WideWorldImporters OLTP データベースでデータ生成ロジックを実行します。
2. まだ行っていない場合は、WideWorldImportersDW データベースのクリーンバージョンをインストールします。 インストール手順については、「[インストールと構成](wide-world-importers-oltp-install-configure.md)」を参照してください。
3. データベースで次のステートメントを実行して、OLAP データベースを再シードします。

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. 日次の*ETL. ispac* SQL Server Integration Services パッケージを実行して、OLAP データベースにデータをインポートします。 ETL ジョブを実行する方法については、「 [WIDEWORLDIMPORTERS etl workflow](wide-world-importers-perform-etl.md)」を参照してください。

## <a name="generate-data-in-wideworldimportersdw-for-performance-testing"></a>パフォーマンステストのために WideWorldImportersDW でデータを生成する

WideWorldImportersDW は、パフォーマンステストのためにデータサイズを任意に増やすことができます。 たとえば、クラスター化列ストアインデックス作成で使用するデータサイズを増やすことができます。

課題の1つとして、ダウンロードのサイズを小さくして、簡単にダウンロードできるようにすることができます。ただし、SQL Server のパフォーマンス機能を示すのに十分な大きさです。 たとえば、列ストアインデックスの大きな利点は、大量の行を処理する場合にのみ実現されます。 

`Application.Configuration_PopulateLargeSaleTable` の手順を使用して、`Fact.Sale` テーブル内の行の数を増やすことができます。 2013年1月1日からの既存のワールドワイドインポーターデータとの衝突を避けるために、行は2012暦年に挿入されます。

### <a name="procedure-details"></a>プロシージャの詳細

#### <a name="name"></a>[オブジェクト名]

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>パラメーター

  `@EstimatedRowsFor2012` **bigint** (既定値は 1200万)

#### <a name="result"></a>結果

2012年の `Fact.Sale` テーブルには、必要な数の行が挿入されます。 この手順では、行数が1日あたり5万に人為的に制限されます。 この制限を変更することはできますが、この制限は、テーブルの偶発的な overinflations を回避するのに役立ちます。

また、クラスター化列ストアインデックスがまだ適用されていない場合は、この手順も適用されます。
