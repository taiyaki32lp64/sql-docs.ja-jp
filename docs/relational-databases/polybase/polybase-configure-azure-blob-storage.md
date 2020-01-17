---
title: 外部データへのアクセス:Azure Blob Storage - PolyBase
ms.date: 12/13/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.custom: seo-dt-2019, seo-lt-2019
ms.openlocfilehash: 680a8e28e807505f4824524a686f244621cb3dd0
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258693"
---
# <a name="configure-polybase-to-access-external-data-in-azure-blob-storage"></a>Azure Blob Storage 上の外部データにアクセスするように PolyBase を構成する

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

この記事では、SQL Server インスタンスで PolyBase を使用し、Azure Blob Storage 上の外部データに対してクエリを実行する方法について説明します。

## <a name="prerequisites"></a>前提条件

PolyBase をインストールしていない場合は、「[PolyBase のインストール](polybase-installation.md)」をご覧ください。 インストールに関する記事では、前提条件について説明します。

### <a name="configure-azure-blob-storage-connectivity"></a>Azure Blob Storage の接続を構成する

最初に、Azure Blob Storage を使用するように SQL Server PolyBase を構成します。

1. 'hadoop connectivity' を Azure Blob Storage プロバイダーに設定して [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) を実行します。 プロバイダーの値を見つけるには、[PolyBase 接続構成 ](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)に関する記事を参照してください。 既定で、Hadoop 接続は 7 に設定されています。

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. **services.msc** を使用して SQL Server を再起動する必要があります。 SQL Server を再起動すると、次のサービスが再起動します。  

   - SQL Server PolyBase Data Movement Service  
   - SQL Server PolyBase エンジン  
  
   ![services.msc で PolyBase サービスを停止および開始する](../../relational-databases/polybase/media/polybase-stop-start.png "|::ref1::|")  
  
## <a name="configure-an-external-table"></a>外部テーブルを構成する

Hadoop データ ソース内のデータのクエリを実行するには、Transact-SQL クエリで使用する外部テーブルを定義する必要があります。 次の手順では、外部テーブルを構成する方法を説明します。

1. データベースにマスター キーを作成します。 これは、資格情報のシークレットの暗号化に必須です。

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
   ```

1. Azure Blob Storage 用のデータベース スコープ資格情報を作成します。

   ```sql
   -- IDENTITY: any string (this is not used for authentication to Azure storage).  
   -- SECRET: your Azure storage account key.  
   CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
   WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';
   ```

1. [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) を使用して外部データ ソースを作成します。

   ```sql
   -- LOCATION:  Azure account storage account name and blob container name.  
   -- CREDENTIAL: The database scoped credential created above.  
   CREATE EXTERNAL DATA SOURCE AzureStorage with (  
         TYPE = HADOOP,
         LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
         CREDENTIAL = AzureStorageCredential  
   );  
   ```

1. [CREATE EXTERNAL FILE FORMAT](../../t-sql/statements/create-external-file-format-transact-sql.md) を使用して外部ファイル形式を作成します。

   ```sql
   -- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE))  
   ```

1. [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md)を使用して、Azure ストレージに格納されているデータをポイントする外部テーブルを作成します。 この例では、外部データには車両センサー データが含まれています。

   ```sql
   -- LOCATION: path to file or directory that contains the data (relative to HDFS root).  
   CREATE EXTERNAL TABLE [dbo].[CarSensor_Data] (  
         [SensorKey] int NOT NULL,
         [CustomerKey] int NOT NULL,
         [GeographyKey] int NULL,
         [Speed] float NOT NULL,
         [YearMeasured] int NOT NULL  
   )  
   WITH (LOCATION='/Demo/',
         DATA_SOURCE = AzureStorage,  
         FILE_FORMAT = TextFileFormat  
   );  
   ```

1. 外部テーブルの統計を作成します。

   ```sql
   CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
   ```

## <a name="polybase-queries"></a>PolyBase クエリ

PolyBase が適している機能には、次の 3 つがあります。  
  
- 外部テーブルに対するアドホック クエリ。  
- データのインポート。  
- データのエクスポート。  

次のクエリでは、架空の車両センサー データの例を示します。

### <a name="ad-hoc-queries"></a>アドホック クエリ  

次のアドホック クエリでは、Hadoop データを結合します。 時速 35 マイルを越えて走行している顧客を選択し、SQL Server に格納されている構造化された顧客データと Hadoop に格納されている車両センサー データを結合します。  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
OPTION (FORCE EXTERNALPUSHDOWN);   -- or OPTION (DISABLE EXTERNALPUSHDOWN)  
```  

### <a name="importing-data"></a>データのインポート  

次のクエリでは、外部データを SQL Server にインポートします。 この例では、高速走行しているドライバーのデータを、さらに詳細な分析を実行するために SQL Server にインポートします。 パフォーマンスを向上させるために、列ストア テクノロジが活用されています。  

```sql
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

### <a name="exporting-data"></a>データのエクスポート  

次のクエリは、SQL Server から Azure Blob Storage にデータをエクスポートします。 これを行うには、先に PolyBase のエクスポートを有効にする必要があります。 データをエクスポートする前に、エクスポート先の外部テーブルを作成します。

```sql
-- Enable INSERT into external table  
sp_configure 'allow polybase export', 1;  
reconfigure  
  
-- Create an external table.
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
INSERT INTO dbo.FastCustomer2009  
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```  

## <a name="view-polybase-objects-in-ssms"></a>SSMS での PolyBase オブジェクトの表示  

SSMS では、外部テーブルが別のフォルダー **[外部テーブル]** に表示されます。 外部データ ソースおよび外部ファイル形式は、 **[外部リソース]** の下のサブフォルダーにあります。  
  
![SSMS での PolyBase オブジェクト](media/polybase-management.png)  

## <a name="next-steps"></a>次のステップ

次の記事を参照して、PolyBase を使用して監視するための方法をさらに調べます。

[PolyBase スケールアウト グループ](../../relational-databases/polybase/polybase-scale-out-groups.md)。  
[PolyBase のトラブルシューティング](polybase-troubleshooting.md)。  
