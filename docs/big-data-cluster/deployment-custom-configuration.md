---
title: 展開を構成する
titleSuffix: SQL Server big data clusters
description: 構成ファイルを使用してビッグ データ クラスターの展開をカスタマイズする方法について説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f984871729ea1d92b8da3b90751988fc33e741ff
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532040"
---
# <a name="configure-deployment-settings-for-cluster-resources-and-services"></a>クラスター リソースとサービスの展開設定を構成する

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

`azdata` 管理ツールに組み込まれている事前定義された構成プロファイルのセットから開始すると、ご自分の BDC ワークロード要件に合わせて、既定の設定を簡単に変更することができます。 構成ファイルの構造により、リソースの各サービスの設定を詳細に更新することができます。

> [!TIP]
> 高可用性サービスを展開する方法の詳細については、[SQL Server マスター](deployment-high-availability.md)や [HDFS 名前ノード](deployment-high-availability-hdfs-spark.md)などのミッション クリティカルなコンポーネントに対して**高可用性**を構成する方法に関する記事を参照してください。

リソース レベルの構成を設定したり、リソース内のすべてのサービスの構成を更新したりすることもできます。 `bdc.json` の構造の概要を次に示します。

```json
{
    "apiVersion": "v1",
    "metadata": {
        "kind": "BigDataCluster",
        "name": "mssql-cluster"
    },
    "spec": {
        "resources": {
            "nmnode-0": {...
            },
            "sparkhead": {...
            },
            "zookeeper": {...
            },
            "gateway": {...
            },
            "appproxy": {...
            },
            "master": {...
            },
            "compute-0": {...
            },
            "data-0": {...
            },
            "storage-0": {...
        },
        "services": {
            "sql": {
                "resources": [
                    "master",
                    "compute-0",
                    "data-0",
                    "storage-0"
                ]
            },
            "hdfs": {
                "resources": [
                    "nmnode-0",
                    "zookeeper",
                    "storage-0",
                    "sparkhead"
                ],
                "settings": {...
            },
            "spark": {
                "resources": [
                    "sparkhead",
                    "storage-0"
                ],
                "settings": {...
            }
        }
    }
}
```

プール内のインスタンスなどのリソース レベルの構成を更新するには、リソース仕様を更新します。たとえば、コンピューティング プール内のインスタンスの数を更新するには、`bdc.json` 構成ファイルでこのセクションを変更します。

```json
"resources": {
    ...
    "compute-0": {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Compute",
            "replicas": 4
        }
    }
    ...
}
``` 

特定のリソース内の 1 つのサービスの設定の変更も同様に行います。 たとえば、記憶域プール内の Spark コンポーネントに対してのみ Spark メモリの設定を変更する場合は、`bdc.json` 構成ファイルで `spark` サービスの `settings` セクションを使用して、`storage-0` リソースを更新します。

```json
"resources":{
    ...
     "storage-0": {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Storage",
            "replicas": 2,
            "settings": {
                "spark": {
                    "spark-defaults-conf.spark.driver.memory": "2g",
                    "spark-defaults-conf.spark.driver.cores": "1",
                    "spark-defaults-conf.spark.executor.instances": "3",
                    "spark-defaults-conf.spark.executor.memory": "1536m",
                    "spark-defaults-conf.spark.executor.cores": "1",
                    "yarn-site.yarn.nodemanager.resource.memory-mb": "18432",
                    "yarn-site.yarn.nodemanager.resource.cpu-vcores": "6",
                    "yarn-site.yarn.scheduler.maximum-allocation-mb": "18432",
                    "yarn-site.yarn.scheduler.maximum-allocation-vcores": "6",
                    "yarn-site.yarn.scheduler.capacity.maximum-am-resource-percent": "0.3"
                }
            }
        }
    }
    ...
}
```

複数のリソースに関連付けられているサービスに対して同じ構成を適用する場合は、`services` セクションで対応する `settings` を更新します。 たとえば、記憶域プールと Spark プールの両方で Spark に同じ設定を設定する場合は、`bdc.json` 構成ファイルの `spark` サービス セクションの `settings` セクションを更新します。

