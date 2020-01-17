---
title: RStudio から sparklyr を使用する
titleSuffix: SQL Server big data clusters
description: RStudio から sparklyr を使用してビッグ データ クラスターに接続します。
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 375993e4fd9506c129e4f98d9ad2193472e03edb
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531615"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>SQL Server のビッグ データ クラスターで sparklyr を使用する

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Sparklyr には、Apache Spark 用の R インターフェイスが用意されています。 Sparklyr は、Spark を使用する R 開発者にとって一般的な方法です。 この記事では、RStudio を使用して [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] で sparklyr を使用する方法について説明します。

## <a name="prerequisites"></a>Prerequisites

- [SQL Server 2019 のビッグ データ クラスターを展開する](quickstart-big-data-cluster-deploy.md).

### <a name="install-rstudio-desktop"></a>RStudio Desktop をインストールする

次の手順で **RStudio Desktop** をインストールして構成します。

1. Windows クライアントで実行している場合は、[R 3.4.4 をダウンロードしてインストールします](https://cran.rstudio.com/bin/windows/base/old/3.4.4)。

1. [RStudio Desktop をダウンロードしてインストールします](https://www.rstudio.com/products/rstudio/download/)。

1. インストールが完了したら、RStudio Desktop 内で次のコマンドを実行して、必要なパッケージをインストールします。

   ```RStudioDesktop
   install.packages("DBI", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("dplyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("sparklyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   ```

## <a name="connect-to-spark-in-a-big-data-cluster"></a>ビッグ データ クラスターで Spark に接続する

sparklyr を使用し、Livy と HDFS/Spark ゲートウェイを使用してクライアントからビッグ データ クラスターに接続できます。 

RStudio で、次の例のように R スクリプトを作成し、Spark に接続します。

> [!TIP]
> `<AZDATA_USERNAME>` と `<AZDATA_PASSWORD>` の値については、ビッグ データ クラスターの展開中に設定したユーザー名 (root など) とパスワードを使用します。 `<IP>` と `<PORT>` の値については、[ビッグ データ クラスターへの接続](connect-to-big-data-cluster.md)に関するドキュメントを参照してください。

```r
library(sparklyr)
library(dplyr)
library(DBI)

#Specify the Knox username and password
config <- livy_config(user = "<AZDATA_USERNAME>", password = "<AZDATA_PASSWORD>")

httr::set_config(httr::config(ssl_verifypeer = 0L, ssl_verifyhost = 0L))

sc <- spark_connect(master = "https://<IP>:<PORT>/gateway/default/livy/v1",
                    method = "livy",
                    config = config)
```

## <a name="run-sparklyr-queries"></a>sparklyr クエリを実行する

Spark に接続すると、sparklyr を実行できます。 次の例では、sparklyr を使用して、iris データセットに対してクエリを実行します。

```r
iris_tbl <- copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="distributed-r-computations"></a>分散 R 計算

sparklyr の機能の 1 つとして、[spark_apply](https://spark.rstudio.com/reference/spark_apply/) を使用して [R 計算を分散](https://spark.rstudio.com/guides/distributed-r/)する機能があります。

ビッグ データ クラスターは Livy 接続が使用されるため、**spark_apply** の呼び出しで `packages = FALSE` を設定する必要があります。 詳細については、分散 R 計算に関する sparklyr のドキュメントの「[Livy](https://spark.rstudio.com/guides/distributed-r/#livy)」セクションを参照してください。 この設定では、**spark_apply** に渡された R コードで、Spark クラスターに既にインストールされている R パッケージのみを使用できます。 この機能について、次の例を示します。

```r
iris_tbl %>% spark_apply(function(e) nrow(e), names = "nrow", group_by = "Species", packages = FALSE)
```

## <a name="next-steps"></a>次の手順

ビッグ データ クラスターの詳細については、[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]の概要](big-data-cluster-overview.md)に関するページを参照してください。
