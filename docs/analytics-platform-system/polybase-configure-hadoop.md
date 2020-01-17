---
title: '外部データへのアクセス: Hadoop-PolyBase'
description: Parallel Data Warehouse で PolyBase を構成して外部 Hadoop に接続する方法について説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 12/13/2019
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019, seo-lt-2019
ms.openlocfilehash: dc796ff58c5320e60011dc46dd45468177a98ed8
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245391"
---
# <a name="configure-polybase-to-access-external-data-in-hadoop"></a>Hadoop 内の外部データにアクセスするように PolyBase を構成する

この記事では、APS アプライアンスで PolyBase を使用して Hadoop の外部データを照会する方法について説明します。

## <a name="prerequisites"></a>前提条件

PolyBase は、Hortonworks Data Platform (HDP) と Cloudera Distributed Hadoop (CDH) の 2 つの Hadoop プロバイダーをサポートしています。 Hadoop では、新規リリースについて "Major.Minor.Version" パターンを採用しており、サポートされているメジャーおよびマイナー リリース内のすべてのバージョンがサポートされています。 次の Hadoop プロバイダーがサポートされています。
 - Linux/Windows Server 上の Hortonworks HDP 1.3  
 - Hortonworks HDP 2.1-2.6 (Linux)
 - Hortonworks HDP 3.0-3.1 (Linux)
 - Windows Server 上の Hortonworks HDP 2.1 - 2.3  
 - Linux 上の Cloudera CDH 4.3  
 - Cloudera CDH 5.1-5.5、5.9-5.13、5.15 & 5.16 (Linux)

### <a name="configure-hadoop-connectivity"></a>Hadoop 接続を構成する

まず、特定の Hadoop プロバイダーを使用するように APS を構成します。

1. 'hadoop connectivity' を使用して [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) を実行し、プロバイダーに対する適切な値を設定します。 プロバイダーの値を見つけるには、[PolyBase 接続構成 ](../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)に関する記事を参照してください。 

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 and 3.0 - 3.1 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. [アプライアンス Configuration Manager](launch-the-configuration-manager.md)の [サービスの状態] ページを使用して、APS リージョンを再起動します。
  
## <a id="pushdown"></a>プッシュダウン計算を有効にする  

クエリ パフォーマンスを高めるには、Hadoop クラスターへのプッシュダウン計算を有効にします。  
  
1. PDW コントロールノードへのリモートデスクトップ接続を開きます。

2. コントロールノードで**yarn-site.xml**ファイルを見つけます。 通常、このパスは次のとおりです。  

   ```xml  
   C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf\  
   ```  

3. Hadoop コンピューターで、Hadoop 構成ディレクトリ内の対応するファイルを検索します。 このファイル内の構成キー yarn.application.classpath の値をコピーします。  
  
4. [コントロール] ノードの**yarn ファイル**で、 **yarn**プロパティを見つけます。これは、 Hadoop コンピューターからこの値要素に値を貼り付けます。  
  
5. すべての CDH 5.X バージョンで、yarn.site.xml file の最後か mapred-site.xml file に mapreduce.application.classpath 構成パラメーターを追加する必要があります。 HortonWorks では、yarn.application.classpath 構成内にこれらの構成が含まれます。 例については、「[PolyBase の構成](../relational-databases/polybase/polybase-configuration.md)」を参照してください。

## <a name="example-xml-files-for-cdh-5x-cluster-default-values"></a>CDH 5.x クラスターの既定値の XML ファイルの例

yarn.application.classpath と mapreduce.application.classpath で構成される Yarn-site.xml。

```xml
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
   <property>
      <name>yarn.resourcemanager.connect.max-wait.ms</name>
      <value>40000</value>
   </property>
   <property>
      <name>yarn.resourcemanager.connect.retry-interval.ms</name>
      <value>30000</value>
   </property>
<!-- Applications' Configuration-->
   <property>
     <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
      <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
      <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
      <name>yarn.application.classpath</name>
      <value>$HADOOP_CLIENT_CONF_DIR,$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/*,$HADOOP_COMMON_HOME/lib/*,$HADOOP_HDFS_HOME/*,$HADOOP_HDFS_HOME/lib/*,$HADOOP_YARN_HOME/*,$HADOOP_YARN_HOME/lib/,$HADOOP_MAPRED_HOME/*,$HADOOP_MAPRED_HOME/lib/*,$MR2_CLASSPATH*</value>
   </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
   <property>
      <name>yarn.resourcemanager.principal</name>
      <value></value>
   </property>
-->
</configuration>
```

2つの構成設定を mapred-site.xml と yarn-site.xml に分割することを選択した場合、ファイルは次のようになります。

**yarn-site.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
   <property>
      <name>yarn.resourcemanager.connect.max-wait.ms</name>
      <value>40000</value>
   </property>
   <property>
      <name>yarn.resourcemanager.connect.retry-interval.ms</name>
      <value>30000</value>
   </property>