```json
"services": {
    ...
    "spark": {
        "resources": [
            "sparkhead",
            "storage-0"
        ],
        "settings": {
            "spark-defaults-conf.spark.driver.memory": "2g",
            "spark-defaults-conf.spark.driver.cores": "1",
            "spark-defaults-conf.spark.executor.instances": "3",
            "spark-defaults-conf.spark.executor.memory": "1536m",
            "spark-defaults-conf.spark.executor.cores": "1",
            "yarn-site.yarn.nodemanager.resource.memory-mb": "18432",
            "yarn-site.yarn.nodemanager.resource.cpu-vcores": "6",
            "yarn-site.yarn.scheduler.maximum-allocation-mb": "18432",
            "yarn-site.yarn.scheduler.maximum-allocation-vcores": "6",
            "yarn-site.yarn.scheduler.capacity.maximum-am-resource-percent": "0.3"
        }
    }
    ...
}
```

クラスターの展開構成ファイルをカスタマイズするには、VSCode など、任意の JSON 形式エディターを使用できます。 自動化のためにこれらの編集をスクリプト化するには、`azdata bdc config` コマンドを使用します。 この記事では、展開構成ファイルを変更してビッグ データ クラスターの展開を構成する方法について説明します。 さまざまなシナリオについて構成の変更方法の例を示します。 展開に構成ファイルを使用する方法の詳細詳細については、「[展開のガイダンス](deployment-guidance.md#configfile)」を参照してください。

## <a name="prerequisites"></a>Prerequisites

- [azdata をインストールします](deploy-install-azdata.md)。

- このセクションの各例では、標準構成のいずれかのコピーを作成済みであることを前提としています。 詳細については、[カスタム構成の作成](deployment-guidance.md#customconfig)に関する記事を参照してください。 たとえば、次のコマンドでは、既定値の `aks-dev-test` 構成に基づいて、2 つの JSON 展開構成ファイル (`bdc.json` と `control.json`) を含む `custom-bdc` というディレクトリが作成されます。

   ```bash
   azdata bdc config init --source aks-dev-test --target custom-bdc
   ```

## <a id="docker"></a> 既定の Docker レジストリ、リポジトリ、およびイメージ タグを変更する

組み込みの構成ファイル (具体的には、control. json) には、`docker` セクションが含まれており、ここでコンテナー レジストリ、リポジトリ、およびイメージ タグが事前に設定されます。 既定では、ビッグ データ クラスターに必要なイメージは、`mssql/bdc` リポジトリ内の Microsoft Container Registry (`mcr.microsoft.com`) にあります。

```json
{
    "apiVersion": "v1",
    "metadata": {
        "kind": "Cluster",
        "name": "mssql-cluster"
    },
    "spec": {
        "docker": {
            "registry": "mcr.microsoft.com",
            "repository": "mssql/bdc",
            "imageTag": "2019-GDR1-ubuntu-16.04",
            "imagePullPolicy": "Always"
        },
        ...
    }
}
```

展開する前に、`control.json` 構成ファイルを直接編集するか `azdata bdc config` コマンドを使用して、`docker` 設定をカスタマイズできます。 たとえば、次のコマンドでは、異なる `<registry>`、`<repository>`、`<image_tag>` を使用して、`custom-bdc` control.json 構成ファイルを更新しています。

```bash
azdata bdc config replace -c custom-bdc/control.json -j "$.spec.docker.registry=<registry>"
azdata bdc config replace -c custom-bdc/control.json -j "$.spec.docker.repository=<repository>"
azdata bdc config replace -c custom-bdc/control.json -j "$.spec.docker.imageTag=<image_tag>"
```

> [!TIP]
> ベスト プラクティスとして、バージョン固有のイメージ タグを使用して、`latest` イメージ タグの使用を避ける必要があります。これによりクラスターの正常性の問題の原因となるバージョンの不一致が発生する可能性があるためです。

> [!TIP]
> ビッグ データ クラスターの展開には、コンテナー レジストリと、コンテナー イメージをプルするリポジトリへのアクセス権が必要です。 ご使用の環境に既定の Microsoft Container Registry へのアクセス権がない場合は、必要なイメージが最初にプライベート Docker リポジトリに配置されるオフライン インストールを実行できます。 オフライン インストールの詳細については、「[SQL Server ビッグ データ クラスターのオフライン展開を実行する](deploy-offline.md)」を参照してください。 展開ワークフローでイメージをプルする元となるプライベート リポジトリにアクセスできるように、`DOCKER_USERNAME` と `DOCKER_PASSWORD` [環境変数](deployment-guidance.md#env)は、展開を発行する前に設定する必要があることに注意してください。

## <a id="clustername"></a> クラスター名を変更する

クラスター名は、ビッグ データ クラスターと、展開時に作成される Kubernetes 名前空間の両方の名前です。 これは `bdc.json` 展開構成ファイルの次の部分で指定されます。

```json
"metadata": {
    "kind": "BigDataCluster",
    "name": "mssql-cluster"
},
```

次のコマンドでは、キーと値のペアを `--json-values` パラメーターに送信し、ビッグ データ クラスター名を `test-cluster` に変更します。

```bash
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> ビッグ データ クラスターの名前は、小文字の英数字のみを使用し、スペースを含めない必要があります クラスターのすべての Kubernetes 成果物 (コンテナー、ポッド、ステートフル セット、サービス) は、指定したクラスター名と同じ名前の名前空間に作成されます。

## <a id="ports"></a> エンドポイント ポートを更新する

エンドポイントは、`control.json` のコントローラー用と、`bdc.json` の対応するセクションのゲートウェイと SQL Server マスター インスタンス用に定義されます。 `control.json` 構成ファイルの次の部分は、コントローラーのエンドポイント定義を示しています。

```json
{
  "endpoints": [
    {
      "name": "Controller",
      "serviceType": "LoadBalancer",
      "port": 30080
    },
    {
      "name": "ServiceProxy",
      "serviceType": "LoadBalancer",
      "port": 30777
    }
  ]
}
```

次の例では、インライン JSON を使用して `controller` エンドポイントのポートを変更します。

```bash
azdata bdc config replace --config-file custom-bdc/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> スケールを構成する

各リソース (記憶域プールなど) の構成は、`bdc.json` 構成ファイルで定義されます。 たとえば、`bdc.json` の次の部分は、`storage-0` リソース定義を示しています。

```json
"storage-0": {
    "metadata": {
        "kind": "Pool",
        "name": "default"
    },
    "spec": {
        "type": "Storage",
        "replicas": 2,
        "settings": {
            "spark": {
                "spark-defaults-conf.spark.driver.memory": "2g",
                "spark-defaults-conf.spark.driver.cores": "1",
                "spark-defaults-conf.spark.executor.instances": "3",
                "spark-defaults-conf.spark.executor.memory": "1536m",
                "spark-defaults-conf.spark.executor.cores": "1",
                "yarn-site.yarn.nodemanager.resource.memory-mb": "18432",
                "yarn-site.yarn.nodemanager.resource.cpu-vcores": "6",
                "yarn-site.yarn.scheduler.maximum-allocation-mb": "18432",
                "yarn-site.yarn.scheduler.maximum-allocation-vcores": "6",
                "yarn-site.yarn.scheduler.capacity.maximum-am-resource-percent": "0.3"
            }
        }
    }
}
```

記憶域プール、コンピューティング プール、またはデータ プール内のインスタンスの数を構成するには、各プールの `replicas` 値を変更します。 次の例では、インライン JSON を使用して、記憶域プール、コンピューティング プール、およびデータ プールのこれらの値をそれぞれ `10`、`4`、`4` に変更します。

```bash
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "$.spec.resources.storage-0.spec.replicas=10"
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "$.spec.resources.compute-0.spec.replicas=4"
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "$.spec.resources.data-0.spec.replicas=4"
```

> [!NOTE]
> コンピューティング プールとデータ プールで検証済みのインスタンスの最大数は、それぞれ `8` です。 この制限は展開時には適用されませんが、運用環境の展開では、これより大きいスケールを構成することはお勧めできません。

## <a id="storage"></a> 記憶域を構成する

各プールに使用される記憶域クラスと特性を変更することもできます。 次の例では、カスタム記憶域クラスを記憶域プールとデータ プールに割り当て、データを格納するための永続ボリューム要求のサイズを HDFS (記憶域プール) 用に 500 Gb、データ プール用に 100 Gb に更新します。 

> [!TIP]
> 記憶域構成の詳細については、「[Kubernetes 上の SQL Server ビッグ データ クラスターでのデータ永続化](concept-data-persistence.md)」を参照してください。

まず、次のように、*type* と *replicas* に加えて新しい *storage* セクションを含む patch.json ファイルを作成します

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.resources.storage-0.spec",
      "value": {
        "type": "Storage",
        "replicas": 2,
        "storage": {
          "data": {
            "size": "500Gi",
            "className": "myHDFSStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myHDFSStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.data-0.spec",
      "value": {
        "type": "Data",
        "replicas": 2,
        "storage": {
          "data": {
            "size": "100Gi",
            "className": "myDataStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myDataStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    }
  ]
}
```

後で `azdata bdc config patch` コマンドを使用して、`bdc.json` 構成ファイルを更新できます。
```bash
azdata bdc config patch --config-file custom-bdc/bdc.json --patch ./patch.json
```

> [!NOTE]
> `kubeadm-dev-test` に基づく構成ファイルには、各プールの記憶域の定義はありませんが、必要に応じて上のプロセスを使用して追加できます。

## <a id="sparkstorage"></a> Spark を使用せずに記憶域プールを構成する

また、Spark を使用せずに実行し、別の Spark プールを作成するように記憶域プールを構成することもできます。 この構成により、記憶域に依存せず、Spark コンピューティングの機能をスケーリングすることができます。 Spark プールを構成する方法については、この記事の「[Spark プールを作成する](#sparkpool)」セクションを参照してください。

> [!NOTE]
> Spark を使用せずにビッグ データ クラスターを展開することはサポートされていません。 そのため、`includeSpark` を `true` に設定するか、少なくとも 1 つのインスタンスを持つ別個の [Spark プール](#sparkpool) を作成する必要があります。 また、Spark を記憶域プール (`includeSpark` は `true`) と、別の Spark プールの両方で実行させることもできます。

既定では、記憶域プール リソースの `includeSpark` 設定は true に設定されているため、変更するには記憶域の構成の `includeSpark` フィールドを編集する必要があります。 次のコマンドは、インライン json を使用してこの値を編集する方法を示しています。

```bash
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "$.spec.resources.storage-0.spec.settings.spark.includeSpark=false"
```

## <a id="sparkpool"></a> Spark プールを作成する

Spark プールは、追加で作成することも、記憶域プールで実行される Spark インスタンスの代わりに作成することもできます。 次の例では、`bdc.json` 構成ファイルに修正プログラムを適用して、2 つのインスタンスを持つ Spark プールを作成する方法を示します。 

まず、次のように `spark-pool-patch.json` ファイルを作成します。

```json
{
    "patch": [
        {
            "op": "add",
            "path": "spec.resources.spark-0",
            "value": {
                "metadata": {
                    "kind": "Pool",
                    "name": "default"
                },
                "spec": {
                    "type": "Spark",
                    "replicas": 2
                }
            }
        },
        {
            "op": "add",
            "path": "spec.services.spark.resources/-",
            "value": "spark-0"
        },
        {
            "op": "add",
            "path": "spec.services.hdfs.resources/-",
            "value": "spark-0"
        }
    ]
}
```

次に、`azdata bdc config patch` コマンドを実行します。

```bash
azdata bdc config patch -c custom-bdc/bdc.json -p spark-pool-patch.json
```

## <a id="podplacement"></a> Kubernetes ラベルを使用してポッドの配置を構成する

Kubernetes ノード上で特定のリソースを持つポッドの配置を制御することで、さまざまな種類のワークロード要件に対応できます。 Kubernetes ラベルを使用すると、ご使用の Kubernetes クラスター内のどのノードがビッグ データ クラスター リソースの展開に使用されるかをカスタマイズできますが、特定のリソースに使用されるノードも制限されます。
たとえば、記憶域プール ポッドがより多くの記憶域があるノードに確実に配置されるようにする一方で、SQL Server マスター インスタンスをより多くの CPU およびメモリ リソースがあるノードに配置することができます。 この場合、まず異なる種類のハードウェアが混在する Kubernetes クラスターを構築してから、それに応じて[ノード ラベルを割り当てます](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)。 ビッグ データ クラスターの展開時に、クラスター レベルで同じラベルを指定して、`control.json` ファイルの `clusterLabel` 属性を使用してビッグ データ クラスターに使用されるノードを示すことができます。 その結果、別のラベルがプール レベルの配置に使用されます。 これらのラベルは、`nodeLabel` 属性を使用して、ビッグ データ クラスターの展開構成ファイルで指定できます。 Kubernetes により、指定されたラベルと一致するノードのポッドが割り当てられます。 Kubernetes クラスター内のノードに追加する必要がある特定のラベル キーは、`mssql-cluster` (ビッグ データ クラスターに使用されるノードを示すため) と `mssql-resource` (さまざまなリソースに対してポッドが配置される特定のノードを示すため) です。 これらのラベルの値には、任意の文字列を指定できます。

> [!NOTE]
> ノード レベルのメトリックを収集するポッドの性質により、`metricsdc` ポッドは、`mssql-cluster` ラベルを持つすべてのノードに展開されます。`mssql-resource` はこれらのポッドには適用されません。

次の例では、ビッグ データ クラスター全体のノード ラベル `bdc`、特定のノードに SQL Server マスター インスタンス ポッドを配置するためのラベル `bdc-master`、記憶域プール リソースの `bdc-storage-pool`、コンピューティング プールとデータ プール ポッドの `bdc-compute-pool`、残りのリソースの `bdc-shared` を含めるように、カスタム構成ファイルを編集する方法を示します。 

まず、Kubernetes ノードにラベルを付けます。

```bash
kubectl label node <kubernetesNodeName1> mssql-cluster=bdc mssql-resource=bdc-shared --overwrite=true
kubectl label node <kubernetesNodeName2> mssql-cluster=bdc mssql-resource=bdc-master --overwrite=true
kubectl label node <kubernetesNodeName3> mssql-cluster=bdc mssql-resource=bdc-compute-pool --overwrite=true
kubectl label node <kubernetesNodeName4> mssql-cluster=bdc mssql-resource=bdc-compute-pool --overwrite=true
kubectl label node <kubernetesNodeName5> mssql-cluster=bdc mssql-resource=bdc-storage-pool --overwrite=true
kubectl label node <kubernetesNodeName6> mssql-cluster=bdc mssql-resource=bdc-storage-pool --overwrite=true
kubectl label node <kubernetesNodeName7> mssql-cluster=bdc mssql-resource=bdc-storage-pool --overwrite=true
kubectl label node <kubernetesNodeName8> mssql-cluster=bdc mssql-resource=bdc-storage-pool --overwrite=true
```

次に、クラスターの展開構成ファイルを更新して、ラベルの値を含めます。 この例では、`custom-bdc` プロファイルの構成ファイルをカスタマイズしていることを前提としています。 既定では、組み込みの構成には `nodeLabel` キーと `clusterLabel` キーがないため、カスタム構成ファイルを手動で編集するか、`azdata bdc config add` コマンドを使用して必要な編集を行う必要があります。

```bash
azdata bdc config add -c custom-bdc/control.json -j "$.spec.clusterLabel=bdc"
azdata bdc config add -c custom-bdc/control.json -j "$.spec.clusterLabel=bdc-shared"

azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.master.spec.nodeLabel=bdc-master"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.compute-0.spec.nodeLabel=bdc-compute-pool"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.data-0.spec.nodeLabel=bdc-compute-pool"
azdata bdc config add -c custom-bdc/bdc.json-j "$.spec.resources.storage-0.spec.nodeLabel=bdc-storage-pool"

# below can be omitted in which case we will take the node label default from the control.json
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.nmnode-0.spec.nodeLabel=bdc-shared"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.sparkhead.spec.nodeLabel=bdc-shared"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.zookeeper.spec.nodeLabel=bdc-shared"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.gateway.spec.nodeLabel=bdc-shared"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.appproxy.spec.nodeLabel=bdc-shared"
```

## <a id="jsonpatch"></a> JSON 修正プログラ ムファイルを使用したその他のカスタマイズ

JSON 修正プログラム ファイルによって、複数の設定が一度で構成されます。 Json 修正プログラムの詳細については、[Python の JSON 修正プログラム](https://github.com/stefankoegl/python-json-patch)と [JSONPath Online Evaluator](https://jsonpath.com/) のページを参照してください。

次の `patch.json` ファイルでは、次の変更が行われます。

- `control.json` で 1 つのエンドポイントのポートを更新します。

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.endpoints[?(@.name=='Controller')].port",
      "value": 30000
    }
  ]
}
```

- `control.json` ですべてのエンドポイント (`port` と `serviceType`) を更新します。

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.endpoints",
      "value": [
        {
          "serviceType": "LoadBalancer",
          "port": 30001,
          "name": "Controller"
        },
        {
          "serviceType": "LoadBalancer",
          "port": 30778,
          "name": "ServiceProxy"
        }
      ]
    }
  ]
}
```

- `control.json` で、コントローラーの記憶域設定を更新します。 これらの設定は、プール レベルで上書きされない限り、すべてのクラスター コンポーネントに適用されます。

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.storage",
      "value": {
        "data": {
          "className": "managed-premium",
          "accessMode": "ReadWriteOnce",
          "size": "100Gi"
        },
        "logs": {
          "className": "managed-premium",
          "accessMode": "ReadWriteOnce",
          "size": "32Gi"
        }
      }
    }
  ]
}
```

- `control.json` で記憶域クラス名を更新します。

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.storage.data.className",
      "value": "managed-premium"
    }
  ]
}
```

- `bdc.json` で、記憶域プールのプール記憶域設定を更新します。

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.resources.storage-0.spec",
      "value": {
        "type": "Storage",
        "replicas": 2,
        "storage": {
          "data": {
            "size": "100Gi",
            "className": "myStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    }
  ]
}
```

- `bdc.json` で、記憶域プールの Spark 設定を更新します。

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.services.spark.settings",
      "value": {
            "spark-defaults-conf.spark.driver.memory": "2g",
            "spark-defaults-conf.spark.driver.cores": "1",
            "spark-defaults-conf.spark.executor.instances": "3",
            "spark-defaults-conf.spark.executor.memory": "1536m",
            "spark-defaults-conf.spark.executor.cores": "1",
            "yarn-site.yarn.nodemanager.resource.memory-mb": "18432",
            "yarn-site.yarn.nodemanager.resource.cpu-vcores": "6",
            "yarn-site.yarn.scheduler.maximum-allocation-mb": "18432",
            "yarn-site.yarn.scheduler.maximum-allocation-vcores": "6",
            "yarn-site.yarn.scheduler.capacity.maximum-am-resource-percent": "0.3"
      }
    }
  ]
}
```

> [!TIP]
> 展開構成ファイルを変更するための構造とオプションの詳細については、「[ビッグ データ クラスターの展開構成ファイル リファレンス](reference-deployment-config.md)」を参照してください。

`azdata bdc config` コマンドを使用して、JSON 修正プログラム ファイルに変更を適用します。 次の例では、`patch.json` ファイルをターゲットの展開構成ファイルである `custom-bdc/bdc.json` に適用します。

```bash
azdata bdc config patch --config-file custom-bdc/bdc.json --patch-file ./patch.json
```

## <a name="disable-elasticsearch-to-run-in-privileged-mode"></a>特権モードで実行するために ElasticSearch を無効にする

既定では、ElasticSearch コンテナーは、ビッグ データ クラスターでは特権モードで実行されます。 この設定により、コンテナーの初期化時に、ElasticSearch がより多くのログを処理するときに必要なホスト上の設定を更新するのに十分なアクセス許可がコンテナーに与えられます。 このトピックの詳細については、[こちらの記事](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html)を参照してください。 

特権モードで実行するために ElasticSearch を実行するコンテナーを無効にするには、`control.json` の `settings` セクションを更新し、`vm.max_map_count` の値を `-1` に指定する必要があります。 このセクションがどのようになるかを示すサンプルを次に示します。

```json
{
    "apiVersion": "v1",
    "metadata": {...},
    "spec": {
        "docker": {...},
        "storage": {...},
        "endpoints": [...],
        "settings": {
            "ElasticSearch": {
                "vm.max_map_count": "-1"
            }
        }
    }
}
```

手動で `control.json` を編集して、上記のセクションを `spec` に追加することができます。または、次のような修正プログラム ファイル `elasticsearch-patch.json` 作成し、`azdata` CLI を使用して `control.json` ファイルに修正プログラムを適用することもできます。

```json
{
  "patch": [
    {
      "op": "add",
      "path": "spec.settings",
      "value": {
            "ElasticSearch": {
                "vm.max_map_count": "-1"
        }
      }
    }
  ]
}
```

次のコマンドを実行して、構成ファイルに修正プログラムを適用します。

```bash
azdata bdc config patch --config-file custom-bdc/control.json --patch-file elasticsearch-patch.json
```

> [!IMPORTANT]
> ペスト プラクティスとして、[この記事](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html)の手順に従って、Kubernetes クラスター内の各ホストで、`max_map_count` 設定を手動で更新することをお勧めします。

## <a name="next-steps"></a>次の手順

ビッグ データ クラスターの展開での構成ファイルの使用について詳しくは、「[Kubernetes に [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]を展開する方法](deployment-guidance.md#configfile)」を参照してください。
