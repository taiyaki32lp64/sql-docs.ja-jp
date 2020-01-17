---
title: PolyBase クエリのシナリオ | Microsoft Docs
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
keywords:
- PolyBase
helpviewer_keywords:
- PolyBase, import and export
- Hadoop, import with PolyBase
- Hadoop, export with PolyBase
- Azure blob storage, import with PolyBase
- Azure blob storage, export with PolyBase
ms.assetid: 2c5aa2bd-af7d-4f57-9a28-9673c2a4c07e
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: a8912a290723e3f0e1d0a0b951a6a5d1ce04b725
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710513"
---
# <a name="polybase-query-scenarios"></a>PolyBase クエリのシナリオ

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

この記事では、SQL Server (2016 以降) の [PolyBase](../../relational-databases/polybase/polybase-guide.md) 機能を使用するクエリの例を示します。 これらの例を使用する前に、先に PolyBase をインストールして構成しておく必要があります。 詳細については、[PolyBase の概要](polybase-guide.md)に関する記事を参照してください。
  
外部テーブルを照会するには、外部テーブルに対して Transact-SQL ステートメントを実行するか、または BI ツールを使用します。
  
## <a name="select-from-external-table"></a>外部テーブルからの SELECT  

定義済みの外部テーブルからデータを返す単純なクエリです。  

```sql  
SELECT TOP 10 * FROM [dbo].[SensorData];   
```

述語を含む単純なクエリです。

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65;
```

## <a name="join-external-tables-with-local-tables"></a>外部テーブルをローカル テーブルと結合する

```sql
SELECT InsuranceCustomers.FirstName,   
   InsuranceCustomers.LastName,   
   SensorData.Speed  
FROM InsuranceCustomers INNER JOIN SensorData    
ON InsuranceCustomers.CustomerKey = SensorData.CustomerKey   
WHERE SensorData.Speed > 65   
ORDER BY SensorData.Speed DESC  
  
```  

## <a name="import-data"></a>データのインポート

Hadoop または Azure ストレージからデータを永続的なストレージの SQL Server にインポートします。 SELECT INTO を使用して、SQL Server の永続記憶装置に、外部テーブルで参照されるデータをインポートします。 リレーショナル テーブルをその場で作成し、2 番目の手順でテーブル上に列ストア インデックスを作成します。

```sql
-- PolyBase scenario - import external data into SQL Server
-- Import data for fast drivers into SQL Server to do more in-depth analysis
-- Leverage columnstore technology
  
SELECT DISTINCT   
        Insured_Customers.FirstName, Insured_Customers.LastName,   
        Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
INTO Fast_Customers from Insured_Customers INNER JOIN   
(  
        SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
ORDER BY YearlyIncome  
  
CREATE CLUSTERED COLUMNSTORE INDEX CCI_FastCustomers ON Fast_Customers;  
```

## <a name="export-data"></a>データのエクスポート

Hadoop または Azure ストレージに SQL Server からのデータをエクスポートします。 

まず、'allow polybase export' の `sp_configure` 値を 1 に設定してエクスポート機能を有効にします。 次に、変換先ディレクトリを指す外部テーブルを作成します。 CREATE EXTERNAL TABLE ステートメントは、変換先ディレクトリが存在しない場合にそれを作成します。 次に、ローカルの SQL Server テーブルからのデータを外部データ ソースをエクスポートするのに INSERT INTO を使用します。 

SELECT ステートメントの結果セットは、指定したファイル形式で指定した場所にエクスポートされます。 外部ファイルの名前は *QueryID_date_time_ID.format*です ( *ID* は増分識別子、 *format* はエクスポートされるデータ形式)。 たとえば、あるファイルの名前は QID776_20160130_182739_0.orc となります。

> [!NOTE]
> データを PolyBase 経由で Hadoop または Azure Blob Storage にエクスポートする場合、データだけがエクスポートされ、CREATE EXTERNAL TABLE コマンドで定義した列名 (メタデータ) はエクスポートされません。

```sql  
-- PolyBase scenario  - export data from SQL Server to Hadoop
-- Create an external table
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] (  
        [FirstName] char(25) NOT NULL,   
        [LastName] char(25) NOT NULL,   
        [YearlyIncome] float NULL,   
        [MaritalStatus] char(1) NOT NULL  
)  
WITH (  
        LOCATION='/old_data/2009/customerdata',  
        DATA_SOURCE = HadoopHDP2,  
        FILE_FORMAT = TextFileFormat,  
        REJECT_TYPE = VALUE,  
        REJECT_VALUE = 0  
);  
  
-- Export data: Move old data to Hadoop while keeping it query-able via an external table.  
INSERT INTO dbo.FastCustomers2009  
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```

## <a name="new-catalog-views"></a>新しいカタログ ビュー

次の新しいカタログ ビューには、外部のリソースが表示されます。

```sql
SELECT * FROM sys.external_data_sources;   
SELECT * FROM sys.external_file_formats;  
SELECT * FROM sys.external_tables;  
```

 テーブルが外部テーブルかどうかを判断するには、次を使用します: `is_external`  

```sql  
SELECT name, type, is_external FROM sys.tables WHERE name='myTableName'   
```  

## <a name="next-steps"></a>次の手順  

トラブルシューティングの詳細については、「 [PolyBase のトラブルシューティング](../../relational-databases/polybase/polybase-troubleshooting.md)」を参照してください。
