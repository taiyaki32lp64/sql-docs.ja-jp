---
title: テンポラル テーブルの使用シナリオ | Microsoft Docs
ms.custom: ''
ms.date: 05/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 4b8fa2dd-1790-4289-8362-f11e6d63bb09
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: eaac8c264caf9009006853e0f02e258ad5d7408f
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165745"
---
# <a name="temporal-table-usage-scenarios"></a>テンポラル テーブルの使用シナリオ

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

テンポラル テーブルは、データの変更履歴を追跡する必要のあるシナリオに一般的に便利です。 生産性が高まるので、次の用途にテンポラル テーブルを使用することをお勧めします。

## <a name="data-audit"></a>データの監査

何が変更されたか、いつ変更されたかを追跡する必要のある重要な情報が保存されている、また任意の時点のデータ フォレンジクスを実行する必要のあるテーブルには、システム バージョン管理されたテンポラル テーブルを使用します。

システム バージョン管理されたテンポラル テーブルでは、開発サイクルの初期段階でデータの監査シナリオを計画したり、必要な時に既存のアプリケーションまたはソリューションにデータ監査を追加したりできます。

次の図に、現在 (青) と履歴行バージョン (グレー) のデータ サンプルを含む Employee テーブルのシナリオを示します。
図の右側部分では、テンポラル テーブルに対して (SYSTEM_TIME 句を使用した場合、または使用しない場合の) 異なる種類のクエリを実行したときに選択される行バージョンを時間軸により視覚化しています。

![テンポラルの使用シナリオ 1](../../relational-databases/tables/media/temporalusagescenario1.png "テンポラルの使用シナリオ 1")

### <a name="enabling-system-versioning-on-a-new-table-for-data-audit"></a>データ監査用に新しいテーブルでシステム バージョン管理を有効にする

データの監査が必要な情報を特定したら、データベース テーブルをシステム バージョン管理されたテンポラル テーブルとして作成します。 次に、Employee 情報が仮定の HR データベースにあるシナリオの簡単な例を示します。

```sql
CREATE TABLE Employee
(
  [EmployeeID] int NOT NULL PRIMARY KEY CLUSTERED
  , [Name] nvarchar(100) NOT NULL
  , [Position] varchar(100) NOT NULL
  , [Department] varchar(100) NOT NULL
  , [Address] nvarchar(1024) NOT NULL
  , [AnnualSalary] decimal (10,2) NOT NULL
  , [ValidFrom] datetime2 (2) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (2) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.EmployeeHistory));
```

システム バージョン管理されたテンポラル テーブルを作成する際のさまざまなオプションは、「[システム バージョン管理されたテンポラル テーブルの作成](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)」で説明されています。

### <a name="enabling-system-versioning-on-an-existing-table-for-data-audit"></a>データ監査用に既存のテーブルでシステム バージョン管理を有効にする

