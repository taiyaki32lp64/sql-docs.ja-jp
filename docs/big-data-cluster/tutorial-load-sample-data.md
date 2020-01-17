---
title: サンプル データを読み込む
titleSuffix: SQL Server big data clusters
description: このチュートリアルでは、SQL Server ビッグ データ クラスターにサンプル データを読み込む方法について説明します。 サンプル データには、SQL Server マスター インスタンス内のリレーショナル データが含まれています。 また、記憶域プール内の HDFS データも取り込まれています。 このデータは、このセクションの他のチュートリアルにも対応しています。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 405df2c66917dc5e5b350aaaa0769bede6ccf6c9
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653288"
---
# <a name="tutorial-load-sample-data-into-a-sql-server-big-data-cluster"></a>チュートリアル:SQL Server ビッグ データ クラスターにサンプル データを読み込む

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

このチュートリアルでは、スクリプトを使用して [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]にサンプル データを読み込む方法について説明します。 ドキュメントに記載されている他のチュートリアルの多くで、このサンプル データが使用されています。

> [!TIP]
> [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]の追加のサンプルは、[sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster) GitHub リポジトリにあります。 それらは、パス **sql-server-samples/samples/features/sql-big-data-cluster/** に置かれています。

## <a name="prerequisites"></a>Prerequisites

- [展開済みのビッグ データ クラスター](deployment-guidance.md)
- [ビッグ データ ツール](deploy-big-data-tools.md)
   - **azdata**
   - **kubectl**
   - **sqlcmd**
   - **curl**
 
## <a id="sampledata"></a> サンプル データを読み込む

次の手順では、ブートストラップ スクリプトを使用して SQL Server データベースのバックアップをダウンロードし、ご利用のビッグ データ クラスターにそのデータを読み込みます。 使いやすいように、これらの手順は 「[Windows](#windows)」セクションと「[Linux](#linux)」セクションに分けられています。

## <a id="windows"></a> Windows

次の手順では、Windows クライアントを使用して、ご利用のビッグ データ クラスターにサンプル データを読み込む方法について説明します。

1. 新しい Windows コマンド プロンプトを開きます。

   > [!IMPORTANT]
   > これらの手順には、Windows PowerShell を使用しないでください。 Powershell では、PowerShell バージョンの **curl** が使用されるため、スクリプトは失敗します。

1. **curl** を使用して、サンプル データ用のブートストラップ スクリプトをダウンロードします。

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. **bootstrap-sample-db.sql** Transact-SQL スクリプトがダウンロードされます。 このスクリプトは、ブートストラップ スクリプトによって呼び出されます。

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. ブートストラップ スクリプトでは、ご利用のビッグ データ クラスターに関する次の位置指定パラメーターが必要です。

   | パラメーター | [説明] |
   |---|---|
   | <CLUSTER_NAMESPACE> | ビッグ データ クラスターに付ける名前。 |
   | <SQL_MASTER_IP> | マスター インスタンスの IP アドレス。 |
   | <SQL_MASTER_SA_PASSWORD> | マスター インスタンスの SA パスワード。 |
   | <KNOX_IP> | HDFS/Spark ゲートウェイの IP アドレス。 |
   | <KNOX_PASSWORD> | HDFS/Spark ゲートウェイのパスワード。 |

   > [!TIP]
   > [kubectl](cluster-troubleshooting-commands.md) を使用して、SQL Server マスター インスタンスと Knox の IP アドレスを検索します。 `kubectl get svc -n <your-big-data-cluster-name>` を実行して、マスター インスタンスの EXTERNAL-IP アドレス (**master-svc-external**) と Knox (**gateway-svc-external**) を確認します。 クラスターの既定の名前は **mssql-cluster** です。

1. ブートストラップ スクリプトを実行します。

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a id="linux"></a> Linux

次の手順では、Linux クライアントを使用して、ご利用のビッグ データ クラスターにサンプル データを読み込む方法について説明します。

1. ブートストラップ スクリプトをダウンロードし、実行可能ファイルのアクセス許可を割り当てます。

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. **bootstrap-sample-db.sql** Transact-SQL スクリプトがダウンロードされます。 このスクリプトは、ブートストラップ スクリプトによって呼び出されます。

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. ブートストラップ スクリプトでは、ご利用のビッグ データ クラスターに関する次の位置指定パラメーターが必要です。

   | パラメーター | [説明] |
   |---|---|
   | <CLUSTER_NAMESPACE> | ビッグ データ クラスターに付ける名前。 |
   | <SQL_MASTER_IP> | マスター インスタンスの IP アドレス。 |
   | <SQL_MASTER_SA_PASSWORD> | マスター インスタンスの SA パスワード。 |
   | <KNOX_IP> | HDFS/Spark ゲートウェイの IP アドレス。 |
   | <KNOX_PASSWORD> | HDFS/Spark ゲートウェイのパスワード。 |

   > [!TIP]
   > [kubectl](cluster-troubleshooting-commands.md) を使用して、SQL Server マスター インスタンスと Knox の IP アドレスを検索します。 `kubectl get svc -n <your-big-data-cluster-name>` を実行して、マスター インスタンスの EXTERNAL-IP アドレス (**master-svc-external**) と Knox (**gateway-svc-external**) を確認します。 クラスターの既定の名前は **mssql-cluster** です。

1. ブートストラップ スクリプトを実行します。

   ```bash
   sudo env "PATH=$PATH" ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_IP> <SQL_MASTER_SA_PASSWORD> <KNOX_IP> <KNOX_PASSWORD>
   ```

## <a name="next-steps"></a>次の手順

ブートストラップ スクリプトが実行されると、ご利用のビッグ データ クラスターにはサンプル データベースと HDFS データが取り込まれます。 次のチュートリアルでは、サンプル データを使用してビッグ データ クラスターの機能を実演します。

データの仮想化:

- [チュートリアル: SQL Server ビッグ データ クラスター内の HDFS にクエリを実行する](tutorial-query-hdfs-storage-pool.md)
- [チュートリアル: SQL Server ビッグ データ クラスターから Oracle にクエリを実行する](tutorial-query-oracle.md)

データ インジェスト:

- [チュートリアル: Transact-SQL を使用して SQL Server のデータ プールにデータを取り込む](tutorial-data-pool-ingest-sql.md)
- [チュートリアル: Spark ジョブを使用して SQL Server のデータ プールにデータを取り込む](tutorial-data-pool-ingest-spark.md)

Notebooks:

- [チュートリアル: SQL Server 2019 ビッグ データ クラスターでサンプルのノートブックを実行する](tutorial-notebook-spark.md)
