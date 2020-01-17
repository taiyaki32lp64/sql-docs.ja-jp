---
title: 監視とトラブルシューティング
titleSuffix: SQL Server big data clusters
description: この記事では、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]の監視とトラブルシューティングに役立つコマンドについて説明します。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e70689d1e4891fefde8fd1feb76b081bc14bfe81
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153633"
---
# <a name="monitoring-and-troubleshoot-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]の監視とトラブルシューティング

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

この記事では、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]の監視とトラブルシューティングに使用できる、いくつかの便利な Kubernetes コマンドについて説明します。 ビッグ データ クラスター内に存在するポッドまたは他の Kubernetes アーティファクトの詳細を表示する方法を示します。 この記事では、SQL Server ビッグ データ クラスター サービスのいずれかが実行されているコンテナーとの間でのファイルのコピーなど、一般的なタスクについても説明します。

> [!TIP]
> ビッグ データ クラスターのコンポーネントの状態を監視するには、[**azdata bdc status**](deployment-guidance.md#status) のコマンドを使用するか、Azure Data Studio に組み込まれている[トラブルシューティングのノートブック](manage-notebooks.md)を使用します。

> [!TIP]
> Windows (cmd または PS) または Linux (bash) のクライアント コンピューターで、次の **kubectl** コマンドを実行します。 それらには、クラスターでの以前の認証と、実行対象のクラスター コンテキストが必要です。 たとえば、以前に作成された AKS クラスターでは、`az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>` を実行して Kubernetes クラスター構成ファイルをダウンロードし、クラスター コンテキストを設定できます。

## <a name="get-status-of-pods"></a>ポッドの状態を取得する

`kubectl get pods` コマンドを使用して、クラスター内のすべての名前空間またはビッグ データ クラスターの名前空間のポッドの状態を取得できます。 次のセクションでは、両方の例を示します。

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>Kubernetes クラスター内のすべてのポッドの状態を表示する

すべてのポッドとその状態を取得するには、次のコマンドを実行します。これには、SQL Server ビッグ データ クラスターのポッドが作成された名前空間の一部であるポッドも含まれます。

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>SQL Server ビッグ データ クラスター内のすべてのポッドの状態を表示する

特定の名前空間を指定するには、`-n` パラメーターを使います。 SQL Server ビッグ データ クラスターのポッドは、展開構成ファイルで指定されているクラスター名に基づいて、クラスターのブートストラップ時に作成される新しい名前空間に作成されることに注意してください。 ここでは、既定の名前 `mssql-cluster` を使います。

```bash
kubectl get pods -n mssql-cluster
```

実行されているビッグ データ クラスターについて、次のような出力が表示されます。

```output
PS C:\> kubectl get pods -n mssql-cluster
NAME              READY   STATUS    RESTARTS   AGE
appproxy-f2qqt    2/2     Running   0          110m
compute-0-0       3/3     Running   0          110m
control-zlncl     4/4     Running   0          118m
data-0-0          3/3     Running   0          110m
data-0-1          3/3     Running   0          110m
gateway-0         2/2     Running   0          109m
logsdb-0          1/1     Running   0          112m
logsui-jtdnv      1/1     Running   0          112m
master-0          7/7     Running   0          110m
metricsdb-0       1/1     Running   0          112m
metricsdc-shv2f   1/1     Running   0          112m
metricsui-9bcj7   1/1     Running   0          112m
mgmtproxy-x6gcs   2/2     Running   0          112m
nmnode-0-0        1/1     Running   0          110m
storage-0-0       7/7     Running   0          110m
storage-0-1       7/7     Running   0          110m
```

> [!NOTE]
> 展開が行われている間、 **[STATUS]** が **[ContainerCreating]** のポッドはまだ起動中です。 何らかの理由で展開がハングする場合、これにより問題がある可能性のある場所についての情報が得られることがあります。 また、 **[READY]** 列も確認してください。 これにより、ポッドで開始されたコンテナーの数がわかります。 構成とネットワークによっては、展開に 30 分以上かかる場合があることに注意してください。 この時間の多くは、さまざまなコンポーネントのコンテナー イメージのダウンロードに費やされます。

## <a name="get-pod-details"></a>ポッドの詳細を取得する

特定のポッドの詳細な説明を JSON 形式の出力で取得するには、次のコマンドを実行します。 これには、ポッドが現在配置されている Kubernetes ノード、ポッド内で実行されているコンテナー、コンテナーのブートストラップに使われたイメージなどの詳細が含まれます。 また、ポッドに関連付けられているラベル、状態、永続化ボリューム要求など、その他の詳細も表示されます。

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

次の例では、`mssql-cluster` という名前のビッグ データ クラスター内の `master-0` ポッドの詳細が示されます。

```bash
kubectl describe pod  master-0 -n mssql-cluster
```

何らかのエラーが発生した場合、ポッドに対する最近のイベントでエラーを確認できることがあります。

## <a name="get-pod-logs"></a>ポッドのログを取得する

ポッドで実行されているコンテナーのログを取得できます。 次のコマンドでは、`master-0` という名前のポッドで実行されているすべてのコンテナーのログが取得されて、ファイル名 `master-0-pod-logs.txt` に出力されます。

```bash
kubectl logs master-0 --all-containers=true -n mssql-cluster > master-0-pod-logs.txt
```

## <a id="services"></a> サービスの状態を取得する

ビッグ データ クラスター サービスの詳細を取得するには、次のコマンドを実行します。 これらの詳細には、それらの種類と、それぞれのサービスおよびポートに関連付けられている IP アドレスが含まれます。 SQL Server ビッグ データ クラスターのサービスは、展開構成ファイルで指定されているクラスター名に基づいて、クラスターのブートストラップ時に作成される新しい名前空間に作成されることに注意してください。

```bash
kubectl get svc -n <namespace_name>
```

次の例では、`mssql-cluster` という名前のビッグ データ クラスター内のサービスの詳細が示されます。

```bash
kubectl get svc -n mssql-cluster
```

次のサービスでは、ビッグ データ クラスターへの外部接続がサポートされています。

| サービス | [説明] |
|---|---|
| **master-svc-external** | マスター インスタンスへのアクセスが提供されます。<br/>(**EXTERNAL-IP,31433** および **SA** ユーザー) |
| **controller-svc-external** | クラスターを管理するツールとクライアントがサポートされます。 |
| **gateway-svc-external** | HDFS/Spark ゲートウェイへのアクセスが提供されます。<br/>(**EXTERNAL-IP** および **root** ユーザー) |
| **appproxy-svc-external** | アプリケーション展開シナリオがサポートされます。 |

> [!TIP]
> これは **kubectl** を使ってサービスを表示する方法ですが、`azdata bdc endpoint list` コマンドを使ってこれらのエンドポイントを表示することもできます。 詳しくは、[ビッグ データ クラスターのエンドポイントの取得](deployment-guidance.md#endpoints)に関する記事をご覧ください。

## <a name="get-service-details"></a>サービスの詳細を取得する

サービスの詳細な説明を JSON 形式の出力で取得するには、このコマンドを実行します。 それには、ラベル、セレクター、IP アドレス、外部 IP アドレス (サービスの種類が LoadBalancer の場合)、ポートなどの詳細が含まれます。

```bash
kubectl describe service <service_name> -n <namespace_name>
```

次の例では、**master-svc-external** サービスの詳細が取得されます。

```bash
kubectl describe service master-svc-external -n mssql-cluster
```

## <a id="copy"></a> ファイルをコピーする

コンテナーからローカル コンピューターにファイルをコピーする必要がある場合は、次の構文で `kubectl cp` コマンドを使います。

```bash
kubectl cp <pod_name>:<source_file_path> -c <container_name> -n <namespace_name> <target_local_file_path>
```

同様に、`kubectl cp` を使って、ローカル コンピューターから特定のコンテナーにファイルをコピーすることもできます。

```bash
kubectl cp <source_local_file_path> <pod_name>:<target_container_path> -c <container_name>  -n <namespace_name>
```

### <a id="copyfrom"></a> コンテナーからファイルをコピーする

次の例では、SQL Server のログ ファイルが、コンテナーからローカル コンピューター上の `~/temp/sqlserverlogs` パスにコピーされます (この例では、ローカル コンピューターは Linux クライアントです)。

```bash
kubectl cp master-0:/var/opt/mssql/log -c mssql-server -n mssql-cluster ~/tmp/sqlserverlogs
```

### <a id="copyinto"></a> コンテナーにファイルをコピーする

次の例では、**AdventureWorks2016CTP3.bak** ファイルが、ローカル コンピューターから `master-0` ポッド内の SQL Server マスター インスタンス コンテナー (`mssql-server`) にコピーされます。 ファイルは、コンテナー内の `/tmp` ディレクトリにコピーされます。 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n mssql-cluster
```

## <a id="forcedelete"></a> ポッドを強制的に削除する
 
ポッドを強制的に削除することはお勧めしません。 ただし、可用性、回復性、またはデータの永続性をテストする場合は、`kubectl delete pods` コマンドでポッドを削除してポッドの障害をシミュレートできます。

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

次の例では、記憶域プールのポッド `storage-0-0` が削除されます。

```bash
kubectl delete pods storage-0-0 -n mssql-cluster --grace-period=0 --force
```

## <a id="getip"></a> ポッドの IP アドレスを取得する
 
トラブルシューティングのために、ポッドが現在実行されているノードの IP アドレスを取得することが必要になる場合があります。 IP アドレスを取得するには、次の構文で `kubectl get pods` コマンドを使います。

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

次の例では、`master-0` ポッドが実行されているノードの IP アドレスが取得されます。

```bash
kubectl get pods master-0 -o yaml -n mssql-cluster | grep hostIP
```

## <a name="kubernetes-dashboard"></a>Kubernetes ダッシュボード

Kubernetes ダッシュボードを起動して、クラスターに関する追加情報を確認できます。 以下のセクションでは、AKS 上の Kubernetes および kubeadm を使ってブートストラップされた Kubernetes のダッシュボードを起動する方法について説明します。
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>クラスターが AKS で実行されているときにダッシュボードを開始する

Kubernetes ダッシュボードを起動するには、以下を実行します。

```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> 次のエラーが発生する場合: *Unable to listen on port 8001: All listeners failed to create with the following errors: Unable to create listener: Error listen tcp4 127.0.0.1:8001: >bind: Only one usage of each socket address (protocol/network address/port) is normally permitted. Unable to create listener: Error listen tcp6: address [[::1]]:8001: missing port in >address error: Unable to listen on any of the requested ports: [{8001 9090}]* (ポート 8001 でリッスンできません: すべてのリスナーが次のエラーで作成できませんでした: リッスン エラー tcp4 127.0.0.1:8001: >bind: 通常、各ソケット アドレスに対してプロトコル、ネットワーク アドレス、またはポートのどれか 1 つのみを使用できます。リスナーを作成できません: リッスン エラー tcp6: アドレス [[::1]]:8001: 不足ポート > アドレス エラー: 要求されたどのポートでもリッスンできません: [{8001 9090}])、別のウィンドウから既にダッシュボードを開始していないことを確認してください。

ブラウザーでダッシュボードを起動すると、AKS クラスターで RBAC が既定で有効になっていて、ダッシュボードで使用されるサービス アカウントにすべてのリソースにアクセスするための十分なアクセス許可がないため、アクセス許可の警告が表示される場合があります (たとえば、*pods is forbidden: User "system:serviceaccount:kube-system:kubernetes-dashboard" cannot list pods in the namespace "default"* (ポッドは禁止されています: ユーザー "system:serviceaccount:kube-system:kubernetes-dashboard" は名前空間 "default" 内のポッドをリストできません))。 次のコマンドを実行して `kubernetes-dashboard` に必要なアクセス許可を付与した後、ダッシュボードを再起動します。

```bash
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>kubeadm を使用して Kubernetes クラスターがブートストラップされたときにダッシュボードを開始する

Kubernetes クラスターでダッシュボードを展開して構成する方法の詳細については、[Kubernetes のドキュメント](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)を参照してください。 Kubernetes ダッシュボードを起動するには、次のコマンドを実行します。

```bash
kubectl proxy
```

## <a name="next-steps"></a>次の手順

ビッグ データ クラスターの詳細については、[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] とは](big-data-cluster-overview.md)の概要に関するページを参照してください。
