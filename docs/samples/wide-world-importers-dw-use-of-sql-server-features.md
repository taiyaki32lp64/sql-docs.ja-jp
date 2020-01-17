---
title: DW WideWorldImporters データベースの主機能
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: dfce2ce4a6f13a25687d668268f532893c1404e0
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056288"
---
# <a name="wideworldimportersdw-use-of-sql-server-features-and-capabilities"></a>SQL Server の機能の WideWorldImportersDW 使用方法
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
WideWorldImportersDW は、データウェアハウスと分析に適した SQL Server の主な機能の多くを紹介するように設計されています。 SQL Server の機能の一覧と、それらが WideWorldImportersDW でどのように使用されるかについての説明を次に示します。

## <a name="polybase"></a>PolyBase

[SQL Server に適用されます (2016 以降)]

PolyBase を使用して、WideWorldImportersDW の売上情報と、人口統計に関するパブリックデータセットを結合し、売上をさらに拡大するために関心のある都市を把握します。

サンプルデータベースで PolyBase を使用できるようにするには、PolyBase がインストールされていることを確認し、データベースで次のストアドプロシージャを実行します。

    EXEC [Application].[Configuration_ApplyPolyBase]

これにより、Azure blob storage でホストされている米国内の都市の人口データを含むパブリックデータセットを参照する外部テーブル `dbo.CityPopulationStatistics` が作成されます。 構成プロセスを理解するために、ストアドプロシージャのコードを確認することをお勧めします。 Azure blob storage で独自のデータをホストし、一般公開されているデータの安全性を維持するには、追加の構成手順を実行する必要があります。 次のクエリでは、その外部データセットからデータが返されます。

    SELECT CityID, StateProvinceCode, CityName, YearNumber, LatestRecordedPopulation FROM dbo.CityPopulationStatistics;

次のクエリでは、さらに拡張するために関心がある都市を把握するために、都市の成長率を確認し、大幅に増加している上位100の都市を返します。また、大規模な輸入者には売上が存在しません。 このクエリでは、リモートテーブル `dbo.CityPopulationStatistics` とローカルテーブル `Dimension.City`との間の結合、およびローカルテーブル `Fact.Sales`を含むフィルターが関係しています。

    WITH PotentialCities
    AS
    (
        SELECT cps.CityName,
               cps.StateProvinceCode,
               MAX(cps.LatestRecordedPopulation) AS PopulationIn2016,
               (MAX(cps.LatestRecordedPopulation) - MIN(cps.LatestRecordedPopulation)) * 100.0
                   / MIN(cps.LatestRecordedPopulation) AS GrowthRate
        FROM dbo.CityPopulationStatistics AS cps
        WHERE cps.LatestRecordedPopulation IS NOT NULL
        AND cps.LatestRecordedPopulation <> 0
        GROUP BY cps.CityName, cps.StateProvinceCode
    ),
    InterestingCities
    AS
    (
        SELECT DISTINCT pc.CityName,
                        pc.StateProvinceCode,
                        pc.PopulationIn2016,
                        FLOOR(pc.GrowthRate) AS GrowthRate
        FROM PotentialCities AS pc
        INNER JOIN Dimension.City AS c
        ON pc.CityName = c.City
        WHERE GrowthRate > 2.0
        AND NOT EXISTS (SELECT 1 FROM Fact.Sale AS s WHERE s.[City Key] = c.[City Key])
    )
    SELECT TOP(100) CityName, StateProvinceCode, PopulationIn2016, GrowthRate
    FROM InterestingCities
    ORDER BY PopulationIn2016 DESC;

## <a name="clustered-columnstore-indexes"></a>クラスター化列ストア インデックス

(完全バージョンのサンプル)

クラスター化列ストアインデックス (CCI) はすべてのファクトテーブルと共に使用され、ストレージフットプリントを削減し、クエリのパフォーマンスを向上させます。 CCI を使用すると、ファクトテーブルの基本ストレージでは列の圧縮が使用されます。

非クラスター化インデックスは、主キー制約と外部キー制約を容易にするために、クラスター化列ストアインデックスの上に使用されます。 これらの制約は、細心の注意を払って追加されました。 ETL プロセスは、整合性を適用するための制約がある WideWorldImporters データベースからデータを送信します。 Primary キー制約と foreign key 制約、およびそれらのサポートインデックスを削除すると、ファクトテーブルのストレージフットプリントが減少します。

**データサイズ**

サンプルデータベースには、サンプルを簡単にダウンロードしてインストールできるように、データサイズが制限されています。 ただし、列ストアインデックスの実際のパフォーマンス上の利点を確認するには、より大きなデータセットを使用することをお勧めします。

次のステートメントを実行すると、別の1200万行のサンプルデータを挿入して `Fact.Sales` テーブルのサイズを増やすことができます。 これらの行はすべて2012年に挿入され、ETL プロセスに干渉しないようになっています。

    EXECUTE [Application].[Configuration_PopulateLargeSaleTable]

このステートメントの実行には約5分かかります。 1200万を超える行を挿入するには、挿入する行の数をこのストアドプロシージャにパラメーターとして渡します。

列ストアの有無に関係なく、クエリのパフォーマンスを比較するには、クラスター化列ストアインデックスを削除または再作成します。

インデックスを削除するには、次のようにします。

    DROP INDEX [CCX_Fact_Order] ON [Fact].[Order]

再作成するには:

    CREATE CLUSTERED COLUMNSTORE INDEX [CCX_Fact_Order] ON [Fact].[Order]

## <a name="partitioning"></a>[パーティション分割]

(完全バージョンのサンプル)

データウェアハウスのデータサイズが非常に大きくなることがあります。 そのため、データベース内の大きなテーブルのストレージを管理するには、パーティション分割を使用することをお勧めします。

より大きなファクトテーブルはすべて年でパーティション分割されます。 唯一の例外は `Fact.Stock Holdings`です。これは、日付ベースではなく、他のファクトテーブルと比較してデータサイズが制限されています。

すべてのパーティションテーブルに使用されるパーティション関数が `PF_Date`、使用されているパーティション構成が `PS_Date`ます。

## <a name="in-memory-oltp"></a>インメモリ OLTP

(完全バージョンのサンプル)

WideWorldImportersDW は、ステージングテーブルに SCHEMA_ONLY メモリ最適化テーブルを使用します。 すべての `Integration.`*`_Staging` テーブルは、メモリ最適化テーブル SCHEMA_ONLY ます。

SCHEMA_ONLY テーブルの利点は、ログに記録されず、ディスクにアクセスする必要がないことです。 これにより、ETL プロセスのパフォーマンスが向上します。 これらのテーブルはログに記録されないため、エラーが発生した場合、内容は失われます。 ただし、データソースは引き続き使用できるので、エラーが発生した場合は ETL プロセスを再起動するだけで済みます。