既存のデータベースのデータを監査する必要がある場合、ALTER TABLE を使用し、非テンポラル テーブルをシステム バージョン管理テーブルにします。 アプリケーションの破壊的変更を回避するために、「[非テンポラル テーブルをシステム バージョン管理されたテンポラル テーブルに変更する](https://msdn.microsoft.com/library/mt590957.aspx#Anchor_3)」の説明に従って、期間列を HIDDEN として追加します。 次の例では、仮定の HR データベース内の既存の Employee テーブルで、システム バージョン管理を有効にする方法について説明します。

```sql
/*
Turn ON system versioning in Employee table in two steps
(1) add new period columns (HIDDEN)
(2) create default history table
*/
ALTER TABLE Employee
ADD
    ValidFrom datetime2 (2) GENERATED ALWAYS AS ROW START HIDDEN
        constraint DF_ValidFrom DEFAULT DATEADD(second, -1, SYSUTCDATETIME())  
    , ValidTo datetime2 (2) GENERATED ALWAYS AS ROW END HIDDEN
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo);
  
ALTER TABLE Employee
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.Employee_History));
```

> [!IMPORTANT]
> datetime2 データ型の有効桁数は、ソース テーブルとシステム バージョン管理された履歴テーブル内と同じです。

前述のスクリプトを実行すると、データに対するすべての変更は履歴テーブルに透過的に収集されます。 典型的なデータの監査シナリオでは、関心のある期間に各行に適用されたすべてのデータ変更を問い合わせます。 この用途に効果的に対応する、クラスター化された行ストア B ツリーを持つ既定の履歴テーブルが作成されます。

### <a name="performing-data-analysis"></a>データ分析の実行

上記のいずれかの方法を使用してシステム バージョン管理を有効にすれば、データの監査はクエリを 1 回のみ実行すればできます。 次のクエリでは、少なくとも 2014年の 1 月 1 日から 2015年 1 月 1 日 (上限の境界を含む) の間にアクティブであった、EmployeeID が 1000 の従業員レコードの行バージョンが検索されます。

```sql
SELECT * FROM Employee
    FOR SYSTEM_TIME
      BETWEEN '2014-01-01 00:00:00.0000000' AND '2015-01-01 00:00:00.0000000'
        WHERE EmployeeID = 1000 ORDER BY ValidFrom;
```

FOR SYSTEM_TIME BETWEEN...AND を FOR SYSTEM_TIME ALL に置き換えると、その特定の従業員のデータの変更履歴がすべて分析されます。

```sql
SELECT * FROM Employee
    FOR SYSTEM_TIME ALL WHERE
        EmployeeID = 1000 ORDER BY ValidFrom;
```

その期間のみアクティブであった行バージョンを探す場合 (それ以外は含みません)、CONTAINED IN を使用します。 このクエリは履歴テーブルのみに対してクエリを行うので、非常に効率的です。

```sql
SELECT * FROM Employee FOR SYSTEM_TIME
    CONTAINED IN ('2014-01-01 00:00:00.0000000', '2015-01-01 00:00:00.0000000')
        WHERE EmployeeID = 1000 ORDER BY ValidFrom;
```

最後に、過去の任意の時点でテーブル全体がどのようであったか確認したい監査シナリオでは、次のように実行します。

```sql
SELECT * FROM Employee FOR SYSTEM_TIME AS OF '2014-01-01 00:00:00.0000000' ;
```

データのフィルター処理と結果の表示には、ローカルのタイム ゾーンを使用した方が常に便利ですが、システム バージョン管理されたテンポラル テーブルでは、期間列の値は UTC タイム ゾーンで保存されます。 次のコード例では、SQL Server 2016 で導入された AT TIME ZONE を使用し、元はローカルのタイム ゾーンが指定され、後で UTC に変換されたものに、フィルター条件を適用する方法を示します。

```sql
/*Add offset of the local time zone to current time*/
DECLARE @asOf DATETIMEOFFSET = GETDATE() AT TIME ZONE 'Pacific Standard Time'
/*Convert AS OF filter to UTC*/
SET @asOf = DATEADD (MONTH, -9, @asOf) AT TIME ZONE 'UTC';

SELECT
    EmployeeID
    , Name
    , Position
    , Department
    , [Address]
    , [AnnualSalary]
    , ValidFrom AT TIME ZONE 'Pacific Standard Time' AS ValidFromPT
    , ValidTo AT TIME ZONE 'Pacific Standard Time' AS ValidToPT
FROM Employee
    FOR SYSTEM_TIME AS OF @asOf where EmployeeId = 1000
```

AT TIME ZONE は、システム バージョン管理されたテーブルを使用するすべてのシナリオに便利です。

> [!TIP]
> FOR SYSTEM_TIME のテンポラル句で指定されたフィルタリング条件は SARG-able です (つまり、 SQL Server は基礎となっているクラスター化インデックスを使用して、スキャン操作ではなくシークを実行します)。
> 履歴テーブルを直接クエリする場合、フィルター条件も、\<期間列> {< | > | =, ...} date_condition AT TIME ZONE 'UTC' の書式を使用して同様に SARGable にする必要があります。
> AT TIME ZONE を期間列に適用すると、SQL Server は非常に負荷のかかるテーブルおよびインデックス スキャンを実行します。 \<期間列> AT TIME ZONE '\<タイム ゾーン>' > {< | > | =, ...} date_condition のような条件は、クエリでは避けてください。

関連項目:[システム バージョン管理されたテンポラル テーブルのデータのクエリ](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)

## <a name="point-in-time-analysis-time-travel"></a>特定の時点の分析 (タイム トラベル)

通常、個々のレコードに発生した変更が注目されるデータの監査とは異なり、タイム トラベルのシナリオでは、ユーザーは、時間の経過とともにデータ セット全体がどのように変わったかを確認したいと考えます。 タイム トラベルには、それぞれが別のペースで変更される、次に示すような分析すべき関連するテンポラル テーブルが含まれることがあります。

- 重要な指標の過去および現在のデータでの傾向
- (昨日や 1 か月前など) 過去の任意の "時点" のデータ全体の正確なスナップショット
- (1 か月前対 3 か月前など) 関心のある 2 つの時点の違い

現実には、タイム トラベル分析が必要なシナリオが多数あります。 この使用シナリオを示す、履歴が自動生成される OLTP で見てみましょう。

### <a name="oltp-with-auto-generated-data-history"></a>自動生成されたデータ履歴を使用する OLTP

トランザクション処理システムでは、しばしば時間の経過とともに重要なメトリックがどのように変わるかが分析されます。 履歴の分析では、理想的には、OLTP アプリケーションのパフォーマンスは落ちないようにする必要があります。これでは、最新状態のデータへ最小限の遅延とデータ ロックでアクセスできる必要があります。 システム バージョン管理されたテンポラル テーブルは、後で分析できるよう、現在のデータとは別に、変更の完全な履歴を透過的に保持できるよう設計されており、これはメインの OLTP ワークロードには最小限にしか影響しません。

トランザクション処理の多いワークロードでは、コスト効率の高い方法で現在のデータをメモリ内に保存し、変更の完全な履歴をディスクに保存できる、[メモリ最適化テーブルでのシステム バージョン管理されたテンポラル テーブル](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)を使用することをお勧めします。

履歴テーブルには、次の理由から、クラスター化列ストア インデックスを使用することお勧めします。

- クラスター化列ストア インデックスのクエリのパフォーマンスは、典型的な傾向の分析に有効です。
- 履歴テーブルにクラスター化列ストア インデックスがあり、OLTP のワークロードが高い場合、メモリが最適化されたテーブルでのデータのフラッシュ タスクは、最も高いパフォーマンスを発揮します。
- クラスター化列ストア インデックスは、特にすべての列が同時に変更されるとは限らないシナリオで優れた圧縮を提供します。

インメモリ OLTP でテンポラル テーブルを使用すると、データ セット全体をメモリ内に保持する必要が減り、ホット データとコールド データを簡単に区別できるようになります。

このカテゴリに適合する実際のシナリオの例は、特に在庫管理や為替取引です。

次の図では、在庫管理に使用される単純なデータ モデルを示します。

![インメモリでのテンポラルの使用](../../relational-databases/tables/media/temporalusageinmemory.png "インメモリでのテンポラルの使用")

次のコード例では、ProductInventory は、(既定で作成される行ストア インデックスを実際に置き換える) クラスター化列ストア インデックスが履歴テーブルにある、システム バージョン管理されたテンポラル テーブルがメモリ内に作成されます。

> [!NOTE]
> データベースでメモリ最適化テーブルの作成が許可されていることを確認します。 「 [メモリ最適化テーブルおよびネイティブ コンパイル ストアド プロシージャの作成](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)」を参照してください。

```sql
USE TemporalProductInventory
GO

BEGIN
    --If table is system-versioned, SYSTEM_VERSIONING must be set to OFF first
    IF ((SELECT temporal_type FROM SYS.TABLES WHERE object_id = OBJECT_ID('dbo.ProductInventory', 'U')) = 2)
    BEGIN
        ALTER TABLE [dbo].[ProductInventory] SET (SYSTEM_VERSIONING = OFF)
    END
    DROP TABLE IF EXISTS [dbo].[ProductInventory]
       DROP TABLE IF EXISTS [dbo].[ProductInventoryHistory]
END
GO

CREATE TABLE [dbo].[ProductInventory]
(
    ProductId int NOT NULL,
    LocationID INT NOT NULL,
    Quantity int NOT NULL CHECK (Quantity >=0),
  
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START NOT NULL ,
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END NOT NULL ,
    PERIOD FOR SYSTEM_TIME(SysStartTime,SysEndTime),

    --Primary key definition
    CONSTRAINT PK_ProductInventory PRIMARY KEY NONCLUSTERED (ProductId, LocationId)
)
WITH
(
    MEMORY_OPTIMIZED=ON,
    SYSTEM_VERSIONING = ON
    (
        HISTORY_TABLE = [dbo].[ProductInventoryHistory],
        DATA_CONSISTENCY_CHECK = ON
    )
)

CREATE CLUSTERED COLUMNSTORE INDEX IX_ProductInventoryHistory ON [ProductInventoryHistory]
WITH (DROP_EXISTING = ON);
```

前述のモデルでは、在庫を管理する手順は次のようになります。

```sql
CREATE PROCEDURE [dbo].[spUpdateInventory]
@productId int,
@locationId int,
@quantityIncrement int

WITH NATIVE_COMPILATION, SCHEMABINDING
AS
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL=SNAPSHOT, LANGUAGE=N'English')
    UPDATE dbo.ProductInventory
        SET Quantity = Quantity + @quantityIncrement
            WHERE ProductId = @productId AND LocationId = @locationId

/*If zero rows were updated than this is insert of the new product for a given location*/
    IF @@rowcount = 0
        BEGIN
            IF @quantityIncrement < 0
                SET @quantityIncrement = 0
            INSERT INTO [dbo].[ProductInventory]
                (
                    [ProductId]
                    ,[LocationID]
                    ,[Quantity]
                )
                VALUES
                   (
                        @productId
                       ,@locationId
                       ,@quantityIncrement
        END
END;
```

spUpdateInventory ストアド プロシージャによって、在庫に新しい製品が挿入されるか、特定の場所の製品の数量が更新されます。 このビジネス ロジックは、テーブルの更新によって Quantity フィールドを増減させ、常に最新の状態を正しく維持することに焦点を当てており、非常に単純です。それに対し、システム バージョン管理されたテーブルでは、次の図のとおり、履歴ディメンションをデータに追加します。

![インメモリでのテンポラルの使用 2b](../../relational-databases/tables/media/temporalusageinmemory2b.png "インメモリでのテンポラルの使用 2b")

これで、ネイティブにコンパイルされているモジュールから最新の状態を効率的にクエリできます。

```sql
CREATE PROCEDURE [dbo].[spQueryInventoryLatestState]
WITH NATIVE_COMPILATION, SCHEMABINDING
AS
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL=SNAPSHOT, LANGUAGE=N'English')
    SELECT ProductId, LocationID, Quantity, SysStartTime
        FROM dbo.ProductInventory
    ORDER BY ProductId, LocationId
END;
GO
EXEC [dbo].[spQueryInventoryLatestState];
```

次の例に示すとおり、FOR SYSTEM_TIME ALL 句を使用すると、長期のデータの変更を非常に簡単に分析できます。

```sql
DROP VIEW IF EXISTS vw_GetProductInventoryHistory;
GO
CREATE VIEW vw_GetProductInventoryHistory
AS
    SELECT ProductId, LocationId, Quantity, SysStartTime, SysEndTime
    FROM [dbo].[ProductInventory]
        FOR SYSTEM_TIME ALL;
GO
SELECT * FROM vw_GetProductInventoryHistory
    WHERE ProductId = 2;
```

次の図には、Power Query、Power BI または類似のビジネス インテリジェンス ツールに前述のビューをインポートすることにより、簡単にレンダリングできる 1 つの製品のデータ履歴を示しています。

![製品履歴の推移](../../relational-databases/tables/media/producthistoryovertime.png "製品履歴の推移")

このシナリオでテンポラル テーブルを使用すると、過去の任意の時点の在庫の状態の再構築や、別の時点のスナップショットとの比較など、その他の種類のタイム トラベル分析を行えます。

この使用シナリオ用に、Product テーブルと Location テーブルをテンポラル テーブルに拡張して、UnitPrice と NumberOfEmployee の変更履歴を後で分析することもできます。

```sql
ALTER TABLE Product
ADD
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN
        constraint DF_ValidFrom DEFAULT DATEADD(second, -1, SYSUTCDATETIME())
    , SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'
    , PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime);

ALTER TABLE Product
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.ProductHistory));

ALTER TABLE [Location]
ADD
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN
        constraint DFValidFrom DEFAULT DATEADD(second, -1, SYSUTCDATETIME())
    , SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN
        constraint DFValidTo DEFAULT '9999.12.31 23:59:59.99'
    , PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime);

ALTER TABLE [Location]
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.LocationHistory));
```

これでデータ モデルは複数のテンポラル テーブルを使用するようになったので、AS OF 分析のベスト プラクティスとしては、関連テーブルから必要なデータを抽出するビューを作成し、そのビューに FOR SYSTEM_TIME AS OF を適用します。こうすることで、データ モデル全体の状態の再構築が非常に簡単になります。

```sql
DROP VIEW IF EXISTS vw_ProductInventoryDetails;
GO

CREATE VIEW vw_ProductInventoryDetails
AS
    SELECT PrInv.ProductId ,PrInv.LocationId, P.ProductName, L.LocationName, PrInv.Quantity
    , P.UnitPrice, L.NumberOfEmployees
    , P.SysStartTime AS ProductStartTime, P.SysEndTime AS ProductEndTime
    , L.SysStartTime AS LocationStartTime, L.SysEndTime AS LocationEndTime
    , PrInv.SysStartTime AS InventoryStartTime, PrInv.SysEndTime AS InventoryEndTime
FROM dbo.ProductInventory as PrInv
JOIN dbo.Product AS P ON PrInv.ProductId = P.ProductID
JOIN dbo.Location AS L ON PrInv.LocationId = L.LocationID;
GO
SELECT * FROM vw_ProductInventoryDetails
    FOR SYSTEM_TIME AS OF '2015.01.01';
```

次の図は、SELECT クエリ用に生成された実行計画です。 これは、テンポラルな関係を処理するすべての複雑さは、完全に SQL Server エンジンに処理されることを示しています。

![AS OF の実行プラン](../../relational-databases/tables/media/asofexecutionplan.png "AS OF の実行プラン")

次のコードを使用すると、ある 2 つの時点 (前日と 1 か月前) の製品の在庫の状態を比較できます。

```sql
DECLARE @dayAgo datetime2 = DATEADD (day, -1, SYSUTCDATETIME());
DECLARE @monthAgo datetime2 = DATEADD (month, -1, SYSUTCDATETIME());

SELECT
    inventoryDayAgo.ProductId
    , inventoryDayAgo.ProductName
    , inventoryDayAgo.LocationName
    , inventoryDayAgo.Quantity AS QuantityDayAgo,inventoryMonthAgo.Quantity AS QuantityMonthAgo
    , inventoryDayAgo.UnitPrice AS UnitPriceDayAgo, inventoryMonthAgo.UnitPrice AS UnitPriceMonthAgo
FROM vw_ProductInventoryDetails
FOR SYSTEM_TIME AS OF @dayAgo AS inventoryDayAgo
JOIN vw_ProductInventoryDetails FOR SYSTEM_TIME AS OF @monthAgo AS inventoryMonthAgo
    ON inventoryDayAgo.ProductId = inventoryMonthAgo.ProductId AND inventoryDayAgo.LocationId = inventoryMonthAgo.LocationID;
```

## <a name="anomaly-detection"></a>異常検出

異常検出 (または外れ値検知) では、予想されているパターンと一致しないアイテムまたはデータセット内の他のアイテムと一致しないアイテムを識別できます。 システム バージョン管理されたテンポラル テーブルを使用すると、一時的なクエリを使用して、特定のパターンをすばやく検索できるので、定期的にまたは不規則に発生する異常を検出できます。 何が異常であるかは、収集するデータの種類およびビジネス ロジックによって異なります。

次の例は、販売数の "急増" を検出する単純化されたロジックです。 購入品の履歴を収集するテンポラル テーブルで作業しているとします。

```sql
CREATE TABLE [dbo].[Product]
                (
            [ProdID] [int] NOT NULL PRIMARY KEY CLUSTERED
        , [ProductName] [varchar](100) NOT NULL
        , [DailySales] INT NOT NULL
        , [ValidFrom] [datetime2] GENERATED ALWAYS AS ROW START NOT NULL
        , [ValidTo] [datetime2] GENERATED ALWAYS AS ROW END NOT NULL
        , PERIOD FOR SYSTEM_TIME ([ValidFrom], [ValidTo])
    )
    WITH( SYSTEM_VERSIONING = ON (HISTORY_TABLE = [dbo].[ProductHistory]
        , DATA_CONSISTENCY_CHECK = ON ))
```

次の図は購入を時間順に示しています。

![テンポラルの異常検出](../../relational-databases/tables/media/temporalanomalydetection.png "テンポラルの異常検出")

通常の日は購入品数にはあまり変動がないことを前提に、次のクエリでは単一の外れ値が識別されます。つまり、周りのサンプルは大きくは変わらない中 (20% 未満)、すぐ隣のものと比較して大きく異なる (2 倍) サンプルが識別されます。

```sql
WITH CTE (ProdId, PrevValue, CurrentValue, NextValue, ValidFrom, ValidTo)
AS
    (
        SELECT
            ProdId, LAG (DailySales, 1, 1) over (partition by ProdId order by ValidFrom) as PrevValue
            , DailySales, LEAD (DailySales, 1, 1) over (partition by ProdId order by ValidFrom) as NextValue
             , ValidFrom, ValidTo from Product
        FOR SYSTEM_TIME ALL
)

SELECT
    ProdId
    , PrevValue
    , CurrentValue
    , NextValue
    , ValidFrom
    , ValidTo
    , ABS (PrevValue - NextValue) / convert (float, (CASE WHEN NextValue > PrevValue THEN PrevValue ELSE NextValue END)) as PrevToNextDiff
    , ABS (CurrentValue - PrevValue) / convert (float, (CASE WHEN CurrentValue > PrevValue THEN PrevValue ELSE CurrentValue END)) as CurrentToPrevDiff
    , ABS (CurrentValue - NextValue) / convert (float, (CASE WHEN CurrentValue > NextValue THEN NextValue ELSE CurrentValue END)) as CurrentToNextDiff
FROM CTE
    WHERE
        ABS (PrevValue - NextValue) / (CASE WHEN NextValue > PrevValue THEN PrevValue ELSE NextValue END) < 0.2
            AND ABS (CurrentValue - PrevValue) / (CASE WHEN CurrentValue > PrevValue THEN PrevValue ELSE CurrentValue END) > 2
            AND ABS (CurrentValue - NextValue) / (CASE WHEN CurrentValue > NextValue THEN NextValue ELSE CurrentValue END) > 2;
```

> [!NOTE]
> この例は意図的に単純化しています。 実稼働のシナリオでは、共通のパターンを示さないサンプルの識別には高度な統計的手法が使用されるでしょう。

## <a name="slowly-changing-dimensions"></a>緩やかに変化するディメンション

通常、データ ウェアハウスのディメンションには、エンティティに関する地理的な場所、顧客、または製品など、比較的静的なデータが含まれます。 ただし、一部のシナリオでは、ディメンション テーブル内のデータも追跡する必要があります。 ディメンションに対する変更は予測できない方法でまれにしか実行されず、ファクト テーブルに適用される定期的な更新スケジュール外のものであるため、この種のディメンション テーブルは、緩やかに変化するディメンション (SCD) と呼ばれています。

変更履歴がどのように保存されるかによって、緩やかに変化するディメンションには、いくつかのカテゴリがあります。

- タイプ 0: 履歴を保持しません。 ディメンション属性は元の値です。
- 型 1:ディメンション属性には最新の値が反映されます (前の値は上書きされます)。
- 型 2:ディメンション メンバーのすべてのバージョンは、通常は有効期間を示す列と共にテーブルに別の行に示されます。
- 型 3:同じ行に追加された列を使用して、選択された属性の限られた履歴を保持します。
- タイプ 4: 元のディメンション テーブルには最新 (現在) のディメンション メンバーのバージョンを保持しながら、別のテーブルに履歴を保持します。

SCD 戦略を選択した場合、ディメンション テーブルは ETL (Extract-Transform-Load) 層によって正確に維持されますが、これでは通常コードをたくさん記述する必要があり、メンテナンスも複雑です。

SQL Server 2016 のシステム バージョン管理されたテンポラル テーブルを使用すると、データ履歴は自動的に保存されるので、コードを劇的に単純化できます。 2 つのテーブルを使用して実装される SQL Server 2016 のテンポラル テーブルは、タイプ 4 の SCD に最も近いです。 ただし、一時的なクエリでは現在のテーブルしか参照できないので、タイプ 2 の SCD の使用を計画している環境でもテンポラル テーブルを検討できます。

標準のディメンションを SCD に変換するには、単に新しいものを作成するか、既存のものをシステム バージョン管理されたテンポラル テーブルになるように変更します。 既存のディメンション テーブルに履歴データが含まれる場合、別のテーブルを作成して、そこに履歴データを移動し、現在 (実際) のディメンション バージョンを元のディメンション テーブルに保存します。 次いで ALTER TABLE 構文を使用し、ディメンション テーブルを事前定義された履歴テーブルを持つシステム バージョン管理されたテンポラル テーブルに変換します。

次の図に処理を示します。ここで、DimLocation ディメンション テーブルには ETL 処理によって入力される null 値を許可しない datetime2 の列として ValidFrom および ValidTo を既に持っていることを前提にしています。

```sql
/*Move "closed" row versions into newly created history table*/
SELECT * INTO DimLocationHistory
    FROM DimLocation
        WHERE ValidTo < '9999-12-31 23:59:59.99';
GO
/*Create clustered columnstore index which is a very good choice in DW scenarios*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_DimLocationHistory ON DimLocationHistory
/*Delete previous versions from DimLocation which will become current table in temporal-system-versioning configuration*/
DELETE FROM DimLocation
    WHERE ValidTo < '9999-12-31 23:59:59.99';
/*Add period definition*/
ALTER TABLE DimLocation ADD PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo);
/*Enable system-versioning and bind history table to the DimLocation*/
ALTER TABLE DimLocation SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DimLocationHistory));
```

一度 SCD を作成したら、データ ウェアハウスの読み込み処理中は、それを維持するための追加のコードは必要ありません。

次の図は、2 つの SCD (DimLocation および DimProduct) と 1 つのファクト テーブルを使用する単純なシナリオでテンポラル テーブルを使用する方法を示します。

![テンポラルの SCD](../../relational-databases/tables/media/temporalscd.png "テンポラルの SCD")

レポートで上述の SCD を使用するには、クエリを効率的に調整する必要があります。 たとえば、過去 6 か月間の売上額合計と 1 人当たりが販売した製品の平均数を計算したいとします。 両方のメトリックでは、ファクト テーブルとディメンションのデータに相関関係がある必要があることに注意してください (DimLocation.NumOfCustomers、DimProduct.UnitPrice)。分析に重要なその属性に変更がある可能性があります。 次のクエリによって、必要なメトリックが正しく計算されます。

```sql
DECLARE @now datetime2 = SYSUTCDATETIME()
DECLARE @sixMonthsAgo datetime2 SET
    @sixMonthsAgo = DATEADD (month, -12, SYSUTCDATETIME())

SELECT DimProduct_History.ProductId
   , DimLocation_History.LocationId
    , SUM(F.Quantity * DimProduct_History.UnitPrice) AS TotalAmount
    , AVG (F.Quantity/DimLocation_History.NumOfCustomers) AS AverageProductsPerCapita
FROM FactProductSales F
/* find corresponding record in SCD history in last 6 months, based on matching fact */
JOIN DimLocation FOR SYSTEM_TIME BETWEEN @sixMonthsAgo AND @now AS DimLocation_History
    ON DimLocation_History.LocationId = F.LocationId
        AND F.FactDate BETWEEN DimLocation_History.ValidFrom AND DimLocation_History.ValidTo
/* find corresponding record in SCD history in last 6 months, based on matching fact */
JOIN DimProduct FOR SYSTEM_TIME BETWEEN @sixMonthsAgo AND @now AS DimProduct_History
    ON DimProduct_History.ProductId = F.ProductId
        AND F.FactDate BETWEEN DimProduct_History.ValidFrom AND DimProduct_History.ValidTo
    WHERE F.FactDate BETWEEN @sixMonthsAgo AND @now
GROUP BY DimProduct_History.ProductId, DimLocation_History.LocationId ;
```

**考慮事項:**

- データベースのトランザクション時間に基づいて計算される有効期間がビジネス ロジックで問題ない場合は、SCD にシステム バージョン管理されたテンポラル テーブルを使用できます。 データが大幅に遅れて読み込まれる場合、トランザクション時間が許可されないものとなってしまう場合があります。
- 既定では、システム バージョン管理されたテンポラル テーブルでは、読み込み後の履歴データは変更できません (SYSTEM_VERSIONING を OFF に設定した後には履歴を変更できます)。 履歴データの変更が定期的に行われる場合、これは制限になる場合があります。
- システム バージョン管理されたテンポラル テーブルでは、すべての列の変更で行バージョンが生成されます。 特定の行の変更で新しいバージョンが作成されるのを抑制したい場合、その制限を ETL ロジックに組み込む必要があります。
- SCD テーブルの履歴行が多くなることが予想される場合、履歴テーブルのメインのストレージ オプションとしてクラスター化列ストア インデックスを使用することを検討してください。 これにより、履歴テーブルのフットプリントが減り、分析クエリを高速化できます。

## <a name="repairing-row-level-data-corruption"></a>データの行レベルでの破損の修復

システム バージョン管理されたテンポラル テーブルの履歴データを使用すると、個々の行を以前にキャプチャした任意の状態に迅速に修復できます。 テンポラル テーブルのこのプロパティは、影響を受けた行を探すことができた場合や、不要なデータ変更が行われた時間がわかっている場合、バックアップを使用する必要がなく修復を非常に効率よく実行できるため、非常に便利です。

このアプローチにはいくつかの利点があります。

- 修復のスコープを非常に正確に制御できます。 影響を受けていないレコードは最新の状態に維持される必要があり、これはしばしば非常に重要な要件になります。
- 非常に効率的に操作でき、そのデータを使用するすべてのワークロードのためにデータベースをオンライン状態に維持できます。
- 修復操作自体が、バージョン管理されます。 修復操作自体の監査記録があるので、必要に応じて後で何が発生したか分析できます。

修復アクションは、比較的簡単に自動化できます。 次に、データの監査シナリオで使用される Employee テーブルのデータの修復を実行するストアド プロシージャのコード例を示します。

```sql
DROP PROCEDURE IF EXISTS sp_RepairEmployeeRecord;
GO

CREATE PROCEDURE sp_RepairEmployeeRecord
    @EmployeeID INT,
    @versionNumber INT = 1
AS

;WITH History
AS
(
        /* Order historical rows by tehir age in DESC order*/
        SELECT ROW_NUMBER () OVER (PARTITION BY EmployeeID ORDER BY [ValidTo] DESC) AS RN, *
        FROM Employee FOR SYSTEM_TIME ALL WHERE YEAR (ValidTo) < 9999 AND Employee.EmployeeID = @EmployeeID
)

/*Update current row by using N-th row version from history (default is 1 - i.e. last version)*/
UPDATE Employee
    SET [Position] = H.[Position], [Department] = H.Department, [Address] = H.[Address], AnnualSalary = H.AnnualSalary
    FROM Employee E JOIN History H ON E.EmployeeID = H.EmployeeID AND RN = @versionNumber
    WHERE E.EmployeeID = @EmployeeID
```

このストアド プロシージャでは、@EmployeeID と @versionNumber を入力パラメーターとして受け取ります。 この手順は、既定では、行の状態を履歴から最新のバージョンに復元します (@versionNumber = 1)。

次の図は、プロシージャの呼び出しの前後に行の状態を示しています。 長方形で赤くマークされているのは、不正な行バージョンで、長方形で緑にマークされているのは履歴の正しいバージョンです。

![テンポラル使用の修復 1](../../relational-databases/tables/media/temporalusagerepair1.png "テンポラル使用の修復 1")

```sql
EXEC sp_RepairEmployeeRecord @EmployeeID = 1, @versionNumber = 1
```

![テンポラル使用の修復 2](../../relational-databases/tables/media/temporalusagerepair2.png "テンポラル使用の修復 2")

この修復のストアド プロシージャは、行のバージョンではなく、正確なタイムスタンプを受け入れるように定義できます。 これでは、提供された時点でアクティブであった任意のバージョンに行を復元します (つまり、AS OF の時点)。

```sql
DROP PROCEDURE IF EXISTS sp_RepairEmployeeRecordAsOf;
GO

CREATE PROCEDURE sp_RepairEmployeeRecordAsOf
    @EmployeeID INT,
    @asOf datetime2
AS

/*Update current row to the state that was actual AS OF provided date*/
UPDATE Employee
    SET [Position] = History.[Position], [Department] = History.Department, [Address] = History.[Address], AnnualSalary = History.AnnualSalary
    FROM Employee AS E JOIN Employee FOR SYSTEM_TIME AS OF @asOf AS History ON E.EmployeeID = History.EmployeeID
    WHERE E.EmployeeID = @EmployeeID
```

次の図では、同じデータ サンプルを時間条件で復元するシナリオを示しています。 @asOf パラメーター、提供された時点で履歴で実際に選択されていた行、修復操作後の現在のテーブルの新しい行バージョンが強調表示されています。

![テンポラル使用の修復 3](../../relational-databases/tables/media/temporalusagerepair3.png "テンポラル使用の修復 3")

データ修正は、データ ウェアハウスおよびレポート システムで自動的にデータを読み込む際の一部にできます。 新しく更新された値がそのとき不正な場合、多くのシナリオでは、履歴から以前のバージョンを復元することで十分に対応できます。 次の図では、これを自動化する手順を示します。

![テンポラル使用の修復 4](../../relational-databases/tables/media/temporalusagerepair4.png "テンポラル使用の修復 4")

## <a name="next-steps"></a>次のステップ

- [テンポラル テーブル](../../relational-databases/tables/temporal-tables.md)
 [システム バージョン管理されたテンポラル テーブルの概要](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [テンポラル テーブルのシステム一貫性のチェック](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [テンポラル テーブルでのパーティション分割](../../relational-databases/tables/partitioning-with-temporal-tables.md)
- [テンポラル テーブルの考慮事項と制約](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [テンポラル テーブル セキュリティ](../../relational-databases/tables/temporal-table-security.md)
- [メモリ最適化テーブルでのシステム バージョン管理されたテンポラル テーブル](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [テンポラル テーブル メタデータのビューおよび関数](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