<!-- Applications' Configuration-->
   <property>
     <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
      <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
      <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
      <name>yarn.application.classpath</name>
      <value>$HADOOP_CLIENT_CONF_DIR,$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/*,$HADOOP_COMMON_HOME/lib/*,$HADOOP_HDFS_HOME/*,$HADOOP_HDFS_HOME/lib/*,$HADOOP_YARN_HOME/*,$HADOOP_YARN_HOME/lib/*</value>
   </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
   <property>
      <name>yarn.resourcemanager.principal</name>
      <value></value>
   </property>
-->
</configuration>
```

**mapred-site.xml**

プロパティ mapreduce.application.classpath が追加されています。 CDH 5.x では、Ambari の名前付け規則に従って構成値を確認できます。

```xml
<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
<configuration xmlns:xi="http://www.w3.org/2001/XInclude">
   <property>
     <name>mapred.min.split.size</name>
       <value>1073741824</value>
   </property>
   <property>
     <name>mapreduce.app-submission.cross-platform</name>
     <value>true</value>
   </property>
<property>
     <name>mapreduce.application.classpath</name>
     <value>$HADOOP_MAPRED_HOME/*,$HADOOP_MAPRED_HOME/lib/*,$MR2_CLASSPATH</value>
   </property>


<!--kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
   <property>
     <name>mapreduce.jobhistory.principal</name>
     <value></value>
   </property>
   <property>
     <name>mapreduce.jobhistory.address</name>
     <value></value>
   </property>
-->
</configuration>
```

## <a name="example-xml-files-for-hdp-3x-cluster-default-values"></a>HDP 3.x クラスターの既定値の XML ファイルの例

**yarn-site.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
  <property>
     <name>yarn.resourcemanager.connect.max-wait.ms</name>
     <value>40000</value>
  </property>
  <property>
     <name>yarn.resourcemanager.connect.retry-interval.ms</name>
     <value>30000</value>
  </property>
<!-- Applications' Configuration-->
  <property>
    <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
     <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
     <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
     <name>yarn.application.classpath</name>
     <value>$HADOOP_CONF_DIR,/usr/hdp/3.1.0.0-78/hadoop/*,/usr/hdp/3.1.0.0-78/hadoop/lib/*,/usr/hdp/current/hadoop-hdfs-client/*,/usr/hdp/current/hadoop-hdfs-client/lib/*,/usr/hdp/current/hadoop-yarn-client/*,/usr/hdp/current/hadoop-yarn-client/lib/*,/usr/hdp/3.1.0.0-78/hadoop-mapreduce/*,/usr/hdp/3.1.0.0-78/hadoop-yarn/*,/usr/hdp/3.1.0.0-78/hadoop-yarn/lib/*,/usr/hdp/3.1.0.0-78/hadoop-mapreduce/lib/*,/usr/hdp/share/hadoop/common/*,/usr/hdp/share/hadoop/common/lib/*,/usr/hdp/share/hadoop/tools/lib/*</value>
  </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
  <property>
     <name>yarn.resourcemanager.principal</name>
     <value></value>
  </property>
-->
</configuration>
```

## <a name="configure-an-external-table"></a>外部テーブルを構成する

Hadoop データ ソース内のデータのクエリを実行するには、Transact-SQL クエリで使用する外部テーブルを定義する必要があります。 次の手順では、外部テーブルを構成する方法を説明します。

1. データベースにマスター キーを作成します。 資格情報のシークレットを暗号化する必要があります。

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
   ```

2. Kerberos でセキュリティ保護された Hadoop クラスターのデータベース スコープ資格情報を作成します。

   ```sql
   -- IDENTITY: the Kerberos user name.  
   -- SECRET: the Kerberos password  
   CREATE DATABASE SCOPED CREDENTIAL HadoopUser1
   WITH IDENTITY = '<hadoop_user_name>', Secret = '<hadoop_password>';  
   ```

3. [CREATE EXTERNAL DATA source](../t-sql/statements/create-external-data-source-transact-sql.md)を使用して外部データソースを作成します。

   ```sql
   -- LOCATION (Required) : Hadoop Name Node IP address and port.  
   -- RESOURCE MANAGER LOCATION (Optional): Hadoop Resource Manager location to enable pushdown computation.  
   -- CREDENTIAL (Optional):  the database scoped credential, created above.  
   CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (  
         TYPE = HADOOP,
         LOCATION ='hdfs://10.xxx.xx.xxx:xxxx',
         RESOURCE_MANAGER_LOCATION = '10.xxx.xx.xxx:xxxx',
         CREDENTIAL = HadoopUser1
   );  
   ```

4. 
  [CREATE EXTERNAL FILE FORMAT](../t-sql/statements/create-external-file-format-transact-sql.md) を使用して外部ファイル形式を作成します。

   ```sql
   -- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE)  
   ```

5. 
  [CREATE EXTERNAL TABLE](../t-sql/statements/create-external-table-transact-sql.md)を使用して、Hadoop に格納されているデータをポイントする外部テーブルを作成します。 この例では、外部データには車両センサー データが含まれています。

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
         DATA_SOURCE = MyHadoopCluster,  
         FILE_FORMAT = TextFileFormat  
   );  
   ```

6. 外部テーブルの統計を作成します。

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

次のアドホッククエリは、Hadoop データとリレーショナルに結合します。 これは、35 mph を上回る顧客を選択し、AP に格納されている構造化顧客データを、Hadoop に格納されている車両センサーデータと結合します。  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
OPTION (FORCE EXTERNALPUSHDOWN);   -- or OPTION (DISABLE EXTERNALPUSHDOWN)  
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

次のクエリでは、APS から Hadoop にデータをエクスポートします。 これを使用すると、リレーショナルデータを Hadoop にアーカイブしながら、クエリを実行することができます。

```sql
-- Export data: Move old data to Hadoop while keeping it query-able via an external table.  
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] 
WITH (  
      LOCATION='/archive/customer/2009',  
      DATA_SOURCE = HadoopHDP2,  
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

Hadoop のセキュリティ設定については、「 [hadoop セキュリティの構成](polybase-configure-hadoop-security.md)」を参照してください。<br>
PolyBase について詳しくは、「[PolyBase とは](../relational-databases/polybase/polybase-guide.md)」をご覧ください。 
 
