---
title: 高可用性を使用して SQL Server ビッグ データ クラスターを展開する
titleSuffix: Deploy SQL Server Big Data Cluster with high availability
description: 高可用性を使用して SQL Server ビッグ データ クラスターを展開する方法を学習します。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 231a33f4d149e442487a7c93c1e2b4c5cdfad8d5
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531988"
---
# <a name="deploy-sql-server-big-data-cluster-with-high-availability"></a>高可用性を使用して SQL Server ビッグ データ クラスターを展開する

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server ビッグ データ クラスターは、コンテナー化アプリケーションとして Kubernetes 上にあり、ステートフル セットや永続ストレージなどの機能を使用するため、このインフラストラクチャには、サービスの正常性を維持するためにクラスター コンポーネントで利用される、正常性監視、障害検出、およびフェールオーバー メカニズムが組み込まれています。 信頼性を向上させるために、高可用性構成で追加のレプリカを使用して展開するように、SQL Server マスター インスタンスまたは HDFS 名前ノードと Spark 共有サービスを構成することもできます。 監視、障害検出、および自動フェールオーバーは、ビッグ データ クラスター管理サービス、つまり、制御サービスによって管理されます。 このサービスでは、可用性グループのセットアップから、データベース ミラーリング エンドポイントの構成、可用性グループへのデータベースの追加またはフェールオーバーとアップグレードの調整まですべて、ユーザーの介入なしで提供されます。 

次の図は、SQL Server ビッグ データ クラスターに可用性グループが展開される方法を示しています。

:::image type="content" source="media/deployment-high-availability/contained-ag.png" alt-text="high-availability-ag-bdc":::

可用性グループで有効になる機能の一部を以下に示します。

