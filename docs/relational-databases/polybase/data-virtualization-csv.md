---
title: '外部データの仮想化: コンマ区切り値 (csv)'
description: このページでは、CSV ファイルに対して外部テーブルの作成ウィザードを使用する詳細な手順を説明します
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.metadata: seo-lt-2019
ms.openlocfilehash: b1bb5f2e807731e1020729e045c017b6f1524ae1
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75256169"
---
# <a name="use-the-external-table-wizard-with-csv-files"></a>CSV ファイルで外部テーブル ウィザードを使用する

SQL Server 2019 では、CSV ファイルからのデータを HDFS に仮想化することもできます。  このプロセスでは、データを元の場所に置いたまま、SQL Server インスタンスでデータを**仮想化**して、SQL Server 内の他のテーブルと同じようにクエリを行うことができます。 この機能により、ETL プロセスの必要性が最小になります。 これは、Polybase コネクタを使用することによって可能です。 データの仮想化について詳しくは、「[PolyBase の概要](polybase-guide.md)」をご覧ください。

## <a name="prerequisite"></a>前提条件

ビッグ データ クラスターでは、データ プールと記憶域プールの外部データ ソースは、既定ではデータベース内には作成されません。 ウィザードを使用する前に、次の Transact-SQL クエリを使用してターゲット データベースに既定の **SqlStoragePool** 外部データ ソースを作成してください。 最初に、クエリのコンテキストをターゲット データベースに変更します。

```sql
-- Create default data sources for SQL Big Data Cluster
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
    CREATE EXTERNAL DATA SOURCE SqlDataPool
    WITH (LOCATION = 'sqldatapool://controller-svc/default');

IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
    CREATE EXTERNAL DATA SOURCE SqlStoragePool
    WITH (LOCATION = 'sqlhdfs://controller-svc/default');
```

## <a name="launch-the-external-table-wizard"></a>外部テーブル ウィザードを起動する

IP アドレスを使用して HDFS ルートに接続します。 オブジェクト エクスプローラーで要素を展開します。 次に、既存の SQL Server インスタンスにデータを仮想化する CSV のいずれかを選択します。 データベースを右クリックして、コンテキスト メニューから **[Create External Table From CSV File]\(CSV ファイルからの外部テーブルの作成\)** を選択します。 HDFS 内のフォルダーの下にある CSV ファイルが同じスキーマに従っている場合、そのフォルダーのファイルから外部テーブルを作成することもできます。 これにより、個々のファイルを処理する必要なしにフォルダー レベルでデータを仮想化でき、結合されたデータに対する結合された結果セットを取得できます。 これにより、データ仮想化ウィザードが起動します。 コマンド パレットで Ctrl + Shift + P (Windows) キーまたは Cmd + Shift + P (Mac) キーを押して、データ仮想化ウィザードを起動することもできます。

![データ仮想化ウィザード](media/data-virtualization/csv-virtualize-data-wizard.png)

## <a name="connect-to-a-sql-server-master-instance"></a>SQL Server マスター インスタンスに接続する

ここでは、IP、ポート、および資格情報を使用して接続する SQL マスター インスタンスを指定できます。 前に保存した接続に、 **[Active SQL Server connections]\(アクティブな SQL Server 接続\)** ドロップダウン ボックスからアクセスできます。 
> [!NOTE]
>保存した接続を使用している場合、他のフィールドはブロックされます。


![データ ソースを選択する](media/data-virtualization/csv-connect-to-master.png)

[次へ] をクリックしてウィザードの次のステップに進み、データベースのマスター キーを設定します。

## <a name="select-destination-database"></a>変換先データベースを選択する

このステップでは、データを仮想化する変換先データベースを選択します。 ドロップダウン フィールドには、前の画面で指定した SQL マスター インスタンスで許容されるすべてのデータベースが含まれます。 ここでは、新しい外部テーブルの名前を指定し、使用されるスキーマを参照することもできます。

![データベースのマスター キーを作成する](media/data-virtualization/csv-select-destination.png)


## <a name="preview-data"></a>データをプレビューする

このウィンドウでは、検証のために、CSV ファイルの最初の 50 行のプレビューを表示することができます。

プレビューの表示が終わったら、[次へ] をクリックして続行します。

![外部データ ソースの資格情報](media/data-virtualization/csv-preview-data.png)

## <a name="modify-columns"></a>列を変更する

次のウィンドウでは、作成する外部テーブルの列を変更できます。 列の名前とデータ型を変更でき、null 許容型の行にすることができます。 

![外部データ ソースの資格情報](media/data-virtualization/csv-modify-columns.png)


## <a name="summary"></a>まとめ

このステップでは、選択内容の要約が提供されます。 SQL マスター インスタンスと提案される外部テーブルの情報が提供されます。 このステップでは、 **[スクリプトの生成]** オプションを選択すると外部データ ソースを作成する構文が T-SQL でスクリプト化され、 **[作成]** を選択すると外部データ ソース オブジェクトが作成されます。

![概要画面](media/data-virtualization/csv-virtualize-data-summary.png)

[作成] をクリックした場合は、出力先データベースに作成された外部テーブルを確認できます。

![外部データ ソース](media/data-virtualization/csv-external-data-sources.png)

**[スクリプトの生成]** をクリックした場合は、外部データ ソース オブジェクトを作成するために生成される T-SQL クエリを確認できます。

![スクリプトの生成](media/data-virtualization/csv-generated-script.png)

> [!NOTE]
> [スクリプトの生成] は、ウィザードの最後のページにのみ表示されるべきです。 現在は、すべてのページに表示されます。

## <a name="next-steps"></a>次のステップ

SQL Server のビッグ データ クラスターおよび関連するシナリオについて詳しくは、「[SQL Server ビッグ データ クラスターとは](../../big-data-cluster/big-data-cluster-overview.md)」をご覧ください。
