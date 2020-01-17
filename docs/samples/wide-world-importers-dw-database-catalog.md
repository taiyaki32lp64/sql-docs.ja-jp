---
title: WideWorldImporters OLAP データベース カタログ - SQL |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 7c3da2af72743cc8f89273bfce24fe74fc7e4dc1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104294"
---
# <a name="wideworldimportersdw-database-catalog"></a>WideWorldImportersDW データベース カタログ
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
スキーマ、テーブル、および WideWorldImportersDW データベース内のストアド プロシージャの説明。 

WideWorldImportersDW データベースは、データ ウェアハウスと分析処理に使用されます。 売り上げ高と購入に関するトランザクション データは、WideWorldImporters データベースで生成され、WideWorldImportersDW を使って、データベースに読み込まれる、**毎日の ETL 処理**します。

WideWorldImportersDW 内のデータしたがって WideWorldImporters、内のデータをミラーリングしますが、テーブルは異なる方法で構成されています。 WideWorldImportersDW WideWorldImporters は従来の正規化されたスキーマが、使用して、[スター スキーマ](https://wikipedia.org/wiki/Star_schema)のテーブル設計のアプローチです。 データベースにはだけでなく、ファクト テーブルとディメンション テーブルは、ETL プロセスで使用されるステージング テーブルの数値が含まれています。

## <a name="schemas"></a>スキーマ

テーブルのさまざまな種類は、3 つのスキーマで編成されます。

|スキーマ|説明|
|-----------------------------|---------------------|
|[ディメンション]|ディメンション テーブル。|
|Fact|ファクト テーブルです。|  
|統合|ステージング テーブルと ETL に必要なその他のオブジェクト。|  

## <a name="tables"></a>テーブル

ディメンションとファクト テーブルは、以下に示します。 統合スキーマ内のテーブルは、ETL プロセスに対してのみ使用されは表示されません。

### <a name="dimension-tables"></a>ディメンション テーブル

WideWorldImportersDW には、次のディメンション テーブルがあります。 説明には、WideWorldImporters データベース内のソース テーブルとの関係が含まれています。

|テーブル|コピー元のテーブル|
|-----------------------------|---------------------|
|City|`Application.Cities`, `Application.StateProvinces`, `Application.Countries`.|
|Customer|`Sales.Customers`, `Sales.BuyingGroups`, `Sales.CustomerCategories`.|
|date|日付、会計年度などに関する情報を含む新しいテーブル (11 月 1 日に基づく会計年度の開始)。|
|Employee|`Application.People`。|
|StockItem|`Warehouse.StockItems`, `Warehouse.Colors`, `Warehouse.PackageType`.|
|業者|`Purchasing.Suppliers`, `Purchasing.SupplierCategories`.|
|PaymentMethod|`Application.PaymentMethods`。|
|TransactionType|`Application.TransactionTypes`。|

### <a name="fact-tables"></a>ファクト テーブル

WideWorldImportersDW が次のファクト テーブルです。 説明には、analytics/レポートのクエリで各ファクト テーブルが使用される通常のクラスと同様に、WideWorldImporters データベースでのソース テーブルとの関係が含まれています。

|テーブル|コピー元のテーブル|分析のサンプル|
|-----------------------------|---------------------|---------------------|
|[オーダー]|`Sales.Orders` および `Sales.OrderLines`|売上は、人、ピッカー/packer の生産性とでは、注文を選択する時間です。 さらに、注文をバックアップする先頭の在庫切れの状況が低い。|
|販売|`Sales.Invoices` および `Sales.InvoiceLines`|日付の売上、出荷日、時間の経過と共に収益性、販売員による収益性。|
|購入|`Purchasing.PurchaseOrderLines`|Vs の予想される実際のリード タイム|
|トランザクション|`Sales.CustomerTransactions` および `Purchasing.SupplierTransactions`|発行日付 vs 最終処理日、および量を測定します。|
|移動|`Warehouse.StockTransactions`|時間の経過と共に移動します。|
|株式を売ります|`Warehouse.StockItemHoldings`|手持ちの在庫レベルと値。|

## <a name="stored-procedures"></a>ストアド プロシージャ

ストアド プロシージャは、主に、ETL プロセスと構成のために使用されます。

サンプルのすべての拡張機能を使用することが推奨されます、 `Reports` Reporting Services レポートでは、スキーマ、 `PowerBI` Power BI へのアクセス用のスキーマ。

### <a name="application-schema"></a>アプリケーションのスキーマ

これらの手順は、サンプルの構成に使用されます。 PolyBase, を追加のサンプルでは、standard edition のバージョンに enterprise edition の機能を適用し、ETL の再シードを実行に使用されます。

|手順|目的|
|-----------------------------|---------------------|
|Configuration_ApplyPartitionedColumnstoreIndexing|ファクト テーブルのパーティション分割と列ストア インデックスに適用されます。|
|Configuration_ConfigureForEnterpriseEdition|パーティション分割、インデックス作成とインメモリ列ストアに適用されます。|
|Configuration_EnableInMemory|SCHEMA_ONLY メモリ最適化テーブルは、ETL のパフォーマンスを向上させるには、統合ステージング テーブルを置き換えます。|
|Configuration_ApplyPolyBase|外部データ ソース、ファイル形式、およびテーブルを構成します。|
|Configuration_PopulateLargeSaleTable|Enterprise edition の変更を適用し、追加の履歴と 2012年のカレンダー年度の大量のデータを設定します。|
|Configuration_ReseedETL|既存のデータを削除し、ETL のシードを再起動します。 これにより、OLAP データベースを再作成、OLTP データベースの更新された行と一致します。|

### <a name="integration-schema"></a>統合スキーマ

ETL プロセスで使用されるプロシージャは、これらのカテゴリに分類されます。
- ETL パッケージのすべての Get * プロシージャのヘルパー プロシージャ。
- 移行するために、ETL パッケージによって使用されるプロシージャは、DW のテーブルのすべての移行 * プロシージャにデータをステージングします。
- `PopulateDateDimensionForYear` -1 年間し、で、その年のすべての日付が設定されているように、`Dimension.Date`テーブル。

### <a name="sequences-schema"></a>シーケンス スキーマ

データベースで、シーケンスを構成する手順。

|手順|目的|
|-----------------------------|---------------------|
|ReseedAllSequences|プロシージャを呼び出す`ReseedSequenceBeyondTableValue`のすべてのシーケンス。|
|ReseedSequenceBeyondTableValue|同じシーケンスを使用する任意のテーブルで、値を上回る次のシーケンス値の位置を変更するために使用します。 (など、`DBCC CHECKIDENT`のシーケンスが、可能性のある複数のテーブルの identity 列と同じです)。|