- 高可用性の設定が展開構成ファイルで指定されている場合は、`containedag` という名前の 1 つの可用性グループが作成されます。 既定では、`containedag` に、プライマリを含む、3 つのレプリカがあります。 可用性グループの CRUD 操作はすべて内部的に管理されます。これには、可用性グループの作成や作成された可用性グループへのレプリカの参加が含まれます。 ビッグ データ クラスターの SQL Server マスター インスタンスで、追加の可用性グループを作成することはできません。
- データベースはすべて可用性グループに自動的に追加されます。これには、すべてのユーザーおよびシステム データベース (`master` や `msdb` など) が含まれます。 この機能により、可用性グループ レプリカ全体で単一システム ビューが提供されます。 追加のモデル データベース (`model_replicatedmaster` と `model_msdb`) は、システム データベースのレプリケートされた部分をシード処理するために使用されます。 これらのデータベースに加えて、インスタンスに直接接続している場合は、`containedag_master` および `containedag_msdb` データベースが表示されます。 `containedag` データベースは、可用性グループ内の `master` と `msdb` を表します。

  > [!IMPORTANT]
  > SQL Server 2019 CU1 リリースの時点では、CREATE DATABASE ステートメントの結果として作成されたデータベースのみが、可用性グループに自動的に追加されます。 復元などの他のワークフローの結果としてインスタンス上に作成されたデータベースは、まだ可用性グループに追加されていないため、ビッグ データ クラスター管理者が手動でこれを行う必要があります。 手順については、「[SQL Server インスタンスに接続する](#instance-connect)」セクションを参照してください。
  >
- Polybase 構成データベースは可用性グループには含まれません。これは、各レプリカに固有のインスタンス レベルのメタデータが含まれているためです。
- 外部エンドポイントは、可用性グループ内のデータベースへの接続用に自動的にプロビジョニングされます。 このエンドポイント `master-svc-external` は、可用性グループ リスナーの役割を果たします。
- 2 つ目の外部エンドポイントは、読み取りワークロードをスケールアウトするために、セカンダリ レプリカへの読み取り専用接続用にプロビジョニングされます。

## <a name="deploy"></a>配置

可用性グループに SQL Server マスターを展開するには、次のようにします。

1. `hadr` 機能を有効にします
1. AG のレプリカの数を指定します (最小値は 3)
1. 読み取り専用セカンダリ レプリカへの接続用に作成された 2 番目の外部エンドポイントの詳細を構成します

`aks-dev-test-ha` または `kubeadm-prod` の組み込み構成プロファイルを使用して、ビッグ データ クラスターのカスタマイズを開始できます。 これらのプロファイルには、追加の高可用性を構成できるリソースに必要な設定が含まれます。 たとえば、以下は、SQL Server マスター インスタンスの可用性グループの有効化に関連する、`bdc.json` 構成ファイルのセクションです。  

```json
{
  ...
    "spec": {
      "type": "Master",
      "replicas": 3,
      "endpoints": [
        {
          "name": "Master",
          "serviceType": "LoadBalancer",
          "port": 31433
        },
        {
          "name": "MasterSecondary",
          "serviceType": "LoadBalancer",
          "port": 31436
        }
      ],
      "settings": {
        "sql": {
          "hadr.enabled": "true"
        }
      }
    }
  ...
}
```

次の手順では、`aks-dev-test-ha` プロファイルから開始し、ビッグ データ クラスターの展開構成をカスタマイズする方法の例について説明します。 `kubeadm` クラスターでの展開でも、同様の手順が適用されますが、`endpoints` セクションの `serviceType` には必ず `NodePort` を使用するようにしてください。

1. ターゲットとなるプロファイルを複製します

    ```bash
    azdata bdc config init --source aks-dev-test-ha --target custom-aks-ha
    ```

1. 必要に応じて、カスタム プロファイルを任意で編集することもできます。 
1. 上記で作成されたクラスター構成プロファイルを使用して、クラスターの展開を開始します

    ```bash
    azdata bdc create --config-profile custom-aks-ha --accept-eula yes
    ```

## <a name="connect-to-sql-server-databases-in-the-availability-group"></a>可用性グループ内の SQL Server データベースに接続する

SQL Server マスターに対して実行するワークロードの種類に応じて、読み取り/書き込みワークロードの場合はプライマリに、読み取り専用の種類のワークロードの場合はセカンダリ レプリカ内のデータベースに接続できます。 接続の種類ごとの概要を以下に示します。

### <a name="connect-to-databases-on-the-primary-replica"></a>プライマリ レプリカのデータベースに接続する

プライマリ レプリカへの接続では、`sql-server-master` エンドポイントを使用します。 このエンドポイントは、AG のリスナーでもあります。 このエンドポイントを使用する場合、すべての接続は可用性グループ内のデータベースのコンテキストにあります。 たとえば、このエンドポイントを使用する既定の接続では、SQL Server インスタンスの `master` データベースではなく、可用性グループ内の `master` データベースに接続することになります。 次のコマンドを実行して、エンドポイントを検索します。

```bash
azdata bdc endpoint list -e sql-server-master -o table
```

```
Description                           Endpoint             Name               Protocol
------------------------------------  -------------------  -----------------  ----------
SQL Server Master Instance Front-End  11.11.111.111,11111  sql-server-master  tds
```

> [!NOTE]
> フェールオーバー イベントは、HDFS やデータ プールなどのリモート データ ソースからデータにアクセスする分散クエリの実行中に発生する可能性があります。 ベスト プラクティスとして、フェールオーバーによる切断が発生した場合に接続再試行ロジックを使用するように、アプリケーションを設計する必要があります。  
>

### <a name="connect-to-databases-on-the-secondary-replicas"></a>セカンダリ レプリカのデータベースに接続する

セカンダリ レプリカのデータベースへの読み取り専用接続では、`sql-server-master-readonly` エンドポイントを使用します。 このエンドポイントは、すべてのセカンダリ レプリカにわたるロード バランサーのように機能します。  このエンドポイントを使用する場合、すべての接続は可用性グループ内のデータベースのコンテキストにあります。 たとえば、このエンドポイントを使用する既定の接続では、SQL Server インスタンスの `master` データベースではなく、可用性グループ内の `master` データベースに接続することになります。 

```bash
azdata bdc endpoint list -e sql-server-master-readonly -o table
```

```
Description                                    Endpoint            Name                        Protocol
---------------------------------------------  ------------------  --------------------------  ----------
SQL Server Master Readable Secondary Replicas  11.11.111.11,11111  sql-server-master-readonly  tds
```

## <a id="instance-connect"></a> SQL Server インスタンスに接続する

サーバー レベルの構成を設定する、または可用性グループにデータベースを手動で追加するなどの特定の操作では、SQL Server インスタンスに接続する必要があります。 `sp_configure`、`RESTORE DATABASE`、または任意の可用性グループの DDL などの操作には、この種の接続が必要になります。 既定では、ビッグ データ クラスターにインスタンス接続を有効にするエンドポイントが含まれていないため、このエンドポイントを手動で公開する必要があります。 

> [!IMPORTANT]
> SQL Server インスタンス接続用に公開されたエンドポイントでは、Active Directory が有効になっているクラスターであっても、サポートされるのは SQL 認証のみとなります。 既定では、ビッグ データ クラスターの展開中に、`sa` ログインが無効になり、`AZDATA_USERNAME` および `AZDATA_PASSWORD` 環境変数の展開時に指定された値に基づいて、新しい `sysadmin` ログインがプロビジョニングされます。

このエンドポイントを公開してから、復元ワークフローで作成されたデータベースを可用性グループに追加する方法の例を以下に示します。 `sp_configure` でサーバー構成を変更する場合は、SQL Server マスター インスタンスへの接続を設定するための同様の手順が適用されます。

- `sql-server-master` エンドポイントに接続してプライマリ レプリカをホストするポッドを特定して、以下を実行します。

    ```sql
    SELECT @@SERVERNAME
   ```

- 新しい Kubernetes サービスを作成して外部エンドポイントを公開します

    `kubeadm` クラスターの場合は、以下のコマンドを実行します。 `podName` を前の手順で返されたサーバーの名前に、`serviceName` を作成された Kubernetes サービスの優先名に、`namespaceName`* を BDC クラスターの名前に置き換えます。

    ```bash
    kubectl -n <namespaceName> expose pod <podName> --port=1533  --name=<serviceName> --type=NodePort
    ```

    aks クラスターを実行する場合も同じコマンドを実行しますが、作成されるサービスの種類は `LoadBalancer` となります。 例: 

    ```bash
    kubectl -n <namespaceName> expose pod <podName> --port=1533  --name=<serviceName> --type=LoadBalancer
    ```

    aks に対して実行されるこのコマンドの例を以下に示します。この場合、プライマリをホストしているポッドは `master-0` となります。

    ```bash
    kubectl -n mssql-cluster expose pod master-0 --port=1533  --name=master-sql-0 --type=LoadBalancer
    ```

    作成された Kubernetes サービスの IP を取得します。

    ```bash
    kubectl get services -n <namespaceName>
    ```

> [!IMPORTANT]
> ベスト プラクティスとして、このコマンドを実行し、上記で作成された Kubernetes サービスを削除してクリーンアップする必要があります。
>
>```bash
>kubectl delete svc master-sql-0 -n mssql-cluster
>```

- 可用性グループにデータベースを追加します。

    データベースを AG に追加するには、完全復旧モードで実行する必要があり、ログ バックアップを作成する必要があります。 上記で作成された Kubernetes サービスの IP を使用して、SQL Server インスタンスに接続し、以下に示すように TSQL ステートメントを実行します。

    ```sql
    ALTER DATABASE <databaseName> SET RECOVERY FULL;
    BACKUP DATABASE <databaseName> TO DISK='<filePath>'
    ALTER AVAILABILITY GROUP containedag ADD DATABASE <databaseName>
    ```

    以下の例では、インスタンスで復元された `sales` という名前のデータベースを追加します。

    ```sql
    ALTER DATABASE sales SET RECOVERY FULL;
    BACKUP DATABASE sales TO DISK='/var/opt/mssql/data/sales.bak'
    ALTER AVAILABILITY GROUP containedag ADD DATABASE sales
    ```

## <a name="known-limitations"></a>既知の制限事項

ビッグ データ クラスターの SQL Server マスターの可用性グループに関する既知の問題と制限事項は、次のとおりです。

- `RESTORE DATABSE`、`CREATE DATABASE FROM SNAPSHOT` などの `CREATE DATABASE` 以外のワークフローの結果として作成されたデータベースは、可用性グループに自動的に追加されません。 [インスタンスに接続](#instance-connect)し、データベースを可用性グループに手動で追加します。
- `sp_configure` でのサーバー構成設定の実行などの特定の操作では、可用性グループ `master` ではなく、SQL Server インスタンス `master` データベースへの接続が必要になります。 対応するプライマリ エンドポイントを使用することはできません。 [指示](#instance-connect)に従ってエンドポイントを公開し、SQL Server インスタンスに接続して `sp_configure` を実行します。 SQL 認証を使用できるのは、エンドポイントを手動で公開して SQL Server インスタンス `master` データベースに接続する場合のみです。
- ビッグ データ クラスターが展開されるときに、高可用性構成が作成される必要があります。 展開後に可用性グループで高可用性構成を有効にすることはできません。

## <a name="next-steps"></a>次の手順

- ビッグ データ クラスターの展開での構成ファイルの使用について詳しくは、「[Kubernetes に [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]を展開する方法](deployment-guidance.md#configfile)」を参照してください。
- SQL Server の可用性グループの機能について詳しくは、「[Overview of Always On Availability Groups (SQL Server)](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)」 (Always On 可用性グループの概要 (SQL Server)) を参照してください。
