---
title: Machine Learning Services (Python、R)
titleSuffix: SQL Server Big Data Clusters
description: Machine Learning Services を使用して SQL Server ビッグ データ クラスターのマスター インスタンスで Python や R のスクリプトを実行する方法について説明します。
author: dphansen
ms.author: davidph
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
ms.openlocfilehash: 66bc987b71bb8b139eec5b69e78532aa54f1294d
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531945"
---
# <a name="run-python-and-r-scripts-with-machine-learning-services-on-sql-server-big-data-clusters"></a>SQL Server ビッグ データ クラスターで Machine Learning Services を使用して Python および R のスクリプトを実行する

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[Machine Learning Services](../advanced-analytics/index.yml) を使用して [SQL Server ビッグ データ クラスター](big-data-cluster-overview.md)のマスター インスタンスで Python や R のスクリプトを実行できます。

> [!NOTE]
> また、[SQL Server 言語拡張機能](../language-extensions/language-extensions-overview.md)を使用して、マスター インスタンスで Java コードを実行することもできます。 以下の手順に従うと、言語拡張機能も有効になります。

## <a name="enable-machine-learning-services"></a>Machine Learning Services を有効にする

Machine Learning Services は、既定でビッグ データ クラスターにインストールされ、個別にインストールする必要があります。

Machine Learning Services を有効にするには、マスター インスタンスで次のステートメントを実行します。

```sql
EXEC sp_configure 'external scripts enabled', 1
RECONFIGURE WITH OVERRIDE
GO
```

## <a name="enable-always-on-availability-groups"></a>AlwaysOn 可用性グループを有効にする

[Always On 可用性グループ](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)で SQL Server ビッグ データ クラスターを使用している場合は、Machine Learning Services を有効にするための追加の手順をいくつか実行する必要があります。

1. マスター インスタンスに接続し、次のステートメントを実行します。

    ```sql
    SELECT @@SERVERNAME
    ```

    サーバー名を記録しておきます。 この例では、マスター インスタンスのサーバー名は **master-2** です。

1. ビッグ データ クラスターの Always On 可用性グループの各レプリカ上で、次の `kubectl` コマンドを実行します。

    ```
    kubectl -n bdc expose pod master-0 --port=1533 --name=mymaster-0 --type=LoadBalancer

    kubectl -n bdc expose pod master-1 --port=1533 --name=mymaster-1 --type=LoadBalancer

    kubectl -n bdc expose pod master-2 --port=1533 --name=mymaster-2 --type=LoadBalancer
    ```

    次のような出力が表示されます。
    
    ```
    service/mymaster-0 exposed

    service/mymaster-1 exposed

    service/mymaster-2 exposed
    ```

1. 各マスター レプリカ エンドポイントに接続し、スクリプトの実行を有効にします。

    次のステートメントを実行します。

    ```sql
    EXEC sp_configure 'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    GO
    ```

ビッグ データ クラスターのマスター インスタンスで、Python および R のスクリプトを実行する準備ができました。 初めてスクリプトを実行する場合は、以下のクイックスタートをご覧ください。

## <a name="next-steps"></a>次の手順

+ [クイックスタート: SQL Server Machine Learning Services で簡単な Python スクリプトを作成して実行する](../advanced-analytics/tutorials/quickstart-python-create-script.md)
+ [クイックスタート: SQL Server Machine Learning Services を使用して Python で予測モデルを作成してスコア付けする](../advanced-analytics/tutorials/quickstart-python-train-score-model.md)
+ [クイックスタート: SQL Server Machine Learning Services で簡単な R スクリプトを作成して実行する](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [クイックスタート: SQL Server Machine Learning Services を使用して R で予測モデルを作成してスコア付けする](../advanced-analytics/tutorials/quickstart-r-train-score-model.md)
