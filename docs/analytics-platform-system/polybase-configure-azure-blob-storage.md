---
title: PolyBase を使用して Azure Blob ストレージ内の外部データにアクセスする
description: Parallel Data Warehouse で PolyBase を構成して外部 Hadoop に接続する方法について説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4ea61ea7e6983f9601783957eee6776f36eccfb4
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400727"
---
# <a name="configure-polybase-to-access-external-data-in-azure-blob-storage"></a>Azure Blob storage 内の外部データにアクセスするように PolyBase を構成する

この記事では、SQL Server インスタンスで PolyBase を使用して、Azure Blob ストレージ内の外部データに対してクエリを実行する方法について説明します。

> [!NOTE]
> 現在、APS は、standard 汎用 v1 ローカル冗長 (LRS) の Azure Blob storage のみをサポートしています。

## <a name="prerequisites"></a>前提条件

 - サブスクリプションの Azure Blob storage。
 - Azure Blob storage に作成されたコンテナー。

### <a name="configure-azure-blob-storage-connectivity"></a>Azure Blob storage の接続を構成する

まず、Azure Blob storage を使用するように APS を構成します。

1. ' Hadoop connectivity ' を Azure Blob storage プロバイダーに設定して[sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)を実行します。 プロバイダーの値を見つけるには、[PolyBase 接続構成 ](../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)に関する記事を参照してください。

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure Blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. [アプライアンス Configuration Manager](launch-the-configuration-manager.md)の [サービスの状態] ページを使用して、APS リージョンを再起動します。
  
## <a name="configure-an-external-table"></a>外部テーブルを構成する

Azure Blob ストレージのデータに対してクエリを実行するには、Transact-sql クエリで使用する外部テーブルを定義する必要があります。 次の手順では、外部テーブルを構成する方法を説明します。

1. データベースにマスター キーを作成します。 資格情報のシークレットを暗号化する必要があります。

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
   ```

1. Azure Blob storage のデータベーススコープ資格情報を作成します。

   ```sql
   -- IDENTITY: any string (this is not used for authentication to Azure storage).  
   -- SECRET: your Azure storage account key.  
   CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
   WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';
   ```

1. 
  [CREATE EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md) を使用して外部データ ソースを作成します。

   ```sql
   -- LOCATION:  Azure account storage account name and blob container name.  
   -- CREDENTIAL: The database scoped credential created above.  
   CREATE EXTERNAL DATA SOURCE AzureStorage with (  
         TYPE = HADOOP,
         LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
         CREDENTIAL = AzureStorageCredential  
   );  
   ```

1. 
  [CREATE EXTERNAL FILE FORMAT](../t-sql/statements/create-external-file-format-transact-sql.md) を使用して外部ファイル形式を作成します。

   ```sql
   -- FORMAT TYPE: Type of format in Azure Blob storage (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   -- In this example, the files are pipe (|) delimited
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE)  
   ```

1. 
  [CREATE EXTERNAL TABLE](../t-sql/statements/create-external-table-transact-sql.md)を使用して、Azure ストレージに格納されているデータをポイントする外部テーブルを作成します。 この例では、外部データには車両センサー データが含まれています。

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
  
- 外部テーブルに対するアドホッククエリ。  
- データのインポート。  
- データのエクスポート。  

次のクエリでは、架空の車両センサー データの例を示します。

### <a name="ad-hoc-queries"></a>アドホック クエリ  

次のアドホッククエリは、Azure Blob ストレージ内のデータとリレーショナルに結合します。 SQL Server に格納されている構造化顧客データを、Azure Blob storage に格納されている車両センサーデータと結合することで、35 mph よりも高速になる顧客を選択します。  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
```  

### <a name="importing-data"></a>データのインポート  

次のクエリでは、外部データを APS にインポートします。 この例では、高速ドライバーのデータを AP にインポートして、さらに詳細な分析を行います。 パフォーマンスを向上させるために、APS の列ストアテクノロジを活用しています。  

```sql
CREATE TABLE Fast_Customers
WITH
(CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH (CustomerKey))
AS
SELECT DISTINCT
      Insured_Customers.CustomerKey, Insured_Customers.FirstName, Insured_Customers.LastName,   
      Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
from Insured_Customers INNER JOIN   
(  
      SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
```  

### <a name="exporting-data"></a>データのエクスポート  

次のクエリでは、APS から Azure Blob ストレージにデータをエクスポートします。 これを使用すると、リレーショナルデータを Azure Blob storage にアーカイブしながら、クエリを実行することができます。

```sql
-- Export data: Move old data to Azure Blob storage while keeping it query-able via an external table.  
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] 
WITH (  
      LOCATION='/archive/customer/2009',  
      DATA_SOURCE = AzureStorage,  
      FILE_FORMAT = TextFileFormat
)  
AS
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```  

## <a name="view-polybase-objects-in-ssdt"></a>SSDT で PolyBase オブジェクトを表示する  

SQL Server Data Tools では、外部テーブルが別のフォルダー**外部テーブル**に表示されます。 外部データ ソースおよび外部ファイル形式は、 **[外部リソース]** の下のサブフォルダーにあります。  
  
![SSDT の PolyBase オブジェクト](media/polybase/external-tables-datasource.png)  

## <a name="next-steps"></a>次の手順

PolyBase について詳しくは、「[PolyBase とは](../relational-databases/polybase/polybase-guide.md)」をご覧ください。 

