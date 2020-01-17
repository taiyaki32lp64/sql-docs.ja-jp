---
title: データベースを復元する
titleSuffix: SQL Server big data clusters
description: この記事では、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]のマスター インスタンスにデータベースを復元する方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bad1a62752dd75e181d30c28485e1c9b707aa888
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652234"
---
# <a name="restore-a-database-into-the-sql-server-big-data-cluster-master-instance"></a>SQL Server ビッグ データ クラスターのマスター インスタンスにデータベースを復元する

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

この記事では、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]のマスター インスタンスに既存のデータベースを復元する方法について説明します。 バックアップ、コピー、復元の方法を使用することをお勧めします。

## <a name="backup-your-existing-database"></a>既存のデータベースをバックアップする

最初に、Windows または Linux のいずれかの SQL Server から既存の SQL Server データベースをバックアップします。 Transact-SQL または SQL Server Management Studio (SSMS) などのツールと共に、標準的なバックアップ手法を使用します。

この記事では、AdventureWorks データベースを復元する方法について説明しますが、どのようなデータベース バックアップでも使用できます。 

> [!TIP]
> AdventureWorks のバックアップは[こちら](https://www.microsoft.com/download/details.aspx?id=49502)からダウンロードできます。

## <a name="copy-the-backup-file"></a>バックアップ ファイルをコピーする

Kubernetes クラスターのマスター インスタンス ポッド内にある SQL Server コンテナーにバックアップ ファイルをコピーします。

```bash
kubectl cp <path to .bak file> master-0:/tmp -c mssql-server -n <name of your big data cluster>
```

例:

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n clustertest
```

次に、バックアップ ファイルがポッド コンテナーにコピーされたことを確認します。

```bash
kubectl exec -it master-0 -n <name of your big data cluster> -c mssql-server -- bin/bash
cd /var/
ls /tmp
exit
```

例:

```bash
kubectl exec -it master-0 -n clustertest -c mssql-server -- bin/bash
ls /tmp
exit
```

## <a name="restore-the-backup-file"></a>バックアップ ファイルを復元する

次に、データベース バックアップをマスター インスタンス SQL Server に復元します。  Windows で作成されたデータベース バックアップを復元する場合は、ファイルの名前を取得する必要があります。  Azure Data Studio では、マスター インスタンスを接続し、この SQL スクリプトを実行します。

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/<db file name>.bak'
```

例:

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
```

![バックアップ ファイル リスト](media/restore-database/database-restore-file-list.png)

ここで、データベースを復元します。 次のスクリプトは一例です。 必要に応じて、データベースのバックアップに合わせて名前とパスを置き換えます。

```sql
RESTORE DATABASE AdventureWorks2016CTP3
FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
WITH MOVE 'AdventureWorks2016CTP3_Data' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Data.mdf',
        MOVE 'AdventureWorks2016CTP3_Log' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Log.ldf',
        MOVE 'AdventureWorks2016CTP3_mod' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_mod'
```

## <a name="configure-data-pool-and-hdfs-access"></a>データ プールと HDFS アクセスを構成する

SQL Server マスター インスタンスがデータ プールと HDFS にアクセスできるよう、データ プールと記憶域プールのストアド プロシージャを実行します。 新しく復元したデータベースに対して、次の Transact-SQL スクリプトを実行します。

```sql
USE AdventureWorks2016CTP3
GO
-- Create the SqlDataPool data source:
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
  CREATE EXTERNAL DATA SOURCE SqlDataPool
  WITH (LOCATION = 'sqldatapool://controller-svc/default');

-- Create the SqlStoragePool data source:
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
   CREATE EXTERNAL DATA SOURCE SqlStoragePool
   WITH (LOCATION = 'sqlhdfs://controller-svc/default');
GO
```

> [!NOTE]
> 以前のバージョンの SQL Server から復元されたデータベースに対してのみ、これらのセットアップ スクリプトを実行する必要があります。 SQL Server マスター インスタンスに新しいデータベースを作成した場合、データ プールと記憶域プールのストアド プロシージャは既に構成されています。

## <a name="next-steps"></a>次の手順

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の詳細については、次の概要を参照してください。

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)
