---
title: クラスターの状態を表示する
titleSuffix: SQL Server big data clusters
description: この記事では、Azure Data Studio、ノートブック、および azdata コマンドを使用して、ビッグ データ クラスターの状態を表示する方法について説明します。
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 45cf5461b9154d397ee5365fd275d2545a3cc376
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531588"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>ビッグ データ クラスターの状態を表示する方法 

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

この記事では、サービス エンドポイントにアクセスして SQL Server ビッグ データ クラスター コンポーネントの状態を表示する方法について説明します。 Azure Data Studio と **azdata** の両方を使用できます。この記事では、両方の手法について説明します。

## <a id="datastudio"></a> Azure Data Studio を使用する

[Azure Data Studio](https://aka.ms/getazuredatastudio) の最新の **Insider ビルド**をダウンロードしたら、SQL Server ビッグ データ クラスター ダッシュボードを使用して、サービス エンドポイントとビッグ データ クラスターの状態を表示できます。 以下の機能の一部については、最初は Azure Data Studio の Insider ビルドでのみ使用可能となります。

1. まず、Azure Data Studio でご利用のビッグ データ クラスターへの接続を作成します。 詳細については、「[Azure Data Studio を使用して SQL Server ビッグ データ クラスターに接続する](connect-to-big-data-cluster.md)」を参照してください。

1. ビッグ データ クラスター エンドポイントを右クリックし、 **[管理]** をクリックします。

   ![[管理] を右クリックする](media/view-cluster-status/right-click-manage.png)

1. **[SQL Server Big Data Cluster]\(SQL Server ビッグ データ クラスター\)** タブを選択して、ビッグ データ クラスターのダッシュボードにアクセスします。

   ![ビッグ データ クラスター ダッシュボード](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>サービス エンドポイント

ビッグ データ クラスター内のさまざまなサービスに簡単にアクセスできるようにすることが重要です。 ビッグ データ クラスター ダッシュボードには、サービス エンドポイントを表示してコピーすることを可能にするサービス エンドポイント テーブルが用意されています。

![サービス エンドポイント](media/view-cluster-status/service-endpoints.png)

これらのサービスに接続するためにエンドポイントが必要なときにコピーして貼り付けることができるエンドポイントが、それらのサービスに一覧表示されます。 たとえば、エンドポイントの右側にあるコピー アイコンをクリックして、そのエンドポイントを要求するテキスト ウィンドウに貼り付けることができます。 [クラスターの状態ノートブック](#notebook)を実行するには、クラスター管理サービスのエンドポイントが必要です。

### <a name="dashboards"></a>ダッシュボード

サービス エンドポイント テーブルには、次の項目を監視するためのダッシュボードもいくつか公開されます。

- メトリック (Grafana)
- ログ (Kibana)
- Spark ジョブの監視
- Spark リソースの管理

これらのリンクを直接クリックできます。 これらのダッシュボードにアクセスするときは、認証が必要になります。 メトリックとログのダッシュボードの場合は、環境変数 **AZDATA_USERNAME** と **AZDATA_PASSWORD** を使用して、展開時に設定するコントローラー管理者の資格情報を指定します。 Spark ダッシュボードでは、AD に統合されたクラスターの AD ID、またはクラスター内で基本認証を使用している場合は、ユーザー **ルート**および **AZDATA_PASSWORD** というゲートウェイ (Knox) 資格情報が使用されます。 

### <a id="notebook"></a> クラスターの状態ノートブック

1. クラスターの状態ノートブックを起動して、ビッグ データ クラスターのクラスターの状態を表示することもできます。 ノートブックを起動するには、 **[クラスターの状態]** タスクをクリックします。

    ![起動する](media/view-cluster-status/cluster-status-launch.png)

2. 開始する前に、次の項目が必要です。

    - ビッグ データのクラスター名
    - コントローラーのユーザー名
    - コントローラーのパスワード
    - コントローラー エンドポイント

    既定のビッグ データ クラスター名は、展開時にカスタマイズしない限り、**mssql-cluster** となります。 コントローラー エンドポイントは、サービス エンドポイント テーブル内のビッグ データ クラスター ダッシュボードから見つけることができます。 エンドポイントは、**クラスター管理サービス**として一覧表示されます。 資格情報がわからない場合は、ご利用のクラスターを展開した管理者に問い合わせてください。

3. 上部のツールバーで **[セルの実行]** をクリックします。

4. ご利用の資格情報を求めるプロンプトに従います。 ビッグ データのクラスター名、コントローラーのユーザー名、コントローラーのパスワードの各資格情報を入力したら、Enter キーを押します。

    > [!Note]
    > ご利用のビッグ データを使用して設定された構成ファイルがない場合は、コントローラー エンドポイントの指定を求められます。 それを入力するか貼り付けてから、Enter キーを押して続行します。

5. 正常に接続された場合、ノートブックの残りの部分には、ビッグ データ クラスターの各コンポーネントの出力が表示されます。 特定のコード セルを再実行する場合は、コード セル上にマウス ポインターを移動し、 **[実行]** アイコンをクリックします。

## <a name="use-azdata"></a>azdata を使用する

[azdata](deploy-install-azdata.md) コマンドを使用して、エンドポイントとクラスターの状態の両方を表示することもできます。

### <a name="service-endpoints"></a>サービス エンドポイント

1. [azdata login](reference-azdata.md) を使用して、ビッグ データ クラスターにログインします。 **--controller-endpoint** パラメーターをコントローラー エンドポイントの外部 IP アドレスに設定します。

   ```bash
   azdata login --endpoint https://<ip-address-of-controller-svc-external>:30080 --username <user-name>
   ```

   展開中にコントローラー (AZDATA_USERNAME と AZDATA_PASSWORD) に対して構成したユーザー名とパスワードを指定します。 
   AD 認証の場合、コマンドは次のようになります。

  ```bash
   azdata login --endpoint https://<control_domain_name>:30080 --auth ad
   ```

1. [`azdata bdc endpoint list`](reference-azdata-bdc-endpoint.md) を実行して、各エンドポイントの説明と、それに対応する IP アドレスとポート値を示した一覧を取得します。 

   ```bash
   azdata bdc endpoint list -o table
   ```

   次の一覧は、このコマンドからの出力例を示しています。

   ```output
   Description                                             Endpoint                                                   Ip              Name               Port    Protocol
   ------------------------------------------------------  ---------------------------------------------------------  --------------  -----------------  ------  ----------
   Gateway to access HDFS files, Spark                     https://11.111.111.111:30443                               11.111.111.111  gateway            30443   https
   Spark Jobs Management and Monitoring Dashboard          https://11.111.111.111:30443/gateway/default/sparkhistory  11.111.111.111  spark-history      30443   https
   Spark Diagnostics and Monitoring Dashboard              https://11.111.111.111:30443/gateway/default/yarn          11.111.111.111  yarn-ui            30443   https
   Application Proxy                                       https://11.111.111.111:30778                               11.111.111.111  app-proxy          30778   https
   Management Proxy                                        https://11.111.111.111:30777                               11.111.111.111  mgmtproxy          30777   https
   Log Search Dashboard                                    https://11.111.111.111:30777/kibana                        11.111.111.111  logsui             30777   https
   Metrics Dashboard                                       https://11.111.111.111:30777/grafana                       11.111.111.111  metricsui          30777   https
   Cluster Management Service                              https://11.111.111.111:30080                               11.111.111.111  controller         30080   https
   SQL Server Master Instance Front-End                    11.111.111.111,31433                                       11.111.111.111  sql-server-master  31433   tcp
   HDFS File System Proxy                                  https://11.111.111.111:30443/gateway/default/webhdfs/v1    11.111.111.111  webhdfs            30443   https
   Proxy for running Spark statements, jobs, applications  https://11.111.111.111:30443/gateway/default/livy/v1       11.111.111.111  livy               30443   https
   ```

### <a name="view-cluster-status"></a>クラスターの状態を表示する

[`azdata bdc status show`](reference-azdata-bdc-status.md) コマンドを使用して、クラスターの状態を表示できます。

```bash
azdata bdc status show
```

> [!TIP]
> status コマンドを実行するには、最初に、前述のエンドポイントのセクションに示した **azdata login** コマンドを使ってログインする必要があります。

このコマンドからの出力例を、次に示します。

```output
 Bdc: ready                                                                                                                                                                                                          Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Services: ready                                                                                                                                                                                                     Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Servicename    State    Healthstatus    Details

 spark          ready    healthy         -
 sql            ready    healthy         -
 hdfs           ready    healthy         -
 control        ready    healthy         -
 gateway        ready    healthy         -
 app            ready    healthy         -


 Spark Services: ready                                                                                                                                                                                               Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 sparkhead       ready    healthy         StatefulSet sparkhead is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Sql Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 master          ready    healthy         StatefulSet master is healthy
 compute-0       ready    healthy         StatefulSet compute-0 is healthy
 data-0          ready    healthy         StatefulSet data-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Hdfs Services: ready                                                                                                                                                                                                Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 nmnode-0        ready    healthy         StatefulSet nmnode-0 is healthy
 zookeeper       ready    healthy         StatefulSet zookeeper is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy
 sparkhead       ready    healthy         StatefulSet sparkhead is healthy


 Control Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 controldb       ready    healthy         StatefulSet controldb is healthy
 control         ready    healthy         ReplicaSet control is healthy
 metricsdc       ready    healthy         DaemonSet metricsdc is healthy
 metricsui       ready    healthy         ReplicaSet metricsui is healthy
 metricsdb       ready    healthy         StatefulSet metricsdb is healthy
 logsui          ready    healthy         ReplicaSet logsui is healthy
 logsdb          ready    healthy         StatefulSet logsdb is healthy
 mgmtproxy       ready    healthy         ReplicaSet mgmtproxy is healthy
 controlwd       ready    healthy         ReplicaSet controlwd is healthy


 Gateway Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 gateway         ready    healthy         StatefulSet gateway is healthy


 App Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 appproxy        ready    healthy         ReplicaSet appproxy is healthy
```

### <a name="view-specific-resource-status"></a>特定のリソースの状態を表示する

[azdata bdc status show](reference-azdata-bdc-status.md) コマンドを使用して、クラスター内の特定のリソースの状態を表示できます。 このコマンドを使用すると、`--resource` パラメーターを使用してフィルター処理できます。 `--resource` パラメーターの入力の例を次にいくつか示します。

- master
- control
- compute-0
- storage-0
- gateway

たとえば、次のコマンドを実行すると、ストレージ プールの状態が表示されます。

```bash
azdata bdc status show --all --resource storage-0
```

特定のサービスを実行しているすべてのコンポーネントの状態を表示するには、対応するコマンドグループ `azdata bdc <serviceName> status show` を使用する必要があります。 例:

- azdata bdc sql status show --all
- azdata bdc hdfs status show --all
- azdata bdc spark status show --all

サンプル出力を次に示します。

```output
  Storage-0: ready                                                                                                                                                                                                    Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Instances: running                                                                                                                                                                                                  Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Instancename    State    Healthstatus    Details

 storage-0-0     running  healthy         Pod storage-0-0 is healthy
 storage-0-1     running  healthy         Pod storage-0-1 is healthy


 Dashboards
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Name            Url

 nodeMetricsUrl  https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/nodemetrics/ui
 sqlMetricsUrl   https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/sqlmetrics/ui
 logsUrl         https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/logs/ui
 ```

> [!TIP]
> 特定のインスタンスに対応するメトリックとログ ダッシュボードへのリンクなど、追加の正常性の詳細については、`--all` パラメーターを使用して status コマンドを実行します。 `--all` パラメーターを使用した場合のサンプル出力を次に示します。

```output
 Spark: ready                                                                                                                                                                                                        Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Resources: ready                                                                                                                                                                                                    Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 sparkhead       ready    healthy         StatefulSet sparkhead is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Sparkhead Resources: running                                                                                                                                                                                        Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Instancename    State    Healthstatus    Details

 sparkhead-0     running  healthy         Pod sparkhead-0 is healthy
 sparkhead-1     running  healthy         Pod sparkhead-1 is healthy


      Dashboards
      --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
      Name            Url

      nodeMetricsUrl  https://13.91.50.9:30777/api/v1/bdc/instances/sparkhead-1/status/nodemetrics/ui
      sqlMetricsUrl   https://13.91.50.9:30777/api/v1/bdc/instances/sparkhead-1/status/sqlmetrics/ui
      logsUrl         https://13.91.50.9:30777/api/v1/bdc/instances/sparkhead-1/status/logs/ui


 Storage-0 Resources: running                                                                                                                                                                                        Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Instancename    State    Healthstatus    Details

 storage-0-0     running  healthy         Pod storage-0-0 is healthy
 storage-0-1     running  healthy         Pod storage-0-1 is healthy


      Dashboards
      --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
      Name            Url

      nodeMetricsUrl  https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/nodemetrics/ui
      sqlMetricsUrl   https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/sqlmetrics/ui
      logsUrl         https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/logs/ui
```

`logsUrl` 値は、次の kibana ダッシュボードにリンクされます。

![Kibana ダッシュボード](./media/view-cluster-status/kibana-dashboard.png)

> [!NOTE]
> 古い Microsoft Edge ブラウザー ios と Kibana との互換性がありません。ダッシュボードを正しく表示するには、chromium ベースのブラウザーを使用する必要があります。 サポートされていないブラウザーを使用してダッシュボードを読み込むと、空のページが表示されます。 Kibana.rs でサポートされるブラウザーについては、こちらを参照してください。

`nodeMetricsUrl` と `sqlMetricsUrl` の値は、Kubernetes ノードのメトリックとビッグ データ クラスターのサービス メトリックを監視するための Grafana ダッシュボードにリンクされています。

![grafana ダッシュボード](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>コントローラーの状態を表示する

[`azdata bdc control status show`](reference-azdata-bdc-control-status.md) コマンドを使用して、コントローラーの状態を表示できます。 ビッグ データ クラスターのコントローラー コンポーネントに関連する監視ダッシュボードへの同様のリンクが表示されます。

## <a name="next-steps"></a>次の手順

ビッグ データ クラスターの詳細については、[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] とは](big-data-cluster-overview.md)の概要に関するページを参照してください。
